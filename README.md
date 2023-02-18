# InnoSetupScripts
Example scripts to accomplish things

## Install .NET 7 Desktop Runtimealong with WinForms app

```pascal
[Run]
Filename: "{app}\desktop_runtime.exe"; Parameters: "/q /norestart"; Description: "Installing .NET desktop runtime"; StatusMsg: "Installing .NET desktop runtime..."; Flags: nowait skipifsilent
Filename: "{sys}\cmd.exe"; Parameters: "/C ping 127.0.0.1 -n 18 > nul"; StatusMsg: "Installing .NET 7 desktop runtime... This can take upto a minuit"; Flags: waituntilterminated skipifsilent runhidden; WorkingDir: "{app}";
Filename: "{app}\{#MyAppExeName}"; Description: "{cm:LaunchProgram,{#StringChange(MyAppName, '&', '&&')}}"; Flags: nowait postinstall skipifsilent
```

Here the second statement, Will wait for 18 seconds to make sure dotnet_runtime is installed. This wait purposefull because else Inno finishes before runtime is correctly installed. The wizard will freeze for 18seconds and shows 'Installing .NET 7 desktop runtime... This can take upto a minuit'
