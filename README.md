# Six-Sense Microneedle: Automated QA and V&V Pipeline

This repository contains a mock Verification and Validation (V&V) data pipeline simulating mechanical load-cell testing for a diagnostic wearable. The project demonstrates the entire medical device workflow process, from physical CAD architecture to automated Python quality assurance and batch release.

### Project Origins & The Pivot
The starting concept for the Six-Sense device—a non-invasive patch designed to detect IL-6 biomarkers for sports injury diagnostics—was initially co-designed in a collaborative group that I was in at a Drexel University summer program in 2023. Our team established the primary biological use case and early design using Onshape and Fusion 360. 

Building upon that initial group ideation, this specific repository represents my individual pivot towards medical product engineering and Quality Assurance (QA). Rather than biological assays, this pipeline focuses entirely on the structural integrity, manufacturability, and automated regulatory compliance of the device hardware. 

### 1. Device Architecture

<img width="143" height="109" alt="Screenshot 2026-09-07 at 9 21 56 PM" src="https://github.com/user-attachments/assets/cc854353-4f18-4db3-b2f6-d459d56f0073" />
<img width="316" height="181" alt="Six-Sense CAD Render" src="https://github.com/user-attachments/assets/2324c3b2-c862-4e99-b15e-c53eb08c0f41" />

The physical structure of the patch was modeled parametrically to withstand physical application without fracturing the micro-structures. Key components include:
* **Woven Base Pad:** A 2mm flexible pad that secures the device to the patient.
* **Microfluidic Channels:** Capillary pathways designed for interstitial fluid transport (i.e., like capillary transport).
* **Central Reservoir & Sense Nodes:** Active detection sites housing the diagnostic arrays.

### 2. Simulated V&V Testing & Methodology
To ensure patient safety, microneedle arrays must pass strict mechanical yield thresholds before a manufacturing lot can be released. 
* **The Simulation:** 50 patches across two manufacturing runs (Lot A and Lot B) were subjected to a simulated compressive load-cell test.
* **Acceptance Criteria:** The polymer structures must withstand a minimum yield stress of 120 MPa before physical failure (fracture or critical deformation).

### 3. Automated Data Pipeline (Software)

<img width="723" height="466" alt="Graph" src="https://github.com/user-attachments/assets/0dd9b207-c7e4-4dd8-b85e-bc30d27ea740" />

To eliminate human error in manufacturing batch reviews, I engineered a custom data pipeline using Python, Pandas, and NumPy to automate the inspection process:
* **Data Analysis:** Raw factory force (N) and displacement (mm) metrics are imported via CSV and computationally translated into true engineering Stress (MPa) and Strain.
* **Automated Sorting:** A vectorized NumPy architecture evaluates each batch against the 120 MPa safety threshold, tagging individual units with a Pass/Fail status.
* **Visual Compliance:** I used Matplotlib to generate regulatory-style stress-strain scatter plots, providing an immediate visual representation of manufacturing consistency across different production lots. 

### 4. Regulatory Framework & V&V Protocol
This pipeline was engineered to mirror the structure of medical device quality system requirements:
* **21 CFR Part 820 (QMSR) / ISO 13485:2016 Clause 7.3 — Design & Development:** The mechanical acceptance criterion was defined as a design input and fixed before any data was analyzed, so the pass/fail call is a verification of design output against a pre-specified requirement rather than a post-hoc reading of the results.
* **ISO 13485:2016 Clauses 8.2.6, 8.3 & 8.5.2 — Measurement, Nonconforming Product, and CAPA:** Units below the yield threshold are tagged as nonconforming. A lot showing an elevated failure rate is flagged for mechanical root-cause analysis and corrective action.
* **Data Integrity (ALCOA+ principles):** The Python pipeline removes manual transcription between raw load-cell output and reported stress values, preserving a traceable path from source CSV through calculation to final plot.
* **Test Methodology:** No published consensus standard currently covers compressive fracture testing of polymer microneedle arrays. Reported buckling loads are known to vary with the number of needles loaded simultaneously and compression angle, so this protocol fixes and documents those parameters explicitly to make the method reproducible.

*(The formal 1-page Design Verification protocol is attached as a PDF and transcribed in the Appendix below).*

### 5. Repository Asset Guide
* **[`VV_Compression_Protocol(1).pdf`](VV_Compression_Protocol.pdf):** 1-page formal testing parameters and acceptance criteria.
* **[`compression_test_data.csv`](compression_test_data.csv):** Simulated batch load-cell data.
* **[`Python.ipynb`](Python.ipynb):** Automated Python pipeline and data analysis.

<hr>

<details>
<summary><b>Appendix: Read the Mock V&V Protocol Text</b></summary>
<br>

**Document ID:** VVP-MEC-001  
**Device:** Six-Sense Diagnostic Microneedle Patch  
**Testing Phase:** Design Verification (Mechanical Integrity)  
**Regulatory Alignment:** 21 CFR Part 820 (QMSR), ISO 13485:2016 Clause 7.3

**1. Objective**  
To verify that the Six-Sense microneedle array withstands standard application forces without fracturing or undergoing critical deformation, satisfying design verification requirements under 21 CFR Part 820 (QMSR) and ISO 13485:2016 Clause 7.3.

**2. Scope**  
This protocol applies to the simulated compressive load testing of 50 randomly sampled microneedle arrays across two manufacturing runs (Lot A and Lot B). This test evaluates the physical yield limit and structural integrity of the individual microneedles under direct axial load. Because the test is destructive, the evaluation is sample-based.

**3. Equipment & Methodology**  
No consensus standard currently exists for compressive fracture testing of polymer microneedle arrays, so the following parameters are specified directly and held constant across all samples:
* **Equipment:** Simulated Instron universal testing machine with axial compression load cell.
* **Methodology:** A continuous downward compressive force is applied to the central axis of the patch at a constant displacement rate until physical failure.
* **Controlled Variables:** Number of needles loaded simultaneously, crosshead displacement rate, and compression angle are fixed and recorded, as published microneedle compression data shows buckling load varies substantially with all three.
* **Data Capture:** Peak force (N) and displacement (mm) at the moment of structural fracture are recorded and exported to a CSV matrix.

**4. Acceptance Criteria**  
* **Minimum Yield Stress Threshold:** 120.0 MPa.
* To pass verification, the calculated engineering stress (force divided by cross-sectional area) at the moment of fracture must be $\ge$ 120.0 MPa.
* Units fracturing below this threshold are recorded as nonconforming. If a specific manufacturing lot demonstrates a high failure rate, it is flagged for mechanical root-cause analysis and corrective action per ISO 13485:2016 Clause 8.5.2.

**5. Automated Analysis & Data Integrity**  
Consistent with ALCOA+ data integrity principles:
* Raw load-cell data is processed through an automated Python pipeline (Pandas / NumPy) that calculates engineering stress and strain, removing manual transcription steps between the source file and the reported values.
* The script tags units failing the acceptance criterion and generates a stress-strain scatter plot for visual review of lot-to-lot consistency.
* Because the analysis is scripted rather than hand-calculated, the same input file reproduces the same output, making the transition from raw data to verification decision traceable.
</details>
