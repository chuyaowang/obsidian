# RustDesk

A remote desktop app.

## Using Wayland desktop and X11 login screen

The modern Wayland desktop is necessary for [Part 5: rog-control-center](Programming%20Environment/ROG%20Performance%20Management%20on%20Ubuntu%2022.04.md#Part%205%20rog-control-center) to work properly. However, the Wayland login screen cannot be accessed remotely. The login screen needs to run on X11. To enforce this, use the following commands:

```bash
systemctl status display-manager.service
```

This identifies the display manager. It needs to be GDM for this configuration to work.

Now edit the configuration:

```bash
sudo vim /etc/gdm3/custom.conf # it may also be called /etc/gdm/custom.conf
```

Uncomment the line:

```text
WaylandEnable=false
```

Then reboot the computer.