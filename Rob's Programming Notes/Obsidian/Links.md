1. [Community - Obsidian](https://obsidian.md/community)
2. [Obsidian Forum](https://forum.obsidian.md/)
3. [Obsidian (@obsdmd) / Twitter](https://twitter.com/obsdmd)
4. [kmaasrud/awesome-obsidian: 🕶️ Awesome stuff for Obsidian (github.com)](https://github.com/kmaasrud/awesome-obsidian)
5. Converting from OneNote to Obsidian
	1. [How to migrate many OneNotes to Obsidian from scratch (2k+ files) - Share & showcase - Obsidian Forum](https://forum.obsidian.md/t/how-to-migrate-many-onenotes-to-obsidian-from-scratch-2k-files/22538)
	2. Modified version of the PowerShell script to create a Map of Contents (MOC).
		1. [rab-bit/ConvertOneNote2MarkDown4Obsidian: Ready to make the step to Markdown and saying farewell to your OneNote, EverNote or whatever proprietary note taking tool you are using? Nothing beats clear text, right? Read on! (github.com)](https://github.com/rab-bit/ConvertOneNote2MarkDown4Obsidian)
	3. Things to modify in the script I'm using:
		1. Timestamps are UTC-6. Is that because I'm currently in TX?  Maybe allow to specify the timestamp.
		2. I may want to remove the {width,height} references that get inserted.
		3. It named C++ as C^M^M.  How do we fix this?
		4. When converting code that starts with \_, it turns it into italics.
		5. **I lost any content on pages that were used as folder names!**, e.g. C++ Tricks and Tips.
		6. Anywhere I had `#include` for code examples lost whatever followed that, e.g. \<string\>.  These need to have \\ inserted before these characters.
			1. Or just put \`\`\`lang around the block of code.
		7. These blocks of code also ended up double-spaced.  How do we fix this?
		8. Create a new notebook with just examples of things that failed and try to fix them so it's easier to eliminate these bugs rather than reconverting my entire notebook.
		9. Look into the eng.ms solution for converting OneNotes to see if it's any better.
		10. 