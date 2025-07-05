# 🔧 Correct Way to Count Filtered Items in Notion

## The Issue
Notion's rollup "Count" options don't filter by themselves. You need to use a different approach.

---

## ✅ Solution 1: Count Values + Filter (Correct Method)

### Steps:
1. **Edit "Completed Subgoals" property**
2. Set it up like this:
   - Relation: `Subgoals`
   - Property: `Status`
   - Calculate: **`Count values`** (not "Count all")
3. **Now you'll see the Filter option!**
4. Add filter:
   - Click "Filter"
   - Set: `Status` `is` `Completed`

The key is using **"Count values"** instead of "Count all"!

---

## ✅ Solution 2: Alternative Checkbox Method

If the above doesn't work, here's a bulletproof alternative:

### Step 1: Add a Formula to Goals
1. In Goals Hierarchy, add a new property:
   - Name: `Is Completed`
   - Type: Formula
   - Formula: `if(prop("Status") == "Completed", 1, 0)`

### Step 2: Update the Rollup
1. Edit "Completed Subgoals":
   - Relation: `Subgoals`
   - Property: `Is Completed` (the new formula)
   - Calculate: `Sum`

This counts 1 for each completed goal, 0 for others.

---

## ✅ Solution 3: Using Checkbox (Simplest)

### Step 1: Add Completion Checkbox
1. In Goals Hierarchy, add:
   - Name: `Is Complete`
   - Type: Checkbox

### Step 2: Update Rollup
1. Edit "Completed Subgoals":
   - Relation: `Subgoals`
   - Property: `Is Complete`
   - Calculate: `Count checked`

### Step 3: Workflow
- When marking a goal complete, check both Status and checkbox
- Or use an automation to sync them

---

## 🎯 Recommended Fix (Quickest)

Try this exact sequence:
1. Delete your current "Completed Subgoals" property
2. Create new Rollup property
3. Name: `Completed Subgoals`
4. Configure:
   ```
   Relation: Subgoals
   Property: Status
   Calculate: Count values ← This is the key!
   Filter: [Now visible] Status is Completed
   ```

---

## 🧪 Test It
- Parent with 0 completed children → Shows 0
- Parent with 1 completed child → Shows 1
- Progress formula updates correctly

---

## 📝 Why This Happens

Notion's rollup logic:
- **Count all**: Counts every linked item (no filter option)
- **Count values**: Counts non-empty values (filter option appears!)
- **Count unique values**: Counts distinct values
- **Sum/Average/etc**: For number properties

You need "Count values" to get the filter option!

---

**Quick Answer**: Change "Count all" to "Count values" and the filter option will appear!