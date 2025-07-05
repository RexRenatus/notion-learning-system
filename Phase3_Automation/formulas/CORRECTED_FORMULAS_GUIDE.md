# ✅ Corrected Formulas Guide - All Databases

## Overview
This guide contains all corrected formulas that work within Notion's limitations. Each formula has been tested and adjusted to use only direct properties or rollups.

---

## 🎯 Goals Hierarchy Formulas

### ✅ Formula 1: Actions Completed Count
**Property Name**: Actions Completed  
**Type**: Rollup (NOT Formula!)  
```
Relation: Actions
Property: Completion Status
Calculate: Count checked
```

### ✅ Formula 2: Total Actions Count
**Property Name**: Total Actions  
**Type**: Rollup (NOT Formula!)  
```
Relation: Actions
Property: Name (or any property)
Calculate: Count all
```

### ✅ Formula 3: Progress Percentage
**Property Name**: Progress %  
**Type**: Formula  
```
if(
  prop("Total Actions") > 0,
  round(prop("Actions Completed") / prop("Total Actions") * 100),
  0
)
```

### ✅ Formula 4: Auto Status
**Property Name**: Auto Status  
**Type**: Formula  
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

### ✅ Formula 5: Days Left
**Property Name**: Days Left  
**Type**: Formula  
```
if(
  prop("Target Date") > now(),
  dateBetween(prop("Target Date"), now(), "days"),
  0
)
```

### ✅ Formula 6: On Track Status
**Property Name**: On Track  
**Type**: Formula  
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

## 📚 Subject Master Formulas

### ✅ Formula 1: Total Sessions
**Property Name**: Total Sessions  
**Type**: Rollup  
```
Relation: Learning Sessions
Property: Name (or any property)
Calculate: Count all
```

### ✅ Formula 2: Time This Week (min)
**Property Name**: Time This Week (min)  
**Type**: Rollup  
```
Relation: Learning Sessions
Property: Duration
Calculate: Sum
```
**Note**: This shows ALL TIME, not just this week (Notion limitation)

### ✅ Formula 3: Weekly Progress %
**Property Name**: Weekly Progress %  
**Type**: Formula  
**Prerequisite**: Must have "Weekly Time Goal" property (Number)
```
if(
  prop("Weekly Time Goal") > 0,
  round(prop("Time This Week (min)") / prop("Weekly Time Goal") * 100),
  0
)
```

### ✅ Formula 4: Last Session Date
**Property Name**: Last Session Date  
**Type**: Rollup  
```
Relation: Learning Sessions
Property: Session Date
Calculate: Latest date
```

### ✅ Formula 5: Days Since Last
**Property Name**: Days Since Last  
**Type**: Formula  
```
if(
  empty(prop("Last Session Date")),
  999,
  dateBetween(now(), prop("Last Session Date"), "days")
)
```

### ✅ Formula 6: Study Status
**Property Name**: Study Status  
**Type**: Formula  
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

### ✅ Formula 7: Momentum
**Property Name**: Momentum  
**Type**: Formula  
```
round(
  if(prop("Days Since Last") == 0, 50, 0) +
  if(prop("Days Since Last") <= 1, 30, 0) +
  if(prop("Total Sessions") > 10, 20, 0)
)
```

---

## ✅ Daily Actions Formulas

### ✅ Formula 1: Days Overdue
**Property Name**: Days Overdue  
**Type**: Formula  
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

### ✅ Formula 2: Priority Score
**Property Name**: Priority Score  
**Type**: Formula  
```
(prop("Difficulty Points") * 10) +
(prop("Days Overdue") * 20) +
if(prop("Recurring") == true, 30, 0) +
if(prop("Action Type") == "Test", 25, 0)
```

### ✅ Formula 3: ROI Score
**Property Name**: ROI Score  
**Type**: Formula  
```
if(
  prop("Estimated Time") > 0,
  round(prop("Difficulty Points") / prop("Estimated Time") * 60),
  0
)
```

---

## 📚 Daily Learning Sessions Formulas

### ✅ Formula 1: Efficiency
**Property Name**: Efficiency  
**Type**: Formula  
```
if(
  prop("Duration") > 0,
  round(prop("XP Earned") / prop("Duration") * 10) / 10,
  0
)
```

### ✅ Formula 2: Quality Score
**Property Name**: Quality Score  
**Type**: Formula  
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

### ✅ Formula 3: Optimal Time
**Property Name**: Optimal Time  
**Type**: Formula  
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

## 📓 Journal Entries Formulas

### ✅ Formula 1: Daily Productivity
**Property Name**: Daily Productivity  
**Type**: Formula  
```
round(
  (prop("Total Time Today") / 60 * 10) +
  (prop("XP Earned Today") / 10) +
  (prop("Subjects Studied") * 20)
)
```

### ✅ Formula 2: Consistency
**Property Name**: Consistency  
**Type**: Formula  
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

### ✅ Formula 3: Day Type
**Property Name**: Day Type  
**Type**: Formula  
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

---

## 🔧 Implementation Order

### Phase 1: Foundation Rollups
1. Goals Hierarchy: Add Actions Completed & Total Actions rollups
2. Subject Master: Add Total Sessions & Time This Week rollups
3. Subject Master: Add Last Session Date rollup

### Phase 2: Core Formulas
1. Goals Hierarchy: Progress %, Auto Status, Days Left
2. Subject Master: Days Since Last, Study Status
3. Daily Actions: Days Overdue

### Phase 3: Advanced Formulas
1. Goals Hierarchy: On Track Status
2. Subject Master: Weekly Progress %, Momentum
3. Daily Actions: Priority Score, ROI Score
4. Learning Sessions: All 3 formulas
5. Journal Entries: All 3 formulas

---

## ⚠️ Critical Reminders

1. **ALWAYS use dropdown to select properties** - Never type property names
2. **Test with sample data** before full implementation
3. **Rollups must be created before formulas that use them**
4. **Check property names are EXACT** (case-sensitive)
5. **Weekly Time Goal property must exist** for Weekly Progress % to work

---

## 🚨 Common Errors & Fixes

### "Property not found"
- Use dropdown to select property
- Check exact spelling and case
- Ensure property exists in database

### "Invalid formula"
- Check parentheses match
- Verify all properties exist
- Use dropdown selection

### Formula shows 0 or empty
- Check if rollup has data
- Verify dates are filled in
- Test with simple values first

---

**Last Updated**: 2025-07-05
**Status**: All formulas corrected for Notion limitations