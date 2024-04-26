## Overview

This project provides a set of measurement plugins demonstrating advanced data structures.

## Software Dependencies

- LabVIEW 2021 SP1
- LabVIEW Add-ons (VI Packages):
  - MeasurementLink Generator
  - MeasurementLink Service
  - JSONtext
- InstrumentStudio 2024 Q1
- Measurement Link 2024 Q1

## Measurement Plugin Details

### Advanced Data Structure Exchange

The `Advanced Data Structure Exchange` plugin is an example that shows how to implement a complex cluster and exchange the cluster data between Measurement UI and Logic.

#### Key Techniques:

- Using Clusters
- Handling Data Exchange through JSON strings and Text File
- Building Measurement UI as PPLs
  - As this example uses JSONtext (external package) to convert data into JSON, the Measurement UI should be built into ppl for InstrumentStudio compatibility.

