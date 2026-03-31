**1\. architecture\_spec.md**

```
# ข้อกำหนดสถาปัตยกรรม (Architecture Specification)

**ชื่อโปรเจกต์:** Animal-AI Network Simulator  
**วิชา:** [ใส่รหัสวิชาและชื่อวิชา] – โปรเจกต์เทอม ป.ตรี สาขาวิทยาการคอมพิวเตอร์  
**ทีม:** 5 คน (Architect, Engineer, Specialist, DevOps, Tester/QA)  
**ระยะเวลา:** 4 สัปดาห์ (หนึ่ง sprint)  
**เวอร์ชันเอกสาร:** 1.0  
**วันที่:** [ใส่วันที่ปัจจุบัน]  
**จัดทำโดย:** Architect (ร่วมกับทีม)

## 1. ภาพรวมและวัตถุประสงค์ของโปรเจกต์
โปรเจกต์นี้พัฒนาเว็บแอปพลิเคชันจำลอง (simulator) แนวคิด Animal–AI Network ที่เสนอในรายงานกลุ่ม  
ผู้ใช้สามารถอัปโหลดข้อมูลจำลองจากสัตว์ (ไฟล์เสียง .wav, CSV การเคลื่อนไหว, JSON สัญญาณชีวภาพ)  
แล้วระบบจะใช้ AI แปลข้อมูลดิบเป็นความหมายเชิงความหมาย (semantic interpretation) เช่น  
- ความเครียดสูง → เตือนภัย  
- หิว → แนะนำให้อาหาร  
- การประสานงาน → แสดงพฤติกรรมร่วมกัน  

แสดงผลตาม 3 Use Case หลักจากรายงาน:  
- Wildlife Communication Network (สัตว์ป่า)  
- Smart Livestock Network (สัตว์เศรษฐกิจ)  
- Companion Animal Network (สัตว์เลี้ยง)

**คุณสมบัติที่ไม่เกี่ยวกับฟังก์ชัน (Non-Functional Requirements)**  
- ใช้งานได้บนเว็บเบราว์เซอร์ทั่วไป (responsive)  
- Deploy ฟรีได้ (Vercel + Render)  
- ใช้เวลาไม่เกิน 200–250 ชั่วโมงมนุษย์  
- โค้ดอ่านง่าย แยกส่วนชัดเจน มีเอกสาร  
- ความปลอดภัยพื้นฐาน (ป้องกัน input injection, ไม่ hard-code ความลับ)

## 2. รูปแบบสถาปัตยกรรมและการตัดสินใจเทคโนโลยี
- **รูปแบบหลัก:** Client-Server แบบ Layered (REST API + MVC)  
- **Frontend:** React 18 + Vite + TypeScript + Tailwind CSS  
- **Backend:** FastAPI (Python) – เหมาะกับการเชื่อม AI/ML  
- **AI/ML:** scikit-learn + librosa (สำหรับเสียง) หรือ rule-based + Hugging Face model เล็ก ๆ  
- **ฐานข้อมูล:** SQLite (พัฒนา) → PostgreSQL บน Supabase (production)  
- **การยืนยันตัวตน:** JWT แบบง่าย (สำหรับ demo เท่านั้น)  
- **การ deploy:** Vercel (frontend) + Render (backend + DB)  

**เหตุผลที่เลือก stack นี้**  
- นักศึกษาส่วนใหญ่คุ้นเคย  
- เร็วในการทำ prototype  
- มี hosting ฟรีเพียงพอสำหรับการสาธิต  
- รองรับการทำงานกับ AI ได้ดี

## 3. ภาพรวมส่วนประกอบระดับสูง (High-Level Diagram)
[ผู้ใช้ – Browser] ── HTTPS ── [Frontend: React]
│
▼
[Backend: FastAPI REST API]
│
┌─────────┼─────────┐
▼         ▼         ▼
[AI Semantic Interpreter]  [Mock Data Service]
│
▼
[Database: SQLite / PostgreSQL]
text**รายละเอียดส่วนประกอบ**

**Frontend**  
- หน้าหลัก: Home, เลือก Use Case (3 แท็บ), อัปโหลดข้อมูล, แสดงผลวิเคราะห์, เกี่ยวกับโปรเจกต์  
- State management: Zustand หรือ Context  
- UI: Tailwind + shadcn/ui

**Backend**  
- Endpoint หลัก: `/api/upload`, `/api/analyze`, `/api/results`  
- Service: `semantic_interpreter.py` (ส่วนหลักของ Specialist)

**AI Semantic Interpreter**  
- รับ: เสียง (.wav), CSV การเคลื่อนไหว, JSON สัญญาณชีวภาพ  
- ประมวลผล: librosa + scikit-learn (หรือ rule-based หากโมเดลหนักเกิน)  
- ส่งออก: JSON เช่น {"meaning": "high stress", "confidence": 0.82, "action": "แจ้งเตือน"}

**ฐานข้อมูล**  
- ตารางหลัก: users, sessions, analysis_results (เก็บข้อมูลดิบ + ผลลัพธ์)

## 4. ตัวอย่าง Data Flow (Companion Animal)
1. ผู้ใช้เลือก "สัตว์เลี้ยง" → อัปโหลดเสียงเห่าของหมา  
2. Frontend ส่งไฟล์ไป POST /api/analyze  
3. Backend รัน AI interpreter → ส่งกลับ {"emotion": "happy", "confidence": 0.87, "action": "เล่นกับเขาเถอะ"}  
4. Frontend แสดงข้อความ + กราฟง่าย ๆ

## 5. ข้อจำกัดและการตัดสินใจยอมรับ
- ไม่ทำ real-time multi-agent (ซับซ้อนเกิน 4 สัปดาห์)  
- ใช้ข้อมูลจำลองแทนเซ็นเซอร์จริง  
- โมเดล AI ง่าย ๆ (ไม่ train เอง)  
- เน้น semantic interpretation ไม่ได้ทำโปรโตคอลเครือข่ายใหม่จริง ๆ

## 6. ความเสี่ยงและแนวทางรับมือ

| ความเสี่ยง                        | โอกาสเกิด | ผลกระทบ | แนวทางรับมือ                          |
|-----------------------------------|-----------|---------|---------------------------------------|
| ความแม่นยำของ AI ต่ำ              | ปานกลาง   | สูง     | มี fallback แบบ rule-based + ระบุข้อจำกัด |
| การอัปโหลดไฟล์ช้า / ขนาดใหญ่      | ต่ำ       | ปานกลาง | จำกัดขนาดไฟล์ 5 MB                   |
| สมาชิกในทีมลา / เจ็บป่วย          | ปานกลาง   | สูง     | Cross-training ตั้งแต่สัปดาห์ 1     |
| ขอบเขตกว้างเกินไป                 | สูง       | สูง     | กำหนด MVP ชัดเจนตั้งแต่ต้น           |

**อนุมัติ**  
Architect: ___________________ Engineer: ___________________ วันที่: ________
```

