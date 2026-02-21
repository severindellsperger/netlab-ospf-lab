# netlab-ospf-lab

A NetLab lab demonstrating OSPF multi-area functionality, inspired by the [netlab OSPF examples](https://github.com/ipspace/netlab-examples/tree/master/OSPF).

## Topology

The lab uses FRRouting (`frr`) as the default device and covers the following OSPF area types:

| Area | Type | Description |
|------|------|-------------|
| 0 | Backbone | LAN switch connecting `abr1` and `abr2`, enabling DR/BDR election |
| 1 | Standard | Normal OSPF area with internal routers (`r1a`, `r1b`) |
| 2 | Stub | Stub area — no external (Type 5) LSAs; `r2b` has no direct backbone connectivity |
| 3 | Totally Stub | No inter-area (Type 3) or external (Type 5) LSAs; `r3b` has no direct backbone connectivity |
| 4 | NSSA | Not-so-stubby area — allows external routes via Type 7 LSAs; `r4b` has no direct backbone connectivity |
| 5 | Totally NSSA | NSSA with no inter-area (Type 3) LSAs; `r5b` has no direct backbone connectivity |

### Design highlights

- **Backbone (Area 0):** `abr1` and `abr2` are connected via a LAN segment (`type: lan`), which forces a DR/BDR election instead of using a point-to-point link.
- **Area Border Routers (ABRs):** `abr1` is the ABR for areas 1 and 2; `abr2` is the ABR for areas 3, 4, and 5.
- **Internal routers:** Each non-backbone area includes two routers. The `b`-suffix router (e.g., `r1b`, `r2b`, …) has no interfaces in area 0, demonstrating routers with no direct backbone connectivity.

## Prerequisites

- [NetLab](https://netlab.tools/) installed
- A supported virtualisation provider (e.g., `clab`, `libvirt`)
- FRRouting container/VM image available

## Usage

```bash
netlab up
```

To connect to a device:

```bash
netlab connect <node-name>
```

To tear down the lab:

```bash
netlab down
```
