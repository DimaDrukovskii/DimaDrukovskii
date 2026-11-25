# OSIRIS — OSINT & Geospatial Intelligence Direction

**Type:** OSINT / geospatial intelligence dashboard concept associated with hackathon work  
**Status:** Concept / related codebase requires contribution details to be confirmed.  
**Attribution note:** The OSIRIS repository currently visible in the account credits another maintainer in its README. This portfolio entry therefore does not claim sole authorship of that upstream codebase or all of its features.

## Product direction

A unified intelligence interface that brings multiple public-data domains into one geospatial workspace: aviation, maritime activity, seismic events, fires, weather, news, satellite information, public Telegram feeds, and cyber/OSINT lookups.

## System concept

```text
Public data sources
  |-- aviation / maritime
  |-- seismic / fires / weather
  |-- news / satellites
  |-- public-channel feeds
  |-- DNS / WHOIS / IP / CVE
          |
          v
     API aggregation
          |
          v
  Geospatial data model
          |
          v
  MapLibre / WebGL interface
          |
          v
  Layers, filters, entity details
```

## Competencies represented by this direction

- Designing a multi-source data aggregation product.
- Thinking in terms of geospatial entities, layers, and viewport-aware loading.
- Integrating heterogeneous APIs and normalizing their outputs.
- Separating map rendering from API aggregation and intelligence tooling.
- Product decomposition for a data-heavy dashboard.

## What needs to be confirmed before making stronger claims

The precise hackathon name, individual role, owned components, and original code contributions should be documented before this is presented as a fully authored project. The current page intentionally describes the product direction and architecture without overstating authorship.

## Related technology

Next.js · TypeScript · MapLibre GL · WebGL · REST APIs · public data sources
