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

# Other info

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
>
>
>Question 5: Full PGO + LTO on Wine?
>
>Answer 5: You won't get LTO. But as for PGO i'm working on it.. (When i do get it working only expect one build per month..)




