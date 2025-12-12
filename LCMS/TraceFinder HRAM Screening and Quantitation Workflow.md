# TraceFinder HRAM Workflow

This document provides a comprehensive summary and analysis of the provided text on the TraceFinder HRAM screening and quantitation workflow.

## High-Level Overview

The text is a transcript of a video tutorial that serves as a step-by-step guide for using the Thermo Fisher TraceFinder software (version 4.1 or later) to process high-resolution accurate mass (HRAM) data. It details two primary workflows: **Targeted Screening** (identifying the presence of specific compounds) and **Quantitation** (measuring the amount of specific compounds). The guide is structured into four main sections, plus an appendix, leading the user from initial software setup to final data processing and review.

## Logical Flow and Section-by-Section Analysis

The tutorial is divided into the following logical parts:

### Inputs and Prerequisites

*   **Data:** An HRAM mass spectrometry data set with triggered MS/MS acquisitions (RAW files).
*   **Software:** TraceFinder 4.1 or later.
*   **Resources:**
    *   A compound database (`.cdb` file) containing compound names, formulas, retention times, etc.
    *   An MS/MS spectral library (`.mzvault` file) for MS/MS confirmation (optional).
*   **Knowledge:** Basic experience with TraceFinder software.

### Section 1: Configuration of TraceFinder

This section prepares the software for HRAM data analysis.

*   **Challenge Resolved:** The default TraceFinder settings are not optimal for high-resolution data. This section adjusts them for better precision and accuracy.
*   **Methods/Steps:**
    1.  Open the **TraceFinder configuration** (gear icon).
    2.  In the **Defaults** tab, change **Mass Precision** from 2 to 4 decimal places.
    3.  In the **Peak Detection Defaults** tab, set the mass tolerance to **5 PPM**.
    4.  In **Optional Features**, uncheck `Intelligence Sequencing` and select `Full Sequence Submission`.
    5.  In the **Library** section, browse and select an MS/MS library (e.g., `mzvault_library`).
*   **Result:** TraceFinder is now configured with the appropriate settings for HRAM data processing. This ensures that subsequent method development and data processing steps use the correct parameters.

### Section 2: Building the Targeted Screening Method

This section details how to create a method to screen for a list of target compounds.

*   **Challenge Resolved:** Creating a robust method that can automatically detect and confirm the presence of specific compounds in a sample.
*   **Methods/Steps:**
    1.  Start a new method in the **Method Development** workflow via `File > QAN by selecting Compounds from CDB`.
    2.  Select the desired compounds from a compound database (e.g., `hrampesticides.cdb`).
    3.  Associate a representative **RAW file** that contains peaks for the selected compounds.
    4.  Save the method with a unique name (e.g., `hram pesticides`).
    5.  **Review and Refine Parameters:**
        *   **Processing Tab:** Verify the mass tolerance is correct.
        *   **Detection Tab:** Check that the scan filter and expected mass are correct for each compound.
        *   **Retention Times Tab:** Adjust the expected retention time for each compound to match the data in the associated RAW file.
    6.  **Add Confirmation Criteria (to reduce false positives):**
        *   **Isotopes Tab:** Enable isotope pattern matching and set a fit threshold (e.g., 80%).
        *   **MZVault Tab:** Enable MS/MS library matching. Set **Search Type** to `HiChem`, **Precursor Tolerance** to `50 mMass`, and enable `Ignore Precursor` and `Reverse Search`.
*   **Result:** A complete targeted screening method is created and saved. This method contains all the necessary information for TraceFinder to find compounds, integrate their peaks, and confirm their identity using isotope patterns and MS/MS library matching.

### Section 3: Building the Quantitative Processing Method

This section explains how to adapt the screening method for quantitation.

*   **Challenge Resolved:** Modifying a screening method to enable the calculation of compound concentrations using an internal standard and calibration curve.
*   **Methods/Steps:**
    1.  Open the previously created screening method and save it under a new name (e.g., `HRAM Pesticides Quant`).
    2.  **Add an Internal Standard (IS):**
        *   Add the IS compound to the method from the database.
        *   In the **Identification** tab, change its **Compound Type** to `Internal Standard`.
    3.  **Assign the Internal Standard:**
        *   In the **Calibration** tab, select the newly added IS for each target compound in the **Internal Standard** column and use `Copy Down`.
    4.  **Define Calibration Levels:**
        *   In the **Calibration Levels** tab, define the names for each calibration level (e.g., `Level 1`, `Level 2`).
        *   Enter the corresponding concentration for each compound at each level in the concentration table and use `Copy Down`.
*   **Result:** A quantitative processing method is created. This method can now be used to process a batch containing calibration standards and unknown samples to determine analyte concentrations.

### Section 4: Building and Processing the Batch

This section covers the final step: using the created methods to analyze a sequence of samples.

*   **Challenge Resolved:** Setting up and running an automated analysis of a batch of samples for either screening or quantitation.
*   **Methods/Steps (Screening & Quantitation workflows are similar):**
    1.  Start a new batch in the **Analysis** workflow via `File > New Batch`.
    2.  Select the appropriate **Master Method** (screening or quantitation).
    3.  Name the batch.
    4.  Add the **RAW files** to the batch sequence.
    5.  Define the **Sample Type** for each file (e.g., `Solvent`, `Unknown`, `Cal Standard`).
    6.  For a quantitation batch, assign the correct **Level** to each `Cal Standard`.
    7.  Click **Submit Batch** to start processing.
*   **Data Review:**
    *   After processing, go to the **Data Review** section.
    *   In **Sample View**, results can be reviewed. Samples are on the left, compounds on the right.
    *   Additional panels can be added to the graphics window to view **Isotope** patterns, **Library Match** results, the **Calibration Curve**, and **ISTD** (Internal Standard) response.
*   **Result:** A processed batch with comprehensive results. For screening, this includes confirmed "hits." For quantitation, this includes a calibration curve and calculated concentrations for each analyte in the unknown samples.

### Appendix: Building an HRAM Database

This section provides instructions for creating the foundational compound database.

*   **Challenge Resolved:** Creating the custom database needed for method development if one does not already exist.
*   **Methods/Steps:**
    1.  In the **Method Development** workflow, go to `File > New Small Molecule Compound Database`.
    2.  Name the new database.
    3.  Enter information for each compound by double-clicking in the respective cells: **Compound Name**, **Chemical Formula**, **Polarity**, and expected **Adduct**. The mass-to-charge is calculated automatically.
    4.  Save the database.
*   **Result:** A new compound database (`.cdb` file) is created, which can be used as the input for building screening or quantitation methods as described in Sections 2 and 3.

## Comprehensive Summary

*   **Motivation:** The primary motivation of this text is to educate users of Thermo Fisher's TraceFinder software on the specific, end-to-end workflow required to analyze high-resolution accurate mass (HRAM) data. It addresses the need for a structured process for both identifying compounds (screening) and measuring their quantities (quantitation), which are common tasks in fields like environmental analysis, food safety, and clinical research.

*   **Research Question/Central Argument:** The central argument is that by following a systematic, four-stage process—**Configuration, Method Building, Batch Processing, and Data Review**—a user can effectively and reliably analyze complex HRAM data. The text implicitly argues that proper initial setup (configuration) and detailed method development (including confirmation criteria) are critical for generating high-quality, trustworthy results and minimizing false positives.

*   **Conclusion:** The tutorial concludes that any user, once equipped with the necessary data and software, can successfully build and execute a targeted screening or quantitation analysis. By mastering the steps to configure the software, create detailed methods with confirmation criteria, process batches, and review the multi-faceted results, the user gains the capability to perform robust HRAM data analysis.

*   **Potential Next Steps:** After following this guide, a user's next steps would be to:
    1.  Apply this workflow to their own specific HRAM data sets and research questions.
    2.  Perform method validation studies to establish performance metrics like linearity, limits of detection (LOD), and limits of quantitation (LOQ) for their quantitative assays.
    3.  Explore more advanced features within TraceFinder, such as creating custom reports or developing methods for unknown screening (non-targeted analysis).
    4.  Integrate the results into a larger research context, such as a scientific publication or a regulatory submission.