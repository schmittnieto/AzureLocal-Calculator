# AzureLocal-Calculator

AzureLocal-Calculator is a repository that provides a set of interactive calculators for estimating key metrics in an Azure Local environment, including Storage, CPU and Pricing estimation.

The calculators are implemented as web-based tools and are organized into individual folders under the `Calculators` directory. They are also available for interactive use on my blog at [Azure Local Calculator](https://schmitt-nieto.com/azurelocal-calculator/).

> [!IMPORTANT]  
> The storage calculator I designed is now outdated, as [Armin](https://www.linkedin.com/in/aoberneder/) has created a much better one. For this reason, I will not continue developing mine, and I recommend using Armin’s calculator for this purpose: [s2d-calculator.com](https://s2d-calculator.com/).

## Calculators

- **Storage Calculator:**
   Estimates raw, effective, and usable storage capacity based on node count, disk count, specified capacity per disk and efficiency factors, when using Azure Local and configuring storage via Express Settings.
- **CPU Calculator:**  
  (Under development) Provides CPU performance estimation.
- **Pricing Calculator:**  
  Provides cost estimation for the Azure Local environment.

## Repository Structure

```
AzureLocal-Calculator/ 
├── Calculators/ 
│ ├── StorageCalculator/ 
│ ├── CPUCalculator/ (under development) 
│ └── PricingCalculator/ 
├── README.md
└── LICENSE
```

## Interactive Demo

Try the calculators interactively on my blog: [Azure Local Calculator](https://schmitt-nieto.com/azurelocal-calculator/).

## Contributors

- **Cristian Schmitt Nieto**  
  Creator of the calculators and the code. [LinkedIn](https://www.linkedin.com/in/cristian-schmitt-nieto/)

- **Florian Hildesheim**  
  Contributed ideas for the Storage Calculator and provided data.  
  [LinkedIn](https://www.linkedin.com/in/florian-hildesheim-757bb0273/)  
  *Additional details on Florian’s contributions can be found in [this LinkedIn post](https://www.linkedin.com/posts/cristian-schmitt-nieto_azure-local-redundancy-activity-7301889003878846464-P3sb).*

- **Karl Wester-Ebbinghaus**  
  Contributed ideas for the Pricing and CPU Calculators and provided data for all calculators.  
  [LinkedIn](https://www.linkedin.com/in/karl-wester-ebbinghaus-a41507153/)

> The initial Storage Calculator is inspired by the approach used in Cosmos Darwin’s S2D Calculator.  
> [LinkedIn](https://www.linkedin.com/in/cosmosd/)

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


