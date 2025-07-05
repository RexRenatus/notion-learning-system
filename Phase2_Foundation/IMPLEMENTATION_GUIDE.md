# 📘 Phase 2 Implementation Guide - Foundation Setup

## Overview
This guide provides step-by-step instructions for implementing the core Notion databases. Follow each step exactly to ensure proper functionality.

---

## 🎯 Phase 2 Goals
- Create 5 core databases with exact schemas
- Set up all relations correctly
- Implement and test formulas
- Create initial test data
- Validate everything works

---

## 📚 Database 1: Subject Master

### Step-by-Step Creation

#### 1. Create the Database
1. In Notion, type `/database` and select "Database - Full page"
2. Name it exactly: **📚 Subject Master**
3. Delete the default properties except "Name"
4. Rename "Name" to **Subject Name**

#### 2. Add Properties (IN THIS EXACT ORDER)

**Property 1: Category**
- Click "+ Add a property"
- Name: `Category`
- Type: Select
- Add options (one by one):
  - Language
  - Finance
  - Philosophy
  - Programming
  - Art
  - Other

**Property 2: Current Status**
- Click "+ Add a property"
- Name: `Current Status`
- Type: Select
- Add options:
  - Active (set as default by clicking ...)
  - Paused
  - Completed
  - Planning

**Property 3: Priority Level**
- Name: `Priority Level`
- Type: Select
- Add options:
  - Primary Focus
  - Secondary
  - Maintenance
  - Future

**Property 4: Date Started**
- Name: `Date Started`
- Type: Date
- Date format: Click format → "Month day, year"

**Property 5: Target Completion**
- Name: `Target Completion`
- Type: Date
- Date format: "Month day, year"

**Property 6: Current Level**
- Name: `Current Level`
- Type: Number
- Number format: Number (not percent or dollar)

**Property 7: Total XP**
- Name: `Total XP`
- Type: Number
- Number format: Number

**Property 8: Current Streak**
- Name: `Current Streak`
- Type: Number
- Number format: Number

**Property 9: Best Streak**
- Name: `Best Streak`
- Type: Number
- Number format: Number

**Property 10: Last Studied**
- Name: `Last Studied`
- Type: Date
- Date format: Click format → "Relative" (shows "2 days ago" etc.)

**Property 11: Auto-Pause Warning**
- Name: `Auto-Pause Warning`
- Type: Formula
- Click "Edit formula" and paste:
```
if(
  dateBetween(now(), prop("Last Studied"), "days") > 5, 
  "⚠️ Auto-pause in " + format(7 - dateBetween(now(), prop("Last Studied"), "days")) + " days", 
  "✅"
)
```

**Property 12: Color Theme**
- Name: `Color Theme`
- Type: Select
- Add options (copy emojis exactly):
  - 🔴 Red
  - 🟠 Orange
  - 🟡 Yellow
  - 🟢 Green
  - 🔵 Blue
  - 🟣 Purple

**Property 13: Resources**
- Name: `Resources`
- Type: URL

**Property 14: Money Invested**
- Name: `Money Invested`
- Type: Number
- Number format: Dollar ($)

**Property 15: Goal Statement**
- Name: `Goal Statement`
- Type: Text

**Property 16: Daily Minimum**
- Name: `Daily Minimum`
- Type: Number
- Number format: Number
- Default value: 15

**Property 17: Flashcard Target**
- Name: `Flashcard Target`
- Type: Number
- Number format: Number
- Default value: 10

**Property 18: Last Increase**
- Name: `Last Increase`
- Type: Date
- Date format: "Month day, year"

**Property 19: Next Increase Date**
- Name: `Next Increase Date`
- Type: Formula
- Click "Edit formula" and paste:
```
if(
  empty(prop("Last Increase")),
  dateAdd(prop("Date Started"), 14, "days"),
  dateAdd(prop("Last Increase"), 14, "days")
)
```

**Property 20: Synergy Subjects**
- Name: `Synergy Subjects`
- Type: Relation
- Search and select: "Subject Master" (this same database)
- Allow multiple relations: Yes

#### 3. Create Database Template
1. Click "New" dropdown → "+ New template"
2. Name it: "📚 New Subject"
3. Set default values:
   - Current Status: Active
   - Current Level: 1
   - Total XP: 0
   - Current Streak: 0
   - Best Streak: 0
   - Daily Minimum: 15
   - Flashcard Target: 10
4. Save template

#### 4. Test the Database
1. Create a test entry using the template:
   - Subject Name: "Korean Language"
   - Category: Language
   - Current Status: Active
   - Priority Level: Primary Focus
   - Date Started: Today's date
   - Current Level: 1
   - Total XP: 0
   - Current Streak: 0
   - Best Streak: 0
   - Last Studied: Today
   - Daily Minimum: 15
   - Flashcard Target: 10

2. Verify:
   - Auto-Pause Warning shows "✅"
   - Next Increase Date shows 14 days from Date Started

---

## 🎯 Database 2: Goals Hierarchy

### Step-by-Step Creation

#### 1. Create the Database
1. Create new database: **🎯 Goals Hierarchy**

#### 2. Add Properties

**Property 1: Goal Title**
- Rename default "Name" to `Goal Title`

**Property 2: Goal Type**
- Type: Select
- Options:
  - Yearly
  - Quarterly
  - Monthly
  - Weekly
  - Daily

**Property 3: Parent Goal**
- Type: Relation
- Search: "Goals Hierarchy" (this same database)
- Allow multiple: Yes

**Property 4: Subject**
- Type: Relation
- Search: "Subject Master"
- Limit: 1 page

**Property 5: Target Date**
- Type: Date
- Format: "Month day, year"

**Property 6: Created Date**
- Type: Created time
- Format: "Month day, year"

**Property 7: Status**
- Type: Select
- Options:
  - Not Started (default)
  - In Progress
  - Completed
  - Paused
  - Cancelled

**Property 8: Priority**
- Type: Select
- Options:
  - 🔥 Critical
  - ⚡ High
  - 🔄 Normal
  - 💤 Low

**Property 9: Success Metrics**
- Type: Text

**Property 10: Decomposition Notes**
- Type: Text

**Property 11: Estimated Hours**
- Type: Number
- Format: Number

**Property 12: Subgoals**
- When you created "Parent Goal" relation, Notion auto-created this
- If not visible, check "Show all properties"

**Property 13: Total Subgoals**
- Type: Rollup
- Relation: Subgoals
- Property: Goal Title
- Calculate: Count

**Property 14: Completed Subgoals**
- Type: Rollup
- Relation: Subgoals
- Property: Status
- Calculate: Count
- Filter: Add filter → Status is Completed

**Property 15: Progress Percentage**
- Type: Formula
- Formula:
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

**Property 16: Actual Hours**
- Type: Rollup
- Relation: Sessions (will be created later)
- For now, skip this property

#### 3. Test the Database
1. Create a parent goal:
   - Goal Title: "Master Korean to B2 Level"
   - Goal Type: Yearly
   - Subject: Korean Language
   - Status: In Progress

2. Create a child goal:
   - Goal Title: "Complete Korean Level 1"
   - Goal Type: Quarterly
   - Parent Goal: "Master Korean to B2 Level"
   - Subject: Korean Language

3. Verify Progress Percentage updates when changing child status

---

## ✅ Database 3: Daily Actions

### Step-by-Step Creation

#### 1. Create the Database
1. Create new database: **✅ Daily Actions**

#### 2. Add Properties

**Property 1: Action Title**
- Rename default to `Action Title`

**Property 2: Parent Goal**
- Type: Relation
- Search: "Goals Hierarchy"
- Limit: 1 page

**Property 3: Subject**
- Type: Relation
- Search: "Subject Master"
- Limit: 1 page

**Property 4: Action Type**
- Type: Select
- Options:
  - Study
  - Practice
  - Review
  - Create
  - Test

**Property 5: Estimated Time**
- Type: Number
- Format: Number
- Description: "Minutes"

**Property 6: Scheduled Date**
- Type: Date
- Format: "Month day, year"

**Property 7: Completion Status**
- Type: Checkbox

**Property 8: Completed Date**
- Type: Date
- Format: "Month day, year"

**Property 9: Recurring**
- Type: Checkbox

**Property 10: Recurrence Pattern**
- Type: Select
- Options:
  - Daily
  - Weekdays
  - Weekly
  - Custom

**Property 11: Difficulty Points**
- Type: Number
- Format: Number
- Description: "1=Easy, 5=Very Hard"

**Property 12: Instructions**
- Type: Text
- Rename to: `Specific Instructions`

**Property 13: Success Criteria**
- Type: Text

**Property 14: Reminder Sent**
- Type: Checkbox

**Property 15: Reminder Time**
- Type: Select
- Options:
  - 09:30
  - 15:00
  - 19:00
  - Custom

**Property 16: Bumped Count**
- Type: Number
- Format: Number
- Default: 0

**Property 17: Sessions** (will auto-create later)
**Property 18: Actual Time** (will add later)

---

## 📝 Database 4: Daily Learning Sessions

### Step-by-Step Creation

#### 1. Create the Database
1. Create new database: **📝 Daily Learning Sessions**

#### 2. Add Properties

**Property 1: Session ID**
- Type: Formula
- Formula:
```
formatDate(prop("Session Date"), "YYYY-MM-DD") + "-" + 
slice(prop("Subject"), 0, 3) + "-" + 
format(toNumber(prop("Duration")))
```
- Note: Keep default Name property, hide it later

**Property 2: Session Date**
- Type: Date
- Format: "Month day, year"

**Property 3: Subject**
- Type: Relation
- Search: "Subject Master"
- Limit: 1 page

**Property 4: Session Type**
- Type: Multi-select
- Options:
  - Flashcards
  - Reading
  - Writing
  - Speaking
  - Listening
  - Practice Problems
  - Video
  - Other

**Property 5: Start Time**
- Type: Date
- Include time: Toggle ON
- Time format: 12 hour

**Property 6: End Time**
- Type: Date
- Include time: Toggle ON
- Time format: 12 hour

**Property 7: Duration**
- Type: Formula
- Formula:
```
if(
  and(not(empty(prop("Start Time"))), not(empty(prop("End Time")))),
  dateBetween(prop("End Time"), prop("Start Time"), "minutes"),
  0
)
```

**Property 8: Focus Quality**
- Type: Select
- Options:
  - 🎯 Deep Focus
  - 👍 Normal
  - 😕 Distracted
- Default: 👍 Normal

**Property 9: Energy Level**
- Type: Select
- Options:
  - ⚡ High
  - 🔄 Medium
  - 😴 Low

**Property 10: Session Notes**
- Type: Text

**Property 11: Tasks Completed**
- Type: Relation
- Search: "Daily Actions"
- Allow multiple

**Property 12: Breakthroughs**
- Type: Text

**Property 13: Struggles**
- Type: Text

**Property 14: XP Earned**
- Type: Formula
- Formula (simplified for now):
```
round(
  prop("Duration") * 
  if(prop("Focus Quality") == "🎯 Deep Focus", 1.5, 1)
)
```
- Note: Full formula needs streak data

**Property 15: Streak Maintained**
- Type: Checkbox

**Property 16: Materials Used**
- Type: Multi-select
- Options:
  - Textbook
  - App
  - Video
  - Flashcards
  - Notebook
  - AI Tool
  - Other

**Property 17: Location**
- Type: Select
- Options:
  - Home
  - Library
  - Cafe
  - Office
  - Transit
  - Other

---

## 📔 Database 5: Journal Entries

### Step-by-Step Creation

#### 1. Create the Database
1. Create new database: **📔 Journal Entries**

#### 2. Add Properties

**Property 1: Entry Title**
- Type: Formula
- Formula:
```
formatDate(prop("Date"), "YYYY-MM-DD") + " Journal"
```

**Property 2: Date**
- Type: Date
- Format: "Month day, year"
- **IMPORTANT**: Make this property unique (prevents duplicate dates)

**Property 3: Tasks Completed**
- Type: Text

**Property 4: Random Thoughts**
- Type: Text

**Property 5: Todo Tomorrow**
- Type: Text

**Property 6: Reflections**
- Type: Text

**Property 7: Mood**
- Type: Select
- Options:
  - 😊 Energized
  - 👍 Focused
  - 😐 Neutral
  - 😔 Struggled
  - 🔥 Breakthrough

**Property 8: Key Insights**
- Type: Text

**Property 9: Hidden TODOs**
- Type: Text

**Property 10: Epiphany Section**
- Type: Text
- Description: "AI-generated patterns and actionable todos"

**Property 11: AI Analysis Complete**
- Type: Checkbox

**Property 12: Summary Sent**
- Type: Checkbox

**Property 13: Calendar Events**
- Type: Text

**Property 14: Energy Pattern**
- Type: Text

**Property 15: Sessions Today**
- Type: Relation
- Search: "Daily Learning Sessions"
- Allow multiple

**Property 16: Total Time Today**
- Type: Rollup
- Relation: Sessions Today
- Property: Duration
- Calculate: Sum

**Property 17: Subjects Studied**
- Type: Rollup
- Relation: Sessions Today
- Property: Subject
- Calculate: Count unique values

**Property 18: XP Earned Today**
- Type: Rollup
- Relation: Sessions Today
- Property: XP Earned
- Calculate: Sum

---

## ✅ Validation Checklist

After creating all 5 databases, verify:

### 1. Subject Master
- [ ] Formula for Auto-Pause Warning works
- [ ] Formula for Next Increase Date calculates correctly
- [ ] Can create self-relations (Synergy Subjects)

### 2. Goals Hierarchy
- [ ] Can create parent-child relationships
- [ ] Progress Percentage updates correctly
- [ ] Relations to Subject Master work

### 3. Daily Actions
- [ ] Relations to Goals and Subjects work
- [ ] All select options are correct
- [ ] Default values are set

### 4. Daily Learning Sessions
- [ ] Duration calculates when times entered
- [ ] Session ID generates correctly
- [ ] Relations to Subject Master and Daily Actions work

### 5. Journal Entries
- [ ] Entry Title auto-generates
- [ ] Date field prevents duplicates
- [ ] All rollups calculate correctly
- [ ] Relations to Sessions work

---

## 🧪 Test Data Creation

Create this test data to verify everything works:

1. **Subject**: "Korean Language" (Active, Primary Focus)
2. **Goal**: "Master Korean B2" (Yearly, In Progress)
3. **Sub-goal**: "Complete Level 1" (Quarterly, In Progress)
4. **Action**: "Study 20 Anki cards" (Daily, Recurring)
5. **Session**: Today, 30 minutes, Deep Focus
6. **Journal**: Today's entry with the session linked

---

## 🚨 Common Issues & Solutions

### Issue: Relation not showing up
**Solution**: Make sure both databases are saved. Refresh the page.

### Issue: Formula shows error
**Solution**: Check property names match exactly (case-sensitive)

### Issue: Rollup not calculating
**Solution**: Ensure the relation has at least one linked item

### Issue: Can't make date unique
**Solution**: In database settings → Properties → Date → Edit → Toggle "No duplicates"

---

## 📝 Next Steps

Once all 5 databases are created and tested:
1. Update PROJECT_JOURNAL.md with completion status
2. Move to creating views and dashboards
3. Begin Phase 3: Automation Layer

---

---

## ⚠️ IMPORTANT UPDATE: Missing Relations for Phase 3

After Phase 2 implementation, add these critical relations BEFORE starting Phase 3:

### 1. Goals Hierarchy → Daily Actions
In **Goals Hierarchy** database:
- Add property "Actions" 
- Type: Relation to Daily Actions
- Toggle ON "Show on Daily Actions"
- This enables progress tracking formulas

### 2. Subject Master → Daily Learning Sessions  
In **Subject Master** database:
- Add property "Learning Sessions"
- Type: Relation to Daily Learning Sessions  
- Toggle ON "Show on Daily Learning Sessions"
- This enables weekly analytics formulas

See `MISSING_RELATIONS_FIX.md` for detailed instructions.

---

**Last Updated**: 2025-07-05
**Guide Version**: 1.1 (Updated with missing relations)