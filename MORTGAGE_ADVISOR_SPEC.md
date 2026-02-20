# Conversational Mortgage Advisor Agent - Functional Specification

## Overview
A conversational mortgage advisor prototype for smartprototypes.net/banking. The agent flips the traditional mortgage flow: instead of asking for everything upfront, it leverages existing customer data and shows what's already available vs. what's still needed.

**Key Innovation:** Pre-approval BEFORE property search. Customer gets a confirmed limit, then shops with confidence.

## Technical Constraints
- **Visual prototype only** - no actual NLP/interpretation of user input
- **Mobile-first** design
- **No side panels** - pure conversational interface
- **George-style UI** - clean, professional, minimal
- **Pre-scripted flow** - user taps suggested responses or uploads docs

## Design Principles
- Conversational tone: professional, explanatory, helpful
- No avatar - just chat bubbles
- No chrome/progress indicators - purely conversational
- Celebrations for key moments (limit reveal)

---

## User Flow

### Entry Point
User is already logged into George (banking app). Conversation starts directly.

---

## PHASE 1: Pre-Approval

### Step 1.1: Conversation Start
**User:** "Ich möchte ein Haus kaufen, kannst du mir bei der Finanzierung helfen?"

**Agent:** "Natürlich! Ich helfe dir gerne bei deiner Immobilienfinanzierung. Lass mich kurz prüfen, welche Informationen wir bereits haben..."

*[Loading animation - 2-3 seconds, e.g., pulsing dots or spinning indicator]*

### Step 1.2: Document Journey Reveal
**Agent:** "Gute Nachrichten! Wir haben bereits einiges von dir:"

*[Document Journey View - Visual Component]*
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📍 PRE-APPROVAL                    ← Du bist hier
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   ✓ Identität verifiziert
   ✓ Einkommensnachweise (letzte 3 Monate)
   
   ○ Lohnzettel hochladen           [Hochladen]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
○ FINANZIERUNG ABSCHLIESSEN         Später
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   ○ Kaufvertrag
   ○ Energieausweis
   ○ Grundbuchauszug
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Agent:** "Für dein Pre-Approval Limit brauche ich nur noch deinen aktuellen Lohnzettel. Die restlichen Dokumente werden erst relevant, wenn du eine Immobilie gefunden hast."

### Step 1.3: Document Upload
User taps "Hochladen" button.

*[Upload Modal]*
- Camera icon: "Foto aufnehmen"
- Gallery icon: "Aus Galerie wählen"
- File icon: "Datei hochladen"

*[After selection: Document preview with "Hochladen" confirmation button]*

**Agent:** "Perfekt, ich habe deinen Lohnzettel erhalten. Ich berechne jetzt dein persönliches Finanzierungslimit..."

*[Processing animation - 3-4 seconds with subtle progress indication]*

### Step 1.4: Limit Reveal (KEY MOMENT 🎉)
**Agent:** "Herzlichen Glückwunsch!"

*[Big animated number reveal - starts small, scales up with subtle celebration effect]*
```
┌─────────────────────────────────────┐
│                                     │
│      Dein Pre-Approval Limit        │
│                                     │
│          € 385.000                  │
│            ████████████             │
│                                     │
│   Basierend auf deinem Einkommen    │
│   und deiner Bonität                │
│                                     │
└─────────────────────────────────────┘
```

**Agent:** "Mit deinem Einkommen und deiner ausgezeichneten Bonität kannst du eine Immobilie bis zu €385.000 finanzieren."

### Step 1.5: Parameter Adjustment
**Agent:** "Möchtest du die Finanzierungsparameter anpassen?"

*[Quick reply buttons]*
- "Ja, Parameter anpassen"
- "Nein, passt so"

**If user selects "Ja, Parameter anpassen":**

*[Parameter Adjustment Card]*
```
┌─────────────────────────────────────┐
│ Finanzierungsparameter anpassen     │
├─────────────────────────────────────┤
│                                     │
│ Laufzeit                            │
│ ○ 10 J  ○ 15 J  ● 20 J  ○ 25 J ○ 30 J │
│                                     │
│ Gewünschte monatliche Rate          │
│ [━━━━━━━━●━━━━━━━━] €1.542          │
│ min €800         max €2.100         │
│                                     │
│ Resultierendes Limit                │
│ € 385.000                           │
│                                     │
│ Effektiver Jahreszins: 3,75%        │
│                                     │
│           [Übernehmen]              │
└─────────────────────────────────────┘
```

*[Parameters update in real-time as user adjusts sliders]*

### Step 1.6: Pre-Approval Summary
**Agent:** "Perfekt! Hier ist die Zusammenfassung deines Pre-Approvals:"

*[Summary Card]*
```
┌─────────────────────────────────────┐
│ 📋 Dein Pre-Approval                │
├─────────────────────────────────────┤
│                                     │
│ Finanzierungslimit    € 385.000     │
│ Laufzeit              20 Jahre      │
│ Monatliche Rate       € 1.542       │
│ Effektiver Jahreszins 3,75%         │
│ Sollzinssatz          3,45%         │
│                                     │
│ Gültig bis            20.05.2026    │
│                                     │
└─────────────────────────────────────┘
```

**Agent:** "Dieses Limit ist 90 Tage gültig. Sobald du eine Immobilie gefunden hast, können wir die Finanzierung abschließen."

### Step 1.7: Pre-Approval Signature
**Agent:** "Wenn du auf 'Akzeptieren' tippst, wird dein Pre-Approval Limit verbindlich gesichert."

*[Action Card]*
```
┌─────────────────────────────────────┐
│                                     │
│  Mit deiner Bestätigung sicherst    │
│  du dir dieses Limit für 90 Tage.   │
│                                     │
│  Keine Verpflichtung zum Kauf.      │
│  Keine Gebühren.                    │
│                                     │
│      [    Akzeptieren    ]          │
│                                     │
└─────────────────────────────────────┘
```

**User taps "Akzeptieren"**

*[Face ID prompt animation]*
```
┌─────────────────────────────────────┐
│                                     │
│          [Face ID Icon]             │
│                                     │
│    Mit Face ID bestätigen           │
│                                     │
└─────────────────────────────────────┘
```

*[Success animation - green checkmark with subtle pulse]*
```
┌─────────────────────────────────────┐
│                                     │
│             ✓                       │
│                                     │
│    Pre-Approval gesichert!          │
│                                     │
└─────────────────────────────────────┘
```

**Agent:** "Ausgezeichnet! Dein Pre-Approval über €385.000 ist jetzt aktiv. Viel Erfolg bei der Immobiliensuche! Melde dich einfach, wenn du etwas gefunden hast."

### Step 1.8: Phase 2 Entry Point
*[After a short pause, show button for demo purposes]*

```
┌─────────────────────────────────────┐
│                                     │
│  Demo: Immobilie gefunden?          │
│                                     │
│      [ Phase 2 starten ]            │
│                                     │
└─────────────────────────────────────┘
```

*[User taps "Phase 2 starten" to continue the demo]*

---

## PHASE 2: Property Found - Finalizing Mortgage

### Step 2.1: User Returns
**User:** "Ich habe ein Haus gefunden!"

**Agent:** "Das freut mich! Dann lass uns deine Finanzierung abschließen. Dein Pre-Approval über €385.000 ist noch aktiv."

### Step 2.2: Property Documents Request
**Agent:** "Für den Abschluss benötige ich noch die Dokumente zur Immobilie:"

*[Document Checklist - Updated Journey View]*
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✓ PRE-APPROVAL                    Abgeschlossen
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   ✓ Identität verifiziert
   ✓ Einkommensnachweise
   ✓ Lohnzettel
   
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📍 FINANZIERUNG ABSCHLIESSEN      ← Du bist hier
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   ○ Kaufvertrag                    
   ○ Energieausweis                 
   ○ Grundbuchauszug                

        [ Alle Dokumente hochladen ]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

*Note: All 3 missing document items should have identical styling: empty circle with blue border and white fill (○)*

*[Single "Alle Dokumente hochladen" button at the bottom of the checklist]*

### Step 2.3: Document Upload Confirmation
User taps "Alle Dokumente hochladen" → File picker simulation → auto-success

**Agent:** "Kaufvertrag erhalten ☑️"

**Agent:** "Energieausweis erhalten ☑️"

**Agent:** "Grundbuchauszug erhalten ☑️"

*(Messages appear sequentially with short delays, ~500ms between each)*

### Step 2.4: Document Verification
**Agent:** "Prüfe Dokumente"

**Agent:** "..."

*[Show "..." for 3 seconds - animated dots pulsing]*

**Agent:** "Perfekt, ich habe alle Dokumente. Ich prüfe jetzt die Immobilie und erstelle deinen finalen Kreditvertrag..."

*[Processing animation - 3-4 seconds]*

### Step 2.5: Final Mortgage Offer
**Agent:** "Alles geprüft! Deine Finanzierung ist bereit."

*[Final Mortgage Summary Card]*
```
┌─────────────────────────────────────┐
│ 🏠 Dein Hypothekenvertrag           │
├─────────────────────────────────────┤
│                                     │
│ Immobilie                           │
│ Musterstraße 42, 1010 Wien          │
│                                     │
│ Kaufpreis           € 350.000       │
│ Finanzierungssumme  € 315.000       │
│ Eigenkapital        € 35.000        │
│                                     │
│ ─────────────────────────────────── │
│                                     │
│ Laufzeit            20 Jahre        │
│ Monatliche Rate     € 1.542         │
│ Effektiver Jahreszins 3,75%         │
│ Sollzinssatz        3,45%           │
│                                     │
│ Erste Rate          01.04.2026      │
│                                     │
└─────────────────────────────────────┘
```

### Step 2.6: Final Signature
**Agent:** "Wenn du auf 'Akzeptieren' tippst, wird dein Hypothekenvertrag verbindlich unterschrieben."

*[Action Card]*
```
┌─────────────────────────────────────┐
│                                     │
│  Mit deiner Bestätigung             │
│  unterzeichnest du den              │
│  Hypothekenvertrag über             │
│  € 315.000                          │
│                                     │
│  Der Betrag wird bei Übergabe       │
│  an den Verkäufer überwiesen.       │
│                                     │
│      [    Akzeptieren    ]          │
│                                     │
└─────────────────────────────────────┘
```

**User taps "Akzeptieren"**

*[Face ID prompt]*

*[Success animation - green checkmark, confetti effect]*
```
┌─────────────────────────────────────┐
│                                     │
│           🎉 ✓ 🎉                   │
│                                     │
│   Hypothekenvertrag unterschrieben! │
│                                     │
│   Willkommen im neuen Zuhause!      │
│                                     │
└─────────────────────────────────────┘
```

**Agent:** "Herzlichen Glückwunsch zu deinem neuen Zuhause! 🏠 Der Kaufbetrag wird zum vereinbarten Übergabetermin überwiesen. Bei Fragen bin ich jederzeit für dich da."

---

## Visual Design Notes

### Color Scheme
- Primary: George blue (#0066B3 or similar)
- Success: Green (#00A86B)
- Background: White/Light gray
- Text: Dark gray (#333)

### Typography
- Clean sans-serif (system font or custom George font)
- Large, readable text for mobile
- Numbers in financial displays slightly larger/bolder

### Animations
- Loading: Subtle pulsing dots or circular progress
- Limit reveal: Number scales up from small to large with subtle bounce
- Success: Checkmark draws in, optional confetti for final signature
- Transitions: Smooth fade/slide for new messages

### Chat Bubbles
- Agent messages: Left-aligned, light gray background
- User messages: Right-aligned, blue background, white text
- Cards/Visuals: Full-width, white background with subtle shadow

### Mobile Considerations
- Minimum tap target: 44x44px
- Thumb-friendly button placement
- Keyboard avoidance for any input fields
- Pull-to-refresh disabled (conversational flow)

---

## Prototype Screens Summary

1. **Conversation Start** - User message + agent greeting + loading
2. **Document Journey Reveal** - Journey visualization component
3. **Upload Modal** - Camera/Gallery/File options
4. **Processing** - Upload confirmation + calculation animation
5. **Limit Reveal** - Big number celebration moment
6. **Parameter Adjustment** - Sliders and options card
7. **Pre-Approval Summary** - Final details before signature
8. **Face ID Prompt** - Biometric confirmation
9. **Success Screen (Pre-Approval)** - Checkmark + confirmation
10. **Phase 2 Start** - User returns, updated journey view
11. **Property Doc Uploads** - Sequential upload flow
12. **Final Mortgage Summary** - Complete loan details
13. **Final Signature** - Acceptance + Face ID
14. **Success Screen (Final)** - Celebration + closing message

---

## Implementation Notes for Dev Agent

- Build as single-page mobile web app
- Use CSS animations for all transitions
- Hardcode all values (no backend)
- Touch interactions: tap to advance, tap buttons for actions
- Document uploads: simulate with file picker, show preview, auto-advance
- Face ID: show icon + "authenticating" animation, auto-succeed after 1.5s
- Test on iPhone Safari viewport (375px width as baseline)

---

## Interaction Model (Prototype Navigation)

Since this is a visual prototype without NLP:

### How User Advances Through Flow
1. **Auto-advance** through messages and animations - NO tapping required for normal flow
2. **Stop and wait for user input ONLY when:**
   - Upload button needs to be tapped
   - Parameter adjustment choice (Ja/Nein)
   - Slider/parameter interactions
   - Accept/signature buttons
   - Phase 2 start button
3. **Slider interactions** work normally in parameter adjustment
4. **Upload simulation**: File picker opens, any selection triggers "success" and auto-continues

### Phase Transition
- After Phase 1 success screen, show **"Phase 2 starten"** button
- User taps button to begin Phase 2 flow
- This simulates user returning later after finding a property

### State Management
- Auto-advancing flow with pauses only at interaction points
- Recommended: Linear with optional parameter card (tap "Ja" shows card, tap "Nein" skips)
- **Reset**: Pull down from top or add hidden "Reset" button in corner

### Timing Guidelines
| Animation | Duration |
|-----------|----------|
| Message appear | 300ms fade-in |
| Loading dots | Loop until next tap or 2-3s auto |
| Limit reveal number | 800ms scale + bounce |
| Success checkmark | 500ms draw-in |
| Confetti (final) | 2s burst then fade |
| Card transitions | 250ms slide-up |

---

## Document Journey Component - Detailed Spec

This is the key reusable component showing progress.

### Visual Structure
```
┌─────────────────────────────────────────────────────┐
│ ┌─────────────────────────────────────────────────┐ │
│ │ 📍 PRE-APPROVAL              ← Du bist hier    │ │ ← Section Header (highlighted when active)
│ └─────────────────────────────────────────────────┘ │
│                                                     │
│    ✓  Identität verifiziert                        │ ← Completed item (green check)
│    ✓  Einkommensnachweise (3 Monate)               │
│                                                     │
│    ○  Lohnzettel                    [Hochladen]    │ ← Pending item (empty circle + action)
│                                                     │
│ ┌─────────────────────────────────────────────────┐ │
│ │ ○ FINANZIERUNG ABSCHLIESSEN         Später     │ │ ← Future section (grayed out)
│ └─────────────────────────────────────────────────┘ │
│                                                     │
│    ○  Kaufvertrag                                  │ ← Future items (no action buttons yet)
│    ○  Energieausweis                               │
│    ○  Grundbuchauszug                              │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### States
- **Active section**: Blue/highlighted header, white background
- **Completed section**: Green header with ✓, collapsed or full
- **Future section**: Gray header, gray text, no interactions
- **Completed item**: Green ✓ icon, normal text
- **Pending item**: Empty ○ icon, action button visible
- **Future item**: Gray ○ icon, no button, lighter text

### Animations
- When item completes: ○ morphs to ✓ with 300ms animation
- When section completes: Header shifts to green, checkmark appears
- When new section activates: Scroll to section, highlight pulse

---

## Accessibility Notes

Even for prototype, good practices:
- **Color contrast**: All text meets WCAG AA (4.5:1 minimum)
- **Touch targets**: Minimum 44x44px for all interactive elements
- **Focus states**: Visible focus rings for buttons (for desktop testing)
- **Text size**: Body text minimum 16px to prevent iOS zoom

---

## Edge Cases to Visualize (Optional Enhancements)

If time permits, these could be added as alternate flows:

1. **Already has Pre-Approval**: User returns, agent recognizes existing limit
2. **Expired Pre-Approval**: "Your limit expired, let's refresh it" → quick re-check
3. **Property exceeds limit**: "This property is €50k over your limit. Options: increase limit (need more docs) or find co-borrower"

For MVP prototype: **Happy path only** as specified.

---

## Copy/Tone Guidelines

### Agent Personality
- Professional but warm
- Explains clearly without being condescending
- Celebrates wins with user ("Herzlichen Glückwunsch!")
- Uses "du" (informal) - George style
- Concise - no fluff

### Key Phrases
| Moment | Copy |
|--------|------|
| Start | "Natürlich! Ich helfe dir gerne..." |
| Checking | "Lass mich kurz prüfen..." |
| Good news | "Gute Nachrichten!" |
| Upload received | "Perfekt, ich habe deinen [X] erhalten." |
| Processing | "Ich berechne jetzt..." / "Ich prüfe jetzt..." |
| Limit reveal | "Herzlichen Glückwunsch!" |
| Pre-sign | "Wenn du auf 'Akzeptieren' tippst..." |
| Success | "Ausgezeichnet!" / "Herzlichen Glückwunsch!" |
| Final | "Willkommen im neuen Zuhause! 🏠" |

---

## Tech Stack Recommendation

For Banking Prototypes agent:
- **HTML5 + CSS3 + Vanilla JS** (consistent with other prototypes)
- **No frameworks** unless already used in other banking prototypes
- **CSS Variables** for theming (easy color adjustments)
- **LocalStorage** for state persistence (optional, for demo continuity)

---

## Priority / Effort Estimate

| Component | Priority | Effort |
|-----------|----------|--------|
| Chat bubble system | P0 | Medium |
| Document Journey component | P0 | Medium |
| Upload simulation | P0 | Low |
| Limit reveal animation | P0 | Medium |
| Parameter adjustment card | P1 | Medium |
| Face ID simulation | P0 | Low |
| Success animations | P1 | Low |
| Confetti effect | P2 | Low |

**Estimated total**: 1-2 days for full implementation
