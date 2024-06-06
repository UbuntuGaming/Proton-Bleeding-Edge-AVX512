# Proton-Bleeding-Edge-AVX512
Proton Builds Built With AVX-512 &amp; Partial PGO+LTO.


# CPU Instruction Requirements:
AVX512🌶️

You can figure out if you meet the requirements by opening a terminal:   `grep avx512 /proc/cpuinfo`

If you see avx512 highlighted you're good to go.

Other CPU features are required but are universally there across both Intel & AMD AVX-512 CPUs.

# Install:

Download a build from <a href="https://github.com/UbuntuGaming/Proton-Bleeding-Edge-AVX512/releases"> Releases</a>

Create a `~/.steam/root/compatibilitytools.d` directory if it does not exist.
Extract the release into `~/.steam/root/compatibilitytools.d/`

# Issues:
Please don't submit issues to Valve using logs from these builds. If you have issues with both Proton_AVX512 and Proton official builds. Please submit them logs from the official builds. Unless both are failing at the same point.


# Titles that don't work:

Any program that requires kernel boot parameter: clearcpuid=304

# Important Notice:
For now packages are only built with -O3.

Some titles may not work. (But if i find them i can solve the issue, If it's simple enough)

# How often will you release packages:
When i feel like it, But i try to make at least one a month.

If Proton only has a few commits, a build will be skipped.

# To do list:

- [X] More performance.

- [ ] Even more performance.

# Other info:

>Question 1: How can i ID the build?
>
>Answer 1: Open the version file in the release you've downloaded.

>Question 2: Explain Build Versions?
>
>Answer 2: ***BleedingEdge9-AVX512 Build 123.4*** "9" as in the wine version, "123" as in the build version. ".4" as in the build revision.

>Question 3: Release vs Pre-release?
>
>Answer 3: From time to time you might get a pre-release build. Days after the stable release. this won't be as refined as the main release, and might contain stuff that will be removed or updated in the actual release.

>Question 4: Can i get the source?
>
>Answer 4: The source is a direct copy of bleeding-edge-(Insert-commit) With a few build changes to Proton & it's subprojects. But this repository does not have any actual source changes excluding workarounds to fix issues.


>Question 5: Is my performance going to increase by a dramatic amount?
>
>Answer 5: Performance gains are negligible in my testing (Tried both -O2 & -O3) even with AVX+PGO+LTO on some subprojects. But i paid for the whole CPU, I'm going to use the whole CPU!. 
>
>This repository serves to save people time bothering to compile Proton with AVX512 support themselves, with most™️ the issues pre-solved, or currently being figured out.


>Question 6: What is the 'Proton-NoSteam' Folder?
>
>Answer 6: This allows you to use Proton outside of Steam for non-steam Windows applications, Read the 'EditMe!' script to learn how to use it.

>Question 7: Proton-No-Steam How do i get the icon for my application to add to a .Desktop file?
>
>Answer 7: Currently it's just a script, I will soon start packaging Proton with a open-source tool for pulling the icon.

>Question 8: Full PGO + LTO on Wine?
>
>Answer 8: ~~You won't get LTO. But as for PGO i'm working on it.. (When i do get it working only expect one build per month..)~~
>
> I don't have the tools to PGO all of Wine, I would need alot of storage & a huge collection of games. I might revisit this in the future.

>Question 9: Proton-No-Steam does music production software work with MIDI devices?
>
>Answer 9: Yes, If the software runs & doesn't require web-browser callbacks to activate. Most MIDI devices will work as if it was native windows. System & software may require additional tuning to get it working flawlessly.

# Universal Variables:

>Question 1: I have this really old application (or an application that doesn't like hyperthreading) & it favours single core performance is there anything i can do to get more fps?
>
>Answer 1: Yes, Well kind of, depends. If you're using a CPU with hyperthreading you can try disabling hyperthreading in software for the single application
>
>Example i have a 6 core CPU that has 12 total threads. If i check `cat /sys/devices/system/cpu/cpu*/topology/thread_siblings_list | sort | uni` I can see the first value (on the left side) i see is 0, now if i follow this list down i get 0,1,2,3,4,5 (this is 6 cores) So in steam if i set `WINE_CPU_TOPOLOGY=6:0,1,2,3,4,5 %command%` I have told the application i only have 6 cores & have sucessfully locked the process onto the specified cores.
> I've done the testing for this and this leads to a 5% performance improvement in Metro 2033 running under Proton and around 1% performance difference in windows gpu benchmarks running under Proton.
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
> You can change mouse and keyboard response times with kernel variables. this can be done with startup parameters *GRUB* `/etc/default/grub` then update grub as normal, guides can be found online. I have no idea for <a href="https://wiki.archlinux.org/title/Kernel_parameters"> systemd-boot</a> when i find a OS with systemd-boot i disable it and install grub.
>
> the variables are as follows `mousepoll=1 kbpoll=1 jspoll=1`

> AMD Mesa Drivers (Building):
>Profiling <a href="https://gitlab.freedesktop.org/mesa/mesa"> Mesa</a> & optimising for your CPU may not lead to a massive performance increase. But the latency reduction & CPU usage is clear.
