# AI SDLC AutoPilot — Ultimate (TH/EN) | ระบบ AutoPilot แบบครบถ้วน

**EN:** A file-driven AI SDLC AutoPilot that builds end-to-end software with **Web + Mobile + Desktop**, **enterprise-quality gates**, **visible UI previews**, and **auditable evidence packs**.  
**TH:** ระบบ AI SDLC AutoPilot ที่ขับเคลื่อนด้วยไฟล์ สร้างซอฟต์แวร์แบบ end-to-end รองรับ **Web + Mobile + Desktop** พร้อม **quality gates**, **UI preview ที่มองเห็นได้**, และ **evidence pack** สำหรับงานองค์กร

---

## TL;DR / สรุปสั้นๆ

### Quick Start (No‑Ask) / เริ่มแบบไม่ต้องถาม
1) แก้ `requirement.md`  
2) รัน **PROMPT‑1** → สร้าง artifacts (Discovery→Requirements)  
3) รัน **PROMPT‑2** → ทำให้ “นิ่ง/consistent/testable”  
4) รัน **PROMPT‑4** → build ระบบ + tests + UI preview + evidence  

### When requirements change / เมื่อ requirement เปลี่ยน
รัน **PROMPT‑3 → PROMPT‑2 → PROMPT‑4**

> Repo นี้ตั้งค่าเริ่มต้นเป็น **No‑Ask** เพื่อไม่ให้คุณต้องตอบคำถามซ้ำ ๆ แต่ยังมี Wizard ไว้ “ถ้าคุณอยาก override ค่า default” เท่านั้น

---

## What is this? / นี่คืออะไร?

**EN:** This repository is an **AI SDLC AutoPilot**. It is designed so that any AI agent (or human) can continue work **from the latest state** without relying on chat history.  
**TH:** Repo นี้คือ **AI SDLC AutoPilot** ที่ออกแบบให้ AI agent หรือมนุษย์สามารถ “เริ่มต่อจากสถานะล่าสุด” ได้ทันที โดยไม่พึ่งความจำแชท

**Core rule / กติกาหลัก:**  
- **File = Source of Truth** (ไฟล์คือความจริงเดียว)  
- **No artifact → cannot proceed** (ไม่มีไฟล์ผลลัพธ์ของขั้นนั้น → ห้ามไปขั้นถัดไป)  
- **Completion is gate-based** (คำว่า “เสร็จ” ถูกตัดสินด้วย Quality Gates ไม่ใช่ความรู้สึก)

---

## Key Ideas / แนวคิดหลัก (ต้องเข้าใจ 5 อย่างนี้)

1) **State Machine SDLC**  
   - ไฟล์ `meta/sdlc-state.json` บอกว่า “ตอนนี้อยู่ phase ไหน” และ “ควรทำอะไรต่อ”

2) **Profiles = Deterministic Decisions**  
   - `meta/project-profile.yaml` : platform/stack/deploy/privacy/security/perf defaults  
   - `meta/engineering-profile.yaml` : TDD/architecture/testing/scans  
   - `meta/design-profile.yaml` : design system/tokens/preview/visual regression

3) **Artifact Contract**  
   - `meta/artifact-map.yaml` ระบุว่า phase ไหน “ต้องมีไฟล์อะไร” ถึงจะถือว่าผ่าน

4) **Quality Gates**  
   - `meta/quality-gates.yaml` ระบุ PASS/FAIL แบบ objective (traceability, tests, evidence, UI preview)

5) **UI MUST be visible**  
   - Web: **Storybook + screenshots**  
   - Mobile/Desktop: **Screenshot packs**  
   - ถ้าไม่มี preview artifacts → ยังไม่ถือว่าเสร็จ

---

## Repository Structure / โครงสร้าง Repo
