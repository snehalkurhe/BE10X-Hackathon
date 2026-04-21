# 🎓 College ID Card Portal

A fully offline, single-file Student ID Card Management System that automates
the entire ID card pipeline — from data collection to print-ready PDF generation.

## 🚀 Quick Start
1. Download `student_idcard_system.html`
2. Open it in any modern browser (Chrome recommended)
3. No installation. No internet. No server. Just open and use.

## 🔑 Default Login
- Admin Username: admin
- Admin Password: admin123
- Student Login: PRN number + admin-assigned password

## ✨ Features
### For Students
- Role-based login (Student / Admin)
- Batch selection (2021–2026)
- Personal info form with real-time validation
- Photo upload (max 2MB)
- Live ID card preview before download
- PDF ID card download
- Print directly from browser

### For Admins
- Add students individually or bulk import via CSV
- Dashboard with batch filter and stats
- Export student data as CSV
- Export all photos as ZIP
- Generate ID cards for all students in one click
- Reset student passwords
- Customize college name and course

## 🛠 Tech Stack
- Pure HTML + CSS + JavaScript (zero frameworks)
- pdf-lib (embedded, offline) — PDF generation
- JSZip (embedded, offline) — Photo ZIP export
- QRCode.js (embedded, offline) — QR code generation
- localStorage — All data stays on device

## 📐 ID Card Specs
- Size: CR80 credit card (85.6mm × 54mm)
- Contains: College branding, student photo, all personal fields, QR code
- QR encodes: PRN, name, batch, blood group, college, mobile, email

## 🔒 Privacy
All data is stored in the browser's localStorage.
Nothing is sent to any server. Ever.

## 📁 File Structure
student_idcard_system.html — entire application (single file)
README.md — this file
DOCUMENTATION.md — detailed technical documentation
demo/ — screenshots and sample output
