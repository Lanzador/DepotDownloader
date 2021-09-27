Lanzador's fork
===============

I added some edits to the original fork. Here's what I changed:
Edit #1

 * Added the `-apptoken` parameter that lets you specify an app token for apps that need one.

Edit #2

 * Fixed a mistake which caused a crash if no app token was given.
 * Improved `-manifest-only` by copying code from version 2.4.4 of the original DepotDownloader. (Not included in this repo for now because I fucked up)

I'm planning to do another edit soon.

DepotDownloader fork
===============

* added support for loading depot keys from a file (with -depotkeys commandline option)
* changed the resulting directory structure


DepotDownloader original readme
===============

Steam depot downloader utilizing the SteamKit2 library. Supports .NET Core 2.0

```
Usage - downloading one or all depots for an app:
	dotnet DepotDownloader.dll -app <id> [-depot <id> [-manifest <id>] | [-ugc <id>]]
		[-username <username> [-password <password>]] [other options]

Usage - downloading a Workshop item published via SteamUGC
	dotnet DepotDownloader.dll -pubfile <id> [-username <username> [-password <password>]]

Parameters:
	-app <#>				- the AppID to download.
	-depot <#>				- the DepotID to download.
	-manifest <id>			- manifest id of content to download (requires -depot, default: current for branch).
	-ugc <#>				- the UGC ID to download.
	-beta <branchname>		- download from specified branch if available (default: Public).
	-betapassword <pass>	- branch password if applicable.
	-all-platforms			- downloads all platform-specific depots when -app is used.
	-os <os>				- the operating system for which to download the game (windows, macos or linux, default: OS the program is currently running on)

	-pubfile <#>			- the PublishedFileId to download. (Will automatically resolve to UGC id)

	-username <user>		- the username of the account to login to for restricted content.
	-password <pass>		- the password of the account to login to for restricted content.
	-remember-password		- if set, remember the password for subsequent logins of this user.

	-dir <installdir>		- the directory in which to place downloaded files.
	-filelist <file.txt>	- a list of files to download (from the manifest). Can optionally use regex to download only certain files.
	-validate				- Include checksum verification of files already downloaded

	-manifest-only			- downloads a human readable manifest for any depots that would be downloaded.
	-cellid <#>				- the overridden CellID of the content server to download from.
	-max-servers <#>		- maximum number of content servers to use. (default: 8).
	-max-downloads <#>		- maximum number of chunks to download concurrently. (default: 4).
```
