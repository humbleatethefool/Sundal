# Sundal

Sundal is a mobile-first app that lets snack shop vendors manage stock, see what each company's employees have bought from the shop, and see the monthly total each company owes. Employees record their own purchases on their phones.

## Users

- **Vendor:** runs the shop from a phone and has very little time to spare. Sets snack prices and stock levels, serves multiple companies, and can void a single entry, meaning one snack line of a purchase.
- **Employee:** works at a company the vendor serves and uses a phone. Has one personal sign-in, active on one phone at a time, and records only their own purchases by adding snacks to a purchase cart, reviewing the total, and recording it. Each snack line becomes its own entry. Cannot cancel an entry.
- **Company admin:** uses a phone. Sees the monthly total the company owes, as cumulative totals only, never who bought what.

## Product rules

- Each company's purchases are totalled per month. The month closes automatically at midnight Indian time on its last day, and a closed month never changes. A void of an entry in a closed month appears in the open month as a labeled line.
- Each purchase keeps the price shown when it was made.
- The vendor builds the catalog: creates a category, names it and uploads its image, then adds items to it.
- Employees never see the stock number. Recording a purchase takes its quantity out of stock, and an employee cannot add more of an item than its stock allows; an item at zero shows "Out of stock". Voiding an entry returns its quantity to stock. Only the vendor changes stock counts directly.
- The employee's purchase cart is kept on their account until they record it or empty it, and shows the same items at the next sign-in. The cart bar is hidden while the cart is empty.
- Employees change quantity with + and − buttons only, one per tap, with no typing and no repeat on hold. The vendor's stock quantity is a number field with + and − buttons.
- Walk-in cash sales happen outside the app and are not recorded, so stock levels the vendor maintains can drift from the shelf.
- Payment features are V2 scope: marking a month as paid, the vendor raising an invoice, and the company paying in the app.

## Constraints

- English only, built for all of India.
- Vendors, employees, and company admins use phones only.
- Online only: every app screen needs an internet connection. A purchase exists only once the server has confirmed it, and retrying the same confirm never records it twice.
- Offline behavior in the employee mobile app: when the phone goes offline, a toast says "You're offline" and nothing else on screen changes. When the employee taps anything that needs the server while offline, the screen shows "You're offline" with a Retry button, and nothing changes on the server. This applies to every action in the app.
- Preferences: simple for non-technical users, light on data, quick to ship.

## Design references

- Blinkit, Zepto, and Instamart are the references for information architecture, UX patterns, and components.
- Sundal has no cart, payment, or delivery, and each entry holds one snack, so a borrowed pattern is adapted to those rules.

## Scope boundaries

- Work is on UX screens. Technology choice is out of scope.
- The employee mobile app comes first.
- The wiki is built once the product is understood.
