# ✅ Daily Actions Database - Exact Implementation Steps

## Quick Reference Card

Step-by-step checklist for creating the Daily Actions database with templates.

---

## 📋 Step-by-Step Implementation

### Step 1: Create Database
```
Action: Type /database → Select "Database - Full page"
Name: ✅ Daily Actions
```

### Step 2: Configure Title Property
```
Action: Click on "Name" property → Rename to "Action Title"
Type: Title (default)
```

### Step 3: Add Each Property

#### ✅ Property: Parent Goal
```
Name: Parent Goal
Type: Relation
Search for: Goals Hierarchy
Limit to: 1 page
```

#### ✅ Property: Subject
```
Name: Subject
Type: Relation
Search for: Subject Master
Limit to: 1 page
```

#### ✅ Property: Action Type
```
Name: Action Type
Type: Select
Options:
  - Study
  - Practice
  - Review
  - Create
  - Test
```

#### ✅ Property: Estimated Time
```
Name: Estimated Time
Type: Number
Format: Number
Description: Minutes
```

#### ✅ Property: Scheduled Date
```
Name: Scheduled Date
Type: Date
Format: Month day, year
```

#### ✅ Property: Completion Status
```
Name: Completion Status
Type: Checkbox
```

#### ✅ Property: Completed Date
```
Name: Completed Date
Type: Date
Format: Month day, year
```

#### ✅ Property: Recurring
```
Name: Recurring
Type: Checkbox
```

#### ✅ Property: Recurrence Pattern
```
Name: Recurrence Pattern
Type: Select
Options:
  - Daily
  - Weekdays
  - Weekly
  - Custom
```

#### ✅ Property: Difficulty Points
```
Name: Difficulty Points
Type: Number
Format: Number
Description: 1=Easy, 5=Very Hard
```

#### ✅ Property: Specific Instructions
```
Name: Specific Instructions
Type: Text
```

#### ✅ Property: Success Criteria
```
Name: Success Criteria
Type: Text
```

#### ✅ Property: Reminder Sent
```
Name: Reminder Sent
Type: Checkbox
```

#### ✅ Property: Reminder Time
```
Name: Reminder Time
Type: Select
Options:
  - 09:30
  - 15:00
  - 19:00
  - Custom
```

#### ✅ Property: Bumped Count
```
Name: Bumped Count
Type: Number
Format: Number
Default: 0 (will set in template)
```

#### ✅ Note: Skip These for Now
```
- Sessions (will auto-create when we link from Sessions database)
- Actual Time (will add after Sessions database exists)
```

---

## 📝 Create Database Templates

### Template 1: Daily Study Task
1. Click "New" dropdown → "+ New template"
2. Name: "📚 Daily Study"
3. Set these values:
   ```
   Action Type: Study
   Estimated Time: 30
   Completion Status: Unchecked
   Recurring: Checked
   Recurrence Pattern: Daily
   Difficulty Points: 2
   Reminder Time: 09:30
   Bumped Count: 0
   ```
4. Save template

### Template 2: Practice Task
1. Click "New" dropdown → "+ New template"
2. Name: "🎯 Practice Task"
3. Set these values:
   ```
   Action Type: Practice
   Estimated Time: 45
   Completion Status: Unchecked
   Recurring: Unchecked
   Difficulty Points: 3
   Reminder Time: 15:00
   Bumped Count: 0
   ```
4. Save template

### Template 3: Review Task
1. Click "New" dropdown → "+ New template"
2. Name: "🔄 Review Task"
3. Set these values:
   ```
   Action Type: Review
   Estimated Time: 20
   Completion Status: Unchecked
   Recurring: Checked
   Recurrence Pattern: Weekly
   Difficulty Points: 1
   Reminder Time: 19:00
   Bumped Count: 0
   ```
4. Save template

### Template 4: Test/Assessment
1. Click "New" dropdown → "+ New template"
2. Name: "📝 Test Task"
3. Set these values:
   ```
   Action Type: Test
   Estimated Time: 60
   Completion Status: Unchecked
   Recurring: Unchecked
   Difficulty Points: 4
   Bumped Count: 0
   ```
4. Save template

---

## 🧪 Test Your Database

### Create Test Actions
1. **Daily Korean Study** (using Daily Study template):
   - Action Title: **Study 20 Korean Flashcards**
   - Parent Goal: **Master Basic Korean Grammar** (link to your monthly goal)
   - Subject: **Korean Language**
   - Scheduled Date: **Today**
   - Specific Instructions: **Focus on verb conjugations**
   - Success Criteria: **All cards reviewed with 80%+ accuracy**

2. **Speaking Practice** (using Practice template):
   - Action Title: **15-min Korean Conversation**
   - Parent Goal: **Complete Korean Level 1**
   - Subject: **Korean Language**
   - Scheduled Date: **Today**
   - Specific Instructions: **Practice introducing yourself**
   - Success Criteria: **Complete without using English**

3. **Weekly Review** (using Review template):
   - Action Title: **Review Week's Vocabulary**
   - Parent Goal: **Master Basic Korean Grammar**
   - Subject: **Korean Language**
   - Scheduled Date: **This Sunday**

### Verify These Work:
- [ ] Relations to Goals and Subjects link properly
- [ ] Templates pre-fill all default values
- [ ] Bumped Count shows 0
- [ ] Can check/uncheck Completion Status
- [ ] Recurring checkbox works

---

## 🎯 Testing Scenarios

### Scenario 1: Bumping a Task
1. Create a task for today
2. Don't complete it
3. Tomorrow, change Scheduled Date to tomorrow
4. Manually increase Bumped Count to 1
5. This tracks how many times you've postponed

### Scenario 2: Recurring Tasks
1. Create a daily recurring task
2. Check Completion Status
3. Note: You'll need to manually create tomorrow's instance
   (Notion doesn't auto-generate recurring tasks)

---

## ✅ Final Checklist

Before moving to next database:
- [ ] All 16 properties created
- [ ] 4 templates created with defaults
- [ ] Test actions link to goals and subjects
- [ ] Recurring and reminder options work
- [ ] Difficulty points are set (1-5 scale)

---

## 🚨 Common Issues

### Relations not showing options
- Make sure Goals Hierarchy and Subject Master are saved
- Refresh the page
- Start typing the database name slowly

### Template not saving values
- Make sure to enter the values before saving template
- Numbers need to be entered (0 for Bumped Count)
- Checkboxes need to be explicitly set

---

## 💡 Usage Tips

1. **Use templates** for consistency
2. **Link to specific goals** not just subjects
3. **Be specific** in instructions and success criteria
4. **Set realistic time estimates** in minutes
5. **Use difficulty points** to balance your daily load

---

## ⏭️ Next Step
Once verified, proceed to create **Daily Learning Sessions** database!

---

**Note**: The magic happens when Sessions link to Actions - you'll track estimated vs actual time!