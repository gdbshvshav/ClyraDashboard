# Clyra Bot Dashboard Design Guidelines

## Design Approach
**System-Based Approach** inspired by Discord's visual language combined with Linear's dashboard clarity and Material Design's form patterns. This creates familiarity for Discord users while maintaining professional dashboard functionality.

## Core Design Principles
1. **Clarity Over Decoration**: Clean, scannable interfaces for quick server management
2. **Progressive Disclosure**: Show complexity only when needed (module configs, advanced settings)
3. **Visual Hierarchy**: Clear distinction between primary actions, secondary info, and metadata
4. **Trust Signals**: Premium badges, status indicators, and configuration states always visible

---

## Typography System

### Font Families
- **Primary**: Inter (400, 500, 600, 700) - all body text, UI elements, forms
- **Display**: Space Grotesk (600, 700) - page headers, bot name, hero section only

### Type Scale
- **Hero Heading**: 3.5rem / 56px (Space Grotesk Bold)
- **Page Titles**: 2rem / 32px (Space Grotesk Semibold)
- **Section Headers**: 1.5rem / 24px (Inter Semibold)
- **Card Titles**: 1.125rem / 18px (Inter Semibold)
- **Body Text**: 0.875rem / 14px (Inter Regular)
- **Small Text/Labels**: 0.75rem / 12px (Inter Medium)
- **Buttons**: 0.875rem / 14px (Inter Semibold)

---

## Layout System

### Spacing Primitives
Use Tailwind units: **2, 4, 6, 8, 12, 16, 24** for consistent rhythm
- Component padding: p-6 or p-8
- Section spacing: py-16 or py-24
- Card gaps: gap-4 or gap-6
- Button padding: px-6 py-3

### Grid Structure
- **Container**: max-w-7xl with px-6 on mobile, px-8 on desktop
- **Dashboard Grid**: 3-column grid on desktop (grid-cols-1 md:grid-cols-2 lg:grid-cols-3)
- **Form Layout**: 2-column on desktop (grid-cols-1 md:grid-cols-2) for side-by-side inputs
- **Server Cards**: 4 columns max on large screens, responsive down to 1 column

---

## Component Library

### Navigation Header
- Fixed top navigation (sticky top-0)
- Height: h-16
- Logo + "Clyra" text on left
- Navigation items centered (Home, Dashboard, Documentation)
- User profile/login on right
- Border bottom with subtle separator

### Home Page Hero
- Full-width section with py-24
- Centered content with max-w-4xl
- Bot name as primary headline with decorative bot icon
- Subtitle describing bot capabilities
- Dual CTA buttons: "Get Started" (primary) + "View Features" (secondary)
- Include trust indicators: "Trusted by X servers" badge below CTAs

### Feature Grid (Home Page)
- 3-column grid showcasing key modules
- Each card includes: module emoji (large), module name, 2-line description, "Learn More" link
- Cards with rounded-2xl borders, p-8 padding
- Hover state with subtle lift (translate-y-1)

### Server Selection Dashboard
- Grid of server cards (mentioned above)
- Each card shows:
  - Server icon (rounded-full, w-16 h-16)
  - Server name (text-lg font-semibold)
  - Member count + bot status indicator
  - "Configure" button (full-width at bottom)
- Cards with defined border, rounded-xl, p-6
- Empty state when no servers: centered message with illustration placeholder

### Module Configuration Interface
- Sidebar navigation (w-64, fixed left side on desktop)
  - Lists all modules with emoji + name
  - Active module highlighted with distinct background
  - Premium badge on premium modules (small pill badge)
- Main content area (remaining width, pl-64 on desktop)
  - Module header: emoji, name, description
  - Configuration status banner (enabled/disabled toggle prominently displayed)
  - Form fields organized in sections
  - "Save Changes" button fixed at bottom or floating

### Forms & Inputs
- **Text Inputs**: rounded-lg, px-4 py-3, border-2, focus ring visible
- **Select Dropdowns**: Same styling as text inputs with chevron icon
- **Textareas**: min-h-32, same border styling
- **Channel Selectors**: Custom dropdown showing # icon + channel names
- **Toggle Switches**: Large, clear on/off states (w-11 h-6)
- **Labels**: Above inputs, text-sm font-medium, mb-2
- **Helper Text**: Below inputs, text-xs, subtle styling

### Buttons
- **Primary**: px-6 py-3, rounded-lg, font-semibold
- **Secondary**: Same size, outlined style
- **Small**: px-4 py-2, text-sm
- **Icon Buttons**: Square, p-2, rounded-lg

### Status Indicators
- **Enabled**: Checkmark emoji + "Enabled" text
- **Disabled**: X emoji + "Disabled" text  
- **Not Configured**: Neutral indicator
- **Premium Required**: Star/crown icon + "Premium" badge

### Cards & Containers
- **Standard Cards**: rounded-xl, p-6, border
- **Elevated Cards**: rounded-xl, p-8, subtle shadow
- **Info Boxes**: rounded-lg, p-4, with icon on left

### Modals/Overlays
- Centered overlay with backdrop blur
- Modal content: rounded-2xl, p-8, max-w-2xl
- Header with title + close button
- Content area with clear sections
- Footer with action buttons (right-aligned)

---

## Page-Specific Layouts

### Home Page Structure
1. **Hero Section** (py-24): Centered content, large headline, CTAs, trust badge
2. **Features Grid** (py-16): 3-column module showcase with cards
3. **How It Works** (py-16): 3-step process with icons and descriptions (horizontal layout)
4. **Premium Features** (py-16): 2-column split (feature list + benefits)
5. **CTA Section** (py-24): Centered call-to-action to dashboard
6. **Footer** (py-12): Navigation links, social links, support link

### Dashboard Page
- Page header with "Your Servers" title + filter/search (if needed)
- Server grid (described above)
- Empty state if no eligible servers
- Footer navigation

### Server Configuration Page
- Breadcrumb navigation: Dashboard > Server Name
- Tab navigation: Overview, Modules, API Settings
- **Overview Tab**: Server info, quick stats, API key status
- **Modules Tab**: Sidebar + main content configuration interface
- **API Settings Tab**: Form for API key and server code input

---

## Images

### Home Page Hero
Include a stylized illustration or screenshot showing the dashboard interface in action. Place it to the right of the hero text (2-column layout on desktop, stacked on mobile). Image should show server cards or module configuration to visualize the product. Size: approximately 600x400px, rounded-2xl corners.

### Feature Cards
Each module feature card includes the corresponding emoji as a large decorative element (text-4xl or larger), positioned at top of card.

### Empty States
When user has no servers or modules not configured, show simple illustration placeholders (friendly robot or server icon) with explanatory text.

---

## Interaction Patterns

### Hover States
- Cards: subtle lift (transform) + enhanced shadow
- Buttons: slight opacity change or solid fill transition
- Navigation links: underline appears
- No complex animations - keep interactions instant and clear

### Loading States
- Skeleton screens for server cards while loading
- Spinner for form submissions
- Progress indicator for multi-step configurations

### Error States
- Inline validation messages below inputs (red text, small icon)
- Toast notifications for system-level errors (top-right corner)
- Disabled states clearly visible with reduced opacity

---

## Responsive Behavior

### Breakpoints
- Mobile: Base (< 768px) - single column, stacked layouts
- Tablet: md (768px+) - 2 columns where applicable
- Desktop: lg (1024px+) - Full grid layouts, sidebar visible

### Mobile Adaptations
- Sidebar navigation becomes bottom sheet or hamburger menu
- Server grid: 1 column with full-width cards
- Forms: Stacked single-column layout
- Hero: Stacked content, smaller text sizes (scale down by 0.75)