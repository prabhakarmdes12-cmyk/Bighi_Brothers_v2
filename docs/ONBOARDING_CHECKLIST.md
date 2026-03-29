# New Team Member Onboarding Checklist

Welcome to Bighi Brothers! This checklist will help you get up to speed quickly.

---

## Day 1: Getting Started

### Setup (Complete these first)

- [ ] Clone/download the project from the repository
- [ ] Install a code editor (VS Code recommended)
- [ ] Install VS Code extensions:
  - [ ] Live Server (for local preview)
  - [ ] Prettier (code formatter)
  - [ ] HTML CSS Support
  - [ ] JavaScript (ES6) code snippets
- [ ] Open the project in your browser using Live Server

### Understanding the Project

- [ ] Read the [Technical Documentation](../TECHNICAL_DOCUMENTATION.md)
- [ ] Read the [Design System](../bighi_premium_design_system.html)
- [ ] Browse all pages in the `/shop/` folder
- [ ] Test the admin panel at `/admin/index.html`
- [ ] Review the [D2C Strategy](../bighi_brothers_d2c_transformation.html)

### Key Concepts to Understand

- [ ] What is "slow luxury ritual" brand positioning?
- [ ] What are the 3 steps in the Routine Builder? (Cleanse → Treat → Moisturize)
- [ ] Why is WhatsApp important for customer retention?
- [ ] What makes Bighi Brothers different from competitors?

---

## Day 2-3: Making Your First Changes

### Practice Exercises

Complete these tasks in order:

#### Exercise 1: Update a Product Price
1. Open [`shop/product.html`](../shop/product.html)
2. Find the price (search for `₹`)
3. Change the price
4. Preview in browser
5. Revert the change

#### Exercise 2: Add a New Navigation Link
1. Open [`index.html`](../index.html)
2. Find the navigation links (search for `<ul class="nav-links">`)
3. Add a new link to Journal
4. Preview and verify
5. Revert the change

#### Exercise 3: Modify a Color
1. Open any shop page
2. Find the `:root` section with CSS variables
3. Change `--amber` from `#C8831A` to a different shade
4. See how it affects the whole page
5. Revert the change

#### Exercise 4: Add a New Product Card
1. Open [`shop/category.html`](../shop/category.html)
2. Find an existing product card (look for `.product-card`)
3. Copy and paste to create a new one
4. Change the image, name, and price
5. Preview and verify

---

## Day 4-5: Working with JavaScript

### JavaScript Basics to Know

#### Custom Cursor
```javascript
// The cursor has two parts: dot and ring
// Find them in HTML: <div id="cur"></div> and <div id="cur-ring"></div>

// They follow the mouse on mousemove event
document.addEventListener('mousemove', e => {
  cur.style.left = e.clientX + 'px';
  cur.style.top = e.clientY + 'px';
});

// Add hover effects to links
document.querySelectorAll('a, button').forEach(el => {
  el.addEventListener('mouseenter', () => document.body.classList.add('cursor-link'));
  el.addEventListener('mouseleave', () => document.body.classList.remove('cursor-link'));
});
```

#### Tab Switching
```javascript
// Each tab section has data-group attribute
// Tab buttons have onclick that calls switchTab()

function switchTab(tabId, groupId) {
  // Hide all in group
  document.querySelectorAll(`[data-group="${groupId}"]`).forEach(s => {
    s.classList.remove('active');
  });
  // Show selected
  document.getElementById(tabId).classList.add('active');
}
```

#### Form Handling
```javascript
// Get form values
const name = document.getElementById('nameInput').value;

// Validate
if (name === '') {
  alert('Please enter your name');
  return;
}

// Submit (in a real app, this would send to a server)
console.log('Form submitted:', { name });
```

---

## Common Tasks Reference

### How to Add a New Page

1. Create a new HTML file in the appropriate folder
2. Copy the header/nav structure from an existing page
3. Copy the footer from an existing page
4. Update the `<title>` tag
5. Link it from the navigation

### How to Update Product Information

1. Open the relevant page (`category.html` or `product.html`)
2. Find the product section
3. Update: name, price, description, images
4. Save and preview

### How to Change Colors

1. Find the `:root` section in the `<style>` block
2. Update the CSS variable value
3. All elements using that variable will update automatically

### How to Add a WhatsApp Link

```html
<a href="https://wa.me/919523180794?text=Hi, I have a question about...">
  💬 Chat with us
</a>
```

Format: `https://wa.me/` + `91` + `phone number without spaces`

---

## Testing Checklist

Before any change is complete, verify:

- [ ] Page loads without errors (check Console)
- [ ] All images display correctly
- [ ] Links go to the right pages
- [ ] Mobile view looks good (resize browser)
- [ ] Forms submit properly (or show correct error)
- [ ] Colors match the design system

---

## Glossary of Terms

| Term | Meaning |
|------|---------|
| CSS Variable | A reusable value like `--amber: #C8831A` |
| Class | A reusable style identifier (e.g., `class="btn"`) |
| ID | A unique identifier (e.g., `id="main-nav"`) |
| DOM | Document Object Model — the page structure |
| Event | An action like click, hover, scroll |
| Function | A reusable block of code |
| Array | A list of items like `[1, 2, 3]` |
| Object | A data structure like `{name: "Soap", price: 50}` |

---

## Troubleshooting

### Something looks broken?

1. Did you save the file?
2. Did you clear the browser cache? (Ctrl+Shift+R)
3. Is there a syntax error? (Check the Console tab)
4. Did you make a typo in a class name?

### Browser Tools to Know

- **Elements Tab** — Inspect and modify HTML/CSS live
- **Console Tab** — See JavaScript errors and logs
- **Sources Tab** — Debug JavaScript step by step
- **Network Tab** — See if images/scripts fail to load

### Getting Help

1. Check the Technical Documentation
2. Ask a senior team member
3. Search online for the specific error

---

## Your First Real Task

Once you've completed all exercises, here's a real task to try:

**Task:** Update the featured products section in `index.html`

1. Open the homepage
2. Find the product showcase section
3. Replace one product with a different one
4. Change the image, name, and price
5. Make sure it links to the correct product page
6. Get it reviewed by a senior developer

---

*Welcome aboard! We're excited to have you on the team.* 🌿
