# brtlvrs-psfunc

Repository of powershell functions written by brtlvrs.
The functions can be used in other scripts by dot sourcing them from a sub folder.
See my Powershell template script for a full example

## LICENSE

This functions are released under the MIT license. See the License file for more details

| | |
|---|---|
| Version | 0.0|
| branch | master|

## CHANGE LOG

|build|branch |  Change |
|---|---|---|
|0.0| Master| Rewrote exit-script function|
|0.0| Master| Initial release|

## How to set up

1. create a subfolder functions in the root of the script you want to use these functions in
1. copy the desired functions to the subfolder.
1. add in the start of your script  the code below (preferably in the begin {} secion
)
1. use the functions in your script

```powershell
begin {

    # Gather all functions
    $Functions  = @(Get-ChildItem -Path ($scriptpath+"\"+$P.FunctionsSubFolder) -Filter *.ps1 -ErrorAction SilentlyContinue)

    # Dot source the functions
    ForEach ($File in @($Functions)) {
        Try {
            . $File.FullName
        } Catch {
            Write-Error -Message "Failed to import function $($File.FullName): $_"
        }
}
```

Note: in this example we assume that the scripts uses a parameter.ps1 file which is loaded in the ```$p.``` variable. If you don't want that, replace the ```"\"+$p.FunctionsSubFolder``` with ```"\functions"```.

## Dependencies

- PowerShell 3.0