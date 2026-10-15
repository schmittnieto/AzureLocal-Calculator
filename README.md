# AzureLocal-Calculator

AzureLocal-Calculator is a repository that provides interactive, web-based calculators for estimating compute, storage and cost in an Azure Local environment. The current version is the **Azure Local Calculator V3**, which sizes all three on a single page. The separate Storage, CPU and Pricing calculators stay in the repo as V2 (previous) and V1 (legacy).

The calculators are organized under the `Calculators` directory and are also available for interactive use on my blog: [Azure Local Calculator](https://schmitt-nieto.com/azurelocal-calculator/).

> [!IMPORTANT]
> The original Storage Calculator (V1) is now outdated. [Armin](https://www.linkedin.com/in/aoberneder/) has created a much better dedicated tool. I recommend using his calculator for storage sizing: [s2d-calculator.com](https://s2d-calculator.com/).
> The Storage Calculator V2 included in this repo offers an improved in-house alternative with multi-tier and multi-platform support.

---

## Azure Local Calculator V3 (current)

V3 puts compute, storage and cost sizing on one page. You pick a deployment type and size the workload, and the node count and physical cores from the compute step feed the storage and cost steps. All three estimates describe the same cluster, so there is nothing to copy between calculators.

| Version | File | Description |
|---------|------|-------------|
| V3 | `azurelocal-calculator-v3.html` | Single-page calculator that combines CPU, storage and pricing in five steps, with planning checks per deployment type and a 3D view of the hardware. |

The page has five steps:

1. **Deployment type**: sets the node limits, the storage model and the host fee.
2. **Compute**: virtual machines in, physical cores and nodes out.
3. **Storage**: Storage Spaces Direct, external SAN or both, sized for the nodes from step 2.
4. **Cost**: hardware, licensing, related costs and Azure services for the cluster from step 2.
5. **Solution**: the hardware and the results as interactive 3D views.

A summary bar stays at the top while you scroll. It shows the deployment type, the node count, the physical cores, the usable storage and the 3-year total.

**V3 key features:**
- **Deployment types** with their minimum Azure Local version:
  - **Hyperconverged**: 1 to 16 nodes with Storage Spaces Direct
  - **Rack aware cluster** (2510 or later): 1+1 to 4+4 machines across two zones, plus the storage NIC speed (10 or 25 GbE)
  - **Hyperconverged with external SAN** (2604 or later): Storage Spaces Direct plus SAN volumes over Fibre Channel or iSCSI
  - **Disaggregated**: 1 to 64 compute nodes on SAN storage only
  - **Disconnected operations** (2602 or later): the workload cluster plus the dedicated management cluster. Clear the management cluster option when it already exists and is already billed
  - **Multi-rack** (2511 or later) and **Small form factor** (preview): planning facts and a cost estimate only
- **Planning checks** next to the deployment type list the requirements and limits of the selected type
- **Work out** selector: switch Compute, Storage or Cost off to work on the other parts alone. With Compute off, you enter the node count and the cores per node yourself
- **Compute**: VM count, vCPUs per VM, vCPU to core ratio, host overhead and N+1, node types from the Azure Local solutions catalog, socket count and the "I know my nodes" and "I know my CPU" modes with CPU recommendation cards. For disconnected operations the management cluster gets its own node type, profile (standard or datacenter), ratio and N+1 setting
- **Storage**: "I know my drives" or "I have a capacity target" for Storage Spaces Direct with the resiliency options. External SAN takes the vendor, Fibre Channel or iSCSI, one LUN per CSV, data reduction and free space headroom. Disconnected operations adds the data drives of the management cluster
- **Cost**: currency (EUR, USD, GBP, CHF), node, switch, management node and SAN prices, the host fee of the selected model (L1, L2, OEM license with external storage or L3 with your quoted rate), Windows Server guest licensing, Azure Hybrid Benefit for L1, the 60-day trial, related costs, AVD and SQL Managed Instance
- **Solution**: a 3D hardware view with the racks, nodes, failover node, management nodes, switches and SAN array, plus 3D charts for core allocation, cores per node, volume distribution, the SAN capacity plan and cost. Drag to turn a view, double-click to reset it, hover or tap a part for its values
- **Full overview** table with every calculation
- **Sources**: superscript numbers next to the values point to a numbered list of the Microsoft Learn pages and catalog entries they come from
- **Import from ODIN**: Sizer and Designer exports set the deployment type, nodes, workload, CPU, drives, resiliency, SAN connectivity, switches and AVD vCPUs. ODIN multi-rack designs map to Multi-rack, and Microsoft 365 Local designs come in as a regular cluster
- Light and dark mode follow the page theme, and the layout adapts to the width of its container

The formulas come unchanged from the three V2 calculators, and the CPU database, the catalog node types and the ODIN parser are copied from them. V3 is a single self-contained HTML file. Its styles are scoped to `#alc-root`, every element ID starts with `alc-` and the file is wrapped in `{% raw %}`, so it can be pasted into a Jekyll page as is.

Limitations:
- There is no PDF export in this version.
- Multi-rack and small form factor aren't sized. Microsoft sells multi-rack as a fixed bill of materials and small form factor on a short list of devices, so the page shows planning facts and a cost estimate for them.
- Microsoft 365 Local has no entry of its own, because a certified partner sizes that workload on hyperconverged or disaggregated hardware.
- The storage model is all-flash with a single drive type.
- In rack aware clusters, N+1 reserves one node. It doesn't reserve a full rack.

---

## Storage, CPU and Pricing Calculators (V1 and V2)

These are the separate calculators that came before V3. V2 is the previous version and V1 is legacy.

### Storage Calculator

Estimates raw, effective, and usable storage capacity based on cluster configuration, disk layout, and resiliency settings.

| Version | File | Description |
|---------|------|-------------|
| V1 | `StorageCalculator.html` | Slider-based calculator for Azure Local with Express Settings. Estimates raw, effective, and usable capacity given node count, disk count, and capacity per disk. |
| V2 | `StorageCalculatorV2.html` | Fully redesigned calculator with platform selection, multi-tier storage support, resiliency option cards, visual charts, PDF export, and print-friendly layout. |

**V2 key features:**
- Platform support: Azure Local, Windows Server 2019 / 2022 / 2025
- Single Node and multi-node cluster modes (2-16 nodes)
- Storage types: Full-Flash (NVMe/SSD), 2-Tier (Cache + Capacity), 3-Tier (Cache + Performance + Capacity)
- Resiliency options per platform and node count (Mirror, Parity, Mirror-Accelerated Parity)
- **Deployment Type** selector:
  - **Hyperconverged** (Storage Spaces Direct)
  - **Hyperconverged with external SAN**: Storage Spaces Direct plus SAN volumes
  - **Disaggregated**: SAN only, up to 64 nodes, internal drives are boot drives
  - **Disconnected operations (ALDO) management cluster**: checks the standard (6 drives) or datacenter (8 drives) minimums of at least 2 TB per drive and 3 nodes, and reserves the 2 TB disconnected operations infrastructure volume
- **External SAN planning** (Azure Local 2604 or later): supported arrays from the Microsoft list (Dell PowerStore, Everpure FlashArray, Hitachi VSP, HPE Alletra MP 10000, Lenovo ThinkSystem DS/DM/DG, NetApp ONTAP) with their MPIO registration, Fibre Channel or iSCSI host requirements, LUN layout (one LUN per CSV), infrastructure volumes, free space headroom and data reduction to estimate the physical array capacity
- Detailed results with raw, effective, and usable capacity breakdown
- Interactive 3D charts (capacity donut, volume distribution) with tooltips, clickable legend and drag to rotate
- PDF export and browser print support

---

### CPU Calculator

Estimates the physical CPU requirements for a given virtual workload across an Azure Local or Windows Server cluster.

| Version | File | Description |
|---------|------|-------------|
| V1 | `CPUCalculator.html` | Slider-based calculator for VM count, vCPU-to-core ratio, management overhead, node count, and processor specs. |
| V2 | `CPUCalculatorV2.html` | Redesigned calculator with two calculation modes, CPU recommendation cards, socket configuration, and HA reservation support. |

**V2 key features:**
- Two calculation modes:
  - **Nodes to CPU**: provide the number of nodes and get CPU model recommendations
  - **CPU to Nodes**: select a CPU model and get the recommended number of nodes
- **Node Type** selector with the systems listed as "Current (2026 or later)" in the [Azure Local solutions catalog](https://azurelocalsolutions.azure.microsoft.com/#/catalog): limits sockets and node count to the selected system and only offers the CPU models it can use (matching CPU generation, published cores-per-socket options and socket support). Sizing then uses the smallest compatible CPU that fits, and results and charts recalculate automatically when the node type, the CPU or any input changes
- **Cluster Type** selector: hyperconverged, disaggregated (external SAN, up to 64 nodes, only catalog systems with that architecture) or the **disconnected operations (ALDO) management cluster**, which sizes the fixed control plane appliance (24 vCPUs) with at least 24 physical cores per node, a host reservation of at least 20% of the cores, 3 nodes for production and only the catalog systems with the Disconnected operations capability
- CPU socket selector (single socket / dual socket)
- N+1 High Availability capacity reservation toggle
- Management overhead and vCPU-to-core ratio configuration
- CPU recommendation cards showing fit, tight, or insufficient status. The recommended CPU is highlighted, and clicking any other card (including a smaller one) sizes the cluster with it; when the CPU is too small, the charts show the missing cores
- Interactive 3D charts (core allocation donut, per-node distribution) with tooltips, clickable legend and drag to rotate
- PDF export and browser print support

---

### Pricing Calculator

Estimates the total cost of ownership (TCO) for an Azure Local deployment, including hardware, licensing, related services, and Azure-specific workloads.

| Version | File | Description |
|---------|------|-------------|
| V1 | `PricingCalculator.html` | Slider-based calculator covering infrastructure, licensing (host fee, Windows Server fee), and basic Azure service costs. |
| V2 | `PricingCalculatorV2.html` | Full redesign with multi-currency support, granular cost categories, Azure Hybrid Benefit options, Azure service pricing, and detailed cost charts. |

**V2 key features:**
- Multi-currency support: EUR, USD, GBP, CHF
- **Infrastructure**: nodes and switches (one-time cost)
- **SAN System** (L2 models): SAN vendor, physical usable capacity, array price (one-time) and support (monthly), shown in the overview with the price per TB and in gray in both breakdown charts
- **Licensing**:
  - Azure Local deployment models: L1 hyperconverged without external storage, L2 disaggregated with SAN storage, L2 hyperconverged with external storage and L3 disconnected operations
  - Azure Local Host Fee: 10/core/month for L1, 20.10/core/month for both L2 variants and a user-provided rate for L3
  - OEM license with external storage pricing at 10/core/month
  - Azure Hybrid Benefit host fee waiver restricted to eligible L1 deployments (not available for disaggregated or any other L2 or L3 deployment)
  - Free 60-day trial applied to eligible term estimates
  - L3 includes the dedicated ALDO management cluster: its nodes are added to the hardware cost and its cores to the billed cores (3 nodes with 24 cores by default), without the Windows Server fee and without trial on the L3 host fee (annual capacity term). Azure Virtual Desktop is not available with disconnected operations, so the AVD fields are disabled for L3
  - Windows Server Datacenter Fee (23.30/core/month), waivable via Hybrid Benefit
  - Custom Windows license pricing per node (monthly + one-time)
- **Related costs** (one-time and monthly per category):
  - Backup
  - Logs / Monitoring
  - Installation
  - External Partner Management
  - Other
- **Azure Local Services**:
  - Azure Virtual Desktop (AVD): vCPUs and monthly usage hours
  - SQL Managed Instance (SQLmi): vCores, usage hours, tier (General Purpose / Business Critical), licensing model (License Included / Azure Hybrid Benefit), and reservation term (PAYG / 1-Year RI / 3-Year RI)
- Full cost overview table with one-time and monthly breakdown
- Interactive 3D charts: total cost, one-time breakdown, monthly breakdown, with tooltips, clickable legend and drag to rotate
- PDF export and browser print support

---

## Shared Design

The three V2 calculators share one design: the same style block, scoped to the calculator roots, so the calculators look alike and neither style the page that embeds them nor get styled by it. The notes and disclaimers of each calculator are collapsed under "Notes and Disclaimers" (the PDF export and printing always include them), and wide tables scroll inside their own box on small screens.

---

## 3D Charts

V3 and the V2 calculators draw their charts with the same small 3D renderer, built into each HTML file, so every calculator is a single self-contained file without external libraries. The charts support:

- **Hover or tap** on a slice or bar to see its value, its share and, for stacked bars, every value of that category plus the total
- **Click a legend entry** to hide or show that part of the chart
- **Drag** to rotate the view (donuts: turn and tilt, bars: change the depth angle) and **double-click** to reset it
- **Keyboard**: focus a chart with Tab and use the arrow keys to read each value, Escape to close the tooltip

Colors are assigned per entity and stay the same in every chart (for example, Windows licensing has the same color in both pricing charts). The palette was checked for color vision deficiency separation, and every value is also shown in the legend or the Full Overview table, so no information depends on color or hover alone.

---

## Import from ODIN

V3 and all three V2 calculators include an **Import from ODIN** button that loads a configuration exported from [ODIN for Azure Local](https://azure.github.io/odinforazurelocal/). Both ODIN export formats are supported:

- **Sizer** "Export JSON" file (`{ _meta, data }` or the bare `data` object)
- **Designer** "Export Configuration" file (`{ version, exportedAt, state }`). Hardware and workload data is only available when the design was started from the Sizer.

The file is read locally in the browser and is never uploaded. After the import, the calculator fills in the matching fields, recalculates and shows a summary of what was applied and what could not be mapped.

All cluster types ODIN exports are supported: Single Node, Hyperconverged, Rack Aware, Disaggregated Storage and Disconnected Operations (management cluster).

In V3 one import fills the compute, storage and cost steps at once (see [Azure Local Calculator V3](#azure-local-calculator-v3-current) for the fields). V3 doesn't share imports with the V2 calculators.

**One import for all V2 calculators:** a configuration imported in one V2 calculator is applied to the other V2 calculators as well, both on the same page and in other open tabs of the site. It is also kept for the browser session, so the other calculator pages load it automatically when they are opened. Closing the browser tab clears it.

| Calculator | Fields imported from ODIN |
|------------|---------------------------|
| Storage V2 | Deployment type (disaggregated or ALDO management cluster), node count (Single Node when 1), capacity drives per node and drive size, resiliency (Simple, two-way, three-way or four-way mirror), target effective storage from the workload total including future growth. Disaggregated designs get the SAN plan with the SAN capacity and connectivity (Fibre Channel or iSCSI) |
| CPU V2 | Cluster type, total workload vCPUs including future growth (as VMs x vCPUs; the fixed appliance for an ALDO management cluster), vCPU to core ratio, node count, sockets, management overhead per node (ODIN host core reservation), and the ODIN CPU as a selectable model in the "I know my CPU" mode |
| Pricing V2 | Deployment model (L1, L2 disaggregated with SAN storage, L3 for disconnected), node count, physical cores per node (the management cluster fields for an ALDO management cluster design), switch count, AVD vCPUs |

The switch count follows the ODIN Sizer network model: 2 ToR and 1 BMC switch per rack (Rack Aware uses 2 racks), a single BMC switch for Single Node, and for Disaggregated Storage 2 ToR and 1 BMC per rack plus 2 FC switches per rack for FC SAN and the spine switches. When a Designer file defines the ToR switch count, that value is used.

**Storage and Pricing in sync:** a change of the deployment type in the Storage Calculator selects the matching deployment model in the Pricing Calculator (hyperconverged with external SAN to L2, disaggregated to L2 disaggregated, ALDO management cluster to L3, Storage Spaces Direct to L1 unless L3 is selected) and the other way around, on the same page and in other open tabs. Every SAN plan also fills in the vendor and the physical capacity of the Pricing SAN System section. ODIN imports set all calculators to the same cluster type.

The Simple and Four-Way Mirror resiliency options (single node and rack aware clusters) only appear in the Storage Calculator when an imported configuration uses them.

Limitations:
- Tiered ODIN layouts are imported as their capacity drives only, because the Storage Calculator models full-flash storage.
- The Storage Calculator supports up to 16 nodes (64 for disaggregated) and 24 drives per node. Larger ODIN values are capped and the summary says so. ODIN exports have no SAN vendor, so choose it after importing a disaggregated design.
- Prices (nodes, switches, related costs) are not part of ODIN exports and must be entered manually.
- For L3 (disconnected operations) the host fee must be entered before the pricing is calculated.

---

## Repository Structure

```
AzureLocal-Calculator/
├── Calculators/
│   ├── StorageCalculator/
│   │   ├── StorageCalculator.html       # V1 (legacy)
│   │   └── StorageCalculatorV2.html     # V2 (previous)
│   ├── CPUCalculator/
│   │   ├── CPUCalculator.html           # V1 (legacy)
│   │   └── CPUCalculatorV2.html         # V2 (previous)
│   ├── PricingCalculator/
│   │   ├── PricingCalculator.html       # V1 (legacy)
│   │   └── PricingCalculatorV2.html     # V2 (previous)
│   └── azurelocal-calculator-v3.html    # V3 (current): compute, storage and cost on one page
├── README.md
└── LICENSE
```

---

## Interactive Demo

Try the calculators interactively on my blog: [Azure Local Calculator](https://schmitt-nieto.com/azurelocal-calculator/).

---

## Contributors

- **Cristian Schmitt Nieto**
  Creator of the calculators and the code. [LinkedIn](https://www.linkedin.com/in/cristian-schmitt-nieto/)

- **Florian Hildesheim**
  Contributed ideas for the Storage Calculator and provided data.
  [LinkedIn](https://www.linkedin.com/in/florian-hildesheim-757bb0273/)
  *Additional details on Florian's contributions: [LinkedIn post](https://www.linkedin.com/posts/cristian-schmitt-nieto_azure-local-redundancy-activity-7301889003878846464-P3sb).*

- **Karl Wester-Ebbinghaus**
  Contributed ideas for the Pricing and CPU Calculators and provided data for all calculators.
  [LinkedIn](https://www.linkedin.com/in/karl-wester-ebbinghaus-a41507153/)

> The original Storage Calculator was inspired by the approach used in Cosmos Darwin's S2D Calculator.
> [LinkedIn](https://www.linkedin.com/in/cosmosd/)

---

## Disclaimer

- **Unofficial:**
  This sample is provided for your reference only and is not official Microsoft documentation or software.

- **No Endorsement:**
  It does not represent an endorsement or final approval of any specific architecture or design.

- **Provided "AS IS":**
  The code sample is offered "AS IS" without any warranties, either express or implied, including warranties of merchantability or fitness for a particular purpose.

- **No Standard Support:**
  This sample is not supported under any Microsoft standard support program or service.

- **Use at Your Own Risk:**
  Microsoft disclaims all implied warranties, and the entire risk arising from the use or performance of this sample remains with you.

- **Limitation of Liability:**
  In no event shall Microsoft, its authors, or anyone involved in its creation, production, or delivery be liable for any damages (including loss of business profits, business interruptions, or other financial losses) arising from the use or inability to use this sample.
