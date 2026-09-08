Six-Sense Microneedle: Automated QA and V&V Pipeline

This repository contains a mock Verification and Validation (V&V) data pipeline simulating mechanical load-cell testing for a diagnostic wearable. The project demonstrates the entire medical device workflow process, from physical CAD architecture to automated Python quality assurance and batch release.

Project Origins & The Pivot

The starting concept for the Six-Sense device- a non-invasive patch designed to detect IL-6 biomarkers for sports injury diagnostics- was initially co-designed in a collaborative group that I was in at a Drexel University summer program in 2023. Our team established the primary biological use case and early design using OnShape and Fusion 360. 

Building upon that initial group ideation, this specific repository represents my individual pivot towards medical product engineering and Quality Assurance (QA). Rather than biological assays, this pipeline focuses entirely on the structural integrity, manufacturability, and automated regulatory compliance of the device hardware. 

1. Device Architecture
   
<img width="143" height="109" alt="Screenshot 2026-09-07 at 9 21 56 PM" src="https://github.com/user-attachments/assets/cc854353-4f18-4db3-b2f6-d459d56f0073" />



<img width="316" height="181" alt="Six-Sense CAD Render" src="https://github.com/user-attachments/assets/2324c3b2-c862-4e99-b15e-c53eb08c0f41" />

The physical structure of the patch was modeled parametrically to withstand physical application without fracturing the micro-structures. Key components include:
* Woven Base Pad: A 2mm flexible pad that secures the device to the patient
* Microfluidic Channels: Capillary pathways designed for interstitial fluid transport (i.e. like capillary transport)
* Central Reservoir & Sense Nodes: Active detection sites housing the diagnostic arrays.

2. Simulated V&V Testing & Methodology

To ensure patient safety, microneedle arrays must pass strict mechanical yield thresholds before a manufacturing lot can be released. 
* The Simulation: 50 patches across two manufacturing runs (Lot A and Lot B) were subjected to a simulated compressive load-cell test.
* Acceptance Criteria: The polymer structures must withstand a minimum yield stress of 120 MPa before physical failure (fracture or critical deformation).

3. Automated Data Pipeline (Software)

<img width="723" height="466" alt="Graph" src="https://github.com/user-attachments/assets/0dd9b207-c7e4-4dd8-b85e-bc30d27ea740" />

To eliminate human error in manufacturing batch reviews, I engineered a custom data pipeline using Python, Pandas, and NumPy to automate the inspection process:
* Data Analysis: Raw factory force (N) and displacement (mm) metrics are imported via CSV and computationally translated into true engineering Stress (MPa) and Strain.
* Automated Sorting: A vectorized NumPy architecture evaluates each batch against the 120 MPa safety threshold, tagging individual units with a Pass/Fail status.
* Visual Compliance: I used Matplotblin to generate regulatory-style stress-strain scatter plots, providing an immediate visual representation of manufacturing consistency across different production lots. 


