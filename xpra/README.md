# xpra

This Xpra shared module was mainly added as a way to run an X11 app in a sandboxed Xorg session
while displaying it on the host using a native Wayland client.


## example usage

```
app-id: FLATPAK_ID
runtime: org.freedesktop.Platform
runtime-version: '21.08'
sdk: org.freedesktop.Sdk
# needed for building python-cryptography
sdk-extensions:
  - org.freedesktop.Sdk.Extension.rust-stable
finish-args:
  - --device=dri
  - --socket=pulseaudio
  # TODO: evalute less permissive session bus access
  - --socket=session-bus
  - --socket=wayland
  - --unset-env=XAUTHORITY
modules:
  - ../shared-modules/xpra/xpra.json
```

## how to test and run apps?
* start and enter the sandbox
  $ flatpak run org.xpra.xpra
* start xpra x session
  $ xpra --xvfb=/app/bin/Xvfb start --encoding=rgb --compress=0 :11
* connect xpra session to the gtk3 client running through wayland
  $ GDK_BACKEND=wayland xpra attach :11 &
* run apps in the xpra x session
  * glxgears
    just use the the binary from your host's mesa-demos package, you can do this as abi is
      is pretty stable as it's only linked against xorg libs and mesa
    add --filesystem=host-os to 'flatpak run' in order to get access to the host os
    $ DISPLAY=:11 /run/host/usr/bin/glxgears
  * gtk3-demo
    available in the freedesktop sdk and you should add --devel to 'flatpak run'
    $ DISPLAY=:11 GDK_BACKEND=x11 gtk3-demo
  * joplin
    $ wget https://github.com/laurent22/joplin/releases/download/v1.7.11/Joplin-1.7.11.AppImage
    $ unappimage Joplin-*.AppImage && cd squashfs-root
    $ DISPLAY=:11 ./\@joplinapp-desktop --no-sandbox
