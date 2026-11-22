# Run guide

## Prerequisites

Use a staging site with HTTPS, a PHP-capable web server, and MySQL or MariaDB with InnoDB. The documented project minimums are WordPress 6.4, PHP 7.4, and WooCommerce 8.5. Choose supported versions that work together. The WordPress database user needs permission to create and upgrade the booking table. Have administrator access and both installable packages available. [WordPress server setup](https://developer.wordpress.org/advanced-administration/before-install/)

The theme and companion plugin are both listed as **MUX Booking** in WordPress. Install the theme at **2.2.7** and the companion plugin at **1.2.0**. Theme and plugin control names are given in English here. Their labels may appear in Arabic in WordPress.

## Install and configure

1. Start the database and web server. Install WordPress, then sign in to its administration area. The WordPress database settings are `DB_NAME`, `DB_USER`, `DB_PASSWORD`, and `DB_HOST`. The WordPress table prefix also applies to the booking table.
2. Install and activate **WooCommerce**, then install and activate the **MUX Booking** companion plugin. Install and activate the theme from **Appearance → Themes**. Choose Arabic as the site language to match the RTL storefront. Set the resort's local timezone under **Settings → General** so date validation follows its calendar.
3. If you need starter content, open **Tools → Tamara Setup** and run it. It creates missing pages and can populate four stay products and two venue records. Review the homepage and shop assignments after setup. Replace the placeholder privacy and terms text before using those pages on a live site.
4. In **Settings → Permalinks**, select **Post name** and save. Check that the homepage, accommodation catalogue and dining routes open. Review **WooCommerce → Settings → Advanced → Page setup** for the Cart and Checkout page assignments. Fresh cart and checkout pages made by Tamara Setup use the classic format. To try block checkout, put the WooCommerce **Checkout** block in the assigned page and use the theme's checkout template. [WooCommerce page setup](https://woocommerce.com/document/configuring-woocommerce-settings/advanced/)
5. On the staging site, use **WooCommerce → Settings → Site visibility → Live** to make the store pages accessible to signed-out visitors. [WooCommerce site visibility](https://woocommerce.com/document/configuring-woocommerce-settings/coming-soon-mode/)
6. Set currency and applicable taxes, guest-account policy, and payment options in WooCommerce. Install and enable a supported gateway separately to exercise payment on staging. Configure it in test or sandbox mode. For the documented Paymob layout scenario, use Paymob for WooCommerce 4.1.x with the Checkout block. [Paymob plugin settings](https://developers.paymob.com/paymob-docs/integration-paths/plugins/wordpress)
7. Keep WordPress Cron working so expiry cleanup and release retries can run. Configure the hosting mail service or SMTP if you want contact and WooCommerce notification delivery. Set the public contact recipient before trying the form.

## Settings that affect behavior

| Setting | Where it is used |
| --- | --- |
| **Bookable** and **Booking Type** | In WooCommerce Product Data, enable the date fields and select **Stay** or **Activity / Boat**. Review the selected type on new products. |
| **Number of identical units available per date** | In Product Data for stays, set the count of equivalent units. A missing value defaults to one. WooCommerce stock remains a separate setting. |
| **Hold stock** (`woocommerce_hold_stock_minutes`) | WooCommerce inventory setting used when allocating a hold to an unpaid order. The plugin uses at least the cart hold duration and falls back to 60 minutes when the stock hold value is empty or zero. |
| `tamara_core_cart_hold_minutes`, `tamara_core_max_stay_nights`, `tamara_core_max_booking_capacity` | WordPress developer filters for the default 20-minute cart hold, 90-night maximum stay, and maximum allowed unit count. The default maximum unit count is 500, with a hard upper bound of 10,000. |
| `tamara_home_hero_image`, `tamara_villas_hero_image` | Customizer settings for the homepage and accommodation catalogue hero images. Upload an alternative homepage JPEG from the theme source if you want to preview it. |
| `tamara_email`, `tamara_phone_primary`, `tamara_phone_secondary`, `tamara_address` | Customizer settings for resort and contact information. The inquiry handler falls back to the WordPress administration email if the configured recipient is missing or invalid. |
| **Menu PDF**, **WhatsApp number**, and **WhatsApp message** | Venue editor settings. Choose a PDF from the Media Library and enter the venue's international-format number and optional prefilled message. |

## Try the workflows on staging

1. Publish a stay with a price and unit capacity. Open the homepage and choose a future range of two or three nights. Open a product from the catalogue and check its prefilled dates and estimate. Add it to the cart and review the dates and total.
2. Open checkout in an RTL phone viewport at 900 px or narrower. With the Checkout block, look for full-width form and summary sections stacked vertically. Submit through the configured sandbox gateway and inspect the order's booking dates and status in **WooCommerce → Orders**. To exercise an availability rejection, use separate shopping sessions and try the same range on a one-unit product while its first cart hold is active.
3. Publish an activity or boat product with a staging price and WooCommerce stock. Choose a future date and quantity, then review the activity date and total in the cart.
4. Edit a venue and verify its listing, detail page, configured menu link, and WhatsApp preview. Send a synthetic Contact form inquiry through the staging site's mail setup and check the displayed response and delivery to the configured recipient.
5. To review the 2.2.6 homepage editing, change a headline in **Appearance → Customize → Homepage Content** and preview the storefront. To preview one of the optional hero concepts, upload the JPEG from the theme source to the **Media Library**, then pick it in **Appearance → Customize → Homepage Images and Banners → Main Hero Image**. Check the preview at mobile and desktop widths before saving on staging.
6. To check the 2.2.7 classic checkout styling, open a staging checkout page using the classic format and verify that the billing rows follow the WooCommerce layout.

[Back to project overview](README.md)
