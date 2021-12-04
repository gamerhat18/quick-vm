[![GitHub](https://img.shields.io/badge/Quick-VM-brightgreen?style=for-the-badge&logo=Material-Design-Icons&logoColor=white)](https://github.com/gamerhat18/Quick-VM/)
![Arch](https://img.shields.io/badge/Arch-blue?style=for-the-badge&logo=Arch-Linux&logoColor=white)
![Fedora](https://img.shields.io/badge/Fedora-blue?style=for-the-badge&logo=Fedora&logoColor=white&color=294172)
![Debian](https://img.shields.io/badge/Debain-red?style=for-the-badge&logo=Debian&logoColor=white&color=A81D33)
![Ubuntu](https://img.shields.io/badge/Ubuntu-orange?style=for-the-badge&logo=Ubuntu&logoColor=white&color=E95420)
![Terminal](https://img.shields.io/badge/Terminal-black?style=for-the-badge&logo=Windows-Terminal&logoColor=white&color=4D4D4D)
![Windows](https://img.shields.io/badge/Windows-blue?style=for-the-badge&logo=Windows&logoColor=white&color=0078D6)


<h1><img src="https://raw.githubusercontent.com/thegamerhat/quick-vm/main/docs/img/quick-vm-icon.svg" width="30px"> Quick VM</h1>

**Setup a Windows VM quickly on Linux in under 100 seconds with just one command**, assuming you have Virtualization enabled (see [how-to](https://github.com/thegamerhat/quick-vm/blob/main/docs/diy-vm.md#enabling-virtualization-in-your-ueficoreboot))

> It is possible to invent a single machine which can be used to compute any computable sequence.
>
> ~ _Alan Turing, 1936_

# 🚀 Getting Started

## 🏅 Simple Install ➜ Follow Step 🥇, Step 🥈 and Step 🥉

### 🥇 Getting ISOs Ready

1. **Download** [Windows 10 Pro ISO](https://www.microsoft.com/en-us/software-download/windows10ISO), **and** [VirtIO Drivers (Stable)](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso)

2. **Place the ISOs in either** `~/WindowsVM/` **or** `/var/lib/libvirt/images/`.

3. **Rename the ISOs as shown below:**
    - **Windows 10 ISO** ➜ `win10.iso`
    - **VirtIO Drivers** ➜ `virtio-win.iso`

4. **Enter the command shown below in the terminal.** 

### 🥈 One-liner to Setup KVM

#### Paste this in your terminal

```bash
bash <(wget -qO- https://git.io/JOeOs)
 ```

> Here is the [Script](https://github.com/thegamerhat/quick-vm/blob/main/one-liner.sh)

### 🥉 Getting the VM Ready:

[Step by Step Guide - Click Me!](docs/installing-windows-vm.md)

### 🎉 That's it, You have successfully created a VM!

---

<p>
<details>
<summary>🖥 Host System Requirements:</summary>
<br>
 
  - **Ubuntu 18.04** or newer
  - **Fedora 30** or newer
  - **Arch** (Read this [Guide by LinuxHint](https://linuxhint.com/install_configure_kvm_archlinux) for permissions and User Group setting)
  - **4 CPUs** (2 Multi-Threaded Cores at minimum)
  - **8 GiB Memory** (more = better)
  - **40+ GiB of Free Storage** typically (**SSD Recommened**)
</br>
</details>
</p>

> **Linux Kernel 5.4 LTS** or newer is recommended 

<p>
<details>
<summary>Default specs of the VM</summary>
<br>

**CPU**: 4 vCPUs Allocated

**GPU**: VirtIO or [VFIO GPU Passthrough - ArchWiki](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF) or [Single-GPU-Passthrough](https://github.com/joeknock90/Single-GPU-Passthrough) 

**Memory**: Total 6 GiB, 1 GiB Allocated initially

**Storage Drive**: 1 TB VirtIO Disk (Dynamically Allocated)

**DVD Drive**: Windows 10 ISO

**Other Drives**: VirtIO Drivers ISO, Essential Tools ISO (to optimize VM performance)

**Network Card**: VirtIO (Recommended Disabled until debloated)
</br>
</details>
</p>

## ⚔️ Advanced Install

### 🔖 [DIY VM (Everything From Scratch + GPU Passthrough)](docs/diy-vm.md)

### 🔖 [Making a Stealth VM (Always being Updated)](docs/stealth-vm.md)

<p>
<details>
<summary>📍 Check KVM Compatibility</summary>
<br>

1. Checks if `AMD-V` or `VT-d`/`VT-x` is supported on your AMD/Intel CPU.
2. Checks if kvm is enabled using `virt-host-validate`.</br>
</details>
</p>

<p>
<details>
<summary>📍 Install required packages</summary>
<br>

- Updates repositories (Debian and Fedora only) and installs required packages.

```
# Debian
sudo apt update -q && sudo apt install -y qemu qemu-kvm libvirt-bin libvirt-daemon libvirt-clients bridge-utils virt-manager

# Fedora
sudo dnf -y install qemu-kvm libvirt bridge-utils virt-install virt-manager

# Arch
sudo pacman -S --noconfirm qemu libvirt bridge-utils edk2-ovmf vde2 ebtables dnsmasq openbsd-netcat virt-manager
```
</br>
</details>
</p>

<p>
<details>
<summary>📍 Enable Libvirt Service & Virtual Networking</summary>
<br>

**Executes the following commands only if systemd is present and running.**

```
# Libvirt service and socket
sudo systemctl enable --now libvirtd

# Virtlogd
sudo systemctl enable --now virtlogd

# Virtual Networking
sudo virsh net-autostart default
sudo virsh net-start default
```
</br>
</details>
</p>

<p>
<details>
<summary>📍 Locate ISOs</summary>
<br>

1. Checks if `win10.iso` and `virtio-win.iso` exist in ~/WindowsVM or /var/lib/libvirt/images
2. Uses `rsync` to copy the ISOs to /var/lib/libvirt/images (_$HOME subdirectories might cause permission issues_)

</br>
</details>
</p>

<p>
<details>
<summary>📍 Selecting a VM Profile</summary>
<br>

### 1. Serious Business 

Ideal for Gaming, Content Creation and other heavy duty applications.

**Adobe Creative Cloud**

**3d Printing Software**: CHITUBOX

**360 Photo/Video Software**: VeeR Editor

|Part|Specification|
| --- | --- |
|CPU|6 vCPU|
|Memory|8 GiB|
|Storage|1 TiB|

### 2. Decently Powerful [Default]

Ideal for Office 365, and some light Photoshop.

|Part|Specification|
| --- | --- |
|CPU|4 vCPU|
|Memory|6 GiB|
|Storage|1 TiB|

### 3. Lightweight and Barebones

Ideal for basic stuff that requires Windows. 

**Printer Software, CNC Application**

**Tax Software in Banks**

|Part|Specification|
| --- | --- |
|CPU|2 vCPU|
|Memory|4 GiB|
|Storage|1 TiB|

### 4. Stealth VM (Beta)

Ideal for DRM/Anticheat Programs like **Valorant**, **Rainbow Six: Siege**

|Part|Specification|
| --- | --- |
|CPU|4 vCPU|
|Memory|8 GiB|
|Storage|1 TiB|


</br>
</details>
</p>

<p>
<details>
<summary>📍 Reload KVM Kernel Modules</summary>
<br>

If `kvm` is enabled correctly, then executes the following commands depending upon the CPU.

```
# AMD
sudo modprobe -r kvm_amd kvm      # safely unloads the modules
sudo modprobe kvm                 # enables kvm first
sudo modprobe kvm_amd nested=1    # then kvm_amd module with nested enabled

# INTEL
sudo modprobe -r kvm_intel kvm    # safely unloads the modules
sudo modprobe kvm                 # enables kvm first
sudo modprobe kvm_intel nested=   # then kvm_intel module with nested enabled
```
</br>
</details>
</p>

## Some more useful stuff

- **[Looking Glass](https://looking-glass.io)** by Wendell from [Level1Techs](https://www.youtube.com/channel/UC4w1YQAJMWOz4qtxinq55LQ)

- **[VFIO on Pop! OS](https://forum.level1techs.com/t/vfio-in-2019-pop-os-how-to-general-guide-though-draft/142287)**

- **Single GPU Passthrough**:
  - [SomeOrdinaryGamers' Video Guide (NVIDIA)](https://youtube.com/watch?v=BUSrdUoedTo)
  - [joeknock90 Central Repository](https://github.com/joeknock90/Single-GPU-Passthrough)
  - [Stetsed NVIDIA Guide](https://github.com/Stetsed/NVIDIA-Single-GPU-Passthrough)
  - [ledisthebest (Ryzen + Radeon)](https://github.com/ledisthebest/LEDs-single-gpu-passthrough)

- **NVIDIA GPU Passthrough**:
  - [clayfreeman](https://clayfreeman.github.io/gpu-passthrough/) 
  - [SomeOrdinaryGamers' Single GPU Passhrough Video (NVIDIA)](https://youtube.com/watch?v=h7SG7ccjn-g)

- **Intel iGPU Passthrough** - [Lan Tian](https://lantian.pub/en/article/modify-computer/laptop-intel-nvidia-optimus-passthrough.lantian/)

## 🎁 Contribute/Help

**Stuff changes all the time, and I can only do so much.**

**If you want to help, THANK YOU, that will be wonderful!** 💜

**This project is aimed at making a Windows VM for gaming/content creation, paired with [WinApps](https://github.com/Fmstrat/winapps/) to make it easier for people to switch to Linux while still being able to use their Adobe CC apps, MS Office, Play Games etc.**

Here's a [list of things](https://github.com/thegamerhat/quick-vm/blob/main/docs/list-things-todo.md) that will make this project way better!

> Now that [NVIDIA has enabled GPU Passthrough for Windows based Virtual Machines](https://nvidia.custhelp.com/app/answers/detail/a_id/5173) (no more Code 43!), this project will also include easy setup and configuration for passing through NVIDIA GPUs in KVM and interfacing Windows apps from linux via [WinApps](https://github.com/Fmstrat/winapps/).
>
> Till then, read [Arch Wiki - PCI Passthrough](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF) and [this](https://github.com/thegamerhat/quick-vm#some-more-useful-stuff).

## 📣 Credits

- **The Entire [r/VFIO](https://reddit.com/r/vfio) Community!**
- **Wendell** from [Level1Techs](https://www.youtube.com/user/teksyndicate)
- **SomeOrdinaryGamers** - For [Video guide](https://youtube.com/watch?v=BUSrdUoedTo)
- **Zeptic** - For [Stealth VM stuff](https://youtube.com/watch?v=VKh2eKPnmXs)
- **joeknock90** (and everyone mentioned in their [repository](https://github.com/joeknock90/Single-GPU-Passthrough)) - For Single GPU Passthrough Central Point
- [**More Credits...**](docs/more-credits.md)

## Donate

[![PayPal.Me](https://img.shields.io/badge/PayPal-%23FFFFFF.svg?&style=for-the-badge&logo=paypal)](https://paypal.me/gamerhat18) 

## 📬 Facing Issues? Contact me

![visitors](https://visitor-badge.glitch.me/badge?page_id=gamerhat18.quick-vm)

[![Telegram](https://img.shields.io/badge/Telegram-%2326A5E4.svg?&style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/thegamerhat)

[![Mail Me](https://img.shields.io/badge/Gmail-%23EA4335.svg?&style=for-the-badge&logo=gmail&logoColor=white)](mailto:gamerhat18@gmail.com) 

[![Secure Mail Me](https://img.shields.io/badge/ProtonMail-%23663399.svg?&style=for-the-badge&logo=proton-mail&logoColor=white)](mailto:gamerhat18@protonmail.com) 

[![GitHub](https://img.shields.io/badge/GitHub-%23181717.svg?&style=for-the-badge&logo=github&logoColor=white)](https://github.com/thegamerhat) 

[![Twitter](https://img.shields.io/badge/Twitter-%231DA1F2.svg?&style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/thegamerhat)

[![Instagran](https://img.shields.io/badge/Instagram-%23E4405F.svg?&style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/thegamerhat)

