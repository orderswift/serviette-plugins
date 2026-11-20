# Serviette for ChatGPT

Order food to collect from independent restaurants, without leaving the conversation. Ask for takeaway near a postcode, or for a particular restaurant by name; choose a restaurant and see its menu and the first time you can collect; and ChatGPT puts the order together and gives you a link to pay on Serviette's own secure page. Serviette is not a marketplace and does not rank restaurants.

## What is in this plugin

- A connection to the Serviette MCP server at `https://agent.withserviette.com/agent/mcp` (the same server as the Serviette connector).
- One skill, `order-takeaway`, which tells the assistant how to take a collection order from start to payment.

## Using it

Add the plugin from the ChatGPT plugin directory, then ask, for example: "Order a pizza to collect near LS1 4AP" or "Is Pizza Express near me on Serviette?". Finding restaurants, reading menus and building an order need no sign-in. Saved orders ("my usual") ask you to sign in once, with an emailed six-digit code, the first time they are needed.

## Data and privacy

Everything goes to `agent.withserviette.com`, and nowhere else. What is sent: the postcode, location, cuisine or restaurant name you ask for; the items and collection time you choose; and, for saved orders only, your email address. You never give card details to ChatGPT: you enter your name, contact details and card yourself on the Serviette payment page (on `agent.withserviette.com`), which is handled by Stripe. Serviette's privacy policy is at https://withserviette.com/privacy and its terms are at https://withserviette.com/terms.

The plugin contains no scripts, hooks or binaries, and no credentials.

## Licence

MIT, see `LICENSE`.
