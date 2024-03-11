# Proton-Bleeding-Edge-AVX512
Proton Builds Built With AVX-512 &amp; Partial PGO+LTO.

# Install

Download a release from the Releases page.
Create a ~/.steam/root/compatibilitytools.d directory if it does not exist.
Extract the release into ~/.steam/root/compatibilitytools.d/

# Issues
Please do not submit issues to Valve without confirming it doesn't work with a regular build of proton directly from them

# Titles that do not work:
The Finals.

Any title that requires kernel Boot parameter: clearcpuid=304

# Titles that work but have issues:
Call Of Duty: Black Ops 3

# Important Notice
For now packages are only built with -O3. Some titles may not work E.G Black Ops 3 is known to crash on main menu if moving around the menus with the zoomies.

# How often will you release packages:
Updated biweekly.

# Other info
Packages are compressed using LZMA.

Question 1: How can i ID the build?

Answer 1: Check the commit number before AVX-512. (Or open the version file in the release you've downloaded)


Question 2: Can i get the source?

Answer 2: The source is a direct copy of bleeding-egde-(Insert-commit)


Question 3: Does this include all instructions ranging from x86-64-v1 to x86-64-v4?

Answer 3: This is a stripped down version. The same as if you was building with core-avx2 (According to GCC source code), But with AVX-512 support (If -mtune=core-avx512 was a feature this would be it)
