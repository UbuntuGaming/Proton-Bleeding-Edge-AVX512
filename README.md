# Proton-Bleeding-Edge-AVX512
Proton Builds Built With AVX-512 &amp; Partial PGO+LTO.


# CPU Instruction Requirements:
AVX512🌶️

You can figure out if you meet the requirements by opening a terminal:   `grep avx512 /proc/cpuinfo`

If you see avx512 in red you're good to go.

Other CPU features are required but are universally there across both Intel & AMD AVX-512 CPUs.

# Install:

Download a release from the Releases page.
Create a `~/.steam/root/compatibilitytools.d` directory if it does not exist.
Extract the release into `~/.steam/root/compatibilitytools.d/`

# Issues:
Please don't submit issues to Valve using logs from these builds. If you have issues with both Proton_AVX512 and Proton official builds. Please submit them logs from the official builds. Unless both are failing at the same point.


# Titles that don't work:
The Finals. (Starting from release _14d7b51_AVX512_ It should now run perfectly)

Battlebit Remastered (Starting from _14d7b51_AVX512.Rev2_ It now launches perfectly everytime.)

Any program that requires kernel boot parameter: clearcpuid=304

# Important Notice:
For now packages are only built with -O3.

Some titles may not work. (But if i find them i can solve the issue, If it's simple enough)

# How often will you release packages:
Updated biweekly.

# To do list:

- [ ] Rework Steam game saves to into "$HOME/Documents" under "ProtonDocuments/APPID" rather than the prefix. (This will create a shared space for game saves that don't support cloud sync.)

# Other info:

>Question 1: How can i ID the build?
>
>Answer 1: Check the commit number before AVX-512 (Or open the version file in the release you've downloaded).
>I'm using the commit numbers to name each build as i'm terrible at naming stuff & since the sources are nearly identical it makes sense.


>Question 2: Can i get the source?
>
>Answer 2: The source is a direct copy of bleeding-edge-(Insert-commit) With a few build changes to Proton & it's subprojects. In the future i may create repository that supports newly supported titles/features by upstream Wine, But this repository does not have any actual source changes, Excluding workarounds to fix issues.


>Question 3: Is my performance going to increase by a dramatic amount?
>
>Answer 3: Performance gains are negligible in my testing (Tried both -O2 & -O3) even with AVX+PGO+LTO on some subprojects. But i paid for the whole CPU, I'm going to use the whole CPU!. 
>
>Expect slightly higher power consumption, If you haven't already now would be a good time to go into the bios & manually setup fan control to be controlled by CPU temp. 
>
>This repository serves to save people time bothering to compile Proton with AVX512 support themselves, with most™️ the issues pre-solved, or currently being figured out.


>Question 4: What is the 'Proton-NoSteam' Folder?
>
>Answer 4: This allows you to use Proton outside of Steam for non-steam Windows applications, Read the 'EditMe!' script to learn how to use it.

>Question 5: Proton-No-Steam How do i get the icon for my application to add to a .Desktop file?
>
>Answer 5: Currently it's just a script, I will soon start packaging Proton with a open-source tool for pulling the icon.

>Question 6: Full PGO + LTO on Wine?
>
>Answer 6: You won't get LTO. But as for PGO i'm working on it.. (When i do get it working only expect one build per month..)

>Question 7: Why is the formatting of this page so terrible?
>
>Answer 7: I'm learning.

# Universal Variables:

>Question 1: I have this really old application (or an application that doesn't like hyperthreading) & it favours single core performance is there anything i can do to get more fps?
>
>Answer 1: Yes, Well kind of, depends. If you're using a CPU with hyperthreading you can try disabling hyperthreading in software for the single application
>
>Example i have a 6 CPU that has 12 total threads. If i check `cat /sys/devices/system/cpu/cpu*/topology/thread_siblings_list | sort | uni` I can see the first value (on the left side) i see is 0, now if i follow this list down i get 0,1,2,3,4,5 (this is 6 cores) So in steam if i set `WINE_CPU_TOPOLOGY=6:0,1,2,3,4,5 %command%` I have told the application i only have 6 cores & have sucessfully locked the process onto the specified cores.
> I've done the testing for this and this leads to a 5% performance improvement in Metro 2033 running under Proton and around 1% performance difference in windows gpu benchmarks running under Proton.

# More performance outside of Proton:
>Theoretical Question: I want more performance.
>
>
>Kernel:
>You can get much more out of the kernel in very old applications
> `grep 'CONFIG_HZ=' /boot/config-$(uname -r)`
>if you're not running a 1000hz kernel you can rebuild the kernel using your current one as a template the source can be found on www.kernel.org. Some people will say 1000hz is snake oil this is false. I've done the testing and in every test i got better performance and lower power consumption. So for gaming 1000hz is recommended, especially if using studio grade audio setups, upsampling ect the reduction in cpu usage is nearly 30%!. If you're sitting on the desktop completely idle, yes less would probably be better.
>
>
> Scheduler:
> If your kernel supports it you can test out scx_lavd, If the kernel does not support it download the source from www.kernel.org use the old kernel config as a template. Guides can be found online.

> AMD Mesa Drivers (Building):
>Profiling mesa's common functions and optimising for your CPU may not lead to a massive performance increase, but the latency reduction & CPU usage is clear. If you're on Debian 13/Trixie/Testing i may be releasing my own repository for packages soon™️.
>
> AMD Mesa Drivers (Git):
> Is newer better?
>
> No, for example in the latest master (on RX 7800XT). Some titles will experience effects alignment issues, in the case of StarWars Battlefront II textures will look like square pieces of cake. find a stable version and work your way forward, You can always backport patches this is what i'm doing. As i don't want to bisect the amount of commits mesa goes through in a month.
