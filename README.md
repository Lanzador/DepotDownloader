Lanzador's fork
===============

I added some edits to the original fork. Here's what I changed:

Edit #1

 * Added the `-apptoken` parameter that lets you specify an app token for apps that need one.

Edit #2

 * Fixed a mistake which caused a crash if no app token was given.
 * Improved `-manifest-only` by copying code from version 2.4.4 of the original DepotDownloader.

Unnumbered edits (I forgot to update the readme...)

 * You can load a manifest - encrypted or decrypted - from a file by putting the file in the "manifests" folder and naming it "\<DepotID\>_\<ManifestID\>.manifest" ~~or "\<DepotID\>.manifest"~~.
 * Fixed the tool not working because Steam removed CDN tokens.
 * When downloading a manifest, it's saved to "manifests\downloaded" (in encrypted form, sorry).
 * Merged this outdated fork's features with a new version of DD (Also, right now when copying the result from Lanzador/merge-dd I had to add a line to the csproj to fix some weird error). The pre-merge version can be found in the pre-merge branch.
 * Finally fixed the fact it says "Will try to use app token given in the parameter." even if none is given.

Edit #4

 * `-delta-manifest` can now be used to provide a custom delta manifest instead of whatever is stored in your config file. It can accept multiple values, just like `-manifest`.

Edit #5

 * Added all features of this fork to DepotDownloader 2.4.6. You can now download manifests through your account again!
 * While re-adding the changes of the original fork, got rid of some unused stuff. Also finally fixed crash when `-dir` is used before the `depots` folder is created.
 * Also put all new parameters into `LanzadorData` to not write each one as an argument in lots of places.
 * Removed loading manifests from "\<DepotID\>.manifest". Use the full file name. Also removed the option to disable manifest saving by creating NOSAVE.txt in "manifests\downloaded" - I didn't even mention it here, I probably forgot about it right after making it.
 * Finally fixed the fact it says "Will try to use app token given in the parameter." even if none is given. Sounds familiar? This time for real.
 * Added `-delta-branch` to specify branch of the old manifest if it was different for requesting the manifest code. Seems to work even without doing this, but I didn't know that until I made it. Perhaps it'll be useful someday.
 * Now prints download time after each depot and the whole download.
 * Use `-progress-every-s` (seconds), `-progress-every-ms` (milliseconds), `-progress-every-p` (percent) or `-progress-every-b` (bytes) with a number to get regular progress reports even if the file is large. You can use multiple of these at the same time (but only one of the first two). The third one can accept decimal numbers.
 * Use `-free-license` to request a FreeOnDemand license if possible. This feature was removed in the original fork, but I brought it back.
 * A separate "no app token" release is no more! Use `-depot-exists` to bypass app token. Can also be used to download workshop items by their depot ID and manifest ID. (You still need to manually enter the manifest ID if using thus)
 * Updated original readme to v2.4.6.

Oh, also, there's a compiled release here.

~~The no-app-token branch is a version that lets you download depots without having the app token - I took the code from @IntriguingTiles. If using this, you must manually provide a manifest ID.~~ Removed in edit #5.


DepotDownloader fork
===============

* added support for loading depot keys from a file (with -depotkeys commandline option)
* changed the resulting directory structure


DepotDownloader original readme
===============

Steam depot downloader utilizing the SteamKit2 library. Supports .NET 6.0

### Downloading one or all depots for an app
```
dotnet DepotDownloader.dll -app <id> [-depot <id> [-manifest <id>]]
    [-username <username> [-password <password>]] [other options]
```

For example: `dotnet DepotDownloader.dll -app 730 -depot 731 -manifest 7617088375292372759`

### Downloading a workshop item using pubfile id
```
dotnet DepotDownloader.dll -app <id> -pubfile <id> [-username <username> [-password <password>]]
```

For example: `dotnet DepotDownloader.dll -app 730 -pubfile 1885082371`

### Downloading a workshop item using ugc id
```
dotnet DepotDownloader.dll -app <id> -ugc <id> [-username <username> [-password <password>]]
```

For example: `dotnet DepotDownloader.dll -app 730 -ugc 770604181014286929`

## Parameters

Parameter | Description
--------- | -----------
-app \<#>				| the AppID to download.
-depot \<#>				| the DepotID to download.
-manifest \<id>			| manifest id of content to download (requires -depot, default: current for branch).
-ugc \<#>				| the UGC ID to download.
-beta \<branchname>		| download from specified branch if available (default: Public).
-betapassword \<pass>	| branch password if applicable.
-all-platforms			| downloads all platform-specific depots when -app is used.
-os \<os>				| the operating system for which to download the game (windows, macos or linux, default: OS the program is currently running on)
-osarch \<arch>			| the architecture for which to download the game (32 or 64, default: the host's architecture)
-all-languages			| download all language-specific depots when -app is used.
-language \<lang>		| the language for which to download the game (default: english)
-lowviolence			| download low violence depots when -app is used.
-pubfile \<#>			| the PublishedFileId to download. (Will automatically resolve to UGC id)
-username \<user>		| the username of the account to login to for restricted content.
-password \<pass>		| the password of the account to login to for restricted content.
-remember-password		| if set, remember the password for subsequent logins of this user. (Use -username <username> -remember-password as login credentials)
-dir \<installdir>		| the directory in which to place downloaded files.
-filelist \<file.txt>	| a list of files to download (from the manifest). Prefix file path with `regex:` if you want to match with regex.
-validate				| Include checksum verification of files already downloaded
-manifest-only			| downloads a human readable manifest for any depots that would be downloaded.
-cellid \<#>			| the overridden CellID of the content server to download from.
-max-servers \<#>		| maximum number of content servers to use. (default: 20).
-max-downloads \<#>		| maximum number of chunks to download concurrently. (default: 8).
-loginid \<#>			| a unique 32-bit integer Steam LogonID in decimal, required if running multiple instances of DepotDownloader concurrently.


## Frequently Asked Questions

### Why am I prompted to enter a 2-factor code every time I run the app?
Your 2-factor code authenticates a Steam session. You need to "remember" your session with `-remember-password` which persists the login key for your Steam session.

### Can I run DepotDownloader while an account is already connected to Steam?
Any connection to Steam will be closed if they share a LoginID. You can specify a different LoginID with `-loginid`.

### Why doesn't my password containing special characters work? Do I have to specify the password on the command line?
If you pass the `-password` parameter with a password that contains special characters, you will need to escape the command appropriately for the shell you are using. You do not have to include the `-password` parameter on the command line as long as you include a `-username`. You will be prompted to enter your password interactively.
