# PersistentDataHandler

TwinCAT 3 library that keeps the `.bootdata` file up to date while the PLC runs.
At startup it calls `FB_WritePersistentData` once. After that it patches only
the persistent variables whose values have changed.

## Install
1. Open the PersistentDataHandler project in TwinCAT XAE.
2. Right-click the **PersistentDataHandler** PLC project → **Save as library and install...**
3. In your project: **References** → **Add library** → **PersistentDataHandler**.

Requires: Tc2_System, Tc2_Utilities, Tc2_Standard.

## Usage
```
VAR
    fbPersist : FB_PersistentMonitor;
END_VAR

fbPersist(bEnable := TRUE, tMinWriteInterval := T#2S);
```

| Input | Description |
|---|---|
| `bEnable` | Initialise, then monitor |
| `bReinit` | Rising edge: rewrite the file and rebuild the variable list (e.g. after an online change) |
| `sBootDataPath` | Leave empty for `C:\TwinCAT\3.1\Boot\Port_<port>.bootdata` |
| `tMinWriteInterval` | Minimum time between file writes |

Outputs: `bReady`, `bBusy`, `bError`, `nErrorId` (see `E_PersistentHandlerError`), `sErrorInfo`.
