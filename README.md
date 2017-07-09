# XenDesktop 7.x Version 2 Documentation Script
Creates an inventory of a Citrix XenDesktop (or XenApp) 7.8+ Site using Microsoft PowerShell and outputs to Microsoft Word, plain text or HTML.

To output to Microsoft Word, Office 2010 or above must be installed on the machine where the script is run from.

This Script requires at least PowerShell version 3 but runs best in version 5. You do NOT have to run this script on a Controller. This script was developed and run from a Windows 10 VM. You can run this script remotely using the –AdminAddress (AA) parameter.
	
By default, only gives summary information for:

		Administrators
		App-V Publishing
		AppDisks
		AppDNA
		Application Groups
		Applications
		Delivery Groups
		Hosting
		Logging
		Machine Catalogs
		Policies
		StoreFront
		Zones

The Summary information is what is shown in the top half of Citrix Studio for:

		Machine Catalogs
		AppDisks
		Delivery Groups
		Applications
		Policies
		Logging
		Administrators
		Hosting
		StoreFront

Using the MachineCatalogs parameter can cause the report to take a very long time to complete and can generate an extremely long report. Using the DeliveryGroups parameter can cause the report to take a very long time to complete and can generate an extremely long report.

Using both the MachineCatalogs and DeliveryGroups parameters can cause the report to take an extremely long time to complete and generate an exceptionally long report.

Creates an output file named after the XenDesktop 7.8+ Site.
	
Word and PDF Document includes a Cover Page, Table of Contents and Footer. Includes support for the following language versions of Microsoft Word:

		Catalan
		Chinese
		Danish
		Dutch
		English
		Finnish
		French
		German
		Norwegian
		Portuguese
		Spanish
		Swedish

NOTE: This script requires PowerShell V3 or later.
NOTE: Best performance is obtained by using PowerShell V5.
NOTE: Word 2007 is not supported. 
Support for non-English Versions of Microsoft Word
The script supports the following languages:

* Catalan
* Chinese
* Danish
* Dutch
* English
* Finnish
* French
* German
* Norwegian
* Portuguese
* Spanish
* Swedish