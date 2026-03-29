# Bighi Brothers — Complete User Flow Documentation

## Overview

This document maps every user flow in the Bighi Brothers website, identifying the intended flows, actual flows, and conflicts between them.

---

## 1. VISITOR DISCOVERY FLOWS

### Flow 1.1: Organic Discovery → Homepage

```
┌────────────────────────────────────────────────────────────────────┐
│  ENTRY POINTS                                                      │
├────────────────────────────────────────────────────────────────────┤
│  • Google Search (SEO)                                             │
│  • Social Media (Instagram, Facebook)                              │
│  • Direct Traffic (Typed URL)                                      │
│  • Referral (Blog mentions)                                        │
└────────────────────────────────────────────────────────────────────┘
                              ↓
                    ┌─────────────────┐
                    │   index.html    │
                    │   (Homepage)    │
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        ↓                    ↓                    ↓
   ┌─────────┐        ┌──────────┐         ┌──────────┐
   │  Shop   │        │  Journal │         │  About   │
   │ Collection     │   (Blog)   │         │  Story   │
   └────┬────┘        └────┬─────┘         └────┬─────┘
        │                  │                    │
        ↓                  ↓                    ↓
   CONVERT           ENGAGE               CONNECT
```

**Key Decision Point at Homepage:**
- Primary CTA: "Begin Ritual" → Shop
- Secondary: Journal → Content engagement
- Tertiary: About → Brand connection

---

## 2. SHOPPING FLOWS (CRITICAL ISSUE IDENTIFIED)

### ⚠️ PROBLEM: Two Competing Shopping Experiences

```
                    ┌─────────────────┐
                    │   index.html    │
                    │   (Homepage)    │
                    └────────┬────────┘
                             │
            ┌────────────────┼────────────────┐
            ↓                ↓                ↓
    ┌───────────────┐ ┌───────────────┐ ┌───────────────┐
    │   Cart Btn    │ │ "Begin Ritual" │ │ Product Cards │
    │   (Header)    │ │    (CTAs)      │ │   (4 cards)   │
    └───────┬───────┘ └───────┬───────┘ └───────┬───────┘
            │                 │                 │
            ↓                 ↓                 ↓
    ┌───────────────┐ ┌───────────────┐ ┌───────────────┐
    │  LEGACY PAGE  │ │  LEGACY PAGE  │ │  LEGACY PAGE  │
    │bighi_shop_    │ │bighi_shop_    │ │bighi_shop_    │
    │pages.html     │ │pages.html     │ │pages.html     │
    └───────────────┘ └───────────────┘ └───────────────┘
            │
            ↓
    ┌─────────────────────────────────────────────┐
    │  ❌ DEAD END: No checkout path              │
    │  ❌ No cart functionality                   │
    │  ❌ No product detail pages                 │
    └─────────────────────────────────────────────┘

    VS

    ┌─────────────────┐
    │   Footer Link   │
    │  "Handmade Soaps"│
    └────────┬────────┘
             ↓
    ┌─────────────────┐
    │  shop/category  │
    │    .html        │
    └────────┬────────┘
             │
    ┌────────┴────────┬────────────────┐
    ↓                 ↓                ↓
┌─────────┐    ┌──────────┐    ┌──────────┐
│ Product │    │  Filter  │    │   Sort   │
│  Card   │    │   Tab    │    │ Dropdown │
└────┬────┘    └────┬─────┘    └────┬─────┘
     │              │               │
     ↓              └───────────────┘
┌─────────┐                         │
│product. │                         │
│html     │◄────────────────────────┘
└────┬────┘
     │
     ↓
┌─────────┐    ┌──────────┐    ┌──────────┐
│  Image  │───→│  Info    │───→│   CTA    │
│ Gallery │    │  Tabs    │    │ Buttons  │
└─────────┘    └──────────┘    └────┬─────┘
                                    │
                    ┌───────────────┼───────────────┐
                    ↓               ↓               ↓
              ┌─────────┐    ┌──────────┐    ┌──────────┐
              │ Add to  │    │ Complete │    │  More    │
              │  Cart   │    │ Routine  │    │  Info    │
              └────┬────┘    └──────────┘    └──────────┘
                   │
                   ↓ (Currently broken)
            ┌───────────────┐
            │  NO CART      │
            │  SYSTEM       │
            └───────────────┘
```

---

## 3. INTENDED SHOPPING FLOW (To Be Fixed)

```
┌─────────────────────────────────────────────────────────────────────┐
│                    IDEAL E-COMMERCE FLOW                            │
└─────────────────────────────────────────────────────────────────────┘

PHASE 1: BROWSE
┌─────────┐     ┌─────────────┐     ┌─────────────┐     ┌───────────┐
│  Entry  │────→│   Category  │────→│   Filter    │────→│   Sort    │
│ Point   │     │    Page     │     │   (Tabs)    │     │ (Options) │
└─────────┘     └─────────────┘     └─────────────┘     └───────────┘
                                              │
                                              ↓
                                       ┌─────────────┐
                                       │ Product Grid │
                                       │   (Cards)    │
                                       └──────┬──────┘
                                              │
PHASE 2: CONSIDER                              ↓
                                       ┌─────────────┐
                                       │ Product Card │
                                       │  - Image     │
                                       │  - Name      │
                                       │  - Price     │
                                       │  - Quick Add │
                                       └──────┬──────┘
                                              │
                        ┌─────────────────────┼─────────────────────┐
                        ↓                     ↓                     ↓
                   ┌─────────┐         ┌──────────┐          ┌──────────┐
                   │  Image  │         │   Info   │          │  Wishlist │
                   │  Hover  │         │  Hover   │          │   (Heart) │
                   └────┬────┘         └────┬─────┘          └──────────┘
                        │                   │
                        └─────────┬─────────┘
                                  ↓
                           ┌─────────────┐
                           │  Click Card  │
                           └──────┬──────┘
                                  ↓
PHASE 3: DECISION
                           ┌─────────────┐
                           │   Product   │
                           │ Detail Page │
                           │   (PDP)     │
                           └──────┬──────┘
                                  │
            ┌─────────────────────┼─────────────────────┐
            ↓                     ↓                     ↓
      ┌───────────┐        ┌───────────┐         ┌───────────┐
      │   Image   │        │  Product  │         │   Tabs    │
      │  Gallery  │        │   Info    │         │ (Details) │
      │  - Zoom   │        │  - Name   │         │           │
      │  - Thumbs │        │  - Price  │         │           │
      └───────────┘        │  - Variants        │         └───────────┘
                           │  - Stock  │                  │
                           └─────┬─────┘                  │
                                 │                        │
                                 ↓                        │
                           ┌───────────┐                  │
                           │  Variant  │                  │
                           │ Selection │                  │
                           │  - Size   │                  │
                           │  - Scent  │                  │
                           └─────┬─────┘                  │
                                 │                        │
                                 ↓                        │
                           ┌───────────┐◄─────────────────┘
                           │  Quantity │
                           │ Selector  │
                           └─────┬─────┘
                                 │
                                 ↓
PHASE 4: CONVERT
                           ┌───────────┐
                           │  ADD TO   │
                           │   CART    │
                           └─────┬─────┘
                                 │
            ┌────────────────────┼────────────────────┐
            ↓                    ↓                    ↓
      ┌───────────┐       ┌───────────┐       ┌───────────┐
      │  Cart     │       │ Continue  │       │ Complete  │
      │  Drawer   │       │ Shopping  │       │  Routine  │
      │  Opens    │       │           │       │           │
      └─────┬─────┘       └───────────┘       └───────────┘
            │
            ↓
      ┌───────────┐
      │  Review   │
      │   Cart    │
      │  - Items  │
      │  - Total  │
      │  - Edit   │
      └─────┬─────┘
            │
            ↓
      ┌───────────┐
      │  PROCEED  │
      │  TO CHECKOUT
      └─────┬─────┘
            │
PHASE 5: PURCHASE
            ↓
      ┌───────────┐
      │  Checkout │
      │   Flow    │
      └─────┬─────┘
            │
    ┌───────┼───────┬───────────┐
    ↓       ↓       ↓           ↓
┌───────┐┌───────┐┌───────┐ ┌───────┐
│Details││Shipping││Payment│ │Confirm│
│  -    ││  -    ││  -    │ │  -    │
│ Name  ││Method ││Method │ │Review │
│ Email ││ Address││ UPI   │ │ Place │
│ Phone ││        ││ Card  │ │ Order │
│Address││        ││  COD  │ │       │
└───┬───┘└───┬───┘└───┬───┘ └───┬───┘
    │        │        │         │
    └────────┴────────┴─────────┘
                              │
                              ↓
                    ┌───────────────┐
                    │  Order Success │
                    │    Page       │
                    └───────┬───────┘
                            │
            ┌───────────────┼───────────────┐
            ↓               ↓               ↓
      ┌───────────┐  ┌───────────┐  ┌───────────┐
      │ WhatsApp  │  │  Order    │  │ Continue  │
      │  Opt-in   │  │  Details  │  │ Shopping  │
      └───────────┘  └───────────┘  └───────────┘
```

---

## 4. ACCOUNT & RETENTION FLOWS

### 4.1 Account Creation Flow

```
┌────────────────────────────────────────────────────────────────┐
│                    ACCOUNT CREATION                            │
└────────────────────────────────────────────────────────────────┘

[Homepage] or [Checkout]
      │
      ↓
┌─────────────────┐
│  shop/account   │
│    .html        │
└────────┬────────┘
         │
    ┌────┴────┐
    ↓         ↓
┌───────┐ ┌───────┐
│ Login │ │Register│
└───┬───┘ └───┬───┘
    │         │
    ↓         ↓
┌─────────────────┐     ┌─────────────────┐
│  Existing User  │     │   New User      │
│  - Email        │     │  - Name         │
│  - Password     │     │  - Email        │
│  - Phone        │     │  - Phone        │
│  - WhatsApp     │     │  - Password     │
│                 │     │  - WhatsApp Opt │
└────────┬────────┘     └────────┬────────┘
         │                       │
         └───────────┬───────────┘
                     ↓
            ┌─────────────────┐
            │  Account Dashboard
            │                 │
            │  - Order History
            │  - Saved Address
            │  - Routine Builder
            │  - Wishlist
            └─────────────────┘
```

### 4.2 Retention Flows

```
┌────────────────────────────────────────────────────────────────┐
│                    CUSTOMER RETENTION                          │
└────────────────────────────────────────────────────────────────┘

POST-PURCHASE ENGAGEMENT:

┌───────────────┐
│ Order Placed  │
└───────┬───────┘
        │
        ↓
┌────────────────────────────────────────┐
│  1. Order Confirmation (Email + WA)   │
│     - Order details                   │
│     - Expected delivery               │
│     - WhatsApp opt-in                 │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  2. Shipping Update (WhatsApp)        │
│     - Tracking link                   │
│     - Carrier info                    │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  3. Delivery Confirmation (WhatsApp)  │
│     - Delivery photo (if available)   │
│     - Review request                  │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  4. Refill Reminder (WhatsApp)        │
│     - Based on product usage rate     │
│     - Personalized timing             │
│     - Direct reorder link             │
└────────────────────────────────────────┘

RE-ENGAGEMENT:

┌────────────────────────────────────────┐
│  5. Win-back Campaign                 │
│     - 30 days inactive: Gentle nudge  │
│     - 60 days inactive: Special offer │
│     - 90 days inactive: We miss you   │
└────────────────────────────────────────┘
```

---

## 5. ADMIN WORKFLOWS

### 5.1 Order Fulfillment Flow

```
┌────────────────────────────────────────────────────────────────┐
│                    ORDER FULFILLMENT                           │
└────────────────────────────────────────────────────────────────┘

[Customer Places Order]
         │
         ↓
┌────────────────────────────────────────┐
│  admin/index.html                      │
│  Dashboard shows new order alert      │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  1. Review Order                      │
│     - Customer details                │
│     - Products ordered                │
│     - Payment status                  │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  2. Update Status: PROCESSING         │
│     - Send WhatsApp notification      │
│     - Pick items from inventory       │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  3. Update Status: SHIPPED            │
│     - Add tracking number             │
│     - Send tracking link (WhatsApp)   │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  4. Update Status: DELIVERED          │
│     - Confirm delivery                │
│     - Schedule refill reminder        │
└────────────────────────────────────────┘
```

### 5.2 Inventory Management Flow

```
┌────────────────────────────────────────────────────────────────┐
│                    INVENTORY MANAGEMENT                        │
└────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────┐
│  Daily Check: Low Stock Alert         │
│  (Admin Dashboard)                    │
└────────────────┬───────────────────────┘
                 │
        ┌────────┴────────┐
        ↓                 ↓
   ┌─────────┐      ┌──────────┐
   │ RESTOCK │      │  UPDATE  │
   │ NEEDED  │      │  STATUS  │
   └────┬────┘      └──────────┘
        │
        ↓
┌────────────────────────────────────────┐
│  1. Check Physical Stock              │
│     - Count items                     │
│     - Update system                   │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  2. Update in Admin Panel             │
│     - Navigate to Inventory           │
│     - Update quantity                 │
│     - Set new low-stock threshold     │
└────────────────┬───────────────────────┘
                 │
                 ↓
┌────────────────────────────────────────┐
│  3. If Out of Stock:                  │
│     - Mark as unavailable             │
│     - Update website                  │
│     - Notify waiting customers        │
└────────────────────────────────────────┘
```

---

## 6. CONFLICTING FLOWS MAP

```
┌─────────────────────────────────────────────────────────────────────┐
│              CURRENT FLOW CONFLICTS (PROBLEMATIC)                   │
└─────────────────────────────────────────────────────────────────────┘

CONFLICT 1: Shopping Entry Points
═══════════════════════════════════

         [index.html]
              │
    ┌─────────┼─────────┬─────────┬─────────┐
    ↓         ↓         ↓         ↓         ↓
  Cart      CTA 1    CTA 2    Product    Footer
  Button   (Hero)   (Ritual)  Cards     (Soaps)
    │         │         │         │         │
    ↓         ↓         ↓         ↓         ↓
   OLD       OLD       OLD       OLD       NEW
    │         │         │         │         │
    └─────────┴─────────┴─────────┘         │
              │                             │
              ↓                             ↓
    ┌─────────────────┐           ┌─────────────────┐
    │  OLD SHOP PAGE  │           │  NEW SHOP PAGE  │
    │  (bighi_shop_   │           │  (shop/category │
    │   pages.html)   │           │   .html)        │
    └─────────────────┘           └─────────────────┘
            ❌                              ✅
         Dead End                      Full Flow

CONFLICT 2: Product Detail Access
═══════════════════════════════════

    [index.html Product Cards]
              │
              ↓
    ┌─────────────────┐
    │  OLD: Links to  │
    │  bighi_shop_    │
    │  pages.html?    │
    │  product=X      │
    └─────────────────┘
            │
            ↓
    ┌─────────────────┐
    │  Page reloads   │
    │  with filter,   │
    │  NOT product    │
    │  detail view    │
    └─────────────────┘
            ❌ WRONG

    VS

    [shop/category.html]
              │
              ↓
    ┌─────────────────┐
    │  NEW: Links to  │
    │  shop/product   │
    │  .html          │
    └─────────────────┘
            │
            ↓
    ┌─────────────────┐
    │  Dedicated      │
    │  product detail │
    │  page with      │
    │  full info      │
    └─────────────────┘
            ✅ CORRECT
```

---

## 7. USER FLOW FIXES REQUIRED

### Priority 1: Consolidate Shopping Flow

```diff
- Remove all links to: bighi_shop_pages.html
+ Update all links to: shop/category.html

Files to update:
  ✓ index.html (10+ locations)
  ⏳ shop/category.html (if any)
  ⏳ journal/index.html (if any)
```

### Priority 2: Implement Cart System

```
MISSING: Cart Drawer/Page

NEEDED:
┌────────────────────────────────────────┐
│  Cart Drawer (Slide from right)       │
│                                       │
│  ┌─────────────────────────────────┐  │
│  │ Item 1                          │  │
│  │ - Image, Name, Qty, Price       │  │
│  │ - Remove button                 │  │
│  └─────────────────────────────────┘  │
│  ┌─────────────────────────────────┐  │
│  │ Item 2                          │  │
│  │ - Image, Name, Qty, Price       │  │
│  │ - Remove button                 │  │
│  └─────────────────────────────────┘  │
│                                       │
│  Subtotal: ₹XXX                       │
│  Shipping: ₹XX                        │
│  ─────────────────                    │
│  Total: ₹XXX                          │
│                                       │
│  [Continue Shopping] [Checkout →]     │
└────────────────────────────────────────┘
```

### Priority 3: Fix Product Links

| Current | Should Be |
|---------|-----------|
| `bighi_shop_pages.html?product=marigold` | `shop/product.html?id=marigold` |
| `bighi_shop_pages.html?filter=soap` | `shop/category.html?filter=soap` |
| `bighi_shop_pages.html` (cart btn) | Cart drawer or `shop/cart.html` |

---

## 8. FLOW METRICS TO TRACK

| Metric | Target | Current Status |
|--------|--------|----------------|
| Homepage → Shop CTR | >15% | Unknown |
| Shop → Product View | >30% | Unknown |
| Product → Add to Cart | >10% | 0% (broken) |
| Cart → Checkout | >40% | N/A |
| Checkout Complete | >60% | N/A |
| Return Visitor Rate | >25% | Unknown |

---

*Document Version: 1.0*  
*Last Updated: March 2026*
