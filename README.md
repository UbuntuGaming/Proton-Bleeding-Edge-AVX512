# Proton-Bleeding-Edge-AVX512
Proton Builds Built With AVX-512 &amp; Partial PGO+LTO.

# Install:

Download a release from the Releases page.
Create a ~/.steam/root/compatibilitytools.d directory if it does not exist.
Extract the release into ~/.steam/root/compatibilitytools.d/

# Issues:
Please do not submit issues to Valve without confirming it doesn't work with a regular build of proton directly from them.

# Titles that do not work:
The Finals.

Any title that requires kernel boot parameter: clearcpuid=304

# Important Notice:
For now packages are only built with -O3. 
Some titles may not work. (But if i find them i can solve the issue, If it's simple enough)

# How often will you release packages:
Updated biweekly.

# Other info
Packages are compressed using LZMA.

Question 1: How can i ID the build?

Answer 1: Check the commit number before AVX-512. (Or open the version file in the release you've downloaded)


Question 2: Can i get the source?

Answer 2: The source is a direct copy of bleeding-edge-(Insert-commit) With a few build changes to Proton & it's subprojects. In the future i may create repository that supports newly supported titles/features by upstream Wine, But this repository does not have any actual source changes, Excluding workarounds to fix issues.


Question 3: Is my performance going to increase by a dramatic amount?

Answer 3: Performance gains are negligible in my testing (Tried both -O2 & -O3) even with AVX+PGO+LTO on some subprojects. But i paid for the whole CPU, I'm going to use the whole CPU! This repo serves to save people time bothering to compile it themselves.


Question 3: What is the 'Proton-NoSteam' Folder?

Answer 3: This allows you to use Proton outside of Steam for non-steam Windows applications, Read the 'EditMe!' script to learn how to use it.


Question 4: Full PGO + LTO on Wine?

Answer 4: You won't get LTO. But as for PGO i'm working on it..
