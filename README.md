# Proton-Bleeding-Edge-AVX512
Proton Builds Built With AVX-512 &amp; Partial PGO+LTO.


# Requirements:
<a href="https://github.com/ValveSoftware/Proton/wiki/Requirements"> **Normal Proton Requirements**</a>

**Linux Kernel: 6.0+** > Starting from Build 5

**AVX512**🌶️

You can figure out if you have AVX512 by opening a terminal:   `grep avx512 /proc/cpuinfo`

If you see avx512 highlighted you're good to go.

**Notices:**

At some point i plan on making Intel 10th generation feature set the minimum target. Older target will be discontinued for AVX512.

All AVX512 CPU's That cannot maintain max boost under heavy 256/512bit workloads are not officially supported. Unless manually overclocked back up to normal boost speeds, with turbo boost disabled.

# Install:

Download a build from <a href="https://github.com/UbuntuGaming/Proton-Bleeding-Edge-AVX512/releases"> Releases</a>

Create a `~/.steam/root/compatibilitytools.d` directory if it does not exist.
Extract the release into `~/.steam/root/compatibilitytools.d/`

# Issues:
Please don't submit issues to Valve using logs from these builds. If you have issues with both Proton_AVX512 & Proton official builds. Please submit them logs from the official builds.

# Important Notices:

This project is not affiliated with Valve Corporation's Proton.

This is a hobby project. (I come & go as i please)

This project does not accept any donations or payment. (If someone claims to be a representative of this project.. They are not...)

While the project has held onto same name as "Proton BleedingEdge" for now. This is not at 100% replica of BleedingEdge starting from build 5.

If a program requires kernel boot parameter: clearcpuid=304 Wine will not work at all.

In credits you might see people outside of the Wine/Proton project. These are people who are credited with the following: initial patches, whole patches or ideas.

This project is a binary release only, sources will be available when i get around to it. (But it might be unbuildable)

# How often will you release packages:
When i feel like it, But i try to make at least one a month.

If Proton only has a few commits, a build will be skipped.

If i have Functionality/Performance regressions builds will be stopped until **all** issues are resolved.

# Roadmap:

**(Stable)**

- [ ] LTO.

- [ ] PGO.

- [ ] More performance.

**(Unstable)**

- [X] LTO.

- [ ] PGO.

# Questions:

>Question 1: How can i ID the build?
>
>Answer 1: Open the version file in the release you've downloaded.

>Question 2: Explain Build Versions?
>
>Answer 2: ***BleedingEdge9-AVX512 Build 123.4*** "9" as in the wine version, "123" as in the build version. ".4" as in the build revision.

>Question 3: Release vs Pre-release?
>
>Answer 3: From time to time you might get a pre-release build. This won't be as refined as the main release & might contain stuff that will be removed or updated in the actual release.

>Question 4: What is the 'Proton-NoSteam' Folder?
>
>Answer 4: This allows you to use Proton outside of Steam for non-steam Windows applications, Read the 'EditMe!' script to learn how to use it.

>Question 5: Full PGO + LTO on Wine?
>
>Answer 5: Working on it.

>Question 6: Does BleedingEdge-AVX512 work with MIDI devices?
>
>Answer 6: Depending how the software communicates with the device, Yes. Most USB MIDI devices will work as if it was native windows, Other device types haven't been tested. System & software may require additional tuning to get everything working flawlessly. MIDI Devices containing software activation codes is being worked out, But is not a priority.

# Universal Variables:

>Question 1: I have this really old application (or an application that doesn't like hyperthreading) & it favours single core performance is there anything i can do to get more fps?
>
>Answer 1: Yes, Well kind of, depends. If you're using a CPU with hyperthreading you can try disabling hyperthreading in software for the single application
>
>Example i have a 6 core CPU that has 12 total threads. If i check `cat /sys/devices/system/cpu/cpu*/topology/thread_siblings_list | sort | uni` I can see the first value (on the left side) i see is 0, now if i follow this list down i get 0,1,2,3,4,5 (this is 6 cores) So in steam if i set `WINE_CPU_TOPOLOGY=6:0,1,2,3,4,5 %command%` I have told the application i only have 6 cores & have sucessfully locked the process onto the specified cores.
> I've done the testing for this & this leads to a 5% performance improvement in Metro 2033 running under Proton & around 1% performance difference in windows gpu benchmarks running under Proton.
>
>Important note on **WINE_CPU_TOPOLOGY:** I've found an issue where WINE_CPU_TOPOLOGY will only set the mask for some threads, But does change total number of cpus. Getting around the issue can be done in steam via taskset `WINE_CPU_TOPOLOGY=6:0,1,2,3,4,5 taskset -c 0,1,2,3,4,5 %command%` note when using taskset it's the same as using WINE_CPU_TOPOLOGY ignore the total number of cores and the delimiter. 

# Universal Game Variables:
 DX12/VKD3D-Proton in games that "don't support it" (This was tested on RADV)

Unity: -force-d3d12

Unreal Engine 4: -dx12

(Note: This can't be done to turn games into native Vulkan as game developers would have to include the processed Vulkan shaders in the DirectX build)

# More performance outside of Proton:
> **Important Note**: This section might be broken off into it's own repository, With much more information. (Or deleted)

>Theoretical Question: I want more performance.
>
>
>Kernel:
>You can get much more out of the kernel in very old applications
> `grep 'CONFIG_HZ=' /boot/config-$(uname -r)`
>if you're not running a 1000hz kernel you can rebuild the <a href="https://www.kernel.org/"> Kernel</a> using your current one as a template. Some people will say 1000hz is snake oil this is false.

> Scheduler:
> If your kernel supports BPF you can test out <a href="https://docs.rs/crate/scx_lavd/latest"> **__scx_lavd__**</a>, If the kernel doesn't support it, Build a new kernel using the old config as a template. guides, <a href="https://github.com/sched-ext/scx-kernel-releases/releases"> patches</a> & <a href="https://www.rust-lang.org/tools/install"> rust compiler</a> can be found online. **_Or ask your distros kernel package maintainer for everything._**
>
> (Performance results -3% to +7%. Basically you'll have to do the testing yourself for each title. Note: My results only include 0.1% lows, 1% lows & average fps. As this is all that matters, fps highs are not included.)

>Mouse & Keyboard:
> You can change mouse & keyboard response times with kernel variables. this can be done with startup parameters *GRUB* `/etc/default/grub` then update grub as normal, guides can be found online. I don't use systemd-boot but i found <a href="https://wiki.archlinux.org/title/Kernel_parameters"> this</a> on Arch wiki.
>
> the variables are as follows `mousepoll=1 kbpoll=1 jspoll=1`

> AMD Mesa Drivers (Building):
>Profiling <a href="https://gitlab.freedesktop.org/mesa/mesa"> Mesa</a> & optimising for your CPU may not lead to a massive GPU performance increase. But the latency reduction & CPU usage is clear.
