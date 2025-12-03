# ProbeDesk

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey.svg)
![Language](https://img.shields.io/badge/language-Go-00ADD8.svg)
[![Release](https://img.shields.io/github/v/release/RainyRoot/ProbeDesk-CLI?label=Latest%20Release)](https://github.com/RainyRoot/ProbeDesk-CLI/releases/latest)


**ProbeDesk — Lightweight Windows System Administration & Information-Gathering Tool**

© 2025 RainyRoot — MIT License

---

## Overview

ProbeDesk is a small, modular command-line tool written in **Go**, designed to quickly enumerate Windows system information, perform common network and maintenance tasks, and export collected data into a comprehensive report. It’s built for **system administrators, pentesters, and power users** who want a unified, scriptable interface for useful PowerShell and Windows commands.

> ⚠️ **Safety Note:** Actions that modify the system (e.g., DNS flush, DISM restore, winget upgrades) require the explicit `--yes` confirmation flag to prevent accidental or destructive changes.

---

## Features / Modules

ProbeDesk is modular — each module provides a specific category of information or executes a defined task.

### Enumeration Modules

* `--system` — General system info (OS, CPU, RAM, uptime)
* `--services` — Service status overview
* `--ipconfig` — Network configuration (ipconfig)
* `--netuse` — Network shares / mapped drives
* `--products` — Installed software / applications
* `--users` — Local user accounts
* `--usb` — Connected USB devices
* `--vpn` — VPN configuration and status
* `--trace <host>` — Trace route to a given host or IP
* `--check-health` — Quick system health check

### Maintenance / Admin Modules (require `--yes`)

* `--flush` — Flush DNS cache
* `--scan-health` — Run DISM health scan
* `--restore-health` — Restore system health (DISM)
* `--winget-update` — Update all installed packages using `winget`

### Other Flags

* `--remote` — Run commands remotely on target hosts (requires PS Remoting)
* `--report` — Generate a combined report (HTML or Markdown)
* `--help` — Display help information
* `--yes` — Confirmation flag for system modifications
* `--autocomplete-install` — Enable PowerShell autocomplete for ProbeDesk flags

---

## Installation

1. Download the latest `probedesk` binary for your platform and run `install.ps1`.
2. (Optional) Move the binary to a directory included in your system `PATH`.

**Example (Windows / PowerShell):**

```powershell
Move-Item .\probedesk.exe -Destination 'C:\Windows\System32\'
```
3. Open the Download-Folder and use the install.ps1 via Powershell >> the install.ps1 must be in the same Folder as ProbeDesk.exe
```powershell
.\install.ps1
```

4. If you plan to use the `--remote` feature, ensure that PowerShell Remoting (WinRM) is enabled on your target machines.

---

## Related Projects

| Project        | Description |
|----------------|-------------|
| ProbeDesk-GUI  | Full Windows GUI version with modular system checks, reporting engine (HTML/MD), and remote execution. |
| ProbeDesk-CLI  | Command-line version (this repo) with autocomplete, safety checks, and script-friendly output. |

---

## Usage

Run ProbeDesk from your terminal or PowerShell:

```powershell
probedesk --[options]
```

### Examples

Run Full-Scan:

```powershell
probedesk
```

Get system information:

```powershell
probedesk --system
```
 
 [Multiple Flags]
Check for VPN and ipconfig:

```powershell
probedesk --ipconfig --vpn
```

Save `ipconfig` output to a file:

```powershell
probedesk --ipconfig --report html/md
```

Trace a host:

```powershell
probedesk --trace 8.8.8.8
```

Flush DNS (confirmation required):

```powershell
probedesk --flush --yes
```

Update installed packages via winget:

```powershell
probedesk --winget-update --yes
```

---

## Example CLI Preview

```powershell
PS C:\> probedesk --system

=== System ===
OS Name:                   Microsoft Windows 10 Home
OS Version:                10.0.19045 N/A Build 19045
BIOS Version:              American Megatrends Inc. 1802, 01/12/2020
✅ Output copied to clipboard!

PS C:\> probedesk --system probedesk --vpn --users --report html

=== Vpn ===
No output (possibly no data found).

=== Users ===

Name            : Rainy
Enabled         : True
PasswordExpires :
PasswordLastSet : 1/12/2025 1:23:45 AM
LastLogon       : 2/12/2025 6:33:40 AM

Name            : WDAGUtilityAccount
Enabled         : False
PasswordExpires : 12/34/5678 1:23:45 AM
PasswordLastSet : 90/12/3456 6:33:40 AM
LastLogon       :
✅ Output copied to clipboard!
✅ Report exported successfully as html
```

---

## Report Export

The `--report` flag aggregates data from available modules and exports a unified system report.

* **Supported formats:** HTML and Markdown (`.html`, `.md`)
* Output format is auto-detected or can be specified (if implemented).

**Example:**

```powershell
probedesk --system --ipconfig --report html
```

---

## PowerShell Autocomplete

Enable autocomplete for ProbeDesk modules:

```powershell
probedesk --autocomplete-install
```

This adds an autocomplete function to your PowerShell profile so module and flag names are suggested while typing.

---

## Best Practices & Notes

* System-changing actions are protected by `--yes`. Double-check commands before confirming.
* `--remote` requires PowerShell Remoting (WinRM) and valid credentials on the target.
* Run your terminal with Administrator privileges when necessary.
* Combine modules and redirect output for custom logs or reports.
* Treat report files as sensitive data — secure them appropriately.

---

## Troubleshooting

* **`--remote` fails:** Verify that WinRM is enabled and allowed through the firewall.
* **Permission denied:** Run PowerShell as Administrator.
* **`winget` not found:** Ensure `winget` is installed and available in `$env:PATH`.
* **Autocomplete not working:** Reload your PowerShell profile or restart PowerShell.

---

## Contributing

Contributions, issues, and feature requests are welcome. Please open an issue or PR in the repository and follow the project’s coding and commit conventions.

**Recommended workflow:**

1. Open or comment on an issue.
2. Create a feature branch: `feature/<short-description>` or `fix/<short-description>`
3. Submit a PR with a description and relevant tests.

---

## License

This project is licensed under the **MIT License** — see `LICENSE` for details.

---

## Contact

**RainyRoot** — *(Discord: rainy123)*

---

## Changelog

* **v1.0.0** — Initial release: core enumeration modules and report export.


---

