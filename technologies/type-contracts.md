# Type Contracts Across Boundaries

Types are generated from whatever owns the truth, never written twice by hand. Schema drift should be a build failure, not a production incident.

## Generation sources
| Boundary | Source of truth | Generated |
|---|---|---|
| Spring Boot → TS client | springdoc OpenAPI spec | TS types/client via `openapi-typescript` |
| Supabase → TS | Database schema | `supabase gen types typescript` |
| Database → Kotlin | Flyway migrations | Aggregate mappings, checked by Testcontainers tests |

## Rules for agents
- Generated files are committed and regenerated in CI. If CI regenerates and the diff is non-empty, the build fails — that is the drift alarm.
- Never hand-edit a generated file. Never hand-write a type that could be generated.
- Generation gives you *compile-time* safety only. Runtime data still needs validating: parse every API response, env var, stored blob and message payload with **Zod** at the boundary, then pass the parsed type inward. See `../patterns/illegal-states-unrepresentable.md`.
- Validate once, at the edge. Do not re-validate the same value at every layer.
- Version the API and add fields additively. Do not break a client to tidy a name.
- The generated client belongs in an adapter, not in components or domain code — `../patterns/anti-corruption-layer.md`.

## Deviate when
A one-off script or a spike. Say that it is a spike.

## Smells
A hand-written interface mirroring a database table, a TS type and a Kotlin data class edited in parallel, `as ApiResponse` on a `fetch` result, a generated file with manual edits, drift discovered by a user.
