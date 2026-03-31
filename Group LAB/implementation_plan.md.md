**2\. implementation\_plan.md**

```
# แผนการดำเนินงาน (Implementation Plan) – โปรเจกต์เทอม 4 สัปดาห์

**ชื่อโปรเจกต์:** Animal-AI Network 
**ขนาดทีม:** 5 คน – นักศึกษาปริญญาตรี สาขาวิทยาการคอมพิวเตอร์  
**ระยะเวลา:** 4 สัปดาห์ (หนึ่ง sprint)

## บทบาทและความรับผิดชอบ

| บทบาท          | ชื่อสมาชิก     | หน้าที่หลัก                                                                 | ผลลัพธ์หลัก                              |
|----------------|----------------|-----------------------------------------------------------------------------|------------------------------------------|
| **Architect**  | [ศุภกร กรมรินทร์]         | ออกแบบภาพรวม, เลือกเทคโนโลยี, เขียนเอกสารสถาปัตยกรรม                       | architecture_spec.md, ไดอะแกรมส่วนประกอบ |
| **Engineer**   | [ณภัทร อรัญพูล]         | เขียนโค้ดหลัก (backend + frontend), เชื่อมต่อระบบ                   | API endpoints, หน้า UI หลัก              |
| **Specialist** | [ณัฐกรณ์ อันธิสาร]         | พัฒนาโมดูล AI semantic interpreter, แมปกับ 3 Use Case                      | semantic_interpreter.py + ตรรกะ 3 use case |
| **DevOps**     | [ณัชพล เพ็งพล]         | ตั้งค่า repository, CI/CD, deploy, จัดการ environment                      | GitHub Actions, URL สำหรับสาธิต           |
| **Tester/QA**  | [ธนินธร อันทรบุตร]         | เขียน test plan, unit/integration test, ทดสอบด้วยมือ, ติดตามบั๊ก            | เอกสาร test cases, รายงาน coverage, bug log |

## ไทม์ไลน์ 4 สัปดาห์

**สัปดาห์ 0 (เตรียมการ – ก่อนเริ่มอย่างเป็นทางการ)**  
- Kick-off ทีม + แบ่งบทบาท  
- กำหนดขอบเขต MVP (3 use case, อัปโหลด + แปล semantic)  
- Architect ส่ง draft architecture_spec.md  
- DevOps สร้าง repo + CI พื้นฐาน (lint + test)

**สัปดาห์ 1 – สร้างโครงสร้างพื้นฐาน**  
เป้าหมาย: มีแอปวิ่งได้ + อัปโหลดไฟล์แล้วตอบกลับ dummy  
- Architect: เสร็จ architecture_spec.md + วาดไดอะแกรม  
- Engineer: ตั้งค่า FastAPI + React skeleton + auth พื้นฐาน  
- Specialist: วิจัยและทำ prototype โมเดลจำแนกเสียงเบื้องต้น  
- DevOps: Deploy frontend & backend ว่าง ๆ ขึ้น Vercel + Render  
- Tester/QA: เขียน test plan + unit test ชุดแรก  
**Demo สิ้นสัปดาห์:** อัปโหลดไฟล์ได้ และได้ JSON ตอบกลับ

**สัปดาห์ 2 – ฟีเจอร์หลัก + เชื่อม AI**  
เป้าหมาย: 3 use case ทำงานได้จริง  
- Engineer: เขียน endpoint หลัก + หน้า dashboard  
- Specialist: สร้าง semantic interpreter เต็มรูปแบบ + แมป 3 use case  
- DevOps: เพิ่ม env variables + GitHub Actions (build & deploy อัตโนมัติ)  
- Tester/QA: unit test API + เริ่มทดสอบด้วยมือ  
**Demo สิ้นสัปดาห์:** ทุก use case แปลความหมายได้

**สัปดาห์ 3 – ปรับแต่ง + แก้บั๊ก**  
เป้าหมาย: คุณภาพใกล้ production  
- Engineer: จัดการ error, responsive, validation  
- Specialist: ปรับปรุง logic AI + เพิ่ม confidence score  
- DevOps: เพิ่ม monitoring พื้นฐาน + README มี URL  
- Tester/QA: ทดสอบเต็มรูปแบบ + แก้บั๊กวนไปวนมา  
- ทั้งทีม: ปรับ UI/UX ให้สวยงาม  
**Demo สิ้นสัปดาห์:** แอปใช้งานได้ดี ดูเป็นมืออาชีพ

**สัปดาห์ 4 – ส่งงาน + นำเสนอ**  
เป้าหมาย: เสร็จสมบูรณ์และนำเสนอ  
- Engineer + Specialist: แก้บั๊กสุดท้าย + optimize  
- DevOps: Deploy สุดท้าย + เขียนเอกสาร  
- Tester/QA: รายงาน test สุดท้าย (coverage ≥ 65%)  
- Architect: อัปเดต architecture_spec.md ให้ตรงกับของจริง  
- ทั้งทีม: ถ่ายวิดีโอ demo 3–5 นาที + สไลด์ + รายงานฉบับสมบูรณ์  
**สิ่งที่ต้องส่ง:** URL สาธิต, GitHub repo, เอกสารทั้งสองไฟล์, วิดีโอ, สไลด์

## เครื่องมือและแนวปฏิบัติที่แนะนำ
- Version Control: GitHub (main + feature branches)  
- การจัดการงาน: GitHub Projects (Kanban)  
- สื่อสาร: Line / Discord + standup 10 นาทีทุกวัน  
- คุณภาพโค้ด: Black (Python), ESLint + Prettier (JS/TS), PR review  
- การทดสอบ: pytest (backend), Vitest (frontend)

## ความเสี่ยงและแผนสำรอง
- AI ช้าเกิน → ใช้ rule-based แทน + อธิบายข้อจำกัด  
- Deploy มีปัญหา → มีวิดีโอ localhost สำรอง  
- ขอบเขตกว้างเกิน → ตัด use case ใด use case หนึ่งในสัปดาห์ 2

**คำมั่นสัญญาของทีม**  
เราจะส่งมอบโปรเจกต์ที่ทำงานได้ มีเอกสารครบ และสาธิตได้ ภายในสิ้นสัปดาห์ที่ 4  

ลงชื่อ: [
	ณภัทร อรัญพูล 
	ธนินธร อันทรบุตร 
	ศุภกร กรมรินทร์ 
	ณัชพล เพ็งพล 
	ณัฐกรณ์ อินธิสาร 
]  
**อัปเดตล่าสุด:** [2026-02-28]

```

