# Testing

## Comparing the theme packages

Ran each archived theme's bundled source tests with Node.js 24.19.0. PHP 8.5.11 syntax checks passed on all 24 PHP files in each package. Archive integrity checks also passed for every file entry.

| Package | Source tests | Verified file entries |
| --- | --- | --- |
| 2.2.5 original | 4 passed. Checked accommodation details and WooCommerce price display wiring. | 69 |
| 2.2.6 | 6 passed. Added checks for homepage Customizer fields, shared defaults, and safe rendering. | 70 |
| 2.2.7 | 10 passed. Added checks for mobile checkout widths, RTL stacking, and contact form scoping. | 71 |

The 2.2.6 and 2.2.7 styles were also compared in a completed headless Chrome 157 fixture. It used simulated RTL WooCommerce checkout markup and Paymob layout rules. On 2.2.6 the main checkout column measured 0 px at viewports of 375 and 900 px. On 2.2.7 both columns stacked and each measured the full available width, 343 px and 852 px respectively. At 901 px both versions used a side-by-side layout. The mock classic checkout row changed from a grid to a block in 2.2.7, and the mock contact form row used a grid in both versions.

## Bundled tests

The 2.2.7 theme and 1.2.0 plugin suites were run for the documented revision with Node.js 24.19.0. All 44 tests passed, with zero failures and zero skips.

| Check | Coverage and observed result |
| --- | --- |
| Theme source tests, 10 passed | Inspected the mobile checkout CSS and contact grid scope, homepage settings and rendering, accommodation detail consumers, and price and variation wiring. |
| Plugin source tests, 28 passed | Inspected the WooCommerce hook wiring, availability schema and allocation logic, retry guards, setup and venue defaults, capacity editor, and Stay Details editor. |
| Plugin JavaScript tests, 6 passed | Executed the booking summary script with a mock DOM and WooCommerce variation events. Date validation, calendar edge cases, nightly totals, currency formatting, and variation changes and resets produced the expected values. |

The source tests inspect declarations and wiring. The JavaScript tests run the packaged browser logic against fixtures.

## WordPress and WooCommerce runtime

Ran the installable theme and companion plugin in a disposable Arabic WordPress 6.8.3 site with WooCommerce 10.2.2, MySQL 8.4.11, and PHP 8.5.11.

| Check | Observed result |
| --- | --- |
| Activation and booking schema | The theme and plugin activated. MySQL contained the version 2 InnoDB availability table with a unique product, unit, and date index. WordPress scheduled hourly hold cleanup. |
| Admin setup and rerun | Submitted Tools → Tamara Setup twice through the WordPress admin. The first submission created four stay products, two venue posts, and eight attachments, kept an existing home page body, and set up classic cart and checkout. The rerun preserved the record IDs, an edited price, and an edited venue title. WordPress core reported two non-fatal image metadata warnings during setup. The expected records and menu attachment metadata were present. |
| Admin screens and access | An administrator opened the Tamara Dashboard, WooCommerce product editor, venue editor, and Customizer. The expected booking, stay details, venue, and theme controls were present. WooCommerce redirected the subscriber away from the setup and theme dashboard screens. |
| Component fallback | In a request that omitted WooCommerce, the venue type, embed, and both venue records remained available. In a request that omitted MUX Booking, the theme returned the two bundled fallback venues. |
| Stay pricing and inventory | A three-night stay used the configured nightly price and wrote three rows for one numbered unit. Departure day was excluded. The cart rejected a duplicate booking for the same product. A separate overlapping hold reserved a second unit. A third hold was rejected. |
| Classic order creation and payment | WooCommerce order creation stored dates and nights, set the booking to awaiting payment, and attached the rows to a longer order hold. Triggering WooCommerce payment completion confirmed the booking and removed the hold expiry. |
| Cancellation and late payment | Cancellation released only the affected order's rows, and the freed unit could be held again. In a separate case, after an order's hold was aged out and another cart claimed the unit, the simulated payment recorded an availability conflict and preserved the other cart's hold. |
| Activity pricing and dates | An activity cart stored the selected date and applied normal quantity pricing. The inventory table had no nightly rows for the activity. |

The seven booking lifecycle cases ran through WooCommerce APIs and hooks with High-Performance Order Storage active and real MySQL rows. The fixture simulated gateway completion by triggering the WooCommerce payment event. It intercepted outgoing mail.

Ran a signed-out storefront smoke check in headless Chrome 157 on that same site.

- The Arabic RTL homepage carried a three-night date range through the catalogue and prefilled the product form. The browser showed the three-night estimate, added the stay to the cart, opened classic checkout, and displayed an empty cart after removal.
- With the actual WooCommerce Checkout block assigned, its fields and order summary stacked at full available width in a 390 px RTL viewport.
- The About, Experience, Accessibility, FAQ, and dining pages opened. Both venue pages produced populated WhatsApp links and served their local PDF menus. The check inspected the external links and fetched the PDFs from the local site.
- The public Contact form showed successful submission when the local mail interceptor accepted the synthetic message.

## PHP and browser checks

| Check | Evidence and observed result |
| --- | --- |
| PHP syntax | Ran PHP 8.5.11 syntax checks across all 32 PHP files in the theme source and extracted companion plugin. Every file passed. |
| Booking rules | Ran eight PHP cases against the booking, capacity, and availability classes with WordPress and WooCommerce stubs and an in-memory inventory simulator. Date and price checks passed. The fixture allocated two units and rejected a third, released and reused a slot, preserved and refreshed hold expiry as expected, rolled back a simulated partial write, and converted an order hold to a booked row after a simulated paid state. |
| Contact and dining fallback | Ran seven PHP cases with WordPress and mail stubs. The handler returned the expected feedback for a valid submission, an invalid recipient setting, a simulated mail failure, a missing nonce, a missing message, and a filled honeypot. The venue fallback built PDF paths and prefilled WhatsApp links for both venues. |
| Theme interactions | Ran the theme scripts in headless Chrome 157 with a small RTL HTML fixture and simulated WooCommerce variation events. Date guidance corrected an invalid departure, the fixture disclosures closed the previous item when a second opened, and the displayed price and discount updated and reset with variation events. |

## Packages and images

- Ran archive integrity checks on the installable theme and plugin. Both passed. The two installable 2.2.7 theme archives matched byte for byte. The two theme source trees matched, and the installable theme matched them apart from the two optional hero images.
- Ran a desktop decoder on both optional homepage images from the theme source. Both decoded as 1983 × 793 JPEGs.

[Back to project overview](README.md)
