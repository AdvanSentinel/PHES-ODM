# Ottawa Wastewater Surveillance Data Model (Ottawa Data Model (ODM))

This repository contains Ottawa Wastewater Surveillance Data Model (Ottawa Data Model (ODM)). Also included are Ottawa wastewater data - other data are welcomed. Plots using this data can be found at: [613covid.ca](https://613covid.ca/wastewater).

See [Metadata](metadata.md) for variable names and definitions.

## Collaborate

The ODM strives to improve wastewater surveillance through the development of a common data structure, including metadata and vocabulary. Also included are templates (under development) to collect and share data. Templates include versions of Excel spreadsheets from different jurisdictions that are based on the ODM. A SQL database structure is available, as well as code to clean data and create tables.

We adhere to the [FAIR Guiding Principles](https://www.go-fair.org/fair-principles/) with recognition of benefit from a common data structure, including metadata and vocabulary.

ODM is a collaborative effort from many people within the wastewater surveillance community in Canada and beyond. See [GH issues](https://github.com/Big-Life-Lab/covid-19-wastewater/issues) or email [dmanuel\@ohri.ca](mailto:dmanuel@ohri.ca), [howard.swerdfeger\@canada.ca](mailto:howard.swerdfeger@canada.ca).

Follow the [`dev`](https://github.com/Big-Life-Lab/covid-19-wastewater/tree/dev) branch for upcoming changes. Also follow version changes in [issues](https://github.com/Big-Life-Lab/covid-19-wastewater/issues), [discussions](https://github.com/Big-Life-Lab/covid-19-wastewater/discussions), and [projects](%3Chttps://github.com/Big-Life-Lab/covid-19-wastewater/projects).

See [Collaborate](collaborate.md) for more information.

## License

Website content is published under a Creative Commons CC BY 4.0 license, which requires users to attribute the source and license type (CC BY 4.0) when sharing our data or website content.

## Changelog

#### 2021-01-15

- Naming conventions were further developed.

- Examples are provided on how to generate wide and long variables and category names.

- Names of variables were updated according to the extended naming conventions. Note that these changes are NOT listed here!

- Information on how to collaborate is updated.

- Measurement metadata
	- `aggregation` - Following the existing options, one more option was added to the list `geoMeanNormal`.

- SiteMeasures metadata: A new table was added  that covers all kinds of measurement data that  are not performed on the wastewater sample but provide additional context necessary for the interpretation of the results.
	- `ID`: (NEW) Unique identifier for each contextual measurement.
	- `Site.ID`: (NEW) Links with the Site table to describe the location of measurement.
	- `dateTime`: (NEW) The date and time the measurement was performed.
	- `type`: (NEW) The type of measurement that was performed. 
	- `typeOther`: (NEW) Description of the measurement in case it is not listed in type.
	- `typeDescription`: (NEW) Additional information on the performed measurement.
	- `instrumentName`: (NEW) Name of the instrument used to perform the measurement.
	- `instrumentType`: (NEW) Type of instrument used to perform the measurement.
	- `instrumentTypeOther`: (NEW) Description of the instrument in case it is not listed in instrumentType.
	- `aggregation`: (NEW) When reporting an aggregate measurement, this field describes the method used.
	- `aggregationOther`: (NEW) Description for other type of aggregation not listed in aggregation.
	- `aggregationDescription`: (NEW) Information on OR reference to which measurements that were included to calculate the aggregated measurement that is being reported.
	- `value`: (NEW) The actual value that is being reported for this measurement.
	- `unit`: (NEW) The engineering unit of the measurement.
	- `qualityFlag`: (NEW) Does the reporter suspect quality issues with the value of this measurement? (Boolean)
	- `notes`: (NEW) Any additional notes.
- Sample metadata
	- `samplingTempC`: (NEW) Temperature that the sample is stored at while it is being sampled. This field is mainly relevant for composite samples which are either kept at ambient temperature or refrigerated while being sampled.
	- `mailedOnIce`: (NEW) Was the sample kept cool while being sent to the lab? (Boolean)
	- `category` - A distinction is now made between SARS-CoV-2 gene measurements `covid` and the measurement of water quality parameters on the sample `wq`.
- Site metadata
	- `type` - Additional site types were added `airplane`, `correctionalFacility`, `elementarySchool`, `hospital`, `longTermCareFacility`, `sewageTruck`, `universityCampus`, `WWTP`
	- `accessType`: (NEW) Access point of where the sample was collected at the site.
	- `measurement.fractionAnalyzedDefault`: (NEW) Used as default when a new measurement is created for this site. See `fractionAnalyzed` in `Measurement` table.
- AssayMethod: New variables were introduced to replace `assayDesc`, those are
	- `methodConcentration`: (NEW) Description of the method used to concentrate the sample
	- `methodExtraction`: (NEW) Description of the method used to extract the sample
	- `methodPcr`: (NEW) Description of the PCR method used
	- `qualityAssuranceQC`: (NEW) Description of the quality control steps taken
	- `inhibition`: (NEW) Description of the inhibition parameters.
	- `surrogateRecovery`: (NEW) Description of the surrogate recovery for this method.
	- `description`: (NEW) Description of the assay.
	- `referenceLink`: (NEW) Link to standard operating procedure (assay reference method)
- CovidPublicHealthData
	- `valueType`: (NEW) A categorical variable that replaces the individual variables, instead it provides listed options: `confirmed`, `active`, `tests`, `positiveTests`, `percentPositivityRate`, `hospitalCensus`, `hospitalAdmit` 
- Lookups metadata: A new table that is used as a reference for categorical variables

#### 2021-01-08

-   All variable names were updated according to the name convention. 

#### 2020-11-25

-   Change date formatting on `wastewater_virus.csv` to YYYY-MM-DD.

#### 2020-11-25

v0.1.1 - Additions to metadata. No breaking changes.

-   Measurement metadata

    -   Add categories `measurementType`:

        -   `geoMean`: GeoMean of results
        -   `rangeLowestValue`: Lowest value in a range of values
        -   `rangeHighestValue`: Highest value in a range of values
        -   `singleton`: This value is not an aggregate measurement in any way, and thus is not a `mean`, `median`, `geomean` or other

    -   Add `measureValueDetected`: Boolean Value if True then covid-19 was detected.

    -   Add `reportDate`: Note use of `reportDate` when historic results are updated for new reporting standards.

-   AssayMethod metadata

    -   Add `sampleSizeL`: Size of the sample that is analysed in liters
    -   Add `loq`: Limit of Quantification for this method if one exists
    -   Add `lod`: Limit of detection for this method if one exists
    -   Add `inhibition`: Text decription of the inhibition
    -   Add `surrogateRecovery`: Text description of the Surrogate Recovery for this method

-   Other small corrections to metadata category labels.

-   CovidPublicHealthData

    -   `dateType`: Type of date used.

-   Updated `wastewater_virus.csv` to reflect metadata v0.1.1.

#### 2020-11-17

v0.1.0 - Breaking changes to metadata.

-   Assay method database added.
-   Change test results to be represented as key:values. Each test result has a measurement type (`measureType`) with a corresponding value (`measureValue`). For example a measureType is `mean` and the corresponding `measureValue` has the mean value.

#### 2020-11-16

-   `wastewater_virus.csv` dataset updated to remove adjustment for percent viral recovery from solids. The adjustment allign reporting with other laboratories. The adjustment reduces N1 and N2 values a maginitude of 10 (approximately).

#### 2020-10-29

-   Replace invalid values (such as \#DIV/0) with `NA`.

#### 2020-10-27

V0.0.2 - Breaking changes to metadata.

-   Change `locationID` to `siteID`.
-   Change `locationName` to `siteName`.

#### 2020-10-16

-   All Ottawa data points prior to Oct 2nd have been slightly modified to normalize data for a new centrifuge that is being used to collect wastewater samples at the Ottawa site.

#### 2020-10-09

V0.0.1 - Initial variable names and labels.
