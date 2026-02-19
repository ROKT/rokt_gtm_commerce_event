# rokt_gtm_commerce_event

## Project Overview

A Google Tag Manager (GTM) community template that enables partners to track
[mParticle Commerce Events](https://docs.mparticle.com/developers/sdk/web/commerce-tracking/)
via the mParticle by Rokt web SDK. The template is published to the
[Google Community Template Gallery](https://tagmanager.google.com/gallery/#/?page=1)
and allows partners to configure commerce event tracking through GTM instead of
managing the Rokt script directly.

**Resident Expert:** Alex Sapountzis (alex.sapountzis@rokt.com)

## Tech Stack

- **Language:** Sandboxed JavaScript (GTM template sandbox)
- **Platform:** Google Tag Manager (Web container)
- **SDK dependency:** mParticle by Rokt web SDK (must be initialized before this
  tag fires)
- **License:** Apache 2.0

## Architecture

The repo contains a single GTM `.tpl` template file (`template.tpl`) that defines:

1. **Tag metadata** — Display name, categories (Marketing, Analytics,
   Personalization), brand info, and description.
2. **Template parameters** — UI fields partners configure in GTM:
   - Commerce Event Category (Product Action, Impression, Promotion)
   - Product Action Type (AddToCart, RemoveFromCart, Checkout, Purchase, Refund,
     etc.)
   - Product Information (Name, SKU, Price, Quantity, Variant, Category, Brand,
     Position, Coupon Code, Custom Attributes)
   - Transaction Attributes (ID, Revenue, Shipping, Tax — for Purchase, Refund,
     Checkout)
   - Promotion fields (ID, Name, Creative)
   - Impression Location
   - Custom Event Attributes and Flags
3. **Sandboxed JS logic** — Calls `mParticle.eCommerce.*` methods via
   `callInWindow` to create products, log product actions, log promotions, and
   log impressions.
4. **Web permissions** — Declares required GTM sandbox permissions
   (`access_globals`, `logging`, `read_data_layer`) for the mParticle API
   surface used.
5. **Tests** — Inline test scenarios validating `createProduct`,
   `logProductAction`, `logImpression`, `logPromotion`, and `setCurrencyCode`.

### Supported Commerce Events

| Category   | Actions/Details                                                     |
| ---------- | ------------------------------------------------------------------- |
| Product    | AddToCart, RemoveFromCart, Checkout, CheckoutOption, Click,          |
|            | ViewDetail, Purchase, Refund, AddToWishlist, RemoveFromWishlist     |
| Promotion  | PromotionClick (with ID, Name, Creative)                            |
| Impression | Product impression at a specified location                          |

**Limitation:** The current iteration only supports a single product per product
action event.

## Project Structure

```text
.
├── template.tpl      # GTM tag template (parameters, JS logic, permissions, tests)
├── metadata.yaml     # Google template gallery metadata (homepage, docs link, versions)
├── LICENSE           # Apache 2.0
├── README.md         # Project overview and usage instructions
└── .gitignore        # Ignores .DS_Store
```

## Development Guide

### Prerequisites

- Access to a [Google Tag Manager](https://tagmanager.google.com/) account
- The mParticle by Rokt SDK must be initialized on the site before this tag fires

### Local Development

1. Clone this repo.
2. Edit `template.tpl` — this single file contains all tag configuration,
   sandboxed JS logic, permissions, and tests.
3. To test locally, download the `.tpl` file and upload it in your GTM Template
   Editor (Templates > New > Import).

### Testing

Follow the [testing guide](https://github.com/ROKT/gtm_wrapper/tree/master/docs/guides/how-to-test.md)
to set up the Testing Playground and test template changes. The `template.tpl`
file also contains inline test scenarios under the `___TESTS___` section.

### Deployment

Follow [Google's instructions](https://developers.google.com/tag-platform/tag-manager/templates/gallery#update_your_template)
to deploy template updates to the Community Template Gallery.

## Key Configuration (metadata.yaml)

- **Homepage:** <https://www.rokt.com>
- **Documentation:** <https://docs.rokt.com/docs/developers/integration-guides/third-party-integrations/google-tag-manager/google-tag-template>
- **Versions tracked by commit SHA** in `metadata.yaml`

## Maintaining This Document

When making changes to this repository that affect the information documented here
(template parameters, supported events, SDK dependencies, deployment process, etc.),
please update this document to keep it accurate. This file is the primary reference
for AI coding assistants working in this codebase.
