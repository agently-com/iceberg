# Patches applied on top of the release tag

`kafka-connect-runtime.yml` applies every `*.patch` here (`git apply`) to the checked-out
`apache-iceberg-<version>` tag before building the runtime zip, when the run's `suffix` input is
non-empty; the release tag carries that suffix. Keep a patch to the main-source hunks of one
upstream commit — the build skips tests — and name it after the upstream PR.

| Patch | Upstream | Why the fork needs it |
|---|---|---|
| `0001-kafka-connect-uuid-schema-mapping-16828.patch` | apache/iceberg#16828 (`3c604fb607`, merged 2026-06-25, after the 1.11.0 tag of 2026-05-15) — `SchemaUtils.toIcebergType` maps a Connect STRING schema named `uuid` to the Iceberg `uuid` type | the lakehouse bronze contract types MySQL `binary(16)` as `uuid`; the fleet's converter emits the `uuid`-named schema, and without this hunk the sink auto-creates the column as `string` for good (agently-com/agently-teams#1221) |

Drop a patch the day the tag the fork builds contains the upstream commit.
