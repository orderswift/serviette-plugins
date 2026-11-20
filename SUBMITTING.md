# Before submitting

Checked locally: `claude plugin validate .` and `claude plugin validate ./claude` pass. Nothing here has been tried in either assistant or submitted yet, and the ChatGPT package has not been through OpenAI's validator.

## Both

- [ ] Make this repository **public** (Claude's directory needs that before a listing goes live).
- [ ] Decide the **licence** (MIT is a placeholder) and the **author / developer name** (now "Serviette"; OpenAI checks it against the verified publisher identity, so it may need to be the company's legal name).
- [ ] Check that https://withserviette.com/privacy and /terms say what the plugins' READMEs say (what is sent, to whom, how long it is kept). OpenAI requires the policy to list the categories of personal data, purposes, recipients, retention and user controls.
- [ ] Create a **support page** (`supportURL` in `chatgpt/plugin.json` points at https://withserviette.com/support, which does not exist yet).
- [ ] Record a short **demo video** for ChatGPT review and put its URL in `review.demo_recording_url`.

## Claude

1. Developer portal (claude.ai/directory/manage, paid plan, an Owner on Team/Enterprise): **Submit new > Plugin bundle**, enter this repo and plugin path `claude`, validate, fill in Data handling and Compliance.
2. Also submit the MCP server as an **MCP connector** (Anthropic asks for this even when a plugin references the server): URL `https://agent.withserviette.com/agent/mcp`, OAuth, authentication "Required when the server asks" (the sign-in is lazy), a title and read/destructive annotations on every tool (already set), one-liner, description, categories, documentation URL, privacy URL, support contact, icon, URL slug (permanent).
3. Test it first: `claude --plugin-dir ./claude`, and the server in MCP Inspector and as a custom connector.

## ChatGPT

1. Org owner (or a member with Apps Management Write) verifies the organisation at platform.openai.com/settings/organization/general. The developer name must match.
2. Zip the **contents of `chatgpt/`** (no secrets, no `.app.json`, no hooks) and upload it at platform.openai.com/plugins.
3. Connect the MCP server in the portal (URL above, authentication: mixed). Prove the domain by serving the portal's token, as plain text, at `https://agent.withserviette.com/.well-known/openai-apps-challenge` (this needs a route on the agent host).
4. Review information: five positive and three negative test cases are in `plugin.json`. Reviewer credentials go in the portal, not the package (the anonymous tier needs none; the test ends at the payment link).
5. Questions to put to OpenAI, because their docs do not settle them:
   - Is food collection "physical goods" for the commerce rule, and is alcohol allowed? (Commerce is declared in `review.commerce`.)
   - Does `auth.type: "mixed"` with `client.mode: "dcr"` work for a server where only two tools need sign-in, and how are those two tools' 401 challenges handled in the scan? (The server also marks them with `securitySchemes`.)
   - Is a plugin without the optional skill accepted, and is the `streamable-http` transport name right?
   - The guidelines bar collecting "MFA/OTP codes". The server's saved-orders code route (`request_saved_orders_code`, then the customer reads out a six-digit code) could be read that way. The sign-in route (`list_my_saved_orders`) does not use it. Consider switching the code route off (`AGENTIC_SAVED_ORDERS_ASSISTANT=false`) before submitting.
   - The pay page is on the same domain as the server and is not embedded in any UI, which is what the checkout rule asks for.
