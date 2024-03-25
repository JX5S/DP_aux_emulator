# DP-aux emulator

Hardware design files for a DP-aux emulation board, designed to allow connection of PSVR2 headsets to PC.

![(Rendered image using Kicad2blender plugin)](render.png)

Prior to a March 2024 update of the PSVR2's firmware, the headset reported incorrect information via DP-aux, among others the EDID and DSC capability. A custom EDID can be set without additional hardware, however DSC options cannot - so the emulator board was born.

On the PCB is an RP2040 microcontroller, which decides which DP-aux requests to modify and which to pass through unchanged. To do so, a pair of SN65MLVD200A differential transceivers are used. The LVDS part of the circuit is based on [Bitec's DisplayPort Daughter Card](https://bitec-dsp.com/wp-content/uploads/2023/03/bitec_fmc_dp_rev12_sch.pdf), however, I believe my voltage divider is closer to correct for this specific chip.

Apart from the core DP-aux emulation circuitry, there is a programming micro-USB connector (I would have used a USB-C, but this way it cannot be confused with the PSVR2 port), orientation detection using USB-C CC pins, and a power section, allowing the board to be powered with either the programming USB port or using VBUS from the USB-Cs. Even though the board was made with specifically the PSVR2 in mind, I tried to make it as compliant as possible with a low part count and it should work well with the maximum voltage of USB-PD3.0, 21V.

Firmware for it was written by the autor of the [iVRy SteamVR driver](https://store.steampowered.com/app/992490), a passthrough-only version of the firmware is provided in this repository for testing.

As of March 2024, after the update, this board is only needed for using Nvidia boards with 3rd party PSVR2 drivers. This board only modifies DP-aux traffic, it doesn't help with connecting a PSVR2 to a card without a USB-C, for an adapter for such GPUs, check out [Swyter's project](https://github.com/Swyter/psdaptwor), but note that it hasn't been tested yet.

Status: This is a third revision of the PCB, it has been verified to work as designed.
