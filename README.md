# SyncMigration
Sync Service Migration Helper Scripts

# Author
Carol Wapshere

# Sync Config Comparison
These scripts are used to summarise the confguration of a FIM Sync server in a set of CSV file reports, and then compare two sets of CSV reports showing the differences. This is helpful when migrating configrations between two environments, comparing the differences between two environments, and comparing configuration before and after a change.

[Link to blog post with screenshots](http://www.wapshere.com/missmiis/comparing-two-fim-sync-services).

# Upgrade Migration Toolkit
Presented at TEC 2012, this group of scripts are designed to help with a migration of a Sync service from MIIS/ILM to FIM. The scripts designed to run on the MIIS/ILM server are written in VBScript in case PowerShell is not installed.

## ReportServer.vbs
* MIIS/ILM/FIM,
* Reports general stats about the Sync Server,
* May be run by the customer as part of pre-consulting research.
This script produces a number of reports about the server:

### Installed Software.html
* Lists Applications installed on the server.
* Look out for:
  * Minimum MIIS SP2 for DB transfer method,
  * Unexpected apps on the server that the customer views as “part of the system”.
### MA Stats.html, MV Stats.html
* Gets stats about MV and CS objects from WMI and the database.
* Look out for:
  * Manual Joins, Explicit Disconnectors,
  * Orphaned objects,
  * Sync Errors,
  * Last Full Sync – “Delta only” MAs a problem,
  * Long Sync run times.
### Server Configuration Export
The script also exports the server configuration to the same Reports folder as the other reports. 

## ReportExtensions.vbs
* MIIS/ILM/FIM,
* Keyword based high-level overview of Extension projects,
* May be run by the customer as part of pre-consulting research.
This script produces the following report:

### Extension Projects.html
* Lists non-MIIS include files and procedures.
* Look out for:
  * Unusual Include files
  * Unsupported configuration – eg., running external processes from extension code
  * Modified GalSync extensions
  * Generally messy extension projects

### ConvertToHTML-ServerConfig.ps1
* MIIS/ILM only,
* Converts a full server config export to HTML reports.
### Report-AttributeFlows.ps1
* MIIS/ILM/FIM,
* Produces a CSV summarising attribute flow rules from a full server config export. 
### Report-Joins.ps1
* MIIS/ILM/FIM,
* May help with judging tidiness (or otherwise) of metaverse data by counting unique join patterns,
* May take some time to run and sync jobs must be stopped - should only be run at a pre-arranged time,
* A large number of different join patterns may indicate bad joins and duplicates. Should be analysed with someone who knows the site well.
### Export_Joins.vbs
* MIIS/ILM/FIM,
* Produces a CSV identifying CS objects and the Metaverse objects they are joined to,
* May be used when a CS needs to be cleared or re-created, to ensure objects are rejoined exactly as before,
* Import the CS object identifier via a seperate CSV MA, then use to join in the reimported CS.
### CSExportToCSV.vbs
* MIIS/ILM/FIM,
* Generate a CSV file from a csexport dump,
* Use when no actual data source exists for a CSV MA, so a repopulation Full Import is not possible,
* The stylesheet must be modified to include the required attraibutes.
### ExportPendingExports.vbs, ConvertToHTML-PendingExports.ps1
* MIIS/ILM/FIM,
* Use to compare pending exports from all MAs on two Sync servers,
* The vbscript uses csexport to generate one XML file per MA,
* The powershell script converts the XML dumps to a single HTML page to allow simpler comparison.
 
