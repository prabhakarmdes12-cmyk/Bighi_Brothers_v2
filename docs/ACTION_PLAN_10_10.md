# Bighi Brothers — Complete Action Plan to Achieve 10/10 Score

> **From:** Current 5.8/10  
> **To:** Target 10/10  
> **Timeline:** 4-6 Weeks  
> **Owner:** Product Manager + Tech Lead

---

## PHASE 1: FOUNDATION FIXES (Week 1)
**Goal:** Fix critical navigation and flow conflicts  
**Impact Score:** +1.5 points (5.8 → 7.3)

---

### 1.1 CONSOLIDATE SHOPPING FLOWS
**Priority:** P0 | **Effort:** 4 hours | **Owner:** Frontend Dev

#### Task: Update All Navigation Links in `index.html`

**Find and Replace (10 locations):**

| Line ~ | Current | Replace With |
|--------|---------|--------------|
| 1505 | `onclick="window.location.href='bighi_shop_pages.html'"` | `onclick="openCart()"` |
| 1509 | `href="bighi_shop_pages.html"` | `href="shop/category.html"` |
| 1519 | `href="bighi_shop_pages.html"` | `href="shop/category.html"` |
| 1526 | `href="bighi_shop_pages.html"` | `href="shop/category.html"` |
| 1602 | `onclick="window.location.href='bighi_shop_pages.html?product=marigold'"` | `onclick="window.location.href='shop/product.html?id=marigold'"` |
| 1778 | `href="bighi_shop_pages.html?filter=soap"` | `href="shop/category.html?filter=soap"` |
| 1793 | `href="bighi_shop_pages.html?filter=cream"` | `href="shop/category.html?filter=cream"` |
| 1808 | `href="bighi_shop_pages.html?filter=lip"` | `href="shop/category.html?filter=lip"` |
| 1829 | `href="bighi_shop_pages.html"` | `href="shop/category.html"` |
| 1838 | `href="bighi_shop_pages.html?product=marigold"` | `href="shop/product.html?id=marigold"` |
| 1869 | `href="bighi_shop_pages.html?product=coffee"` | `href="shop/product.html?id=coffee'"` |
| 1897 | `href="bighi_shop_pages.html?product=peach-lip"` | `href="shop/product.html?id=peach-lip'"` |
| 1925 | `href="bighi_shop_pages.html?product=rose"` | `href="shop/product.html?id=rose'"` |
| 2043 | `href="bighi_shop_pages.html"` | `href="shop/category.html"` |

#### Task: Deprecate Legacy Page
**Option A:** Delete `bighi_shop_pages.html`  
**Option B:** Add redirect to `shop/category.html`:
```html
<!-- Add to top of bighi_shop_pages.html -->
<script>window.location.href = 'shop/category.html';</script>
```

**Acceptance Criteria:**
- [ ] All links tested and working
- [ ] No references to `bighi_shop_pages.html` remain
- [ ] Mobile nav also updated

---

### 1.2 IMPLEMENT CART SYSTEM
**Priority:** P0 | **Effort:** 16 hours | **Owner:** Frontend Dev

#### 1.2.1 Create Cart State Management

Create new file: `shop/cart.js`
```javascript
// Cart State
const Cart = {
  items: [],
  
  // Add item to cart
  add(product) {
    const existing = this.items.find(i => i.id === product.id);
    if (existing) {
      existing.qty += 1;
    } else {
      this.items.push({...product, qty: 1});
    }
    this.save();
    this.updateUI();
  },
  
  // Remove item
  remove(id) {
    this.items = this.items.filter(i => i.id !== id);
    this.save();
    this.updateUI();
  },
  
  // Update quantity
  updateQty(id, qty) {
    const item = this.items.find(i => i.id === id);
    if (item) item.qty = qty;
    this.save();
    this.updateUI();
  },
  
  // Calculate totals
  getTotal() {
    return this.items.reduce((sum, i) => sum + (i.price * i.qty), 0);
  },
  
  // Get item count
  getCount() {
    return this.items.reduce((sum, i) => sum + i.qty, 0);
  },
  
  // Save to localStorage
  save() {
    localStorage.setItem('bighi_cart', JSON.stringify(this.items));
  },
  
  // Load from localStorage
  load() {
    const saved = localStorage.getItem('bighi_cart');
    if (saved) this.items = JSON.parse(saved);
    this.updateUI();
  },
  
  // Update cart badge and drawer
  updateUI() {
    const count = this.getCount();
    const badge = document.querySelector('.nav-cart-badge');
    if (badge) {
      badge.textContent = count;
      badge.classList.toggle('show', count > 0);
    }
  }
};

// Initialize
document.addEventListener('DOMContentLoaded', () => Cart.load());
```

#### 1.2.2 Create Cart Drawer Component

Add to all shop pages and index.html:

```html
<!-- Cart Drawer -->
<div id="cart-drawer" class="cart-drawer">
  <div class="cart-drawer-header">
    <h3>Your Ritual</h3>
    <button onclick="closeCart()" class="cart-close">×</button>
  </div>
  
  <div id="cart-items" class="cart-items">
    <!-- Items injected here -->
  </div>
  
  <div class="cart-drawer-footer">
    <div class="cart-subtotal">
      <span>Subtotal</span>
      <span id="cart-total">₹0</span>
    </div>
    <p class="cart-note">Shipping calculated at checkout</p>
    <button class="btn-cart-checkout" onclick="window.location.href='shop/checkout.html'">
      Checkout →
    </button>
    <button class="btn-cart-continue" onclick="closeCart()">
      Continue Shopping
    </button>
  </div>
</div>

<div id="cart-overlay" class="cart-overlay" onclick="closeCart()"></div>
```

#### 1.2.3 Cart Drawer CSS

```css
/* Cart Drawer */
.cart-drawer {
  position: fixed;
  top: 0;
  right: 0;
  width: 420px;
  max-width: 100%;
  height: 100vh;
  background: var(--cream);
  z-index: 1000;
  transform: translateX(100%);
  transition: transform 0.4s var(--ease);
  display: flex;
  flex-direction: column;
}

.cart-drawer.open {
  transform: translateX(0);
}

.cart-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.5);
  z-index: 999;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s;
}

.cart-overlay.open {
  opacity: 1;
  visibility: visible;
}

.cart-drawer-header {
  padding: 24px;
  border-bottom: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.cart-drawer-header h3 {
  font-family: 'Playfair Display', serif;
  font-size: 1.4rem;
  color: var(--forest);
}

.cart-close {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: var(--forest);
}

.cart-items {
  flex: 1;
  overflow-y: auto;
  padding: 20px;
}

.cart-item {
  display: flex;
  gap: 16px;
  padding: 16px 0;
  border-bottom: 1px solid var(--border);
}

.cart-item-img {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 2px;
}

.cart-item-info {
  flex: 1;
}

.cart-item-name {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1rem;
  color: var(--forest);
  margin-bottom: 4px;
}

.cart-item-price {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  color: var(--amber);
}

.cart-item-qty {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-top: 8px;
}

.cart-item-qty button {
  width: 28px;
  height: 28px;
  border: 1px solid var(--border);
  background: none;
  cursor: pointer;
  font-family: 'DM Mono', monospace;
}

.cart-item-remove {
  color: var(--warm);
  font-size: 0.75rem;
  text-decoration: underline;
  cursor: pointer;
}

.cart-drawer-footer {
  padding: 24px;
  border-top: 1px solid var(--border);
}

.cart-subtotal {
  display: flex;
  justify-content: space-between;
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  margin-bottom: 8px;
}

.cart-note {
  font-size: 0.8rem;
  color: var(--warm);
  margin-bottom: 16px;
}

.btn-cart-checkout {
  width: 100%;
  background: var(--amber);
  color: white;
  border: none;
  padding: 16px;
  font-family: 'Cormorant Garamond', serif;
  font-size: 0.9rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  cursor: pointer;
  margin-bottom: 8px;
}

.btn-cart-continue {
  width: 100%;
  background: none;
  border: 1px solid var(--border);
  padding: 16px;
  font-family: 'Cormorant Garamond', serif;
  font-size: 0.9rem;
  cursor: pointer;
}
```

#### 1.2.4 Make "Add to Cart" Buttons Work

Update in `shop/category.html`:
```javascript
// Replace existing quick-add buttons with:
<button class="quick-add-btn" onclick="Cart.add({
  id: 'marigold-soap',
  name: 'Marigold Mountain Soap',
  price: 50,
  image: 'IMAGE_URL'
}); openCart();">
  + Add
</button>
```

Update in `shop/product.html`:
```javascript
// Add to main CTA:
<button class="btn-atc" onclick="Cart.add({
  id: document.querySelector('.variant-select').value,
  name: document.querySelector('.product-title').textContent,
  price: parseInt(document.querySelector('.product-price').textContent.replace('₹', '')),
  image: document.getElementById('mainImage').src
}); openCart();">
  Add to Ritual — ₹<span id="atc-price">50</span>
</button>
```

**Acceptance Criteria:**
- [ ] Cart drawer opens from cart button
- [ ] Products can be added to cart
- [ ] Quantities can be adjusted
- [ ] Cart persists across page reloads
- [ ] Cart shows correct totals

---

## PHASE 2: E-COMMERCE ENHANCEMENTS (Week 2)
**Goal:** Add missing e-commerce features  
**Impact Score:** +1.0 points (7.3 → 8.3)

---

### 2.1 IMPLEMENT REAL PRODUCT DATA
**Priority:** P1 | **Effort:** 8 hours | **Owner:** Content + Dev

#### Task: Create Product Database

Create `shop/products.json`:
```json
{
  "products": [
    {
      "id": "marigold-mountain-soap",
      "name": "Marigold Mountain Soap",
      "tagline": "Handmade with mountain herbs",
      "category": "soap",
      "price": 50,
      "comparePrice": null,
      "variants": [
        {"id": "marigold-90g", "size": "90g", "price": 50},
        {"id": "marigold-150g", "size": "150g", "price": 80}
      ],
      "images": [
        "https://images.unsplash.com/photo-1607006344380-b6775a0824a7?w=800",
        "https://images.unsplash.com/photo-1570194065650-d99fb4b38b15?w=800"
      ],
      "description": "A cold-process bar...",
      "ingredients": ["Marigold extract", "Coconut oil", "Neem powder"],
      "howToUse": "Wet skin, lather...",
      "stock": 45,
      "badge": "Bestseller"
    }
  ]
}
```

#### Task: Load Products Dynamically

Update `shop/category.html` to fetch from JSON:
```javascript
async function loadProducts() {
  const response = await fetch('products.json');
  const data = await response.json();
  renderProducts(data.products);
}

function renderProducts(products) {
  const grid = document.querySelector('.product-grid');
  grid.innerHTML = products.map(p => `
    <div class="product-card">
      <a href="product.html?id=${p.id}">
        <img src="${p.images[0]}" alt="${p.name}">
      </a>
      <div class="product-info">
        <h3>${p.name}</h3>
        <p>${p.tagline}</p>
        <div class="product-footer">
          <span class="price">₹${p.price}</span>
          <button onclick="quickAdd('${p.id}')">+ Add</button>
        </div>
      </div>
    </div>
  `).join('');
}
```

---

### 2.2 ADD PRODUCT REVIEWS
**Priority:** P1 | **Effort:** 6 hours | **Owner:** Frontend Dev

Add to `shop/product.html`:
```html
<section class="reviews-section">
  <h3>Customer Rituals</h3>
  
  <div class="review-summary">
    <div class="review-stars">★★★★★</div>
    <div class="review-count">4.8 out of 5 (124 reviews)</div>
  </div>
  
  <div class="review-list">
    <!-- Review cards -->
    <div class="review-card">
      <div class="review-header">
        <span class="reviewer-name">Priya S.</span>
        <span class="review-date">Verified Buyer</span>
        <div class="review-stars">★★★★★</div>
      </div>
      <p class="review-text">"This soap has transformed my morning ritual..."</p>
      <div class="review-product">Marigold Mountain Soap — 90g</div>
    </div>
  </div>
  
  <button class="btn-load-more">Load More Reviews</button>
</section>
```

---

### 2.3 IMPLEMENT ANALYTICS
**Priority:** P1 | **Effort:** 4 hours | **Owner:** Dev + Marketing

Add Google Analytics 4 to all pages:
```html
<!-- Add to <head> of all pages -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

Add e-commerce events:
```javascript
// Track add to cart
gtag('event', 'add_to_cart', {
  currency: 'INR',
  value: product.price,
  items: [{
    item_id: product.id,
    item_name: product.name,
    price: product.price
  }]
});

// Track purchase (on order-success.html)
gtag('event', 'purchase', {
  transaction_id: 'BB-2026-XXXX',
  value: 270,
  currency: 'INR',
  items: cart.items
});
```

---

## PHASE 3: UX POLISH (Week 3)
**Goal:** Fix design inconsistencies and accessibility  
**Impact Score:** +0.8 points (8.3 → 9.1)

---

### 3.1 STANDARDIZE DESIGN SYSTEM
**Priority:** P2 | **Effort:** 8 hours | **Owner:** UI Designer + Frontend Dev

Create `assets/styles/global.css`:
```css
/* Universal Design Tokens */
:root {
  /* Colors */
  --bb-cream: #F5EFE0;
  --bb-forest: #1C3A2E;
  --bb-forest-dark: #162D24;
  --bb-amber: #C8831A;
  --bb-amber-light: #E8A830;
  
  /* Spacing Scale */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 48px;
  
  /* Border Radius */
  --radius-sm: 2px;
  --radius-md: 4px;
  --radius-lg: 8px;
  
  /* Shadows */
  --shadow-sm: 0 2px 8px rgba(0,0,0,0.06);
  --shadow-md: 0 4px 16px rgba(0,0,0,0.1);
  --shadow-lg: 0 8px 32px rgba(0,0,0,0.12);
  
  /* Transitions */
  --transition-fast: 0.2s ease;
  --transition-base: 0.3s ease;
  --transition-slow: 0.5s ease;
}

/* Universal Button Styles */
.bb-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 24px;
  border-radius: var(--radius-sm);
  font-family: 'Cormorant Garamond', serif;
  font-size: 0.85rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  cursor: pointer;
  transition: all var(--transition-base);
}

.bb-btn-primary {
  background: var(--bb-amber);
  color: white;
  border: none;
}

.bb-btn-primary:hover {
  background: var(--bb-forest);
}

.bb-btn-secondary {
  background: transparent;
  color: var(--bb-forest);
  border: 1px solid var(--bb-forest);
}
```

Update all pages to use these tokens.

---

### 3.2 ACCESSIBILITY IMPROVEMENTS
**Priority:** P2 | **Effort:** 6 hours | **Owner:** Frontend Dev

#### 3.2.1 Add Skip Links
```html
<!-- Add as first element in <body> -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Add to main content area -->
<main id="main-content">
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: var(--forest);
  color: var(--cream);
  padding: 8px 16px;
  z-index: 10000;
  transition: top 0.3s;
}

.skip-link:focus {
  top: 0;
}
```

#### 3.2.2 Fix Form Labels
```html
<!-- Before -->
<input type="email" class="form-input" placeholder="Email">

<!-- After -->
<label for="email" class="form-label">Email Address</label>
<input type="email" id="email" class="form-input" aria-required="true">
```

#### 3.2.3 Add Focus Indicators
```css
/* Remove default outline only if providing alternative */
a:focus-visible,
button:focus-visible {
  outline: 2px solid var(--amber);
  outline-offset: 2px;
}
```

#### 3.2.4 Color Contrast Fixes
```css
/* Ensure text meets WCAG AA (4.5:1 ratio) */
.text-secondary {
  color: #6B6B6B; /* Instead of lighter gray */
}
```

---

### 3.3 MOBILE OPTIMIZATIONS
**Priority:** P2 | **Effort:** 6 hours | **Owner:** Frontend Dev

#### 3.3.1 Add Mobile Admin Toggle
Update `admin/index.html`:
```html
<button class="mobile-menu-toggle" onclick="toggleSidebar()">
  ☰
</button>

<script>
function toggleSidebar() {
  document.querySelector('.sidebar').classList.toggle('mobile-open');
}
</script>
```

```css
@media (max-width: 768px) {
  .sidebar {
    position: fixed;
    left: -240px;
    transition: left 0.3s;
  }
  
  .sidebar.mobile-open {
    left: 0;
  }
}
```

#### 3.3.2 Product Gallery Swipe
Add to `shop/product.html`:
```javascript
// Swipe support for mobile
let touchStartX = 0;
let touchEndX = 0;

const gallery = document.querySelector('.product-gallery');

gallery.addEventListener('touchstart', e => {
  touchStartX = e.changedTouches[0].screenX;
});

gallery.addEventListener('touchend', e => {
  touchEndX = e.changedTouches[0].screenX;
  handleSwipe();
});

function handleSwipe() {
  if (touchEndX < touchStartX - 50) nextImage();
  if (touchEndX > touchStartX + 50) prevImage();
}
```

---

## PHASE 4: ADVANCED FEATURES (Week 4)
**Goal:** Add competitive differentiators  
**Impact Score:** +0.6 points (9.1 → 9.7)

---

### 4.1 WISHLIST FUNCTIONALITY
**Priority:** P2 | **Effort:** 6 hours | **Owner:** Frontend Dev

Add heart icon to product cards:
```html
<button class="wishlist-btn" onclick="toggleWishlist('${p.id}')">
  <span class="heart">♡</span>
</button>
```

```javascript
const Wishlist = {
  items: [],
  
  toggle(id) {
    const index = this.items.indexOf(id);
    if (index > -1) {
      this.items.splice(index, 1);
    } else {
      this.items.push(id);
    }
    this.save();
    this.updateUI();
  },
  
  save() {
    localStorage.setItem('bighi_wishlist', JSON.stringify(this.items));
  },
  
  load() {
    const saved = localStorage.getItem('bighi_wishlist');
    if (saved) this.items = JSON.parse(saved);
  }
};
```

---

### 4.2 INTERACTIVE ROUTINE BUILDER
**Priority:** P3 | **Effort:** 12 hours | **Owner:** Frontend Dev

Create `shop/routine-builder.html`:
```html
<div class="routine-builder">
  <div class="routine-steps">
    <div class="step" data-step="1">
      <h3>1. Cleanse</h3>
      <div class="product-selector">
        <!-- Soap products -->
      </div>
    </div>
    <div class="step" data-step="2">
      <h3>2. Treat</h3>
      <div class="product-selector">
        <!-- Serum/scrub products -->
      </div>
    </div>
    <div class="step" data-step="3">
      <h3>3. Moisturize</h3>
      <div class="product-selector">
        <!-- Cream/lip products -->
      </div>
    </div>
  </div>
  
  <div class="routine-summary">
    <h4>Your Ritual</h4>
    <div id="selected-products"></div>
    <div class="routine-total">
      Total: ₹<span id="routine-total">0</span>
    </div>
    <button onclick="addRoutineToCart()">Add Ritual to Cart</button>
  </div>
</div>
```

---

### 4.3 SUBSCRIPTION OPTIONS
**Priority:** P3 | **Effort:** 8 hours | **Owner:** Dev + PM

Add to product pages:
```html
<div class="purchase-options">
  <label class="option">
    <input type="radio" name="purchase-type" value="one-time" checked>
    <span>One-time purchase — ₹50</span>
  </label>
  <label class="option">
    <input type="radio" name="purchase-type" value="subscription">
    <span>Subscribe & Save 15% — ₹42.50</span>
    <small>Delivered every 30 days. Cancel anytime.</small>
  </label>
</div>
```

---

## PHASE 5: OPTIMIZATION (Week 5-6)
**Goal:** Performance and final polish  
**Impact Score:** +0.3 points (9.7 → 10.0)

---

### 5.1 PERFORMANCE OPTIMIZATION
**Priority:** P2 | **Effort:** 8 hours | **Owner:** Frontend Dev

#### 5.1.1 Image Optimization
```html
<!-- Use responsive images -->
<img 
  src="image-400w.jpg"
  srcset="image-400w.jpg 400w, image-800w.jpg 800w, image-1200w.jpg 1200w"
  sizes="(max-width: 600px) 400px, (max-width: 1200px) 800px, 1200px"
  alt="Product"
  loading="lazy"
>
```

#### 5.1.2 Lazy Loading
```javascript
// Lazy load images
const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;
      img.classList.remove('lazy');
      observer.unobserve(img);
    }
  });
});

document.querySelectorAll('img.lazy').forEach(img => {
  imageObserver.observe(img);
});
```

#### 5.1.3 Minification
- Minify CSS and JavaScript for production
- Enable Gzip/Brotli compression on server

---

### 5.2 SEO OPTIMIZATION
**Priority:** P2 | **Effort:** 4 hours | **Owner:** SEO Specialist

Update all pages with:
```html
<!-- Meta tags -->
<title>Marigold Mountain Soap — Handmade Natural Skincare | Bighi Brothers</title>
<meta name="description" content="Experience the ritual of handmade Marigold Mountain Soap. Cold-processed with natural ingredients. Free shipping on orders over ₹500.">

<!-- Open Graph -->
<meta property="og:title" content="Marigold Mountain Soap">
<meta property="og:description" content="Handmade natural skincare">
<meta property="og:image" content="https://bighibrothers.com/images/soap.jpg">

<!-- Structured Data -->
<script type="application/ld+json">
{
  "@context": "https://schema.org/",
  "@type": "Product",
  "name": "Marigold Mountain Soap",
  "image": "https://bighibrothers.com/images/soap.jpg",
  "description": "Handmade natural soap",
  "brand": {
    "@type": "Brand",
    "name": "Bighi Brothers"
  },
  "offers": {
    "@type": "Offer",
    "price": "50.00",
    "priceCurrency": "INR"
  }
}
</script>
```

---

### 5.3 TESTING & QA
**Priority:** P0 | **Effort:** 12 hours | **Owner:** QA Team

#### Test Checklist:
- [ ] All navigation links work
- [ ] Cart functionality (add, remove, update qty)
- [ ] Checkout flow (all 4 steps)
- [ ] Form validation
- [ ] Mobile responsiveness (iOS + Android)
- [ ] Cross-browser testing (Chrome, Safari, Firefox)
- [ ] Accessibility audit (axe or Lighthouse)
- [ ] Performance audit (Lighthouse score >90)
- [ ] Analytics events firing correctly

---

## SUCCESS METRICS

### Quantitative KPIs:
| Metric | Current | Target (3 months) |
|--------|---------|-------------------|
| Bounce Rate | Unknown | <40% |
| Add to Cart Rate | 0% | >8% |
| Checkout Completion | N/A | >60% |
| Page Load Time | Unknown | <3s |
| Mobile Conversion | N/A | >50% of total |

### Qualitative Goals:
- [ ] Users can complete purchase in <5 minutes
- [ ] Cart drawer feels "premium" (matches brand)
- [ ] Mobile experience is "frictionless"
- [ ] Admin panel is "intuitive" for shopkeepers

---

## RESOURCE REQUIREMENTS

| Role | Hours | Cost Estimate |
|------|-------|---------------|
| Frontend Developer | 80 | ₹80,000 |
| UI Designer | 20 | ₹30,000 |
| QA Tester | 20 | ₹20,000 |
| SEO Specialist | 10 | ₹15,000 |
| **TOTAL** | **130** | **₹1,45,000** |

---

## TIMELINE SUMMARY

```
Week 1:  ████████░░░░░░░░░░░░  Foundation Fixes (+1.5 pts)
Week 2:  ░░████████░░░░░░░░░░  E-Commerce (+1.0 pt)
Week 3:  ░░░░████████░░░░░░░░  UX Polish (+0.8 pt)
Week 4:  ░░░░░░████████░░░░░░  Advanced Features (+0.6 pt)
Week 5-6: ░░░░░░░░████████████  Optimization (+0.3 pt)

Total: 6 Weeks to 10/10
```

---

## RISK MITIGATION

| Risk | Impact | Mitigation |
|------|--------|------------|
| Scope creep | High | Strict P0/P1/P2 prioritization |
| Technical debt | Medium | Code review every PR |
| Timeline slip | Medium | Weekly standups, buffer in schedule |
| Performance issues | Medium | Test on real devices, not just emulators |

---

*Plan Version: 1.0*  
*Target Score: 10/10*  
*Estimated Timeline: 6 Weeks*  
*Investment: ₹1,45,000*
