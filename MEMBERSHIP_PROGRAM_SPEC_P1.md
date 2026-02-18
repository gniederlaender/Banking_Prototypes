# Specification: Interactive Sparefroh Batches & Functional CTAs

**Prototype:** Membership Program  
**Priority:** P1 - Critical  
**Created:** 2026-02-16  
**Status:** Ready for Implementation

---

## Overview

This specification addresses two related critical UX issues:
1. Non-functional CTA buttons in the Dashboard
2. Non-interactive Sparefroh batch icons

Both issues stem from the same root cause: the prototype shows information but doesn't support meaningful user interaction.

---

## Requirement 1: Interactive Sparefroh Batch Icons

### Current State
- 7 batch icons displayed in a grid (5 active, 2 inactive)
- Clicking icons does nothing
- Hover shows only "Batch X - Active/Inactive" tooltip

### Target State
Clicking any batch icon should reveal how that batch was earned (or how to earn it).

### Implementation Details

#### For Active Batches
Display a modal or popover with:
```
┌─────────────────────────────────────┐
│ 🎉 Batch 3 - Earned!                │
├─────────────────────────────────────┤
│ Action: Set Up Automatic Savings    │
│ Earned on: 2026-01-15               │
│                                     │
│ You save €50/month automatically    │
│ to your "Vacation Fund" account.    │
│                                     │
│         [View Savings Setup]        │
└─────────────────────────────────────┘
```

#### For Inactive Batches
Display a modal with actionable guidance:
```
┌─────────────────────────────────────┐
│ 🔒 Batch 6 - Not Yet Earned         │
├─────────────────────────────────────┤
│ Suggested Action:                   │
│ Complete Financial Health Check     │
│                                     │
│ Review your financial profile and   │
│ complete our personalized health    │
│ assessment to earn this batch.      │
│                                     │
│ [Start Health Check] [Maybe Later]  │
└─────────────────────────────────────┘
```

### Data Model (for prototype)

```javascript
const batchData = [
  { id: 1, active: true, action: "savings_account", earnedDate: "2025-12-01", details: "Opened savings account 'Vacation Fund'" },
  { id: 2, active: true, action: "auto_savings", earnedDate: "2026-01-15", details: "€50/month to Vacation Fund" },
  { id: 3, active: true, action: "mobile_banking", earnedDate: "2026-01-20", details: "15 mobile transactions this month" },
  { id: 4, active: true, action: "contactless", earnedDate: "2026-01-22", details: "Activated Apple Pay" },
  { id: 5, active: true, action: "positive_balance", earnedDate: "2026-02-01", details: "3 consecutive months positive" },
  { id: 6, active: false, suggestedAction: "digital_statements", cta: "Go Paperless" },
  { id: 7, active: false, suggestedAction: "health_check", cta: "Start Health Check" }
];
```

### Acceptance Criteria
- [ ] Clicking active batch shows earned details modal
- [ ] Clicking inactive batch shows suggestion modal with CTA
- [ ] Modal can be closed with X button or click outside
- [ ] Works in both English and German
- [ ] Mobile responsive (modal centered, readable)

---

## Requirement 2: Functional CTA Buttons

### Current State
- "Set Up Auto-Savings" button only scrolls to measures section
- "View All Ways to Earn" button only scrolls to measures section
- No actual workflow initiated

### Target State
CTAs should initiate meaningful user flows.

### Implementation Details

#### "Set Up Auto-Savings" Button
Open a multi-step modal flow:

**Step 1: Source Account**
```
┌─────────────────────────────────────────┐
│ 💰 Set Up Automatic Savings             │
├─────────────────────────────────────────┤
│ Step 1 of 3: Choose Source Account      │
│                                         │
│ ○ Checking Account ****1134             │
│   Balance: €2,450.00                    │
│                                         │
│ ○ Salary Account ****5678               │
│   Balance: €3,120.00                    │
│                                         │
│              [Cancel] [Next →]          │
└─────────────────────────────────────────┘
```

**Step 2: Amount & Frequency**
```
┌─────────────────────────────────────────┐
│ 💰 Set Up Automatic Savings             │
├─────────────────────────────────────────┤
│ Step 2 of 3: Set Amount                 │
│                                         │
│ Save: [€ 50______] per [month ▼]        │
│                                         │
│ On day: [1st ▼] of each month           │
│                                         │
│ To: [Vacation Fund ▼]                   │
│                                         │
│         [← Back] [Cancel] [Next →]      │
└─────────────────────────────────────────┘
```

**Step 3: Confirmation**
```
┌─────────────────────────────────────────────┐
│ ✅ You're About to Earn a Batch!            │
├─────────────────────────────────────────────┤
│                                             │
│ €50.00 will be transferred monthly          │
│ from Checking ****1134                      │
│ to Vacation Fund                            │
│ starting on March 1st, 2026                 │
│                                             │
│ 🎯 This action will earn you 1 batch!       │
│                                             │
│         [← Back] [Cancel] [Confirm ✓]       │
└─────────────────────────────────────────────┘
```

**Success State (prototype only)**
```
┌─────────────────────────────────────────┐
│ 🎉 Congratulations!                     │
├─────────────────────────────────────────┤
│                                         │
│ Automatic savings set up successfully!  │
│                                         │
│ You earned 1 Sparefroh Batch!           │
│ [Animation: batch icon fills in]        │
│                                         │
│ Only 1 more batch to reach Platinum!    │
│                                         │
│               [Done]                    │
└─────────────────────────────────────────┘
```

#### "View All Ways to Earn" Button
- Current scroll behavior is acceptable
- Enhance: Add smooth scroll animation
- Enhance: Briefly highlight the measures section after scroll

### Acceptance Criteria
- [ ] "Set Up Auto-Savings" opens multi-step modal
- [ ] All steps navigable forward/back
- [ ] Cancel closes modal at any step
- [ ] Confirm shows success with batch animation (mock)
- [ ] Updates batch count from 5/7 to 6/7 (in prototype session)
- [ ] "View All Ways to Earn" smooth scrolls and highlights section
- [ ] Works in both English and German

---

## Technical Notes

### Existing Modal Infrastructure
The prototype already has a modal system in place (`.modal`, `.modal-content`, etc.). Extend this pattern:

```javascript
function showBatchModal(batchId) {
  const batch = batchData.find(b => b.id === batchId);
  // Populate modal content based on batch.active
  document.getElementById('batchModal').classList.add('show');
}
```

### State Management (Prototype)
For prototype purposes, batch state can be managed in localStorage to persist across page reloads:

```javascript
const defaultState = { activeBatches: [1,2,3,4,5], selectedBenefits: [1,2,3] };
const state = JSON.parse(localStorage.getItem('membershipState')) || defaultState;
```

### i18n Additions Required
Add to translations object:
```javascript
{
  "batch.earned": "Earned!",
  "batch.not_earned": "Not Yet Earned",
  "batch.earned_on": "Earned on",
  "batch.suggested_action": "Suggested Action",
  "batch.start_action": "Start",
  "batch.maybe_later": "Maybe Later",
  "autosave.title": "Set Up Automatic Savings",
  "autosave.step1": "Choose Source Account",
  "autosave.step2": "Set Amount",
  "autosave.step3": "Confirm",
  "autosave.success": "Automatic savings set up successfully!",
  "autosave.earned_batch": "You earned 1 Sparefroh Batch!"
}
```

---

## Out of Scope

- Actual backend integration
- Real account data
- Persistent state across sessions (beyond localStorage prototype)
- Email/notification sending

---

## Estimated Effort

- Interactive batches: 3-4 hours
- Auto-savings flow: 4-6 hours
- i18n updates: 1-2 hours
- Testing & polish: 2-3 hours

**Total: ~12-15 hours**

---

## Related Documentation

- UI/UX Analysis: `MEMBERSHIP_PROGRAM_UX_ANALYSIS.md`
- George UI Guide: `GEORGE_UI.md`
- Prototype: `/prototypes/membership-program.html`
