# Content Management Guide

## For Shopkeepers & Content Managers

> This guide explains how to update website content without needing to know how to code. Follow the step-by-step instructions carefully.

---

## Table of Contents

1. [Updating Product Information](#1-updating-product-information)
2. [Adding New Products](#2-adding-new-products)
3. [Managing Journal/Blog Posts](#3-managing-journalblog-posts)
4. [Updating the Homepage](#4-updating-the-homepage)
5. [Managing Orders](#5-managing-orders)
6. [Customer Communication](#6-customer-communication)
7. [Inventory Management](#7-inventory-management)

---

## 1. Updating Product Information

### Where Products Are Located

Products appear in multiple places:
- [`shop/category.html`](../shop/category.html) — Product grid/list
- [`shop/product.html`](../shop/product.html) — Individual product details
- [`index.html`](../index.html) — Featured products on homepage

### How to Edit a Product

#### Step 1: Find the Product Code

Open the relevant file and search for the product name. For example, to edit "Marigold Mountain Soap":

1. Press `Ctrl+F` (Windows) or `Cmd+F` (Mac)
2. Type "Marigold"
3. Press Enter

#### Step 2: Identify Product Sections

A product typically has these parts:

```html
<!-- Product Card (in category.html) -->
<div class="product-card">
  <img src="IMAGE_URL" alt="Product Name">
  <div class="product-name">Marigold Mountain Soap</div>
  <div class="product-price">₹50</div>
  <button>Add to Cart</button>
</div>
```

#### Step 3: Make Your Changes

| What to Change | How to Change It |
|----------------|------------------|
| Product Name | Edit the text between tags |
| Price | Change the number (keep ₹ symbol) |
| Image | Replace the URL in `src="..."` |
| Description | Find and edit the description text |

#### Step 4: Save and Preview

1. Save the file (`Ctrl+S`)
2. Open in browser (or refresh)
3. Verify the changes look correct

---

## 2. Adding New Products

### Quick Method: Copy and Modify

1. Find an existing product similar to what you want to add
2. Copy the entire product section
3. Paste it below
4. Modify the details (name, price, image, description)
5. Save and test

### Product Card Template

```html
<div class="product-card">
  <a href="shop/product.html">
    <img src="IMAGE_URL_HERE" alt="PRODUCT NAME">
  </a>
  <div class="product-info">
    <a href="shop/product.html"><h3 class="product-name">PRODUCT NAME</h3></a>
    <p class="product-tagline">Brief tagline here</p>
    <div class="product-footer">
      <span class="product-price">₹PRICE</span>
      <button class="quick-add-btn" onclick="addToCart('prod_id')">+ Add</button>
    </div>
  </div>
</div>
```

### Image Guidelines

| Type | Recommended Size | Format |
|------|------------------|--------|
| Product Main | 800×800 px | JPG, WebP |
| Product Thumb | 200×200 px | JPG, WebP |
| Hero/Banner | 1600×600 px | JPG, WebP |

**Free Image Sources:**
- [Unsplash](https://unsplash.com) — Search for skincare/nature
- [Pexels](https://pexels.com) — Free stock photos
- Take your own photos with good lighting

### Where to Get Image URLs

For development, use Unsplash URLs:
1. Go to [unsplash.com](https://unsplash.com)
2. Search for your image
3. Click on it
4. Copy the URL from the browser address bar
5. Or right-click → Copy Image Address

---

## 3. Managing Journal/Blog Posts

### Journal Structure

The Journal page ([`journal/index.html`](../journal/index.html)) has:
- Featured post (large card at top)
- Category filter tabs
- Post grid
- Sidebar with categories and newsletter

### How to Add a New Post

1. Open [`journal/index.html`](../journal/index.html)
2. Find an existing post in the grid
3. Copy and paste the entire `<article class="jp-card">` section
4. Modify the content:

```html
<article class="jp-card">
  <a href="#" class="jp-img-wrap">
    <img src="POST_IMAGE_URL" alt="Post Title" class="jp-img">
  </a>
  <div class="jp-content">
    <div class="jp-meta">
      <span class="jp-cat" style="background: rgba(200,131,26,0.1); color: var(--amber);">CATEGORY</span>
      <span class="jp-date">March 29, 2026</span>
    </div>
    <h3 class="jp-title"><a href="#">POST TITLE</a></h3>
    <p class="jp-excerpt">Brief excerpt of the post...</p>
    <a href="#" class="jp-read">Read More →</a>
  </div>
</article>
```

### Category Colors

| Category | Color Code |
|----------|------------|
| Updates | `--amber` (#C8831A) |
| Ingredients | `--forest` (#1C3A2E) |
| Rituals | Green |
| Behind the Scenes | Brown |
| Changelog | Gray |

---

## 4. Updating the Homepage

### Homepage Sections

The homepage ([`index.html`](../index.html)) has these key sections:

| Section | What's There | Line Number |
|---------|---------------|-------------|
| Announcement Bar | Shipping promos, sales | ~Line 77 |
| Navigation | Menu links | ~Line 87 |
| Hero | Main banner with CTA | ~Line 149 |
| Routine Section | 3-step ritual | ~Line 950 |
| Products | Featured products | ~Line 1250 |
| About | Brand story | ~Line 1400 |
| Footer | Links, social, newsletter | ~Line 2078 |

### Common Homepage Edits

#### Change Hero Text
```html
<h1 class="hero-title">Your New Title Here</h1>
<p class="hero-sub">Your subtitle text here</p>
```

#### Update Announcement Bar
```html
<div class="ann">
  Your announcement text here — <b>Bold highlight</b>
</div>
```

#### Change CTA Button Link
```html
<a href="shop/category.html" class="hero-cta">
  Shop Collection <span>→</span>
</a>
```

---

## 5. Managing Orders

### Accessing the Admin Panel

1. Go to [`admin/index.html`](../admin/index.html)
2. The dashboard shows order statistics

### Order Status Flow

```
New Order → Processing → Shipped → Delivered
              ↓
           Cancelled
```

### Updating Order Status

1. Find the order in the Orders table
2. Click on the order row
3. Change the status dropdown
4. Click Update

### Order ID Format

Orders use this format: `BB-YYYY-NNNN`
- `BB` = Bighi Brothers
- `YYYY` = Year
- `NNNN` = Sequential number

Example: `BB-2026-0342`

---

## 6. Customer Communication

### WhatsApp Templates

Use these pre-written messages:

#### Order Confirmation
```
Namaste [Name]! 🎉

Your Bighi Brothers order #[ORDER_ID] is confirmed!

📦 What's Coming:
[Product List]

We ship within 2-3 business days. You'll get tracking info via WhatsApp when it's dispatched.

Questions? Just reply here! 🙏
```

#### Shipping Update
```
Hi [Name]! 📦

Your order #[ORDER_ID] is on its way!

🚚 Tracking: [TRACKING_LINK]

Estimated delivery: [DATE]

Reply anytime if you have questions! 🙏
```

#### Refill Reminder
```
Hi [Name]! 🌿

Just a gentle reminder — your [PRODUCT] is running low.

Based on your routine, you typically reorder every [TIMEFRAME].

Need a refill? Just tap: [SHOP_LINK]

Have questions? Reply here! 🙏
```

### How to Send WhatsApp Messages

1. Click the phone number in the order details
2. Open WhatsApp Web or app
3. Paste the template
4. Personalize with customer details
5. Send

---

## 7. Inventory Management

### Stock Levels

| Level | Meaning | Action |
|-------|---------|--------|
| High | 20+ items | No action needed |
| Medium | 10-19 items | Monitor |
| Low | 5-9 items | Reorder soon |
| Critical | 1-4 items | Reorder immediately |
| Out | 0 items | Urgent reorder + disable product |

### Low Stock Alerts

The admin panel shows items below threshold (default: 10 units).

To update stock:
1. Find the product in [`shop/category.html`](../shop/category.html)
2. Find the stock indicator or data attribute
3. Update the number

### Temporarily Hiding Out-of-Stock Products

Add `style="display:none;"` to hide without deleting:

```html
<div class="product-card" style="display:none;">
  <!-- Product content -->
</div>
```

---

## Checklist: Before Publishing Changes

- [ ] Tested all links
- [ ] Checked images load correctly
- [ ] Verified prices are accurate
- [ ] Read through content for typos
- [ ] Checked mobile view
- [ ] Asked someone else to review
- [ ] Backed up original files

---

## Emergency Rollback

If something goes wrong:

1. If using Git: `git checkout HEAD -- filename.html`
2. If not using Git: Restore from your backup copy
3. If everything fails: Contact senior developer

---

## Getting Help

| Issue | Who to Ask |
|-------|------------|
| Code not working | Tech Team Lead |
| Product information wrong | Product Manager |
| Pricing/discounts | Business Owner |
| Design questions | Creative Lead |
| Customer complaints | Customer Support Lead |

---

*Last Updated: March 2026 | Version 1.0*
