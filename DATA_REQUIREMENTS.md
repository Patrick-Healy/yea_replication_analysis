# Data Requirements

This document lists all data files required to run the replication package. These files are **NOT** included in the repository and must be obtained separately.

## Overview

All data files have been anonymized with Personally Identifiable Information (PII) removed. Files are named with the `_noPII` suffix to indicate this anonymization.

## Required Directory Structure

Create the following directory structure in your repository:

```
yea_replication_analysis/
└── data/
    ├── 01_base/
    │   ├── admin_data/
    │   └── survey_data/
    ├── 02_intermediate/   (created automatically by 2_Data_Construction.do)
    └── 03_clean_combined/ (created automatically by 2_Data_Construction.do)
```

## Required Data Files

### Administrative Data Files
**Location:** `data/01_base/admin_data/`

| File Name | Format | Description | Used In |
|-----------|--------|-------------|---------|
| `concessions_chefferies.csv` | CSV | Geographic base data linking concessions to chefferies | 2_Data_Construction.do:24 |
| `campaign_2016_neighborhoods.dta` | Stata | 2016 treatment assignment by neighborhood | 2_Data_Construction.do:30 |
| `randomization_schedule.dta` | Stata | Randomization schedule for 2018 treatment assignment | 2_Data_Construction.do:43 |
| `fliers_pilot_set1.xlsx` | Excel | Flier treatment assignment - Pilot Set 1 | 2_Data_Construction.do:80 |
| `fliers_pilot_set2.xlsx` | Excel | Flier treatment assignment - Pilot Set 2 | 2_Data_Construction.do:94 |
| `fliers_pilot_set3.xlsx` | Excel | Flier treatment assignment - Pilot Set 3 | 2_Data_Construction.do:108 |
| `fliers_campaign.dta` | Stata | Flier treatment assignment - Main campaign | 2_Data_Construction.do:123 |
| `registration_noPII.dta` | Stata | Cartography registration data (anonymized) | 2_Data_Construction.do:151 |
| `taxroll_noPII.dta` | Stata | Tax roll (repertoire) data (anonymized) | 2_Data_Construction.do:180 |
| `tax_payments_noPII.dta` | Stata | Tax payment records from TDM (anonymized) | 2_Data_Construction.do:223 |
| `stratum.dta` | Stata | Stratification assignments | Multiple tables/figures |
| `randomization_assignment.dta` | Stata | Treatment assignment details | 2_Data_Construction.do:43-78 |
| `chief_collector_candidates.dta` | Stata | Information on chief and tax collector candidates | Various appendix tables |
| `tax_payments_neighborhoods.dta` | Stata | Neighborhood-level tax payment aggregates | TableA45.do and others |
| `property_values_MLestimates.csv` | CSV | Machine learning estimates of property values | Various tables |
| `neighborhood_transport_cost.dta` | Stata | Transportation costs by neighborhood | Appendix tables |

### Survey Data Files
**Location:** `data/01_base/survey_data/`

| File Name | Format | Description | Used In |
|-----------|--------|-------------|---------|
| `baseline_noPII.dta` | Stata | Baseline survey data (anonymized) | Multiple tables/figures |
| `midline_noPII.dta` | Stata | Midline monitoring survey data (anonymized) | 2_Data_Construction.do:190 |
| `endline_round1_noPII.dta` | Stata | Endline Round 1 survey data (anonymized) | Multiple tables/figures |
| `endline_2016campaign_noPII.dta` | Stata | Endline survey for 2016 campaign (anonymized) | Appendix tables |
| `chief_survey_randbasis_noPII.dta` | Stata | Survey of chiefs on randomization basis (anonymized) | Appendix tables |
| `chief_consultations.dta` | Stata | Data on chief consultation activities | Table 5 and appendix |

## Data Characteristics

### Treatment Arms

The study includes the following treatment arms (variable: `treatment` or `tmt`):

| Code | Description |
|------|-------------|
| 0 | Control |
| 1 | Central authority implementation only |
| 2 | Local chief implementation only |
| 3 | Central with chief information |
| 4 | Central × Local coordination |

### Geographic Units

- **Chefferies:** Traditional administrative units led by local chiefs
- **Concessions:** Property parcels subject to taxation
- **Polygons:** Geographic units for spatial analysis
- **Neighborhoods:** Groupings of concessions for administrative purposes

### Key Variables

The data construction script creates numerous outcome and analysis variables, including:

**Outcome Variables:**
- `taxes_paid` - Binary indicator of tax payment
- `taxes_paid_amount` - Amount of taxes paid
- `bribe_paid` - Indicator for bribe payment
- `collector_visits` - Number of tax collector visits

**Treatment Indicators:**
- `flier_treatment` - Whether property received a flier
- `central_treatment` - Central authority intervention
- `chief_treatment` - Chief-led intervention
- `info_treatment` - Information sharing treatment
- `coordinated_treatment` - Coordinated central-local treatment

**Control Variables:**
- Employment status indicators
- Property characteristics
- Geographic identifiers
- Baseline covariates

## Data Access

### For Replication

To obtain the data files for replication purposes:

1. **Contact the Original Authors**
   - See the published paper for author contact information
   - Request access to the replication data package
   - Cite your intended use (e.g., academic replication, teaching)

2. **Data Repository** (if applicable)
   - Check if data is available through journal's dataverse
   - Look for DOI or persistent identifier in the paper
   - Follow repository's access procedures

3. **Restricted Access**
   - Some data may require Data Use Agreements (DUA)
   - IRB approval may be required for sensitive data
   - Confidentiality commitments may be necessary

### Data Use Conditions

- Data is for **academic research and replication purposes only**
- Do **not** redistribute the data without permission
- Respect all anonymization and confidentiality protections
- Cite the original study in any work using the data

## Data Quality Notes

### Known Issues Addressed in Code

The `2_Data_Construction.do` script includes several manual corrections for known data quality issues:

1. **Treatment Assignment Corrections** (Lines 67-70)
   - Manual corrections for specific properties with incorrect treatment assignments
   - Documented in code comments

2. **Cartography Date Corrections** (Lines 953-1029)
   - 76 lines of manual date fixes for registration data
   - Addresses inconsistencies in source data entry

3. **Employment Status Classification** (Lines 400-900+)
   - Extensive recoding of employment categories
   - Standardizes inconsistent survey responses

### Missing Value Codes

The data uses several missing value indicators:
- `.` - Standard Stata missing
- `.d` - "Don't know" responses
- `99999`, `99998` - Legacy missing codes (recoded in scripts)
- `316037` - Special missing code (purpose unclear, check documentation)

## Verification

After obtaining and placing all data files, verify your setup:

1. Check that all files are in the correct directories
2. Ensure file names match exactly (case-sensitive on macOS/Linux)
3. Verify file formats match expectations (.dta, .csv, .xlsx)
4. Run `2_Data_Construction.do` to test data loading

### Expected File Sizes (Approximate)

While exact sizes vary by version, expect:
- Survey data files: 1-10 MB each
- Administrative data files: 500 KB - 5 MB each
- Total raw data: ~50-100 MB

## Support

For questions about data access or requirements:

1. Consult the `README.pdf` included in the repository
2. Check the original paper's supplementary materials
3. Contact the replication package author (see README.md)
4. Contact the original study authors for data access

## Data Version History

See `CHANGES.txt` for information about changes across versions:
- **V3**: Removed additional variables with potential PII
- **V2**: Removed extraneous variables for usability
- **V1**: Original data files

Ensure you obtain the data version corresponding to the code version you are using (currently V3).

---

**Last Updated:** November 2024
**Note:** This is a living document. Report any discrepancies or missing files via GitHub issues.
