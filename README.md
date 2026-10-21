# Event Network

Search the public Event Network directory, rental listings, used-equipment offers and event venues. Check shared specialist calendar status and shared date-specific rental counts. The connector uses the hosted production MCP endpoint `https://mcp.eventnetwork.eu/mcp` without API keys or sign-in. No local server or backend source is included.

## Tools

search_companies, search_specialists, search_equipment, search_equipment_marketplace, search_locations, get_company_profile, get_specialist_profile, check_specialist_availability.

Equipment listed on a profile is not proof of operating skill. Unknown availability is not availability or zero stock. Venue largest-room values do not guarantee seating capacity. The service cannot book, send messages, reveal private contacts, exact addresses, coordinates, booking details or private calendar events.

## Support and privacy

- Website: https://eventnetwork.eu
- Support: https://eventnetwork.eu/support
- Privacy: https://eventnetwork.eu/privacy-policy
- Terms: https://eventnetwork.eu/terms

MIT covers these plugin configuration and instruction files only. Hosted service access and service data remain subject to Event Network terms and privacy policy.

## Installation and testing

For Claude chat/Cowork, upload the ZIP from Customize > Plugins > Add > Upload plugin, then connect Event Network on the plugin's Connectors tab. A custom connector can also use the same MCP URL directly. For Claude Code, run `claude --plugin-dir /absolute/path/to/claude-plugin`. Validate with `claude plugin validate /absolute/path/to/claude-plugin`.

## Public listing

Publish this folder as a dedicated public GitHub repository. An authorized owner submits the hosted server as an MCP connector at https://claude.ai/directory/manage, then submits this repository as a plugin bundle. Approval/publication is separate from preparing this package.
