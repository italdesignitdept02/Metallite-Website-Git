# 🚀 QUICK START: Custom Mega Menu Setup

## ✅ What I've Done For You

I've created a **custom mega menu system** that lets you control everything via code!

### Files Created:
1. ✅ `snippets/custom-mega-menu.liquid` - Your custom mega menu
2. ✅ `snippets/desktop-menu-standard.liquid` - Fallback for regular menus
3. ✅ `assets/custom-mega-menu.css` - Styling for mega menus
4. ✅ `MEGA-MENU-GUIDE.md` - Full documentation

### Files Modified:
1. ✅ `snippets/desktop-menu.liquid` - Now uses your custom system

---

## 🎯 3 Simple Steps to Get Started

### STEP 1: Choose Which Menus Are Mega Menus

**Edit:** `snippets/desktop-menu.liquid` (Line 24)

```liquid
{%- assign mega_menu_items = 'lighting,furniture,brands,home improvement' | split: ',' -%}
```

**Change to your menu items:**
```liquid
{%- assign mega_menu_items = 'lighting,furniture,brands' | split: ',' -%}
```

💡 **Tip:** Menu names must match EXACTLY what you have in Shopify Navigation (case doesn't matter)

---

### STEP 2: Create Your Menu in Shopify Admin

1. Go to **Shopify Admin** → **Navigation** → **main-menu**
2. Create your structure with **up to 3 levels**:

**Example for "Lighting":**
```
Lighting
├─ Indoor Lighting
│  ├─ Downlights
│  ├─ Panel Lights
│  └─ Spotlights
├─ Outdoor Lighting
│  ├─ Wall Lights
│  └─ Flood Lights
└─ Decorative Lighting
```

---

### STEP 3: Add the CSS File

**Edit:** `layout/theme.liquid`

Find this line (around line 44):
```liquid
<link rel="stylesheet" href="{{ 'theme.css' | asset_url }}">
```

Add this line RIGHT AFTER it:
```liquid
<link rel="stylesheet" href="{{ 'custom-mega-menu.css' | asset_url }}">
```

**Result:**
```liquid
<link rel="stylesheet" href="{{ 'theme.css' | asset_url }}">
<link rel="stylesheet" href="{{ 'custom-mega-menu.css' | asset_url }}">
```

---

## 🎨 OPTIONAL: Add Promotional Images

**Edit:** `snippets/custom-mega-menu.liquid` (Line 75)

Find this section:
```liquid
{%- case downcase_title -%}
  {%- when 'lighting' -%}
    {%- assign promo_image_1 = 'your-lighting-promo-1.jpg' -%}
```

**Replace with your actual images:**
```liquid
{%- case downcase_title -%}
  {%- when 'lighting' -%}
    {%- assign promo_image_1 = 'shopify://shop_images/lighting-banner.jpg' -%}
    {%- assign promo_heading_1 = 'New LED Collection' -%}
    {%- assign promo_text_1 = 'Energy-efficient lighting solutions' -%}
    {%- assign promo_link_1 = '/collections/new-led-lights' -%}
    
  {%- when 'furniture' -%}
    {%- assign promo_image_1 = 'shopify://shop_images/furniture-banner.jpg' -%}
    {%- assign promo_heading_1 = 'Comfort Collection' -%}
    {%- assign promo_text_1 = 'Premium recliners and sofas' -%}
    {%- assign promo_link_1 = '/collections/premium-furniture' -%}
{%- endcase -%}
```

---

## 📋 Example: Complete Setup for "Lighting"

### 1. Mark as Mega Menu
```liquid
{%- assign mega_menu_items = 'lighting' | split: ',' -%}
```

### 2. Create in Shopify Navigation
```
Lighting
├─ Indoor Lighting
│  ├─ Downlights (3W)
│  ├─ Downlights (5W)
│  ├─ Downlights (7.5W)
│  ├─ Panel Lights
│  └─ Spotlights
├─ Outdoor Lighting
│  ├─ Wall Lights
│  ├─ Bollard Lights
│  └─ Flood Lights
└─ Decorative Lighting
   ├─ Chandeliers
   ├─ Pendant Lights
   └─ Table Lamps
```

### 3. Add Promo Image
```liquid
{%- when 'lighting' -%}
  {%- assign promo_image_1 = 'shopify://shop_images/lighting-promo.jpg' -%}
  {%- assign promo_heading_1 = 'Featured Lighting' -%}
  {%- assign promo_text_1 = 'Brighten your space' -%}
  {%- assign promo_link_1 = '/collections/featured-lighting' -%}
```

---

## 🎯 What Your Mega Menu Will Look Like

```
┌─────────────────────────────────────────────────────────────────┐
│  LIGHTING MEGA MENU                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌─────┐│
│  │ Indoor       │  │ Outdoor      │  │ Decorative   │  │Promo││
│  │ Lighting     │  │ Lighting     │  │ Lighting     │  │Image││
│  │              │  │              │  │              │  │     ││
│  │ › Downlights │  │ › Wall Lights│  │ › Chandeliers│  │     ││
│  │   • 3W       │  │ › Bollards   │  │ › Pendants   │  │     ││
│  │   • 5W       │  │ › Floods     │  │ › Table Lamps│  │     ││
│  │   • 7.5W     │  │              │  │              │  │     ││
│  │ › Panels     │  │              │  │              │  │     ││
│  │ › Spotlights │  │              │  │              │  │     ││
│  └──────────────┘  └──────────────┘  └──────────────┘  └─────┘│
└─────────────────────────────────────────────────────────────────┘
```

---

## ✨ Features You Get

✅ **3-Level Nested Menus** - Main → Sub → Sub-sub categories  
✅ **Promotional Images** - Add featured products/collections  
✅ **Hover Animations** - Smooth, professional transitions  
✅ **Responsive Design** - Works on all devices  
✅ **SEO Friendly** - Proper HTML structure  
✅ **Easy to Update** - Just edit the code!  

---

## 🔍 Testing Your Mega Menu

1. **Save all files**
2. **Upload to Shopify** (if using local development)
3. **Go to your store** and hover over your menu items
4. **Check that:**
   - Mega menu appears for configured items
   - Nested subcategories show with "›" indicator
   - Promotional images display (if configured)
   - Hover effects work smoothly

---

## 🆘 Quick Troubleshooting

**Mega menu not showing?**
- Check menu name matches exactly in `mega_menu_items`
- Verify navigation layout is "inline" (not "condensed")

**Nested items not displaying?**
- Ensure you have 3 levels in Shopify Navigation
- Check that parent item is in `mega_menu_items` list

**CSS not loading?**
- Verify you added the CSS link to `theme.liquid`
- Clear browser cache and Shopify theme cache

---

## 📚 Need More Help?

Check the full documentation: **`MEGA-MENU-GUIDE.md`**

---

**That's it! You're ready to create amazing mega menus! 🎉**
