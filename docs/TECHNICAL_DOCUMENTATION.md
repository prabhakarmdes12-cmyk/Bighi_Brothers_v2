# Bighi Brothers Website — Technical Documentation

> **Version:** 1.0.0  
> **Last Updated:** March 2026  
> **For:** Tech Team, Interns, New Developers  
> **Stack:** Vanilla HTML/CSS/JavaScript (Static Site)

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [File Structure](#2-file-structure)
3. [Design System](#3-design-system)
4. [Styling Guidelines](#4-stylling-guidelines)
5. [JavaScript Components](#5-javascript-components)
6. [Admin Panel Guide](#6-admin-panel-guide)
7. [Content Management](#7-content-management)
8. [Deployment](#8-deployment)
9. [Troubleshooting](#9-troubleshooting)
10. [Glossary](#10-glossary)

---

## 1. Project Overview

### What is Bighi Brothers?
Bighi Brothers is a handmade natural skincare brand. The website showcases products, tells their story, and enables e-commerce transactions.

### Technology Stack
| Component | Technology | Notes |
|-----------|------------|-------|
| Frontend | Vanilla HTML5, CSS3, JS (ES6) | No framework dependencies |
| Styling | CSS Custom Properties | Variables defined in `:root` |
| Fonts | Google Fonts | Playfair Display, EB Garamond, Cormorant Garamond, DM Mono |
| Images | Unsplash CDN | Placeholder images for development |
| Deployment | Static Hosting | Netlify, Vercel, or standard web hosting |

### Key Design Principles
1. **Slow Luxury Aesthetic** — Inspired by Aesop × Forest Essentials
2. **Dark-to-Cream Narrative** — Dark hero sections transitioning to light content
3. **Minimalist Typography** — Serif fonts with generous spacing
4. **Natural Color Palette** — Forest greens, warm ambers, cream neutrals

---

## 2. File Structure

```
Bighi_Brothers_Website/
├── index.html                 # Main homepage
│
├── docs/
│   ├── TECHNICAL_DOCUMENTATION.md   # This file
│   ├── DESIGN_SYSTEM.md             # Design specifications
│   └── ONBOARDING_CHECKLIST.md      # New team member checklist
│
├── journal/
│   └── index.html             # Blog/journal page
│
├── shop/
│   ├── category.html          # Product listing page
│   ├── product.html           # Single product detail page
│   ├── account.html           # Login/register/profile
│   ├── checkout.html          # 4-step checkout flow
│   └── order-success.html     # Order confirmation
│
├── admin/
│   └── index.html             # Shopkeeper admin panel
│
├── bighi_brothers_d2c_transformation.html   # Business strategy doc
├── bighi_premium_design_system.html         # Design system reference
└── bighi_shop_pages.html                   # Legacy shop page
```

---

## 3. Design System

### Color Palette

```css
:root {
  /* Primary Colors */
  --cream: #F5EFE0;        /* Main light background */
  --forest: #1C3A2E;       /* Primary dark green */
  --forest2: #162D24;      /* Darker shade for contrast */
  
  /* Accent Colors */
  --amber: #C8831A;        /* Primary CTA, highlights */
  --amberl: #E8A830;       /* Lighter amber for hover states */
  
  /* Neutral Colors */
  --offwhite: #FAF7F2;     /* Light sections */
  --charcoal: #2D2D2D;     /* Dark text */
  --warm: #8C8070;         /* Muted text */
  
  /* Functional */
  --border: rgba(28,58,46,0.11);  /* Subtle borders */
  --ease: cubic-bezier(0.25,0.46,0.45,0.94);  /* Custom easing */
  --green: #25D366;       /* WhatsApp green */
}
```

### Typography Scale

| Element | Font | Size | Weight | Style |
|---------|------|------|--------|-------|
| Hero Title | Playfair Display | 4-6rem | 400-600 | Italic |
| Section Title | Playfair Display | 2-3rem | 400 | Italic |
| Body Text | EB Garamond | 1rem | 400 | Normal |
| Navigation | Cormorant Garamond | 0.8rem | 400-500 | Uppercase, Letter-spacing |
| Labels | DM Mono | 0.6rem | 400 | Uppercase |
| Prices | Cormorant Garamond | 0.9-1.3rem | 400-500 | Normal |

### Breakpoints

```css
/* Mobile First */
@media (max-width: 600px) { /* Mobile */ }
@media (max-width: 900px) { /* Tablet */ }
@media (max-width: 1200px) { /* Small Desktop */ }
```

---

## 4. Styling Guidelines

### CSS Organization

Each HTML file contains its own styles in a `<style>` block. For larger projects, consider extracting to separate CSS files.

### Common Patterns

#### Button Styles
```css
.btn-primary {
  background: var(--amber);
  color: white;
  padding: 12px 24px;
  font-family: 'Cormorant Garamond', serif;
  font-size: 0.8rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  border: none;
  border-radius: 1px;
  cursor: pointer;
  transition: all 0.3s var(--ease);
}

.btn-primary:hover {
  background: var(--forest);
}
```

#### Card Components
```css
.card {
  background: var(--offwhite);
  border: 1px solid var(--border);
  padding: 24px;
  border-radius: 2px;
  transition: all 0.3s var(--ease);
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(0,0,0,0.1);
}
```

#### Form Inputs
```css
.form-input {
  width: 100%;
  padding: 12px 16px;
  background: var(--offwhite);
  border: 1px solid var(--border);
  font-family: 'EB Garamond', serif;
  font-size: 0.95rem;
  color: var(--charcoal);
  border-radius: 1px;
  outline: none;
  transition: border-color 0.3s;
}

.form-input:focus {
  border-color: var(--amber);
}
```

---

## 5. JavaScript Components

### Custom Cursor

The website uses a custom cursor with a trailing ring effect:

```javascript
const cur = document.getElementById('cur');
const curRing = document.getElementById('cur-ring');

document.addEventListener('mousemove', e => {
  cur.style.left = e.clientX + 'px';
  cur.style.top = e.clientY + 'px';
  curRing.style.left = e.clientX + 'px';
  curRing.style.top = e.clientY + 'px';
});

// Hover states
document.querySelectorAll('a, button').forEach(el => {
  el.addEventListener('mouseenter', () => document.body.classList.add('cursor-link'));
  el.addEventListener('mouseleave', () => document.body.classList.remove('cursor-link'));
});
```

**CSS States:**
- `body.cursor-link` — Cursor changes to smaller circle
- `body.cursor-product` — Larger cursor for product images

### Tab Navigation

Used in product detail pages and admin panels:

```javascript
function switchTab(tabId, groupId) {
  // Hide all sections in group
  document.querySelectorAll(`[data-group="${groupId}"]`).forEach(s => {
    s.classList.remove('active');
  });
  // Show selected section
  document.getElementById(tabId).classList.add('active');
  
  // Update tab buttons
  document.querySelectorAll(`[onclick*="${groupId}"]`).forEach(btn => {
    btn.classList.remove('active');
  });
  event.target.classList.add('active');
}
```

### Image Gallery

```javascript
function changeImage(src) {
  document.getElementById('mainImage').src = src;
  // Update thumbnail active state
  document.querySelectorAll('.thumbs img').forEach(t => {
    t.classList.remove('active');
  });
  event.target.classList.add('active');
}
```

---

## 6. Admin Panel Guide

### Access Levels

| Role | Permissions |
|------|-------------|
| Super Admin | Full access to all features |
| Manager | Products, Orders, Customers, Marketing |
| Fulfillment Staff | Orders only |
| Customer Support | Orders, Customers, WhatsApp |

### Dashboard Sections

#### 1. Stats Overview
- Revenue (today, this week, this month)
- Orders (pending, processing, shipped, delivered)
- Conversion rate
- Active customers

#### 2. Orders Management
- View all orders with status filters
- Update order status
- Print packing slips
- Export order data

#### 3. Product Inventory
- Add/edit/delete products
- Manage variants (sizes, scents)
- Update stock levels
- Set prices

#### 4. WhatsApp Queue
- Review pending messages
- Resend failed messages
- Message templates

### Common Tasks

#### Adding a New Product
1. Go to **Commerce → Products**
2. Click **Add New**
3. Fill in details:
   - Product name
   - Description
   - Price
   - Category
   - Images
   - Stock quantity
4. Click **Save Product**

#### Updating Order Status
1. Go to **Commerce → Orders**
2. Find the order by ID or customer name
3. Click on the order
4. Change status dropdown
5. Optionally send WhatsApp update
6. Click **Update**

#### Managing Inventory Alerts
1. Go to **Commerce → Inventory**
2. Set low stock threshold (default: 10)
3. Review items below threshold
4. Click **Restock** to update quantity

---

## 7. Content Management

### Product Data Structure

```javascript
const product = {
  id: "prod_001",
  name: "Marigold Mountain Soap",
  tagline: "Handmade with mountain herbs",
  price: 50,
  currency: "₹",
  category: "soap",
  images: [
    "https://images.unsplash.com/...",
    "https://images.unsplash.com/..."
  ],
  variants: [
    { size: "90g", price: 50 },
    { size: "150g", price: 80 }
  ],
  description: "Full product description...",
  ingredients: ["Marigold", "Neem", "Coconut Oil"],
  howToUse: "Step by step instructions...",
  stock: 45,
  featured: true
};
```

### Journal Post Structure

```javascript
const post = {
  id: "post_001",
  title: "New Spring Collection Launch",
  category: "updates", // updates, ingredients, rituals, behind-scenes, changelog
  date: "2026-03-15",
  excerpt: "Brief excerpt for cards...",
  content: "Full HTML content...",
  featured: true
};
```

### Customer Data Structure

```javascript
const customer = {
  id: "cust_001",
  name: "Priya Sharma",
  email: "priya@example.com",
  phone: "+91 98765 43210",
  whatsapp: true, // opted in
  orders: ["BB-2026-0342", "BB-2026-0310"],
  routine: ["Marigold Soap", "Shea Cream"],
  created: "2026-01-15"
};
```

---

## 8. Deployment

### Static Hosting Options

1. **Netlify** (Recommended)
   - Drag and drop deployment
   - Free SSL
   - Custom domain support
   
2. **Vercel**
   - Similar to Netlify
   - Good Git integration

3. **GitHub Pages**
   - Free for public repos
   - Limited features

### Deployment Steps

#### Netlify
1. Go to [netlify.com](https://netlify.com)
2. Sign up / Log in
3. Drag the entire project folder to the dashboard
4. Your site will be live at `random-name.netlify.app`
5. Connect custom domain in settings

#### Custom Domain
1. Purchase domain (e.g., from GoDaddy, Namecheap)
2. Add domain to hosting provider
3. Update DNS records:
   - A record: Points to hosting IP
   - CNAME: www points to @ or vice versa
4. Enable SSL/HTTPS

### File Upload
For simple hosting (cPanel, FTP):
1. Upload all HTML, CSS, JS files to `public_html` or `www` folder
2. Keep folder structure intact
3. Index page must be named `index.html`

---

## 9. Troubleshooting

### Common Issues

#### Cursor Not Working
**Symptom:** Custom cursor doesn't appear or moves erratically  
**Fix:** Check that `#cur` and `#cur-ring` elements exist in HTML

#### Images Not Loading
**Symptom:** Product images show broken icons  
**Fix:** 
- Check image URLs are correct
- Verify CORS settings if using external images
- Replace with local images in `/images/` folder

#### CSS Not Applying
**Symptom:** Styles look wrong  
**Fix:**
- Clear browser cache (Ctrl+Shift+R)
- Check for syntax errors in CSS
- Verify class names match in HTML

#### Mobile Layout Broken
**Symptom:** Site looks wrong on phones  
**Fix:**
- Check `@media` queries are in correct order
- Verify viewport meta tag: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- Test on actual devices, not just DevTools

#### WhatsApp Links Not Working
**Symptom:** WhatsApp button doesn't open chat  
**Fix:** Update phone number in format: `https://wa.me/91XXXXXXXXXX`

### Debug Mode

Add this to temporarily enable console logging:

```javascript
const DEBUG = true;
if (DEBUG) {
  console.log('Current state:', state);
  console.log('Clicked element:', event.target);
}
```

---

## 10. Glossary

| Term | Definition |
|------|------------|
| **CTA** | Call to Action — A button or link prompting user action |
| **D2C** | Direct to Consumer — Selling directly without middlemen |
| **PDP** | Product Detail Page — Single product information page |
| **PLP** | Product Listing Page — Grid of multiple products |
| **SKU** | Stock Keeping Unit — Unique product identifier |
| **CRM** | Customer Relationship Management — System for managing customer data |
| **KPI** | Key Performance Indicator — Metrics to track success |
| **UI/UX** | User Interface / User Experience — Design and interaction |
| **CSS Variables** | Reusable values defined in CSS (custom properties) |
| **Vanilla JS** | Plain JavaScript without frameworks |
| **CDN** | Content Delivery Network — Server network for fast asset delivery |
| **SSL** | Secure Sockets Layer — Encrypts data between browser and server |
| **Refill Reminder** | Automated message reminding customers to reorder |
| **Routine Builder** | Tool helping customers build a complete skincare routine |
| **WhatsApp Queue** | System for managing automated WhatsApp messages |

---

## Quick Reference Card

```
╔═══════════════════════════════════════════════════════════╗
║                 BIGHI BROTHERS QUICK REF                 ║
╠═══════════════════════════════════════════════════════════╣
║ Color Variables:   --cream, --forest, --amber             ║
║ Font Families:     Playfair Display, EB Garamond         ║
║ Primary CTA:       var(--amber) background               ║
║ Secondary:         var(--forest) background              ║
║ Hover Transition:  0.3s var(--ease)                      ║
║ Cursor Class:      .cursor-link                           ║
║ Breakpoints:       600px, 900px, 1200px                  ║
║ WhatsApp Green:     #25D366                               ║
║ Main Email:        namaste@bighibrothers.com             ║
║ Phone:             +91 89279 4459                        ║
║ WhatsApp:          +91 95231 80794                        ║
╚═══════════════════════════════════════════════════════════╝
```

---

## Getting Help

1. **Code Issues:** Check this documentation first
2. **Design Questions:** See `bighi_premium_design_system.html`
3. **Business Logic:** See `bighi_brothers_d2c_transformation.html`
4. **Unresolved:** Contact senior developer or create issue ticket

---

*Document Version: 1.0.0 | Last Updated: March 2026*
