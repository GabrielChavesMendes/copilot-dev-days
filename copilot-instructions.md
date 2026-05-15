# Copilot Instructions - Demon Slayer Social Bingo

## Design Guide

### Theme: Dark & Atmospheric Demon Slayer Aesthetic

This application uses a cohesive dark theme inspired by the Demon Slayer anime, featuring dramatic colors, smooth animations, and an immersive battle-ready atmosphere.

#### Color Palette

**Primary Colors (CSS Variables):**
```css
--demon-dark: #0f0a0a;           /* Nearly black background */
--demon-crimson: #8b1429;        /* Deep blood red */
--demon-deep-red: #5a0f15;       /* Darker red for shadows */
--demon-purple: #2a1644;         /* Mystical purple accent */
--demon-gold: #d4a574;           /* Warm gold/bronze highlights */
--demon-accent: #ff4444;         /* Bright red for CTAs & focus */
--demon-glow: #ff6b6b;           /* Lighter red for glows */
```

**Color Usage:**
- **Backgrounds**: Use gradients combining `--demon-dark`, `--demon-deep-red`, and `--demon-purple` (135deg angle)
- **Text**: Primary text uses `#e8dcc8` (warm cream), headers use `--demon-gold` or `--demon-accent`
- **Borders**: All borders use 2px thickness with `--demon-gold` (never 1px)
- **Hover States**: Increase brightness and add subtle glow effects
- **Action Buttons**: Use `--demon-accent` (#ff4444) with hover shadow enhancement

#### Typography

**Font Stack:**
```css
font-family: 'Georgia', 'Garamond', serif;
```
- Classic serif font for elegance and dramatic impact
- Bold weights (600-700) for headers and labels
- Uppercase tracking (0.1em - 0.15em) for dramatic spacing
- Text shadows on prominent elements: `0 0 10px rgba(255, 68, 68, 0.6)` or `0 0 20px rgba(212, 165, 116, 0.6)`

**Text Sizes (Existing Utilities):**
- `.text-5xl` (3rem) - Main titles
- `.text-4xl` (2.25rem) - Section headers
- `.text-lg` (1.125rem) - Instructions/descriptions
- `.text-sm` (0.875rem) - Secondary content
- `.text-xs` (0.75rem) - Metadata/hints

#### Key Design Elements

**Backgrounds:**
- Always use gradient overlays, never solid colors
- Entry point: `linear-gradient(135deg, var(--demon-dark) 0%, var(--demon-deep-red) 50%, var(--demon-purple) 100%)`
- Darker card overlays: `rgba(42, 22, 68, 0.6)` or `rgba(90, 15, 21, 0.4)`
- Semi-transparent elements support contrast and depth

**Borders:**
- Always 2px thickness (not 1px)
- Cards: `border-2 border-amber-400` (gold)
- Headers: `border-b-2 border-amber-400` for separation
- Winning/active states: `border-accent` (#ff4444)

**Shadows & Glows:**
- Subtle shadows: `0 0 20px rgba(255, 68, 68, 0.1), inset 0 0 20px rgba(212, 165, 116, 0.05)`
- Prominent shadows: `0 0 40px rgba(255, 68, 68, 0.2), 0 0 60px rgba(139, 20, 41, 0.3)`
- Glow on hover/active: `text-shadow: 0 0 10px rgba(255, 68, 68, 0.5)`

#### Animations

**Core Animations:**
1. **demonGlow** (2s, infinite)
   - Pulsing red/gold effect for victory states
   - Used on winning board squares
   - ```css
     @keyframes demonGlow {
         0%, 100% { box-shadow: 0 0 20px rgba(255, 68, 68, 0.3), ...; }
         50% { box-shadow: 0 0 40px rgba(255, 68, 68, 0.6), ...; }
     }
     ```

2. **slideIn** (0.6s, ease-out)
   - Entrance animation from top with fade
   - Used on modals, cards, and main content
   - Combines `translateY(-20px)` → `translateY(0)` with opacity

3. **fadeIn** (0.8s, ease-in)
   - Smooth opacity transition for overlays and backgrounds
   - Used on modals and backdrop

4. **spin** (3s, linear, infinite)
   - 360° rotation for decorative background elements
   - Creates mystical atmosphere without distraction

5. **pulse** (2s, cubic-bezier)
   - Breathing effect: opacity 1 → 0.7 → 1
   - Used on victory notifications

**Animation Classes:**
- `.animate-glow` - demonGlow effect
- `.animate-slide-in` - slideIn entrance
- `.animate-fade-in` - fadeIn overlay
- `.animate-spin` - rotating decorative elements
- `.animate-pulse` - breathing effect
- `.animate-bounce` - subtle bouncing (for urgent elements)

#### Component Styling

**Buttons:**
```css
button {
    cursor: pointer;
    border: none;
    background: none;
    font: inherit;
    transition: all 0.3s ease;
}

button:hover {
    filter: brightness(1.2);
    text-shadow: 0 0 10px rgba(255, 68, 68, 0.5);
}
```
- Primary CTAs: `bg-accent text-white font-bold uppercase tracking-wider`
- Hover adds 20% brightness boost and red glow
- Active state: darker background with shadow

**Cards:**
- Base: `rounded-lg p-6 shadow-xl border-2 border-amber-400`
- Background: Semi-transparent with backdrop blur: `backdrop-blur-sm`
- Gradient overlays for depth: `from-demon-deep-red via-demon-crimson to-demon-purple`
- Entry animation: `animate-slide-in`

**Board Squares:**
- Unmarked: `bg-gray-50 text-gray-800 border-2 border-amber-400`
- Marked: `bg-accent border-amber-300 text-white shadow-lg`
- Winning: `bg-gradient-to-br from-amber-400 to-amber-600 border-amber-500 animate-glow`
- Free space: Always gradient + gold border, no interaction
- Checkmark replaced with ⚡ bolt symbol

**Headers:**
- Pattern: `flex items-center justify-between p-4 bg-gradient-to-r from-demon-deep-red to-demon-crimson border-b-2 border-amber-400`
- Text: Uppercase with `.tracking-widest` and `--demon-gold` color
- Adds `text-shadow` with glow effect

**Modals:**
- Backdrop: `fixed inset-0 bg-black/70 backdrop-blur-sm z-50`
- Content: `bg-gradient-to-br from-demon-deep-red via-demon-crimson to-demon-purple`
- Border: `border-2 border-amber-400`
- Animation: `animate-slide-in`
- Entry effect: bounce or glow icon

#### Accessibility & Interaction

**Hover States:**
- All interactive elements brighten by 20% on hover
- Add subtle text glow for buttons
- Shadow enhancement for depth perception

**Active States:**
- Darker background color
- Enhanced shadow effect
- Used for pressed buttons and selected squares

**Focus States (for keyboard nav):**
- Border color changes to `--demon-accent`
- Text glow activated
- Clear visual feedback

**Text Color Contrast:**
- Warm cream (#e8dcc8) on dark backgrounds for readability
- Gold (#d4a574) for secondary text maintaining hierarchy
- Bright red (#ff4444) for important alerts/CTAs
- Always maintain WCAG AA minimum contrast (4.5:1)

#### Spacing & Layout

**Padding:**
- Containers: `p-4` to `p-8`
- Cards: `p-6` standard
- Buttons: `px-6 py-3` to `px-8 py-4`
- Gaps: `gap-1` for board squares, `space-y-2` for text

**Layout:**
- Hero sections: `flex flex-col items-center justify-center min-h-full`
- Headers: `flex items-center justify-between`
- Boards: `grid grid-cols-5 gap-1 aspect-square max-w-md`
- Centering: Always use `mx-auto` with `max-w-*` utilities

#### When Adding New Components

1. **Use existing color variables** - Never hardcode colors outside CSS variables
2. **Add 2px borders** - Thicker borders reinforce the dramatic aesthetic
3. **Apply gradients** - No solid backgrounds; always layer with transparency + gradient
4. **Include animations** - At minimum `animate-fade-in` or `animate-slide-in`
5. **Add text glow** - On hover/active states for interactive elements
6. **Use uppercase tracking** - For headings and CTAs: `.uppercase .tracking-wider` or `.tracking-widest`
7. **Maintain serif typography** - Keep Georgia/Garamond stack
8. **Test in dark mode** - All elements must be readable on dark gradient background

#### CSS Utility Classes Reference

**Layout & Sizing:**
- `.flex`, `.flex-col`, `.grid`, `.grid-cols-5`, `.gap-1`
- `.items-center`, `.justify-center`, `.justify-between`
- `.w-full`, `.h-full`, `.aspect-square`, `.max-w-md`
- `.p-4`, `.px-6`, `.py-3` (padding utilities)
- `.mb-2`, `.mb-4`, `.mx-auto` (margin utilities)

**Typography:**
- `.text-5xl`, `.text-4xl`, `.text-lg`, `.text-sm`, `.text-xs`
- `.font-bold`, `.font-semibold`
- `.text-center`, `.text-left`, `.uppercase`
- `.tracking-wider`, `.tracking-widest`, `.leading-tight`

**Colors:**
- `.bg-accent`, `.bg-marked`, `.bg-gray-50`, `.bg-gray-100`
- `.text-white`, `.text-gray-800`, `.text-amber-500`, `.text-accent`
- `.border-amber-400`, `.border-accent`

**Effects:**
- `.rounded-lg`, `.rounded-xl`, `.border`, `.border-b`
- `.shadow-sm`, `.shadow-xl`
- `.transition-all`, `.transition-colors`, `.duration-150`
- `.animate-glow`, `.animate-slide-in`, `.animate-fade-in`, `.animate-spin`, `.animate-pulse`

**Positioning:**
- `.fixed`, `.absolute`, `.relative`
- `.inset-0`, `.z-50`
- `.top-0\.5`, `.right-0\.5`

### File Structure

- **`app/static/css/app.css`** - All theme colors, animations, and utility classes
- **`app/templates/base.html`** - Base template with meta tags and asset links
- **`app/templates/home.html`** - Home page shell (delegates to start_screen)
- **`app/templates/components/start_screen.html`** - Hero/intro screen
- **`app/templates/components/game_screen.html`** - Main game interface
- **`app/templates/components/bingo_board.html`** - 5x5 board grid
- **`app/templates/components/bingo_modal.html`** - Victory modal

### Design Principles

1. **Dark & Atmospheric** - Never break the dark theme; it's essential to the aesthetic
2. **Dramatic Typography** - Use text shadows, uppercase, and wide tracking for impact
3. **Glowing Accents** - Gold and red provide visual hierarchy and focus
4. **Smooth Transitions** - All interactions have 0.3s+ transitions for polish
5. **Consistent Theming** - Every new element should feel part of the Demon Slayer world
6. **Animation Purpose** - Every animation should enhance immersion, not distract

---

## Development Guidelines

### Adding New Features

When adding new features or pages:

1. **Import existing color variables** from `:root` in CSS
2. **Extend animations** using the established keyframes pattern
3. **Follow the button pattern** for all interactive elements
4. **Apply card styling** for content containers
5. **Use grid/flex utilities** for layout
6. **Test with the app running** - Visual feedback is critical

### Testing the Design

- Run the app: `python -c "from app.main import run; run()"` (starts on port 8000)
- Check all interaction states: hover, active, focused
- Verify animations play smoothly (no jank)
- Test on different screen sizes (responsive design)
- Ensure text contrast meets WCAG AA standards

### Common Customizations

**Change accent color:**
1. Update `--demon-accent` in `:root`
2. All accent-colored elements automatically update

**Modify animation speed:**
1. Adjust keyframe percentages or duration in `.animate-*` classes
2. Example: Change `2s` to `3s` in `demonGlow` for slower pulse

**Add new gradient background:**
1. Use CSS variables: `linear-gradient(angle, var(--demon-color1) 0%, var(--demon-color2) 100%)`
2. Maintain the 135deg diagonal pattern for consistency

---

*Last updated: May 15, 2026 - Demon Slayer Theme Implementation*
