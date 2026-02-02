# Custom Mega Menu Implementation Guide

## 📋 Overview
This custom mega menu system allows you to create rich, multi-column navigation menus with nested subcategories directly in your codebase, without relying on Shopify admin blocks.

## 🎯 Features
- ✅ Hardcoded mega menu configuration
- ✅ Support for nested subcategories (3 levels deep)
- ✅ Promotional images per category
- ✅ Fully customizable via code
- ✅ Responsive design
- ✅ Hover animations
- ✅ SEO-friendly structure

## 📁 Files Created/Modified

### New Files:
1. **`snippets/custom-mega-menu.liquid`** - Main mega menu logic
2. **`snippets/desktop-menu-standard.liquid`** - Standard dropdown fallback
3. **`assets/custom-mega-menu.css`** - Mega menu styles
4. **`MEGA-MENU-GUIDE.md`** - This documentation

### Modified Files:
1. **`snippets/desktop-menu.liquid`** - Updated to use custom mega menu system

## 🚀 How to Use

### Step 1: Define Which Menu Items Should Be Mega Menus

Edit `snippets/desktop-menu.liquid` (line ~24):

```liquid
{%- assign mega_menu_items = 'lighting,furniture,brands,home improvement' | split: ',' -%}
```

**Add or remove menu items** from this list. Menu item names must match exactly (case-insensitive).

### Step 2: Create Your Menu Structure in Shopify Admin

1. Go to **Shopify Admin** → **Online Store** → **Navigation**
2. Edit your **main-menu**
3. Create a structure like this:

```
Lighting
├─ Indoor Lighting
│  ├─ Downlights
│  ├─ Panel Lights
│  ├─ Spotlights
│  └─ Track Lights
├─ Outdoor Lighting
│  ├─ Wall Lights
│  ├─ Bollard Lights
│  └─ Flood Lights
└─ Decorative Lighting
   ├─ Chandeliers
   ├─ Pendant Lights
   └─ Table Lamps
```

### Step 3: Configure Promotional Images (Optional)

Edit `snippets/custom-mega-menu.liquid` (around line 75):

```liquid
{%- case downcase_title -%}
  {%- when 'lighting' -%}
    {%- assign promo_image_1 = 'your-lighting-promo-1.jpg' -%}
    {%- assign promo_heading_1 = 'Featured Lighting' -%}
    {%- assign promo_text_1 = 'Discover our latest collection' -%}
    {%- assign promo_link_1 = '/collections/featured-lighting' -%}
    
  {%- when 'furniture' -%}
    {%- assign promo_image_1 = 'your-furniture-promo-1.jpg' -%}
    {%- assign promo_heading_1 = 'Premium Furniture' -%}
    {%- assign promo_text_1 = 'Comfort meets style' -%}
    {%- assign promo_link_1 = '/collections/premium-furniture' -%}
{%- endcase -%}
```

**To add promotional images:**
1. Upload images to Shopify Files
2. Replace `'your-lighting-promo-1.jpg'` with your actual image filename
3. Update heading, text, and link

### Step 4: Include Custom CSS

Add this line to your `layout/theme.liquid` file (after the main theme.css):

```liquid
<link rel="stylesheet" href="{{ 'custom-mega-menu.css' | asset_url }}">
```

Or copy the CSS from `assets/custom-mega-menu.css` and paste it into your `assets/theme.css` file.

## 📖 Example Menu Structures

### Example 1: Lighting Category
```
Lighting (Mega Menu)
├─ Indoor Lighting
│  ├─ Downlights (3W, 5W, 7.5W, 10W)
│  ├─ Panel Lights
│  ├─ Spotlights
│  └─ Track Lights
├─ Outdoor Lighting
│  ├─ Wall Lights
│  ├─ Bollard Lights
│  └─ Flood Lights
└─ Decorative Lighting
   ├─ Chandeliers
   ├─ Pendant Lights
   └─ Table Lamps
```

### Example 2: Brands Category
```
Brands (Mega Menu)
├─ Panasonic
│  ├─ Water Heaters
│  ├─ Ceiling Fans
│  └─ Ventilation
├─ Dunlopillo
│  ├─ Mattresses
│  └─ Bed Frames
├─ Endo
│  ├─ Downlights
│  └─ Track Lights
└─ Sigma
   ├─ Magnetic Track
   └─ Smart Lighting
```

## 🎨 Customization Options

### Change Mega Menu Items List
Edit the list in both files:
- `snippets/desktop-menu.liquid` (line ~24)
- `snippets/custom-mega-menu.liquid` (line ~19)

### Adjust Column Width
Edit `assets/custom-mega-menu.css`:

```css
.mega-menu__column {
  min-width: 250px; /* Change from 200px */
}
```

### Change Nested Item Indicator
Edit `assets/custom-mega-menu.css`:

```css
.mega-menu__nested-link:before {
  content: "•"; /* Change from "›" */
}
```

### Add More Promotional Images
Edit `snippets/custom-mega-menu.liquid` and add after line 100:

```liquid
{%- if promo_image_2 and promo_image_2 != '' -%}
  <a href="{{ promo_link_2 | default: '#' }}" class="mega-menu__promo">
    <div class="mega-menu__image-wrapper">
      <div class="aspect-ratio" style="padding-bottom: 66.67%">
        <img class="lazyload image--fade-in" data-src="{{ promo_image_2 | img_url: '550x' }}" alt="{{ promo_heading_2 | escape }}">
      </div>
    </div>
    <span class="mega-menu__image-heading heading h4">{{ promo_heading_2 | escape }}</span>
    <p class="mega-menu__image-text">{{ promo_text_2 | escape }}</p>
  </a>
{%- endif -%}
```

## 🔧 Troubleshooting

### Mega Menu Not Showing
1. Check that the menu item name in `mega_menu_items` matches exactly
2. Verify your navigation layout is set to "inline" (not "condensed")
3. Clear your browser cache

### Nested Items Not Displaying
1. Ensure your menu structure in Shopify has 3 levels
2. Check that the parent menu item is in the `mega_menu_items` list

### Promotional Images Not Loading
1. Verify the image filename is correct
2. Check that the image is uploaded to Shopify Files
3. Use the full Shopify image path: `shopify://shop_images/your-image.jpg`

### Styling Issues
1. Ensure `custom-mega-menu.css` is loaded after `theme.css`
2. Check browser console for CSS errors
3. Clear Shopify theme cache

## 📱 Mobile Support

The mega menu automatically converts to a standard mobile menu on small screens. The mobile menu is handled by `snippets/mobile-menu.liquid` and supports:
- Collapsible sections
- Nested navigation
- Promotional images (in a scrollable carousel)

## 🎯 Best Practices

1. **Keep menu depth to 3 levels max** for better UX
2. **Use descriptive menu item names** for better SEO
3. **Optimize promotional images** (recommended: 550x367px)
4. **Test on mobile devices** to ensure responsive behavior
5. **Use consistent naming** across all menu items

## 🔄 Reverting to Original

If you want to revert to the original Shopify admin-based mega menu system:

1. Restore the original `snippets/desktop-menu.liquid` from your backup
2. Remove the custom CSS from your theme
3. Configure mega menus via Shopify Theme Editor → Header section

## 📞 Support

For questions or issues:
- Check this documentation first
- Review the code comments in each file
- Test in Shopify preview mode before publishing

## 🎉 Quick Start Example

Here's a complete example for a "Lighting" mega menu:

**1. Add to mega_menu_items:**
```liquid
{%- assign mega_menu_items = 'lighting' | split: ',' -%}
```

**2. Create menu in Shopify:**
```
Lighting
├─ Indoor
│  ├─ Downlights
│  └─ Panel Lights
└─ Outdoor
   └─ Wall Lights
```

**3. Add promo image:**
```liquid
{%- when 'lighting' -%}
  {%- assign promo_image_1 = 'shopify://shop_images/lighting-promo.jpg' -%}
  {%- assign promo_heading_1 = 'New Collection' -%}
  {%- assign promo_text_1 = 'Check out our latest lighting' -%}
  {%- assign promo_link_1 = '/collections/new-lighting' -%}
```

**4. Save and test!**

---

**Version:** 1.0  
**Last Updated:** February 2, 2026  
**Compatible with:** Warehouse Theme v2.5.3
