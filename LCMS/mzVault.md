# mzVault Database

## Sample Analysis

### Sample preparation

- Dissolve standard in acetonitrile.
- Mix into a standard mixture.
- Dilute to 2.5 ppm and 500 ppb.

### MS1

- Do MS1 in both polarities first to see which standards can be found.
- Document m/z value, peak area, and retention time for both polarities.

### MS2

- Make *Target Mass* list for MS2.
- Run samples.

## Build Database

> The first two steps can be skipped if an .xml file exported from mzVault already exists.

### XCalibur Sequence (First time)

An XCalibur sequence can be built to make importing compound information easier:

1. Build a .csv file that will be imported into XCalibur. Fill in compound information in the respective columns
2. Import into XCalibur. Check for errors and save as a .sld file

### Import into mzVault (First time)

1. Import the sequence file into mzVault's **Build** panel.
2. Edit the adduct column.
3. Export to an .xml file to add in further information.

### Edit the xml file

1. Open the .xml file in Excel and choose 'As an XML table'.
2. Use the advanced filter to look up the missing information from the 'msmls-lot-230-13.xlsx' table and fill them in.
3. Save the document as a new .xml file.

### Import into mzVault again

1. Choose 'Open Compound List' under **Build**.
2. Open the save xml file.
3. Select 'Threshold' and 'Recalibrate'.
4. Open 'Selection Parameters'. Choose 'Retrieve one spectrum for each unique collision energy'.
5. Check for errors and click 'Process List'.

## Maintain Database

### Check for errors

- If a compound has spectra in both positive and negative polarities, check that the retention times align. If they don't, go back to the raw file to verify.