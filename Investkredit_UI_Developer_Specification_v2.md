# Investitionskredit UI/UX Developer Specification
## George Business Banking Prototype - Technical Implementation Guide
**Date:** January 17, 2026
**Version:** 2.0 (Chrome Extension Analysis)

---

# Phase 1: Quick Wins
**Estimated Effort:** 1-2 Sprints | **Priority:** CRITICAL

These items can be implemented with minimal code changes and provide immediate UX improvements.

---

## 1.1 Pre-Qualification Button State Communication

**Current Issue:** Users don't know they must click "Vorqualifizierung prufen" before proceeding.

**Specification:**
```
Location: Step 1 (Pre-Check)
Component: Button group at bottom of form

Requirements:
1. "Weiter zum Antrag" button should be:
   - Visually disabled (opacity: 0.5, cursor: not-allowed)
   - Show tooltip on hover: "Bitte zuerst Vorqualifizierung prufen"

2. After successful pre-qualification:
   - Enable button with animation (fade-in, color change)
   - Add checkmark icon to "Vorqualifizierung prufen" button
   - Optional: Auto-scroll to success message

CSS Changes:
.btn-weiter-disabled {
  opacity: 0.5;
  pointer-events: none;
  position: relative;
}
.btn-weiter-disabled::after {
  content: "Bitte zuerst Vorqualifizierung prufen";
  /* tooltip styling */
}
```

---

## 1.2 Required Field Legend

**Current Issue:** Asterisks (*) used without explanation.

**Specification:**
```
Location: All form steps (Steps 1-7)
Position: Top of each form section

Implementation:
<div class="form-legend">
  <span class="required-indicator">*</span> Pflichtfeld
</div>

Styling:
- Font size: 12px
- Color: #6c757d (muted)
- Margin-bottom: 16px
- Position: Below section heading, above first field
```

---

## 1.3 Progress Auto-Save

**Current Issue:** No save functionality; users lose progress on page close.

**Specification:**
```
Trigger: On every field blur event + 30-second interval
Storage: localStorage (for prototype) / Backend API (production)

Implementation:
1. Create FormStatePersistence service
2. On field change: debounce 2 seconds, then save
3. On page load: check for saved state, prompt restoration
4. Show discrete "Gespeichert" indicator (toast, 2 seconds)

Data Structure:
{
  "applicationId": "uuid",
  "currentStep": 3,
  "lastSaved": "2026-01-17T10:30:00Z",
  "formData": {
    "step1": {...},
    "step2": {...}
  }
}

UI Element:
<div class="auto-save-indicator">
  <span class="icon-check"></span> Automatisch gespeichert
</div>
```

---

## 1.4 Step Completion Indicators

**Current Issue:** Completed steps show yellow but no explicit checkmark.

**Specification:**
```
Location: Progress stepper (all pages)

Visual Updates:
1. Completed steps: Add white checkmark inside yellow circle
2. Current step: Blue circle with step number
3. Future steps: Gray outline with step number

HTML Structure:
<div class="step completed">
  <span class="step-circle">
    <svg class="checkmark">...</svg>
  </span>
  <span class="step-label">Pre-Check</span>
</div>

Animation:
- Checkmark draws in (0.3s ease-out) when step completes
```

---

## 1.5 Button Loading States

**Current Issue:** No feedback when clicking action buttons.

**Specification:**
```
Affected Buttons:
- "Vorqualifizierung prufen"
- "Prufung starten"
- "Antrag abschliessen & signieren"

Implementation:
1. On click:
   - Disable button
   - Replace text with spinner + "Wird verarbeitet..."
   - Prevent double-clicks

2. On success:
   - Show checkmark briefly (1s)
   - Proceed to next action

Component:
<button class="btn-primary" [loading]="isLoading">
  <span *ngIf="!isLoading">Vorqualifizierung prufen</span>
  <span *ngIf="isLoading">
    <spinner></spinner> Wird gepruft...
  </span>
</button>
```

---

# Phase 2: Must-Improve Features
**Estimated Effort:** 3-4 Sprints | **Priority:** HIGH

Core functionality improvements that significantly impact usability and conversion.

---

## 2.1 Inline Form Validation

**Current Issue:** No real-time validation feedback.

**Specification:**
```
Validation Rules by Field:

Step 1 - Pre-Check:
| Field | Rule | Error Message |
|-------|------|---------------|
| Kreditbetrag | min: 10000, max: 5000000 | "Betrag muss zwischen EUR 10.000 und EUR 5.000.000 liegen" |
| Laufzeit | required | "Bitte Laufzeit auswahlen" |
| Kundentyp | required | "Bitte Kundentyp auswahlen" |

Step 2 - Antrag:
| Field | Rule | Error Message |
|-------|------|---------------|
| UID-Nummer | pattern: /^ATU\d{8}$/ | "Format: ATU12345678" |
| Firmenbuchnummer | pattern: /^FN \d+[a-z]$/ | "Format: FN 123456a" |
| Umsatz | min: 0 | "Bitte gultigen Umsatz eingeben" |

Visual Feedback:
- Valid: Green border (#28a745), checkmark icon
- Invalid: Red border (#dc3545), error text below field
- Pending: Default border

Implementation:
<div class="form-group" [class.is-valid]="field.valid" [class.is-invalid]="field.invalid">
  <input [formControl]="field">
  <div class="invalid-feedback">{{field.errors | errorMessage}}</div>
</div>
```

---

## 2.2 Document Upload Enhancement

**Current Issue:** Basic upload areas without proper feedback.

**Specification:**
```
Location: Step 4 (Dokumente)

Enhanced Features:
1. Drag & Drop:
   - Visual highlight on drag-over (dashed border, background color)
   - Drop zone text: "Datei hier ablegen"

2. File Restrictions Display:
   <div class="upload-restrictions">
     Erlaubte Formate: PDF, JPG, PNG | Max. 10 MB
   </div>

3. Upload Progress:
   - Progress bar during upload
   - File name display after upload
   - Delete/replace option

4. Multi-file Support:
   - Allow multiple files per category
   - Show file list with individual delete options

Component Structure:
<upload-zone
  [accept]="'.pdf,.jpg,.png'"
  [maxSize]="10485760"
  [multiple]="true"
  (fileSelected)="onUpload($event)">
  <upload-icon></upload-icon>
  <p>Klicken oder Datei hierher ziehen</p>
  <small>PDF, JPG, PNG - Max. 10 MB</small>
</upload-zone>

<file-list [files]="uploadedFiles">
  <file-item *ngFor="let file of files">
    {{file.name}} ({{file.size | fileSize}})
    <button (click)="remove(file)">Entfernen</button>
  </file-item>
</file-list>
```

---

## 2.3 Collateral Section Restructure (Step 5)

**Current Issue:** 6 radio options in flat list; conditional fields not well organized.

**Specification:**
```
Redesign Approach:
1. Use card-based selection instead of radio list
2. Show/hide detail forms based on selection
3. Add icons for each collateral type

Layout:
<div class="collateral-grid">
  <collateral-card
    *ngFor="let type of collateralTypes"
    [icon]="type.icon"
    [label]="type.label"
    [selected]="selectedType === type.id"
    (select)="selectCollateral(type.id)">
  </collateral-card>
</div>

<div class="collateral-details" *ngIf="selectedType">
  <ng-container [ngSwitch]="selectedType">
    <liegenschaft-form *ngSwitchCase="'liegenschaft'"></liegenschaft-form>
    <fahrzeug-form *ngSwitchCase="'fahrzeug'"></fahrzeug-form>
    <!-- etc -->
  </ng-container>
</div>

Card Styling:
- Grid: 3 columns desktop, 2 tablet, 1 mobile
- Card size: 120x100px
- Selected state: Blue border, light blue background
- Icon: 32px, centered
```

---

## 2.4 Mobile Responsive Layout

**Current Issue:** Desktop-only layout.

**Specification:**
```
Breakpoints:
- Desktop: > 992px (current layout)
- Tablet: 768px - 991px
- Mobile: < 768px

Key Changes:

1. Progress Stepper (Mobile):
   - Horizontal scroll with current step centered
   - Or: Show only current + adjacent steps
   - Step labels below numbers (truncated)

2. Form Layout (Mobile):
   - Single column
   - Full-width inputs
   - Stacked label/input (not side-by-side)

3. Button Group (Mobile):
   - Stack vertically
   - Primary action on top
   - Full width

4. Upload Zones (Mobile):
   - Larger touch targets (min 48px height)
   - Simplified text

CSS Framework Additions:
@media (max-width: 767px) {
  .form-row { flex-direction: column; }
  .btn-group { flex-direction: column; gap: 8px; }
  .stepper { overflow-x: auto; }
}
```

---

## 2.5 Consent Checkboxes Enhancement (Step 3)

**Current Issue:** Plain checkboxes without expandable detail.

**Specification:**
```
Location: KYC/AML step - Einwilligungen section

Enhancement:
1. Add expandable text for each consent
2. Link to full legal documents
3. Visual feedback on selection

Component:
<consent-item
  [label]="'Ich stimme der Datenverarbeitung gemass DSGVO zu'"
  [expandedText]="gdprFullText"
  [documentLink]="'/legal/dsgvo.pdf'"
  [(checked)]="consents.gdpr">
</consent-item>

Interaction:
- Checkbox on left
- Label clickable (toggles checkbox)
- "Mehr erfahren" link expands detail text
- Document icon links to PDF
```

---

# Phase 3: All Other Features
**Estimated Effort:** 5-6 Sprints | **Priority:** MEDIUM

Advanced features for enhanced user experience and operational efficiency.

---

## 3.1 Clickable Step Navigation

**Specification:**
```
Behavior:
- Completed steps: Clickable, navigate back
- Current step: Active, not clickable
- Future steps: Disabled, show tooltip "Bitte vorherige Schritte abschliessen"

Implementation:
- Add click handlers to step circles
- Validate data before allowing backward navigation
- Confirm if user has unsaved changes

<step-indicator
  *ngFor="let step of steps; let i = index"
  [number]="i + 1"
  [label]="step.label"
  [status]="step.status"
  [clickable]="step.status === 'completed'"
  (click)="navigateToStep(i)">
</step-indicator>
```

---

## 3.2 Smart Document Recognition

**Specification:**
```
Feature: Auto-detect uploaded document type

Implementation:
1. On file upload, analyze first page
2. Match against known document patterns:
   - Jahresabschluss: Contains "Bilanz", "GuV"
   - Firmenbuchauszug: Contains "Firmenbuch", official stamps
   - Grundbuchauszug: Contains "Grundbuch", parcel numbers

3. Suggest categorization to user
4. Auto-fill metadata where possible

API:
POST /api/documents/analyze
{
  "file": "base64...",
  "expectedTypes": ["jahresabschluss", "firmenbuch"]
}

Response:
{
  "detectedType": "jahresabschluss",
  "confidence": 0.92,
  "extractedData": {
    "year": "2024",
    "companyName": "..."
  }
}
```

---

## 3.3 Application Dashboard

**Specification:**
```
Location: New section accessible from George Business main menu

Features:
1. List of in-progress applications
2. Status tracking with timeline
3. Required actions highlighted
4. Document request management

Components:
<application-list>
  <application-card *ngFor="let app of applications">
    <status-badge [status]="app.status"></status-badge>
    <h3>{{app.productName}}</h3>
    <p>Beantragt: {{app.createdDate | date}}</p>
    <p>Betrag: {{app.amount | currency:'EUR'}}</p>
    <action-items [items]="app.pendingActions"></action-items>
    <button (click)="continue(app)">Fortsetzen</button>
  </application-card>
</application-list>
```

---

## 3.4 Multi-Language Support

**Specification:**
```
Languages:
- German (de-AT) - Default
- English (en)

Implementation:
1. Extract all UI strings to i18n files
2. Add language selector in header
3. Store preference in user profile

File Structure:
/i18n/
  de-AT.json
  en.json

Usage:
<h2>{{ 'steps.precheck.title' | translate }}</h2>

Key Translations:
{
  "steps": {
    "precheck": {
      "title": "Pre-Check & Vorqualifizierung",
      "goal": "Ziel: Fruhzeitige \"No-Touch\"-Filterung..."
    }
  }
}
```

---

## 3.5 Analytics Integration

**Specification:**
```
Events to Track:

Step Progression:
- step_started: {step_number, step_name, timestamp}
- step_completed: {step_number, duration_seconds}
- step_abandoned: {step_number, last_field_touched}

Form Interactions:
- field_focused: {field_name, step}
- field_error: {field_name, error_type}
- validation_failed: {step, fields[]}

Document Upload:
- upload_started: {document_type}
- upload_completed: {document_type, file_size, duration}
- upload_failed: {document_type, error}

Implementation:
analyticsService.track('step_completed', {
  step_number: 3,
  step_name: 'KYC/AML',
  duration_seconds: 245
});
```

---

## 3.6 Accessibility Improvements (WCAG 2.1 AA)

**Specification:**
```
Requirements:

1. Keyboard Navigation:
   - All interactive elements focusable
   - Visible focus indicators
   - Skip links for main content

2. Screen Reader:
   - ARIA labels on all form fields
   - Live regions for status updates
   - Meaningful link text

3. Color Contrast:
   - Minimum 4.5:1 for text
   - 3:1 for large text and UI components

4. Form Labels:
   - Always visible labels (no placeholder-only)
   - Error messages linked via aria-describedby

Example:
<label for="kreditbetrag" id="kreditbetrag-label">
  Kreditbetrag (EUR) <span class="required">*</span>
</label>
<input
  id="kreditbetrag"
  aria-labelledby="kreditbetrag-label"
  aria-describedby="kreditbetrag-error"
  aria-required="true"
  aria-invalid="false">
<div id="kreditbetrag-error" role="alert" class="error-message">
  <!-- Error text appears here -->
</div>
```

---

# Technical Debt & Recommendations

## Code Quality
- Implement component library for consistent UI elements
- Create form validation service for reusable rules
- Add unit tests for all validation logic
- Document API contracts for backend integration

## Performance
- Lazy load step components
- Optimize document upload with chunked transfer
- Cache form state in IndexedDB for offline support
- Implement virtual scrolling for long document lists

## Security
- Sanitize all user inputs
- Implement CSRF protection on form submissions
- Encrypt sensitive data in localStorage
- Add rate limiting on validation endpoints

---

*Document generated from live prototype analysis via Chrome extension browser automation.*
