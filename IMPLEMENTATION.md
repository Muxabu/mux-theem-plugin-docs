# Implementation

## Repository map

| Location | What it contains |
| --- | --- |
| `theme/source/tamara-beach/` | Tamara Beach theme 2.2.7. PHP templates, theme options, product display helpers, styles, browser scripts, bundled assets, and source tests. |
| `theme/tamara-beach-work/` | A working copy of the same theme tree at this revision. |
| `theme/tamara-beach-2.2.7.zip` | The installable theme. The unversioned theme archive contains the same package. The two optional homepage hero concepts are in the theme source trees. |
| `plugin/tamara-core.zip` | The installable MUX Booking plugin 1.2.0. The archive contains its PHP bootstrap, six modules, browser assets, tests, and starter media. |

This is a server-rendered WordPress application. The theme and plugin run in the same PHP process, share WordPress's database and admin, and use WooCommerce's hooks and data APIs. The theme ships ready-to-load CSS and JavaScript assets. WooCommerce provides product records, sessions, checkout, orders, and the payment interface.

## Public screens and theme modules

| Surface | How it works |
| --- | --- |
| Homepage | The front-page template reads Customizer settings with bundled defaults for resort copy and imagery. It displays accommodation cards and dining highlights. The date form sends `tamara_check_in` and `tamara_check_out` to the catalogue, and eligible product links carry the dates into the stay form. |
| Catalogue and product details | The product archive and card templates use the WooCommerce product loop. The product detail template shows its gallery, amenities, description, and booking controls. Display helpers read Stay Details from the companion plugin and supply legacy display defaults for older products. WooCommerce price markup is preserved, with an active discount display and variation updates. The theme price presentation is geared toward overnight rates. Activity totals follow the activity pricing rule in the cart. The theme suppresses product reviews. |
| Cart and checkout | The theme wraps WordPress page content containing the WooCommerce block or classic checkout. WooCommerce owns the form and totals. At 900 px and below, the 2.2.7 checkout styles force the block layout to stack, including the reversed RTL arrangement. The main form and summary use the full available width, with field widths bounded by their containers. The sidebar uses normal document positioning. These rules address the Paymob 4.1.x zero-width conflict. The base stylesheet confines its contact grid to contact form rows so it stays out of classic checkout. |
| Resort information and contact | The theme provides dedicated About, Experience, Accessibility, FAQ, and Contact templates, plus the normal WordPress templates for other content. The header and FAQ use native disclosures. The shared browser script adds date field guidance and scroll and reveal behavior. The Contact template posts to WordPress and displays the returned result. |
| Dining | The homepage highlights Pavilion and MOJO and links to the dining directory. The dining archive and detail templates read published venue posts and metadata. The plugin registers the public dining archive and detail routes, exposes the venue type through the WordPress REST API, and provides the `tamara_venues`, `tamara_dining`, and `tamara_venue` embeds. The theme fills missing venue fields with Pavilion or MOJO defaults and supplies fallback routes when the venue post type is absent. |
| WordPress administration | The theme's Tamara Dashboard provides shortcuts to product, order, page, venue, and appearance screens. The Customizer writes theme settings. Product and venue editors write data to their respective WordPress records. |

## Companion plugin modules

| Module | Responsibility |
| --- | --- |
| Booking | Adds dated product fields and the browser price estimate. Validates purchase input, attaches booking data to the WooCommerce cart, synchronizes it into classic and Store API checkout orders, and reacts to payment and order transitions. |
| Availability | Creates and checks the InnoDB schema. Allocates numbered units across a complete date range, attaches holds to orders, finalizes qualifying stays, and releases expired or cancelled inventory. |
| Booking capacity | Adds the per-day count of identical units to product editing. It checks the integer limit and coordinates capacity reductions with the availability module. A variation can inherit its parent's setting. |
| Stay Details | Adds the accommodation information tab and normalizes the data used by theme cards and product pages. |
| Dining | Registers the venue content type, editor, metadata, Media Library controls, and rendering helpers. It can run independently of WooCommerce booking. |
| Setup | Provides the administrator action that populates starter pages, products, venues, and attachments and refreshes routes. |

The plugin starts after WordPress has loaded the active plugins. It enables booking and capacity hooks when WooCommerce is active and the availability schema is ready. When the schema check fails, purchase guards block bookable products, administrators receive a notice, and later requests can retry setup. Dining remains available independently.

## Data, requests, and background work

- **WordPress database.** Pages and venues are WordPress posts. Venue details are post metadata, images and PDFs are Media Library attachments, general settings are WordPress options, and homepage and contact settings are theme modifications.
- **WooCommerce data.** Bookability, booking type, capacity, and display attributes are product metadata. Cart sessions hold the selected dates and allocation. Order line metadata stores dates and the information needed to recover the allocation. A separate order field stores the booking state. The plugin uses WooCommerce order APIs and declares High-Performance Order Storage and Cart and Checkout Blocks compatibility.
- **Nightly inventory.** The site-prefixed `tamara_booking_dates` table stores product or variation ID, unit number, night, hold token, order ID, status, and expiry. The product, unit, and night uniquely identify a slot. Allocation uses InnoDB transactions and product-level database locks where available. Every night in a stay must belong to the same unit. On paid transitions, the module also checks overlapping paid orders before confirmation.
- **Scheduled work.** WordPress Cron runs expired-hold cleanup hourly. Booking requests also clear expired holds when checking products. Release retries are scheduled for temporary failures and recheck order state before acting. Confirmed rows have no expiry and are released through the relevant order lifecycle actions.
- **Access.** WordPress login and capabilities govern admin access. Setup checks `manage_options`, the theme dashboard checks `edit_theme_options`, and venue and product writes use WordPress or WooCommerce editing permissions. Form handlers use nonces and sanitize input. Public browsing and inquiries use anonymous WordPress routes. WooCommerce controls checkout accounts and order access.

## External boundaries

WooCommerce integrates with the separately installed payment gateway. The booking plugin reads WooCommerce payment events and paid states. It records a conflict when paid inventory cannot be confirmed so staff can handle the order. Dining and general inquiry links open WhatsApp outside WordPress. The Contact form calls `wp_mail` and returns a status to the browser. The handler passes the sender's name, email, phone, and message to the configured contact recipient and does not create a WordPress inquiry record. Mail transport and actual delivery depend on the site's hosting or SMTP configuration.

[Back to project overview](README.md)
