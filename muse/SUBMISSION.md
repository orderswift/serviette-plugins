# Submitting Serviette to Meta Muse

Muse has no package or manifest: a connector is a live MCP server described in a web form at **muse.ai/platform** ("Submit a connector", behind a work-email sign-in). This file has the answers to paste, what Meta's connector guidelines (platform.muse.ai/docs) and terms (platform.muse.ai/terms) ask for, and what is still open. The field labels come from a third-party description of the form, so check them against the live form. Nothing has been submitted.

## Describe your product

| Field                                  | Answer                                                                                                                                                                                       |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Connector name                         | Serviette                                                                                                                                                                                    |
| Company or developer                   | Tasty Tech Limited (company number 08467443) _(check: this is the operator named in the terms and privacy pages)_                                                                            |
| Product website                        | https://withserviette.com                                                                                                                                                                    |
| Example prompts                        | "Find a takeaway to collect near LS1 4AP"; "Is Pizza Express near me on Serviette?"; "Order a margherita pizza from the first one, ready as soon as possible"; "Order the same as last time" |
| Connector icon (512 × 512, PNG or SVG) | `icon.png` (512 × 512) or `icon.svg` in this folder: the Serviette mark                                                                                                                      |
| Payments                               | **Yes.** Orders are paid by card on Serviette's own payment page (Stripe). No payment details pass through the connector                                                                     |
| Support email or URL                   | https://withserviette.com/support                                                                                                                                                            |
| Privacy policy URL                     | https://withserviette.com/privacy                                                                                                                                                            |
| Terms of service URL                   | https://withserviette.com/terms                                                                                                                                                              |

**Short description** (for any description field): Order food to collect from independent restaurants. Find restaurants near a UK postcode or by name, choose from the menu and collection times, and pay on Serviette's own secure page. Collection only, UK.

## Technical specs

| Field               | Answer                                                                                                                                                                                                                                                                                                                                                                |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Connection type     | Existing MCP                                                                                                                                                                                                                                                                                                                                                          |
| Hosted MCP endpoint | https://agent.withserviette.com/agent/mcp                                                                                                                                                                                                                                                                                                                             |
| Documentation       | https://withserviette.com/for-agents/tools (the same text as `TOOLS.md` in this folder)                                                                                                                                                                                                                                                                               |
| Authentication      | **OAuth with PKCE.** Only two tools need it (the customer's saved orders); everything else works with no sign-in, and a call that needs it is answered with HTTP 401 and a `WWW-Authenticate` challenge. Dynamic client registration, `S256` PKCE, `resource` parameter, one scope (`orders`). The customer proves their email address with an emailed six-digit code |
| Access requirements | UK restaurants only; collection only (no delivery). Browsing, menus and building an order need no account. Saved orders ("my usual") need the customer to sign in. Muse's redirect address must be allowed: see below                                                                                                                                                 |

## What Meta's guidelines ask for, and where we stand

Official sources: platform.muse.ai/docs ("Connector guidelines") and platform.muse.ai/terms ("Muse Connector Terms").

- **Read / write / sensitive-write classification:** done in `TOOLS.md`. No tool is a sensitive write (nothing is charged or placed by a tool). Meta's portal will ask for this; "sensitive write" classification is described as coming to the portal.
- **Business verification and authority** (5.2): needs evidence that Tasty Tech Limited exists and that the submitter may act for it. **To do.**
- **Data-processing questionnaire, security and support contacts, a responsible developer** (5): **to do.** The terms require notifying vendor-incident@meta.com within 48 hours of a security incident involving user data (4.8) and encryption of data in transit and sensitive data at rest (4.4).
- **Test account for reviewers** (5.5): sign-in is an emailed code. Meta's reviewers give an address they can read, and we make demo saved orders for it with `php artisan agent:review-saved-orders <their address> <operator>/<site>`. **To do once they name the address.**
- **A way to test checkout without real charges** (5.5): production takes real cards. A staging site with Stripe test mode (`AGENTIC_ALLOW_TEST_PAYMENTS`) can do it. **To do: decide whether to stand one up.**

## Risks to settle before submitting

1. **Guideline 1.1: "the connector must complete the task, including checkout"; sending the user to finish checkout on the web does not count.** Serviette's design hands the customer to its own payment page: nothing is charged by the connector. Meta may count that as not completing checkout. Ask them (or submit and see). Changing it would mean taking payment inside Muse, which Meta says it does with Stripe Link; that is a build, not a form answer.
2. **Guideline 4.7 (transactions)** wants seller, full price and currency, key terms, and the cancellation or refund policy shown before commitment, quoted/pending/confirmed/failed states, no duplicates, and receipts. The quote and payment page cover price, items, time and states; check the refund policy is stated on the payment page.
3. **Sensitive writes always need "Allow once" or "Deny" in Muse** (never "Always allow"). If Meta classes quoting a purchase as sensitive, every order asks the customer to allow it.
4. **Food, alcohol and age-restricted goods** are not mentioned in the guidelines we could read. Ask if anything applies.
5. **Muse's OAuth redirect address** is not documented. Serviette only accepts sign-in redirects to hosts on an allowlist (`AGENTIC_OAUTH_REDIRECT_HOSTS`: claude.ai, claude.com, chatgpt.com, chat.openai.com, platform.openai.com, plus loopback). Muse's callback host must be added once Meta says what it is, or sign-in will be refused.
6. **Whether the consumer Muse app accepts arbitrary MCP servers** is reported differently by different third parties. Meta's catalog is the route that matters.
