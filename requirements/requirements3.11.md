# AgriForward — Consolidated Requirements (requirements.md)
> **Updated – 24/04/2026**  
> **Version: v3.11 – VAT calculation, suspension deposit handling, GPS validation, penetration testing, re‑auth failure state, subscribe eligibility, server‑time UX, admin force‑cancel double confirmation**

> **Purpose**: This document consolidates **all requirements** from the entire SRS development, subsequent clarifications, risk analysis, and final business decisions. It is exhaustive, unambiguous, and reflects the final agreed-upon design ready for production development.

> **Guarantee**: No requirement discussed or implied so far is omitted. This file is intentionally verbose and atomic.

---

## 0. Global Principles & Baseline Constraints

### AF-GLOBAL-REQ-001 — Deterministic Behavior
The system **shall** behave deterministically for identical inputs, states, and timestamps.

### AF-GLOBAL-REQ-002 — State-Driven Authority
The system **shall** permit behavior exclusively through explicitly defined state transitions.

### AF-GLOBAL-REQ-003 — Irreversibility Enforcement
The system **shall** prevent transitions from irreversible states to any prior state.

### AF-GLOBAL-REQ-004 — Idempotent System Jobs
All background or scheduled jobs **shall** be idempotent.

### AF-GLOBAL-REQ-005 — Deadline Consistency
All deadlines **shall** be evaluated using server-side deterministic timestamps only. The UI **shall** display all countdowns and deadlines based on the server time, with a brief label “ตามเวลาระบบ” to avoid confusion with local device time.

---

## 1. Authentication & Access

### AF-AUTH-REQ-001 — Unified User Role
All regular users **shall** have both Buyer and Seller capabilities enabled on the same account. A single user can create POs, browse POs, submit Offers, and manage logistics from the same account.

### AF-AUTH-REQ-002 — Single Dashboard Interface
The system **shall** provide a single unified dashboard that combines both Buyer and Seller functionality without any mode switching button.

### AF-AUTH-REQ-003 — Admin Role Separation
Only Admin role **shall** be separated as privileged access. No other specialized roles exist.

### AF-AUTH-REQ-004 — Unauthorized Access Rejection
The system **shall** return an authorization error when a user attempts access outside their permission scope.

### AF-AUTH-REQ-005 — Terms of Service & Privacy Policy Acceptance
Before completing registration, every user **shall** be presented with the platform’s Terms of Service and Privacy Policy. The user must explicitly check a box or click an “I Agree” button to indicate acceptance. The acceptance timestamp is recorded and stored in the user’s profile.

---

## 2. Identity Verification (KYC)

### AF-KYC-REQ-001 — Identity Verification Requirement
All users **shall** have the ability to voluntarily complete identity verification. To submit an Offer, a user **must** have completed verification. Verified Buyers receive a **"Verified Buyer" badge**.

### AF-KYC-REQ-002 — Verification Documents
Acceptable documents: Thai national ID card or business registration certificate. Verified by Admin.

### AF-KYC-REQ-003 — Verification Status Display
Verified status is shown via badges on Offers and profiles.

### AF-KYC-REQ-004 — Re-Verification
Admin **shall** be able to request re-verification if suspicious activity is detected.

---

## 3. Purchase Order (PO) Requirements

### PO States (Enumeration)
`DRAFT`, `OPEN`, `LOCKED`, `PAYMENT_IN_PROGRESS`, `AWAITING_SELLER_CONFIRM`, `PAYMENT_PENDING`, `CONTRACT`, `OFF_PLATFORM`, `EXPIRED`, `CANCELLED`.

### AF-PO-REQ-001 — Buyer-Initiated PO Creation
Any user (acting as Buyer) **shall** be able to create a Purchase Order.

### AF-PO-REQ-002 — PO Initial State
A newly created PO **shall** start in the `DRAFT` state.

### AF-PO-REQ-003 — PO Publication
The system **shall** transition a PO from `DRAFT` to `OPEN` only upon explicit publish action by the Buyer.

### AF-PO-REQ-004 — Seller Visibility
`OPEN` POs are visible to all verified users subscribed for the product category.

### AF-PO-REQ-005 — Locking and Unlocking
When the Buyer selects at least one Offer and proceeds to the shipping selection page, the PO transitions to `LOCKED`. In `LOCKED`:
- All associated Offers become immutable by their respective Sellers.
- The Buyer can cancel the PO (→ `CANCELLED`), proceed to shipping selection, or **return to `OPEN`** state.
- If the Buyer returns to `OPEN`, **all current Offer selections are deselected**, all Offers are unlocked, and Sellers are notified. The existing group chat remains active but its members are updated dynamically (see AF-CHAT-REQ-007).
- Transition back to `OPEN` is only allowed from `LOCKED`, not from any later state.
- **Crucially:** The Buyer **cannot** proceed from `LOCKED` to any shipping confirmation unless the logistics API returns a definitive delivery cost. If the API is unavailable, the “Proceed” action is disabled with a clear message (see AF-LOG-REQ-006).

### AF-PO-REQ-006 — Self Pickup Termination (Off-Platform)
When the Buyer selects "Self Pickup" from the shipping selection page (PO is `LOCKED`):
- PO transitions to `OFF_PLATFORM` immediately.
- No payment, no contract.
- Full deposit (10%) returned to all selected Sellers.
- Notification sent to both Buyer and Seller.

### AF-PO-REQ-007 — Transition to Payment (Logistics)
When the Buyer selects "AgriForward Logistics" and confirms the payment method:
- For methods that support authorization hold (e.g., cards), the system places a hold. **Only after successful authorization** does the PO transition to `AWAITING_SELLER_CONFIRM`. If authorization fails, the PO stays in `LOCKED` and the Buyer is notified.
- For push payment methods (QR, Internet Banking, TrueMoney, Counter Service) that require the Buyer to actively complete the payment outside the system, the PO transitions to `PAYMENT_IN_PROGRESS`. In this state, the Buyer must complete the payment within a configurable time limit (default 15 minutes). Once the gateway confirms successful payment, the PO moves to `AWAITING_SELLER_CONFIRM`. If the time limit expires without payment, the PO returns to `LOCKED` and the Buyer is notified.

### AF-PO-REQ-008 — Seller Actions during AWAITING_SELLER_CONFIRM
Sellers can only cancel their Offer (no modifications). Upon cancellation, removed from PO and group chat; deposit returned immediately.

**Auto‑cancel for non‑responsive Sellers:** If a Seller does **not** explicitly confirm or cancel within the 24‑hour window, the system **shall** treat their Offer as **cancelled by the Seller** at the deadline. All consequences of a voluntary cancellation apply (removal from PO, deposit return, cancellation rate increment). **A notification must be sent to both the Seller and the Buyer immediately when an auto‑cancellation occurs.**

### AF-PO-REQ-008-A — Seller Inability-to-Deliver Report
After a Seller has confirmed (during `AWAITING_SELLER_CONFIRM`) or after the PO has reached `CONTRACT`, if the Seller encounters an event beyond their control that prevents delivery (e.g., goods damaged before shipment), the Seller **shall** have the option to report "ไม่สามารถส่งมอบได้" (Unable to deliver) through the system.
- This action automatically creates a dispute case (AF‑SUPPORT‑REQ‑001).
- The system temporarily freezes the Seller’s deposit and notifies both parties and Admin.
- Admin reviews and decides whether to force‑cancel the PO or take other measures.

### AF-PO-REQ-009 — Recalculation and Buyer Reconfirmation
After the 24‑hour window expires or when all selected Sellers have responded (including auto‑cancelled ones):
- The system recalculates the total amount based on the remaining Offers.
- If no Offers remain, the PO transitions to `CANCELLED`.
- If the amount changes, the Buyer is notified and can:
  - **Accept** the new amount (proceed to capture).
  - **Cancel** the PO (→ `CANCELLED`).
  - **Return to Offer selection** (revert PO to `OPEN`, unlock all Offers, clear current selections, and later re‑enter `LOCKED` with new selections). Any pending payment authorizations are voided.
- If the amount is unchanged, the Buyer is still prompted to reconfirm explicitly before capture.

**Buyer Reconfirmation Deadline:** The Buyer **must** respond to the recalculation notification within **24 hours** from the time the notification is delivered. If the Buyer does not respond within this period, the system **shall** treat it as a **rejection**: the PO transitions to `CANCELLED`, all payment authorizations are voided, and all deposits are returned.

### AF-PO-REQ-010 — Payment Capture and Contract Creation
Upon reconfirmation, system captures full payment.
- **Before capture, if the authorization hold has expired, the system automatically re‑authorizes the full amount.** If re‑authorization fails, the PO enters `PAYMENT_PENDING` immediately.
- On successful capture → `CONTRACT`, immutable contract, shipment request dispatched.
- On failure → `PAYMENT_PENDING`.

### AF-PO-REQ-011 — Payment Pending Resolution
Buyer has 24 hours to resolve payment issues. System retries capture after expiration or manual trigger. Persistent failure → `CANCELLED`.

### AF-PO-REQ-012 — Contract Completion
On `CONTRACT`, read-only shipment status. After full delivery acceptance, contract is fulfilled.

### AF-PO-REQ-013 — PO Cancellation
- **By Buyer**: Allowed any time before `CONTRACT`. Immediate `CANCELLED`. If payment has already been made (push payment succeeded), the system processes a refund (see AF-PAY-REQ-008).
- **By System**: As specified.

### AF-PO-REQ-014 — PO Expiry (Extended)
The system **shall** automatically transition a PO to `EXPIRED` when its expiry datetime is reached, **regardless of the current state**, unless the PO is already in a terminal state (`CONTRACT`, `OFF_PLATFORM`, `CANCELLED`, `EXPIRED`). This applies to `OPEN`, `LOCKED`, `PAYMENT_IN_PROGRESS`, `AWAITING_SELLER_CONFIRM`, and `PAYMENT_PENDING`.
- **Special handling in `PAYMENT_IN_PROGRESS`**:
  - The system immediately cancels the associated payment request (QR/link) at the gateway.
  - The PO is marked as “not accepting payments”. 
  - If a payment is received **after** the cancellation (e.g., buyer already initiated the transfer), the system **shall** automatically refund the full amount to the original payment method and notify the Buyer that the PO has expired.
- When expired, all locks are released, deposits returned, and participants notified.

### AF-PO-REQ-015 — PO Page for PO Owner
On the PO detail page for the PO owner:
- A **Cost Calculation Block** displays the total all-in cost based on selected Offers and delivery cost.
- **Real‑time logistics recalculation**: Whenever the Buyer modifies Offer selections (including when returning from `LOCKED` to `OPEN` and re‑selecting), the system immediately calls the Logistics API to update the delivery cost. If the API is unavailable, the block displays the last known cost with a warning and disables the “Proceed” button (as per AF‑LOG‑REQ‑006).
- A **"Select Best Offers"** button triggers the automatic selection logic.

### AF-PO-REQ-016 — Mandatory Delivery Address with Geo‑Coordinates
The system **shall** require the Buyer to specify a delivery address **including at least geographical coordinates (latitude and longitude)** before the PO can be published to `OPEN`. 
- The UI may provide a map pin or address selection widget to obtain these coordinates.
- The system **shall** validate that the coordinates lie within Thailand and that the distance from the nearest provincial center is within a configurable threshold (to avoid implausible locations). If validation fails, the Buyer is asked to correct the coordinates.
- If the Logistics API requires additional fields (postal code, province, etc.), those fields are mandatory as well.
- The address data is used for delivery cost calculation and shipment requests.

---

## 4. Offer Requirements

### AF-OFFER-REQ-001 — Offer Eligibility
Only verified users can submit Offers for `OPEN` POs.

### AF-OFFER-REQ-002 — Offer Binding
Each Offer **shall** be bound to exactly one PO.

### AF-OFFER-REQ-003 — Offer Modification Rules
- Freely modifiable in `OPEN`.
- Immutable after `LOCKED` (except cancellation in `AWAITING_SELLER_CONFIRM`).

### AF-OFFER-REQ-004 — Automatic Best Offer Suggestion (with Delivery Cost)
The system **shall** present the cost calculation **including delivery cost** on the Offer selection page, before the Buyer proceeds to shipping confirmation. The optimized combination uses unit price + actual calculated delivery cost (from Logistics API). **If the API is unavailable the Buyer cannot proceed** (the UI is disabled with a warning). All subsequent changes to Offer selections will trigger a fresh delivery cost calculation.

### AF-OFFER-REQ-005 — Manual Selection Override
Buyer may manually modify selections before `LOCKED`. After returning from `LOCKED` to `OPEN`, manual selection is also possible (all previous selections are cleared).

### AF-OFFER-REQ-006 — Seller Cancellation Rate Limit
Threshold: 3 cancellations in 30 days → 7-day suspension from new Offers. Does not affect ongoing transactions. The system counts only cancellations initiated by the Seller (including auto‑cancellations) during `AWAITING_SELLER_CONFIRM`; cancellations caused by Buyer or system expiry are not counted.

### AF-OFFER-REQ-007 — Fast Confirmation Badge
Badge awarded to Sellers whose **average confirmation time** for transactions that **successfully reached `CONTRACT` or `OFF_PLATFORM`** is below a configurable threshold (default 2 hours). 
- Confirmations that are later cancelled by the Seller are excluded from the average calculation.
- The badge is recalculated weekly or upon a significant status change.

### AF-OFFER-REQ-008 — Multi‑PO Selection Notification
When an Offer is selected by a Buyer and the containing PO transitions to `LOCKED`, the system **shall** notify the Seller if that same Offer is currently selected in other `LOCKED` or `AWAITING_SELLER_CONFIRM` POs. The notification includes a count of active PO selections and advises the Seller to manage their available stock. The Seller may use this information to consider cancelling Offers in other `OPEN` POs if necessary.

---

## 5. Deposit System

### AF-DEPOSIT-REQ-001 — Deposit Deduction
10% of Offer value deducted immediately upon Offer creation.

### AF-DEPOSIT-REQ-002 — Full Refund Rule
Deposits returned in full when: PO is `CANCELLED` before `CONTRACT`, `OFF_PLATFORM`, `EXPIRED`, after Buyer acceptance for that Seller’s goods (see AF‑FULFILL‑REQ‑001), or when Seller cancels (or is auto‑cancelled) during `AWAITING_SELLER_CONFIRM`.

### AF-DEPOSIT-REQ-003 — No Automatic Forfeiture
System does not forfeit deposits.

### AF-DEPOSIT-REQ-004 — Wallet Top‑Up
Users **shall** be able to add funds to their deposit wallet via the integrated payment gateway (Omise/PaySo). Supported methods include TrueMoney Wallet, QR Payment, Internet Banking, and Counter Service. The top‑up amount is credited to the wallet immediately upon successful payment, or after verification for manual methods. A clear transaction history of all top‑ups and deductions is maintained in the wallet.

---

## 6. Payment Requirements

### AF-PAY-REQ-001 — Payment Gateway Integration
The system **shall** integrate with Omise and PaySo for all online payments.
- **Omise**: cards, TrueMoney Wallet, Internet Banking, QR, installment plans.
- **PaySo**: e-Payment, Payment Link, SureSure for automatic slip verification.

### AF-PAY-REQ-002 — Supported Payment Methods
Credit/Debit Cards, Internet Banking, QR (PromptPay), TrueMoney Wallet, Counter Service (Lotus's), Installment Plans, Offline Slips (verified via SureSure).

### AF-PAY-REQ-003 — Authorization Hold Verification
For card payments, an authorization hold is placed where supported. **The system must verify the hold was successful** before transitioning to `AWAITING_SELLER_CONFIRM`. If hold fails, the PO remains in `LOCKED` and the Buyer is notified. For methods without hold, Sellers are informed that payment is not yet secured.

### AF-PAY-REQ-004 — Payment Flow (Push Payments)
For methods where the Buyer must push payment (QR, TrueMoney Wallet, Internet Banking, Counter Service):
1. Upon confirmation, the system creates a payment request via the gateway and PO enters `PAYMENT_IN_PROGRESS`.
2. The Buyer has a configurable time limit (default 15 minutes) to complete the payment.
3. When the gateway confirms payment success, the PO transitions to `AWAITING_SELLER_CONFIRM`.
4. If the time limit expires, the PO returns to `LOCKED` and the Buyer is notified.

### AF-PAY-REQ-005 — Payment Flow (Pull/Card)
For card payments with authorization hold:
1. Authorization hold placed and verified → `AWAITING_SELLER_CONFIRM`.
2. After reconfirmation, capture is executed. If the original hold has expired, the system **re-authorizes** before capture.
3. Capture failure → `PAYMENT_PENDING` with 24-hour window.
4. Success → Contract.

### AF-PAY-REQ-006 — Offline Payment Flow (Slip with Verification Gate)
1. Buyer uploads slip → PO moves to `AWAITING_SELLER_CONFIRM`.
2. After reconfirmation, a Contract is created but marked with `payment_status = "pending_verification"`. **No shipment request is dispatched** until payment verification is complete.
3. Slip verification is performed by the SureSure service (or manually by Admin if needed). **If the SureSure API is unavailable, the system immediately notifies Admin to perform manual verification and does not leave the slip in pending state indefinitely.**
4. Upon successful verification, the Contract is activated and the shipment request is dispatched.
5. If verification fails (slip rejected), the PO transitions to `CANCELLED` and the deposit/refund procedure is triggered.

### AF-PAY-REQ-007 — Payment Status Clarity for Sellers
In `AWAITING_SELLER_CONFIRM`, Sellers see whether payment is authorized, pending, or (for slips) awaiting verification.

### AF-PAY-REQ-008 — Refund on Cancellation After Payment
If the PO is cancelled after the Buyer has successfully completed a payment (push payment or capture) but before the shipment request is dispatched (i.e., during `AWAITING_SELLER_CONFIRM` or `PAYMENT_PENDING`), the system **shall** automatically initiate a **full refund** via the payment gateway. 
- The refund method follows the original payment channel: card refunds go back to the card; TrueMoney returns to the wallet; Counter Service payments will require manual bank account refund and the Buyer is contacted accordingly.
- Estimated refund time: 5–10 business days depending on the gateway.
- The Buyer is notified with an estimated time to refund.

### AF-PAY-REQ-009 — Payment Gateway Fee Transparency
The system **shall** display any fees charged by the payment gateway (e.g., card processing fee) as a separate line item from the optional AgriForward transaction fee. The total amount charged to the Buyer = item total + shipping + gateway fee + AgriForward fee (if any). These fees are frozen according to AF‑BIZ‑REQ‑003.

---

## 7. Logistics & Delivery

### AF-LOG-REQ-001 — Shipment Status Read Only
System displays shipment status, timeline, tracking reference, and POD evidence as read-only.

### AF-LOG-REQ-002 — Shipment Data Origin
Shipment status updates imported automatically from external logistics systems only.

### AF-LOG-REQ-003 — Shipment Request Dispatch with Retry
Upon contract activation (payment verified for slip, or immediate for online payments), system dispatches a shipment request to the external logistics API via a Message Queue. The queue implements automatic retry with exponential backoff. After exceeding max retries, message goes to dead-letter queue and Admin is notified.

### AF-LOG-REQ-004 — Logistics API Fallback for Status
If the external logistics API is unavailable for status updates, system displays last known status with a message: "สถานะการขนส่งอยู่ระหว่างอัปเดต".

### AF-LOG-REQ-005 — Delivery Cost Calculation
System calls the external Logistics API to calculate actual delivery cost based on vehicle type, distance, and product attributes. This cost is used in the Best Offer calculation and shown on the Offer selection page.

### AF-LOG-REQ-006 — Mandatory Delivery Cost Availability
**The system shall not allow a Buyer to proceed from `LOCKED` to any shipping confirmation (neither Self Pickup nor Logistics) unless a definitive delivery cost has been obtained from the Logistics API.** If the API is unavailable, the “Proceed” action is disabled and a clear error message is displayed. No fallback flat rate is used during transaction creation.

---

## 8. Proof of Delivery (POD)

### AF-POD-REQ-001 — POD Display
System displays POD records including PIN confirmation status, signature, and photographic evidence.

---

## 9. Contract Fulfillment

### AF-FULFILL-REQ-001 — Per‑Seller Deposit Return
When the logistics API confirms that the Buyer has accepted the items provided by a specific Seller (partial delivery), the system **shall immediately** return that Seller’s deposit (10%) to their wallet. The contract is considered fully fulfilled when all Sellers’ items have been accepted.

### AF-FULFILL-REQ-002 — Self Pickup Completion
After PO reaches `OFF_PLATFORM`:
- No confirmation is required from either party.
- The PO is closed immediately.
- Notification sent to both Buyer and Seller.

### AF-FULFILL-REQ-003 — Delivery Rejection Handling
If the logistics API reports that the Buyer **rejected** (refused to accept) the delivery:
- The system immediately **suspends** the return of the deposit for that Seller.
- Both Buyer and Seller are notified, and a dispute case is automatically created (refer to AF‑SUPPORT‑REQ‑001).
- No further automatic refund or deposit return occurs until Admin resolves the dispute.

---

## 10. Insurance (Quality Protection)

### AF-INS-REQ-001 — Insurance Purchase Option
Optional quality insurance available during shipping selection (configurable % of order value, default 3%).

### AF-INS-REQ-002 — Claim Submission
Buyer can submit claims via system; forwarded to external insurance provider. The system tracks the claim status (submitted, under review, approved, rejected, paid).

### AF-INS-REQ-003 — Claim Status Visibility
Buyer can view claim status. System does not adjudicate.

### AF-INS-REQ-004 — Insurance Policy Details
Before purchase, the Buyer is presented with the insurance policy details (coverage period, terms, claim process). These details are configurable by Admin and are frozen at the time of purchase. The insurance premium is **non-refundable** once the Contract is formed, except when the entire PO is cancelled before the shipment request is dispatched.

---

## 11. Reputation, Reporting & Scores

### AF-REP-REQ-001 — Buyer Reporting of Seller
Buyers may file reports with evidence for any completed transaction.

### AF-REP-REQ-002 — Report Review
Admin reviews and may suspend Offer submission or lower visibility.

### AF-REP-REQ-003 — Seller Score
Public score (0–5) based on ratings, reports, and cancellation rate. Minimum 3.0 to submit Offers.

### AF-REP-REQ-004 — Default Seller Score
A newly verified Seller **shall** start with a default score of 3.0, enabling them to submit Offers immediately.

### AF-REP-REQ-005 — Seller Reporting of Buyers
Sellers may also file reports against Buyers (e.g., failure to accept delivery without reason, repeated PO abandonment). Admin reviews these reports similarly and can take actions against the Buyer’s ability to create POs or lower their internal rating.

### AF-REP-REQ-006 — Buyer Score
A **Buyer Score** (0–5) is calculated from:
- The average rating received from Sellers (AF‑RATE‑REQ‑003).
- The number of unresolved or upheld reports against the Buyer.
If a Buyer’s score falls below a configurable threshold (default 2.5), the system **shall** restrict the Buyer from creating new POs until the score improves. The score is recalculated weekly.

### AF-REP-REQ-007 — Default Buyer Score
A newly registered Buyer **shall** start with a default score of 3.0, enabling immediate PO creation.

---

## 12. Rating System

### AF-RATE-REQ-001 — Post-Transaction Rating (Buyer → Seller)
- For logistics: Buyer may rate after fulfillment (any time within 30 days).
- For Self Pickup: Buyer may rate **7 calendar days after the PO transitions to `OFF_PLATFORM`**.
Ratings (1–5 stars) can be submitted within 30 days of the event.

### AF-RATE-REQ-002 — Rating Display (Sellers)
Average rating and count publicly visible on the Seller’s profile and Offers.

### AF-RATE-REQ-003 — Seller → Buyer Rating
After a transaction reaches `CONTRACT` or `OFF_PLATFORM`, the Seller may also rate the Buyer (1–5 stars) and leave an optional comment. The rating period is 30 days. The average Buyer rating is displayed on the Buyer’s profile and feeds into the Buyer Score.

---

## 13. Communication (Group Chat)

### AF-CHAT-REQ-001 — Group Chat Creation
Group chat created when PO transitions from `OPEN` to `LOCKED`. **Only one group chat is ever created per PO**; it is reused if the Buyer returns to `OPEN` and then re-enters `LOCKED`.

### AF-CHAT-REQ-002 — Members
Initial members: Buyer, Sellers whose Offers were selected at the moment of entering `LOCKED`. Admin(s) **may** be added to a group chat only when necessary (configurable; default: no Admin is automatically added, but Admin can access any chat history via the backend).

### AF-CHAT-REQ-003 — Features
Text, voice, video, image sharing, file sharing via third-party service.

### AF-CHAT-REQ-004 — Lifetime and Post‑Closure Access
Active for **30 calendar days from the first group creation (first `LOCKED` date)**. Afterwards automatically archived. **After closure, original members and Admins can still read the full conversation history** for at least 12 months, but cannot send new messages.

### AF-CHAT-REQ-005 — Read-Only After PO Closure
- For `CANCELLED`, `EXPIRED`, or after `CONTRACT` fulfillment: the group chat becomes **read-only immediately**.
- For `OFF_PLATFORM` (Self Pickup): the group chat remains **active for 7 calendar days** after the transition, then becomes read-only.

### AF-CHAT-REQ-006 — Privacy, Auditing, and Automatic Moderation
- No personal contact information is intentionally exposed by the system.
- **Automatic moderation**: The system **shall** scan messages for patterns resembling phone numbers, email addresses, or external links. Detected content is blocked from sending and the user is warned. Repeated violations are flagged to Admin.
- All messages retained for at least 12 months in secure archive.

### AF-CHAT-REQ-007 — Dynamic Member Update on Re-selection
If the Buyer returns the PO from `LOCKED` to `OPEN`, changes the Offer selection, and then re-enters `LOCKED`:
- The existing group chat is **updated**.
- Sellers whose Offers are **no longer selected** are **removed** from the chat.
- Sellers whose Offers are **newly selected** are **added** to the chat.
- Admin and Buyer remain always.

---

## 14. Notifications

### AF-NOTIF-REQ-001 — Multi-Channel Notification
The system **shall** send notifications for the following critical events via In-app, Email, and optional Line OA:
- PO state changes (to all relevant parties).
- New Offer received on an owned PO.
- Counter-party actions (confirmation, cancellation).
- Approaching deadlines (PO expiry, Seller confirmation window, payment pending).
- Successful payment / receipt.
- Shipment status updates.
- **New PO published in a subscribed product category**.
- Rating request.

### AF-NOTIF-REQ-002 — Notification Preferences
Users can configure channels.

---

## 15. Unified Dashboard Requirements

### AF-DASHBOARD-REQ-001 — Single Interface
Unified dashboard combining Buyer and Seller functionality without mode switching.

### AF-DASHBOARD-REQ-002 — Combined PO View
All POs (buying and selling) in a single integrated view.

### AF-DASHBOARD-REQ-003 — Desktop First Design
Optimized for desktop with responsive adaptation.

### AF-DASHBOARD-REQ-004 — Tab-based Navigation
Tab-based navigation for different activity views.

---

## 16. Product Catalog & Navigation Requirements

### AF-CATALOG-REQ-001 — Admin Only Product Management
Only Admin role **shall** be allowed to add, edit, or remove products from the catalog.

### AF-CATALOG-REQ-002 — No Free Text Product Entry
Users **shall not** be allowed to enter free text product names. Products must be selected from the existing catalog only.

### AF-CATALOG-REQ-003 — Standardized Product Listing
The system **shall** maintain a standardized product list with predefined categories, grades, and units.

### AF-CATALOG-REQ-004 — Product Listing Page
The system **shall** provide a product listing page where:
- Each product displays a **"Create New Purchase Order"** button and a **"Subscribe to New POs"** button (for receiving notifications when new POs for this product are published).
- Clicking a product navigates to a view listing all **OPEN POs** for that product, with a button to **"Create New Purchase Order"**.

### AF-CATALOG-REQ-005 — Product Detail / PO List View
From the product detail (or PO list) page:
- Clicking on an individual PO **shall** display the list of Offers for that PO.
- A button **"Submit Offer"** is displayed to enable the user to act as a Seller for that PO.

### AF-CATALOG-REQ-006 — Subscription Eligibility
Only users who have completed identity verification (KYC) can subscribe to product categories. Unsubscription is possible at any time from the same product page or from the user’s notification settings.

---

## 17. User Interface Requirements

### AF-UI-REQ-001 — Desktop First Responsive Design
### AF-UI-REQ-002 — Minimum 48px Tap Target
### AF-UI-REQ-003 — Thai Language Support
### AF-UI-REQ-004 — Figma Color Palette Compliance

(Unchanged)

---

## 18. Data Governance & System Integrity

### AF-DATA-REQ-001 — Data Classification
Public, Internal, Confidential, Sensitive.

### AF-DATA-REQ-002 — Retention Compliance
Chat logs and transaction records retained for at least 2 years. After 12 months, the system may apply **pseudo‑anonymization** (e.g., replace member names with generic labels) to protect personal data while preserving conversation content for legal or dispute purposes.

### AF-DATA-REQ-003 — Right to Erasure (PDPA)
Users **shall** be able to request deletion of their personal data. The system must respond within 30 days. Data that is legally required for financial records, ongoing disputes, or regulatory compliance may be retained but access will be restricted; any non‑essential personal data will be permanently deleted.

### AF-SYS-REQ-001 — Error Transparency
All rejected actions return explicit error reasons.

### AF-SYS-REQ-002 — Auditability
All state transitions **shall** be audited with immutable logs.

### AF-SYS-REQ-003 — Payment Testing Requirement
Comprehensive integration tests covering all payment scenarios.

### AF-SYS-REQ-004 — Security & Backup
- All data transmitted between client and server encrypted using TLS 1.2 or higher.
- All sensitive data at rest (KYC documents, payment tokens) encrypted using AES-256.
- **Raw credit card numbers shall never be stored.** Only payment tokens received from the gateway are stored, in compliance with PCI-DSS.
- Database backed up daily. RTO: 4 hours, RPO: 24 hours.

### AF-SYS-REQ-005 — Monitoring & Alerting
The system **shall** expose health‑check endpoints and integrate with a monitoring service (e.g., Azure Monitor, Grafana). Alerts must be sent to the technical team for critical failures such as Payment Gateway downtime, Logistics API unavailability, or Message Queue dead‑letter threshold breaches.

### AF-SYS-REQ-006 — Rate Limiting
The system **shall** enforce configurable rate limits to prevent abuse:
- Default: maximum 10 PO creations per user per day.
- Default: maximum 50 Offer submissions per user per day.
- Users are notified when approaching the limit. Limits can be adjusted by Admin.

### AF-SYS-REQ-007 — Scalability & Performance
The system **shall** be designed to support at least 500 concurrent active user sessions. Under normal load, API response time (average) should not exceed 2 seconds.

### AF-SYS-REQ-008 — Penetration Testing
A third‑party security penetration test **shall** be conducted before the system goes live for public access. All critical and high‑severity findings must be resolved before launch.

---

## 19. Revenue & Fee Configuration

### AF-BIZ-REQ-001 — Transaction Fee & Gateway Fee Transparency
- The system may apply a configurable transaction fee (AgriForward fee).
- Any payment gateway processing fee is shown as a separate line item.
- Both fees are displayed clearly in the cost breakdown and are frozen at the time of payment method confirmation.

### AF-BIZ-REQ-002 — Logistics Service Margin
The delivery cost quoted to the Buyer **shall** be the sum of:
- The base cost obtained from the Logistics API.
- A configurable margin (percentage, set by Admin) applied on top of the base cost.
The system **shall** display the total logistics cost to the Buyer either as a single value or broken down as “ค่าขนส่ง (รวมค่าบริการ)” for full transparency.

### AF-BIZ-REQ-003 — Fee Freeze
The transaction fee, gateway fee, and logistics margin presented to the Buyer at the time they confirm the payment method **shall be stored** and remain unchanged for that PO, regardless of subsequent admin modifications.

---

## 20. Invoicing & Receipts

### AF-INV-REQ-001 — Automatic Receipt Generation
After a successful payment capture (or verified slip), the system **shall** generate a digital receipt for the Buyer and a fee invoice for the Seller (if applicable). These documents are accessible in the user’s transaction history.

### AF-INV-REQ-002 — Tax Information
Users who require full tax invoices (e.g., registered companies) must provide their tax identification number and company name during identity verification. The system includes this information on the generated documents when applicable.

### AF-INV-REQ-003 — VAT Calculation
The system **shall** calculate Value Added Tax (VAT) at the prevailing rate (7%) on applicable items (transaction fees, service margins, logistics margins, insurance premiums). The VAT amount must be displayed as a separate line item on receipts and tax invoices where required. The VAT rate is configurable by Admin to comply with future regulatory changes.

---

## 21. Admin Intervention & Dispute Handling

### AF-SUPPORT-REQ-001 — Dispute Submission
The system **shall** provide a dedicated channel for users to submit complaints or disputes, including supporting evidence. A dispute is automatically created when a delivery is rejected or when a Seller reports inability to deliver.

### AF-SUPPORT-REQ-002 — Admin Ticket Management
Admins **shall** be able to track, manage, and resolve submitted tickets. In justified cases, Admins may extend deadlines, force‑cancel offers, or suspend accounts. All interventions are logged.

### AF-SUPPORT-REQ-003 — Dispute Logging
All dispute cases and their outcomes are permanently logged for audit and regulatory compliance.

### AF-SUPPORT-REQ-004 — Admin Force‑Cancel After Contract
In exceptional circumstances (fraud, dispute, regulatory requirement), Admin **may** force‑cancel a PO even after it has reached `CONTRACT` state. 
- This action requires a **two‑step confirmation** by the Admin to prevent accidental cancellations. The cancellation cannot be automatically undone, but Admin may initiate corrective actions manually.
- The contract is flagged as **voided**.
- Any associated payment is **refunded** to the Buyer automatically (using the standard refund mechanism).
- The logistic provider is notified with a request to halt shipment (the external system may or may not be able to comply, but the notification is sent).
- **Seller deposits are returned in full** unless Admin determines, based on clear evidence, that the cancellation is due to the Seller’s fault (e.g., wrong goods). In that case, Admin may override the deposit return; the reason must be recorded in the audit log.
- Admin must decide on the deposit return within **5 business days** of the force‑cancel.
- All parties are notified.

### AF-SUPPORT-REQ-005 — Global Account Suspension
Admin **shall** be able to suspend a user account entirely. While suspended, the user cannot log in or perform any action. For any active Offers belonging to the suspended user that are part of a `LOCKED` or `AWAITING_SELLER_CONFIRM` PO, Admin must specify whether to cancel them (with full deposit refund) or leave them active pending further review. The decision is logged.

### AF-SUPPORT-REQ-006 — Support Response SLA
The system **shall** display a message to users upon dispute submission indicating the expected response time (“ทีมงานจะตอบกลับภายใน 1–2 วันทำการ”). Admin has a dashboard to view tickets that have exceeded the SLA.

---

**End of consolidated requirements v3.11**