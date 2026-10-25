# ShopNest frontend

ShopNest is a React single-page storefront built with Vite, React Router, Axios,
and the Context API. The cart is shared across routes and saved in browser
`localStorage`.

## Run locally

1. Install dependencies with `npm install`.
2. Copy `.env.example` to `.env.local`.
3. Start the Phase 4 backend, then set `VITE_API_PROXY_TARGET` in `.env.local`
   to its origin (the default is `http://localhost:5000`).
4. Run `npm run dev` and open the URL printed by Vite.

The frontend requests `GET /api/products` by default. Set
`VITE_API_BASE_URL` to the backend API base URL when it differs from `/api`,
for example `https://api.example.com/api`. The API may return a product array
directly or as `{ "products": [...] }` / `{ "data": [...] }`. Each product needs
an `id`, `name`, `category`, and numeric `price`; `imageUrl`, `originalPrice`,
`rating`, and `description` are optional. Product detail pages also display
optional `brand`, `images` (string array), `highlights` (string array),
`specifications` (object of primitive values), `availability` (a status string
or `{ "status", "inStock", "quantity" }`), `inStock`, `stockQuantity`, and
`reviews` (objects with `rating`, `comment`, optional `name`/`author`, `date`,
and `id`). Reviews, stock, specs, and extra images are not fabricated when
those fields are missing.

The Contact page posts `{ "name", "email", "subject", "message" }` to
`VITE_CONTACT_API_URL`. Configure this variable with the support endpoint URL
to enable message delivery; without it, the form informs visitors that support
is not connected.

The Login popup validates an email and password locally. Authentication is not
connected, so the form does not send or store credentials.

When the API is unreachable, the app displays the bundled `products.json`
catalog in both development and production. A warning is logged to the browser
console. Configure `VITE_API_BASE_URL` for the deployed backend to load its
catalog instead.

## Production build

Run `npm run build` to create the deployable static site in `dist/`, then
`npm run preview` to inspect that build locally. Configure the hosting service
to serve `index.html` for unknown paths so direct navigation to routes such as
`/products/1` works. Configure `VITE_API_BASE_URL` for the deployed backend
before building, and ensure that backend allows requests from the frontend
origin when using an absolute API URL.

The Cart page shows a 5% tax estimate; this is a frontend estimate, not a
checkout or tax calculation service.
