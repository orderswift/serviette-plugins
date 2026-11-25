---
name: order-takeaway
description: Find restaurants on Serviette and help the customer order food to collect from them, using the Serviette tools.
---

# Order food to collect with Serviette

Use the Serviette tools to help the customer order food from an independent restaurant, to collect.

1. Ask for a UK postcode, then use `find_restaurants`. If the customer names a restaurant, give its name as `brand`. Show the list and let the customer choose a site.
2. For the chosen site, use `get_menu` and `get_availability`, and confirm the items and the collection time with the customer.
3. Use `create_order_quote` to price the order. Give the customer the payment link it returns: they pay on that page themselves.
4. Use `get_order_status` to check whether the order has been paid, then give the customer the order reference and the collection time.

The tools' own descriptions and the server's instructions have the details.
