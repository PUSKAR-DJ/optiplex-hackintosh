# Installing macOS Big Sur on a Windows PC (Hackintosh Guide)

A step-by-step guide to installing macOS on non-Apple hardware (Hackintosh), tested on a Dell OptiPlex 7020.

📺 **Watch the full video walkthrough:** [YouTube](https://youtu.be/QLxIWA0tOvE?si=tyN4GhOvssyfQZi4) — created by **Spec Tech** ([@Spectechofficiall](https://twitter.com/Spectechofficiall))

---

## Hardware Used

| Component | Spec |
|---|---|
| Device | Dell OptiPlex 7020 |
| CPU | Intel i5-4590 @ 3.30GHz |
| RAM | 8 GB DDR3 |

---

## 1. Check Hardware Compatibility

Before doing anything, scan your hardware to see which macOS versions are supported, using **[OpCore-Simplify](https://github.com/lzhoang2801/OpCore-Simplify)** — a tool built by the Hackintosh community that scans your system and lists compatible macOS versions.

> On this hardware, compatibility went up to **Monterey**, but this guide uses **Big Sur** for stability.

---

## 2. Create the EFI

macOS isn't built to run on standard PCs. To bridge that gap, we need an **EFI** — essentially an interpreter that lets macOS understand non-Apple hardware.

- In OpCore-Simplify, select **Option 6** to generate the EFI folder for your specific hardware.

---

## 3. Download macOS (Recovery Image)

We'll use **[OpenCorePkg](https://github.com/acidanthera/OpenCorePkg)** to fetch the macOS recovery image.

1. Download the full repo ZIP from OpenCorePkg.
2. Inside the tools, locate **macrecovery** and open a Command Prompt in that folder.
3. To download the correct Big Sur build, you need its **recovery product code**. Find it in the official list: [recovery_urls.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/macrecovery/recovery_urls.txt)
4. Paste the Big Sur code into CMD — **remove the `./` prefix** before running it.
5. Wait for the download to finish. You'll get a `com.apple.recovery.boot` folder.

At this point you should have:
- An **EFI** folder (from step 2)
- A **com.apple.recovery.boot** folder (from step 3)

---

## 4. Prepare the USB Installer

1. Get a USB drive with **at least 8GB** of storage.
2. Use **[Rufus](https://rufus.ie/)** to format it with:
   - Partition scheme: **GPT**
   - File system: **FAT32**
3. Copy the **EFI** folder and the **com.apple.recovery.boot** folder onto the USB drive.

---

## 5. BIOS Settings

Before booting into the installer, go into your BIOS and **disable Secure Boot**.

---

## 6. Install macOS

1. Boot from the USB drive.
2. When prompted, open **Disk Utility** and format your target hard drive as:
   - Format: **APFS**
   - Scheme: **GUID Partition Map**
   - Give the drive a name.
3. Choose **Reinstall macOS Big Sur** and proceed with the installation.
4. Complete the standard macOS initial setup.

---

## 7. Final Step — Install EFI on the Internal Drive

Your macOS install on the internal drive doesn't have an EFI yet, so the final step is copying it over.

1. Download **[MountEFI](https://github.com/corpnewt/MountEFI)** (by CorpNewt).
2. Run `mountEFI.cmd`.
3. Select the hard drive macOS is installed on.
4. Copy the **EFI** folder from your USB drive into the **EFI partition** of your macOS drive.

---

## 8. Done

Shut down, remove the USB drive, and boot into your fully installed Hackintosh.

---

## Bonus: Minecraft Java Edition

To run Minecraft Java Edition on this setup, use **[Legacy Launcher](https://llaun.ch/en)**.

---

## Disclaimer

This guide documents a personal hardware experiment. Hackintosh installs are unsupported by Apple, may violate macOS's EULA depending on your jurisdiction and use case, and carry risk of data loss — back up your drive first. Hardware compatibility (Wi-Fi, audio, sleep, etc.) varies and may require additional kexts/tuning not covered here.

## Credits

- **Spec Tech** ([@Spectechofficiall](https://twitter.com/Spectechofficiall)) — creator of the [original video walkthrough](https://youtu.be/QLxIWA0tOvE?si=tyN4GhOvssyfQZi4) this guide is based on
- [OpCore-Simplify](https://github.com/lzhoang2801/OpCore-Simplify) — lzhoang2801
- [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) — Acidanthera
- [MountEFI](https://github.com/corpnewt/MountEFI) — CorpNewt
- [Rufus](https://rufus.ie/)
- [Legacy Launcher](https://llaun.ch/en)
