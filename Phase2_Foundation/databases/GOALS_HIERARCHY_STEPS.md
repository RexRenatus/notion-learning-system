# 🎯 Goals Hierarchy Database - Exact Implementation Steps

## Quick Reference Card

Step-by-step checklist for creating the Goals Hierarchy database with templates.

---

## 📋 Step-by-Step Implementation

### Step 1: Create Database
```
Action: Type /database → Select "Database - Full page"
Name: 🎯 Goals Hierarchy
```

### Step 2: Configure Title Property
```
Action: Click on "Name" property → Rename to "Goal Title"
Type: Title (default)
```

### Step 3: Add Each Property

#### ✅ Property: Goal Type
```
Name: Goal Type
Type: Select
Options:
  - Yearly
  - Quarterly
  - Monthly
  - Weekly
  - Daily
```

#### ✅ Property: Parent Goal
```
Name: Parent Goal
Type: Relation
Search for: Goals Hierarchy ← This same database!
Allow linking to multiple pages: Yes
```
**Note**: This creates "Parent Goal" and auto-creates "Subgoals" property

#### ✅ Property: Subject
```
Name: Subject
Type: Relation
Search for: Subject Master
Limit to: 1 page
```

#### ✅ Property: Actions (IMPORTANT - Needed for Phase 3)
```
Name: Actions
Type: Relation
Search for: Daily Actions
No limit on pages
Toggle ON: Show on Daily Actions
```
**Note**: This creates bidirectional relation for progress tracking

#### ✅ Property: Target Date
```
Name: Target Date
Type: Date
Format: Month day, year
```

#### ✅ Property: Created Date
```
Name: Created Date
Type: Created time
Format: Month day, year
```

#### ✅ Property: Status
```
Name: Status
Type: Select
Options:
  - Not Started
  - In Progress
  - Completed
  - Paused
  - Cancelled
```

#### ✅ Property: Priority
```
Name: Priority
Type: Select
Options:
  - 🔥 Critical
  - ⚡ High
  - 🔄 Normal
  - 💤 Low
```

#### ✅ Property: Success Metrics
```
Name: Success Metrics
Type: Text
```

#### ✅ Property: Decomposition Notes
```
Name: Decomposition Notes
Type: Text
```

#### ✅ Property: Estimated Hours
```
Name: Estimated Hours
Type: Number
Format: Number
```

#### ✅ Property: Subgoals
```
Note: This was auto-created when you made Parent Goal relation
Action: Find it in properties list (might need to show all)
Should already be configured correctly
```

#### ✅ Property: Total Subgoals
```
Name: Total Subgoals
Type: Rollup
Configuration:
  - Relation: Subgoals
  - Property: Goal Title
  - Calculate: Count
```

#### ✅ Property: Completed Subgoals
```
Name: Completed Subgoals
Type: Rollup
Configuration:
  - Relation: Subgoals
  - Property: Status
  - Calculate: Count
  - Show as: Number
  - Filter: Add filter → Status is Completed
```

#### ✅ Property: Progress Percentage (FORMULA)
```
Name: Progress Percentage
Type: Formula
```
**Copy this formula exactly:**
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

#### ✅ Property: Actual Hours
```
Name: Actual Hours
Type: Rollup
Note: Skip for now - needs Sessions relation (created later)
```

---

## 📝 Create Database Templates

### Template 1: Yearly Goal
1. Click "New" dropdown → "+ New template"
2. Name: "📅 Yearly Goal"
3. Set these values:
   ```
   Goal Type: Yearly
   Status: Not Started
   Priority: ⚡ High
   ```
4. Save template

### Template 2: Quarterly Goal
1. Click "New" dropdown → "+ New template"
2. Name: "📆 Quarterly Goal"
3. Set these values:
   ```
   Goal Type: Quarterly
   Status: Not Started
   Priority: 🔄 Normal
   ```
4. Save template

### Template 3: Monthly Goal
1. Click "New" dropdown → "+ New template"
2. Name: "📄 Monthly Goal"
3. Set these values:
   ```
   Goal Type: Monthly
   Status: Not Started
   Priority: 🔄 Normal
   ```
4. Save template

### Template 4: Weekly Goal
1. Click "New" dropdown → "+ New template"
2. Name: "📋 Weekly Goal"
3. Set these values:
   ```
   Goal Type: Weekly
   Status: Not Started
   Priority: 🔄 Normal
   ```
4. Save template

### Template 5: Daily Action
1. Click "New" dropdown → "+ New template"
2. Name: "✅ Daily Goal"
3. Set these values:
   ```
   Goal Type: Daily
   Status: Not Started
   Priority: 🔄 Normal
   ```
4. Save template

---

## 🧪 Test Your Database

### Create Test Hierarchy
1. **Create Yearly Goal** (using template):
   - Goal Title: **Master Korean to B2 Level**
   - Subject: **Korean Language** (link to your Subject Master entry)
   - Target Date: **December 31, 2025**
   - Status: Change to **In Progress**

2. **Create Quarterly Goal**:
   - Goal Title: **Complete Korean Level 1**
   - Parent Goal: **Master Korean to B2 Level** (link to above)
   - Subject: **Korean Language**
   - Target Date: **March 31, 2025**
   - Status: **In Progress**

3. **Create Monthly Goal**:
   - Goal Title: **Master Basic Korean Grammar**
   - Parent Goal: **Complete Korean Level 1**
   - Subject: **Korean Language**
   - Target Date: **January 31, 2025**

### Verify These Work:
- [ ] Parent-child relationships show correctly
- [ ] Progress Percentage shows:
  - 0% for "Not Started" goals
  - 100% for "Completed" goals
  - Calculated % based on subgoals
- [ ] Subgoals appear under parent goals

---

## ✅ Final Checklist

Before moving to next database:
- [ ] All properties created (skip Actual Hours for now)
- [ ] Progress Percentage formula works
- [ ] All 5 templates created
- [ ] Test hierarchy shows proper relationships
- [ ] Progress updates when changing child status

---

## 🚨 Troubleshooting

### "Formula invalid" error
- Ensure Total Subgoals and Completed Subgoals are created first
- Check property names match exactly
- Status options must match formula exactly ("Completed" not "Complete")

### Parent Goal not linking
- Make sure you selected "Goals Hierarchy" (this database)
- Enable "multiple pages" option
- Save and refresh if needed

### Progress not calculating
- Parent needs at least one subgoal
- Check the filter on Completed Subgoals rollup
- Verify Status has "Completed" option

---

## 📸 Success Indicators

Your database should:
1. Show goal hierarchies (parent → child → grandchild)
2. Calculate progress automatically
3. Have 5 ready-to-use templates
4. Link properly to Subject Master

---

## ⏭️ Next Step
Once verified, proceed to create **Daily Actions** database!

---

**Pro Tip**: Use the templates! They save time and ensure consistency.