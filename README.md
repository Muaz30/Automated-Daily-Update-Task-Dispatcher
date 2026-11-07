# Automated-Daily-Update-Task-Dispatcher
An automated end-to-end task and religious routine tracking system built for study groups and organizations. This solution automates daily Al-Quran relay progress calculations, dynamically aggregates weekly task assignments, and dispatches rich-text scheduled updates directly to WhatsApp groups without manual intervention.
 
🌟 Key Features

- **Automated Sequence & Relay Progression:** Calculates cumulative group reading progress (+15 pages/day across members) using dynamic date-offset formulas in real-time.
- **Dynamic Content Aggregation:** Blends daily auto-incremented readings with weekly static assignments (Memorization & Reading materials) into a single structured WhatsApp payload.
- **Zero-Maintenance Execution:** Scheduled daily cron triggers via Make.com eliminate manual message formatting and repetitive manual data entries.
- **Enterprise-Grade Integration:** Connects Google Sheets API directly to WhatsApp Business infrastructure via 2Chat RESTful APIs.

## 🏗 System Architecture & Workflow

[ Google Sheets Database ]
│
├── Auto-calculates daily page increments (=TODAY() - Start_Date)
├── Formats dynamic concatenated text payload (Cell M2)
│
▼
[ Make.com Automation Engine ]
│
├── Daily Scheduled Trigger (Cron Job @ 06:00 AM)
├── Fetches formatted string via Google Sheets API ("Get a Cell")
│
▼
[ 2Chat Gateway (WhatsApp API) ]
│
└── Outbound HTTP POST Broadcast to Target WhatsApp Group

## 🛠 Tech Stack & Tools

- **Automation & Integration:** Make.com (formerly Integromat)
- **API Gateway:** 2Chat WhatsApp Business API
- **Data Store & Engine:** Google Sheets (Advanced Formulas & Date/Text Functions)
- **Messaging Target:** WhatsApp Group Broadcast

---

## 📐 Data Engine & Logic Design

The core intelligence resides in the Google Sheets Data Engine, which eliminates daily manual input by computing sequence-based page offsets:

## Relay Formula Logic (Auto-Increment +15 Pages/Day)
```excel
= (Base_Start_Page + (TODAY() - $A$2) * 15) & "-" & (Base_End_Page + (TODAY() - $A$2) * 15)
```

="🗓 *" & UPPER(B2) & "*" & CHAR(10) & CHAR(10) &
"1️⃣ *Al Quran*: /3page" & CHAR(10) &
"- Member A : " & C2 & CHAR(10) &
"- Member B : " & D2 & CHAR(10) & CHAR(10) &
"2️⃣ *Hafalan Quran* = Surah / Ayat" & CHAR(10) & H2 & CHAR(10) & CHAR(10) &
"3️⃣ *Tugasan / Bahan Bacaan*" & CHAR(10) & K2

🚀 Deployment & Setup Instructions ;
**Google Sheets Configuration:**
Create a primary tracking worksheet.
Insert the reference start date in cell A2.
Apply the sequence formula across member columns.
Set cell M2 as the aggregated master output string.

**2Chat WhatsApp API Gateway:**
Link WhatsApp Business account via QR Code.
Sync target WhatsApp groups and obtain the target Group ID.
Issue bearer access tokens from the developer portal.

**Make.com Scenario Build:**
Add Google Sheets: Get a Cell module (Target Cell: M2).
Connect 2Chat: Send a Text Message to a WhatsApp Group module.
Set execution schedule trigger to Daily at 06:00 AM. 
Enable scenario and test payload delivery.

📈 Impact & Results
100% Time Reduction: Replaced 10–15 minutes of manual daily formatting and tracking with an automated background process.

Zero Human Error: Eliminates page numbering mistakes, manual typos, and forgotten broadcasts.

High Scalability: Modular architecture allows quick addition of new group members or additional data fields with zero changes to the Make.com core pipeline.

_Developed by a Computer Science Undergraduate passionate about Cloud Automations, API Integrations, and Productivity Engineering._
