# AzureLocal-Calculator

AzureLocal-Calculator is a repository that provides a set of interactive calculators for estimating key metrics in an Azure Local environment, including Storage, CPU, and Pricing estimation.

The calculators are implemented as web-based tools and are organized into individual folders under the `Calculators` directory. They are also available for interactive use on my blog at [Azure Local Calculator](https://schmitt-nieto.com/azurelocal-calculator/).

## Calculators

- **Storage Calculator:**  
  Estimates raw, effective, and usable storage capacity based on node count, disk count, specified capacity per disk and efficiency factors, when using Azure Local and configuring storage via Express Settings.
- **CPU Calculator:**  
  (Under development) Provides CPU performance estimation.
- **Pricing Calculator:**  
  (Under development) Provides cost estimation for the Azure Local environment.

## Repository Structure

```
AzureLocal-Calculator/ 
├── Calculators/ 
│ ├── StorageCalculator/ 
│ ├── CPUCalculator/ (under development) 
│ └── PricingCalculator/ (under development) 
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

This is not official Microsoft documentation or software.  
This is not an endorsement or a sign-off of an architecture or a design.  
This code sample is provided "AS IT IS" without warranty of any kind, either expressed or implied, including but not limited to the implied warranties of merchantability and/or fitness for a particular purpose.  
This sample is not supported under any Microsoft standard support program or service.  
Microsoft further disclaims all implied warranties, including, without limitation, any implied warranties of merchantability or fitness for a particular purpose.  
The entire risk arising out of the use or performance of the sample and documentation remains with you.  
In no event shall Microsoft, its authors, or anyone else involved in the creation, production, or delivery of the script be liable for any damages whatsoever (including, without limitation, damages for loss of business profits, business interruption, loss of business information, or other pecuniary loss) arising out of the use of or inability to use the sample or documentation, even if Microsoft has been advised of the possibility of such damages.

