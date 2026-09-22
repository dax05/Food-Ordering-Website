# Complete Beginner's Guide: CSS Properties & The Family Tree

Welcome to part two! If HTML is the **skeleton and bricks** of a house, CSS (**Cascading Style Sheets**) is the **interior designer, painter, and architect**.

CSS decides:
- What colors things are.
- How big things are.
- Where elements sit on the screen.
- What happens when you hover over a button.
- How elements arrange themselves in rows or layers.

This guide breaks down **every single property** used in `style.css` line-by-line, and explains how CSS works hand-in-hand with the **HTML Family Tree**.

---

## 1. The Core Concepts Every Beginner Must Know

### A. The Anatomy of a CSS Rule
```css
.hero-heading {
    color: #007676;
    font-size: 4rem;
}
```
* **Selector (`.hero-heading`)**: Tells the browser: *"Who am I styling?"* (The dot `.` means class name).
* **Declaration Block (`{ ... }`)**: Holds all the design instructions.
* **Property (`color`, `font-size`)**: The specific feature you want to change.
* **Value (`#007676`, `4rem`)**: What you are setting that feature to.
* **Semicolon (`;`)**: Ends the instruction (like a period at the end of a sentence).

---

### B. Understanding CSS Units
| Unit | What it stands for | Real-World Meaning |
| :--- | :--- | :--- |
| `px` | Pixels | Exact digital dots on screen (e.g., `16px`). Fixed and static. |
| `rem` | Root EM | Relative to the `<html>` root font size (`1rem = 16px` by default). Scales cleanly when users zoom in. |
| `%` | Percentage | Relative to the **Parent element's** size (e.g., `width: 50%` means half the parent's width). |
| `vw` | Viewport Width | 1% of the browser window's full width (`10vw = 10%` of screen width). |
| `vh` | Viewport Height | 1% of the browser window's full height (`100vh = 100%` of full screen height). |

---

### C. The Famous "Box Model"
Every single HTML element on your screen is a rectangular box made of four layers:

```text
┌───────────────────────────────────────────────┐
│                    MARGIN                     │  <- Space OUTSIDE the box (pushes neighbors away)
│   ┌───────────────────────────────────────┐   │
│   │                BORDER                 │   │  <- The frame line around the box
│   │   ┌───────────────────────────────┐   │   │
│   │   │            PADDING            │   │   │  <- Space INSIDE the box (breathing room)
│   │   │   ┌───────────────────────┐   │   │   │
│   │   │   │        CONTENT        │   │   │   │  <- The actual text, icon, or image
│   │   │   └───────────────────────┘   │   │   │
│   │   └───────────────────────────────┘   │   │
│   └───────────────────────────────────────┘   │
└───────────────────────────────────────────────┘
```

---

## 2. How the Family Tree Controls CSS

CSS is called **Cascading** because styles cascade down the Family Tree from **Parents** to **Children**.

### Concept 1: Inheritance (Passing Down DNA)
When you give a style to an ancestor, certain properties automatically flow down to all children and grandchildren.
* **Example in your code**:
  ```css
  body {
      font-family: 'Lato', sans-serif;
      color: #141414;
  }
  ```
  Because `<body>` is the parent of everything on the page, every heading, paragraph, button, and list item automatically inherits the `Lato` font and dark text color without you having to write it 50 times!

---

### Concept 2: The Flexbox Parent-Child Contract
Flexbox turns a parent into a **traffic director**:
* You put `display: flex;` on the **Parent**.
* The **Children** instantly line up side-by-side in a row instead of stacking on top of each other!

```text
[ Parent: display: flex; justify-content: space-between; align-items: center; ]
├── Child 1: .hero-content ───────> Pushed to far left
└── Child 2: .hero-img-container ─> Pushed to far right
```

---

### Concept 3: The Positioning Anchor (`relative` vs `absolute`)
This is one of the most powerful tricks in web design:
* If a **Parent** has `position: relative;`, it becomes a **fenced playground**.
* Any **Child** with `position: absolute;` can now be pinned anywhere inside that fence using `top`, `bottom`, `left`, or `right`.

```text
┌────────────────────────────────────────────────────────┐
│ PARENT (.hero-img-container) [position: relative]       │
│                                                        │
│   [Child: Biryani Image]                               │
│    position: absolute; top: -15%; left: -8%;           │
│                                                        │
│   [Child: Testimonial Card]                            │
│    position: absolute; bottom: 5%; left: -25%;         │
└────────────────────────────────────────────────────────┘
```
Without `position: relative` on the parent, the child would fly all the way up to the very top corner of the entire browser window!

---

## 3. Deep Line-by-Line Breakdown of `style.css`

---

### Section 1: The Global Reset (Lines 1–5)
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```
* `*` (Universal Selector): Targets **every single element** on the webpage.
* `margin: 0; padding: 0;`: Every browser (Chrome, Safari, Edge) has default margins and padding that look inconsistent. This wipes them clean to zero so you start with a blank slate.
* `box-sizing: border-box;`: By default, if a box is `200px` wide and you add `20px` padding, the browser makes the box `240px` wide. `border-box` forces the browser to keep the total width at `200px` and absorb padding and borders inside.

---

### Section 2: CSS Custom Properties / Variables (Lines 7–29)
```css
:root {
    --accent-color: #EAF2F5;
    --primary-text-color: #141414;
    --secondary-text-color: #007676;
    --light-text-color: #fff;
    --primary-color: #fff;
    --secondary-color: #007676;
    --alpha-secondary-color: rgba(0, 118, 118, 0.2);
    --discount-color: #E71A1C;
    --card-hover-bg-color: #F9F9F9;
    --border-color: #f9f9f9;
    --box-shadow-color: var(--accent-color);
    --shadow: rgba(0, 0, 0, 0.094);
    --box-shadow: rgba(0, 0, 0, 0.25);
    --discount-banner-background-overlay: linear-gradient(rgba(0, 118, 118, 0.8), rgba(0, 118, 118, 0.8));
    --phone-app-shadow: #C7E1EB;
    --alpha-primary-color: rgba(255, 255, 255, 0.5);
    --rating-color: #FFA800;
    --transition-curve: cubic-bezier(0.36, -0.21, 0.16, 1.97);
}
```
* `:root`: Targets the highest ancestor in the tree (the `<html>` element). Variables defined here are available everywhere.
* `--variable-name`: Custom variables. Think of them as labels/nicknames.
  - If you want to change your brand color later, you change `--secondary-color: #007676;` here once, and it updates across all 50 places on the site!
* `rgba(r, g, b, alpha)`: Red, Green, Blue, and **Alpha** (transparency).
  - `rgba(0, 118, 118, 0.2)` is 20% visible teal.
  - `rgba(255, 255, 255, 0.5)` is 50% semi-transparent white (used for the frosted glass review card).
* `linear-gradient(...)`: A smooth transition between two colors.
* `cubic-bezier(...)`: A custom math curve for bouncy animations.

---

### Section 3: Base Typography & Background (Lines 31–43)
```css
html {
    font-size: 16px; 
}

body {
    font-family: 'Lato', sans-serif;
    color: var(--primary-text-color);
    background-color: var(--primary-color);
}
```
* `font-size: 16px;`: Defines the base ruler for the entire document (`1rem = 16px`).
* `font-family: 'Lato', sans-serif;`: Tells the browser: *"Use the downloaded Lato font. If Lato fails, fall back to any sans-serif font"*.
* `color: var(--primary-text-color);`: Sets text color to dark gray/black `#141414`.
* `background-color: var(--primary-color);`: Sets the page background to white `#fff`.

---

### Section 4: The Navigation Bar (`.navbar`, Lines 45–58)
```css
.navbar {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 4rem;
    display: flex;
    align-items: center;
    padding: 0 10vw;
    z-index: 9;
    background: var(--accent-color);
}
```
* `position: fixed;`: Takes the navbar out of normal flow and locks it to the screen. Even when the user scrolls down, the navbar stays pinned at the top.
* `top: 0; left: 0;`: Positions the fixed navbar flush with the top-left corner.
* `width: 100%;`: Spans edge-to-edge across the screen.
* `height: 4rem;`: `4 * 16px = 64px` tall.
* `display: flex;`: Turns `.navbar` into a Flex Parent. Its direct children (`.logo`, `.links-container`, and `.nav-extras`) line up horizontally side-by-side.
* `align-items: center;`: Centers all children vertically in the middle of the 64px bar.
* `padding: 0 10vw;`: `0` on top/bottom, and `10vw` (10% of screen width) on the left and right sides.
* `z-index: 9;`: Controls stacking layer order. A higher number ensures the navbar floats **on top** of scrolling content below it.
* `background: var(--accent-color);`: Soft light-blue background (`#EAF2F5`).

---

### Section 5: The Logo & Link Items (Lines 60–85)
```css
.logo {
    height: 1.5rem;
}
```
* `height: 1.5rem;`: Scales the logo image to `24px` tall while letting width scale proportionally.

```css
.links-container {
    display: flex;
    gap: 1rem;
    list-style: none;
    margin-left: 7.5%;
}
```
* `display: flex;`: Makes the 4 `<li>` items sit side-by-side horizontally.
* `gap: 1rem;`: Puts `16px` of clean space between each link.
* `list-style: none;`: Removes the default black bullet points from `<ul>`.
* `margin-left: 7.5%;`: Pushes the links list slightly away from the logo.

```css
.links {
    color: var(--primary-text-color);
    text-decoration: none;
    text-transform: capitalize;
    padding: .5rem 1rem;
    transition: .2s;
}

.links:hover {
    color: var(--secondary-text-color);
}
```
* `text-decoration: none;`: Removes the default blue underline from `<a>` tags.
* `text-transform: capitalize;`: Automatically capitalizes the first letter of each link ("menu" -> "Menu").
* `padding: .5rem 1rem;`: `8px` top/bottom, `16px` left/right to enlarge the clickable touch target.
* `transition: .2s;`: Tells the browser: *"When styling changes on hover, animate smoothly over 0.2 seconds rather than jumping instantly."*
* `.links:hover`: Triggered when the user hovers their mouse over the link; changes the color to teal (`#007676`).

---

### Section 6: Right Navigation Group (`.nav-extras`, Lines 87–140)
```css
.nav-extras {
    display: flex;
    align-items: center;
    margin-left: auto;
    gap: 1rem;
}
```
* `display: flex; align-items: center;`: Keeps the search bar and cart icon aligned horizontally and centered.
* `margin-left: auto;`: **CSS Flexbox Secret!** In a flex container, setting `margin-left: auto` on an item consumes all available empty space to its left, pushing this item all the way to the far right edge of the navbar!
* `gap: 1rem;`: Puts a `16px` gap between the search bar and the cart icon.

```css
.search {
    position: relative;
    width: 20vw;
    min-width: 150px;
    height: 2.5rem;
    overflow: hidden;
}
```
* `position: relative;`: Makes this search box the positioning anchor for the absolute search button inside it.
* `width: 20vw; min-width: 150px;`: Takes 20% of the screen width, but will never shrink narrower than 150px.
* `height: 2.5rem;`: `40px` tall.
* `overflow: hidden;`: Cuts off anything inside that spills outside its rounded corners.

```css
.search-box {
    width: 100%;
    height: 100%;
    background: var(--primary-color);
    border: none;
    padding: 1rem;
    outline: none;
    font-size: .9rem;
}
```
* `width: 100%; height: 100%;`: Fills the entire parent `.search` box.
* `border: none;`: Removes default browser input border.
* `padding: 1rem;`: Puts breathing space inside the text box so typed letters don't touch the edges.
* `outline: none;`: Removes the blue/black focus ring when clicked.

```css
.search-btn {
    position: absolute;
    border: none;
    right: 0;
    width: 3rem;
    height: 100%;
    background: var(--primary-color);
    text-align: center;
    cursor: pointer;
    color: var(--secondary-color);
}
```
* `position: absolute; right: 0;`: Glues the magnifying glass button to the inside-right edge of the search box.
* `cursor: pointer;`: Changes the mouse cursor from an arrow to a pointing hand icon when hovered.

```css
.cart {
    width: 2.5rem;
    height: 2.5rem;
    color: var(--secondary-color);
    border-radius: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    transition: .5s;
}

.cart:hover, .locate-btn:hover {
    background: var(--alpha-secondary-color);
}
```
* `border-radius: 100%;`: Turns a square box (`2.5rem x 2.5rem`) into a perfect circle.
* `justify-content: center; align-items: center;`: Centers the cart icon perfectly inside the circle.
* Hover effect: Fills the circle with semi-transparent teal tint (`var(--alpha-secondary-color)`).

---

### Section 7: The Hero Section Layout (`#hero-section`, Lines 144–153)
```css
#hero-section {
    min-height: 100vh;
    padding: 0 10vw;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: var(--accent-color);
}
```
* `min-height: 100vh;`: Guarantees the hero section takes at least 100% of the screen height.
* `display: flex;`: Turns the hero section into a Flex Parent.
* `justify-content: space-between;`: Pushes `.hero-content` (text) to the far left and `.hero-img-container` (graphics) to the far right.
* `align-items: center;`: Centers both columns vertically.

---

### Section 8: Left Column Content (`.hero-content`, Lines 155–188)
```css
.hero-content {
    width: 40%;
}

.hero-heading {
    font-size: 4rem;
    line-height: 5rem;
    font-weight: 700;
    color: var(--secondary-text-color);
}

.hero-line {
    line-height: 2rem;
    opacity: 0.75;
    margin-top: 2rem;
}
```
* `width: 40%;`: Dedicates 40% of the container width to the text column.
* `font-size: 4rem;`: `64px` text size for huge, punchy impact.
* `line-height: 5rem;`: Distance between lines of text so letters don't collide vertically.
* `font-weight: 700;`: Heavy bold weight.
* `opacity: 0.75;`: Makes the descriptive text 75% opaque (slightly faded) for nice visual hierarchy.
* `margin-top: 2rem;`: Pushes the paragraph `32px` down away from the title.

```css
.search.location {
    width: 100%;
    height: 3.5rem;
    border-radius: .2rem;
    margin: 2.5rem 0;
}

.locate-btn {
    font-size: 1.2rem;
    width: 4rem;
    transition: .5s;
}
```
* `.search.location`: Compound selector (matches an element that has **both** `.search` and `.location` classes).
* `margin: 2.5rem 0;`: Puts `40px` of space above and below the search bar.

---

### Section 9: Hero Action Buttons (Lines 190–229)
```css
.hero-action-btn-container {
    display: flex;
    align-items: center;
    gap: 2rem;
}

.btn {
    padding: 1rem 1.5rem;
    border: none;
    border-radius: .3rem;
    font-size: 1rem;
    color: var(--light-text-color);
    background: var(--secondary-color);
    text-transform: capitalize;
    cursor: pointer;
}

.btn.transparent {
    background: transparent;
    border: .1rem solid var(--secondary-color);
    color: var(--secondary-text-color);
}
```
* `display: flex; gap: 2rem;`: Keeps the two buttons and the word "or" lined up with `32px` spacing between them.
* `border-radius: .3rem;`: Gives the buttons softly rounded corners.
* `.btn.transparent`: Overrides the base `.btn` to have a transparent background with a teal border outline.

---

### Section 10: The Right Graphics & Rotating Rings (Lines 230–267)
```css
.hero-img-container {
    min-width: 30rem;
    min-height: 30rem;
    position: relative;
    transform: scale(0.9) translateY(1rem);
}
```
* `min-width: 30rem; min-height: 30rem;`: Sets a square `480px x 480px` canvas.
* `position: relative;`: **Crucial!** This is the anchor fence for the background rings, food dishes, and testimonial card.
* `transform: scale(0.9) translateY(1rem);`: Shrinks everything inside by 10% (`scale(0.9)`) and nudges it down `16px` (`translateY(1rem)`).

```css
.background-ele, .forground-elements {
    width: 100%;
    height: 100%;
    position: absolute;
}
```
* `position: absolute; width: 100%; height: 100%;`: Both layer containers occupy the exact same space, sitting directly on top of each other.

```css
.ellipse {
    position: absolute;
    height: 100%;
    top: 50%;
    left: 50%;
    border-radius: 100%;
    border: .01rem solid var(--secondary-color);
    transform-origin: center;
}

.ellipse:nth-child(1) { width: 80%; transform: translate(-50%, -50%) rotate(20deg); }
.ellipse:nth-child(2) { width: 90%; transform: translate(-50%, -50%) rotate(40deg); }
.ellipse:nth-child(3) { width: 90%; transform: translate(-50%, -50%) rotate(-20deg); }
```
* `top: 50%; left: 50%;`: Pushes the top-left of each ring to the exact center of the parent box.
* `transform: translate(-50%, -50%)`: Offsets the ring back by half its own width and height, centering it perfectly!
* `rotate(20deg)` / `rotate(40deg)` / `rotate(-20deg)`: Rotates each ring at different angles to create an atomic/orbital ring design!
* `:nth-child(n)`: Targets the 1st, 2nd, or 3rd child inside `.background-ele`.

---

### Section 11: Floating Food Dishes (Lines 268–292)
```css
.hero-img {
    position: absolute;
    width: 10rem;
    border-radius: 100%;
    box-shadow: 0rem 1rem 1rem var(--shadow);
}

.hero-img:nth-child(1) { width: 20rem; left: -8%;  top: -15%; }
.hero-img:nth-child(2) { width: 15rem; right: -15%; top: 15%; }
.hero-img:nth-child(3) { width: 15rem; left: 35%;  bottom: -15%; }
```
* `position: absolute;`: Allows each food image to float independently.
* `box-shadow: 0rem 1rem 1rem var(--shadow);`: Adds a soft shadow underneath (`X=0`, `Y=16px`, `Blur=16px`) making the dishes look 3D and hovering above the page.
* Coordinates:
  - Dish 1 (Biryani): Large (`20rem = 320px`), placed near the top-left.
  - Dish 2 (Burger): Medium (`15rem = 240px`), placed on the right.
  - Dish 3 (Pizza): Medium (`15rem = 240px`), placed near the bottom.

---

### Section 12: The Testimonial Review Card (Lines 293–348)
```css
.review-box {
    position: absolute;
    width: 30rem;
    padding: 1rem 2rem;
    bottom: 5%;
    left: -25%;
    border-radius: .5rem;
    background: var(--alpha-primary-color);
    backdrop-filter: blur(.5rem);
}
```
* `bottom: 5%; left: -25%;`: Floats the card over the bottom-left corner of the graphics area.
* `background: var(--alpha-primary-color);`: Semi-transparent white (`rgba(255, 255, 255, 0.5)`).
* `backdrop-filter: blur(.5rem);`: **Glassmorphism effect!** Blurs whatever food or rings are behind this card, creating the modern frosted-glass look.

```css
.reviewer-info {
    display: flex;
    gap: 1rem;
}

.reviewer-img {
    height: 3rem;
    width: 3rem;
    border-radius: 100%;
}

.reviewer-rating {
    display: flex;
    gap: .1rem;
    font-size: .7rem;
    align-items: center;
}

.reviewer-rating i {
    color: var(--rating-color);
}
```
* `.reviewer-info`: A flex parent keeping the customer image and name/rating side-by-side.
* `.reviewer-img`: Makes the user photo a 48px circle (`border-radius: 100%`).
* `.reviewer-rating i`: Descendant selector (styles only `<i>` star icons that live inside `.reviewer-rating`). Sets star color to gold (`#FFA800`).

```css
.reviewer-body {
    display: flex;
    gap: 1rem;
    margin-top: .5rem;
    padding: 1rem 0;
}

.reviewer-body i {
    font-size: 1.4rem;
    color: var(--secondary-color);
}

.review {
    line-height: 1.75rem;
}
```
* `.reviewer-body`: Puts the quotation mark icon (`<i>`) and the text (`<p class="review">`) side-by-side.
* `line-height: 1.75rem;`: Gives the testimonial text plenty of vertical reading comfort.

---

## 4. Visual Summary of CSS Selectors & Tree Relationships

| Selector Type | Example in Code | Meaning in Family Tree |
| :--- | :--- | :--- |
| **Element Selector** | `body`, `html` | Styles every occurrence of that HTML tag. |
| **Class Selector** | `.navbar`, `.btn` | Styles any element that carries `class="..."`. |
| **ID Selector** | `#hero-section` | Styles the one unique element with `id="..."`. |
| **Compound Selector** | `.search.location`, `.btn.transparent` | Styles an element that has **both** classes at the same time. |
| **Descendant Selector** | `.reviewer-rating i`, `.reviewer-body i` | Styles any `<i>` that is a child or grandchild inside that class. |
| **Pseudo-class** | `.links:hover`, `.btn:hover` | Styles the element only when a user interacts with it (e.g. mouse hover). |
| **Structural Selector** | `.ellipse:nth-child(1)` | Targets specifically the 1st child of its parent. |

---

## 5. Next Level Habits for Beginners

1. **Always check parent positioning**: When using `position: absolute;`, make sure the parent has `position: relative;`.
2. **Never leave spaces in units**: Always write `1rem`, `100%`, `10px` without spaces (never `1 rem`).
3. **Use Flexbox on parents**: To arrange children horizontally or center them, style the **parent** (`display: flex; justify-content: center; align-items: center;`).
4. **Use variables for colors**: Define colors once in `:root` so your design stays consistent and easy to update!
