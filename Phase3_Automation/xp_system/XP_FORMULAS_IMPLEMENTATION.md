# 🎮 XP Formulas - Step-by-Step Implementation

## Overview
This guide provides exact formulas to add to your Notion databases for the XP system.

---

## 📝 Daily Actions - XP Formula

### Add New Property: Action XP
**Type**: Formula  
**Purpose**: Calculate XP earned when completing actions

```
if(
  prop("Completion Status"),
  if(prop("Action Type") == "Study", 25,
  if(prop("Action Type") == "Practice", 30,
  if(prop("Action Type") == "Review", 20,
  if(prop("Action Type") == "Create", 40,
  if(prop("Action Type") == "Test", 50, 25))))) * 
  if(
    prop("Days Overdue") > 0, 0.8,
    if(
      dateBetween(prop("Scheduled Date"), prop("Completed Date"), "days") > 0, 1.5,
      1.2
    )
  ),
  0
)
```

**How it works**:
- Base XP by type: Study (25), Practice (30), Review (20), Create (40), Test (50)
- Multipliers: Early (1.5x), On-time (1.2x), Overdue (0.8x)
- Only awards XP when completed

---

## 📚 Subject Master - Level System

### 1. Change Current Level from Number to Formula
**Property Name**: Current Level  
**Type**: Formula (change from Number)  
```
floor(sqrt(prop("Total XP") / 100))
```

### 2. Add XP to Next Level
**Property Name**: XP to Next Level  
**Type**: Formula  
```
pow(prop("Current Level") + 1, 2) * 100 - prop("Total XP")
```

### 3. Add Level Progress
**Property Name**: Level Progress %  
**Type**: Formula  
```
round(
  (prop("Total XP") - pow(prop("Current Level"), 2) * 100) / 
  (pow(prop("Current Level") + 1, 2) * 100 - pow(prop("Current Level"), 2) * 100) * 100
)
```

### 4. Add Level Title
**Property Name**: Level Title  
**Type**: Formula  
```
if(prop("Current Level") <= 5, "🌱 Novice Learner",
if(prop("Current Level") <= 10, "📚 Dedicated Student",
if(prop("Current Level") <= 20, "🔍 Knowledge Seeker",
if(prop("Current Level") <= 35, "🎓 Subject Expert",
if(prop("Current Level") <= 50, "🏆 Master Scholar",
if(prop("Current Level") <= 75, "🧙 Sage",
if(prop("Current Level") <= 99, "👑 Grandmaster",
"⚡ Legendary")))))))
```

### 5. Add Session XP Rollup
**Property Name**: Session XP Total  
**Type**: Rollup  
```
Relation: Learning Sessions
Property: XP Earned
Calculate: Sum
```

---

## 📓 Journal Entries - Daily XP

### Add Daily XP Total
**Property Name**: Daily XP Total  
**Type**: Formula  
```
prop("XP Earned Today") + 
if(prop("AI Analysis Complete"), 50, 0) +
if(prop("Subjects Studied") >= 3, 100, 0) +
if(prop("Total Time Today") >= 120, 200, 0)
```

**Bonuses**:
- AI Analysis: +50 XP
- Study 3+ subjects: +100 XP
- 2+ hour study day: +200 XP

---

## 🏆 Quick Achievement Checks

### In Subject Master, add Streak Achievement Check
**Property Name**: Streak Achievement  
**Type**: Formula  
```
if(prop("Current Streak") >= 365, "🏆 Year of Learning",
if(prop("Current Streak") >= 100, "💯 Century Club",
if(prop("Current Streak") >= 30, "📅 Monthly Master",
if(prop("Current Streak") >= 7, "🗓️ Week Warrior", ""))))
```

### In Daily Learning Sessions, add Session Achievement
**Property Name**: Session Achievement  
**Type**: Formula  
```
if(prop("Duration") >= 120, "🏃 Marathon Session",
if(hour(prop("Start Time")) < 7, "🌅 Early Bird",
if(hour(prop("Start Time")) >= 22, "🦉 Night Owl", "")))
```

---

## 🎯 Testing Your XP System

### Create Test Data:
1. **Daily Action Test**:
   - Create action with type "Test"
   - Mark as completed
   - Should show 50 XP (or 60 if on-time)

2. **Session XP Test**:
   - Create 60-minute session
   - Deep Focus quality
   - Should show 90 XP (60 × 1.5)

3. **Level Calculation Test**:
   - Set Total XP to 400
   - Current Level should show: 2
   - XP to Next Level: 500
   - Level Progress %: 44%

---

## 📊 XP Dashboard Views

### 1. XP Leaderboard (Subject Master)
**View Type**: Gallery  
**Sort**: Total XP (Descending)  
**Card Preview**: 
- Subject Name (large)
- Level Title
- Progress bar visual
- Total XP

### 2. Daily XP Tracker (Journal Entries)
**View Type**: Calendar  
**Properties**: Daily XP Total  
**Color**: By XP ranges (0-99, 100-199, 200+)

### 3. Achievement Gallery (Subject Master)
**View Type**: Gallery  
**Filter**: Streak Achievement is not empty  
**Show**: Subject, Streak, Achievement badge

---

## ⚠️ Important Notes

1. **Total XP Calculation**: Currently, Total XP needs manual updating. In future phases, automation can sum all XP sources.

2. **Missing Relations**: You may need to create an "Actions" relation in Subject Master to track action XP.

3. **Performance**: Complex formulas may slow large databases. Consider simplifying if needed.

---

**Next Step**: Create Dashboard Views to visualize your XP progress!