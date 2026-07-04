# Linux Nyxcore Infinity Kernel

A custom Linux kernel focused on **low latency, high responsiveness, and fine-grained CPU scheduling**, built from upstream kernel.org sources and powered by the **underrated Infinity Scheduler**.

---

## Overview

**Linux Nyxcore Infinity** is a custom kernel tailored for desktop and enthusiast use. It prioritizes:

* Smooth interactivity
* Efficient CPU utilization
* Advanced scheduling behavior

At its core, it replaces the default Linux scheduler with the **Infinity Scheduler**, a lesser-known but highly capable alternative that emphasizes responsiveness and tunability.

---

## Features

### 1. Infinity Scheduler (Underrated but Powerful)

* Community-developed scheduler
* Often overlooked compared to BORE or EEVDF
* Focuses on:

  * Low latency
  * Fast task wake-up
  * Adaptive CPU distribution
* Tunable parameters:

  * `carriage` (controls scheduling timeslice behavior)
  * `smt_divisor` (optimizes SMT/Hyperthreading handling)

---

### 2. Low Latency Behavior

* Prioritizes interactive workloads
* Reduces delay for:

  * UI rendering
  * Input handling
  * Gaming loops
  * Light multitasking

---

### 3. Improved CPU Load Balancing

* More even distribution across CPU cores
* Better handling of SMT/Hyperthreading
* Reduces core overloading and improves consistency

---

### 4. Custom Kernel Configuration

* Tuned specifically for desktop usage
* Minimizes unnecessary overhead
* Flexible for further customization

---

### 5. mkinitcpio Integration

* Fully compatible with Arch Linux initramfs system
* Custom preset support:

  * default
  * fallback
* Ensures reliable boot after installation

---

### 6. Arch-Based Build System

* Uses PKGBUILD for reproducible builds
* Easy to:

  * rebuild
  * update kernel versions
  * integrate new patches
* Compatible with `makepkg` workflow

---

### 7. Custom Identity

* Kernel name:

  ```
  linux-nyxcore-infinity
  ```
* Example output:

  ```
  uname -a
  → Linux ... nyxcore-infinity ...
  ```

---

## Performance Characteristics

### Strengths

* Very responsive for desktop usage
* Lower perceived latency than default schedulers
* Smooth multitasking for everyday workloads

### Trade-offs

* Not always optimal for heavy workloads:

  * large compilations
  * rendering tasks
  * server environments
* Stability depends on scheduler patch compatibility

---

## Build System

Built using:

* `makepkg` (Arch Linux)
* Custom PKGBUILD
* Upstream kernel.org sources
* Infinity Scheduler patches (GitHub)

---

## Requirements

* Arch Linux or compatible environment
* `base-devel`
* `bc`, `flex`, `bison`, `openssl`, etc
* mkinitcpio
* Bootloader (GRUB or systemd-boot)

---

## Installation

### Build & Install

```bash
makepkg -sri
```

### Generate initramfs

```bash
sudo mkinitcpio -p linux-nyxcore-infinity
```

### Update bootloader

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

---

## Verification

```bash
uname -a
```

Check scheduler status:

```bash
dmesg | grep -i sched
```

---

## Updating

### Kernel Update

* Update `pkgver` in PKGBUILD
* Rebuild using `makepkg -sri`

### Scheduler Update

* Pull latest scheduler changes
* Reapply patch
* Rebuild kernel

---

## Notes

* Every update requires a **full rebuild**
* Recommended:

  * Enable `ccache` for faster builds
  * Limit `MAKEFLAGS` to avoid system overload

---

## Disclaimer

This kernel is intended for:

* Enthusiasts
* Experimental setups
* Desktop performance tuning

Not recommended for:

* Production servers
* Critical systems

---

## Credits

* Linux Kernel Developers
* Infinity Scheduler contributors
* Arch Linux ecosystem
