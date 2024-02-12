# Standard Operating Procedure for Using Compound Discoverer 3.3 for Untargeted Metabolomics Study<br>使用Compound Discoverer 3.3进行非靶向代谢组学分析

## Introduction<br>简介

### Purpose<br>目的

> The purpose of this Standard Operating Procedure (SOP) is to provide guidelines for using Compound Discoverer 3.3 software for untargeted metabolomics studies.

> 本标准操作程序（SOP）的目的是为使用Compound Discoverer 3.3 (CD 3.3)软件进行非靶向代谢组学研究提供指导。

### Scope<br>适用范围

> This SOP applies to researchers and analysts who are using Compound Discoverer 3.3 for untargeted metabolomics analysis.

> 本SOP适用于使用CD 3.3进行非靶向代谢组学分析的研究和分析人员。

## Equipment and Software Requirements<br>设备和软件要求

### CD 3.3<br>软件

- Ensure that Compound Discoverer 3.3 software is installed and properly configured on the analysis computer.

### Mass spectrometry data<br>质谱数据

- Have the .raw format data files ready.
- (Recommended) Make sensible names for the data by including relevant information such as sample group and ionization mode.

### Connection to the databases<br>数据库连接

- Test the internet connection to the mzCloud database from **Help** > **Communication Tests**.
- Click *Run Tests*, and make sure the connection test passes.

## Pre-analysis Preparation<br>设置分析文件

### Create a new study<br>创建新项目

- Create a new study for new samples. Do not use old studies repeatedly.
- At **Start Page**, click *New Study and Analysis...*.
- Specify a *Study Name* and a *Studies Folder*. A new folder will be automatically created for the new study within the *Studies Folder*.
- (Recommended) In the *Description* box, write down relevant information of the study.
- Select a *Workflow* from the drop-down list.
- Click *Next* to proceed. 

### Add files to the study<br>添加数据文件

- Click *Add Files* to add all the data files.
- Click *Next* to proceed.
- Specify *Sample Type*. Important sample types are:
	- *Sample*, *Control*, *Standard*: Identifies the compound in these files.
	- *Blank*: Blanks, used for marking background compounds.
	- *Identification Only*: Use the fragmentation in this type of files for compound identification, but peak areas in these files are not reported.
	- *Quality Control*: QC samples used for correcting peak area deviation for long sequences of samples. QC samples should be placed at least every 10 samples.
	- *Labeled*: Used for identifying isotope labeled compounds.
- (Optional) Additional groups can be defined by the user. Click *Add* in the **Study Factors** panel to add a new group. This can be based on experimental conditions, time points, or any other relevant criteria. If the grouping information is included in the [file names](###Mass%20Spectrometry%20Data), the grouping for each data file can be populated automatically by clicking *Assign*.
- Click *Next* to proceed.

### (Optional) Set groups for statistical analysis<br>设置样本分组

- CD 3.3 can perform t test or ANOVA.
- Set the groups to compare (i.e. treatment vs. control).
- Click *Next* to proceed.

### Finish setting up the study<br>完成创建

- Click *Finish*.

## Analysis Parameters Configuration<br>设定分析参数

### Set the files to be analyzed<br>设定分析文件

- Navigate to the **Workflows** panel.
- Modify the **Files for Analysis** according to the study.
- If the data are acquired in pos or neg ionization mode separately, analyze them separately. Otherwise [retention time alignment](####Align%20Retention%20Time%20(ChromAlign)) will not work properly.

### Modify the workflow<br>修改分析流程

> A brief introduction is given below for each important node. For more information, consult the help document.

#### Select Spectra

- Provides a set of filters to limit what spectra are analyzed.
- Basic parameters are upper and lower *RT limit*. Adjust as needed.

#### Align Retention Time (ChromAlign)

- Aligns the retention time of peaks across multiple data files.
- *Reference File*: Use the drop-down menu to choose one file as the reference. This could be the first sample or a QC sample.

#### Detect Compounds

- Finds the peaks in the samples.
- *Max Peak Width \[min]*: the max allowed peak width at half height. This parameter should be adjusted according to the data for better results.
- *Ions*: a list of possible adducts present in the sample should be selected here. Adjust this list according to sample preparation procedures, mobile phase conditions, and the ionization mode.
- *Base Ions*: Adducts that are most likely to have the highest intensity, usually just \[M+H]+ and \[M-H]-.

#### Group Compounds

- Group the peaks likely from the same compound across the sample files using m/z value and retention time.
- *Mass Tolerance*, *RT Tolerance*: peaks within both these ranges will be grouped as the same compound.
- *Preferred Ions*: The preferred adduct to select fragmentation data for mzCloud database search, usually \[M+H]+ or \[M-H]- depending on the ionization mode.
- *Peak Rating Contributions*: determines the weights for calculating the peak rating.
- *Peak Rating Filter*: set a filter for low quality peaks. Peaks must have > *Peak Rating Threshold* in at least *Number of Files* to be analyzed in the next steps. A filter is mandatory when there are many sample files.

> The next few nodes identify the peaks by querying databases with m/z value, retention time, and MS2 spectra.

#### Predict Compositions

- Predict the elemental compositions of the compounds.
- Must have this node.

#### Search ChemSpider

- *Databases*: choose a few databases to search according to the nature of study.
- *Search Mode*:
	- Formula: Use predicted formula from the [Predict Compositions](####Predict%20Compositions) node to search ChemSpider.
	- Mass: Use calculated molecular weight to search ChemSpider.

#### Search mzCloud

- Searches MS2 spectra in the mzCloud database.
- *Compound Classes*: choose a few databases to search according to the nature of study.
- *Identity Search*: the algorithm to calculate similarity of the spectra. Choose HighChem HighRes.

#### Search mzVault

- Searches offline MS2 spectra libraries.
- Custom libraries can be loaded by clicking the *Open the Lists & Libraries Manager* button in the **Tool Bar**.

#### Apply mzLogic

- Complements mzCloud search when the mzCloud database does not have a match for the spectra.
- Compares spectra of unknown to spectra in mzCloud.
- Use spectra matches to identify substructures present.
- Use exact mass of the compound to search online databases.
- Screen the exact mass matches for the substructures.
- Score the candidates based on a number of factors, including the similarity of the structure to known compounds, the presence of characteristic fragmentation ions, and the overall quality of the mass spectrum.

#### Assign Compound Annotations

- Sets the priority of the data sources for the final compound annotation.
- (Recommended) Set mzCloud at the top when MS2 data is available.

> The following nodes are used in more specific situations.

#### Analyze Labeled Compounds

- Require unlabeled and labeled samples. This node finds labeled compound in the sample in an untargeted way. 
- The labeled samples should have [sample type](###Add%20Files%20to%20the%20study) set to *Labeled*.
- *Label Element* can be set to other elements from \[13]C.
- *Exchange Rates* can be viewed in the **Compounds** table in the result:
	- Exchange Rate: % of each mass isotopologue.
	- Max Exchange: Max number of atoms that can be labeled.
	- Avg. Exchange: Weighted sum of exchange rates for the mass isotopologues.
	- Rel. Exchange: Avg. Exchange/Max Exchange in percentages (Isotope Abundance).
- *Labeling Status* can have the following colors:
	- <mark style="background: #FF5582A6;">Red</mark>: Contaminating mass; a compound has avg. exchange > 0.1 in unlabeled sample.
	- <mark style="background: #BBFABBA6;">Green</mark>: No warnings; the measured isotope patterns and the exchange rates are within acceptable limits. 
	- <mark style="background: #CACFD9A6;">Gray</mark>: Compound not found.
	- <mark style="background: #FFB86CA6;">Orange</mark>: Low pattern fit; The measured isotopic distribution is very different from theoretical distribution according to *SFit*, *Measured Coverage*, or *Fitted Coverage*.
	- <mark style="background: #ADCCFFA6;">Blue</mark>: Irregular distribution; The distribution is not continuous (i.e. have M+1, M+4 but not M+2, M+3).  

#### Mark Background Compounds

- Should be used when there are blank samples.
- *Max Sample/Blank*: set to a reasonable number; when a compound found in blank is found also in at least this many number of samples, it is not considered a background compound.

#### Apply SERRF QC Correction

- Should be used when peak areas will be used for statistical analysis and when there is a large number of samples.
- [QC](###Add%20Files%20to%20the%20study) sample types need to be set.
- Compounds not passing the *Min QC Coverage*, *Max QC Area RSD*, *Max Corrected QC Area RSD* will not have corrected area.
- *# Batches* should be set according to experimental conditions.

#### Fill Gaps

- Should be used when peak areas will be used for statistical analysis.
- If a peak is found in sample A and C, look for the compound in sample B. 
- If it is present in B but removed due to low intensity or other reasons, add it back into the result.

#### Apply Missing Value Imputation

- Consider using when peak areas will be used for statistical analysis.
- Use the *Random Forest Imputation* algorithm to fill missing peaks (not real data) when [groups](###Optional%20Set%20groups%20for%20statistical%20analysis) are set.
- Otherwise uses *Median + Small Value with Variability*.

### Run the analysis<br>执行分析

- Double check the workflow before proceeding. Save a copy if necessary by clicking *Save* or *Save Common* at the top of the **Workflows** panel.
- (Recommended) Change the name of the result file at the *Result File* box. Make a sensible name.
- Click *Run*.

### View analysis progress<br>查看进度

- Go to the **Job Queue** tab.
- Click the ﹢sign next to a job to expand its progress report.
- Check the *Display Verbose Messages* to display verbose progress report.
- Click on a job, then click the *Abort* button to abort a job.

## Result Visualization<br>查看结果

### View the result tables<br>查看结果表格

- The **Compounds** table lists all the compounds detected in the data.
- The **Compounds per File** table lists all the compounds in each study file.
	- Each compound can be associated with more than one adduct.
	- *# Adducts*: The number of associated adducts.
	- *Area (All Ions)*: Sum of area for all associated adducts of this compound.
	- *Area Ref. Ion*: Sum of area for all the major adducts of this compound. Usually the major adduct is \[M+H]+ or \[M-H]-.
- The **Features per File** table lists all the adduct ions associated with each compound.
- Click *Show Related Tables* at the bottom to show the related tables for the row selected.

### Filter the result tables<br>筛选表格内容

- Filters can be applied to any of the result tables.
- Click the *Show result filters* button in the **Tool Bar** to open the filter window.
- Select a table on the left and edit the filters on the right. Any column can be filtered. In addition, AND and OR clauses can be used.

### Export the result tables<br>导出结果表格

- The result tables can be saved as an Excel spreadsheet.
- *Right click* anywhere on the table, a menu will show up.
- Move the cursor to *Export* at the bottom of the menu, and choose *As Excel...*
- Enter the name of the Excel file, the tables to be exported, and the range of items. Click *Export*, the current table will be saved.
- If a filter has been applied to the table, the table is saved at its filtered state automatically.

### Reprocess the result<br>重新进行分析

- The results can be reprocessed by going to the **Analysis Results** tab, right clicking on a result row, and selecting *Reprocess*.
- The workflow used for the selected result will appear in the **Workflow** tab. Make edits and rerun the analysis.

## Data Storage and Management<br>数据存储及管理

### Data Backup<br>数据备份

- Ensure that all raw data files, CD 3.3 study files, and analysis results are properly backed up and stored securely to prevent data loss.
- Workflow parameters can be viewed by clicking the *Show result summary* button in the **Tool Bar**
- (Recommended) Write a brief description.txt in the study folder to document any other information pertinent to the study.

### Data Retention<br>数据保留

- Establish a data retention policy to determine the duration and storage location for your data based on the specific requirements of your organization or funding agency.

## Revision History<br>版本历史

> Document the revisions made to this SOP, including the date of each revision and a brief description of the changes according to the following example.

> 参照以下示例记录对本 SOP 所做的修订，包括每次修订的日期，并简要说明修订内容。

| Date       | Person      | Detail       |
| ---------- | ----------- | ------------ |
| 2023-07-11 | Chuyao Wang | First draft. |
| 2023-07-17 | Chuyao Wang | Added the *Reprocess the result* section.|

## Note<br>注意事项

> This SOP provides general guidelines for using Compound Discoverer 3.3 for untargeted metabolomics studies. It is important to refer to the software's user manual, tutorials, and other documentation for detailed instructions specific to the experiment and analysis you are performing.  

> 本 SOP 提供了使用 Compound Discoverer 3.3 进行非靶向代谢组学研究的一般指导原则。请参阅软件的用户手册、教程和其他文档，以了解针对您正在进行的实验和分析的详细说明。