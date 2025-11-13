# Local Elites as State Capacity: Replication Package

This repository contains replication materials for:

**"Local Elites as State Capacity: How City Chiefs Use Local Information to Increase Tax Compliance in the D.R. Congo"**
*Balan et al. (2021)*

## Overview

This replication package provides all code necessary to reproduce the tables and figures in the main text and appendix of the paper. The study examines how local chiefs can improve tax compliance in Kananga, Democratic Republic of Congo, through a randomized controlled trial with multiple treatment arms.

## Requirements

### Software
- **Stata 15.0 or higher** (tested with Stata 15-17)
- **Operating System**: Windows, macOS, or Linux
  - Note: This package is now cross-platform compatible
- **Memory**: At least 4 GB RAM recommended
- **Disk Space**: At least 2 GB free space for data and outputs
- **Internet Connection**: Required for initial package installation

### Stata Packages

All required Stata packages are automatically installed by `1_Package_Setup.do`. The following packages will be installed:

**From SSC:**
- estout
- outtable
- mmat2tex
- geodist
- center
- grstyle
- palettes
- balancetable
- winsor
- revrs
- distplot
- blindschemes
- binscatter
- cibar

**Custom Packages:**
- GSSU (from https://www.jcsurez.com/GSSU/)
- cem (from https://www.mattblackwell.org/files/stata)

## Installation

### Step 1: Clone or Download Repository

```bash
git clone https://github.com/Patrick-Healy/yea_replication_analysis.git
cd yea_replication_analysis
```

Or download and extract the ZIP file from GitHub.

### Step 2: Obtain Data Files

**IMPORTANT:** The data files are not included in this repository due to size and privacy considerations. You must obtain the data separately and place it in the appropriate directory structure.

See [DATA_REQUIREMENTS.md](DATA_REQUIREMENTS.md) for a complete list of required data files and their expected locations.

Expected directory structure:
```
yea_replication_analysis/
├── Dofiles/           (provided in repository)
├── Documents/         (provided in repository)
├── data/              (YOU MUST CREATE AND POPULATE)
│   ├── 01_base/
│   │   ├── admin_data/
│   │   └── survey_data/
│   ├── 02_intermediate/   (created automatically)
│   └── 03_clean_combined/ (created automatically)
└── Output/            (created automatically)
```

### Step 3: Configure Paths

Edit line 23 in `Dofiles/0_Master.do`:

```stata
gl stem "Your Directory/Replication Materials - Updated October 2024"
```

Replace `"Your Directory/Replication Materials - Updated October 2024"` with the **full path** to your repository directory.

**Examples:**
- Windows: `gl stem "C:/Users/YourName/Documents/yea_replication_analysis"`
- macOS: `gl stem "/Users/YourName/Documents/yea_replication_analysis"`
- Linux: `gl stem "/home/username/yea_replication_analysis"`

## Execution

### Quick Start

1. Open Stata
2. Change directory to your replication materials folder:
   ```stata
   cd "path/to/yea_replication_analysis"
   ```
3. Run the master script:
   ```stata
   do "Dofiles/0_Master.do"
   ```

The master script will automatically:
1. Install all required Stata packages
2. Construct the analysis datasets from raw data
3. Generate all main tables and figures
4. Generate all appendix tables and figures

### Step-by-Step Execution

If you prefer to run scripts individually:

1. **Install packages:**
   ```stata
   do "Dofiles/1_Package_Setup.do"
   ```

2. **Construct datasets:**
   ```stata
   do "Dofiles/2_Data_Construction.do"
   ```
   - Runtime: ~10-15 minutes
   - Creates intermediate and final analysis datasets

3. **Generate main tables and figures:**
   ```stata
   do "Dofiles/3_Main_Tables_Figures.do"
   ```
   - Runtime: ~30-45 minutes
   - Produces Tables 1-9 and main figures

4. **Generate appendix materials:**
   ```stata
   do "Dofiles/4_Appendix_Tables_Figures.do"
   ```
   - Runtime: ~45-60 minutes
   - Produces 45 appendix tables and 18 appendix figures

**Total expected runtime:** Approximately 90-120 minutes on a modern computer.

## Output

All outputs are saved to the `Output/` directory, which is automatically created:

- **Tables:** `.tex` (LaTeX) and `.csv` formats
- **Figures:** `.pdf` and `.png` formats
- **Logs:** `.log` files (if logging is enabled)

### Expected Outputs

**Main Paper:**
- Tables 1-9
- Figures 1, A9, A10, A11, A14

**Appendix:**
- Tables A1-A45 (note: not all numbers used due to removed tables)
- Figures A4-A22

## Repository Structure

```
yea_replication_analysis/
├── .github/workflows/     # GitHub Actions configuration
├── Dofiles/               # All Stata analysis scripts
│   ├── 0_Master.do                    # Master control script
│   ├── 1_Package_Setup.do             # Package installation
│   ├── 2_Data_Construction.do         # Data pipeline (1,044 lines)
│   ├── 3_Main_Tables_Figures.do       # Main outputs router
│   ├── 4_Appendix_Tables_Figures.do   # Appendix outputs router
│   └── Tables_Figures/                # Individual table/figure scripts (52 files)
├── Documents/             # Supporting documentation and reference materials
│   ├── central_v_local_paper_20210810.bbl  # Bibliography
│   ├── flier3000control.png                 # Flier example
│   ├── polygons.png                         # Geographic units map
│   ├── property_registration_path.pdf       # Registration process diagram
│   └── strata.png                           # Stratification visualization
├── .gitignore             # Git ignore rules
├── CHANGES.txt            # Version history
├── README.md              # This file
├── README.pdf             # Comprehensive documentation (209 KB)
└── DATA_REQUIREMENTS.md   # Required data files documentation
```

## Troubleshooting

### Common Issues

**1. "file not found" error when loading data**
- Ensure all data files are in the correct `data/` subdirectories
- Check that paths use forward slashes (/) not backslashes (\)
- Verify that file names match exactly (case-sensitive on macOS/Linux)

**2. "command not found" error for a Stata package**
- Re-run `Dofiles/1_Package_Setup.do`
- Ensure you have internet connectivity
- Check Stata version compatibility (minimum Stata 15)

**3. "insufficient memory" error**
- Increase Stata's memory allocation: `set max_memory 8g`
- Close other applications to free up RAM
- Consider running scripts individually rather than all at once

**4. Path with spaces causes errors**
- Ensure paths are properly quoted in `0_Master.do`
- Avoid using directory names with special characters

**5. Output directory not found**
- The `Output/` directory should be created automatically
- If not, create it manually: `mkdir Output` (in terminal) or `!mkdir Output` (in Stata)

### Getting Help

For issues specific to this replication package:
1. Check the comprehensive documentation in `README.pdf`
2. Review the CHANGES.txt file for version-specific notes
3. Open an issue on the GitHub repository

For issues with the original study:
- Refer to the published paper's supplementary materials
- Contact the original authors (information in paper)

## Data Confidentiality

All data files in this replication package have been anonymized and PII (Personally Identifiable Information) has been removed. File names ending in `_noPII.dta` indicate cleaned versions without sensitive information.

See `CHANGES.txt` for details on PII removal across versions.

## Citation

If you use this replication package, please cite:

```bibtex
@article{balan2021local,
  title={Local Elites as State Capacity: How City Chiefs Use Local Information to Increase Tax Compliance in the D.R. Congo},
  author={Balan, Pablo and Bergeron, Augustin and Tourek, Gabriel and Weigel, Jonathan},
  year={2021},
  journal={[Journal Name]},
  note={Replication materials available at https://github.com/Patrick-Healy/yea_replication_analysis}
}
```

## Version History

See [CHANGES.txt](CHANGES.txt) for detailed version history.

- **V3** (Current): Removed additional variables with potential PII
- **V2**: Removed extraneous variables for improved usability
- **V1**: Original version

## License

[Add appropriate license information here]

## Authors

**Replication Package Author:** Gabriel Tourek
**Original Study Authors:** Balan, Bergeron, Tourek, Weigel

## Acknowledgments

See the original paper for research acknowledgments and funding sources.

---

**Last Updated:** November 2024
**Repository:** https://github.com/Patrick-Healy/yea_replication_analysis
