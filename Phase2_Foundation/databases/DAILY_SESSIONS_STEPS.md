# 📚 Daily Learning Sessions Database - Exact Implementation Steps

## Quick Reference Card

Step-by-step checklist for creating the Daily Learning Sessions database with formulas.

---

## 📋 Step-by-Step Implementation

### Step 1: Create Database
```
Action: Type /database → Select "Database - Full page"
Name: 📚 Daily Learning Sessions
```

### Step 2: Configure Title Property
```
Action: Click on "Name" property → Delete it
We'll use Session ID formula as the title instead
```

### Step 3: Add Each Property (IN ORDER)

#### ✅ Property 1: Session Date
```
Name: Session Date
Type: Date
Format: Month day, year
```

#### ✅ Property 2: Subject
```
Name: Subject
Type: Relation
Search for: Subject Master
Limit to: 1 page
```

#### ✅ Property 3: Session Type
```
Name: Session Type
Type: Multi-select
Options:
  - Flashcards
  - Reading
  - Writing
  - Speaking
  - Listening
  - Practice Problems
  - Video
  - Other
```

#### ✅ Property 4: Start Time
```
Name: Start Time
Type: Date
Include time: Toggle ON ⚠️ IMPORTANT
Format: Month day, year
```

#### ✅ Property 5: End Time
```
Name: End Time
Type: Date
Include time: Toggle ON ⚠️ IMPORTANT
Format: Month day, year
```

#### ✅ Property 6: Duration (Formula)
```
Name: Duration
Type: Formula
Formula: Copy exactly:

if(
  and(not(empty(prop("Start Time"))), not(empty(prop("End Time")))),
  dateBetween(prop("End Time"), prop("Start Time"), "minutes"),
  0
)
```

#### ✅ Property 7: Session ID (Formula)
```
Name: Session ID
Type: Formula
Formula: Copy exactly:

formatDate(prop("Session Date"), "YYYY-MM-DD") + "-" + 
slice(prop("Subject"), 0, 3) + "-" + 
format(toNumber(prop("Duration")))
```

**AFTER CREATING**: Click "..." on Session ID → Set as title

#### ✅ Property 8: Focus Quality
```
Name: Focus Quality
Type: Select
Options:
  - 🎯 Deep Focus
  - 👍 Normal
  - 😕 Distracted
```

#### ✅ Property 9: Energy Level
```
Name: Energy Level
Type: Select
Options:
  - ⚡ High
  - 🔄 Medium
  - 😴 Low
```

#### ✅ Property 10: Session Notes
```
Name: Session Notes
Type: Text
```

#### ✅ Property 11: Tasks Completed
```
Name: Tasks Completed
Type: Relation
Search for: Daily Actions
Limit: No limit
```

#### ✅ Property 12: Breakthroughs
```
Name: Breakthroughs
Type: Text
```

#### ✅ Property 13: Struggles
```
Name: Struggles
Type: Text
```

#### ✅ Property 14: Streak Maintained
```
Name: Streak Maintained
Type: Checkbox
```

#### ✅ Property 15: Materials Used
```
Name: Materials Used
Type: Multi-select
Options:
  - Textbook
  - App
  - Video
  - Flashcards
  - Notebook
  - AI Tool
  - Other
```

#### ✅ Property 16: Location
```
Name: Location
Type: Select
Options:
  - Home
  - Library
  - Cafe
  - Office
  - Transit
  - Other
```

#### ✅ Property 17: XP Earned (Formula) - TEMPORARY VERSION
```
Name: XP Earned
Type: Formula
Formula: Copy exactly (simplified for now):

round(
  prop("Duration") * 
  if(prop("Focus Quality") == "🎯 Deep Focus", 1.5, 1)
)
```

**Note**: We'll update this formula later when Subject has Current Streak property

#### ✅ Note: Skip These for Now
```
- Journal Entry (will auto-create when we link from Journal database)
```

---

## 📝 Create Database Templates

### Template 1: Quick Study Session
1. Click "New" dropdown → "+ New template"
2. Name: "⚡ Quick Study"
3. Set these values:
   ```
   Session Date: Today
   Session Type: Flashcards
   Focus Quality: 👍 Normal
   Energy Level: 🔄 Medium
   Location: Home
   ```
4. Save template

### Template 2: Deep Learning Session
1. Click "New" dropdown → "+ New template"
2. Name: "🎯 Deep Study"
3. Set these values:
   ```
   Session Date: Today
   Session Type: Reading
   Focus Quality: 🎯 Deep Focus
   Energy Level: ⚡ High
   Location: Library
   ```
4. Save template

### Template 3: Practice Session
1. Click "New" dropdown → "+ New template"
2. Name: "💪 Practice"
3. Set these values:
   ```
   Session Date: Today
   Session Type: Practice Problems
   Focus Quality: 👍 Normal
   Location: Home
   ```
4. Save template

---

## 🧪 Test Your Database

### Create Test Session
1. Use "⚡ Quick Study" template
2. Fill in:
   - **Session Date**: Today
   - **Subject**: Korean Language (link it)
   - **Start Time**: Click date, toggle time, set to 10:00 AM
   - **End Time**: Click date, toggle time, set to 10:30 AM
   - **Tasks Completed**: Link to any tasks from Daily Actions
   - **Session Notes**: "Reviewed basic greetings"
   - **Materials Used**: App, Flashcards

### Verify These Work:
- [ ] Duration shows "30" (minutes)
- [ ] Session ID shows format like "2025-01-05-Kor-30"
- [ ] Relations to Subject and Tasks work
- [ ] XP Earned calculates (should be 30 for normal focus)

---

## 🚨 Critical Setup Steps

### Make Session ID the Title
1. Find Session ID property
2. Click "..." menu → "Set as title"
3. This makes Session ID show as the main title

### Enable Time for Date Properties
1. **Start Time**: Click property → Edit property → Toggle "Include time" ON
2. **End Time**: Click property → Edit property → Toggle "Include time" ON
3. Without this, Duration won't calculate!

---

## 🎯 Testing Scenarios

### Scenario 1: Duration Calculation
1. Set Start Time: 2:00 PM
2. Set End Time: 3:30 PM
3. Duration should show: 90

### Scenario 2: XP Calculation
- 30-minute session + Normal focus = 30 XP
- 30-minute session + Deep Focus = 45 XP
- 60-minute session + Deep Focus = 90 XP

### Scenario 3: Session ID Format
- Date: 2025-01-05, Subject: Korean, Duration: 45
- Session ID: "2025-01-05-Kor-45"

---

## ✅ Final Checklist

Before moving to next database:
- [ ] All 17 properties created
- [ ] Session ID set as title
- [ ] Time enabled for Start/End Time
- [ ] Duration formula working
- [ ] XP formula calculating
- [ ] 3 templates created
- [ ] Test session shows correct calculations

---

## 🚨 Common Issues

### Duration shows 0
- Check Start Time and End Time have time enabled
- Make sure End Time is after Start Time
- Both times must be filled for calculation

### Session ID not showing as title
- Click "..." on Session ID property
- Select "Set as title"
- Refresh page if needed

### XP not calculating
- Check Focus Quality is set
- Make sure Duration is calculating first
- Formula syntax must be exact

---

## 💡 Usage Tips

1. **Always set times** for accurate duration
2. **Link tasks** to track what you accomplished
3. **Note breakthroughs** for AI analysis later
4. **Be honest** about focus quality
5. **Use templates** for consistency

---

## ⏭️ Next Step
Once verified, proceed to create **Journal Entries** database!

---

**Note**: The real magic happens when Journal Entries aggregate your daily sessions!