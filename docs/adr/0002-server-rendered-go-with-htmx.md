# Server-rendered Go with HTMX, not a JavaScript single-page app

The app is a single Go binary. It routes with the standard library's `net/http`, renders pages with `html/template`, and uses HTMX for partial page updates. Accord and Rating bars are plain HTML/CSS, so there is no JavaScript framework or chart library. Data access is hand-written SQL compiled to Go by sqlc on top of pgx, with no ORM. Migrations are goose files compiled into the binary and applied at startup. The user wants to maintain the app in Go, and it only ever runs on localhost for one person, so nothing needs client-side state beyond what HTMX provides.

## Considered Options

- TypeScript throughout (Next.js or SvelteKit): one language for server and charts, but not the language the user wants to maintain.
- Python (FastAPI or Django with HTMX): same page model as this one, but not the user's choice.
- templ instead of `html/template`, or GORM instead of sqlc: rejected to avoid an extra code-generation step and to keep queries as plain SQL.

## Consequences

If a view later needs richer interactive charts, add a small chart library to that page rather than moving to a single-page app.
