# 🧪 Foundation Testing Guide - Phase 2

## Overview
Complete testing checklist to verify all 5 databases work correctly with relations, formulas, and templates.

---

## 📊 Testing Data Set

### Test Subjects (Create 3)
```
1. Korean Language
   - Ultimate Goal: "Achieve Conversational Fluency"
   - Status: Active
   - Priority: High
   - Category: Languages
   - Resources: "Talk to Me in Korean, HelloTalk app"
   - Weekly Time Goal: 300

2. Python Programming
   - Ultimate Goal: "Build Full-Stack Web Applications"
   - Status: Active
   - Priority: Medium
   - Category: Technical Skills
   - Resources: "Python Crash Course, Real Python"
   - Weekly Time Goal: 420

3. Financial Analysis
   - Ultimate Goal: "Pass CFA Level 1"
   - Status: Planning
   - Priority: Low
   - Category: Professional
   - Resources: "CFA Institute materials"
   - Weekly Time Goal: 600
```

### Test Goal Hierarchy (Korean Language)
```
Yearly Goal:
- Title: "Achieve Korean Conversational Fluency - 2025"
- Subject: Korean Language
- Target Date: Dec 31, 2025
- Goal Type: Yearly
- Status: In Progress

  └── Quarterly Goal:
      - Title: "Complete Korean Level 1 - Q1 2025"
      - Parent Goal: [Link to Yearly]
      - Target Date: Mar 31, 2025
      - Goal Type: Quarterly
      
      └── Monthly Goal:
          - Title: "Master Basic Korean Grammar - Jan 2025"
          - Parent Goal: [Link to Quarterly]
          - Target Date: Jan 31, 2025
          - Goal Type: Monthly
          
          └── Weekly Goal:
              - Title: "Complete Chapter 5 - Week 1"
              - Parent Goal: [Link to Monthly]
              - Target Date: Jan 11, 2025
              - Goal Type: Weekly
              
              └── Daily Goal:
                  - Title: "Study Korean 30 minutes"
                  - Parent Goal: [Link to Weekly]
                  - Target Date: Today
                  - Goal Type: Daily
```

### Test Daily Actions (Create 5)
```
1. Daily Study (Recurring):
   - Title: "Review 20 Korean Flashcards"
   - Parent Goal: "Study Korean 30 minutes"
   - Subject: Korean Language
   - Action Type: Study
   - Estimated Time: 15
   - Scheduled Date: Today
   - Recurring: ✓
   - Recurrence Pattern: Daily
   - Difficulty Points: 2

2. Practice Task:
   - Title: "Korean Speaking Practice - Introductions"
   - Parent Goal: "Master Basic Korean Grammar - Jan 2025"
   - Subject: Korean Language
   - Action Type: Practice
   - Estimated Time: 30
   - Scheduled Date: Today
   - Difficulty Points: 3

3. Python Coding:
   - Title: "Complete Python Function Exercises"
   - Subject: Python Programming
   - Action Type: Practice
   - Estimated Time: 45
   - Scheduled Date: Today
   - Difficulty Points: 4

4. Review Task:
   - Title: "Review Week's Korean Vocabulary"
   - Parent Goal: "Complete Chapter 5 - Week 1"
   - Subject: Korean Language
   - Action Type: Review
   - Estimated Time: 20
   - Scheduled Date: Sunday
   - Recurring: ✓
   - Recurrence Pattern: Weekly

5. Test Task:
   - Title: "Korean Chapter 5 Quiz"
   - Parent Goal: "Complete Chapter 5 - Week 1"
   - Subject: Korean Language
   - Action Type: Test
   - Estimated Time: 30
   - Scheduled Date: Friday
   - Difficulty Points: 5
```

### Test Learning Sessions (Create 3)
```
Session 1 - Morning Korean:
- Name: "Morning Korean Study"
- Session Date: Today
- Subject: Korean Language
- Session Type: Flashcards, Reading
- Start Time: Today 9:00 AM
- End Time: Today 9:45 AM
- Focus Quality: 🎯 Deep Focus
- Energy Level: ⚡ High
- Tasks Completed: Link "Review 20 Korean Flashcards"
- Materials Used: App, Flashcards
- Location: Home
- Session Notes: "Struggled with food vocabulary"
- Breakthroughs: "Finally understood particle usage"

Session 2 - Afternoon Python:
- Name: "Python Practice Session"
- Session Date: Today
- Subject: Python Programming
- Session Type: Practice Problems
- Start Time: Today 2:00 PM
- End Time: Today 3:30 PM
- Focus Quality: 👍 Normal
- Energy Level: 🔄 Medium
- Tasks Completed: Link "Complete Python Function Exercises"
- Materials Used: Textbook, AI Tool
- Location: Library

Session 3 - Evening Korean:
- Name: "Korean Speaking Practice"
- Session Date: Today
- Subject: Korean Language
- Session Type: Speaking
- Start Time: Today 7:00 PM
- End Time: Today 7:30 PM
- Focus Quality: 😕 Distracted
- Energy Level: 😴 Low
- Tasks Completed: Link "Korean Speaking Practice - Introductions"
- Struggles: "Too tired, need to practice earlier"
```

### Test Journal Entry
```
Daily Journal Entry:
- Date: Today
- Mood: 👍 Focused
- Sessions Today: Link all 3 sessions above

Page Content:
## 📝 Daily Reflections

### ✅ What I Accomplished Today
- Completed 45 minutes of Korean study
- Finished Python function exercises
- Practiced Korean speaking for 30 minutes
- Total study time: 2 hours 45 minutes

### 💭 Random Thoughts & Ideas
- Morning is definitely my best time for language learning
- Need to find a Korean conversation partner
- Python clicking better after today's practice
- Consider moving speaking practice to morning when energy is higher

### ⚡ Energy Levels Throughout the Day
**Morning**: High - Deep focus during flashcards
**Afternoon**: Medium - Good for coding
**Evening**: Low - Too tired for speaking practice

### 💡 Key Insights & Learnings
- Korean particles finally making sense!
- Python functions are just like math functions
- Need to schedule difficult tasks when energy is high

### 🎯 Tomorrow's Focus
[ ] Complete Korean Chapter 5 exercises
[ ] Start Python OOP chapter
[ ] Schedule speaking practice for morning
[ ] Review all this week's vocabulary

### 🙏 Gratitude
I'm grateful for:
1. Having time to study what I love
2. The "aha" moment with Korean particles
3. Access to great learning resources
```

---

## ✅ Testing Checklist

### 1. Subject Master Testing
- [ ] All 3 subjects created with templates
- [ ] Check formula: Subject ID generates correctly
- [ ] Current Streak shows 0 (expected)
- [ ] Status dropdown works
- [ ] Priority levels display correctly
- [ ] Can switch between Active/Paused/Planning

### 2. Goals Hierarchy Testing
- [ ] All 5 goal levels created
- [ ] Parent-child relations visible
- [ ] Goal Path formula shows: "Yearly > Quarterly > Monthly > Weekly > Daily"
- [ ] Progress % shows 0% (no completed actions yet)
- [ ] Can navigate between parent/child goals
- [ ] Templates pre-fill Goal Type correctly

### 3. Daily Actions Testing
- [ ] All 5 actions created
- [ ] Relations to Goals work
- [ ] Relations to Subjects work
- [ ] Recurring checkbox functionality
- [ ] Templates set default values
- [ ] Difficulty Points (1-5) set correctly
- [ ] Can mark Completion Status

### 4. Daily Learning Sessions Testing
- [ ] Duration calculates correctly:
  - Session 1: 45 minutes
  - Session 2: 90 minutes
  - Session 3: 30 minutes
- [ ] Session ID format correct: "2025-01-05-Kor-45"
- [ ] XP Earned calculates:
  - Session 1: 45 × 1.5 (deep focus) = 67.5 → 68
  - Session 2: 90 × 1 = 90
  - Session 3: 30 × 1 = 30
- [ ] Can link multiple Tasks Completed
- [ ] Time must be enabled for duration to work

### 5. Journal Entries Testing
- [ ] Entry Title shows "2025-01-05 Journal"
- [ ] Can link multiple sessions
- [ ] Full page content saves correctly
- [ ] Templates provide structure
- [ ] Rollups calculate (after converting):
  - Total Time Today: 165 minutes
  - Subjects Studied: 2
  - XP Earned Today: 188

### 6. Cross-Database Relations
- [ ] Subject Master ← → Goals (bidirectional)
- [ ] Subject Master ← → Daily Actions (bidirectional)
- [ ] Subject Master ← → Learning Sessions (bidirectional)
- [ ] Goals ← → Daily Actions (bidirectional)
- [ ] Daily Actions ← → Learning Sessions (bidirectional)
- [ ] Learning Sessions → Journal Entries (one direction)

### 7. Formula Testing
- [ ] Subject ID: "LANG-001", "TECH-001", "PROF-001"
- [ ] Goal Path: Shows full hierarchy
- [ ] Session Duration: Calculates minutes correctly
- [ ] Session ID: Combines date + subject + duration
- [ ] XP Earned: Multiplies by focus quality
- [ ] Entry Title: Formats date correctly

### 8. Template Testing
- [ ] Subject Master: 1 template works
- [ ] Goals Hierarchy: 5 templates with correct Goal Types
- [ ] Daily Actions: 4 templates with pre-filled values
- [ ] Learning Sessions: 3 templates with defaults
- [ ] Journal Entries: 2 templates with page structures

---

## 🚨 Common Issues & Solutions

### Duration Shows 0
- Enable time on Start Time AND End Time properties
- End Time must be after Start Time

### Relations Not Linking
- Refresh the page
- Start typing slowly in relation field
- Make sure target database has entries

### Rollups Showing Wrong Count
- Use formulas instead (see NOTION_WORKAROUNDS.md)
- Apply filters to rollups
- Check calculation type

### Session ID Not Showing as Title
- Click "..." on Session ID → "Set as title"
- In Gallery view: configure card preview

### Templates Not Working
- Save template after adding values
- Make sure to fill in values before saving
- Some properties can't have defaults (Notion limitation)

---

## 🎯 Success Criteria

Your Foundation is working correctly when:
1. ✅ All relations link bidirectionally
2. ✅ All formulas calculate accurate values
3. ✅ Templates speed up data entry
4. ✅ You can track a full day's learning journey:
   - Plan actions → Complete sessions → Link to journal → Review insights
5. ✅ The workflow feels natural and sustainable

---

## 📋 Next Steps After Testing

1. **Clean up test data** (optional - keep if helpful)
2. **Create your real subjects** and goals
3. **Set up daily workflow**:
   - Morning: Review today's actions
   - During day: Log sessions as you complete them
   - Evening: Create journal entry and reflect
4. **Move to Phase 3**: Automation Layer

---

**Remember**: The goal is to make tracking effortless so you can focus on learning!