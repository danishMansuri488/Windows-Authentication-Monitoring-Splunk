# SPL Queries – Windows Authentication Monitoring Dashboard

This document contains all the SPL queries used in this project along with their purpose, explanation, and expected output.

---

# Query 1 – Total Successful Logins

## Objective

Display the total number of successful login events.

## SPL Query

```spl
index=main EventCode=4624
| stats count
```

## Query Explanation

### index=main

Searches the Windows Security logs stored in the **main** index.

### EventCode=4624

Filters only **Successful Login** events.

### |

The pipe operator sends the search results to the next command.

### stats

Used to calculate statistics.

### count

Counts the total number of successful login events.

## Expected Output

```
count
1056
```

## SOC Use Case

SOC analysts use this query to monitor the number of successful user authentications.

---

# Query 2 – Total Failed Logins

## Objective

Display the total number of failed login attempts.

## SPL Query

```spl
index=main EventCode=4625
| stats count
```

## Query Explanation

### EventCode=4625

Filters only failed login events.

### stats count

Counts the number of failed login attempts.

## Expected Output

```
count
45
```

## SOC Use Case

Multiple failed logins may indicate:

- Brute-force attack
- Password guessing
- User typing the wrong password

---

# Query 3 – Failed Login Trend

## Objective

Visualize failed login attempts over time.

## SPL Query

```spl
index=main EventCode=4625
| timechart count
```

## Query Explanation

### timechart

Creates a time-based graph.

### count

Counts the number of events during each time interval.

## Expected Output

A graph showing failed login attempts over time.

## SOC Use Case

Helps identify sudden spikes in failed logins.

---

# Query 4 – Most Active Host

## Objective

Find the host generating the most authentication events.

## SPL Query

```spl
index=main
| top host
```

## Query Explanation

### top

Displays the most common values.

### host

Shows which computer generated the events.

## Expected Output

| Host | Count |
|------|------:|
| Demo-PC | 560 |
| Danish_Mansuri | 320 |

## SOC Use Case

Identifies systems generating the highest amount of authentication activity.

---

# Query 5 – Successful Login Details

## Objective

Display detailed successful login events.

## SPL Query

```spl
index=main EventCode=4624
| table _time Account_Name ComputerName Logon_Type
```

## Fields

- _time → Event timestamp
- Account_Name → Logged-in user
- ComputerName → Source computer
- Logon_Type → Type of logon

## SOC Use Case

Useful during investigations to determine who logged in, when, and from which system.

---

# Query 6 – Failed Login Details

## Objective

Display detailed failed login events.

## SPL Query

```spl
index=main EventCode=4625
| table _time Account_Name ComputerName Failure_Reason
```

## SOC Use Case

Helps investigate failed authentication attempts.

---

# Query 7 – Brute Force Detection

## Objective

Detect multiple failed login attempts.

## SPL Query

```spl
index=main EventCode=4625
| stats count by Account_Name
| where count>5
```

## Query Explanation

### stats count by Account_Name

Counts failed login attempts for each user.

### where count>5

Displays only users with more than five failed login attempts.

## SOC Use Case

Detects possible brute-force attacks.

---

# Windows Event IDs

| Event ID | Description |
|----------|-------------|
| 4624 | Successful Login |
| 4625 | Failed Login |

---

# Skills Demonstrated

- SPL Query Writing
- Windows Event Log Analysis
- Dashboard Development
- Security Monitoring
- Authentication Monitoring
- Basic Threat Detection
- Alert Creation
