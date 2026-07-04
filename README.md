# กินไรดีนะ

เว็บช่วยตัดสินใจว่า "วันนี้กินอะไรดี?" ด้วยการปัดเลือกเมนูให้เข้ารอบ 3 รายการ แล้วสุ่มหรือเลือกผู้ชนะในรอบสุดท้าย

ลองเล่นได้ที่: [what-should-we-eat-ten.vercel.app](https://what-should-we-eat-ten.vercel.app)

## จุดเด่น

- เลือกหมวดได้: สุ่มทั้งหมด, อาหาร, ของหวาน, เครื่องดื่ม
- ปัดเมนูเพื่อคัดเข้ารอบ 3 รายการ
- เลือกผู้ชนะเองหรือสุ่มจากผู้เข้ารอบ
- บันทึกเมนูโปรดและประวัติผู้ชนะด้วย `localStorage`
- รองรับหน้าจอมือถือและเดสก์ท็อป
- มี manifest และไอคอนสำหรับใช้งานเป็นเว็บแอปแบบ standalone

## เมนูในระบบ

รายการเมนูอยู่ในไฟล์ `menus.js` ตอนนี้มีทั้งหมด 300 รายการ แบ่งเป็น:

- อาหาร: 100 รายการ
- ของหวาน: 100 รายการ
- เครื่องดื่ม: 100 รายการ

เมนูแต่ละรายการมีข้อมูลหลัก เช่น `id`, `name`, `category`, `description`, `emoji`, `tags`, `priceRange`, `reason` และอาจมี `image` สำหรับรูปประกอบ

## โครงสร้างโปรเจกต์

```text
.
├── index.html          # หน้าเว็บหลัก รวม CSS และ JavaScript ของแอป
├── menus.js            # ข้อมูลเมนูทั้งหมด
├── site.webmanifest    # manifest สำหรับเว็บแอป
├── icons/              # ไอคอนแอปและ favicon
└── images/             # รูปประกอบเมนู
```

## วิธีรันในเครื่อง

โปรเจกต์นี้เป็น static site จึงไม่ต้องติดตั้ง dependencies

เปิด `index.html` ในเบราว์เซอร์ได้เลย หรือรัน local server ง่าย ๆ:

```bash
python3 -m http.server 5173
```

แล้วเปิด:

```text
http://localhost:5173
```

## วิธีเพิ่มหรือแก้เมนู

แก้ข้อมูลใน `menus.js` โดยเพิ่ม object ใน `window.MENU_ITEMS`

ตัวอย่าง:

```js
{
  "id": "new-menu-id",
  "name": "ชื่อเมนู",
  "category": "food",
  "description": "คำอธิบายสั้น ๆ",
  "emoji": "🍛",
  "tags": ["อิ่ม", "ง่าย", "คลาสสิก"],
  "priceRange": "50-90",
  "reason": "เหตุผลสนุก ๆ ตอนเมนูนี้ชนะ",
  "image": "images/new-menu-id.png",
  "imageSource": "User-provided AI-generated image",
  "imageLicense": "User-provided AI-generated asset"
}
```

ค่าของ `category` ที่ใช้ในแอป:

- `food`
- `dessert`
- `drink`

ถ้าเพิ่มรูปประกอบ ให้ใส่ไฟล์ไว้ในโฟลเดอร์ `images/` และอ้าง path ให้ตรงกับค่า `image`

## การ deploy

โปรเจกต์นี้ deploy บน Vercel จาก branch `main`

เมื่อ push commit ใหม่ขึ้น GitHub แล้ว Vercel จะสร้าง production deployment อัตโนมัติ

## หมายเหตุเรื่อง asset

รูปเมนูในโปรเจกต์ระบุเป็น user-provided AI-generated assets ตามข้อมูลใน `menus.js`
