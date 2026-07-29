# Your Gift Story — Website

Handmade & personalised gifts, delivered pan India. Static site (no build step) powered by Supabase for products, orders, testimonials and admin.

## Repo structure

```
your-gift-story/
├── index.html          # Storefront (shop, cart, checkout)
├── admin.html          # Admin dashboard (login required)
├── testimonial.html    # Customer testimonial submission page
├── vercel.json         # Clean URLs + rewrites (/admin, /testimonial)
├── css/
│   ├── main.css        # Storefront styles
│   ├── admin.css       # Admin styles
│   └── testimonial.css # Testimonial page styles
└── js/
    ├── config.js       # ★ Supabase URL + anon key — ONLY place keys live
    ├── main.js         # Storefront logic
    ├── admin.js        # Admin logic
    └── testimonial.js  # Testimonial form logic
```

## Changing keys / Supabase project

Edit **`js/config.js`** only. Both values are read by every page:

```js
window.APP_CONFIG = Object.freeze({
  SUPABASE_URL: '...',
  SUPABASE_ANON_KEY: '...'
});
```

The anon key is a public key by design — it is safe in frontend code **only if Row Level Security (RLS) is enabled on every Supabase table**. Double-check RLS policies for `products`, `orders`, `testimonials`, and especially `admin_users`.

## Hosting

No build step — deploy the folder as-is.

**Vercel (recommended, uses vercel.json):**
1. Push this repo to GitHub.
2. Import the repo at vercel.com → Deploy. Done.
   Clean URLs (`/admin`, `/testimonial`) work automatically.

**Netlify:** drag-and-drop the folder, or connect the repo. For clean URLs add a `_redirects` file:
```
/admin        /admin.html        200
/testimonial  /testimonial.html  200
```

**GitHub Pages / any static host:** upload everything. Pages will be at `/admin.html` and `/testimonial.html` (no clean-URL rewrites without a config).

## Local preview

```bash
# from the repo root
python3 -m http.server 8000
# open http://localhost:8000
```

(Open via a local server, not by double-clicking the file — fetch calls need an http origin.)
