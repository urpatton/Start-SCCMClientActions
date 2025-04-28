## SYNOPSIS
```
		Run SCCM client actions policy check from an executable.
```

## DESCRIPTION
```
		A simple script to run a few SCCM client actions without needing to open the Control Panel applet.
		I recommend converting the .ps1 script to an exe file. (I use Start-CMClientActions.exe)
```

## NOTES
```
		To get a list of actions to run use the below command
		(New-Object -ComObject CPApplet.CPAppletmgr).GetClientActions() | select Name,DisplayNameResID
		
		Name																          DisplayNameResID
		-----------------------------------						----------------
		Hardware Inventory Collection Cycle			    	10001
		Discovery Data Collection Cycle					    	10004
		Software Inventory Collection Cycle			   		10005
		Standard File Collection Cycle					  		10006
		Request & Evaluate User Policy					    	10007
		Request & Evaluate Machine Policy			    		10008
		Software Metering Usage Report Cycle	    		10009
		MSI Product Source Update Cycle				      	10010
		Software Updates Assignments Evaluation Cycle	10011
		Updates Source Scan Cycle							      	10013
		Application Global Evaluation Task						10014
		
		I highly recommend converting the .ps1 file to an exe.
		I have had success converting it using the PSGallery module "ps2exe" but there are other methods available.
```

## EXTERNALREQUIREMENTS
```
		ps2exe module - https://www.powershellgallery.com/packages/ps2exe
		ps2exe github - https://github.com/MScholtes/PS2EXE
```

## EXAMPLE
```
		Convert the .ps1 to exe using the ps2exe module with the below command
		$FileInput = "\\Your\Path\To\SourceFolder\Start-CMClientAction_Public.ps1"
		$IconFile = "\\Your\Path\To\SourceFolder\SMSCFGRC_8.ico"
		$OutputPath = "\\Your\Path\To\SourceFolder\PSToExe Output"
		$OutputFileName = "Start-CMClientActions.exe"
		
		Invoke-ps2exe -Verbose -STA -configFile -DPIAware -longPaths `
		-inputFile $FileInput `
		-outputFile "$OutputPath\$OutputFileName" `
		-iconFile $IconFile `
		-version "1.0.0.0" `
		-title "Initiate SCCM Control Panel applet client actions." `
		-description "Initiate SCCM Control Panel applet client actions." `
		-copyright "Uriah Patton Copyright (c) 2020 All rights reserved" `
		-product "Start-CMClientActions" `
```

## FUNCTIONALITY
```
		Will open a PowerShell command window and will run the client actions as it finds them. If the action is not available, then the action is skipped.
		By default it will run the below actions
		
		Name																DisplayNameResID
		-----------------------------------							----------------
		Discovery Data Collection Cycle							10004
		Request & Evaluate Machine Policy						10008
		Software Updates Assignments Evaluation Cycle	10011
		Updates Source Scan Cycle								10013
		Application Global Evaluation Task						10014
```
