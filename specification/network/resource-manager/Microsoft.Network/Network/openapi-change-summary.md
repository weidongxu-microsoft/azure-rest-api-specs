# OpenAPI change summary

## Comparison

This report compares the generated Network OpenAPI documents on
`copilot/test-net-core-legacy-version` with the original `test-net` branch.

- Original `test-net` commit: `9a31e08d1e35be8d412c0820e1b334f9700c4033`
- Merged Azure `main` commit: `11a9847b20ecda089434861c47293d9e7c31917a`
- Files compared: JSON documents under `stable/` and `preview/`

The comparison contains 998 changed files, with 158,808 added lines and 45
deleted lines. There are no changes under `preview/`.

## Changes from Azure `main`

### New `2025-09-01` API version

The upstream merge adds the complete stable `2025-09-01` Network API:

- 20 top-level OpenAPI documents
- 940 example documents
- New feature documents for `firstPartyServiceTag` and the existing
  `interconnectGroup` feature
- VMSS feature documents generated from the main Network TypeSpec project

### Existing `2025-05-01` and `2025-07-01` documents

The upstream merge updates 18 documents in `2025-05-01` and 19 documents in
`2025-07-01`.

The common change is the service description:

```text
APIs to manage web application firewall rules.
```

becomes:

```text
APIs to manage Microsoft Azure network resources.
```

The following additional documentation-only corrections are included:

- `loadBalancer.json`: clarifies `enableConnectionTracking` behavior and the
  precedence of the frontend IP configuration setting.
- `serviceGateway.json`: corrects the create-or-update request parameter
  descriptions.

### Captured `2018-10-01` VMSS schema

`stable/2018-10-01/vmssNetwork.json` changes by 55 additions and 2 deletions.
These changes come from updates to the latest shared Network models captured by
the long-standing VMSS `2018-10-01` schema exception:

- Adds `FrontendIPConfigurationProperties.enableConnectionTracking`.
- Adds `IpTag.firstPartyServiceTagId`, constrained to
  `Microsoft.Network/firstPartyServiceTags` resource IDs.
- Adds the extensible `LoadBalancerMode` definition and
  `LoadBalancerProperties.mode`.
- Adds the `Service` load balancer SKU value.
- Updates the `LoadBalancingRuleProperties.enableConnectionTracking`
  description.
- Adds the read-only `PublicIPAddressProperties.upgradedToV2` property.

No VMSS paths or operations are added or removed.

## Recompilation-only differences

After merging upstream `main`, recompiling the Network TypeSpec project changes
five files relative to the automatic Git merge result:

- The four `2025-05-01` and `2025-07-01` VMSS feature documents receive the
  updated Network service description from upstream.
- `stable/2025-09-01/virtualNetwork.json` uses the existing TypeSpec wording
  "The name of the ip configuration." instead of "The name of the ip
  configuration name."

The consolidated `stable/2018-10-01/vmssNetwork.json` document is byte-for-byte
unchanged by recompilation relative to the merged baseline.

## VMSS API-version validation

Replacing the TCGC legacy decorator with
`Azure.Core.Legacy.overrideApiVersion("2018-10-01")` does not change the
OpenAPI API version. All generated VMSS documents continue to declare
`info.version` as `2018-10-01`:

| Document | Operations | `info.version` |
| --- | ---: | --- |
| `stable/2018-10-01/vmssNetwork.json` | 8 | `2018-10-01` |
| `stable/2025-05-01/vmssNetworkConfiguration.json` | 3 | `2018-10-01` |
| `stable/2025-05-01/vmssPublicIpAddress.json` | 3 | `2018-10-01` |
| `stable/2025-07-01/vmssNetworkConfiguration.json` | 3 | `2018-10-01` |
| `stable/2025-07-01/vmssPublicIpAddress.json` | 3 | `2018-10-01` |
| `stable/2025-09-01/vmssNetworkConfiguration.json` | 3 | `2018-10-01` |
| `stable/2025-09-01/vmssPublicIpAddress.json` | 3 | `2018-10-01` |

The VMSS operations continue to reference the standard ARM
`ApiVersionParameter`; the document-level version remains pinned to
`2018-10-01`.
