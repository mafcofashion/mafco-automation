# MAFCO n8n Automation

Automated workflows for MAFCO Fashion using n8n and WooCommerce.

## What's Inside

- **MAFCO PUBLISH WEBHOOK** — Publish variable products with images, colors, sizes, and SEO metadata to WooCommerce via webhook
- Image upload automation to WordPress media library
- Product variant generation with attributes
- Metadata handling (Rank Math SEO fields)

## Prerequisites

- n8n (localhost or cloud)
- WooCommerce store with REST API enabled
- WordPress Basic Authentication credentials
- Node.js 14+ (if running n8n locally)

## Setup

1. **Import workflow**
   - Download `MAFCO_PUBLISH_WEBHOOK___VARIANTS__v2___CLEAN.json`
   - Open n8n → Workflows → Import from file
   - Select the JSON file

2. **Add credentials**
   - WordPress Auth: WP username & application password
   - WooCommerce Auth: Same as WordPress (REST API credentials)

3. **Configure endpoints**
   - Replace `https://api.mafcofashion.com` with your site URL
   - Update category IDs and brand IDs as needed

4. **Test webhook**
   - Webhook path: `/mafco-publish-variants`
   - Test with sample payload (see below)

## Webhook Payload

```json
{
  "article": "ARTICLE001",
  "data": {
    "articleNo": "ZZTEST-001",
    "shortDescription": "Premium school shoes",
    "longDescription": "Durable school footwear",
    "brand": "MAFCO",
    "categories": [15, 20],
    "seoTitle": "Buy School Shoes",
    "metaDescription": "Quality school shoes",
    "focusKeyword": "school shoes"
  },
  "sizes": ["7X12", "8X12"],
  "images": [
    {
      "slot": 1,
      "color": "Black",
      "filename": "shoe-black-1.jpg",
      "base64": "iVBORw0KGgoAAAANS..."
    }
  ]
}
```

## Workflow Flow

```
Webhook → Upload Images → Prepare WC Payload → Check Product Exists
                           ↓
                    ├→ New Product → Build Variations → Create Variations
                    └→ Existing Product → Merge Attributes → Update Product
                           ↓
                        Build Response → Return JSON
```

## Key Features

- **Variant Management** — Auto-generates SKUs from article + color + size
- **Image Handling** — Base64 image upload to WordPress media
- **Duplicate Prevention** — Skips existing variations
- **Error Handling** — Continues on variation errors, reports status
- **Category Support** — Maps brand names to WooCommerce category IDs

## Environment Variables

No env variables needed (all config in n8n credentials UI).

## Support

For MAFCO automation setup, refer to the dashboard integration docs.

---

**Version:** v2  
**Last Updated:** Sept 2026  
**Status:** Production
