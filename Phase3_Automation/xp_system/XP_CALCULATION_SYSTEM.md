# 🎮 XP Calculation System

## Overview
The XP (Experience Points) system gamifies your learning journey by rewarding consistent study habits, quality sessions, and goal completion.

---

## 📊 XP Sources & Calculations

### 1. Daily Learning Sessions
**Base XP = Duration in minutes**

**Multipliers**:
- Focus Quality:
  - 🎯 Deep Focus: 1.5x
  - 👍 Normal: 1.0x
  - 😕 Distracted: 0.8x
- Streak Bonus: 1 + (Current Streak × 0.1), max 2.0x
- Difficulty Bonus: +10 XP per difficulty point from completed tasks

**Formula** (Already in Daily Learning Sessions):
```
round(
  prop("Duration") * 
  if(prop("Focus Quality") == "🎯 Deep Focus", 1.5, 
    if(prop("Focus Quality") == "👍 Normal", 1.0, 0.8)) *
  min(1 + (toNumber(prop("Subject.Current Streak")) * 0.1), 2) +
  sum(prop("Tasks Completed.Difficulty Points")) * 10
)
```

### 2. Daily Actions Completion
**XP Awards**:
- Study Action: 25 XP
- Practice Action: 30 XP
- Review Action: 20 XP
- Create Action: 40 XP
- Test Action: 50 XP

**Bonus Multipliers**:
- On-time completion: 1.2x
- Early completion: 1.5x
- Overdue: 0.8x

### 3. Goal Achievements
**XP by Goal Type**:
- Daily Goal: 50 XP
- Weekly Goal: 200 XP
- Monthly Goal: 500 XP
- Quarterly Goal: 1000 XP
- Yearly Goal: 5000 XP

**Bonus**: +10% for early completion

### 4. Streak Milestones
- 7-day streak: 100 XP
- 30-day streak: 500 XP
- 100-day streak: 2000 XP
- 365-day streak: 10000 XP

### 5. Special Achievements
- First Session: 50 XP
- Perfect Week (7/7 days): 300 XP
- Marathon Session (120+ min): 200 XP
- Early Bird (before 7 AM): 50 XP
- Night Owl (after 10 PM): 50 XP

---

## 🎯 Level System

### Level Calculation
```
Level = floor(sqrt(Total XP / 100))
```

### Level Thresholds
- Level 1: 0 XP
- Level 2: 100 XP
- Level 3: 400 XP
- Level 4: 900 XP
- Level 5: 1,600 XP
- Level 10: 10,000 XP
- Level 20: 40,000 XP
- Level 50: 250,000 XP
- Level 100: 1,000,000 XP

### Level Titles
- 1-5: Novice Learner
- 6-10: Dedicated Student
- 11-20: Knowledge Seeker
- 21-35: Subject Expert
- 36-50: Master Scholar
- 51-75: Sage
- 76-99: Grandmaster
- 100+: Legendary

---

## 📐 Implementation in Notion

### 1. Add XP Properties to Daily Actions

**Property Name**: Action XP  
**Type**: Formula  
```
if(
  prop("Completion Status"),
  switch(
    prop("Action Type"),
    "Study", 25,
    "Practice", 30,
    "Review", 20,
    "Create", 40,
    "Test", 50,
    25
  ) * 
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

### 2. Add Level Calculation to Subject Master

**Property Name**: Current Level  
**Type**: Formula  
```
floor(sqrt(prop("Total XP") / 100))
```

**Property Name**: XP to Next Level  
**Type**: Formula  
```
pow(prop("Current Level") + 1, 2) * 100 - prop("Total XP")
```

**Property Name**: Level Progress %  
**Type**: Formula  
```
round(
  (prop("Total XP") - pow(prop("Current Level"), 2) * 100) / 
  (pow(prop("Current Level") + 1, 2) * 100 - pow(prop("Current Level"), 2) * 100) * 100
)
```

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

### 3. Add XP Rollup to Subject Master

**Property Name**: Session XP Total  
**Type**: Rollup  
```
Relation: Learning Sessions
Property: XP Earned
Calculate: Sum
```

**Property Name**: Action XP Total  
**Type**: Rollup  
```
Relation: Actions (need to create this relation)
Property: Action XP
Calculate: Sum
```

**Note**: Total XP would need to combine multiple sources. In practice, you might track this manually or use automation.

### 4. Create XP Leaderboard View

**Database**: Subject Master  
**View Type**: Gallery  
**Sort**: Total XP (Descending)  
**Properties Shown**:
- Subject Name
- Level Title
- Current Level
- Total XP
- XP to Next Level
- Level Progress %

**Card Preview**: Show Level Title and progress bar visual

---

## 🏆 Achievement Tracking

### Create Achievement Tracker Database

**Properties**:
- Achievement Name (Title)
- XP Reward (Number)
- Date Earned (Date)
- Subject (Relation to Subject Master)
- Type (Select: Streak, Milestone, Special, Goal)
- Description (Text)

### Common Achievements to Track

1. **Streak Achievements**
   - "Week Warrior" - 7-day streak
   - "Monthly Master" - 30-day streak
   - "Century Club" - 100-day streak
   - "Year of Learning" - 365-day streak

2. **Study Achievements**
   - "Early Bird" - 10 sessions before 7 AM
   - "Night Owl" - 10 sessions after 10 PM
   - "Marathon Runner" - 5 sessions over 120 minutes
   - "Consistency King" - 30 days without missing

3. **Progress Achievements**
   - "Level 10" - Reach level 10 in any subject
   - "Polymath" - Level 5+ in 3 subjects
   - "Specialist" - Level 20 in one subject
   - "XP Millionaire" - 1,000,000 total XP

---

## 📊 XP Analytics Dashboard

### Daily XP Summary
**In Journal Entries, add**:

**Property Name**: Daily XP Total  
**Type**: Formula  
```
prop("XP Earned Today") + 
if(prop("AI Analysis Complete"), 50, 0) +
if(prop("Subjects Studied") >= 3, 100, 0)
```

### Weekly XP Tracking
Create filtered view of Journal Entries:
- Filter: This Week
- Show: Daily XP Total
- Calculate weekly average and total

### Subject XP Comparison
Gallery view of Subject Master:
- Show XP progress bars
- Color code by level
- Display recent XP gains

---

## 🎮 Gamification Tips

1. **Set XP Goals**: Weekly/Monthly XP targets
2. **Create Challenges**: "Earn 1000 XP this week"
3. **Reward Milestones**: Treat yourself at level ups
4. **Track Efficiency**: XP per hour metrics
5. **Compete**: Share progress with study partners

---

## 🔧 Advanced Features (Future)

1. **XP Decay**: Lose XP for extended inactivity
2. **Bonus Events**: Double XP weekends
3. **Subject Mastery**: Prestige system after Level 100
4. **XP Store**: Spend XP on rewards/features
5. **Team XP**: Collaborative learning bonuses

---

**Next Steps**: After implementing XP system, create Dashboard Views for visualization!