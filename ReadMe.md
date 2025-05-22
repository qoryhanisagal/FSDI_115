### MOBILE-FIRST LAYOUT
---

This challenge demonstrates a **mobile-first responsive CSS layout**. The design starts with styles for small screens and scales up for larger devices. The approach ensures optimal user experience on mobile devices before adapting to tablets and desktops.

---

### CSS STRUCTURE
---

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem;
}

@media (min-width: 600px) {
  .container {
    padding: 2rem;
  }
}

@media (min-width: 900px) {
  .container {
    display: flex;
    flex-direction: row;
    gap: 2rem;
  }
}
```

---

### Explanation & Comments
---

- **Mobile-first:**  
  - The base CSS applies to all devices, focusing on readability and simple layout for mobile users.
- **Container:**  
  - `.container` centers the content and limits its maximum width.
  - Padding increases at 600px for tablets and above.
- **Media Queries:**  
  - At 900px and up, `.container` becomes a flex container for a side-by-side layout, suitable for desktops.
- **Why mobile-first?**  
  - Ensures fast loading and best experience for the majority of users who visit on mobile devices.
  - Enhances progressive enhancement and accessibility.

---
Let me explain the important bits. So I started mobile-first using Flexbox for vertical stacking. When the screen is big enough, I switch to Grid because it gives me more control. I define named grid areas like main, nav, or footer, and then I assign each box to its area using grid-area. This lets me keep my layout logic super readable and makes it easy to rearrange things across screen sizes.
```css
.container {
  display: flex; 
  flex-direction: column; 
  gap: 1rem;
  padding: 1rem;
}
```
I’m starting with a mobile-first layout, so I’m using Flexbox to stack everything vertically. It’s simple and easy to follow for small screens.

- **display:** flex creates a flex container.
- **flex-direction:** column makes the items stack vertically.
- **gap:** 1rem adds space between the stacked items.
- **padding:** 1rem gives breathing room around the content.

### Base Box Styling + Colors
```css
.box {
  height: 80px;
  background-color: gray;
}
```
- **I give all my layout boxes a base height and gray background, just to start.**

```css
.header { background: gold; }
.nav { background: #666; }
.subnav-1, .subnav-2 { background: hotpink; }
.side { background: skyblue; }
.main { background: black; height: 150px; }
.banner { background: lightgreen; }
.footer { background: orange; }
```
- Then I give each section a different color so I can see which is which during development.

- I made `.main` taller so it stands out — my thought is was made to represent more content.

### Tablet Layout `(min-width: 641px)` - Switch to Grid
```css
@media (min-width: 641px) {
  .container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-areas:
      "header header"
      "nav nav"
      "subnav-1 subnav-2"
      "side main"
      "banner banner"
      "footer footer";
    gap: 1rem;
  }
```

- Once the screen hits 641px, I switch to Grid so I can layout content side-by-side. I define two equal columns with 1fr 1fr. Then I name the layout zones using grid-template-areas so I don’t have to manually place everything by numbers.

- This makes it easy to visualize how the layout is structured.

#### **What does `1fr` mean in a CSS Grid?**
```css
grid-template-columns: 1fr 2fr;
```
**You’re telling the browser:**
- Divide the available space into **3 equal parts**
- The **first column** gets **1 part**
- The **second column** gets **2 parts**
 
 **So:**
- The first column takes up **⅓** of the space
- The second column takes up **⅔**

#### **Line 35: 
```css
grid-template-columns: 1fr 1fr;
```
- You’re dividing the space **evenly** into **2 equal columns.**
- Each `1fr` takes up **half** of the available horizontal space (after margins/gaps/padding are considered).**

**Remember you can mix and match:**
```css
grid-template-columns: 1fr 3fr;
```
- First column: 25%
- Second column: 75%

#### Tips to Remember
**Think of fr as “share of the space” — not pixels, not percent, but fractions of whatever space is left.**

#### **Line 37: `header header` 
This line is part of the grid-template-areas in the tablet media query. It tells the browser to place the header element across both columns in this row.

- **So visually, it's like**

```
| header | header |
```
**Then on the line:**
```
"side main"
```
**This means**

- The **left column** should hold the side element
- The **right column** should hold the main element

- **So it looks like:**
```
|  side  |  main  |
```
- Each quoted line in grid-template-areas represents one row, and each word represents a grid area (box) placed in that column for that row. Remember by 10x10 analogy

- The structure tells the browser exactly how to place and span elements across rows and columns. Repeating the same name (like header header) means that element should span both columns.

**Here I’m assigning each box to the area I named above**
```css
  .header { grid-area: header; }
  .nav { grid-area: nav; }
  .subnav-1 { grid-area: subnav-1; }
  .subnav-2 { grid-area: subnav-2; }
  .side { grid-area: side; }
  .main { grid-area: main; }
  .banner { grid-area: banner; }
  .footer { grid-area: footer; }
}
```
- Each section is then assigned to one of the grid areas using grid-area. This way I can move things around in my layout just by changing the grid template. Therefore, there is no need to adjust each element manually.

####  How each box is getting assigned to a specific area using grid-area and grid-template-areas?
Looking at the full code for Table Layout
```css
/* Tablet layout starts here — this is for screens 641px and wider */
@media (min-width: 641px) {
  .container {
    display: grid; /* I’m switching from flex to grid so I can control layout more precisely */
    grid-template-columns: 1fr 1fr; /* Two equal columns */
    grid-template-areas:
      "header header"        /* Header spans both columns */
      "nav nav"              /* Nav spans both columns */
      "subnav-1 subnav-2"    /* Subnavs go side-by-side */
      "side main"            /* Side and main content side-by-side */
      "banner banner"        /* Banner spans full width */
      "footer footer";       /* Footer also spans full width */
    gap: 1rem; /* Space between all the areas */
  }

  /* Here I’m assigning each box to the area I named above */
  .header { grid-area: header; }
  .nav { grid-area: nav; }
  .subnav-1 { grid-area: subnav-1; }
  .subnav-2 { grid-area: subnav-2; }
  .side { grid-area: side; }
  .main { grid-area: main; }
  .banner { grid-area: banner; }
  .footer { grid-area: footer; }
}
```
**Let's do this in step so it is easier to follow along.**

#### Step 1: Define the Layout Blueprint with grid-template-areas
 Inside the media query:
 ```css
    grid-template-areas:
    "header header"
    "nav nav"
    "subnav-1 subnav-2"
    "side main"
    "banner banner"
    "footer footer";
```
**What I am doing here:**
 I am naming the sections `(grid areas)` of my layout **like a blueprint**

**Each string:**
- Represents one row in the grid
- Each word represents a cell (or slot) in that row
- If a word is repeated, it means that element spans across multiple columns
 ```css
"header header"
 ```
 Means: the header element takes up **both columns** in **row 1.**

 ####  Step 2: Assign Elements to Those Named Areas

 Then, you use grid-area to **match each HTML element to the area name** from the blueprint:
```css
.header { grid-area: header; }
.nav { grid-area: nav; }
.subnav-1 { grid-area: subnav-1; }
.subnav-2 { grid-area: subnav-2; }
.side { grid-area: side; }
.main { grid-area: main; }
.banner { grid-area: banner; }
.footer { grid-area: footer; }
```
#### How it works?
- The `.header` class is told: “You belong to the `"header"` area in the grid layout”
- The browser then **places that box** in the spot where `header` appears in grid-template-areas

#### Think of It Like This:

1.	`grid-template-areas` is your **map**
2.	`grid-area` is your way of **dropping each box into its labeled destination**

So if `"nav nav"` is row 2 in your map,
and you write `.nav` `{ grid-area: nav; }`, then that `.nav` element gets placed right there, spanning across both columns.

#### What Happens if You Mismatch?
If you don’t use grid-area or misspell it (like .navbar instead of .nav), your item won’t be placed in the grid correctly and may either not show up or appear outside the layout.

### Desktop Layout `(min-width: 1008px)` - More Columns

```css
@media (min-width: 1008px) {
  .container {
    grid-template-columns: 1fr 2fr 1fr;
    grid-template-areas:
      "header header header"
      "nav nav nav"
      "subnav-1 subnav-2 subnav-2"
      "side main main"
      "banner banner banner"
      "footer footer footer";
  }
}
```

- **For desktop, I add a third column and update the layout to give more space to areas like main and subnav-2. This lets the content breathe more on wider screens.**

### More on Gris Templates Line: 59
```css
 grid-template-columns: 1fr 2fr 1fr;
```

This defines a 3-column grid layout, and here’s what each part means:
- `1fr` → First column gets 1 share of available space
- `2fr` → Second column gets 2 shares (twice as wide)
- `1fr` → Third column gets 1 share

#### What does this do?
It splits the row into 4 equal parts (1 + 2 + 1 = 4 parts total):
```
| Column         | Fraction | Percentage of space |
|----------------|----------|---------------------|
| First column   | 1fr      | 25%                 |
| Second column  | 2fr      | 50%                 |
| Third column   | 1fr      | 25%                 |
```
So if your container is 1200px wide:
- First column: 300px
- Second column: 600px
- Third column: 300px

#### When do you use this?
Use this layout when:
- You want the middle column (main content) to be wider than the sides
- The left and right columns are usually for a sidebar or spacing
- It’s perfect for a center-focused layout with balanced margins on each side.