# 🔧 Notion Workarounds & Solutions

## Default Values in Notion

Unfortunately, Notion doesn't support true default values for Number properties. Here are the solutions:

---

## 🎯 Solution 1: Database Templates (Recommended)

### How to Set Up:
1. In your Subject Master database, click the dropdown arrow next to "New" button
2. Click "+ New template"
3. Name it "New Subject Template"
4. In the template, set:
   - Daily Minimum: **15**
   - Flashcard Target: **10**
   - Current Status: **Active** (if you want this as default)
   - Current Level: **1**
   - Total XP: **0**
   - Current Streak: **0**
   - Best Streak: **0**
5. Save the template

### How to Use:
- When creating new subjects, click "New" → Select "New Subject Template"
- All default values will be pre-filled!

---

## 🎯 Solution 2: Quick-Fill Method

Since we only have a few subjects to create initially:
1. Create your subjects normally
2. For each one, manually enter:
   - Daily Minimum: 15
   - Flashcard Target: 10

---

## 🎯 Solution 3: Bulk Edit (For Multiple Entries)

1. Create all your subjects first (without the defaults)
2. In database view, select all entries (checkbox on left)
3. Right-click → "Edit property"
4. Set Daily Minimum to 15
5. Repeat for Flashcard Target to 10

---

## 📝 Updated Instructions for Subject Master

Since we can't set true defaults, here's what to do:

### Option A: Create Template Now
1. Before adding any subjects, create the template
2. Use template for all new subjects

### Option B: Manual Entry
1. Just remember to set:
   - Daily Minimum: 15
   - Flashcard Target: 10
   - For each subject you create

### Option C: Formula Workaround (Advanced)
Replace the Daily Minimum and Flashcard Target properties with formulas:

**Daily Minimum Formula:**
```
if(empty(prop("Custom Daily Minimum")), 15, prop("Custom Daily Minimum"))
```

**Flashcard Target Formula:**
```
if(empty(prop("Custom Flashcard Target")), 10, prop("Custom Flashcard Target"))
```

Then create two new Number properties:
- Custom Daily Minimum
- Custom Flashcard Target

This way, it shows 15 and 10 by default, but you can override by filling in the Custom fields.

---

## ✅ What This Means for Your Setup

1. **Don't worry about it!** The default values are nice-to-have, not critical
2. **Use templates** - They're actually better than defaults because you can set multiple fields
3. **For now**, just manually enter 15 and 10 when creating subjects

---

## 🎯 Creating Your First Template

Here's exactly how:

1. In Subject Master database
2. Click "New" dropdown → "+ New template"
3. Fill in these values:
   ```
   Subject Name: [Leave empty - fill when using]
   Current Status: Active
   Current Level: 1
   Total XP: 0
   Current Streak: 0
   Best Streak: 0
   Daily Minimum: 15
   Flashcard Target: 10
   ```
4. Name template: "📚 New Subject"
5. Save

Now every new subject starts with these values!

---

## 🚨 Other Notion Limitations You Might Hit

### 1. Can't Set Select Property Defaults
**Solution**: Use templates (same as above)

### 2. Formula Properties Can't Be Edited
**Solution**: This is by design - formulas auto-calculate

### 3. Relation Shows All Items
**Solution**: Use filters in views to show only relevant items

### 4. No Conditional Formatting in Formulas
**Solution**: Use emojis in formula output (like we did with ⚠️ and ✅)

---

## ✅ Bottom Line

The lack of default values doesn't affect functionality. You can either:
1. Use templates (best option)
2. Enter 15 and 10 manually (totally fine for now)
3. Skip it entirely (won't break anything)

The important thing is that the formulas work and relations are set up correctly!

---

**Last Updated**: 2025-07-05