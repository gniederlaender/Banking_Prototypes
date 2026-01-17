# George UI Design Guide

## Overview

This guide documents the design system used by George, the banking platform by Sparkasse Austria. All UI prototypes in this repository should follow these guidelines to maintain consistency with the George look and feel.

George is a modern, digital banking platform that emphasizes clarity, accessibility, and user-friendliness. The design system is characterized by bold colors, clean typography, and intuitive interactions.

---

## Table of Contents

1. [Color Palette](#color-palette)
2. [Typography](#typography)
3. [Layout & Spacing](#layout--spacing)
4. [Navigation](#navigation)
5. [Components](#components)
6. [Cards & Containers](#cards--containers)
7. [Forms & Inputs](#forms--inputs)
8. [Buttons](#buttons)
9. [Icons & Visuals](#icons--visuals)
10. [Notifications & Alerts](#notifications--alerts)
11. [Data Visualization](#data-visualization)
12. [Responsive Design](#responsive-design)
13. [Interaction Patterns](#interaction-patterns)

---

## Color Palette

### Primary Colors

**Blue (Primary Brand Color)**
- Primary Blue: `#1E5EBE` or `rgb(30, 94, 190)`
- Used for: Primary navigation bar, primary buttons, links, active states
- Gradient: Blue gradient backgrounds on header areas

**Teal/Turquoise (Secondary)**
- Teal: `#00A19C` or similar
- Used for: Account detail headers, secondary navigation states
- Provides variation from primary blue

**Magenta/Pink (Accent)**
- Magenta: `#DC004E` or `#E2007A`
- Used for: Promotional banners, call-to-action elements, important notifications
- High contrast accent color

**Green (Investment/Savings)**
- Green: `#00916E` or similar emerald green
- Used for: Investment products, savings features, positive actions
- Multiple shades used in gradient tiles

### Neutral Colors

**Backgrounds**
- Light Gray: `#F5F5F5` or `#FAFAFA` - Main background
- White: `#FFFFFF` - Card backgrounds, content areas
- Medium Gray: `#E0E0E0` - Borders, dividers

**Text Colors**
- Primary Text: `#212121` or very dark gray
- Secondary Text: `#666666` or `#757575`
- Disabled Text: `#9E9E9E`

### Semantic Colors

**Status Colors**
- Success/Positive: Green (positive account balances, confirmations)
- Error/Negative: Red `#D32F2F` (negative balances, errors, debits)
- Warning: Orange/Yellow tones
- Info: Blue tones (matching primary)

### Color Usage Guidelines

1. **Header/Navigation**: Always use primary blue with white text
2. **Account Cards**: Use colored top borders to differentiate account types
3. **Amounts**: Red for negative amounts (with minus sign), black/dark gray for positive
4. **CTAs**: Blue for primary actions, white/outlined for secondary actions
5. **Promotional Elements**: Use magenta/pink sparingly for high-impact promotions

---

## Typography

### Font Family

George uses a clean, modern sans-serif font family. For prototypes, use:
- Primary: **System fonts** or **"Segoe UI", "Roboto", "Helvetica Neue", Arial, sans-serif**
- The font should be highly legible and work well at various sizes

### Font Sizes & Hierarchy

**Headers**
- H1 (Page Titles): 28-32px, bold
- H2 (Section Headers): 20-24px, bold
- H3 (Card/Module Headers): 16-18px, semi-bold or bold

**Body Text**
- Large Body: 16px, regular
- Standard Body: 14px, regular
- Small Text: 12px, regular
- Micro Text: 10-11px (for disclaimers, labels)

**Specialized Text**
- Account Balances (Large): 24-28px, bold
- Card Amounts: 18-22px, semi-bold
- Navigation Items: 14-16px, medium

### Font Weights

- Regular: 400
- Medium: 500
- Semi-Bold: 600
- Bold: 700

### Text Styling

- **Line Height**: 1.5 for body text, 1.2-1.3 for headers
- **Letter Spacing**: Normal to slightly increased (0.01-0.02em for body)
- **Text Color**: Use high contrast - dark text on light backgrounds
- **Links**: Blue color, underline on hover

---

## Layout & Spacing

### Grid System

- Use a **responsive grid** with consistent gutters
- Main content areas typically centered with max-width constraints
- Card-based layouts with 12-16px spacing between cards

### Container Widths

- **Full Width**: Navigation, headers, promotional banners
- **Content Container**: Max-width 1200-1400px, centered
- **Card Grids**: Responsive columns (1, 2, 3, or 4 columns based on viewport)

### Spacing Scale

Use a consistent spacing scale based on 4px or 8px increments:

- **4px**: Tight spacing (inline elements, icon-text gaps)
- **8px**: Small spacing (within cards, form field spacing)
- **16px**: Standard spacing (between sections, card padding)
- **24px**: Medium spacing (section gaps)
- **32px**: Large spacing (major section separators)
- **48px+**: Extra large spacing (header padding, hero sections)

### Padding Guidelines

- **Cards**: 16-24px padding
- **Buttons**: 12px vertical, 24px horizontal
- **Form Inputs**: 12px vertical, 16px horizontal
- **Page Margins**: 16px on mobile, 24-32px on desktop

---

## Navigation

### Top Navigation Bar

**Structure:**
- Fixed to top of viewport
- Full-width with primary blue background
- Height: 60-72px
- Contains: Logo (left), navigation items (center-left), user controls (right)

**Logo:**
- George logo with "g" symbol in white
- Positioned left, with link to home/overview
- Size: approximately 40-48px height

**Navigation Items:**
- Horizontal menu items in white text
- Items include: "Übersicht" (Overview), "Ihre Produkte" (Your Products), "Ihre Zusatzfunktionen" (Additional Functions), "Discover", "Kontakt" (Contact)
- Notification badges (red circles with counts) can appear on menu items
- Active state: pill-shaped background highlight (darker blue or semi-transparent white)
- Dropdown indicators (chevron down) for expandable menus

**User Controls (Right Side):**
- User profile icon (circular, white)
- Settings/preferences icon
- Logout button with power icon
- All icons in white

**Interaction:**
- Hover states: Slight opacity change or background highlight
- Dropdowns expand below navigation bar
- Sticky/fixed positioning while scrolling

### Side Navigation (Account Details)

On account detail pages, a left sidebar navigation appears with:
- Account information at top (name, number, balance)
- Vertical menu items (Kontohistorie, Neue Überweisung, Spenden, Karten, etc.)
- Selected item highlighted with blue text or background
- Expandable sections where needed

---

## Components

### 1. Greeting/Welcome Section

- Located below header, spans full width
- Blue gradient background
- Large, friendly greeting text in white: "Angenehmen Nachmittag, [Name]" (time-based)
- Notification cards with icons (semi-transparent white cards)
- Examples: "Sie haben Post" (You have mail), "Es wartet ein offener Auftrag" (Pending task)

### 2. Search Bar

**Appearance:**
- Large, prominent search field below greeting section
- White background with subtle shadow
- Placeholder: "Sie suchen, ich finde." (You search, I find.)
- Search icon button on right (blue background)
- Additional filter/sort options: "Betrag" (Amount), "Datum" (Date)
- View toggle buttons (grid/list view)
- "Personalisieren" (Personalize) option

**Behavior:**
- Expands on focus
- Auto-suggest/autocomplete functionality
- Real-time filtering

### 3. Promotional Banners

**Style:**
- Full-width colored backgrounds (typically magenta/pink)
- Icon on left (white)
- Text message in white
- CTA button on right (white outline or filled)
- Close button (X) on far right
- Example: "Investieren durch Aufrunden" banner

**Usage:**
- Promote features, products, or special offers
- Dismissible
- Should not be overused (max 1-2 visible at once)

### 4. Spotlights Section

**Purpose:** Highlight key financial categories or quick-access items

**Layout:**
- Grid of cards (typically 4 columns on desktop)
- Category name as header
- Large amount display with currency
- Icon representing category (colored, themed)
- Optional: Small chart or graph
- Link to detail view or action

**Card Styling:**
- White background
- Rounded corners (8px)
- Subtle shadow on hover
- Colored accent (icon or top border)
- Categories: "Ausgaben im Jänner" (Expenses), "Kfz" (Car), "Wohnen" (Housing), "Lebensmittel" (Groceries)

### 5. Account Cards

**Design:**
- White card with colored top border (2-4px)
- Account name and holder
- Account number (if applicable)
- Balance (large, prominent)
- Available amount (smaller, gray text)
- Payment method icon (Visa, Mastercard, bank icon)
- Optional: Mini chart/graph showing trend
- Action buttons at bottom ("Neue Überweisung", "Erhöhen", more options)

**Color Coding:**
- Different border colors for different account types
- Teal for checking accounts
- Pink/Magenta for credit cards
- Yellow/Gold for investment accounts
- Navy for other credit products

**Hover State:**
- Slight elevation (increased shadow)
- Cursor pointer

---

## Cards & Containers

### Card Anatomy

**Standard Card:**
```
- Border-radius: 8-12px
- Background: white (#FFFFFF)
- Shadow: 0 2px 4px rgba(0,0,0,0.1)
- Padding: 16-24px
- Margin: 12-16px between cards
```

**Card Variations:**
1. **Info Card**: Icon + title + description
2. **Account Card**: Detailed account information (see above)
3. **Transaction Card**: Date, merchant, category icon, amount
4. **Product Card**: Image, title, description, CTA button

### Visual Hierarchy in Cards

- Top border or icon for category identification
- Title/header at top
- Primary content in center
- Actions/buttons at bottom
- Use dividers (1px, light gray) for content separation

---

## Forms & Inputs

### Input Fields

**Text Inputs:**
- Border: 1px solid light gray (#E0E0E0)
- Border-radius: 4px
- Padding: 12px 16px
- Font-size: 14-16px
- Focus state: Blue border, slight shadow
- Error state: Red border, error message below
- Disabled state: Gray background, lighter text

**With Labels:**
- Label above input (12-14px, semi-bold or medium weight)
- Required fields marked with asterisk or "(erforderlich)"
- Optional help text below in smaller gray font

**Dropdowns/Select:**
- Similar styling to text inputs
- Chevron down icon on right
- Dropdown menu with white background, shadow
- Hover state on options
- Selected option highlighted

**Number Inputs:**
- Currency symbol (€) positioned appropriately
- Right-aligned for amounts
- Formatted with thousands separators (space or comma)
- Decimal precision (2 places for currency)

### Sliders

**Range Sliders:**
- Track: Light gray background
- Filled track: Blue
- Handle: Circular, blue, with shadow
- Labels below showing min/max values
- Current value displayed above handle or in separate field

**Usage:** Loan calculator, budget settings

### Checkboxes & Radio Buttons

**Checkboxes:**
- Square, 18-20px
- Border: gray
- Checked: blue background with white checkmark
- Label to the right

**Radio Buttons:**
- Circular, 18-20px
- Border: gray
- Selected: blue filled center
- Label to the right

### Information Boxes

**Info Box:**
- Light blue background (#E3F2FD or similar)
- Blue border (left or all around)
- Info icon (blue)
- Text in dark gray
- Used for helpful hints, important information

**Example from loan form:** Data collection notice with bullet points

---

## Buttons

### Button Hierarchy

**1. Primary Button**
- Background: Blue (#1E5EBE)
- Text: White, 14-16px, medium/semi-bold
- Padding: 12px 24px
- Border-radius: 4-6px
- Shadow: Subtle (0 2px 4px rgba(0,0,0,0.15))
- Hover: Darker blue, increased shadow
- Active: Even darker, slight scale down
- Examples: "Weiter" (Continue), "Zur Funktion" (To Function)

**2. Secondary Button**
- Background: White or transparent
- Border: 1px solid blue
- Text: Blue, 14-16px, medium
- Padding: 12px 24px
- Border-radius: 4-6px
- Hover: Light blue background
- Examples: "Später fortfahren" (Continue later), "Berechnung drucken" (Print calculation)

**3. Tertiary/Text Button**
- No background
- No border
- Text: Blue, 14-16px, medium
- Underline on hover
- Examples: "Bearbeiten" (Edit), "Ausklappen" (Expand)

**4. Icon Button**
- Circular or square
- Icon only (no text)
- Examples: Search button, filter button, more options (•••)

**5. Outlined Button (White)**
- White background with white border (for colored backgrounds)
- Example: "Zur Funktion" on magenta banner

### Button States

- **Default**: Base styling
- **Hover**: Color change, shadow increase
- **Active/Pressed**: Darker color, slight transform
- **Disabled**: Gray background, gray text, no hover effect, cursor not-allowed
- **Loading**: Spinner icon, disabled interaction

### Button Groups

When multiple buttons are together:
- Primary action on the right
- Secondary/cancel on the left
- Spacing: 8-12px between buttons
- Align horizontally (side by side) on desktop
- Stack vertically on mobile

**Example:** "Später fortfahren" | "Betreuer:in kontaktieren" | "Weiter"

---

## Icons & Visuals

### Icon Style

- **Line icons** or **simple filled icons**
- Consistent stroke width (2px typically)
- Size: 20-24px for inline, 32-48px for featured icons
- Color: Match context (white on blue header, blue for actions, category colors for accounts)

### Common Icons

- **Navigation**: Home, Products, Functions, Discover, Contact
- **Actions**: Search, Filter, Print, Edit (pencil), More (•••)
- **Status**: Notification bell, mail/envelope, warning, info (i), checkmark
- **Financial**: Piggy bank (savings), chart/graph, card, transfer arrows
- **User**: Profile circle, logout/power, settings/gear

### Category Icons

- **Kfz (Car)**: Car icon in pink/red
- **Wohnen (Housing)**: House icon in purple
- **Lebensmittel (Groceries)**: Shopping bag/cart in green
- **Ausgaben (Expenses)**: Chart icon in blue

### Account/Payment Icons

- Visa logo
- Mastercard logo
- Bank/institution logo
- Maestro logo

### Illustrations

- Modern, minimal illustrations for promotional content
- Photographs for product marketing (s Gold Plan, Wertpapier-Depot)
- Real people in lifestyle settings
- Warm, approachable tone

---

## Notifications & Alerts

### Notification Cards (Dashboard)

- Semi-transparent white background on blue gradient
- Icon on left (message, document, etc.)
- Text message in white
- Clickable entire card

### Notification Badges

- Small red circle with white count number
- Position: Top-right of navigation items or icons
- Example: "99+" on "Kontakt" menu item

### Toast/Snackbar Notifications

- Appear at top or bottom of screen
- Background: Dark gray or color-coded (green for success, red for error)
- Text: White
- Dismiss button (X) or auto-dismiss
- Duration: 3-5 seconds for auto-dismiss

### Alert Banners

- Full-width colored bar
- Icon + message + action button
- Dismissible with X button
- Examples: Promotional banner (magenta), info banner (blue), warning (yellow/orange)

---

## Data Visualization

### Charts & Graphs

**Bar Charts:**
- Vertical bars
- Colored bars (green for positive/income, red for negative/expenses)
- X-axis: Time periods (Aug, Sep, Okt, Nov, Dez, Jän)
- Y-axis: Implied by bar height (no explicit axis shown in minimal views)
- Minimal grid lines or no grid
- Bars with slight spacing

**Line Charts:**
- Smooth curves
- Blue line typically
- Filled area below line (gradient from blue to transparent)
- Points on line for data values
- Clean, minimal design

**Usage:**
- Account balance trends (6-month view)
- Spending by category
- Investment performance

### Progress Indicators

**Linear Progress Bar:**
- Track: Light gray background
- Fill: Blue (or red for usage warnings)
- Height: 4-8px
- Rounded ends
- Percentage or amount labels

**Example:** Credit card usage (€ 584,67 verfügbar / € 7.000,00 Limit)

---

## Responsive Design

### Breakpoints

- **Mobile**: < 600px
- **Tablet**: 600px - 1024px
- **Desktop**: > 1024px

### Responsive Behavior

**Navigation:**
- Desktop: Full horizontal menu
- Tablet/Mobile: Hamburger menu, drawer navigation

**Card Grids:**
- Desktop: 4 columns (Spotlights), 2-3 columns (Account cards)
- Tablet: 2-3 columns
- Mobile: 1 column, full-width cards

**Search & Filters:**
- Desktop: Inline, horizontal layout
- Mobile: Stacked, may collapse into filter drawer

**Buttons:**
- Desktop: Side-by-side
- Mobile: Stacked vertically, full-width

**Typography:**
- Scale down heading sizes on mobile (H1: 24px instead of 32px)
- Maintain readability (min 14px for body text)

### Touch Targets

- Minimum 44x44px for all interactive elements on mobile
- Adequate spacing between clickable items
- Larger buttons on mobile for easier interaction

---

## Interaction Patterns

### Hover States

- **Cards**: Elevation increase (shadow depth), slight scale (1.02)
- **Buttons**: Background color darkening, shadow increase
- **Links**: Underline, color change
- **Navigation Items**: Background highlight (pill shape)

### Active/Focus States

- **Inputs**: Blue border, box-shadow glow
- **Buttons**: Darker color, slight scale down (0.98)
- **Navigation**: Persistent background highlight for current page

### Transitions

- Use smooth transitions (200-300ms)
- Ease-in-out timing function
- Apply to: color, background, shadow, transform
- Avoid jarring animations

### Loading States

- **Skeleton screens**: Gray placeholder shapes while content loads
- **Spinners**: Circular blue spinner for button/action loading
- **Progressive loading**: Load critical content first, defer images

### Expandable Sections

- **Accordion style**: Click header to expand/collapse
- **Chevron icon**: Rotates down when expanded, up when collapsed
- **Animation**: Smooth expand/collapse (300-400ms)
- **Example**: "Ausklappen" (Expand) in Spotlights section

### Modals/Dialogs

- **Overlay**: Semi-transparent dark background (rgba(0,0,0,0.5))
- **Modal**: White card, centered, max-width 600px
- **Header**: Title, close button (X)
- **Content**: Scrollable if needed
- **Actions**: Buttons at bottom (primary on right)

### Feedback

- **Success**: Green checkmark, confirmation message
- **Error**: Red text, icon, clear error description
- **Validation**: Real-time or on-blur for forms
- **Progress**: Step indicators for multi-step flows (e.g., "Schritt 1 von 4")

---

## Specific Examples from Screenshots

### Loan Application Process (Klick-Kredit)

**Page Structure:**
1. **Header**: Blue bar with "Klick-Kredit" title, back button ("< Zurück"), logout button
2. **Step Indicator**: "Schritt 1 von 4" (Step 1 of 4) centered below header
3. **Content Card**: White card with all form content
4. **Section Headers**: Navy blue text, semi-bold, larger font
5. **Sliders**: Dual sliders for loan amount and duration
6. **Calculation Display**: Large amount (737,40 €) prominently displayed
7. **Details Table**: Two-column layout with labels and values
8. **Info Text**: Smaller gray text for disclaimers and explanations
9. **Buttons**: "Berechnung drucken" (Print, secondary) and "Weiter" (Continue, primary)

**Form Sections:**
- "Ihre Wohnsituation" (Your housing situation)
- "Ihre Arbeitssituation" (Your employment situation)
- "Familien- und Finanzdaten" (Family and financial data)
- "Rechtliche Angaben" (Legal information)

**Input Patterns:**
- Dropdowns for selection (nationality, occupation, etc.)
- Number inputs with € symbol for financial amounts
- Checkboxes for legal confirmations (with detailed text)
- Info tooltips (ⓘ icon) next to certain fields

**Multi-Step Navigation:**
- "Später fortfahren" (Continue later)
- "Betreuer:in kontaktieren" (Contact advisor)
- "Weiter" (Continue to next step)

### Account/Transaction View (Kontohistorie)

**Header:**
- Teal/turquoise background
- White text: "Kontohistorie" (Account History)
- "Neue Überweisung" (New Transfer) button on right

**Sidebar:**
- Account information card at top (balance, account number)
- Vertical navigation menu
- Selected item highlighted

**Main Content:**
- Search bar: "Nach Transaktionen auf diesem Konto suchen"
- Filter button
- "Betrag" and "Datum" sort options
- Export options (print, download icons)

**Transaction Items:**
- Grouped by time period ("1 offener Auftrag", "3 vorgemerkte Kartenzahlungen", "Jänner 2026")
- Each transaction: Date, merchant name, category icon, amount
- Expandable details (arrow icon)
- "Freigaben" (Release) button for pending transactions
- Color-coded icons (yellow for bills, blue for bank transactions, green for specific categories)

**Transaction Categories:**
- Visual icons with background colors
- Examples: Yellow circle (Billa), Blue circle (Bank), Green circle (Spar)

---

## Best Practices Summary

### Do's

1. **Use the blue-teal-magenta color scheme** consistently
2. **Implement card-based layouts** for content organization
3. **Ensure high contrast** for text readability
4. **Provide clear visual hierarchy** with font sizes and weights
5. **Use consistent spacing** (8px/16px/24px increments)
6. **Include hover and focus states** for all interactive elements
7. **Show loading and error states** for all async actions
8. **Use icons** to enhance understanding and visual appeal
9. **Implement responsive design** from mobile-first
10. **Provide clear feedback** for user actions

### Don'ts

1. **Don't use colors inconsistently** - stick to the defined palette
2. **Don't overcrowd the interface** - use whitespace generously
3. **Don't use low contrast** text (ensure WCAG AA compliance minimum)
4. **Don't forget mobile optimization** - test on various screen sizes
5. **Don't overuse animations** - keep them subtle and purposeful
6. **Don't hide important actions** - make CTAs visible and accessible
7. **Don't use inconsistent button styles** - follow the hierarchy
8. **Don't neglect accessibility** - include ARIA labels, keyboard navigation

---

## Accessibility Guidelines

1. **Color Contrast**: Maintain 4.5:1 ratio for normal text, 3:1 for large text
2. **Keyboard Navigation**: All interactive elements should be keyboard accessible
3. **Focus Indicators**: Visible focus states (blue outline, glow)
4. **Alt Text**: Provide for all images and icons
5. **ARIA Labels**: Use for icon-only buttons and complex widgets
6. **Semantic HTML**: Use proper heading hierarchy, landmarks
7. **Form Labels**: Associate labels with inputs explicitly
8. **Error Messages**: Clear, specific, programmatically associated with fields

---

## Code Snippets

### Example: Primary Button CSS

```css
.btn-primary {
    background-color: #1E5EBE;
    color: #FFFFFF;
    border: none;
    border-radius: 4px;
    padding: 12px 24px;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.15);
    transition: all 0.2s ease-in-out;
}

.btn-primary:hover {
    background-color: #174A99;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.btn-primary:active {
    background-color: #0F3A7A;
    transform: scale(0.98);
}

.btn-primary:disabled {
    background-color: #9E9E9E;
    cursor: not-allowed;
    box-shadow: none;
}
```

### Example: Card Component CSS

```css
.card {
    background-color: #FFFFFF;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    padding: 24px;
    margin-bottom: 16px;
    transition: box-shadow 0.2s ease-in-out, transform 0.2s ease-in-out;
}

.card:hover {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    transform: translateY(-2px);
}

.card.account-card {
    border-top: 4px solid #00A19C; /* Teal for checking account */
}

.card.account-card.credit-card {
    border-top-color: #DC004E; /* Magenta for credit cards */
}
```

### Example: Navigation Bar HTML

```html
<nav class="top-nav">
    <div class="nav-container">
        <div class="nav-logo">
            <a href="#"><img src="george-logo.svg" alt="George"></a>
        </div>
        <ul class="nav-menu">
            <li class="nav-item active"><a href="#">Übersicht</a></li>
            <li class="nav-item">
                <a href="#">
                    Ihre Produkte
                    <span class="notification-badge">1</span>
                </a>
            </li>
            <li class="nav-item"><a href="#">Ihre Zusatzfunktionen</a></li>
            <li class="nav-item"><a href="#">Discover</a></li>
            <li class="nav-item">
                <a href="#">
                    Kontakt
                    <span class="notification-badge">99+</span>
                </a>
            </li>
        </ul>
        <div class="nav-user">
            <button class="user-profile-btn">
                <img src="user-icon.svg" alt="Profile">
            </button>
            <button class="logout-btn">
                <span>Logout</span>
            </button>
        </div>
    </div>
</nav>
```

---

## Additional Resources

### Typography Resources
- Use web-safe sans-serif fonts for maximum compatibility
- Consider loading custom fonts for exact brand matching (if licensed)

### Icon Libraries
- Font Awesome (for general icons)
- Material Design Icons
- Custom SVG icons for brand-specific elements

### Color Tools
- Use color contrast checkers (e.g., WebAIM Contrast Checker)
- Create color palettes with tools like Coolors or Adobe Color

### Testing
- Test on multiple browsers (Chrome, Firefox, Safari, Edge)
- Test on various devices (iOS, Android, desktop)
- Use browser dev tools for responsive testing
- Validate accessibility with tools like WAVE or Axe

---

## Version History

- **v1.0** (2026-01-17): Initial documentation based on George screenshots analysis

---

## Contact & Contributions

For questions or suggestions regarding this UI guide, please contact the development team or submit feedback through the project repository.

---

**Remember:** The goal is to create a consistent, user-friendly experience that aligns with the George brand while maintaining accessibility and usability standards. When in doubt, refer to the screenshots and prioritize clarity and user needs.
