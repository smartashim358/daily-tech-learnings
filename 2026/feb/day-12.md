# Linux Filesystem Hierarchy – Quick Professional Reference  
`/etc` • `/var` • `/usr` • and all the other top-level directories explained

**Purpose of this document**  
One-page (well… long page) cheat-sheet / training material / onboarding reference explaining **why each standard top-level directory exists**, what usually lives inside, and the most useful real-world commands.

Last meaningfully aligned with: FHS 3.0 (2015) + common modern practices (2024–2026 merged-/usr systems)

───────────────────────────────────────────────────────────────────────────────

## Quick One-Line Purpose Table

| Directory     | One-sentence purpose                                      | Read-only possible? | Survives reboot? | Usually large? |
|---------------|------------------------------------------------------------|----------------------|------------------|----------------|
| `/`           | Root of everything                                         | sometimes            | yes              | small–medium   |
| `/bin`        | Essential commands (merged → `/usr/bin` on many distros)  | yes                  | yes              | small          |
| `/boot`       | Kernel(s), initramfs, bootloader files                     | yes                  | yes              | medium         |
| `/dev`        | Device nodes (managed by udev or devtmpfs)                 | virtual              | no               | tiny           |
| `/etc`        | **Host-specific configuration**                            | yes                  | yes              | small–medium   |
| `/home`       | User home directories                                      | no                   | yes              | often huge     |
| `/lib`        | Libraries needed for boot & essential commands             | yes                  | yes              | medium         |
| `/media`      | Mount point for removable media (USB, DVD…)                | no                   | no               | temporary      |
| `/mnt`        | Temporary manual mount point (admin use)                   | no                   | no               | temporary      |
| `/opt`        | 3rd-party / commercial software packages                   | yes                  | yes              | varies         |
| `/proc`       | Process & kernel information (virtual)                     | virtual              | no               | tiny           |
| `/root`       | Root user's home directory                                 | no                   | yes              | small          |
| `/run`        | Runtime data (PIDs, sockets, locks…)                       | no                   | no               | small          |
| `/sbin`       | System administration binaries                             | yes                  | yes              | small          |
| `/srv`        | Data served by this system (www, ftp, git…)                | no                   | yes              | varies         |
| `/sys`        | Kernel device & driver information (sysfs)                 | virtual              | no               | tiny           |
| `/tmp`        | Temporary files (usually cleaned on boot)                  | no                   | no               | varies         |
| `/usr`        | **Most of the operating system** – shareable & read-only   | yes                  | yes              | **large**      |
| `/var`        | **Variable data** – logs, caches, databases, mail, spool   | no                   | yes              | often large    |

───────────────────────────────────────────────────────────────────────────────

## The Most Important Three – Deep Dive

### /etc – Host-specific system configuration

**Core idea**  
Everything that makes *this exact machine* different from others.

**Common important files & folders**

    /etc/passwd           /etc/group            /etc/shadow
    /etc/fstab            /etc/hostname         /etc/hosts
    /etc/resolv.conf      /etc/localtime
    /etc/ssh/sshd_config  /etc/sudoers
    /etc/systemd/         /etc/NetworkManager/
    /etc/nginx/           /etc/apache2/         /etc/postgresql/
    /etc/default/         /etc/modprobe.d/      /etc/security/
    /etc/skel/            /etc/profile.d/

**Useful commands**

```bash
# Show OS & version info
cat /etc/os-release

# See mount points in nice table
grep -v '^#' /etc/fstab | column -t

# Quick list of interesting config folders
ls -d /etc/* | grep -E 'ssh|sudo|systemd|NetworkManager|nginx|apache|mysql|postgres'