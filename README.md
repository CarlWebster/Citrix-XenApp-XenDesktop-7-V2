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

## Prerequisites
Before we can start using PowerShell to document anything in a XenDesktop 7.x Site, let us ensure we have the necessary requirements.

If the script will be run remotely, there are two choices: install Citrix Studio or manually install the PowerShell snap-ins.
		1. [ ] Install Studio from the full XenDesktop 7.x installation media. Installing Citrix Studio will install all the necessary PowerShell snapins.
		2. [ ] Install the PowerShell snapins individually. Depending on the bitness of the computer, from the full XenDesktop 7.x installation media, install the following files from either x64 or x86 (?? is either 86 or 64):
	* Citrix Desktop Delivery Controller\ADIdentity_PowerShellSnapIn_x??
	* Citrix Desktop Delivery Controller\Analytics_PowerShell_SnapIn_x??
	* Citrix Desktop Delivery Controller\AppLibrary_PowerShell_SnapIn_x??
	* Citrix Desktop Delivery Controller\Broker_PowerShell_SnapIn_x??
	* Citrix Desktop Delivery Controller\Configuration_PowerShell_SnapIn_x??
	* Citrix Desktop Delivery Controller\ConfigurationLogging_PowerShell_SnapIn_x??
	* Citrix Desktop Delivery Controller\DelegatedAdmin_PowerShellSnapIn_x??
	* Citrix Desktop Delivery Controller\EnvTest_PowerShell_SnapIn_x??
	* Citrix Desktop Delivery Controller\Host_PowerShell_SnapIn_x??
	* Citrix Desktop Delivery Controller\MachineCreation_PowerShellSnapIn_x??
	* Citrix Desktop Delivery Controller\Monitor_PowerShellSnapIn_x??
	* Citrix Desktop Delivery Controller\Orchestration_PowerShellSnapIn_x??
	* Citrix Desktop Delivery Controller\Storefront_PowerShellSnapIn_x??
	* Citrix Desktop Delivery Controller\Trust_PowerShellSnapIn_x??
	* Citrix Desktop Delivery Controller\UserProfileManager_PowerShellSnapIn_x??
	* 7.13 and later: Citrix Desktop Delivery Controller\XDPoshSnapin_x??
	* Citrix Policy\CitrixGroupPolicyManagement_x??
	* DesktopStudio\PVS PowerShell SDK x??
	* DesktopStudio\PzAppV_Studio_PowershellSnapin_x??
	* Licensing\LicensingAdmin_PowerShellSnapIn_x??

Install the Citrix Group Policy PowerShell module. There are two options, download the module or copy the file from a Controller.
1. Download the file:
	* In your Internet browser; go to https://dl.dropboxusercontent.com/u/43555945/Citrix.GroupPolicy.Commands.zip.
	* Save the file to your default download folder.
	* Extract the file to C:\XD7Script.
	* Close your Internet browser.
2. Copy the file from a Controller:
* On a 32-bit Controller, go to %PROGRAMFILES%\Citrix\Scout\Current\Utilities
* On a 64-bit Controller, go to %PROGRAMFILES(x86)%\Citrix\Scout\Current\Utilities
* If you are running 32-bit or 64-bit Windows, copy the file Citrix.GroupPolicy.Commands.psm1 to C:\Windows\System32\WindowsPowerShell\v1.0\Modules, in a new folder named Citrix.GroupPolicy.Commands. This should be placed on the computer where the script is run.
* If you are running 64-bit Windows, copy the file Citrix.GroupPolicy.Commands.psm1 to C:\Windows\SysWOW64\WindowsPowerShell\v1.0\Modules, in a new folder named Citrix.GroupPolicy.Commands. This should be placed on the computer where the script is run.

**Note**: The Citrix.GroupPolicy.Commands.psm1 file is not the version that comes with XenApp 6.5. This is an updated version that comes installed with XenDesktop 7.x or with Citrix Scout.  The XenApp 6.5 file is from September 2011, the updated version is from June 2014. The updated version allows the policy cmdlets to be run against a remote Controller. You cannot use the updated version to run against a remote XenApp 6.5 Collector.