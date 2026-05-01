# Architecture

## Tech Stack

- **Framework:** Angular (version TBD)
- **Language:** TypeScript (strict mode)
- **Styling:** SCSS with a design-token system
- **Reactive layer:** RxJS, Angular Signals (TBD)
- **State management:** TBD (Signals-based store, NgRx, or lightweight service pattern)
- **Testing:** Jasmine/Karma or Jest (TBD)

## Module Structure

```
src/app/
├── core/            # Singleton services, guards, interceptors
├── shared/          # Reusable components, directives, pipes
├── features/
│   ├── home/        # Homepage module (lazy)
│   ├── gallery/     # Gallery module (lazy)
│   ├── store/       # Store module (lazy)
│   └── blog/        # Blog module (lazy)
└── pages/           # Static informational pages (lazy)
    ├── about/
    ├── contact/
    └── legal/
```

## Routing

```
/                     → HomeComponent
/gallery              → GalleryModule (lazy)
/gallery/:id          → GalleryDetailComponent
/store                → StoreModule (lazy)
/store/:id            → ProductDetailComponent
/store/cart           → CartComponent
/store/checkout       → CheckoutComponent (guard: cart not empty)
/blog                 → BlogModule (lazy)
/blog/:slug           → BlogPostComponent
/about                → AboutComponent
/contact              → ContactComponent
/legal                → LegalComponent
/**                   → NotFoundComponent
```

## Component Tree

```
AppComponent
├── HeaderComponent
│   ├── LogoComponent
│   ├── MainNavComponent
│   └── CartIconComponent
├── RouterOutlet
│   └── [Lazy-loaded feature or static page]
└── FooterComponent
    ├── FooterNavComponent
    ├── SocialLinksComponent
    └── NewsletterSignupComponent
```

## Service Layer

| Service | Responsibility |
|---------|---------------|
| `GalleryService` | Fetch/filter gallery items, asset URLs |
| `StoreService` | Product catalog, cart state, checkout flow |
| `BlogService` | Fetch blog posts from CMS, pagination |
| `ContactService` | Submit contact form, email notifications |
| `SeoService` | Meta tags, Open Graph, structured data |
| `AnalyticsService` | Page views, events, e-commerce tracking |
