# Windows Authentication Monitoring Dashboard using Splunk

## 📌 Project Overview

This project demonstrates how Splunk can be used to monitor Windows authentication events. Windows Security logs were collected using the Splunk Universal Forwarder, and an interactive dashboard was created to help detect login activity and potential security threats.

---

## 🎯 Project Objectives

- Monitor successful login attempts.
- Monitor failed login attempts.
- Identify authentication trends.
- Detect suspicious login activity.
- Create basic security alerts.

---

## 🏗️ Architecture

```
Windows System
      │
      │ Windows Security Logs
      ▼
Splunk Universal Forwarder
      │
      ▼
Splunk Enterprise
      │
      ▼
Dashboard & Alerts
```

---

## 🛠️ Technologies Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Windows Security Event Logs
- SPL (Search Processing Language)
- Windows 11

---

## 📊 Dashboard Panels

- ✅ Total Successful Logins
- ✅ Total Failed Logins
- ✅ Failed Login Trend
- ✅ Most Active Host

---

## 🔍 SPL Queries

### Successful Logins

```spl
index=main EventCode=4624
| stats count
```

### Failed Logins

```spl
index=main EventCode=4625
| stats count
```

### Failed Login Trend

```spl
index=main EventCode=4625
| timechart count
```

### Most Active Host

```spl
index=main
| top host
```

---

## 🚨 Alert

### Brute Force Detection

```spl
index=main EventCode=4625
| stats count
| where count > 5
```

---

## 🪟 Windows Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Login |
| 4625 | Failed Login |

---

## 📁 Project Structure

```
Windows-Authentication-Monitoring-Splunk/
│
├── README.md
├── Screenshots/
├── Queries/
├── Architecture/
└── Documentation/
```

---

## 📸 Screenshots

- Dashboard
- Failed Login Trend
- Successful Login Panel
- Alert Configuration

---

## 📚 Skills Learned

- Splunk Fundamentals
- SPL Queries
- Dashboard Creation
- Windows Event Log Analysis
- Security Monitoring
- Alert Configuration

---

## 👨‍💻 Author

**Danish Mansuri**

Cyber Security | SOC Analyst Aspirant
