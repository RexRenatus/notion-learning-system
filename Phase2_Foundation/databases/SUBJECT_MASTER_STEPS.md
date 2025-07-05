# 📚 Subject Master Database - Exact Implementation Steps

## Quick Reference Card

This is your step-by-step checklist for creating the Subject Master database in Notion.

---

## 🚀 Pre-Setup
1. Open Notion
2. Create or navigate to your Learning System workspace
3. Create a new page for databases (optional but recommended)

---

## 📋 Step-by-Step Implementation

### Step 1: Create Database
```
Action: Type /database → Select "Database - Full page"
Name: 📚 Subject Master
```

### Step 2: Configure Title Property
```
Action: Click on "Name" property → Rename to "Subject Name"
Type: Title (default)
```

### Step 3: Add Each Property

#### ✅ Property: Category
```
Click: + Add a property
Name: Category
Type: Select
Options: 
  - Language
  - Finance
  - Philosophy
  - Programming
  - Art
  - Other
```

#### ✅ Property: Current Status
```
Name: Current Status
Type: Select
Options:
  - Active ← Set as default
  - Paused
  - Completed
  - Planning
```

#### ✅ Property: Priority Level
```
Name: Priority Level
Type: Select
Options:
  - Primary Focus
  - Secondary
  - Maintenance
  - Future
```

#### ✅ Property: Date Started
```
Name: Date Started
Type: Date
Format: Month day, year
```

#### ✅ Property: Target Completion
```
Name: Target Completion
Type: Date
Format: Month day, year
```

#### ✅ Property: Current Level
```
Name: Current Level
Type: Number
Format: Number
```

#### ✅ Property: Total XP
```
Name: Total XP
Type: Number
Format: Number
```

#### ✅ Property: Current Streak
```
Name: Current Streak
Type: Number
Format: Number
```

#### ✅ Property: Best Streak
```
Name: Best Streak
Type: Number
Format: Number
```

#### ✅ Property: Last Studied
```
Name: Last Studied
Type: Date
Format: Relative ← Important!
```

#### ✅ Property: Weekly Time Goal (IMPORTANT - Needed for Phase 3)
```
Name: Weekly Time Goal
Type: Number
Format: Number
Description: Target minutes per week
Default: 300 (5 hours)
```

#### ✅ Property: Learning Sessions (IMPORTANT - Needed for Phase 3)
```
Name: Learning Sessions
Type: Relation
Search for: Daily Learning Sessions
No limit on pages
Toggle ON: Show on Daily Learning Sessions
```
**Note**: This creates bidirectional relation for session tracking

#### ✅ Property: Auto-Pause Warning (FORMULA)
```
Name: Auto-Pause Warning
Type: Formula
```
**Copy this formula exactly:**
```
if(
  dateBetween(now(), prop("Last Studied"), "days") > 5, 
  "⚠️ Auto-pause in " + format(7 - dateBetween(now(), prop("Last Studied"), "days")) + " days", 
  "✅"
)
```

#### ✅ Property: Color Theme
```
Name: Color Theme
Type: Select
Options: (copy emojis)
  - 🔴 Red
  - 🟠 Orange
  - 🟡 Yellow
  - 🟢 Green
  - 🔵 Blue
  - 🟣 Purple
```

#### ✅ Property: Resources
```
Name: Resources
Type: URL
```

#### ✅ Property: Money Invested
```
Name: Money Invested
Type: Number
Format: Dollar
```

#### ✅ Property: Goal Statement
```
Name: Goal Statement
Type: Text
```

#### ✅ Property: Daily Minimum
```
Name: Daily Minimum
Type: Number
Format: Number
Default: 15 ← Set in property settings
```

#### ✅ Property: Flashcard Target
```
Name: Flashcard Target
Type: Number
Format: Number
Default: 10 ← Set in property settings
```

#### ✅ Property: Last Increase
```
Name: Last Increase
Type: Date
Format: Month day, year
```

#### ✅ Property: Next Increase Date (FORMULA)
```
Name: Next Increase Date
Type: Formula
```
**Copy this formula exactly:**
```
if(
  empty(prop("Last Increase")),
  dateAdd(prop("Date Started"), 14, "days"),
  dateAdd(prop("Last Increase"), 14, "days")
)
```

#### ✅ Property: Synergy Subjects (RELATION)
```
Name: Synergy Subjects
Type: Relation
Search for: Subject Master ← This same database!
Allow linking to multiple pages: Yes
```

---

## 🧪 Test Your Database

### Create Test Entry #1
1. Click "New" to create an entry
2. Fill in:
   - Subject Name: **Korean Language**
   - Category: **Language**
   - Current Status: **Active**
   - Priority Level: **Primary Focus**
   - Date Started: **Today's date**
   - Current Level: **1**
   - Total XP: **0**
   - Current Streak: **0**
   - Best Streak: **0**
   - Last Studied: **Today**
   - Color Theme: **🔵 Blue**
   - Daily Minimum: **15** (should auto-fill)
   - Flashcard Target: **10** (should auto-fill)

### Verify These Work:
- [ ] Auto-Pause Warning shows: **✅**
- [ ] Next Increase Date shows: **14 days from today**

### Create Test Entry #2
1. Create another entry:
   - Subject Name: **CFA Level 1**
   - Category: **Finance**
   - Current Status: **Planning**
   - Priority Level: **Secondary**

### Test Synergy Relation
1. In Korean Language entry
2. Click Synergy Subjects
3. Link to "CFA Level 1"
4. Verify bidirectional link appears

---

## ✅ Final Checklist

Before moving to next database:
- [ ] All 20 properties created
- [ ] Both formulas work without errors
- [ ] Test data validates correctly
- [ ] Synergy relation links both ways
- [ ] Default values (15, 10) appear for new entries

---

## 🚨 Troubleshooting

### "Formula invalid" error
- Check property names are EXACT (case matters!)
- "Last Studied" not "last studied"
- No extra spaces in property names

### Relation not finding database
- Save the database first
- Refresh the page
- Try typing "Subject Master" slowly

### Date showing wrong format
- Click date property → Edit property → Date format
- Select correct format from dropdown

---

## 📸 Success Indicators

Your database should:
1. Have exactly 20 properties
2. Show ✅ for subjects studied today
3. Calculate next increase dates automatically
4. Allow subjects to link to each other

---

## ⏭️ Next Step
Once verified, proceed to create **Goals Hierarchy** database!

---

**Quick Tip**: Keep this guide open in a separate tab while building!