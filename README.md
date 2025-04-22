
# Hostel Outing Request Automation using WhatsApp Chatbot & n8n

## 📘 Project Overview

This project automates the student outing request process in a college hostel environment using WhatsApp, n8n workflows, Google Sheets, and QR code verification. It is designed to streamline the process of raising, approving, and tracking student outings while ensuring safety, transparency, and operational efficiency.

## 🎯 Objective

To build a seamless, secure, and automated system that allows students to request outing permissions and ensures timely approvals from parents and wardens, while providing an easy mechanism for gate verification using QR codes.

## 🧰 Tech Stack

- **n8n** (Workflow automation platform)
- **WhatsApp Cloud API** (for messaging and approvals)
- **Google Sheets API** (for data storage and logging)
- **QRServer API** (for generating QR codes)
- **Webhook** (for gate scan logging)

## 📁 Google Sheets Structure

### 1. **Student Database Sheet**

| Column             | Description                         |
|--------------------|-------------------------------------|
| Student Name       | Full name of the student            |
| Phone Number       | Student's WhatsApp number           |
| Parent Name        | Parent’s name                       |
| Parent Number      | Parent's WhatsApp number            |
| Hostel Name        | Hostel name                         |
| Warden Number      | Warden's WhatsApp number            |
| Student ID         | Unique student ID (Register No.)    |
| Current Status     | In/Out                              |

### 2. **Outing Requests Sheet**

| Column             | Description                         |
|--------------------|-------------------------------------|
| Name               | Student name                        |
| From               | Outing start date                   |
| To                 | Outing end date                     |
| Reason             | Reason for outing                   |
| Approval Status    | Pending/Approved/Rejected           |
| Student ID         | Unique identifier                   |

### 3. **In and Out Logs Sheet**

| Column             | Description                         |
|--------------------|-------------------------------------|
| Register No        | Student ID                          |
| Name               | Student name                        |
| In/Out             | Entry or Exit                       |
| Time               | Timestamp of the scan               |

## 🔄 Workflow Breakdown

### 1. **Student Sends Message**

- Trigger: WhatsApp Cloud API.
- Bot identifies student using phone number linked in Google Sheet.

### 2. **Bot Collects Request Info**

- Gathers: Outing dates (From/To), Reason.
- Confirms details with the student.

### 3. **Approval Sequence**

- Parent receives WhatsApp message → taps to approve or deny.
- If approved, Warden receives the same request.
- If both approve, status updated to `Approved`.

### 4. **QR Code Generation**

- QR Code generated using QRServer API.
- QR data contains student ID + outing date.
- Bot sends QR as a permission card.

### 5. **QR Code Scan at Gate**

- Webhook receives scan → checks QR validity.
- Matches with approved requests in sheet.
- Logs the event (In/Out) in the system.
- Sends notification to student and parent.

## 📷 System Implementation Screenshots

> 🖼️ **Student WhatsApp Chat with Bot**  
<img title="a title" alt="Alt text" src="Screenshots\Student Chat.jpg">  

> 🖼️ **Approval Flow in n8n**  
> <img title="a title" alt="Alt text" src="Screenshots\n8n workflow-1.jpg">
[View PDF](./n8n%20workflow.pdf)  

> 🖼️ **Outing Request Form**
> <img title="a title" alt="Alt text" src="Screenshots\Outing request form.jpg">  

> 🖼️ **Spreadsheet**  
  > [View Spread sheet](https://docs.google.com/spreadsheets/d/11OyOqkj_BNrO477fXvTK44QyW5U9TswZksE1vsnwuc8/edit?usp=sharing)  
> **Student Database Sheet**  
> <img title="a title" alt="Alt text" src="Screenshots\Excel sheet db.png">  
> **Outing Requests Sheet**  
> <img title="a title" alt="Alt text" src="Screenshots\Excel sheet approval requests.png">  
> **in and out logs**  
><img title="a title" alt="Alt text" src="Screenshots\Excel sheet in and out logs.png">  

> 🖼️ **Parent whatsapp chat window**  
> <img title="a title" alt="Alt text" src="Screenshots\Parent chat screenshot.png">

> 🖼️ **Warden whatsapp chat window**  
> <img title="a title" alt="Alt text" src="Screenshots\warden chat.jpg">  

> 🖼️ **Gate Scanner Interface**  
> <img title="a title" alt="Alt text" src="Screenshots\Scanner Interface.png">

## ⚠️ Error Handling

- **Invalid Phone Numbers**: Bot responds with “You're not registered. Please contact the warden.”
- **Timeout from Parents or Wardens**: Auto-reject request after 24 hours or configurable timeout.
- **Unmatched QR Codes at Gate**: Show message “Invalid or expired QR code.”
- **Duplicate Requests**: Prevent new request if one is already `Pending` or `Approved`.
- **Approval Rejection**: If either Parent or Warden rejects, notify student and stop the flow.

## 🧪 Edge Cases to Consider

- Student sending incomplete details.
- Request raised with overlapping date range.
- Parent or Warden unavailable (alternate contact mechanism).
- Multiple outing requests submitted before approval.
- QR code reused or forged (use token-based expiry).
- Internet issues causing delayed webhook triggers.  

## 🔗 External Services Used

- [QR Server API](https://goqr.me/api/)
- [n8n](https://n8n.io/)
- [Google Sheets](https://sheets.google.com)
- [WhatsApp Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api)

## 📝 Developer Notes

- Maintain data` integrity by always updating sheets through n8n.
- Use expression-based mapping in n8n to avoid hardcoding.
- Add retry mechanism for failed WhatsApp API calls.
- Use webhook testing tools like Postman for local testing.

## 📈 Future Enhancements

- Email-based backup notification system.
- Admin dashboard using Google Data Studio or Firebase.
- OTP-based parent/warden verification.
- Daily and weekly reports to admin.
- Integration with RFID systems at gate.

## 👨‍💻 Maintainer

**Haswanth Kumar Kurevella**  
Email: <haswanthkurevella1@gmail.com>
Domain: Workflow Automation | Chatbots | Campus Tech
