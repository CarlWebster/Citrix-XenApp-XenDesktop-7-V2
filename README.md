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

1. Install Studio from the full XenDesktop 7.x installation media. Installing Citrix Studio will install all the necessary PowerShell snapins.

2. Install the PowerShell snapins individually. Depending on the bitness of the computer, from the full XenDesktop 7.x installation media, install the following files from either x64 or x86 (?? is either 86 or 64):

		Citrix Desktop Delivery Controller\ADIdentity_PowerShellSnapIn_x??
		Citrix Desktop Delivery Controller\Analytics_PowerShell_SnapIn_x??
		Citrix Desktop Delivery Controller\AppLibrary_PowerShell_SnapIn_x??
		Citrix Desktop Delivery Controller\Broker_PowerShell_SnapIn_x??
		Citrix Desktop Delivery Controller\Configuration_PowerShell_SnapIn_x??
		Citrix Desktop Delivery Controller\ConfigurationLogging_PowerShell_SnapIn_x??
		Citrix Desktop Delivery Controller\DelegatedAdmin_PowerShellSnapIn_x??
		Citrix Desktop Delivery Controller\EnvTest_PowerShell_SnapIn_x??
		Citrix Desktop Delivery Controller\Host_PowerShell_SnapIn_x??
		Citrix Desktop Delivery Controller\MachineCreation_PowerShellSnapIn_x??
		Citrix Desktop Delivery Controller\Monitor_PowerShellSnapIn_x??
		Citrix Desktop Delivery Controller\Orchestration_PowerShellSnapIn_x??
		Citrix Desktop Delivery Controller\Storefront_PowerShellSnapIn_x??
		Citrix Desktop Delivery Controller\Trust_PowerShellSnapIn_x??
		Citrix Desktop Delivery Controller\UserProfileManager_PowerShellSnapIn_x??
		7.13 and later: Citrix Desktop Delivery Controller\XDPoshSnapin_x??
		Citrix Policy\CitrixGroupPolicyManagement_x??
		DesktopStudio\PVS PowerShell SDK x??
		DesktopStudio\PzAppV_Studio_PowershellSnapin_x??
		Licensing\LicensingAdmin_PowerShellSnapIn_x??

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

## Script Usage
How to use this script:

1. Save the script as XD7_Inventory_V2.ps1 in your PowerShell scripts folder.

2. From the PowerShell prompt, change to your PowerShell scripts folder. From the PowerShell prompt, type in:

		.\XD7_Inventory_V2.ps1

By default, a Microsoft Word document is created named after the XenDesktop 7.x Site.

If you use the –PDF option, a PDF file is created named after the XenDesktop 7.x Site.

If you use the –HTML option, an HTML file is created named after the XenDesktop 7.x Site.

If you use the –Text option, a Text file is created named after the XenDesktop 7.x Site.

3. To run the script against a remote Controller:

		.\XD7_Inventory_V2.ps1-AdminAddress DDCName

4. Full help text is available.

		Get-Help .\XD7_Inventory_V2.ps1 –full

The help text explains all the parameters the script accepts.

## Help Text

PS C:\Scripts> get-help .\XD7_Inventory_V2.ps1 -full

NAME
    C:\Scripts\XD7_Inventory_V2.ps1

SYNOPSIS
    Creates an inventory of a Citrix XenDesktop 7.8+ Site.

SYNTAX

    C:\Scripts\XD7_Inventory_V2.ps1 [-MSWord] [-AddDateTime] [-AdminAddress 
    <String>] [-Administrators] [-AppDisks] [-Applications] [-BrokerRegistryKeys] 
    [-CompanyAddress <String>] [-CompanyEmail <String>] [-CompanyFax <String>] 
    [-CompanyName <String>] [-CompanyPhone <String>] [-CoverPage <String>] 
    [-DeliveryGroups] [-DeliveryGroupsUtilization] [-Dev] [-EndDate <DateTime>] [-Folder 
    <String>] [-Hardware] [-Hosting] [-Log] [-Logging] [-MachineCatalogs] [-MaxDetails] 
    [-NoADPolicies] [-NoPolicies] [-Policies] [-ScriptInfo] [-Section <String>] 
    [-StartDate <DateTime>] [-StoreFront] [-UserName <String>] [-VDARegistryKeys] 
    [<CommonParameters>]

    C:\Scripts\XD7_Inventory_V2.ps1 [-HTML] [-MSWord] [-PDF] [-Text] [-AddDateTime] 
    [-AdminAddress <String>] [-Administrators] [-AppDisks] [-Applications] 
    [-BrokerRegistryKeys] [-CompanyAddress <String>] [-CompanyEmail <String>] 
    [-CompanyFax <String>] [-CompanyName <String>] [-CompanyPhone <String>] [-CoverPage 
    <String>] [-DeliveryGroups] [-DeliveryGroupsUtilization] [-Dev] [-EndDate <DateTime>] 
    [-Folder <String>] [-Hardware] [-Hosting] [-Log] [-Logging] [-MachineCatalogs] 
    [-MaxDetails] [-NoADPolicies] [-NoPolicies] [-Policies] [-ScriptInfo] [-Section 
    <String>] [-StartDate <DateTime>] [-StoreFront] [-UserName <String>] 
    [-VDARegistryKeys] -SmtpServer <String> [-SmtpPort <Int32>] [-UseSSL]
    -From <String> -To <String> [<CommonParameters>]

    C:\Scripts\XD7_Inventory_V2.ps1 [-HTML] [-AddDateTime] [-AdminAddress 
    <String>] [-Administrators] [-AppDisks] [-Applications] [-BrokerRegistryKeys] 
    [-DeliveryGroups] [-DeliveryGroupsUtilization] [-Dev] [-EndDate <DateTime>] [-Folder 
    <String>] [-Hardware] [-Hosting] [-Log] [-Logging] [-MachineCatalogs] [-MaxDetails] 
    [-NoADPolicies] [-NoPolicies] [-Policies] [-ScriptInfo] [-Section <String>] 
    [-StartDate <DateTime>] [-StoreFront] [-VDARegistryKeys] [<CommonParameters>]

    C:\Scripts\XD7_Inventory_V2.ps1 [-PDF] [-AddDateTime] [-AdminAddress <String>] 
    [-Administrators] [-AppDisks] [-Applications] [-BrokerRegistryKeys] [-CompanyAddress 
    <String>] [-CompanyEmail <String>] [-CompanyFax <String>] [-CompanyName <String>] 
    [-CompanyPhone <String>] [-CoverPage <String>] [-DeliveryGroups] 
    [-DeliveryGroupsUtilization] [-Dev] [-EndDate <DateTime>] [-Folder <String>] 
    [-Hardware] [-Hosting] [-Log] [-Logging] [-MachineCatalogs] [-MaxDetails] 
    [-NoADPolicies] [-NoPolicies] [-Policies] [-ScriptInfo] [-Section <String>] 
    [-StartDate <DateTime>] [-StoreFront] [-UserName <String>] [-VDARegistryKeys] 
    [<CommonParameters>]

    C:\Scripts\XD7_Inventory_V2.ps1 [-Text] [-AddDateTime] [-AdminAddress 
    <String>] [-Administrators] [-AppDisks] [-Applications] [-BrokerRegistryKeys] 
    [-DeliveryGroups] [-DeliveryGroupsUtilization] [-Dev] [-EndDate <DateTime>] [-Folder 
    <String>] [-Hardware] [-Hosting] [-Log] [-Logging] [-MachineCatalogs] [-MaxDetails] 
    [-NoADPolicies] [-NoPolicies] [-Policies] [-ScriptInfo] [-Section <String>] 
    [-StartDate <DateTime>] [-StoreFront] [-VDARegistryKeys] [<CommonParameters>]


DESCRIPTION
    Creates an inventory of a Citrix XenDesktop 7.8+ Site using Microsoft PowerShell, Word,
    plain text, or HTML.

    This Script requires at least PowerShell version 3 but runs best in version 5.

    Word is NOT needed to run the script. This script will output in Text and HTML.

    You do NOT have to run this script on a Controller. This script was developed and run
    from a Windows 10 VM.

    You can run this script remotely using the –AdminAddress (AA) parameter.

    This script supports versions of XenApp/XenDesktop starting with 7.8.

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

    Using the MachineCatalogs parameter can cause the report to take a very long time to
    complete and can generate an extremely long report.

    Using the DeliveryGroups parameter can cause the report to take a very long time to
    complete and can generate an extremely long report.

    Using both the MachineCatalogs and DeliveryGroups parameters can cause the report to
    take an extremely long time to complete and generate an exceptionally long report.

    Creates an output file named after the XenDesktop 7.8+ Site.

    Word and PDF Document includes a Cover Page, Table of Contents and Footer.
    Includes support for the following language versions of Microsoft Word:
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



PARAMETERS
    -HTML [<SwitchParameter>]
        Creates an HTML file with an .html extension.
        This parameter is disabled by default.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -MSWord [<SwitchParameter>]
        SaveAs DOCX file
        This parameter is set True if no other output format is selected.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -PDF [<SwitchParameter>]
        SaveAs PDF file instead of DOCX file.
        This parameter is disabled by default.
        The PDF file is roughly 5X to 10X larger than the DOCX file.
        This parameter requires Microsoft Word to be installed.
        This parameter uses the Word SaveAs PDF capability.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Text [<SwitchParameter>]
        Creates a formatted text file with a .txt extension.
        This parameter is disabled by default.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -AddDateTime [<SwitchParameter>]
        Adds a date timestamp to the end of the file name.
        The timestamp is in the format of yyyy-MM-dd_HHmm.
        June 1, 2019 at 6PM is 2019-06-01_1800.
        Output filename will be ReportName_2019-06-01_1800.docx (or .pdf).
        This parameter is disabled by default.
        This parameter has an alias of ADT.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -AdminAddress <String>
        Specifies the address of a XenDesktop controller the PowerShell snapins will connect
        to.
        This can be provided as a hostname or an IP address.
        This parameter defaults to Localhost.
        This parameter has an alias of AA.

        Required?                    false
        Position?                    named
        Default value                Localhost
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Administrators [<SwitchParameter>]
        Give detailed information for Administrator Scopes and Roles.
        This parameter is disabled by default.
        This parameter has an alias of Admins.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -AppDisks [<SwitchParameter>]
        Gives detailed information for all AppDisks.

        This parameter is disabled by default.
        This parameter has an alias of AD.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Applications [<SwitchParameter>]
        Gives detailed information for all applications.
        This parameter is disabled by default.
        This parameter has an alias of Apps.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -BrokerRegistryKeys [<SwitchParameter>]
        Adds information on 315 registry keys to the Controller section.

        For Word and PDF output, this adds eights pages, per Controller, to the report.
        For Text and HTML, this adds 315 lines, per Controller, to the report.

        This parameter is disabled by default.
        This parameter has an alias of BRK.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -CompanyAddress <String>
        Company Address to use for the Cover Page, if the Cover Page has the Address field.

        The following Cover Pages have an Address field:
                Banded (Word 2013/2016)
                Contrast (Word 2010)
                Exposure (Word 2010)
                Filigree (Word 2013/2016)
                Ion (Dark) (Word 2013/2016)
                Retrospect (Word 2013/2016)
                Semaphore (Word 2013/2016)
                Tiles (Word 2010)
                ViewMaster (Word 2013/2016)

        This parameter is only valid with the MSWORD and PDF output parameters.
        This parameter has an alias of CA.

        Required?                    false
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -CompanyEmail <String>
        Company Email to use for the Cover Page, if the Cover Page has the Email field.

        The following Cover Pages have an Email field:
                Facet (Word 2013/2016)

        This parameter is only valid with the MSWORD and PDF output parameters.
        This parameter has an alias of CE.

        Required?                    false
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -CompanyFax <String>
        Company Fax to use for the Cover Page, if the Cover Page has the Fax field.

        The following Cover Pages have a Fax field:
                Contrast (Word 2010)
                Exposure (Word 2010)

        This parameter is only valid with the MSWORD and PDF output parameters.
        This parameter has an alias of CF.

        Required?                    false
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -CompanyName <String>
        Company Name to use for the Cover Page.
        The default value is contained in
        HKCU:\Software\Microsoft\Office\Common\UserInfo\CompanyName or
        HKCU:\Software\Microsoft\Office\Common\UserInfo\Company, whichever is populated
        on the computer running the script.

        This parameter is only valid with the MSWORD and PDF output parameters.
        This parameter has an alias of CN.

        Required?                    false
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -CompanyPhone <String>
        Company Phone to use for the Cover Page if the Cover Page has the Phone field.

        The following Cover Pages have a Phone field:
                Contrast (Word 2010)
                Exposure (Word 2010)

        This parameter is only valid with the MSWORD and PDF output parameters.
        This parameter has an alias of CPh.

        Required?                    false
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -CoverPage <String>
        What Microsoft Word Cover Page to use.
        Only Word 2010, 2013 and 2016 are supported.
        (default cover pages in Word en-US)

        Valid input is:
                Alphabet (Word 2010. Works)
                Annual (Word 2010. Doesn't work well for this report)
                Austere (Word 2010. Works)
                Austin (Word 2010/2013/2016. Doesn't work in 2013 or 2016, mostly
                works in 2010 but Subtitle/Subject & Author fields need to be moved
                after title box is moved up)
                Banded (Word 2013/2016. Works)
                Conservative (Word 2010. Works)
                Contrast (Word 2010. Works)
                Cubicles (Word 2010. Works)
                Exposure (Word 2010. Works if you like looking sideways)
                Facet (Word 2013/2016. Works)
                Filigree (Word 2013/2016. Works)
                Grid (Word 2010/2013/2016. Works in 2010)
                Integral (Word 2013/2016. Works)
                Ion (Dark) (Word 2013/2016. Top date doesn't fit; box needs to be
                manually resized or font changed to 8 point)
                Ion (Light) (Word 2013/2016. Top date doesn't fit; box needs to be
                manually resized or font changed to 8 point)
                Mod (Word 2010. Works)
                Motion (Word 2010/2013/2016. Works if top date is manually changed to
                36 point)
                Newsprint (Word 2010. Works but date is not populated)
                Perspective (Word 2010. Works)
                Pinstripes (Word 2010. Works)
                Puzzle (Word 2010. Top date doesn't fit; box needs to be manually
                resized or font changed to 14 point)
                Retrospect (Word 2013/2016. Works)
                Semaphore (Word 2013/2016. Works)
                Sideline (Word 2010/2013/2016. Doesn't work in 2013 or 2016, works in
                2010)
                Slice (Dark) (Word 2013/2016. Doesn't work)
                Slice (Light) (Word 2013/2016. Doesn't work)
                Stacks (Word 2010. Works)
                Tiles (Word 2010. Date doesn't fit unless changed to 26 point)
                Transcend (Word 2010. Works)
                ViewMaster (Word 2013/2016. Works)
                Whisp (Word 2013/2016. Works)

        The default value is Sideline.
        This parameter has an alias of CP.
        This parameter is only valid with the MSWORD and PDF output parameters.

        Required?                    false
        Position?                    named
        Default value                Sideline
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -DeliveryGroups [<SwitchParameter>]
        Gives detailed information on all desktops in all Desktop (Delivery) Groups.

        Using the DeliveryGroups parameter can cause the report to take a very long
        time to complete and can generate an extremely long report.

        Using both the MachineCatalogs and DeliveryGroups parameters can cause the
        report to take an extremely long time to complete and generate an exceptionally
        long report.

        This parameter is disabled by default.
        This parameter has an alias of DG.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -DeliveryGroupsUtilization [<SwitchParameter>]
        Gives a chart with the delivery group utilization for the last 7 days
        depending on the information in the database.

        This option is only available when the report is generated in Word and requires
        Microsoft Excel to be locally installed.

        Using the DeliveryGroupsUtilization parameter causes the report to take a longer
        time to complete and generates a longer report.

        This parameter is disabled by default.
        This parameter has an alias of DGU.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Dev [<SwitchParameter>]
        Clears errors at the beginning of the script.
        Outputs all errors to a text file at the end of the script.

        This is used when the script developer requests more troubleshooting data.
        The text file is placed in the same folder from where the script is run.

        This parameter is disabled by default.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -EndDate <DateTime>
        The end date for the Configuration Logging report.

        The format for date only is MM/DD/YYYY.

        Format to include a specific time range is "MM/DD/YYYY HH:MM:SS" in 24-hour format.
        The double quotes are needed.

        The default is today's date.
        This parameter has an alias of ED.

        Required?                    false
        Position?                    named
        Default value                (Get-Date -displayhint date)
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Folder <String>
        Specifies the optional output folder to save the output report.

        Required?                    false
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Hardware [<SwitchParameter>]
        Use WMI to gather hardware information on Computer System, Disks, Processor, and
        Network Interface Cards

        This parameter may require the script be run from an elevated PowerShell session
        using an account with permission to retrieve hardware information (i.e. Domain Admin
        or Local Administrator).

        Selecting this parameter will add to both the time it takes to run the script and
        size of the report.

        This parameter is disabled by default.
        This parameter has an alias of HW.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Hosting [<SwitchParameter>]
        Give detailed information for Hosts, Host Connections, and Resources.
        This parameter is disabled by default.
        This parameter has an alias of Host.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Log [<SwitchParameter>]
        Generates a log file for troubleshooting.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Logging [<SwitchParameter>]
        Give the Configuration Logging report with, by default, details for the previous
        seven days.
        This parameter is disabled by default.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -MachineCatalogs [<SwitchParameter>]
        Gives detailed information for all machines in all Machine Catalogs.

        Using the MachineCatalogs parameter can cause the report to take a very long
        time to complete and can generate an extremely long report.

        Using both the MachineCatalogs and DeliveryGroups parameters can cause the
        report to take an extremely long time to complete and generate an exceptionally
        long report.

        This parameter is disabled by default.
        This parameter has an alias of MC.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -MaxDetails [<SwitchParameter>]
        Adds maximum detail to the report.

        This is the same as using the following parameters:
                Administrators
                AppDisks
                Applications
                BrokerRegistryKeys
                VDARegistryKeys
                DeliveryGroups
                HardWare
                Hosting
                Logging
                MachineCatalogs
                Policies
                StoreFront

        Does not change the value of NoADPolicies.

        WARNING: Using this parameter can create an extremely large report and
        can take a very long time to run.

        This parameter has an alias of MAX.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -NoADPolicies [<SwitchParameter>]
        Excludes all Citrix AD-based policy information from the output document.
        Includes only Site policies created in Studio.

        This switch is useful in large AD environments, where there may be thousands
        of policies, to keep SYSVOL from being searched.

        This parameter is disabled by default.
        This parameter has an alias of NoAD.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -NoPolicies [<SwitchParameter>]
        Excludes all Site and Citrix AD-based policy information from the output document.

        Using the NoPolicies parameter will cause the Policies parameter to be set to False.

        This parameter is disabled by default.
        This parameter has an alias of NP.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Policies [<SwitchParameter>]
        Give detailed information for both Site and Citrix AD based Policies.

        Using the Policies parameter can cause the report to take a very long time
        to complete and can generate an extremely long report.

        Note: The Citrix Group Policy PowerShell module will not load from an elevated 
        PowerShell session.
        If the module is manually imported, the module is not detected from an elevated 
        PowerShell session.

        There are three related parameters: Policies, NoPolicies, and NoADPolicies.

        Policies and NoPolicies are mutually exclusive and priority is given to NoPolicies.

        This parameter is disabled by default.
        This parameter has an alias of Pol.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -ScriptInfo [<SwitchParameter>]
        Outputs information about the script to a text file.
        The text file is placed in the same folder from where the script is run.

        This parameter is disabled by default.
        This parameter has an alias of SI.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -Section <String>
        Processes a specific section of the report.
        Valid options are:
                Admins (Administrators)
                AppDisks
                AppDNA
                Apps (Applications and Application Group Details)
                AppV
                Catalogs (Machine Catalogs)
                Config (Configuration)
                Controllers
                Groups (Delivery Groups)
                Hosting
                Licensing
                Logging
                Policies
                StoreFront
                Zones
                All
        This parameter defaults to All sections.

        Notes:
        Using Logging will force the Logging switch to True.
        Using Policies will force the Policies switch to True.
        If Policies is selected and the NoPolicies switch is used, the script will terminate.

        Required?                    false
        Position?                    named
        Default value                All
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -StartDate <DateTime>
        The start date for the Configuration Logging report.

        The format for date only is MM/DD/YYYY.

        Format to include a specific time range is "MM/DD/YYYY HH:MM:SS" in 24-hour format.
        The double quotes are needed.

        The default is today's date minus seven days.
        This parameter has an alias of SD.

        Required?                    false
        Position?                    named
        Default value                ((Get-Date -displayhint date).AddDays(-7))
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -StoreFront [<SwitchParameter>]
        Give detailed information for StoreFront.
        This parameter is disabled by default.
        This parameter has an alias of SF.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -UserName <String>
        Username to use for the Cover Page and Footer.
        The default value is contained in $env:username
        This parameter has an alias of UN.
        This parameter is only valid with the MSWORD and PDF output parameters.

        Required?                    false
        Position?                    named
        Default value                $env:username
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -VDARegistryKeys [<SwitchParameter>]
        Adds information on registry keys to the Machine Details section.

        If this parameter is used, MachineCatalogs is set to True.

        This parameter is disabled by default.
        This parameter has an alias of VRK.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -SmtpServer <String>
        Specifies the optional email server to send the output report.

        Required?                    true
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -SmtpPort <Int32>
        Specifies the SMTP port.
        The default is 25.

        Required?                    false
        Position?                    named
        Default value                25
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -UseSSL [<SwitchParameter>]
        Specifies whether to use SSL for the SmtpServer.
        The default is False.

        Required?                    false
        Position?                    named
        Default value                False
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -From <String>
        Specifies the username for the From email address.
        If SmtpServer is used, this is a required parameter.

        Required?                    true
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    -To <String>
        Specifies the username for the To email address.
        If SmtpServer is used, this is a required parameter.

        Required?                    true
        Position?                    named
        Default value
        Accept pipeline input?       false
        Accept wildcard characters?  false

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (https:/go.microsoft.com/fwlink/?LinkID=113216).

INPUTS
    None.  You cannot pipe objects to this script.


OUTPUTS
    No objects are output from this script.
    This script creates a Word, PDF, plain text, or HTML document.

NOTES
        NAME: XD7_Inventory_V2.ps1
        VERSION: 2.21
        AUTHOR: Carl Webster
        LASTEDIT: January 26, 2019

    -------------------------- EXAMPLE 1 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1

    Will use all default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    The computer running the script for the AdminAddress.



    -------------------------- EXAMPLE 2 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -AdminAddress DDC01

    Will use all default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    DDC01 for the AdminAddress.
    -------------------------- EXAMPLE 3 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -PDF

    Will use all default values and save the document as a PDF file.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    The computer running the script for the AdminAddress.



    -------------------------- EXAMPLE 4 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -TEXT

    Will use all default values and save the document as a formatted text file.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.



    -------------------------- EXAMPLE 5 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -HTML

    Will use all default values and save the document as an HTML file.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.



    -------------------------- EXAMPLE 6 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -MachineCatalogs

    Creates a report with full details for all machines in all Machine Catalogs.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    -------------------------- EXAMPLE 7 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -DeliveryGroups

    Creates a report with full details for all desktops in all Desktop (Delivery) Groups.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.


    -------------------------- EXAMPLE 8 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -DeliveryGroupsUtilization

    Creates a report with utilization details for all Desktop (Delivery) Groups.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.


    -------------------------- EXAMPLE 9 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -DeliveryGroups -MachineCatalogs

    Creates a report with full details for all machines in all Machine Catalogs and
    all desktops in all Delivery Groups.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.


    -------------------------- EXAMPLE 10 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Applications

    Creates a report with full details for all applications.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    -------------------------- EXAMPLE 11 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Policies

    Creates a report with full details for Policies.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.


    -------------------------- EXAMPLE 12 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -NoPolicies

    Creates a report with no Policy information.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.


    -------------------------- EXAMPLE 13 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -NoADPolicies

    Creates a report with no Citrix AD based Policy information.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    -------------------------- EXAMPLE 14 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Policies -NoADPolicies

    Creates a report with full details on Site policies created in Studio but
    no Citrix AD based Policy information.

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    -------------------------- EXAMPLE 15 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Administrators

    Creates a report with full details on Administrator Scopes and Roles.

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.




    -------------------------- EXAMPLE 16 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Logging -StartDate 01/01/2019
    -EndDate 01/31/2019

    Creates a report with Configuration Logging details for the dates 01/01/2019 through
    01/31/2019.

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.




    -------------------------- EXAMPLE 17 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Logging -StartDate "06/01/2019 10:00:00"
    -EndDate "06/01/2019 14:00:00"

    Creates a report with Configuration Logging details for the time range
    06/01/2019 10:00:00AM through 06/01/2019 02:00:00PM.

    Narrowing the report down to seconds does not work. Seconds must be either 00 or 59.

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.




    -------------------------- EXAMPLE 18 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Hosting

    Creates a report with full details for Hosts, Host Connections, and Resources.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.




    -------------------------- EXAMPLE 19 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -StoreFront

    Creates a report with full details for StoreFront.
    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.




    -------------------------- EXAMPLE 20 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -MachineCatalogs -DeliveryGroups
    -Applications -Policies -Hosting -StoreFront

    Creates a report with full details for all:
        Machines in all Machine Catalogs
        Desktops in all Delivery Groups
        Applications
        Policies
        Hosts, Host Connections, and Resources
        StoreFront

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.





    -------------------------- EXAMPLE 21 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -MC -DG -Apps -Policies -Hosting

    Creates a report with full details for all:
        Machines in all Machine Catalogs
        Desktops in all Delivery Groups
        Applications
        Policies
        Hosts, Host Connections, and Resources

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.


    -------------------------- EXAMPLE 22 --------------------------

    PS C:\>PS C:\PSScript .\XD7_Inventory_V2.ps1 -CompanyName "Carl Webster Consulting"
    -CoverPage "Mod" -UserName "Carl Webster" -AdminAddress DDC01

    Will use:
        Carl Webster Consulting for the Company Name.
        Mod for the Cover Page format.
        Carl Webster for the User Name.
        Controller named DDC01 for the AdminAddress.


    -------------------------- EXAMPLE 23 --------------------------

    PS C:\>PS C:\PSScript .\XD7_Inventory_V2.ps1 -CN "Carl Webster Consulting" -CP "Mod"
    -UN "Carl Webster"

    Will use:
        Carl Webster Consulting for the Company Name (alias CN).
        Mod for the Cover Page format (alias CP).
        Carl Webster for the User Name (alias UN).
        The computer running the script for the AdminAddress.


    -------------------------- EXAMPLE 24 --------------------------

    PS C:\>PS C:\PSScript .\XD7_Inventory_V2.ps1 -CompanyName "Sherlock Holmes Consulting"
    -CoverPage Exposure -UserName "Dr. Watson"
    -CompanyAddress "221B Baker Street, London, England"
    -CompanyFax "+44 1753 276600"
    -CompanyPhone "+44 1753 276200"

    Will use:
        Sherlock Holmes Consulting for the Company Name.
        Exposure for the Cover Page format.
        Dr. Watson for the User Name.
        221B Baker Street, London, England for the Company Address.
        +44 1753 276600 for the Company Fax.
        +44 1753 276200 for the Company Phone.


    -------------------------- EXAMPLE 25 --------------------------

    PS C:\>PS C:\PSScript .\XD7_Inventory_V2.ps1 -CompanyName "Sherlock Holmes Consulting"
    -CoverPage Facet -UserName "Dr. Watson"
    -CompanyEmail SuperSleuth@SherlockHolmes.com

    Will use:
        Sherlock Holmes Consulting for the Company Name.
        Facet for the Cover Page format.
        Dr. Watson for the User Name.
        SuperSleuth@SherlockHolmes.com for the Company Email.




    -------------------------- EXAMPLE 26 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -AddDateTime

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    Adds a date time stamp to the end of the file name.
    The timestamp is in the format of yyyy-MM-dd_HHmm.
    June 1, 2019 at 6PM is 2019-06-01_1800.
    Output filename will be XD7SiteName_2019-06-01_1800.docx




    -------------------------- EXAMPLE 27 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -PDF -AddDateTime

    Will use all Default values and save the document as a PDF file.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    Adds a date time stamp to the end of the file name.
    The timestamp is in the format of yyyy-MM-dd_HHmm.
    June 1, 2019 at 6PM is 2019-06-01_1800.
    Output filename will be XD7SiteName_2019-06-01_1800.pdf




 



   -------------------------- EXAMPLE 28 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Hardware

    Will use all default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.




    -------------------------- EXAMPLE 29 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Folder \\FileServer\ShareName

    Will use all default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    Output file will be saved in the path \\FileServer\ShareName




    -------------------------- EXAMPLE 30 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -SmtpServer mail.domain.tld
    -From XDAdmin@domain.tld -To ITGroup@domain.tld

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    The script will use the email server mail.domain.tld, sending from XDAdmin@domain.tld,
    sending to ITGroup@domain.tld.

    The script will use the default SMTP port 25 and will not use SSL.

    If the current user's credentials are not valid to send email,
    the user will be prompted to enter valid credentials.




  
    -------------------------- EXAMPLE 31 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -SmtpServer smtp.office365.com -SmtpPort 587
    -UseSSL -From Webster@CarlWebster.com -To ITGroup@CarlWebster.com

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    The script will use the email server smtp.office365.com on port 587 using SSL,
    sending from webster@carlwebster.com, sending to ITGroup@carlwebster.com.

    If the current user's credentials are not valid to send email,
    the user will be prompted to enter valid credentials.




    -------------------------- EXAMPLE 32 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Section Policies

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    Processes only the Policies section of the report.




    -------------------------- EXAMPLE 33 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Section Groups -DG

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    Processes only the Delivery Groups section of the report with Delivery Group details.




   


    -------------------------- EXAMPLE 34 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Section Groups

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    Processes only the Delivery Groups section of the report with no Delivery Group details.




    -------------------------- EXAMPLE 35 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -BrokerRegistryKeys

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    Adds the information on over 300 Broker registry keys to the Controllers section.




    -------------------------- EXAMPLE 36 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -VDARegistryKeys

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.
    Adds the information on VDA registry keys to the Machine Details section.
    Forces the MachineCatalogs parameter to $True




    -------------------------- EXAMPLE 37 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -MaxDetails

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    Set the following parameter values:
        Administrators      = True
        AppDisks            = True
        Applications        = True
        BrokerRegistryKeys  = True
        VDARegistryKeys         = True
        DeliveryGroups      = True
        HardWare            = True
        Hosting             = True
        Logging             = True
        MachineCatalogs     = True
        Policies            = True
        StoreFront          = True

        NoPolicies          = False
        Section             = "All"




    -------------------------- EXAMPLE 38 --------------------------

    PS C:\PSScript >.\XD7_Inventory_V2.ps1 -Dev -ScriptInfo -Log

    Will use all Default values.
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\CompanyName="Carl
    Webster" or
    HKEY_CURRENT_USER\Software\Microsoft\Office\Common\UserInfo\Company="Carl Webster"
    $env:username = Administrator

    Carl Webster for the Company Name.
    Sideline for the Cover Page format.
    Administrator for the User Name.

    Creates a text file named XAXDV2InventoryScriptErrors_yyyy-MM-dd_HHmm.txt that
    contains up to the last 250 errors reported by the script.

    Creates a text file named XAXDV2InventoryScriptInfo_yyyy-MM-dd_HHmm.txt that
    contains all the script parameters and other basic information.

    Creates a text file for transcript logging named
    XDV2DocScriptTranscript_yyyy-MM-dd_HHmm.txt.
	
	RELATED LINKS
	
