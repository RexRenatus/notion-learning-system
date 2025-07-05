# 🔧 Missing Weekly Time Goal Property Fix

## Issue Discovered
During Phase 3 formula implementation, the "Weekly Progress %" formula references a "Weekly Time Goal" property that wasn't included in the original Subject Master implementation guide.

---

## 🎯 The Fix

### Add to Subject Master Database:

**Property Name**: Weekly Time Goal  
**Type**: Number  
**Format**: Number  
**Description**: Target study minutes per week  
**Suggested Default**: 300 (equals 5 hours)

### Where to Add:
1. Open Subject Master database
2. Add new property after "Last Studied"
3. Configure as shown above
4. Set default value for existing subjects

---

## 📊 Common Weekly Goals

- **Casual Learning**: 150 minutes (2.5 hours)
- **Regular Study**: 300 minutes (5 hours)
- **Intensive Study**: 600 minutes (10 hours)
- **Full-Time Learning**: 1200 minutes (20 hours)

---

## ✅ After Adding

The following Phase 3 formulas will now work:
- Weekly Progress % (shows progress toward goal)
- Any dashboard views showing weekly targets

---

## 📝 Lesson Learned

When creating formulas that reference properties, always verify those properties exist in the implementation guide first!