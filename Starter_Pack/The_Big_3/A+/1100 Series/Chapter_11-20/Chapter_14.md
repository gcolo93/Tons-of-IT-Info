- **Chapter 14: Maintaining and Optimizing Operating Systems**
  - **Introduction**
    - Every computer running a modern operating system (OS) requires occasional optimization and ongoing maintenance.
    - Maintenance involves tasks like cleaning up junk on mass storage devices, while optimization includes making changes to improve system performance.
    - This chapter covers standard maintenance and optimization activities for Windows, macOS, and Linux, along with the tools used.
  - **Maintaining Operating Systems**
    - **Patch Management**
      - Patch management involves keeping software updated to support new hardware and defend against security threats.
      - Windows, macOS, and Linux all require patch management.
    - **Windows Patch Management**
      - Updates in Windows are handled through Windows Update, available in the Settings app.
      - Windows has quality updates for problem fixes and feature updates for new versions.
      - Users can't turn off updates but can pause them temporarily.
    - **Patch Management in macOS and Linux**
      - macOS and Linux use automated mechanisms to handle patching and alert users when updates are available.
    - **Scheduling Maintenance**
      - Modern operating systems automate essential maintenance tasks but still require scheduling for specific needs.
      - Windows uses Task Scheduler for scheduling maintenance tasks.
      - Unix-like systems like macOS and Linux use cron or init systems for automated tasks.
    - **Controlling Autostarting Software**
      - Autostarting software can impact system performance and startup times.
      - Windows, macOS, and Linux provide tools to manage autostarting programs.
  - **Optimizing Operating Systems**
    - **Installing and Removing Software**
      - Software installation and removal affect system performance and functionality.
      - Understanding software requirements, distribution methods, and impact on devices, networks, and operations is crucial.
    - **Installing Software in Windows**
      - Software installation in Windows involves accepting terms, making decisions during installation, and managing User Account Control (UAC).
      - The Microsoft Store offers a curated selection of applications for installation.

- **Installing Software in macOS**
  - Options: Mac App Store or direct download installer
  - Mac App Store: Similar to installing apps on a phone, click to install
  - Direct download: Usually a .dmg file, mountable as a volume in Finder
    - Contains .app file, drag to Applications folder to install

- **Installing Software in Linux**
  - Options: Store (e.g., Pop!_Shop) or downloading package file
  - Store: Similar to Microsoft or Mac App Store, handles updates
  - Package file: Double-click, select Install
  - Common method: Built-in package manager like APT in Ubuntu
    - Access via Terminal with apt-get or apt command

- **Removing Software**
  - Windows: Use app's uninstall program or Programs and Features in Control Panel
    - Uninstall/Change button in app folder or Control Panel
  - macOS: Mac App Store apps remove like phone apps, drag to Trash
    - Other apps: Drag to Trash or run uninstaller if available
  - Linux: Use software manager to uninstall or package manager like APT

- **Adding or Removing Windows Components/Features**
  - Old way: Control Panel > Programs and Features > Turn Windows features on or off
  - New way: Settings app > Apps > Optional features > More Windows features
  - Toggle features by clicking checkbox

- **Performance Options**
  - Access: Right-click Start button > System > Advanced system settings
  - Three tabs: Visual Effects, Advanced, Data Execution Prevention (DEP)
  - Adjust visual effects, processor scheduling, virtual memory, DEP settings

- **Backup and Recovery Options**
  - Types of backups: Full, incremental, differential, synthetic
  - Backup media: Hard drives, magnetic tapes, optical discs, flash media, cloud storage
  - Testing backups: Verify regularly, test restoration of critical data

- **Backup Rotation Schemes**
  - Aim: Balance risk of data loss with cost, convenience, effort
  - 3-2-1 backup rule: Three copies on two types of media, one offsite
  - Example scheme: Grandfather-father-son (GFS) rotation
    - Daily backups to SSD, weekly to one hard drive, monthly to another, store offsite
    - Provides multiple backup points for recovery without overwriting all data frequently

- **Backing Up Personal Data:**
  - Windows Backup and Restore:
    - Choose backup location and content (user files or system image).
    - Options: Let Windows choose (recommended) or Let me choose.
    - System Image creation.
  - Windows File History:
    - Focuses on personal files and folders.
    - Requires a second drive; not enabled by default.
  - Time Machine in macOS:
    - Full system backups called local snapshots.
    - Recovers files, restores deleted files, and recovers previous file versions.
  - Backups in Linux:
    - Ubuntu Linux uses Déjà Dup (Backups app) to back up files to specified locations.
- **System Restore in Windows:**
  - Creates restore points for system configuration snapshots.
  - Manual creation and management of restore points.
- **Beyond A+ (Third-Party Backup Tools):**
  - Backup Tools:
    - Programs for capturing various types of backups with user control.
  - Backup Appliance:
    - Hardware and software combination for making and storing backups.
  - Backup Service:
    - Online backup services integrated with backup software for cloud storage.