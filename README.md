# Awesome-Graphql-Clients

# Top GraphQL Clients Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Normalized Caching, Type-Safe Queries & Self-Hosted Client Libraries*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **GraphQL Clients**. These libraries handle the client-side complexity of GraphQL—sending queries, caching responses, managing loading states, and synchronizing data after mutations—so frontend developers can focus on building UIs instead of data plumbing.

**Examples** include Apollo Client, Relay, urql, TanStack Query (React Query), SWR, RTK Query, Graffle, and Houdini (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, framework-specific bindings, and transparent caching strategies—ideal for React, Svelte, and framework-agnostic teams that need control over their data layer. The open-source landscape is anchored by **Apollo Client** (the feature-rich standard with normalized caching and ~4M weekly downloads), **Relay** (Meta's compiler-driven enterprise client), and **urql** (the lightweight, exchange-based alternative at ~1M weekly downloads), with **TanStack Query** serving teams that want GraphQL treated as generic async data and **Graffle** offering a minimal, typed HTTP client.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Apollo Studio (GraphOS)](https://studio.apollographql.com/)**  
  Apollo's commercial platform for schema registry, usage reporting, and federation management. The open-source Apollo Client integrates with Studio for schema checks and metrics, but the client itself remains MIT licensed. Enterprise-tier pricing for teams needing schema governance and federation.

- **[GraphQL Editor (Cloud)](https://graphqleditor.com/)**  
  Visual schema design and collaboration platform with a free tier. Not a client—included for ecosystem context as a schema-focused SaaS tool.

## Open-Source GitHub Projects

- **[Apollo Client](https://github.com/apollographql/apollo-client)**  
  The most widely adopted GraphQL client for React (~4M weekly downloads) and the reference implementation for normalized caching . **Apollo Client 4.x** (shipped September 2025) split React bindings into `@apollo/client/react`, swapped `zen-observable` for RxJS, and made ESM-first packaging standard . **4.1** added full `@stream` directive support and array support for `useFragment`, while **4.2** introduced type-safe default options and event-based refetching (window focus, network reconnection) via `RefetchEventManager` . **Strengths**: built-in normalized cache, DevTools, subscriptions, optimistic UI, and the largest ecosystem. **Trade-offs**: ~40–47KB gzipped bundle and complex cache configuration (`typePolicies`, `keyFields`, merge functions) that can produce subtle bugs if misconfigured . Best for applications with complex entity relationships where the same object appears across multiple queries and must stay synchronized.

- **[Relay](https://github.com/facebook/relay)**  
  Meta's compiler-driven GraphQL client, the most opinionated and performance-focused option. **Requires** the Relay Compiler and server schema conventions (Node interface, Connection spec for pagination). **Strengths**: ahead-of-time compilation produces small artifacts with aggressive dead-code elimination; fragment colocation is enforced by the compiler, preventing implicit coupling; Suspense and `@defer`/`@stream` integrate cleanly with fragment composition . **Trade-offs**: steepest learning curve; assumes server-side schema influence; local state must live outside Relay (Zustand, Redux) . Best for large-scale applications with dedicated GraphQL infrastructure teams where compile-time correctness justifies the setup cost.

- **[urql](https://github.com/urql-graphql/urql)**  
  The lightweight, exchange-based alternative (~1M weekly downloads). **Architecture**: behavior is composed from middleware-like exchanges; **document caching is the default**, with normalized caching available opt-in via `@urql/exchange-graphcache` . **urql 5.0** (React binding) on `@urql/core` 6.x simplified custom-exchange authoring (`composeExchanges` handles `share()` internally), added `TypedDocumentNode` inference, and exported previously-missing SSR types . **Bundle size advantage**: ~14KB + 12KB (Graphcache) vs Apollo's ~47KB . **Gotcha**: `@urql/core` 6 sends short queries as GET by default; servers requiring POST need `preferGetMethod: false` . Best for bundle-sensitive applications and teams that want fine-grained control over client behavior without Apollo's cache complexity.

- **[TanStack Query (React Query)](https://github.com/TanStack/query)**  
  The dominant data-fetching library (~5M weekly downloads), primarily used for REST but viable for GraphQL as a **pattern rather than native integration** . Write a function that sends a GraphQL request (via `graphql-request` or `fetch`) and pass it to `useQuery`—TanStack Query handles caching, deduplication, background refetching, and loading states. **Trade-off**: cache is keyed by `queryKey`, not entity identity—no normalized caching, no automatic cross-query synchronization after mutations . Best for teams already using TanStack Query for REST that want a single data layer without adding a second cache, and for applications where normalized caching provides no real benefit.

- **[SWR](https://github.com/vercel/swr)**  
  Vercel's React hooks library for data fetching with a stale-while-revalidate strategy. Can wrap GraphQL requests with `graphql-request` or similar. **Lightweight** and well-integrated with Next.js. No normalized caching or GraphQL-specific features. Best for simple GraphQL queries in Next.js applications where a full client would be overkill.

- **[RTK Query](https://github.com/reduxjs/redux-toolkit)**  
  Redux Toolkit's data fetching and caching solution. Can handle GraphQL queries as async endpoints, integrating GraphQL into existing Redux stores. No normalized GraphQL cache. Best for teams already committed to Redux that want GraphQL without adding a separate client library.

- **[Graffle (formerly graphql-request)](https://github.com/graffle-js/graffle)**  
  A minimal GraphQL client for JavaScript with no caching, no UI bindings, and no framework assumptions. **~6k GitHub stars**. Sends queries and returns typed data—that's it. **Best for server-side usage** (Next.js Server Components, scripts, CLIs) where a client-side cache is unnecessary or harmful . Often paired with TanStack Query for client-side caching when needed.

- **[Houdini](https://github.com/HoudiniGraphQL/houdini)**  
  A compiler-first GraphQL client designed for **Svelte** (with a React plugin also available). Features fragment colocation, generated types, and a "disappearing" runtime that produces minimal client artifacts. **Active development** with the `houdini-lsp` language server for editor intelligence . Best for Svelte developers who want Relay-like compile-time guarantees without Relay's complexity.

### Additional Strong Open-Source Options

- **graphql-hooks** — Minimal GraphQL client with a small footprint (~7KB) and simple caching. Best for lightweight React applications where Apollo's feature set is unnecessary.
- **Villus** — A tiny (~3KB) and fast GraphQL client for Vue 3. Best for Vue developers who want a dedicated GraphQL client without Apollo's Vue integration overhead.
- **Frameworks for building custom systems**: Use **Apollo Client** when normalized caching is essential and bundle size is acceptable. Choose **urql** for a lighter footprint with comparable features and optional Graphcache. Use **Relay** only when you control the server schema and need compile-time fragment guarantees. Pair **TanStack Query** with **Graffle** for a simple, REST-consistent data layer. Use **Graffle** alone in Server Components where no client cache is needed.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- **Normalized caching is the primary differentiator**: Apollo and urql (with Graphcache) provide it; TanStack Query, SWR, and Graffle do not. If the same entity appears in multiple queries and must stay synchronized, normalized caching saves significant manual invalidation work .
- **Bundle size matters for public-facing apps**: Apollo (~40–47KB gzipped) vs urql (~14KB + 12KB Graphcache) vs Graffle (~5KB). For performance-sensitive sites, the lighter options may be sufficient .
- **TanStack Query is a pattern, not a native GraphQL client**: it treats GraphQL as generic async data, losing normalized caching and subscription support. It excels at incremental REST-to-GraphQL migration .

---

**Made for frontend engineers, full-stack developers, and teams building data-driven applications with GraphQL.**  
Let's make GraphQL clients more open, understandable, and appropriately sized for their use case.
