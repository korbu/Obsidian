# Clone the C++ Core Guidelines onto each machine
**Created**: Monday, January 03, 2022 04:18:47 PM -05:00

```PowerShell
md C:\Dev\GitHub\isocpp
pushd C:\Dev\GitHub\isocpp
git clone https://github.com/isocpp/CppCoreGuidelines.git
cd .\CppCoreGuidelines\
start .\CppCoreGuidelines.md
```

Note: I don't recommend viewing this in Obsidian, as the links don't work.  I had a better experience opening it in VS Code using a Markdown preview window by running the following:

```PowerShell
code .\CppCoreGuidelines.md
```
