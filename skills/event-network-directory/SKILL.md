---
name: event-network-directory
description: Search Event Network companies, specialists, rental and used-equipment listings, public venues, and shared availability using the Event Network MCP tools.
---

# Event Network directory workflow

Use the Event Network MCP tools whenever the user asks for current companies, specialists, equipment listings, public profiles, or specialist availability. Do not fabricate results from general knowledge. Respond in the language used by the user and include returned profile links when available.

## Company searches

- Call `search_companies` with the requested profile city and country when known.
- For a rental request, use relevant search words such as `rental` or the user's local-language equivalent, then inspect the returned `companyType`, specializations, and public profile evidence.
- The directory does not define a universal rental category in this tool contract. Do not label a company a rental company based only on a loose keyword match; call it a candidate and state the evidence if the profile is ambiguous.
- A city's company filter matches the city saved on the profile, not a geographic radius.

## Specialist searches and equipment skill claims

- Call `search_specialists` for public specialist profiles. Use `city` for the profile city, `worksInCountries` for country-level work coverage, `specializations` for Event Network specialization keys, and `skills` only for public certificate/skill names.
- For a console or software such as grandMA3, search for the exact term in public profile data and listed equipment as appropriate. A returned equipment entry proves only that the item appears in the profile's active equipment list; it does not prove that the specialist can operate it. State this distinction unless a returned skill, certificate, or profile statement explicitly confirms proficiency.
- Use the returned `specialistId` for follow-up profile and availability calls. Do not use an ID guessed from a name.

## Public equipment listings

- Call `search_equipment` with `manufacturer` and `model` in separate fields when both are known. For example, search Robe MegaPointe with `manufacturer: "Robe"` and `model: "MegaPointe"`. The `query` field searches model text only; do not combine the manufacturer and model in `query`.
- Group listings by returned `companyId` when the user asks which companies have the equipment. Call `get_company_profile` only when more company details are needed.
- A result is an active public listing. Report `quantityTotal` as the published listing quantity and `availabilitySharingEnabled` as the company’s sharing setting. These values do not reveal a reservation.
- When the user asks about a date, pass `dateFrom`, `dateTo` when a range is requested, and the locality’s IANA timezone. If only one date is requested, pass it as `dateFrom`; `dateTo` defaults to that date. The maximum range is 31 inclusive dates.
- Report `quantityAvailable` only when `availabilityStatus` is `available` or `unavailable`. `unknown` means no confirmed quantity was returned; never turn it into zero or infer availability from a general company calendar. The tool returns aggregate quantities only, not booking details.

## Used-equipment marketplace

- Use `search_equipment_marketplace` for second-hand equipment being offered for sale. Use `search_equipment` for rental listings; do not mix the two results.
- When the user gives both manufacturer and model, pass them separately as `manufacturer` and `query` (the marketplace query matches the listing name/model).
- The marketplace returns active public listings and may include listed price, condition, city, and a public seller company name. It omits personal seller contacts and quantity counts. Do not infer stock quantity or date-specific availability for sale listings.

## Public venues and geographic searches

- Use `search_locations` for venues. Pass a public type name such as `hotel`, `minStars` for a minimum rating, and `minCapacity` for a minimum largest-room value.
- For a request such as “a hotel with at least 4 stars for 500 people near Warsaw,” search with `locationType: "hotel"`, `minStars: 4`, `minCapacity: 500`, `nearCity: "Warszawa"`, `country: "PL"`. The geographic radius defaults to 50 km; use `radiusKm` when the user specifies another radius.
- `minCapacity` filters Event Network’s `biggest_room` field. Call it the largest-room value or a capacity proxy; it does not verify the seating layout or guarantee that 500 people fit. Recommend confirming the exact room setup with the venue.
- City-radius searches resolve a public city center through Event Network’s location-search service. If the city cannot be resolved unambiguously, report that and ask which city/country to use. The result does not expose an exact distance for each venue.
- Return the venue’s name, type, stars, largest-room value, city/region, and profile link when present. Do not expose exact street addresses, coordinates, private contacts, or internal owner IDs.

## Specialist availability and location

- First search for candidate specialists. For a job in Germany, `worksInCountries: ["DE"]` means the profile says the specialist works in Germany; it does not mean Berlin-specific coverage.
- The `city` search matches the profile's saved city. It does not verify travel to the job location. The availability tool checks calendar status and does not accept a venue or city parameter; disclose this when the user asks about a specific job location.
- Call `check_specialist_availability` using each candidate's returned `specialistId`, inclusive `dateFrom` and `dateTo` in `YYYY-MM-DD`, and the IANA timezone for the requested locality (for Berlin, `Europe/Berlin`).
- Report `available` only for status `available`, `busy` only for `busy`, and explain that `unknown` cannot be confirmed. Never describe `unknown` as free.
- If the user omits the year and context does not establish it safely, ask for the year. If the date has passed this year, do not silently change it to next year.

## Search quality, pagination, and privacy

- Search results are public directory matches, not an endorsement or independent validation. Separate returned facts from your interpretation.
- If `nextPage` is non-null and more results are needed, continue with that page number; do not repeat page one.
- Use only the public fields returned by the MCP tools. Do not seek or infer private contacts, exact addresses, calendar event details, or account data. Do not infer an available equipment quantity when the result is unknown.
- This MCP is read-only. Do not claim to book equipment, contact a company, or change an Event Network record.
