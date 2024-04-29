# YBKY saralash bosqichi topshirig'i

Impactt co-working markazi rezidentlariga majlis xonalarni oldindan oson band qilish uchun tizim yaratmoqchi va bunda sizning yordamingiz kerak.

Backend yo'nalishiga topshirganlar tizim uchun REST API tuzishi kerak bo'ladi. Frontend yo'nalishi qatnashchilaridan esa ushbu tizim uchun foydalanuvchi interfeysini yasash kutiladi.

## Tizimning funksional talablari:

- Xonalar haqida ma'lumot saqlash va taqdim qila olish;
- Xonani ko'rsatilgan vaqt oralig'i uchun band qila olish;
- Bir xonaning band qilingan vaqtlari ustma-ust tushmasligi kerak;
- Autentifikatsiya (login) imkoniyatini qo'shish talab qilinmaydi.

## Mavjud xonalarni olish uchun API

```
GET /api/rooms
```

Parametrlar:

- `search`: Xona nomi orqali qidirish
- `type`: xona turi bo'yicha saralash (`focus`, `team`, `conference`)

HTTP 200

```json
{
  "count": 3,
  "results": [
    {
      "id": 1,
      "name": "mytaxi",
      "type": "focus",
      "capacity": 1
    },
    {
      "id": 2,
      "name": "workly",
      "type": "team",
      "capacity": 5
    },
    {
      "id": 3,
      "name": "express24",
      "type": "conference",
      "capacity": 15
    }
  ]
}
```

---

## Xonani id orqali olish uchun API

```
GET /api/rooms/{id}
```

HTTP 200

```json
{
  "id": 3,
  "name": "express24",
  "type": "conference",
  "capacity": 15
}
```

HTTP 404

```json
{
  "error": "topilmadi"
}
```

---

## Xonaning bo'sh vaqtlarini olish uchun API

```
GET /api/rooms/{id}/availability
```

Parametrlar:

- `date`: sana (ko'rsatilmasa bugungi sana olinadi)

Response 200

```json
[
  {
    "start": "05-06-2024 9:00:00",
    "end": "05-06-2024 11:00:00"
  },
  {
    "start": "05-06-2024 13:00:00",
    "end": "05-06-2024 18:00:00"
  }
]
```

---

## Xonani band qilish uchun API

```
POST /api/rooms/{id}/book
```

```json
{
  "resident": {
    "name": "Anvar Sanayev"
  },
  "start": "05-06-2024 9:00:00",
  "end": "05-06-2024 10:00:00"
}
```

---

HTTP 201: Xona muvaffaqiyatli band qilinganda

```json
{
  "message": "xona muvaffaqiyatli band qilindi"
}
```

HTTP 410: Tanlangan vaqtda xona band bo'lganda

```json
{
  "error": "uzr, siz tanlagan vaqtda xona band"
}
```
