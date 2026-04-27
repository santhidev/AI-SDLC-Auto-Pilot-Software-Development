# AI SDLC Autopilot Framework v2.3.0

## เปลี่ยน Requirement เป็นซอฟต์แวร์ที่พร้อมใช้งาน โดย AI Agent ใน Code Editor ของคุณ

---

## เกี่ยวกับ Framework

AI SDLC Autopilot Framework คือชุดคำสั่งสำหรับ AI Agent ที่ทำงานใน Code Editor (เช่น Zed, Cursor, VS Code) เพื่อทำหน้าที่เป็น Software Development Lifecycle Pipeline แบบอัตโนมัติเต็มรูปแบบ

เพียงคุณวางไฟล์ requirement.md และสั่ง Start จากนั้น AI จะ:

- วิเคราะห์และปรับ Requirement ให้สมบูรณ์ (วนซ้ำเชิงลึกกว่า 1,000 รอบ)
- เลือก Stack ที่เหมาะสม (Next.js + NestJS + SQLite เป็นค่าเริ่มต้น)
- ออกแบบ UX/UI, สถาปัตยกรรม, และ API Contract
- เขียนโค้ดทั้ง Frontend และ Backend ด้วย Test‑Driven Development และ Clean Architecture
- สร้าง Demo ที่ใช้งานได้ทันที พร้อมข้อมูลตัวอย่างที่สมจริง
- หยุดหลังจากแต่ละ User Story เพื่อให้คุณทดสอบระบบที่ทำงานได้จริง (Continuous Integrated Demo)
- รองรับการเพิ่มแพลตฟอร์มใหม่ (Web, Mobile, Desktop) ในภายหลัง
- เรียนรู้และจดจำข้อผิดพลาดเพื่อปรับปรุงในอนาคต

ทุกอย่างถูกบันทึกเป็นไฟล์บนเครื่องคุณ โดยไม่ต้องใช้ API Key จากผู้ให้บริการภายนอก

---

## คุณสมบัติเด่น

- ทำงานอัตโนมัติ 3 โหมด (Full Auto, Safe Auto, Manual)
- รองรับหลายแพลตฟอร์ม: Web, Mobile, Desktop โดยใช้ Backend และ Core ร่วมกัน
- Deep Requirement Refinement วิเคราะห์จุดบอดของ Requirement วนซ้ำกว่า 1,000 รอบ
- Platform‑Specific Stack Analysis ตรวจสอบและปรับ Stack ให้ตรงกับแพลตฟอร์ม
- Component‑First (Atomic Design) UI ทั้งหมดมาจาก Design Tokens
- Cross‑Platform Design Consistency ด้วย Component Signatures
- API Contract Versioning พร้อม API_CHANGELOG และ Regression Tests
- Pre‑Development Tool Check ตรวจสอบเครื่องมือที่จำเป็นและแจ้งหากขาด
- Continuous Integrated Demo สร้างซอฟต์แวร์ที่ทำงานได้ทันทีหลังจากแต่ละ Story
- Self‑Audit 1,000+ รอบ ด้วย Checklist 17 ข้อ จนกว่าจะไม่มีจุดบอด
- Resume & Handoff หยุดเมื่อไหร่ก็ได้ แล้วกลับมาทำต่อ
- Memory & Learning จดจำข้อผิดพลาดและการตัดสินใจ
- Model Switching Advisory แนะนำ AI Model ที่เหมาะสมกับงานแต่ละเฟส
- Requirement Change Detection ตรวจจับเมื่อ Requirement ถูกแก้

---

## โหมดการทำงาน

1. Full Auto – ไม่ถามอะไรเลย ดำเนินการทุกอย่างเอง
2. Safe Auto – หยุดถามเมื่อความมั่นใจต่ำกว่า 70% หรือเรื่องสำคัญ
3. Manual – แสดงผลลัพธ์หลักทุกชิ้นและรอการอนุมัติ

---

## แพลตฟอร์มที่รองรับ

| Platform | Frontend | Backend |
|---|---|---|
| Web | Next.js (App Router) + Tailwind | NestJS + TypeORM + SQLite |
| Mobile | React Native + Expo | ใช้ Backend เดียวกับ Web |
| Desktop | Electron หรือ Tauri + Next.js/React | ใช้ Backend เดียวกับ Web |

---

## ข้อกำหนดเบื้องต้น

- Node.js 18 ขึ้นไป
- npm หรือ yarn
- สำหรับ Mobile: Expo CLI
- สำหรับ Desktop: Electron หรือ Tauri
- (ตัวเลือก) Docker
- AI Code Editor ที่มี Agent (Zed, Cursor, VS Code with Copilot/Cody)

ระบบจะตรวจสอบให้ก่อนเริ่มพัฒนา และแจ้งหากขาดเครื่องมือใด

---

## การเริ่มต้นใช้งาน

1. สร้างโฟลเดอร์โปรเจกต์ใหม่
2. วางไฟล์ ai_sdlc_autopilot_framework.md และ requirement.md ใน root
3. เปิดโปรเจกต์ใน AI Code Editor
4. สั่ง AI Agent: “Read this file and start the SDLC pipeline.” หรือ “Start”
5. ตอบคำถาม: โหมด, แพลตฟอร์ม, และ Continuous Demo
6. AI จะจัดการทุกอย่างให้ คุณจะเห็น Demo ตั้งแต่ Story แรก

---

## ขั้นตอนการทำงาน (Pipeline Phases)

1. Mode & Configuration
2. Requirement Deep Refinement (1,000+ รอบ)
3. Mega‑Phase (Specs, Stack, Design Tokens)
4. Platform‑Specific Stack Analysis
5. Tool Check
6. Architecture Design
7. Atomic Design Component Extraction
8. Dependency‑Aware Story Sequencing
9. Feature‑Driven Development (ต่อ Story):
   - Tests (Backend + Frontend)
   - Implementation
   - Mock Data Generation
   - Integrated Demo Script
   - หยุดให้คุณทดสอบ (Continuous Demo)
10. Continuous Self‑Audit
11. Finalization

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
    ├── .sdlc/                   (ข้อมูลภายใน Pipeline)
    │   ├── pipeline_state.json
    │   ├── pipeline_config.json
    │   ├── context_card.json
    │   ├── artifacts/
    │   ├── memory/
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

## Continuous Integrated Demo

คุณสมบัติเด่นที่สุด: หลังจากแต่ละ User Story ระบบจะหยุดและให้คุณทดสอบระบบที่ทำงานได้จริง (Backend + Frontend) พร้อมข้อมูล Mock ที่สมจริง

คุณจะเห็น:

- URL http://localhost:3000 สำหรับ Web App
- Swagger http://localhost:4000/docs สำหรับทดสอบ API
- ข้อมูลตัวอย่างในฐานข้อมูล (ชื่อ, เบอร์โทร ฯลฯ) ที่มาจากการวิเคราะห์ Domain ของ Requirement

คุณสามารถพิมพ์ 'f' เพื่อแก้ไข (เช่นเปลี่ยนสี, เพิ่มฟีเจอร์) แล้วระบบจะปรับเฉพาะส่วนที่เกี่ยวข้อง และเปิด Demo ใหม่ให้คุณดูทันที

---

## Scrum Mode

เปิดใช้ได้ใน .sdlc/pipeline_config.json ด้วย scrum_mode: true  
ระบบจะแบ่ง Stories เป็น Sprints (3‑5 stories) พร้อม Planning, Review, Retrospective และ Demo ทุก Sprint

---

## Self‑Audit

ทุกครั้งหลัง Phase หรือ Story ระบบจะตรวจสอบตัวเองด้วย Checklist 17 ข้อ (รวมถึง syntax, contract, dependencies, ports, accessibility, regression, ฯลฯ) และวนซ้ำภายใน 1,000 รอบจนกว่าจะไม่มีจุดบอด

---

## การจัดการ Context Window

หาก Context ใกล้เต็ม ระบบจะแนะนำให้เปิด Chat ใหม่และ resume โดยข้อมูลทั้งหมดจะถูกบันทึกใน .sdlc/context_card.json และ pipeline_state.json

---

## การปรับแต่ง

คุณสามารถแก้ .sdlc/pipeline_config.json เพื่อเปลี่ยนโหมด, เปิด Scrum, เปิด Docker, หรือปรับจำนวนการ retry

---

## ตัวอย่างการใช้งาน

ดูตัวอย่าง requirement.md สำหรับระบบจัดการเบอร์โทรศัพท์ได้ในตัวอย่างท้าย README

---

## คำถามที่พบบ่อย

**Q: ต้องใช้ API Key หรือไม่?**  
A: ไม่จำเป็น เพราะ AI Agent ใช้ Model ภายใน Editor

**Q: ใช้กับ Editor อะไรได้บ้าง?**  
A: ทุก Editor ที่มี AI Agent (Zed, Cursor, VS Code)

**Q: จะเพิ่ม Mobile หลังจาก Web เสร็จได้หรือไม่?**  
A: ได้ ระบบจะเพิ่มเฉพาะ Frontend และทดสอบ Regression ให้

**Q: Safe Auto ถามบ่อยแค่ไหน?**  
A: ถามเมื่อความมั่นใจต่ำกว่า 70% หรือเรื่องสำคัญ เช่น Architecture, Security

---

## เปลี่ยน Requirement เป็นผลงาน เพราะคุณสมควรได้เห็นซอฟต์แวร์ที่ใช้งานได้ตั้งแต่เนิ่น ๆ

Made with love by the AI SDLC Autopilot Framework v2.3.0
