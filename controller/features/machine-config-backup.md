# Machine configuration backup

The Controller can copy **specific configuration files from the machine’s SD card** to the **computer** where the Controller is running, so you keep a local backup of your machine specific configuration.

## Where to run it

Open **Settings** and use the **Machine - Backup** section to start the backup workflow. Alternatively the button "Back up machine config" is present on the Firmware Upgrade screen. When a backup is triggered the Controller lists the files on the SD card root, downloads only the files in the list below, then asks you to **choose a folder on the computer** where those files should be saved.

## Files that are backed up

Backup includes **only** these paths on the machine:

| Remote path | Typical purpose |
| ----------- | ---------------- |
| `config.txt` | Main machine configuration. |
| `config.default` | Default configuration snapshot used by the firmware restore flow. |
| `cartesian_nm.grid` | Saved **bed leveling** data. |
| `flex_compensation.dat` | Saved **flex compensation** measurement data (when used). |
| `custom_tool_slots.txt` | **Custom tool rack** slot positions (when defined; file may be absent). |

If a listed file **does not exist** on the SD card, it is simply skipped—there is no error for missing optional files.

## What is not backed up

**G-code programs are not backed up** by this feature. No `.nc`, `.ngc`, `.tap`, or other job files on the SD card are downloaded. The backup is **configuration and compensation data only**.

Likewise, **firmware**, logs, arbitrary folders, and any other files on the card that are **not** in the table above are **not** included.

## Mobile platforms

Backup from the machine to the Controller host is **disabled on mobile** builds. Use the desktop Controller when you need this workflow.


## Restore
If you need to restore the configuration files back to the machine it is required to remove the SD card, and perform the file operations manually on a computer. If using a brand new SD card, first format it as FAT32, then transfer the backed up files to the root of the card.
