# Fix `snd_sof_pci_intel_tgl` sound issues with Debian

Upon boot, the sound is fragmented and coming only from one channel.

This repository has scripts and instructions on how to fix this problem.

Tested with Debian 12 (kernel 6.1.0-38-amd64).

> WARNING: Stopping the script (`$0 stop`) will **PREVENT** the script from being able to be started again. DO NOT use unless you are manually testing the script and can do `modprobe` as root after stopping the script.

## Create `init.d` script

1. Place the script in `/etc/init.d`
1. Execute `chmod` on the script:
   ```console
   chmod 755 /etc/init.d/fix-sound
   ```

## Systemd service

1. Have `/etc/systemd/system/fix-sound.service` created
1. Reload systemd daemon via `systemctl`
    ```console
    systemctl daemon-reload
    ```
1. Enable service via `systemctl`
    ```console
    systemctl enable fix-sound.service
    ```

## Create boot script

1. Place `rc.local` script in `/etc`
1. Execute `chmod` on the script:
    ```console
    chmod 755 /etc/rc.local
    ```

## Reboot

You're good to go. Upon boot, the driver should have been reloaded by the script.

You can check this with (as root):

```console
journalctl | grep --color fix-sound
```

and

```console
systemctl status fix-sound
```
