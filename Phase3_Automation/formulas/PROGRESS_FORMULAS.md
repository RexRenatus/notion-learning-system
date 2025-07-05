# 📊 Progress Calculation Formulas

## ⚠️ CRITICAL: How to Enter Formulas
**DO NOT COPY-PASTE!** You must manually select properties from the dropdown in Notion's formula editor.  
**See `HOW_TO_ADD_FORMULAS.md` for detailed instructions!**

## Overview
Advanced formulas to automatically calculate progress across goals, subjects, and daily activities.

## 📌 Important Notion Limitations
- **Cannot access properties of related items in formulas** (e.g., can't get Session Date from Learning Sessions)
- **Cannot filter rollups by date** in formulas
- **Solution**: Use rollups for aggregations, formulas for calculations on direct properties

---

## 🎯 Goals Hierarchy - Progress Formulas

### 1. Actions Completed Count (New Property)
**Property Name**: Actions Completed  
**Type**: Formula  
**Purpose**: Count how many linked actions are marked complete

```
length(
  filter(
    prop("Actions"),
    prop("Completion Status") == true
  )
)
```

**Note**: This requires Actions relation to be set up

### 2. Total Actions Count (New Property)
**Property Name**: Total Actions  
**Type**: Formula  
**Purpose**: Count total number of linked actions

```
length(prop("Actions"))
```

### 3. Progress Percentage (Update Existing)
**Property Name**: Progress %  
**Type**: Formula  
**Purpose**: Calculate completion percentage

```
if(
  prop("Total Actions") > 0,
  round(prop("Actions Completed") / prop("Total Actions") * 100),
  0
)
```

### 4. Status Auto-Update (New Property)
**Property Name**: Auto Status  
**Type**: Formula  
**Purpose**: Automatically set status based on progress and dates

```
if(
  prop("Progress %") == 100,
  "✅ Completed",
  if(
    prop("Target Date") < now(),
    "⚠️ Overdue",
    if(
      prop("Progress %") > 0,
      "🚧 In Progress",
      "📋 Not Started"
    )
  )
)
```

### 5. Days Remaining (New Property)
**Property Name**: Days Left  
**Type**: Formula  
**Purpose**: Show days until target date

```
if(
  prop("Target Date") > now(),
  dateBetween(prop("Target Date"), now(), "days"),
  0
)
```

### 6. On Track Status (New Property)
**Property Name**: On Track  
**Type**: Formula  
**Purpose**: Are you on pace to complete by deadline?

```
if(
  prop("Goal Type") == "Yearly",
  if(
    prop("Progress %") >= (dateBetween(now(), dateSubtract(prop("Target Date"), 365, "days"), "days") / 365 * 100),
    "✅ On Track",
    "⚠️ Behind"
  ),
  if(
    prop("Goal Type") == "Monthly",
    if(
      prop("Progress %") >= (dateBetween(now(), dateSubtract(prop("Target Date"), 30, "days"), "days") / 30 * 100),
      "✅ On Track",
      "⚠️ Behind"
    ),
    ""
  )
)
```

---

## 📚 Subject Master - Progress Formulas

### 1. Active Sessions Count (New Property)
**Property Name**: Total Sessions  
**Type**: Rollup  
**Purpose**: Count total learning sessions

```
Relation: Learning Sessions
Property: Name (or any property)
Calculate: Count all
```

### 2. Time This Week (New Property)
**Property Name**: Time This Week (min)  
**Type**: Rollup  
**Purpose**: Total minutes studied (all time for now)

```
Relation: Learning Sessions
Property: Duration
Calculate: Sum
```

**Note**: Notion can't filter rollups by date in formulas. To get "this week" data, you'll need to create a filtered view or use the API.

### 3. Weekly Goal Progress (New Property)
**Property Name**: Weekly Progress %  
**Type**: Formula  
**Purpose**: Progress toward weekly time goal

**Prerequisites**: 
- Must have "Weekly Time Goal" property (Number, in minutes)
- Must have "Time This Week (min)" rollup from previous step

```
if(
  prop("Weekly Time Goal") > 0,
  round(prop("Time This Week (min)") / prop("Weekly Time Goal") * 100),
  0
)
```

**Note**: Since we can't filter by "this week", this shows progress toward your weekly goal based on ALL TIME. For true weekly tracking, manually reset or use views.

### 4. Last Session Date (New Property)
**Property Name**: Last Session Date  
**Type**: Rollup  
**Purpose**: Track most recent session

```
Relation: Learning Sessions
Property: Session Date
Calculate: Latest date
```

### 5. Days Since Last Session (New Property)
**Property Name**: Days Since Last  
**Type**: Formula  
**Purpose**: Calculate days since last study session

```
if(
  empty(prop("Last Session Date")),
  999,
  dateBetween(now(), prop("Last Session Date"), "days")
)
```

### 6. Study Status (New Property)
**Property Name**: Study Status  
**Type**: Formula  
**Purpose**: Visual indicator of study consistency

```
if(
  prop("Days Since Last") == 0,
  "🔥 Studied Today",
  if(
    prop("Days Since Last") == 1,
    "✅ Yesterday",
    if(
      prop("Days Since Last") <= 3,
      "⚠️ " + format(prop("Days Since Last")) + " days ago",
      "❌ Inactive"
    )
  )
)
```

### 7. Momentum Score (New Property)
**Property Name**: Momentum  
**Type**: Formula  
**Purpose**: Simple momentum indicator

```
round(
  if(prop("Days Since Last") == 0, 50, 0) +
  if(prop("Days Since Last") <= 1, 30, 0) +
  if(prop("Total Sessions") > 10, 20, 0)
)
```

---

## ✅ Daily Actions - Progress Formulas

### 1. Days Overdue (New Property)
**Property Name**: Days Overdue  
**Type**: Formula  
**Purpose**: How many days past scheduled date

```
if(
  and(
    prop("Completion Status") == false,
    prop("Scheduled Date") < now()
  ),
  dateBetween(now(), prop("Scheduled Date"), "days"),
  0
)
```

### 2. Priority Score (New Property)
**Property Name**: Priority Score  
**Type**: Formula  
**Purpose**: Combine multiple factors for smart sorting

```
(prop("Difficulty Points") * 10) +
(prop("Days Overdue") * 20) +
if(prop("Recurring") == true, 30, 0) +
if(prop("Action Type") == "Test", 25, 0)
```

**Note**: We can't access "Goal Type" through the Parent Goal relation. Instead, we prioritize recurring tasks and tests.

### 3. Time Value Ratio (New Property)
**Property Name**: ROI Score  
**Type**: Formula  
**Purpose**: Points per minute - efficiency metric

```
if(
  prop("Estimated Time") > 0,
  round(prop("Difficulty Points") / prop("Estimated Time") * 60),
  0
)
```

---

## 📚 Daily Learning Sessions - Enhanced Formulas

### 1. Efficiency Score (New Property)
**Property Name**: Efficiency  
**Type**: Formula  
**Purpose**: XP per minute

```
if(
  prop("Duration") > 0,
  round(prop("XP Earned") / prop("Duration") * 10) / 10,
  0
)
```

### 2. Session Quality (New Property)
**Property Name**: Quality Score  
**Type**: Formula  
**Purpose**: Comprehensive session rating

```
round(
  (if(prop("Focus Quality") == "🎯 Deep Focus", 40, 
    if(prop("Focus Quality") == "👍 Normal", 25, 10))) +
  (if(prop("Energy Level") == "⚡ High", 30,
    if(prop("Energy Level") == "🔄 Medium", 20, 10))) +
  (if(not empty(prop("Breakthroughs")), 20, 0)) +
  (if(prop("Streak Maintained") == true, 10, 0))
)
```

### 3. Optimal Time Indicator (New Property)
**Property Name**: Optimal Time  
**Type**: Formula  
**Purpose**: Was this during your peak hours?

```
if(
  and(
    hour(prop("Start Time")) >= 6,
    hour(prop("Start Time")) <= 11
  ),
  "🌅 Peak Morning",
  if(
    and(
      hour(prop("Start Time")) >= 14,
      hour(prop("Start Time")) <= 17
    ),
    "☀️ Good Afternoon",
    if(
      hour(prop("Start Time")) >= 20,
      "🌙 Late Session",
      "⏰ Off-Peak"
    )
  )
)
```

---

## 📓 Journal Entries - Analytics Formulas

### 1. Productivity Score (New Property)
**Property Name**: Daily Productivity  
**Type**: Formula  
**Purpose**: Overall productivity metric

```
round(
  (prop("Total Time Today") / 60 * 10) +
  (prop("XP Earned Today") / 10) +
  (prop("Subjects Studied") * 20)
)
```

### 2. Consistency Check (New Property)
**Property Name**: Consistency  
**Type**: Formula  
**Purpose**: Met daily minimums?

```
if(
  and(
    prop("Total Time Today") >= 30,
    prop("Subjects Studied") >= 1
  ),
  "✅ Consistent Day",
  "⚠️ Below Minimum"
)
```

### 3. Week Day Number (New Property)
**Property Name**: Day of Week  
**Type**: Formula  
**Purpose**: Get numeric day of week (0=Sunday, 6=Saturday)

```
day(prop("Date"))
```

### 4. Day Type (New Property)
**Property Name**: Day Type  
**Type**: Formula  
**Purpose**: Categorize for pattern analysis

```
if(
  or(
    day(prop("Date")) == 0,
    day(prop("Date")) == 6
  ),
  "🏖️ Weekend",
  "💼 Weekday"
)
```

**Note**: Notion's `day()` function returns the day of the week as a number (0=Sunday, 1=Monday, etc.)

---

## 🔧 Implementation Guide

### Step 1: Add to Goals Hierarchy
1. Add all 6 new formula properties
2. Test with a few goals that have actions
3. Verify progress calculations are accurate

### Step 2: Enhance Subject Master
1. Add the 5 progress tracking formulas
2. Create some test sessions to verify weekly calculations
3. Check momentum score makes sense

### Step 3: Update Daily Actions
1. Add priority and efficiency formulas
2. Sort by Priority Score to see smart ordering
3. Use ROI Score to identify quick wins

### Step 4: Enhance Sessions & Journal
1. Add quality metrics to sessions
2. Add productivity scoring to journal
3. Test consistency tracking

---

## 🎯 Testing Checklist

- [ ] Goal progress updates when actions are completed
- [ ] Weekly time tracking is accurate
- [ ] Streak calculation works correctly
- [ ] Priority scoring puts important tasks first
- [ ] Productivity metrics feel accurate
- [ ] All formulas handle empty/null values

---

## 💡 Pro Tips

1. **Start Simple**: Implement one formula at a time
2. **Test Edge Cases**: What happens with 0 values?
3. **Performance**: Complex formulas may slow large databases
4. **Iterate**: Adjust scoring weights based on your needs

---

**Next Step**: After formulas are working, move to Dashboard Views!