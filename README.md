# AzureLocal-Calculator

AzureLocal-Calculator is a repository that provides a set of interactive, web-based calculators for estimating key metrics in an Azure Local environment, including Storage, CPU, and Pricing estimation. Each calculator is available in an original version (V1) and an improved version (V2).

The calculators are organized under the `Calculators` directory and are also available for interactive use on my blog: [Azure Local Calculator](https://schmitt-nieto.com/azurelocal-calculator/).

> [!IMPORTANT]
> The original Storage Calculator (V1) is now outdated. [Armin](https://www.linkedin.com/in/aoberneder/) has created a much better dedicated tool. I recommend using his calculator for storage sizing: [s2d-calculator.com](https://s2d-calculator.com/).
> The Storage Calculator V2 included in this repo offers an improved in-house alternative with multi-tier and multi-platform support.

---

## Calculators

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
- Detailed results with raw, effective, and usable capacity breakdown
- Interactive Chart.js visualizations
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
- CPU socket selector (single socket / dual socket)
- N+1 High Availability capacity reservation toggle
- Management overhead and vCPU-to-core ratio configuration
- CPU recommendation cards showing fit, tight, or insufficient status
- Interactive Chart.js visualizations
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
- **Licensing**:
  - Azure Local Host Fee (10/core/month), waivable via Azure Hybrid Benefit
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
- Interactive Chart.js visualizations: total cost, one-time breakdown, monthly breakdown
- PDF export and browser print support

---

## Repository Structure

```
AzureLocal-Calculator/
├── Calculators/
│   ├── StorageCalculator/
│   │   ├── StorageCalculator.html       # V1 (legacy)
│   │   └── StorageCalculatorV2.html     # V2 (current)
│   ├── CPUCalculator/
│   │   ├── CPUCalculator.html           # V1 (legacy)
│   │   └── CPUCalculatorV2.html         # V2 (current)
│   └── PricingCalculator/
│       ├── PricingCalculator.html       # V1 (legacy)
│       └── PricingCalculatorV2.html     # V2 (current)
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
