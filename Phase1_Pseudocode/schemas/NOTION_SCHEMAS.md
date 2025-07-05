# 📋 Notion Database Schemas - Implementation Guide

## Overview
This document provides exact Notion database schemas ready for implementation, including property configurations, formulas, and relations.

---

## 🚀 Implementation Order

1. **Subject Master** (no dependencies)
2. **Goals Hierarchy** (depends on Subject Master)
3. **Daily Actions** (depends on Goals)
4. **Daily Learning Sessions** (depends on Subject, Actions)
5. **Journal Entries** (depends on Sessions)
6. **Process Library** (depends on Subject)
7. **Achievements** (standalone)
8. **Progress Snapshots** (depends on all)
9. **Learning Investments** (depends on Subject)
10. **Notification Queue** (depends on Subject, Actions)

---

## 📊 Database 1: Subject Master

### Notion Setup Instructions
1. Create new database: "📚 Subject Master"
2. Add properties in this exact order:

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Subject Name          | Title             | Default
Category              | Select            | Options: Language, Finance, Philosophy, Programming, Art, Other
Current Status        | Select            | Options: Active, Paused, Completed, Planning (Default: Active)
Priority Level        | Select            | Options: Primary Focus, Secondary, Maintenance, Future
Date Started          | Date              | Date format: Month day, year
Target Completion     | Date              | Date format: Month day, year
Current Level         | Number            | Number format: Number
Total XP              | Number            | Number format: Number
Current Streak        | Number            | Number format: Number
Best Streak           | Number            | Number format: Number
Last Studied          | Date              | Date format: Relative
Auto-Pause Warning    | Formula           | See formula below
Color Theme           | Select            | Options: 🔴 Red, 🟠 Orange, 🟡 Yellow, 🟢 Green, 🔵 Blue, 🟣 Purple
Resources             | URL               | Default
Money Invested        | Number            | Number format: Dollar
Goal Statement        | Text              | Default
Daily Minimum         | Number            | Number format: Number (Default: 15)
Flashcard Target      | Number            | Number format: Number (Default: 10)
Last Increase         | Date              | Date format: Month day, year
Next Increase Date    | Formula           | See formula below
Synergy Subjects      | Relation          | Relation to: Subject Master, No limit
```

### Formulas

**Auto-Pause Warning:**
```
if(
  dateBetween(now(), prop("Last Studied"), "days") > 5, 
  "⚠️ Auto-pause in " + format(7 - dateBetween(now(), prop("Last Studied"), "days")) + " days", 
  "✅"
)
```

**Next Increase Date:**
```
if(
  empty(prop("Last Increase")),
  dateAdd(prop("Date Started"), 14, "days"),
  dateAdd(prop("Last Increase"), 14, "days")
)
```

---

## 📊 Database 2: Goals Hierarchy

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Goal Title            | Title             | Default
Goal Type             | Select            | Options: Yearly, Quarterly, Monthly, Weekly, Daily
Parent Goal           | Relation          | Relation to: Goals Hierarchy, No limit
Subject               | Relation          | Relation to: Subject Master, Limit 1
Target Date           | Date              | Date format: Month day, year
Created Date          | Created time      | Date format: Month day, year
Status                | Select            | Options: Not Started, In Progress, Completed, Paused, Cancelled
Priority              | Select            | Options: 🔥 Critical, ⚡ High, 🔄 Normal, 💤 Low
Success Metrics       | Text              | Default
Decomposition Notes   | Text              | Default
Estimated Hours       | Number            | Number format: Number
Subgoals              | Relation          | Create new property in Goals Hierarchy
Total Subgoals        | Rollup            | Relation: Subgoals, Property: Goal Title, Calculate: Count
Completed Subgoals    | Rollup            | Relation: Subgoals, Property: Status, Calculate: Count, Filter: Status is Completed
Progress Percentage   | Formula           | See formula below
Actual Hours          | Rollup            | Relation: Sessions, Property: Duration, Calculate: Sum
```

**Progress Percentage Formula:**
```
if(
  prop("Goal Type") == "Daily",
  if(prop("Status") == "Completed", 100, 0),
  if(
    prop("Total Subgoals") > 0,
    round(100 * prop("Completed Subgoals") / prop("Total Subgoals")),
    0
  )
)
```

---

## 📊 Database 3: Daily Actions

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Action Title          | Title             | Default
Parent Goal           | Relation          | Relation to: Goals Hierarchy, Limit 1
Subject               | Relation          | Relation to: Subject Master, Limit 1
Action Type           | Select            | Options: Study, Practice, Review, Create, Test
Estimated Time        | Number            | Number format: Number (minutes)
Scheduled Date        | Date              | Date format: Month day, year
Completion Status     | Checkbox          | Default
Completed Date        | Date              | Date format: Month day, year
Recurring             | Checkbox          | Default
Recurrence Pattern    | Select            | Options: Daily, Weekdays, Weekly, Custom
Difficulty Points     | Number            | Number format: Number (1-5)
Instructions          | Text              | Default
Success Criteria      | Text              | Default
Reminder Sent         | Checkbox          | Default
Reminder Time         | Select            | Options: 09:30, 15:00, 19:00, Custom
Bumped Count          | Number            | Number format: Number (Default: 0)
Sessions              | Relation          | Create new property in Daily Learning Sessions
Actual Time           | Rollup            | Relation: Sessions, Property: Duration, Calculate: Sum
```

---

## 📊 Database 4: Daily Learning Sessions

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Session ID            | Formula           | See formula below
Session Date          | Date              | Date format: Month day, year
Subject               | Relation          | Relation to: Subject Master, Limit 1
Session Type          | Multi-select      | Options: Flashcards, Reading, Writing, Speaking, Listening, Practice Problems, Video, Other
Start Time            | Date              | Include time: ON
End Time              | Date              | Include time: ON
Duration              | Formula           | See formula below
Focus Quality         | Select            | Options: 🎯 Deep Focus, 👍 Normal, 😕 Distracted
Energy Level          | Select            | Options: ⚡ High, 🔄 Medium, 😴 Low
Session Notes         | Text              | Default
Tasks Completed       | Relation          | Relation to: Daily Actions, No limit
Breakthroughs         | Text              | Default
Struggles             | Text              | Default
XP Earned             | Formula           | See formula below
Streak Maintained     | Checkbox          | Default
Materials Used        | Multi-select      | Options: Textbook, App, Video, Flashcards, Notebook, AI Tool, Other
Location              | Select            | Options: Home, Library, Cafe, Office, Transit, Other
Journal Entry         | Relation          | Create new property in Journal Entries
```

### Session Formulas

**Session ID:**
```
formatDate(prop("Session Date"), "YYYY-MM-DD") + "-" + 
slice(prop("Subject"), 0, 3) + "-" + 
format(toNumber(prop("Duration")))
```

**Duration:**
```
if(
  and(not(empty(prop("Start Time"))), not(empty(prop("End Time")))),
  dateBetween(prop("End Time"), prop("Start Time"), "minutes"),
  0
)
```

**XP Earned:**
```
round(
  prop("Duration") * 
  if(prop("Focus Quality") == "🎯 Deep Focus", 1.5, 1) *
  min(1 + (toNumber(prop("Subject.Current Streak")) * 0.1), 2) +
  sum(prop("Tasks Completed.Difficulty Points")) * 10
)
```

---

## 📊 Database 5: Journal Entries

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Entry Title           | Formula           | formatDate(prop("Date"), "YYYY-MM-DD") + " Journal"
Date                  | Date              | Date format: Month day, year (UNIQUE)
Tasks Completed       | Text              | Default
Random Thoughts       | Text              | Default
Todo Tomorrow         | Text              | Default
Reflections           | Text              | Default
Mood                  | Select            | Options: 😊 Energized, 👍 Focused, 😐 Neutral, 😔 Struggled, 🔥 Breakthrough
Key Insights          | Text              | Default
Hidden TODOs          | Text              | Default
Epiphany Section      | Text              | Default (AI-filled)
AI Analysis Complete  | Checkbox          | Default
Summary Sent          | Checkbox          | Default
Calendar Events       | Text              | Default
Energy Pattern        | Text              | Default (AI-filled)
Sessions Today        | Relation          | Relation to: Daily Learning Sessions, No limit
Total Time Today      | Rollup            | Relation: Sessions Today, Property: Duration, Calculate: Sum
Subjects Studied      | Rollup            | Relation: Sessions Today, Property: Subject, Calculate: Count unique values
XP Earned Today       | Rollup            | Relation: Sessions Today, Property: XP Earned, Calculate: Sum
```

---

## 📊 Database 6: Process Library

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Process Name          | Title             | Default
Process Type          | Select            | Options: Study Routine, Decision Tree, Workflow, Problem Solving, Review Process
Subject               | Relation          | Relation to: Subject Master, Limit 1
Questionnaire         | Text              | Default
AI Refinements        | Text              | Default
Flowchart             | Files & media     | Default
Mermaid Code          | Code              | Language: Mermaid
Created Date          | Created time      | Default
Last Used             | Date              | Date format: Month day, year
Times Used            | Number            | Number format: Number (Default: 0)
Effectiveness         | Select            | Options: ⭐⭐⭐⭐⭐, ⭐⭐⭐⭐, ⭐⭐⭐, ⭐⭐, ⭐
Tags                  | Multi-select      | Create as needed
Related Processes     | Relation          | Relation to: Process Library, No limit
Improvement Notes     | Text              | Default
```

---

## 📊 Database 7: Achievements

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Achievement Name      | Title             | Default
Achievement Type      | Select            | Options: Streak, Milestone, Challenge, Special, Hidden
Description           | Text              | Default
Unlock Criteria       | Text              | Default
Icon                  | Select            | Options: 🔥, ⭐, 🏆, 💎, 🎯, 🚀, 👑, 💪
XP Reward             | Number            | Number format: Number
Unlocked              | Checkbox          | Default
Unlock Date           | Date              | Date format: Month day, year
Rarity                | Select            | Options: Common, Uncommon, Rare, Epic, Legendary
Progress              | Number            | Number format: Percentage
```

---

## 📊 Database 8: Progress Snapshots

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Snapshot Title        | Formula           | formatDate(prop("Date"), "YYYY-MM-DD") + " " + prop("Period")
Date                  | Date              | Date format: Month day, year
Period                | Select            | Options: Daily, Weekly, Monthly
Subjects Data         | Text              | Default (JSON)
Total XP              | Number            | Number format: Number
Total Hours           | Number            | Number format: Number
Streaks Data          | Text              | Default (JSON)
Achievements Count    | Number            | Number format: Number
Goals Completed       | Number            | Number format: Number
Consistency Rate      | Number            | Number format: Percentage
AI Insights           | Text              | Default
```

---

## 📊 Database 9: Learning Investments

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Purchase Name         | Title             | Default
Subject               | Relation          | Relation to: Subject Master, Limit 1
Purchase Date         | Date              | Date format: Month day, year
Amount                | Number            | Number format: Dollar
Currency              | Select            | Options: USD, EUR, KRW, CNY
Category              | Select            | Options: Course, Book, App, Tutor, Exam Fee, Tool, Other
Recurring             | Checkbox          | Default
Billing Period        | Select            | Options: One-time, Monthly, Yearly
Value Rating          | Select            | Options: 💎 Excellent, 👍 Good, 🤷 Okay, 👎 Poor
Notes                 | Text              | Default
```

---

## 📊 Database 10: Notification Queue

```
Property Name          | Type              | Configuration
--------------------- | ----------------- | ------------------
Notification ID       | Title             | Default (auto-generate)
Type                  | Select            | Options: Reminder, Achievement, Summary, Alert, Motivation
Scheduled Time        | Date              | Include time: ON
Recipient             | Select            | Options: Telegram, Email, Notion, Multiple
Content               | Text              | Default
Urgency               | Select            | Options: 🚨 Urgent, ⚡ High, 🔄 Normal, 💤 Low
Sent                  | Checkbox          | Default
Sent Time             | Date              | Include time: ON
Related Subject       | Relation          | Relation to: Subject Master, Limit 1
Related Action        | Relation          | Relation to: Daily Actions, Limit 1
Emoji Style           | Checkbox          | Default: Checked
```

---

## 🎨 View Templates

### Today's Command Center
```
Database: Multiple (Sessions, Actions, Journal)
Filter: Date is Today
Group by: Subject
Sort: Priority descending, Time ascending
Properties shown: Title, Subject, Time, Status, XP
```

### Streak Dashboard
```
Database: Subject Master
Filter: Current Status is Active
Sort: Current Streak descending
Properties shown: Subject Name, Current Streak, Best Streak, Last Studied, Auto-Pause Warning
Layout: Gallery
```

### Weekly Review
```
Database: Journal Entries
Filter: Date is This week
Sort: Date descending
Properties shown: Entry Title, Total Time, Subjects Studied, XP Earned, Mood, Epiphany Section
```

---

## 🔧 Implementation Tips

1. **Create databases in order** to avoid relation errors
2. **Test formulas** with sample data before full implementation
3. **Set up templates** for recurring entries
4. **Create filtered views** before adding lots of data
5. **Use synced blocks** for shared configuration

---

**Last Updated**: 2025-07-04
**Status**: Ready for Implementation
**Phase 1 Complete**: ✅