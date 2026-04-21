# Technical Documentation — College ID Card Portal

## Problem Statement
Indian colleges run a manual, fragmented ID card process:
- Paper forms or Google Forms for data collection
- Manual card design in Canva / Photoshop
- 2–3 week turnaround
- Breaks down without internet

## Solution Architecture
A single self-contained HTML file with two user roles,
complete offline functionality, and automated PDF generation.

## System Flow

[Student Login] → [Batch Selection] → [Form Filling]
      ↓
[Live Preview] → [PDF Download] → [Print]

[Admin Login] → [Student Management] → [Bulk PDF Generation]

## Core Modules

### 1. Authentication Module
- Role-based login (student / admin)
- Admin credentials stored in localStorage settings
- Student passwords managed by admin

### 2. Data Management Module
- All data in localStorage under key: idportal_v2
- Schema:
  {
    students: { [prn]: { name, dob, blood, mobile, email,
                         address, photo, batch, password } },
    settings: { college, course, adminUser, adminPass }
  }

### 3. PDF Generation Module
- Library: pdf-lib (embedded, no CDN)
- Card dimensions: 243pt × 153pt (CR80 ratio)
- Fonts: Helvetica, Helvetica-Bold, Courier-Bold (StandardFonts)
- Photo embedding: embedJpg() with base64 conversion
- Why pdf-lib over jsPDF: Standard fonts render correctly
  in all PDF viewers; jsPDF caused emoji rendering failures

### 4. QR Code Module
- Library: QRCode.js (embedded canvas-based)
- Encodes JSON payload:
  { prn, name, batch, blood, college, course, mobile, email }
- Scannable by any smartphone camera without an app

### 5. Export Module
- CSV export: manual string building, Blob download
- Photo ZIP: JSZip library, async blob generation
- Bulk PDF: sequential async generation per student

### 6. Print Module
- @media print CSS hides everything except #printArea
- Card cloned into printArea before window.print()
- Page size: A4, card size: 85.6mm × 54mm
- print-color-adjust: exact preserves colors

## Key Technical Decisions

| Decision | Chosen | Rejected | Reason |
|----------|--------|----------|--------|
| PDF Library | pdf-lib | jsPDF | jsPDF broke on emoji |
| Storage | localStorage | IndexedDB | Simpler, sufficient |
| Fonts | StandardFonts | Google Fonts | Must work offline |
| Architecture | Single HTML | Multi-file | Zero setup for judges |
| Framework | Vanilla JS | React/Vue | No build step needed |

## Browser Compatibility
- Chrome 90+ ✅ (recommended)
- Firefox 88+ ✅
- Edge 90+ ✅
- Safari 14+ ✅ (minor layout differences)
- Mobile browsers ✅ (responsive layout)

## Limitations
- localStorage limit: ~5MB per origin (limits photo storage)
- No multi-device sync (by design — offline first)
- No server-side backup
- PDF generation may be slow for 100+ students on older hardware

## Future Scope
- IndexedDB for larger storage capacity
- Export / import full data as encrypted JSON backup
- Biometric QR verification at gate
- Integration with college ERP systems
- Progressive Web App (PWA) for installation
