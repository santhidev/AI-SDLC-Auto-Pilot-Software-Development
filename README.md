# AI SDLC Autopilot Framework v2.0.0

**เปลี่ยน Requirement เป็นซอฟต์แวร์ที่พร้อมใช้งาน โดย AI Agent ใน Code Editor ของคุณ**

---

## เกี่ยวกับ Framework

AI SDLC Autopilot Framework คือชุดคำสั่งสำหรับ AI Agent ที่ทำงานภายใน Code Editor (เช่น Zed, Cursor, VS Code) เพื่อทำหน้าที่เป็น Software Development Lifecycle Pipeline แบบอัตโนมัติเต็มรูปแบบ  
เพียงคุณวางไฟล์ requirement.md และพูดว่า Start จากนั้นระบบจะ:

- วิเคราะห์และปรับ Requirement ให้สมบูรณ์ (วนซ้ำเชิงลึกกว่า 1000 รอบ)
- เลือก Stack ที่เหมาะสม (Next.js + NestJS + SQLite เป็นค่าเริ่มต้น)
- ออกแบบ UX/UI, สถาปัตยกรรม, API Contract
- เขียนโค้ดทั้ง Frontend และ Backend ด้วย Test‑Driven Development และ Clean Architecture
- ทดสอบและตรวจสอบความปลอดภัย
- สร้าง Demo และ Build Script ที่ใช้งานได้จริงบนเครื่องของคุณ
- รองรับการเพิ่มแพลตฟอร์มใหม่ (Web, Mobile, Desktop) ในภายหลัง

ทุกอย่างถูกบันทึกเป็นไฟล์บนเครื่องของคุณ โดยไม่ต้องใช้ API Key จากผู้ให้บริการภายนอก

---

## คุณสมบัติเด่น

- ทำงานอัตโนมัติระดับสูง: มี 3 โหมด (Full Auto, Safe Auto, Manual) เพื่อควบคุมระดับการถาม
- รองรับหลายแพลตฟอร์ม: Web, Mobile, Desktop โดยใช้ Backend และ Core ร่วมกัน
- Deep Requirement Refinement: วิเคราะห์และแก้ไขจุดบอดของ Requirement วนซ้ำกว่า 1000 รอบภายใน
- Platform-Specific Stack Analysis: ตรวจสอบความเหมาะสมของ Stack สำหรับแต่ละแพลตฟอร์ม
- Component-First (Atomic Design): UI ทั้งหมดสร้างจาก Design Tokens ในรูปแบบ Atom, Molecule, Organism
- Cross‑Platform Design Consistency: ตรวจสอบ Component Signatures ข้ามแพลตฟอร์ม
- API Contract Versioning: api_spec.yaml มีเวอร์ชัน, API_CHANGELOG, และ Regression Tests
- Pre‑Development Tool Check: ตรวจสอบว่าเครื่องมือที่จำเป็น (Node, npm, Expo, Docker) พร้อมใช้งาน
- Demo และ Build Scripts: สคริปต์สำหรับรัน Demo และ Build ที่ตรวจสอบพอร์ตและสิ่งแวดล้อมให้
- Self‑Audit: ระบบตรวจสอบตัวเองทุกเฟสด้วย Checklist 10 ข้อ
- Resume และ Handoff: หยุดเมื่อไหร่ก็ได้ กลับมาทำต่อจากไฟล์ State, Context Card และ Backup
- Memory & Learning: จดจำข้อผิดพลาดและการตัดสินใจ เพื่อใช้ในอนาคต
- Model Switching Advisory: แนะนำว่า AI Model ตัวไหนเหมาะกับงานแต่ละเฟส
- Requirement Change Detection: ตรวจจับเมื่อ Requirement ถูกแก้ระหว่างทาง พร้อมข้อเสนอการจัดการ

---

## โหมดการทำงาน

เมื่อเริ่มต้น ระบบจะถามให้คุณเลือกโหมด:

1. Full Auto – ไม่ถามอะไรเลย เดินหน้าทำทุกอย่างจนเสร็จ ถ้าพบปัญหาจะพยายามแก้เองหรือข้าม (log ไว้)
2. Safe Auto – หยุดถามเฉพาะเมื่อความมั่นใจต่ำกว่า 70% หรือเจอเรื่องสำคัญ (ความปลอดภัย/สถาปัตยกรรม)
3. Manual – แสดงทุกผลลัพธ์หลักและรอให้คุณอนุมัติก่อนเดินต่อ

---

## แพลตฟอร์มที่รองรับ

| Platform   | Frontend Technology              | Backend Technology      |
|------------|----------------------------------|-------------------------|
| Web        | Next.js (App Router) + Tailwind  | NestJS + TypeORM + SQLite |
| Mobile     | React Native + Expo             | แชร์ Backend เดียวกัน      |
| Desktop    | Electron (หรือ Tauri) + Next.js/React | แชร์ Backend เดียวกัน      |

คุณสามารถเริ่มจากแพลตฟอร์มใดก็ได้ และเพิ่มแพลตฟอร์มอื่นภายหลังโดยไม่ต้องเริ่มใหม่

---

## ข้อกำหนดเบื้องต้น

- Node.js เวอร์ชัน 18 ขึ้นไป
- npm (หรือ yarn)
- (สำหรับ Mobile) Expo CLI (แนะนำให้ใช้ผ่าน npx expo)
- (สำหรับ Desktop) Electron หรือ Tauri
- (ตัวเลือก) Docker หากต้องการรัน Demo ผ่าน Container
- AI Code Editor ที่มี Agent (Zed, Cursor, VS Code with Copilot/Cody)

ก่อนเริ่มพัฒนาในแต่ละแพลตฟอร์ม ระบบจะตรวจสอบให้ว่ามีเครื่องมือเหล่านี้พร้อมหรือไม่ ถ้าขาดจะแจ้งให้คุณทราบและหยุดจนกว่าจะแก้ไข

---

## การเริ่มต้นใช้งาน

1. สร้างโฟลเดอร์โปรเจกต์ใหม่ (หรือเปิดโฟลเดอร์ว่าง)
2. วางไฟล์ ai_sdlc_autopilot_framework.md และ requirement.md ลงใน root
3. เปิดโปรเจกต์ใน AI Code Editor
4. สั่ง AI Agent: “Read this file and start the SDLC pipeline.” หรือ “Start”
5. ตอบคำถามเลือกโหมดและแพลตฟอร์ม
6. AI จะทำงานที่เหลือให้เอง จนกว่าจะมี Demo หรือ Build Script พร้อมใช้

---

## ขั้นตอนการทำงาน (Pipeline Phases)

1. Mode & Platform Selection – เลือกโหมดและแพลตฟอร์มแรก
2. Requirement Deep Refinement – ปรับ Requirement ให้สมบูรณ์ด้วยการวิเคราะห์ภายในกว่า 1000 รอบ
3. Mega‑Phase (Specs, Stack Baseline, Design Tokens) – วิเคราะห์ สร้าง Spec, เลือก Stack, ออกแบบ Design Tokens และ Component Spec
4. Platform‑Specific Stack Deep Analysis – ตรวจสอบและปรับ Stack สำหรับแพลตฟอร์มที่เลือก
5. Architecture Design – ออกแบบโครงสร้างโปรเจกต์, API สัญญา (OpenAPI 3.0), Database Schema และข้อกำหนดการเขียนโค้ด
6. Developer (Efficient TDD) – เขียน Test → Implementation → Self‑Review พร้อมอัปเดต Dependencies
7. Tester – ตรวจสอบ Test, Contract Tests, และ Regression สำหรับแพลตฟอร์มเดิม
8. Security Auditor – ตรวจ OWASP Top 10, Dependency Audit, การเก็บความลับ
9. Deployer & Demo – สร้าง Demo Scripts, Build Scripts, Environment Files และ README
10. Finalization – รวมทุกอย่างเป็น Unified Demo เมื่อทุกแพลตฟอร์มเสร็จ

---

## โครงสร้างโปรเจกต์

  root/
  ├── requirement.md
  ├── ai_sdlc_autopilot_framework.md
  ├── README.md (สร้างโดย AI)
  ├── SUMMARY.md
  ├── BLOCKED_STORIES.md (ถ้ามี)
  ├── .gitignore
  ├── setup_and_demo.sh / .ps1
  ├── docker-compose.yml
  ├── API_CHANGELOG.md
  ├── .sdlc/                   (ข้อมูลภายในของ Pipeline)
  │   ├── pipeline_state.json
  │   ├── pipeline_config.json
  │   ├── context_card.json
  │   ├── artifacts/           (ผลลัพธ์จากทุกเฟส)
  │   ├── memory/              (การเรียนรู้)
  │   ├── demos/
  │   ├── builds/
  │   └── backups/
  ├── src/
  │   ├── core/    (แชร์ทุกแพลตฟอร์ม)
  │   ├── api/     (NestJS Backend)
  │   ├── web/     (Next.js Frontend)
  │   ├── mobile/  (React Native)
  │   └── desktop/ (Electron)
  ├── tests/
  │   ├── web/
  │   ├── api/
  │   ├── mobile/
  │   ├── desktop/
  │   ├── contract/
  │   └── e2e/
  └── docs/

---

## การทำงานแบบ Multi‑Platform

- แพลตฟอร์มแรก: สร้าง Core, Backend, และ Frontend ของแพลตฟอร์มนั้น
- แพลตฟอร์มถัดไป: สร้างเฉพาะ Frontend ใหม่ ส่วน Backend ที่มีอยู่จะถูกขยายแบบ Backward‑Compatible
- ใช้ Component Signatures ตรวจสอบความสอดคล้องของ UI ข้ามแพลตฟอร์ม
- บันทึก Design Deviations เมื่อจำเป็นต้องปรับแต่งเฉพาะแพลตฟอร์ม

---

## Component‑First & Cross‑Platform Consistency

- UI ทั้งหมดถูกสร้างด้วย Atomic Design (Atoms, Molecules, Organisms)
- ทุกค่าสี, ขนาด, ระยะห่าง มาจาก Design Tokens เท่านั้น ห้าม Hardcode
- Component Signatures (props, variants, states) ถูกบันทึกและเปรียบเทียบข้ามแพลตฟอร์ม
- ระบบแจ้งเตือนเมื่อพบความไม่สอดคล้อง

---

## API Contract Versioning & Regression Tests

- api_spec.yaml ถูกกำหนดเวอร์ชัน (เช่น 1.0.0) และเก็บ Checksum
- ทุกครั้งที่แก้ไข Backend: เพิ่ม Minor Version, อัปเดต API_CHANGELOG.md
- สร้าง Contract Tests สำหรับทุกแพลตฟอร์มที่มีอยู่ เพื่อรับประกัน Backward Compatibility
- มี run_contract_tests.sh สำหรับให้คุณรันภายหลัง

---

## การตรวจสอบเครื่องมือก่อนเริ่มพัฒนา

ก่อนเขียนโค้ดในแต่ละแพลตฟอร์ม ระบบจะ:
- ตรวจสอบ node, npm, expo, electron, docker (ตามที่ใช้จริง)
- ทดสอบคำสั่งเบื้องต้นว่าใช้งานได้จริง
- หากขาดหรือเวอร์ชันเก่า: แจ้งเตือนทันทีและหยุดจนกว่าจะแก้ไข

---

## Demo และ Build Scripts

- Demo Script แยกแพลตฟอร์ม ถูกเก็บใน .sdlc/demos/
- Unified Demo Script (setup_and_demo.sh และ .ps1) จะ:
  - ตรวจสอบว่า Port ที่ต้องใช้ว่างหรือไม่ (3000, 4000, 19000)
  - ติดตั้ง Dependencies ด้วย npm install
  - เริ่ม Backend และรอจนกว่า Health Endpoint ตอบกลับ
  - เริ่ม Frontend ทั้งหมด พร้อมแสดง URL
  - สำหรับ Mobile: แสดง QR Code (Expo)
- Build Scripts:
  - Mobile: expo_build.sh
  - Desktop: electron_build.sh

---

## Environment Files

- .env.example ที่ root รวบรวมตัวแปรทั้งหมดที่จำเป็น
- .env แยกตามแพลตฟอร์ม (src/web/.env.local, src/mobile/.env) พร้อมค่าเริ่มต้นที่เหมาะสม
- ตัวอย่าง: API_URL=http://localhost:4000 สำหรับ Web; สำหรับ Android Emulator ใช้ http://10.0.2.2:4000

---

## Scrum Mode (ทางเลือก)

เปิดใช้งานได้ใน .sdlc/pipeline_config.json (scrum_mode: true)
- แบ่ง Stories เป็น Sprints (3-5 Stories ต่อ Sprint)
- มี Sprint Planning, Review, Retrospective อัตโนมัติ (ใน Manual/Safe Auto จะถาม Approve)
- Action Items จาก Retrospective จะถูกส่งต่อไปยัง Sprint ถัดไป

---

## Self‑Audit & Continuous Improvement

หลังจบแต่ละเฟส ระบบจะตรวจสอบตัวเองด้วย Checklist นี้ (วนซ้ำจนกว่าจะผ่านทั้งหมด):

1. ไฟล์ทั้งหมดมี syntax ถูกต้อง
2. Contract Version ตรงกับ SHA256 ที่เก็บไว้
3. Health Endpoint (/health) มีอยู่และถูกต้อง
4. Component Signatures ครบถ้วนและตรงกันข้ามแพลตฟอร์ม
5. ไฟล์ package.json มี Dependencies ครบและไม่มีส่วนเกิน
6. Demo/Build Scripts ไม่มี syntax error
7. Environment Files สอดคล้องกันทุกแพลตฟอร์ม
8. Security Report ไม่มีปัญหา Critical ที่ยังไม่ได้รับการแก้ไข
9. แพลตฟอร์มเดิมยังทำงานได้ (ไม่เกิด Regression)
10. ผลตรวจสอบเครื่องมือ (Tool Check) ระบุว่าทุกอย่างพร้อม

---

## การจัดการ Context Window และ Resume

- หาก Context ใกล้เต็ม (70%): ระบบจะแจ้งให้คุณเปิด Chat ใหม่ และใช้คำสั่ง “Resume from saved state”
- State ทั้งหมดถูกบันทึกใน .sdlc/pipeline_state.json และ context_card.json
- ระบบสำรองข้อมูลอัตโนมัติ (Backup) ก่อนดำเนินการสำคัญ
- หลังจาก Finalize แล้ว คุณสามารถกลับมาสั่ง “Add platform: Mobile” เพื่อเริ่มพัฒนาต่อได้ทันที

---

## Memory & Learning

- .sdlc/memory/fix_history.json: บันทึกข้อผิดพลาดและวิธีแก้ไข (200 รายการล่าสุด)
- .sdlc/memory/decisions.json: บันทึกการตัดสินใจด้านสถาปัตยกรรม
- ก่อนตัดสินใจใหญ่ ระบบจะค้นหาด้วย Substring เพื่อใช้ข้อมูลเดิม

---

## Model Switching Advisory

ก่อนเข้าแต่ละเฟส AI Agent จะแนะนำ Model ที่เหมาะสม เช่น:
- Analyst: GPT‑4o หรือ Claude 3.5 Sonnet
- Architecture: Claude 3.5 Sonnet หรือ GPT‑4o
- Developer: GPT‑4o หรือ Claude 3.5 Sonnet

คุณสามารถเปลี่ยน Model ใน Editor แล้วยืนยัน ระบบจะเดินหน้าต่อโดยไม่มีผลกระทบกับงานที่ทำไว้

---

## Requirement Change Detection

- ระบบเก็บบ MD5 Hash ของ Requirement
- หากคุณแก้ไข Requirement ระหว่างทาง (หลัง Refinement) ระบบจะถามว่าต้องการ Re‑refine หรือไม่
- รองรับการอัปเดตแบบ Incremental โดยคุณสามารถให้คำแนะนำเพิ่มเติมได้

---

## การปรับแต่ง (Configuration)

ไฟล์ .sdlc/pipeline_config.json (สร้างอัตโนมัติ):

  {
    "mode": "full_auto",
    "auto_confirm": true,
    "scrum_mode": false,
    "docker_enabled": false,
    "test_depth": "lite",
    "retry_max": 3
  }

คุณสามารถเปลี่ยนโหมด, เปิด Scrum, หรือเปิด Docker ได้ตลอดเวลา

---

## ตัวอย่าง Requirement

ด้านล่างคือตัวอย่าง requirement.md สำหรับระบบจัดการเบอร์โทรอย่างง่าย (CRUD):

  # Requirement: Phone Number CRUD Application

  ## Project Overview
  A simple web application for storing and managing contact phone numbers.
  Users can create, read, edit, and delete contact entries (name + phone number).

  ## Target Platform
  Web (Next.js + NestJS + SQLite)

  ## Functional Requirements
  - Contact List: แสดงรายชื่อและเบอร์ พร้อมปุ่ม Add/Edit/Delete
  - Add Contact: ฟอร์มรับชื่อและเบอร์ พร้อม Validation
  - Edit Contact: ฟอร์มแก้ไข
  - Delete Contact: ยืนยันก่อนลบ
  - Validation: ห้ามว่าง, เบอร์ต้อง 10 หลัก, ห้ามเบอร์ซ้ำ

  ## Non‑Functional
  - REST API, JSON
  - Responsive, ภาษาไทย
  - ไม่มี Authentication

เพียงวางไฟล์นี้คู่กับ Framework แล้วสั่ง Start AI จะสร้างเว็บแอปให้คุณภายในไม่กี่คำสั่ง

---

## คำถามที่พบบ่อย

Q: ต้องใช้ API Key ของ OpenAI หรือไม่?
A: ไม่จำเป็น เพราะ AI Agent ใช้ Model ภายใน Editor

Q: ใช้กับ Editor อื่นได้ไหม?
A: ได้กับทุก Editor ที่มี AI Agent (Zed, Cursor, VS Code)

Q: เพิ่ม Mobile หรือ Desktop หลังจาก Web เสร็จได้ไหม?
A: ได้ ระบบจะเพิ่มเฉพาะ Frontend และทดสอบ Regression ให้

Q: Safe Auto ถามบ่อยแค่ไหน?
A: เฉพาะเมื่อความมั่นใจต่ำกว่า 70% หรือเรื่องสำคัญ เช่น Architecture/Security Critical

---

**Made with ❤️ by AI SDLC Autopilot Framework v2.0.0**
