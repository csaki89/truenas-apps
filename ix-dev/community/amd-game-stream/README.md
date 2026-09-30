# AMD Game Stream

Headless game streaming on an AMD GPU: Xorg + amdgpu + DRI3, Sunshine (VA-API),
Steam, RetroArch, Lutris, Heroic and noVNC.

Image source: https://github.com/csaki89/amd-game-stream

The container uses the host network (needed for Sunshine/Moonlight discovery).
`/dev/dri` is passed through the Devices section, never as a bind mount.
