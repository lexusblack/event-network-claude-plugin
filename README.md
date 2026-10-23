# Event Network

Search public Event Network companies, specialists, rental and used-equipment listings, jobs, venues, purchase groups and technical riders. Public tools work without sign-in. For protected account tools, Claude connects to New Systems OAuth and reads only data the signed-in account is allowed to access. The connector uses the hosted production MCP endpoint `https://mcp.eventnetwork.eu/mcp`; no API key or local server is included.

## Tools

Public tools: `search_companies`, `search_specialists`, `search_equipment`, `search_equipment_marketplace`, `search_locations`, `search_jobs`, `get_job_details`, `get_equipment_details`, `get_technical_plans`, `list_filter_values`, `check_room_availability`, `get_location_profile`, `get_company_profile`, `get_specialist_profile`, and `check_specialist_availability`.

OAuth-protected read-only tools: `list_account_contexts`, `get_my_jobs`, `get_my_job_detail`, `get_my_listings`, `find_matching_jobs`, `get_my_calendar`, `search_purchase_groups`, and `search_technical_riders`. These request the `eventnetwork:read` scope and require the user's New Systems sign-in and consent. Ask which personal/company context to use when more than one is available. No tool publishes, applies, books, messages, or edits data.

## Sign-in and consent

Public directory searches do not require an account. When Claude first calls a protected account tool without an authorized session, it should open the New Systems sign-in and consent flow in a browser. Sign in or create your New Systems account there, then review and approve the read-only `eventnetwork:read` permission before private account data is returned.

For the Claude connector, choose **Sign in when needed** and **Register automatically**. Claude uses OAuth authorization code with PKCE and Dynamic Client Registration (DCR) to create its public OAuth client automatically; the package contains no pre-created client ID or client secret. DCR registers Claude as a client; it does not create or sign in to your New Systems user account. New Systems rotates refresh tokens so Claude can renew access after an access token expires.

If a protected call returns an authentication error without opening the browser flow, reconnect Event Network from Claude's connector settings and try the protected call again. Do not paste passwords or tokens into chat.

Equipment listed on a profile is not proof of operating skill. Unknown availability is not availability or zero stock. Venue largest-room values do not guarantee seating capacity. The service does not reveal private contacts, exact addresses, coordinates, booking details or private calendar events.

## Support and privacy

- Website: https://eventnetwork.eu
- Support: https://eventnetwork.eu/support
- Privacy: https://eventnetwork.eu/privacy-policy
- Terms: https://eventnetwork.eu/terms

MIT covers these plugin configuration and instruction files only. Hosted service access and service data remain subject to Event Network terms and privacy policy.

## Installation and testing

For Claude chat/Cowork, upload the ZIP from Customize > Plugins > Add > Upload plugin, then connect Event Network on the plugin's Connectors tab. In connector authentication settings, use **Sign in when needed** and **Register automatically**. A custom connector can also use the same MCP URL directly. For Claude Code, run `claude --plugin-dir /absolute/path/to/claude-plugin`. Validate with `claude plugin validate /absolute/path/to/claude-plugin`.

## Public listing

Publish this folder as a dedicated public GitHub repository. An authorized owner submits the hosted server as an MCP connector at https://claude.ai/directory/manage, then submits this repository as a plugin bundle. Approval/publication is separate from preparing this package.
