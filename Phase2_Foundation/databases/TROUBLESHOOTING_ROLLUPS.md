# 🔧 Fixing Rollup Issues - Goals Hierarchy

## Problem: Completed Subgoals Showing Wrong Count

### 🔍 Diagnosis
The "Completed Subgoals" rollup is counting 1 even though no subgoals are marked "Completed".

---

## 🎯 Solution Steps

### Step 1: Check the Rollup Configuration

1. Click on the **Completed Subgoals** property
2. Click **Edit property**
3. Verify these settings:
   - Relation: **Subgoals**
   - Property: **Status**
   - Calculate: **Count**
   - Filter: Must be configured!

### Step 2: Fix the Filter

The filter is the critical part. Here's how to set it:

1. In the rollup configuration, look for **Filter**
2. Click **Add filter**
3. Set up the filter:
   ```
   Status → is → Completed
   ```
   
**Important**: The filter must match EXACTLY:
- Not "Complete" but "Completed"
- Not "contains" but "is"

### Step 3: Alternative Filter Methods

If the above doesn't work, try:

**Method A - Checkbox Method**:
1. Change the Calculate option to:
   - Property: **Status**
   - Calculate: **Count values**
   - Filter: **Status is Completed**

**Method B - Show Original**:
1. Change settings to:
   - Property: **Status**
   - Calculate: **Show original**
   - Then count manually in view

---

## 🔄 Complete Fix Process

1. **Delete the current Completed Subgoals property**
2. **Recreate it fresh**:
   ```
   Name: Completed Subgoals
   Type: Rollup
   Relation: Subgoals
   Property: Status
   Calculate: Count
   ```
3. **Add the filter**:
   - Click the filter icon
   - Add rule: Status → is → Completed
4. **Test immediately**:
   - Should show 0 for goals with no completed subgoals
   - Should show correct count when you mark subgoals complete

---

## 🧪 Test Your Fix

1. Your parent goal should now show:
   - Total Subgoals: 1 (or however many children it has)
   - Completed Subgoals: 0 (if none are completed)
   - Progress Percentage: 0%

2. Test by changing a subgoal:
   - Change one subgoal Status to "Completed"
   - Parent should update to show:
     - Completed Subgoals: 1
     - Progress Percentage: 100% (if only 1 subgoal)

---

## 🚨 Common Rollup Gotchas

### Issue: Filter not working
**Fix**: The Status value in the filter must match EXACTLY what's in your Select options

### Issue: Shows all values instead of count
**Fix**: Make sure Calculate is set to "Count" not "Show original"

### Issue: Updates delayed
**Fix**: Notion rollups can lag. Try:
- Refreshing the page
- Clicking out and back into the database
- Waiting a few seconds

---

## ✅ Verification Steps

After fixing, verify:
1. [ ] Parent with no completed children shows: Completed = 0
2. [ ] Parent with all completed children shows: Completed = Total
3. [ ] Progress Percentage calculates correctly
4. [ ] Changing child status updates parent immediately

---

## 📝 If Still Not Working

Try this nuclear option:
1. Screenshot your current setup
2. Delete both Total Subgoals and Completed Subgoals
3. Delete the Progress Percentage formula
4. Recreate all three in order:
   - First: Total Subgoals (no filter)
   - Second: Completed Subgoals (with filter)
   - Third: Progress Percentage formula
5. Test with fresh data

---

**Quick Check**: In your Completed Subgoals rollup, do you see a filter icon that says "Status is Completed"? If not, that's your issue!