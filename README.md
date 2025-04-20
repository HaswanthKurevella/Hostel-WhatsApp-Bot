# Hostel Outing Request Bot (n8n + WhatsApp)

## 📌 Overview
This project automates the student outing request process in a college environment using WhatsApp chatbot, Google Sheets as a database, and QR code-based entry/exit tracking. It facilitates seamless communication and approval flow between students, parents, and wardens.

---

## 🛠️ Tech Stack
- **n8n** – Workflow automation platform
- **WhatsApp Cloud API** – Messaging interface
- **Google Sheets** – Data storage
- **QR Server API** – QR code generation
- **Webhook** – For gate in/out scan logging

---

## 📁 Google Sheets Structure

### Sheet1 (Student Database)
| Column Name        | Description                  |
|--------------------|------------------------------|
| Student Name       | Full name of the student     |
| Phone Number       | Student's WhatsApp number    |
| Parent Name        | Parent's name                |
| Parent Number      | Parent's WhatsApp number     |
| Hostel Name        | Hostel student resides in    |
| Warden Number      | Warden's WhatsApp number     |
| Student ID         | Unique ID (Register number)  |
| Current Status     | In/Out                       |

### Requests
| Column Name       | Description                    |
|-------------------|--------------------------------|
| Name              | Student name                   |
| From              | Outing start date              |
| To                | Outing end date                |
| Reason            | Reason for outing              |
| Approval status   | Submitted / Approved / Rejected|
| Student ID        | Unique identifier              |

### In and Out Log
| Column Name       | Description            |
|-------------------|------------------------|
| Register No       | Student ID             |
| Name              | Student name           |
| In/out            | In or Out              |
| Time              | Timestamp of the event |

---

## 🔄 Workflow Logic

### 1. WhatsApp Trigger
- Initiated when a student sends a message to the bot.
- Student verified against phone number in Sheet1.

### 2. Booking & Form Collection
- Bot sends a form to collect: `From`, `To`, `Reason for outing`.

### 3. Confirmation
- Details shown back to student for approval.
- If confirmed, moves to approval phase.

### 4. Approval Workflow
- Request logged in **Requests** sheet.
- Approval requested from **Parent** → If approved → proceed to **Warden**.
- If both approve, status marked `Approved`.

### 5. QR Code Generation
- QR code generated using QRServer API with Student ID as data.
- QR code uploaded and sent to student on WhatsApp.

### 6. Gate Logging (Webhook)
- Webhook receives scan request from gate.
- Validates QR + date range + approval.
- Logs data in **In and Out Log**.
- Sends WhatsApp notifications to student and parent.

---

## 🧪 Testing and Demo
- Use sample numbers and entries in Sheets.
- Run through all paths: approved, parent rejected, warden rejected.
- Use Postman or curl to simulate webhook calls.

---

## 🔒 Authentication
- WhatsApp API token configured via credentials in n8n.
- Google Sheets linked via OAuth2.

---

## 📈 Future Enhancements
- OTP-based verification for security
- Email fallback system
- Admin dashboard with filters
- Weekly activity reports to hostel heads

---

## 👨‍💻 Developer Notes
- Keep sheet columns fixed as mapped in n8n.
- Use pinned test data in n8n for simulations.
- All data mapping is dynamic using expressions.

---

## 🔗 External Services Used
- [QR Server API](https://goqr.me/api/)
- [n8n](https://n8n.io/)
- [Google Sheets](https://sheets.google.com)
- [WhatsApp Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api)

---

> Project maintained by: **Haswanth Kumar Kurevella**
> For any issues or help, contact: `haswanthkurevella@gmail.com`
