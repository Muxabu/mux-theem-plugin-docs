# Project flow

## Book a villa or chalet

1. **Guest.** Open the accommodation catalogue directly or submit arrival and departure dates from the homepage. The dates can carry through the catalogue links into a stay product's form. The catalogue shows products and carries those dates forward. MUX Booking checks stay inventory when the guest adds the product to the cart.
2. **Guest and product page.** Select a villa or chalet, choose a variation if the product offers one, and enter arrival and departure. For example, arriving on the 10th and leaving on the 13th uses three nights. At 800 per night the estimate is 2,400 before any WooCommerce adjustments. The browser updates the estimate as dates or the selected variation change.
3. **MUX Booking.** On add to cart, validate dates, use the WooCommerce product or variation price, and look for one unit available across all nights. A successful add holds that unit temporarily and shows the dates in the cart. For a capacity of two, two separate carts can hold different units for the same nights. If both units are occupied, the next guest must pick different dates or accommodation.
4. **Guest and WooCommerce.** Review the dates and totals, enter checkout details, and choose an available payment method. MUX Booking rechecks availability and associates the hold with the order. The order records the booking dates and starts with a separate awaiting-payment booking status. The theme supports the classic checkout and a Checkout block layout.
5. **Payment provider and MUX Booking.** The configured gateway handles payment and WooCommerce reports its outcome. On a paid state, the plugin attempts to finalize the stay's inventory, then marks and displays the booking as confirmed if that succeeds. Staff can see the booking state and dates in the WooCommerce order.

### When the checkout takes a different path

- If a guest enters an invalid date range or the stay is over the configured maximum, the validation rejects it. The guest can correct the dates on the product page.
- While a cart is open, its active hold keeps its original expiry. When an expired hold is still available, a cart check can take it again. If no unit is available across the full date range, the guest sees an availability error. Removing the item or emptying the cart releases the cart hold.
- A new order that is pending payment or on hold stays unconfirmed until it reaches a paid state. When WooCommerce reports a failed, cancelled, or refunded order, MUX Booking marks the booking cancelled and attempts to release its inventory.
- If payment arrives after the hold has expired and no unit can be allocated, the order can show an availability conflict despite being paid. MUX Booking adds an order note. Staff resolve the case in WooCommerce, including arranging a refund if appropriate.

## Book an activity or boat

1. **Store staff.** Configure a WooCommerce product as bookable and choose the activity or boat booking type. Set its price and any WooCommerce stock or quantity limits.
2. **Guest.** Choose one current or future date and a quantity. For example, three places on an activity priced at 100 each start with a line total of 300 before WooCommerce adjustments.
3. **WooCommerce and MUX Booking.** Validate the date, carry it into the cart and order, and use regular WooCommerce pricing and stock. The date is recorded on the order. Activities use a different inventory path from overnight stays and have no built-in timeslot capacity.

## Browse dining and contact the resort

1. **Venue editor.** Publish a Pavilion or MOJO record with a title, description and image. Add a PDF menu and a venue WhatsApp destination to replace the theme defaults.
2. **Visitor.** Open the dining directory or a venue page, view the menu when provided, and use the WhatsApp action to open a prefilled conversation. The visitor completes that conversation outside the storefront.
3. **Visitor seeking general help.** Open the Contact page. Use the displayed inquiry links or fill in the contact form. It asks for a name, email, phone, inquiry type, and message.
4. **Theme and WordPress.** Validate the submission, then send the message through WordPress mail to the site's configured contact recipient. The page shows feedback from the submission. The resort team can respond using the reply-to address.

## Update the storefront

1. **Site administrator.** Use Tamara Setup to create starter pages, accommodation products, and venue records as needed. Review the page assignments and placeholder text before launch.
2. **Store staff.** Edit the product price, gallery, booking type, identical-unit capacity, and Stay Details. Updates to accommodation details feed the product display, while changes to rates and capacity affect future cart and availability checks.
3. **Site or venue editor.** Use the WordPress Customizer and venue editor for the settings they have permission to change. Preview homepage copy and images, and review the public dining page after publishing a venue update.

[Back to project overview](README.md)
