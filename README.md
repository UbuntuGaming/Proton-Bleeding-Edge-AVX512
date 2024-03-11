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

Q: How can i ID the build

A: Check the commit number before AVX-512. (Or open the version file in the release you've downloaded)


Q: Can i get the source

A: The source is a direct copy of bleeding-egde-(Insert-commit)
