# API

## Overview

The API surface supports the blog (headless CMS), store (e-commerce backend),
contact form, and gallery asset management. Final backend choices are TBD
during the design phase.

## Contact Form

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/contact` | POST | Submit a contact/inquiry message |

**Request body:**
```json
{
  "name": "string",
  "email": "string",
  "subject": "string",
  "message": "string",
  "recaptcha": "string"
}
```

**Response:** `201 Created` with confirmation message.
Triggers email notification to admin.

## Store API

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/products` | GET | List products (supports `?category=`, `?featured=true`) |
| `/api/products/:id` | GET | Single product detail |
| `/api/products/:id/stock` | GET | Stock/variant availability |
| `/api/cart` | GET | Retrieve current cart (session/token) |
| `/api/cart/items` | POST | Add item to cart |
| `/api/cart/items/:id` | PATCH | Update cart item quantity |
| `/api/cart/items/:id` | DELETE | Remove item from cart |
| `/api/checkout` | POST | Process order (payment, shipping, confirmation) |
| `/api/orders/:id` | GET | Order status and details |

**Payment integration TBD:** Stripe, PayPal, or local payment processor.

## Blog (Headless CMS)

CMS candidates: Contentful, Strapi, Sanity, or WordPress REST API.

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/cms/posts` | GET | List published posts (paginated) |
| `/cms/posts/:slug` | GET | Single post by slug |
| `/cms/posts?tag=` | GET | Filter posts by tag/category |
| `/cms/authors/:id` | GET | Author profile |

**Response** (typical CMS shape):
```json
{
  "title": "string",
  "slug": "string",
  "excerpt": "string",
  "body": "string (rich HTML/Markdown)",
  "coverImage": "url",
  "author": { "name": "string", "avatar": "url" },
  "tags": ["string"],
  "publishedAt": "ISO8601",
  "updatedAt": "ISO8601"
}
```

## Gallery / Asset Management

Asset hosting TBD: Cloudinary, Sanity, or self-hosted CDN.

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/gallery` | GET | List gallery items (supports `?medium=`, `?year=`, `?tag=`) |
| `/api/gallery/:id` | GET | Single artwork with metadata |

**Artwork model:**
```json
{
  "id": "string",
  "title": "string",
  "description": "string",
  "images": ["url (multiple sizes)"],
  "medium": "mural | illustration | canvas | digital",
  "dimensions": "string",
  "year": 2024,
  "tags": ["string"],
  "forSale": false,
  "productId": "string | null"
}
```

## Email / Notifications

| Event | Trigger |
|-------|---------|
| Contact form submission | Email to admin with inquiry details |
| Order confirmation | Email to customer with order summary |
| Order notification | Email to admin for new orders |
| Newsletter signup | Welcome email (if Mailchimp/MailerLite integrated) |

## Authentication

Admin-only dashboard for content management (TBD whether needed or managed
entirely through headless CMS).
