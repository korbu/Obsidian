1. [Community - Obsidian](https://obsidian.md/community)
2. [Obsidian Forum](https://forum.obsidian.md/)
3. [Obsidian (@obsdmd) / Twitter](https://twitter.com/obsdmd)
4. [kmaasrud/awesome-obsidian: 🕶️ Awesome stuff for Obsidian (github.com)](https://github.com/kmaasrud/awesome-obsidian)
5. Converting from OneNote to Obsidian
	1. [How to migrate many OneNote notebooks to Obsidian from scratch (2k+ files) - Share & showcase - Obsidian Forum](https://forum.obsidian.md/t/how-to-migrate-many-onenotes-to-obsidian-from-scratch-2k-files/22538)
	2. Modified version of the PowerShell script to create a Map of Contents (MOC).
		1. [rab-bit/ConvertOneNote2MarkDown4Obsidian: Ready to make the step to Markdown and saying farewell to your OneNote, EverNote or whatever proprietary note taking tool you are using? Nothing beats clear text, right? Read on! (github.com)](https://github.com/rab-bit/ConvertOneNote2MarkDown4Obsidian)
	3. Things to modify in the script I'm using:
		1. Timestamps are UTC-6. Is that because I'm currently in TX?  Maybe allow to specify the timestamp.
		2. I may want to remove the {width,height} references that get inserted.
		3. It named C++ as C^M^M.  How do we fix this?
		4. When converting code that starts with \_, it turns it into italics.
		5. **I lost any content on pages that were used as folder names!**, e.g. C++ Tricks and Tips.
		6. Anywhere I had `#include` for code examples lost whatever followed that, e.g. \<string\>.  These need to have \\ inserted before these characters.
			1. [ ] Or just put \`\`\`lang around the block of code.
			2. [ ] Look for \#\include and a close curly brace to see if that helps.
			3. [ ] Don't remove indentation when this is found.
		7. [ ] Do I need to do something similar for `using` and C#?
		8. These blocks of code also ended up double-spaced.  How do we fix this?
		9. [x] Create a new notebook with just examples of things that failed and try to fix them so it's easier to eliminate these bugs rather than reconverting my entire notebook.
		10. [x] Look into the eng.ms solution for converting OneNotes to see if it's any better.
			1. ~~I tried it; it's okay.  I need to compare it to how this script works and see if either one is better.~~
			2. It was better! Modifying that VS .sln going forward.
		11. The "Created" and "Modified" timestamps come from the theohbrothers script.
			1. [x] Add these to the Visual Studio project.
		12. [x] Don't add hyphens to folder (and file?) names.
		13. [x] Replace forward slashes in filenames with " & ".
		14. [x] Replace colons in filenames with " - ".
		15. [x] Replace double quotes in filenames with single quotes.
		16. [x] Stop converting hyphens to %2D.
		17. [x] Remove .order files from AzDO output.
			1. Changed default metadata generation to None.
		18. [x] Get rid of WriteNotebookTitle.
		19. [x] Change (Get rid of?) WriteAllSectionTitles to put those files in their subdirectories.			
		20. [x] Get rid of the image sizing, which is only included in AzDO.
		21. [x] Put the page for a folder in the subfolder. It currently gets created above it.
		22. [ ] Figure out how to fix "Bart's Top Resources that Help you Learn C++".
			1. The formatting is all wrong!
		23. Why did  the "Jason Turner "The Best Parts of C++"" page lose all of its highlighting?
			1.   The "Beginner: Learn How to Program with C++" page also lost all its highlighting.
		24. [x] When fixing up links between OneNote notebooks, don't use the \(\)\[\] format.  Use \[\[\]\] instead. See the "Training To-Do" page.
		25. ~~[ ] Add an empty row for table headers (most of the time? What about when a table actually has a header?).~~
			1. I found a table that actually has a header and it looks correct, so not sure how to fix this.
		26. ~~[ ] Add shading to table headers?~~
			1. This doesn't appear to work in Obsidian (yet).
		27. [ ] Ensure that http URLs also get converted to links (in addition to https).
		28. [ ] Get rid of any \ufffc characters (see the converted C++ Glossary page for an example. It shows up as OBJ.
		29. [ ] Convert any \<span style="background-color:yellow"\> to \<mark...yellow\> for Obsidian.
		30. [ ] Convert any \<span style="background-color:lime"\> to \<mark...green\> for Obsidian.
		31. [ ] Add c++ after \`\`\` to make code appear correctly.
		32. [x] How do we differentiate C# for code blocks?
			1. According to [Prism (prismjs.com)](https://prismjs.com/#supported-languages), you can use: `csharp`, `cs`, `dotnet`.
			2. See the bottom of this page for a test.
		33. Update ReverseMarkdown nuget package.
		34. [x] Why does the Prism theme look great on my Azure Storage notebook and horrible on my Programming notebook?
			1. This has nothing to do with OneNote conversions.
			2. Maybe try disabling all of the plugins.
			3. <mark style="background: #BBFABBA6;">I needed to install and enable the Style Settings plugin.</mark> 
		35. <mark style="background: #FFF3A3A6;">It looks like Microsoft.Graph v1.14.0.0 is not retrieving data-tag entries correctly.</mark> 
			1. `IOnenoteRequestBuilder` is the suspicious class.
			2. `IOnenotePageContentRequest.Request` is the suspicious method.
			3. [Input and output HTML in OneNote pages - Microsoft Graph | Microsoft Docs](https://docs.microsoft.com/en-us/graph/onenote-input-output-html)
			4. [Use Graph Explorer to try Microsoft Graph APIs - Microsoft Graph | Microsoft Docs](https://docs.microsoft.com/en-us/graph/graph-explorer/graph-explorer-overview)
			5. https://graph.microsoft.com/v1.0/users/aaa72475-f50f-43e5-800f-f8c9d44cf60b/onenote/pages/1-2f4d320c1b83414585c0b424b6e6d8d5!1-84e33c5e-834a-4e25-b57c-9878ee46bd83/content
			6. Using the Microsoft Graph explorer returned the wrong data-tags, e.g., \<span data-tag="remember-for-later"\> instead of \<span data-tag="definition"\>
			7. [Microsoft Graph - Microsoft Graph Contacts - All Items (sharepoint.com)](https://microsoft.sharepoint.com/sites/Graph/Lists/Microsoft%20Graph%20Contacts/AllItems.aspx)
		36. To include a line break in a table where there are URLs, you need to ensure that you do not use bare URLs, e.g., use \<URL\>.

```csharp
using System;
class HelloWorld {
  static void Main() {
    Console.WriteLine("Hello World");
  }
}
```