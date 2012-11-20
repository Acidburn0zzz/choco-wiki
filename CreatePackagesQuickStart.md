## Creating Chocolatey Packages - TL;DR version

Here's a TL;DR quick start version of the package creating tutorial. Follow these steps to create a simple package.

**Problem?** Read the lengthy version: [[Creating Chocolatey Packages|CreatePackages]]

## Prerequisites


* You have Chocolatey installed.

## Quick start guide


* **Generate package template** using [[WarmuP|http://chocolatey.org/packages/warmup]]:
   * _cinst warmup_
   * Get templates:
      * _cinst git_
      * _cd %ChocolateyInstall%_
      * _git clone [[https://github.com/chocolatey/chocolateytemplates.git]]_
      * _cd chocolateytemplates\_templates_
      * _warmup  addTemplateFolder chocolatey "%CD%\chocolatey"_
   * Add replacements. You can get more creative once you start making more complicated packages.
      * _warmup addTextReplacement __CHOCO_PKG_OWNER_NAME__ "Your Name"_
(could be same as other)"_
   * _warmup chocolatey PackageName_
* **Edit template** using common sense
   * _cd PackageName_
   * Complete PackageName.nuspec
   * Complete ./tools/chocolateyInstall.ps1
* **Build the package**
   * Still in package directory
   * _cpack_
      * "successfully created PackageName.1.1.0.nupkg"
* **Test the package**
   * **Testing should probably be done on a Virtual Machine**
   * In your package directory, use: 
      * _cinst PackageName -source '%cd%'_
   * Otherwise, use the full path:
      * _cinst PackageName -source 'c:\path\to\PackageName.1.1.0.nupkg'_
* **Push the package** to the Chocolatey repository:
   * Get a Chocolatey account:
      * [[http://chocolatey.org/account/Register]]
   * Copy the API key [[from your Chocolatey account|http://chocolatey.org/account]].
   * _cinst nuget.commandline_
   * _nuget SetApiKey [API_KEY_HERE] -source [[http://chocolatey.org/]]_
   * _cpush PackageName.1.1.0.nupkg_

## Common Mistakes


* **NuSpec**
   * **id** is the package name and should contain no spaces and weird characters.
   * **version** is a dot-separated identifier containing a maximum of 4 numbers. e.g. _1.0_ or _2.4.0.16_
   * **The path to your package** should contain no spaces, or enclose pathnames with single or double doublequotes, like so:
      * 'PackageName'
      * ""PackageName""
* **Using NuGet tools**
   * **Specify the source** if you accidentally use NuGet commands when following some guide in stead of Chocolatey commands. E.g.:
      * _nuget push package.nupkg** -source [[http://chocolatey.org/]]**_ # in stead of:
      * _cpush package.nupkg_

## Environmental Variables


* %ChocolateyInstall% Chocolatey installation directory
* %ChocolateyInstall%\lib\PackageName - Package directory
* %chocolatey_bin_root% - Path of Binaries
* %cd% - current directory