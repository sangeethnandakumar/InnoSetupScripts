# InnoSetupScripts
Example scripts to accomplish things

## Install .NET 7 Desktop Runtime along with WinForms app

```pascal
[Run]
Filename: "{app}\desktop_runtime.exe"; Parameters: "/q /norestart"; Description: "Installing .NET desktop runtime"; StatusMsg: "Installing .NET desktop runtime..."; Flags: nowait skipifsilent
Filename: "{sys}\cmd.exe"; Parameters: "/C ping 127.0.0.1 -n 18 > nul"; StatusMsg: "Installing .NET 7 desktop runtime... This can take upto a minuit"; Flags: waituntilterminated skipifsilent runhidden; WorkingDir: "{app}";
Filename: "{app}\{#MyAppExeName}"; Description: "{cm:LaunchProgram,{#StringChange(MyAppName, '&', '&&')}}"; Flags: nowait postinstall skipifsilent
```

Here the second statement, Will wait for 18 seconds to make sure dotnet_runtime is installed. This wait purposefull because else Inno finishes before runtime is correctly installed. The wizard will freeze for 18seconds and shows 'Installing .NET 7 desktop runtime... This can take upto a minuit'

## Associate a filetype in Windows

```pascal
[Registry]
Root: HKCR; Subkey: ".tdoc"; ValueType: string; ValueData: "Twileloop.Document"; Flags: uninsdeletevalue
Root: HKCR; Subkey: "Twileloop.Document"; ValueType: string; ValueData: "Twileloop Document File"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\DefaultIcon"; ValueType: string; ValueData: "{app}\tdoc_icon.ico"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\open\command"; ValueType: string; ValueData: """{app}\{#MyAppExeName}"" ""%1"""; Flags: uninsdeletekey
```

This will register `*.tdoc` and shows a description `Twileloop Document File` in Windows Explorer. It makes your application launch when double clicked. Also during Unistallation, the reg entries are removed.

MAKE SURE ICON FILE IS PRESENT

## Advanced Shell Integration

```pascal
[Registry]
[Registry]
Root: HKCR; Subkey: ".tdoc"; ValueType: string; ValueData: "Twileloop.Document"; Flags: uninsdeletevalue
Root: HKCR; Subkey: "Twileloop.Document"; ValueType: string; ValueData: "Twileloop Document File"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\DefaultIcon"; ValueType: string; ValueData: "{app}\tdoc_icon.ico"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionA\command"; ValueType: string; ValueData: """{app}\{#MyAppExeName}"" -optA ""%1"""; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionA"; ValueType: string; ValueData: "Option A"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionB\command"; ValueType: string; ValueData: """{app}\{#MyAppExeName}"" -optB ""%1"""; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionB"; ValueType: string; ValueData: "Option B"; Flags: uninsdeletekey
```

This will bring 2 options `Option A` and `Option B` when right clicking on a `.tdoc` file. It'll issue `-optA` or `-optB` as arguments to the application

## Advanced Nested Shell Integration

```pascal
[Registry]
[Registry]
Root: HKCR; Subkey: ".tdoc"; ValueType: string; ValueData: "Twileloop.Document"; Flags: uninsdeletevalue
Root: HKCR; Subkey: "Twileloop.Document"; ValueType: string; ValueData: "Twileloop Document File"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\DefaultIcon"; ValueType: string; ValueData: "{app}\tdoc_icon.ico"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionA\command"; ValueType: string; ValueData: """{app}\{#MyAppExeName}"" -optA ""%1"""; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionA"; ValueType: string; ValueData: "Option A"; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionB\command"; ValueType: string; ValueData: """{app}\{#MyAppExeName}"" -optB ""%1"""; Flags: uninsdeletekey
Root: HKCR; Subkey: "Twileloop.Document\shell\OptionB"; ValueType: string; ValueData: "Option B"; Flags: uninsdeletekey
```

This will bring 2 options `Option A` and `Option B` when right clicking on a `.tdoc` file. It'll issue `-optA` or `-optB` as arguments to the application
