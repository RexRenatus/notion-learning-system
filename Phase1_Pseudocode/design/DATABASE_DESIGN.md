# 🗄️ Database Design - Notion Learning System

## Overview
This document defines the complete database architecture for the learning system, incorporating all requirements including the AI Epiphany engine, process flowchart generator, and dopamine-driven gamification.

---

## 🏗️ Database Architecture

### Core Principle: Modular & Interconnected
- Each database has a single responsibility
- Relations enable rich data connections
- Formulas provide real-time calculations
- Views offer multiple perspectives

---

## 📊 Primary Databases

### 1. 📚 Subject Master Database
**Purpose**: Central registry of all learning subjects with gamification metadata

```yaml
Fields:
  - subject_name: 
      type: Title
      description: "Name of the subject (e.g., Korean, CFA Level 1)"
      
  - category:
      type: Select
      options: ["Language", "Finance", "Philosophy", "Programming", "Art", "Other"]
      
  - current_status:
      type: Select
      options: ["Active", "Paused", "Completed", "Planning"]
      default: "Active"
      
  - priority_level:
      type: Select
      options: ["Primary Focus", "Secondary", "Maintenance", "Future"]
      
  - date_started:
      type: Date
      
  - target_completion:
      type: Date
      
  - current_level:
      type: Number
      description: "Subject-specific level (1-100)"
      
  - total_xp:
      type: Number
      description: "Total XP earned in this subject"
      
  - current_streak:
      type: Number
      description: "Days studied consecutively"
      
  - best_streak:
      type: Number
      description: "Longest streak achieved"
      
  - last_studied:
      type: Date
      
  - auto_pause_warning:
      type: Formula
      formula: "if(dateBetween(now(), prop('Last Studied'), 'days') > 5, '⚠️ Auto-pause in ' + (7 - dateBetween(now(), prop('Last Studied'), 'days')) + ' days', '✅')"
      
  - color_theme:
      type: Select
      options: ["🔴 Red", "🟠 Orange", "🟡 Yellow", "🟢 Green", "🔵 Blue", "🟣 Purple"]
      
  - resources:
      type: URL
      description: "Link to learning resources"
      
  - money_invested:
      type: Number
      description: "Total money spent on this subject"
      
  - goal_statement:
      type: Text
      description: "Why am I learning this?"
      
  - daily_minimum:
      type: Number
      default: 15
      description: "Minimum minutes per day"
      
  - flashcard_target:
      type: Number
      default: 10
      description: "Current daily flashcard target"
      
  - next_increase_date:
      type: Formula
      formula: "dateAdd(prop('Last Increase'), 14, 'days')"
      
  - synergy_subjects:
      type: Relation
      target: "Subject Master"
      description: "Subjects that pair well with this"
```

### 2. 🎯 Goals Hierarchy Database
**Purpose**: Break down broad goals into achievable milestones

```yaml
Fields:
  - goal_title:
      type: Title
      
  - goal_type:
      type: Select
      options: ["Yearly", "Quarterly", "Monthly", "Weekly", "Daily"]
      
  - parent_goal:
      type: Relation
      target: "Goals Hierarchy"
      description: "Self-referential for hierarchy"
      
  - subject:
      type: Relation
      target: "Subject Master"
      
  - target_date:
      type: Date
      
  - created_date:
      type: Created Time
      
  - status:
      type: Select
      options: ["Not Started", "In Progress", "Completed", "Paused", "Cancelled"]
      default: "Not Started"
      
  - progress_percentage:
      type: Formula
      formula: |
        if(prop("Goal Type") == "Daily",
          if(prop("Completion Status"), 100, 0),
          if(prop("Total Subgoals") > 0,
            round(100 * prop("Completed Subgoals") / prop("Total Subgoals")),
            0
          )
        )
        
  - subgoals:
      type: Relation
      target: "Goals Hierarchy"
      description: "Child goals"
      
  - total_subgoals:
      type: Rollup
      relation: "Subgoals"
      property: "Title"
      calculate: Count
      
  - completed_subgoals:
      type: Rollup
      relation: "Subgoals"
      property: "Status"
      calculate: Count
      filter: "Status == 'Completed'"
      
  - success_metrics:
      type: Text
      description: "How to measure success"
      
  - decomposition_notes:
      type: Text
      description: "Notes on breaking down this goal"
      
  - priority:
      type: Select
      options: ["🔥 Critical", "⚡ High", "🔄 Normal", "💤 Low"]
      
  - estimated_hours:
      type: Number
      description: "Total hours to complete"
      
  - actual_hours:
      type: Rollup
      relation: "Sessions"
      property: "Duration"
      calculate: Sum
```

### 3. 📝 Daily Learning Sessions Database
**Purpose**: Track individual study sessions with rich metadata

```yaml
Fields:
  - session_id:
      type: Title
      formula: "formatDate(prop('Session Date'), 'YYYY-MM-DD') + '-' + prop('Subject').name + '-' + prop('Session Number')"
      
  - session_date:
      type: Date
      
  - subject:
      type: Relation
      target: "Subject Master"
      
  - session_type:
      type: Multi-select
      options: ["Flashcards", "Reading", "Writing", "Speaking", "Listening", "Practice Problems", "Video", "Other"]
      
  - start_time:
      type: Date
      include_time: true
      
  - end_time:
      type: Date
      include_time: true
      
  - duration:
      type: Formula
      formula: "dateBetween(prop('End Time'), prop('Start Time'), 'minutes')"
      
  - focus_quality:
      type: Select
      options: ["🎯 Deep Focus", "👍 Normal", "😕 Distracted"]
      default: "👍 Normal"
      
  - energy_level:
      type: Select
      options: ["⚡ High", "🔄 Medium", "😴 Low"]
      
  - session_notes:
      type: Text
      description: "What happened during this session"
      
  - tasks_completed:
      type: Relation
      target: "Daily Actions"
      
  - breakthroughs:
      type: Text
      description: "Any 'aha' moments"
      
  - struggles:
      type: Text
      description: "What was difficult"
      
  - xp_earned:
      type: Formula
      formula: |
        round(
          prop('Duration') * 
          if(prop('Focus Quality') == '🎯 Deep Focus', 1.5, 1) *
          min(1 + (prop('Subject').currentStreak * 0.1), 2)
        )
        
  - streak_maintained:
      type: Checkbox
      
  - materials_used:
      type: Multi-select
      options: ["Textbook", "App", "Video", "Flashcards", "Notebook", "AI Tool", "Other"]
      
  - location:
      type: Select
      options: ["Home", "Library", "Cafe", "Office", "Transit", "Other"]
      
  - session_number:
      type: Formula
      formula: "length(prop('Subject').sessions) + 1"
```

### 4. ✅ Daily Actions Database
**Purpose**: Concrete, measurable tasks derived from goals

```yaml
Fields:
  - action_title:
      type: Title
      
  - parent_goal:
      type: Relation
      target: "Goals Hierarchy"
      
  - subject:
      type: Relation
      target: "Subject Master"
      
  - action_type:
      type: Select
      options: ["Study", "Practice", "Review", "Create", "Test"]
      
  - estimated_time:
      type: Number
      description: "Minutes"
      
  - actual_time:
      type: Rollup
      relation: "Sessions"
      property: "Duration"
      calculate: Sum
      
  - scheduled_date:
      type: Date
      
  - completion_status:
      type: Checkbox
      
  - completed_date:
      type: Date
      
  - recurring:
      type: Checkbox
      
  - recurrence_pattern:
      type: Select
      options: ["Daily", "Weekdays", "Weekly", "Custom"]
      
  - difficulty_points:
      type: Number
      min: 1
      max: 5
      description: "1=Easy, 5=Very Hard"
      
  - specific_instructions:
      type: Text
      description: "Exactly what to do"
      
  - success_criteria:
      type: Text
      description: "How to know it's done well"
      
  - reminder_sent:
      type: Checkbox
      
  - reminder_time:
      type: Select
      options: ["09:30", "15:00", "19:00", "Custom"]
      
  - bumped_count:
      type: Number
      default: 0
      description: "Times moved to next day"
```

### 5. 📔 Journal Entries Database
**Purpose**: Daily reflections with AI-generated epiphanies

```yaml
Fields:
  - entry_date:
      type: Title
      formula: "formatDate(prop('Date'), 'YYYY-MM-DD') + ' Journal'"
      
  - date:
      type: Date
      unique: true
      
  - tasks_completed:
      type: Text
      description: "What I accomplished today"
      
  - random_thoughts:
      type: Text
      description: "Stream of consciousness, ideas, observations"
      
  - todo_tomorrow:
      type: Text
      description: "What needs attention tomorrow"
      
  - reflections:
      type: Text
      description: "How did today go? What did I learn?"
      
  - mood:
      type: Select
      options: ["😊 Energized", "👍 Focused", "😐 Neutral", "😔 Struggled", "🔥 Breakthrough"]
      
  - key_insights:
      type: Text
      description: "Important realizations"
      
  - hidden_todos:
      type: Text
      description: "Tasks mentioned in thoughts but not formalized"
      
  - epiphany_section:
      type: Text
      description: "AI-generated patterns and actionable todos"
      
  - ai_analysis_complete:
      type: Checkbox
      
  - summary_sent:
      type: Checkbox
      
  - sessions_today:
      type: Relation
      target: "Daily Learning Sessions"
      
  - total_time_today:
      type: Rollup
      relation: "Sessions Today"
      property: "Duration"
      calculate: Sum
      
  - subjects_studied:
      type: Rollup
      relation: "Sessions Today"
      property: "Subject"
      calculate: Count unique
      
  - calendar_events:
      type: Text
      description: "Imported from Google Calendar"
      
  - energy_pattern:
      type: Text
      description: "AI-identified energy flow"
```

---

## 🎮 Gamification Databases

### 6. 🏆 Achievements Database
**Purpose**: Track unlocked achievements and badges

```yaml
Fields:
  - achievement_name:
      type: Title
      
  - achievement_type:
      type: Select
      options: ["Streak", "Milestone", "Challenge", "Special", "Hidden"]
      
  - description:
      type: Text
      
  - unlock_criteria:
      type: Text
      description: "What triggers this achievement"
      
  - icon:
      type: Select
      options: ["🔥", "⭐", "🏆", "💎", "🎯", "🚀", "👑", "💪"]
      
  - xp_reward:
      type: Number
      
  - unlocked:
      type: Checkbox
      
  - unlock_date:
      type: Date
      
  - rarity:
      type: Select
      options: ["Common", "Uncommon", "Rare", "Epic", "Legendary"]
      
  - progress_formula:
      type: Formula
      description: "Shows progress toward unlocking"
```

### 7. 📈 Progress Snapshots Database
**Purpose**: Weekly/monthly progress captures for trend analysis

```yaml
Fields:
  - snapshot_date:
      type: Title
      formula: "formatDate(prop('Date'), 'YYYY-MM-DD') + ' - ' + prop('Period')"
      
  - date:
      type: Date
      
  - period:
      type: Select
      options: ["Daily", "Weekly", "Monthly"]
      
  - subjects_data:
      type: Text
      description: "JSON of subject progress"
      
  - total_xp:
      type: Number
      
  - total_hours:
      type: Number
      
  - streaks_data:
      type: Text
      description: "JSON of all streaks"
      
  - achievements_unlocked:
      type: Number
      
  - goals_completed:
      type: Number
      
  - consistency_rate:
      type: Number
      description: "Percentage of days with study"
      
  - ai_insights:
      type: Text
      description: "Pattern analysis"
```

---

## 🔄 Special Feature Databases

### 8. 🔄 Process Library Database
**Purpose**: Store AI-generated process flowcharts

```yaml
Fields:
  - process_name:
      type: Title
      
  - process_type:
      type: Select
      options: ["Study Routine", "Decision Tree", "Workflow", "Problem Solving", "Review Process"]
      
  - subject:
      type: Relation
      target: "Subject Master"
      
  - questionnaire_responses:
      type: Text
      description: "Original user input"
      
  - ai_refinements:
      type: Text
      description: "How AI improved the process"
      
  - flowchart_image:
      type: Files
      description: "Generated SVG/PNG flowchart"
      
  - mermaid_code:
      type: Code
      description: "Flowchart source code"
      
  - created_date:
      type: Created Time
      
  - last_used:
      type: Date
      
  - times_used:
      type: Number
      default: 0
      
  - effectiveness_rating:
      type: Select
      options: ["⭐⭐⭐⭐⭐", "⭐⭐⭐⭐", "⭐⭐⭐", "⭐⭐", "⭐"]
      
  - tags:
      type: Multi-select
      
  - related_processes:
      type: Relation
      target: "Process Library"
      
  - improvement_notes:
      type: Text
```

### 9. 💰 Learning Investments Database
**Purpose**: Track money spent on learning resources

```yaml
Fields:
  - purchase_name:
      type: Title
      
  - subject:
      type: Relation
      target: "Subject Master"
      
  - purchase_date:
      type: Date
      
  - amount:
      type: Number
      
  - currency:
      type: Select
      options: ["USD", "EUR", "KRW", "CNY"]
      default: "USD"
      
  - category:
      type: Select
      options: ["Course", "Book", "App", "Tutor", "Exam Fee", "Tool", "Other"]
      
  - recurring:
      type: Checkbox
      
  - billing_period:
      type: Select
      options: ["One-time", "Monthly", "Yearly"]
      
  - value_rating:
      type: Select
      options: ["💎 Excellent", "👍 Good", "🤷 Okay", "👎 Poor"]
      
  - notes:
      type: Text
      
  - roi_calculation:
      type: Formula
      description: "Return on investment based on usage"
```

### 10. 🔔 Notification Queue Database
**Purpose**: Manage all system notifications and reminders

```yaml
Fields:
  - notification_id:
      type: Title
      
  - notification_type:
      type: Select
      options: ["Reminder", "Achievement", "Summary", "Alert", "Motivation"]
      
  - scheduled_time:
      type: Date
      include_time: true
      
  - recipient:
      type: Select
      options: ["Telegram", "Email", "Notion", "Multiple"]
      
  - content:
      type: Text
      
  - urgency:
      type: Select
      options: ["🚨 Urgent", "⚡ High", "🔄 Normal", "💤 Low"]
      
  - sent:
      type: Checkbox
      
  - sent_time:
      type: Date
      include_time: true
      
  - related_subject:
      type: Relation
      target: "Subject Master"
      
  - related_action:
      type: Relation
      target: "Daily Actions"
      
  - emoji_style:
      type: Checkbox
      default: true
      description: "Use urgent emojis"
```

---

## 🔗 Key Relationships

### Primary Relations
1. **Subject Master ↔ Goals**: One-to-many
2. **Goals ↔ Goals**: Self-referential hierarchy
3. **Goals ↔ Daily Actions**: One-to-many
4. **Subject Master ↔ Sessions**: One-to-many
5. **Sessions ↔ Daily Actions**: Many-to-many
6. **Journal ↔ Sessions**: One-to-many (daily)

### Secondary Relations
7. **Subject Master ↔ Process Library**: One-to-many
8. **Subject Master ↔ Investments**: One-to-many
9. **Actions/Sessions ↔ Notifications**: One-to-many
10. **Subject Master ↔ Subject Master**: Many-to-many (synergies)

---

## 📊 Critical Formulas

### XP Calculation (Sessions)
```javascript
round(
  prop('Duration') * 
  if(prop('Focus Quality') == '🎯 Deep Focus', 1.5, 1) *
  min(1 + (prop('Subject').currentStreak * 0.1), 2) +
  sum(prop('Tasks Completed').difficultyPoints * 10)
)
```

### Progress Percentage (Goals)
```javascript
if(prop("Goal Type") == "Daily",
  if(prop("Completion Status"), 100, 0),
  if(prop("Total Subgoals") > 0,
    round(100 * prop("Completed Subgoals") / prop("Total Subgoals")),
    0
  )
)
```

### Auto-Pause Warning (Subjects)
```javascript
if(dateBetween(now(), prop('Last Studied'), 'days') > 5, 
  '⚠️ Auto-pause in ' + (7 - dateBetween(now(), prop('Last Studied'), 'days')) + ' days', 
  '✅'
)
```

### Habit Formation Check
```javascript
if(prop('Current Streak') >= 60,
  '✅ Second Nature (Day ' + prop('Current Streak') + ')',
  '🔄 Building Habit (' + prop('Current Streak') + '/60 days)'
)
```

---

## 🎯 Database Views

### 1. Today's Command Center
- Filter: Sessions Date = Today OR Actions Date = Today
- Group by: Subject
- Sort by: Priority, Scheduled Time
- Show: Progress bars, streaks, quick actions

### 2. AI Epiphany Dashboard
- Database: Journal Entries
- Filter: AI Analysis Complete = True
- Sort by: Date Descending
- Show: Epiphany sections, patterns, todos

### 3. Process Library Gallery
- Database: Process Library
- View: Gallery
- Sort by: Times Used, Effectiveness
- Show: Flowchart previews

### 4. Streak Tracker
- Database: Subject Master
- Filter: Status = Active
- Sort by: Current Streak Descending
- Show: Streak flames, last studied, warnings

### 5. Weekly Analytics
- Database: Progress Snapshots
- Filter: Period = Weekly
- View: Timeline
- Show: Trends, comparisons, insights

---

## 🔐 Data Integrity Rules

1. **One Journal per Day**: Date field unique
2. **Session Continuity**: End Time > Start Time
3. **Goal Hierarchy**: No circular references
4. **Streak Logic**: Reset if gap > 1 day
5. **XP Non-negative**: All calculations ≥ 0
6. **Progress Bounds**: 0 ≤ percentage ≤ 100

---

## 🚀 Implementation Notes

### Phase 1 Essentials
- Subject Master
- Goals Hierarchy
- Daily Sessions
- Daily Actions
- Journal Entries

### Phase 2 Additions
- Achievements
- Progress Snapshots
- Basic formulas

### Phase 3 Advanced
- Process Library
- Investment Tracking
- Notification Queue
- Complex formulas

---

**Last Updated**: 2025-07-04
**Status**: Design Complete
**Next Step**: Create Notion schemas document