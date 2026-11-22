# Features

## Guest storefront

| Feature | Who uses it and what it does | Prerequisites and limits |
| --- | --- | --- |
| Resort information | Visitors can open the homepage, About, Experience, Accessibility, FAQ, and Contact pages. The theme supplies Arabic RTL layouts and responsive navigation. | The specialist page layouts are provided by the theme. General WordPress pages use the normal page editor. |
| Accommodation catalogue | Visitors browse WooCommerce villa and chalet cards with images, stay details, and prices. Product pages add a gallery, description, amenities, booking form, and related accommodation. | Browsing uses published, catalogue-visible products. Buying requires that the product be purchasable in WooCommerce. Homepage dates prefill the stay form. Availability is determined during booking, and the guest-count control does not filter the catalogue. |
| Dated stays | Shoppers choose arrival and departure dates and see a nightly estimate. One cart line holds one unit across all nights, with departure day excluded. | Requires a bookable stay product, WooCommerce, and usable booking storage. Arrival must be today or later in the site timezone. The default maximum is 90 nights. The same product or selected variation can appear only once in a cart as a stay. |
| Dated activities and boats | Shoppers choose a date and quantity. The selected date appears on the order. | Requires a configured activity product. Availability follows WooCommerce stock and quantity. Date-specific slots or activity capacity require a separate system. |
| Cart, checkout, and status | Shoppers see booking details, check out with WooCommerce, and see booking status in order views. At 900 px and below, the theme stacks the Checkout block fields and summary. | Site checkout settings determine guest checkout and available gateways. A booking is confirmed when WooCommerce reports payment and, for a stay, the plugin can finalize inventory. |
| Dining and inquiries | Visitors browse venue listings and detail pages, view configured menus, and open a prefilled WhatsApp chat for dining. The Contact page handles general inquiries. | The dining templates use saved menu and WhatsApp settings, with built-in defaults. Venue embeds show their links when the required values are present. WhatsApp conversations are external. Form delivery depends on WordPress mail. |

## Store and site administration

| Feature | Who uses it and what it does | Prerequisites and limits |
| --- | --- | --- |
| Product and rate management | Staff with WooCommerce product editing access manage prices, stock, images, booking type, and per-stay capacity. | Nightly capacity is a separate setting from WooCommerce inventory. Missing stay capacity defaults to one. The editor rejects a capacity below an active or booked unit number. New products can default to a bookable stay, so review that setting on ordinary merchandise and activities. |
| Stay Details | Product editors maintain the English name, bedroom count, pool, sea-view and family attributes, custom features, and three amenity descriptions. | The tab appears on simple and variable products. These are display fields. The booking validator uses dates and unit capacity. |
| Order follow-up | Staff with WooCommerce order access view dates and booking status and review availability conflicts. | Booking state follows WooCommerce payment and order events plus the plugin's inventory checks. A conflict is flagged for staff handling. |
| Homepage and catalogue presentation | Staff with theme-options access maintain homepage text and images, the accommodation catalogue hero, and displayed contact details. The Tamara Dashboard links to the relevant WordPress screens. | The Customizer stores per-theme settings. The two alternative homepage JPEGs in the source directories can be uploaded and selected manually. |
| Venue management | Staff with permission to edit venue posts manage the image, type, description, English name, tagline, menu link, and WhatsApp settings. | The MUX Booking plugin supplies the public dining archive, detail routes, and venue embeds. A theme fallback supplies the principal venue displays when editable records are unavailable. |
| Site setup | Administrators with `manage_options` can use Tools → Tamara Setup to create starter content and configure key page assignments. | The tool can set the homepage and shop page. Review existing assignments and the placeholder privacy and terms content on staging. |

[Back to project overview](README.md)
