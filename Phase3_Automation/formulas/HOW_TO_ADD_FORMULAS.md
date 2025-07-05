# 🎯 How to Add Formulas in Notion - CRITICAL GUIDE

## ⚠️ MOST COMMON MISTAKE

**DO NOT** just copy-paste formula text into the formula box!  
**YOU MUST** manually select properties from the dropdown menu within the formula editor.

---

## ✅ Correct Way to Add Formulas

### Step 1: Create the Formula Property
1. Click "+ New property"
2. Name your property
3. Select type: **Formula**
4. Click "Edit formula" to open the formula editor

### Step 2: Build the Formula Correctly

#### Example Formula:
```
if(
  prop("Total Actions") > 0,
  round(prop("Actions Completed") / prop("Total Actions") * 100),
  0
)
```

#### How to Build It:

1. **Type** `if(`
2. **Type** `prop(` 
3. **Click** the property dropdown that appears
4. **Select** "Total Actions" from the list (don't type it!)
5. **Type** `) > 0,`
6. **Type** `round(prop(`
7. **Click** dropdown and **select** "Actions Completed"
8. **Type** `) / prop(`
9. **Click** dropdown and **select** "Total Actions"
10. **Type** `) * 100), 0)`

### Visual Guide:
```
When you type prop( → A dropdown appears:
┌─────────────────────────┐
│ Select a property       │
├─────────────────────────┤
│ 📋 Actions Completed    │
│ 📊 Total Actions        │
│ 🎯 Goal Type           │
│ 📅 Target Date         │
└─────────────────────────┘
↑ CLICK the property you need!
```

---

## 🚫 What Goes Wrong with Copy-Paste

If you just paste `prop("Total Actions")`, Notion sees it as:
- ❌ Text string "Total Actions" (not recognized)
- ❌ Formula shows error or undefined
- ❌ Red error message appears

When you SELECT from dropdown, Notion sees it as:
- ✅ Actual property reference
- ✅ Formula calculates correctly
- ✅ Updates when data changes

---

## 💡 Pro Tips for Formula Entry

### 1. Use the Property Menu
- After typing `prop(`, wait for dropdown
- Start typing property name to filter
- Click or press Enter to select

### 2. Complex Formulas
For formulas with many properties:
1. Copy the formula to a text editor
2. Use it as a reference
3. Build it piece by piece in Notion
4. Select each property from dropdown

### 3. Testing Your Formula
- Create test entries with known values
- Verify calculations match expectations
- Check edge cases (0 values, empty fields)

---

## 📝 Example: Adding Progress % Formula

### The Formula:
```
if(
  prop("Total Actions") > 0,
  round(prop("Actions Completed") / prop("Total Actions") * 100),
  0
)
```

### Step-by-Step:
1. **Create property**: "Progress %"
2. **Type**: Formula
3. **Edit formula**
4. **Build it**:
   - Type: `if(prop(`
   - Select: "Total Actions" from dropdown
   - Type: `) > 0, round(prop(`
   - Select: "Actions Completed" from dropdown
   - Type: `) / prop(`
   - Select: "Total Actions" from dropdown
   - Type: `) * 100), 0)`
5. **Click**: Done

---

## 🔍 How to Verify It's Working

### Good Signs:
- ✅ No red error messages
- ✅ Shows a number (even if 0)
- ✅ Updates when you change related properties

### Bad Signs:
- ❌ Shows "undefined"
- ❌ Red error text
- ❌ Doesn't update with changes

---

## 🆘 Troubleshooting

### "Property not found" Error
- You typed the property name instead of selecting it
- Delete and rebuild using dropdown selection

### Formula Not Calculating
- Check all properties exist
- Verify property names match exactly
- Ensure all prop() use selected properties

### Showing Wrong Values
- Test with simple known values
- Check your math logic
- Verify property types (number vs text)

---

## 📋 Quick Reference

**Every time you see `prop("Something")` in a formula:**
1. Type `prop(`
2. Wait for dropdown
3. Click/select the property
4. Continue with formula

**Never:**
- Copy-paste the entire formula
- Type property names manually
- Ignore the dropdown menu

---

**Remember**: The dropdown is your friend! Always select, never type property names.