<p align="center">
  <img width="120" height="120" src="https://github.com/turbosmurfen/spoton/blob/main/img/spoton_logo.png">
</p>

[![Github All Releases](https://img.shields.io/github/downloads/turbosmurfen/spoton/total.svg)]() [![CodeQL](https://github.com/turbosmurfen/spoton/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/turbosmurfen/spoton/actions/workflows/codeql-analysis.yml)

# Spoton - Spotify Now Playing for mIRC  

### Notice to everyone
If you are using Spoton 1.1.4 or earlier versions. Please update to version 1.1.5.   
Reason: Spoton in earlier versions keep adding more data to the memory each executing. 

# Get Started

* [FAQ](#faq)
* [Requirements](#requeirments)
* Installation Steps
    * [Downloading](#download)
    * [Installation](#install)
    * [Usage](#usage)
    * [mIRC Script Basic](#script)
    * [Errors](#errors)
* [Credits & licenses](#creds)

### Example image for mIRC 7.67  
![Image](https://github.com/turbosmurfen/spoton/blob/main/img/spoton_example.png)
  

# <a id="faq">Frequently Asked Questions</a>
**Q**: I can't find vx.x.x on download section, what do I do wrong?  
**A**: **X** stands for a number. I don't write down every new version.  
So go by number.  

**Q**: Does Spoton use Internet connection?  
**A**: No. Spoton is never using Internet connection.  

**Q**: Does Spoton require Spotify API-KEY?  
**A**: No. Spoton does not use Spotify API-KEYs. It works offline.  

**Q**: If Spoton doesn't use connection how does it work?  
**A**: It's reading Windows API calls from Spotify to detect artist - title.    
The tool is also using media controls that Spotify support.  



# <a id="reqeirments">Requeirments</a>

**Supported Operating System**: Windows  

**Visual C++ Redistributable 2015-2022 (x86)**  
  
**Supported Windows Edition**: Vista, 7, 8.1, 10, and 11.   
**Tested Windows Edition**: 7, 10, 11  
  
**Tested mIRC version**: 7.61 - 7.69  
**Tested Spotify Version**: 1.1.91

**Harddrive Space**: 17,4 KB.  

# <a id="download">Downloads</a>
1. Download `spoton_vx.x.x.zip` zip archive of Spoton in Assets in the [Releases](https://github.com/turbosmurfen/spoton/releases/latest) section.  

2. If you don't have the package `Visual C++ Redistributable 2015-2022 (x86)` installed.   
You need to Download this. You can click on the Microsoft site, here: [https://aka.ms/vs/17/release/vc_redist.x86.exe](https://aka.ms/vs/17/release/vc_redist.x86.exe).  

# <a id="install">Installation</a>

When you have downloaded everything that is needed for Spoton. Follow these steps.  
Step **3** is only needed if you want to verifcation the file hash.    

1. If you don't have `Visual C++ Redistributable 2015-2022 (x86)` Installed. 
Click on `vc_redist.x86.exe` and install the Redistributable, to be able to use Spoton.
 
2. Right Click on the archive which is named: spoton_vx.x.x.zip. And extract the archive.  

3. Open up powershell and **cd** to **Downloads\spoton_vx.x.x** folder. Run this command `Get-FileHash spoton.dll`. Then look if the sha256 checksum is correct from [Releases](https://github.com/turbosmurfen/spoton/releases/latest). If it's correct you should be fine. 

4. When finished you need to put the spoton.dll inside the mIRC folder (look at the steps below).  

### Steps for Windows Vista, 7 8.1, 10, 11:  

1. First open up mIRC. Now write this text and paste inside mIRC:   `//noop $sfile($mircdir)` and press enter.  
You are going to get a popup where to open a file.  

3. Copy `spoton.dll` and paste inside this popup window. **OR** save it where you have your other DLL files. 


# <a id="usage">How to use Spoton</a>


Use: $dll(pathtospoton\spoton.dll,**command**,)  

| Command       | output        | Description   |   
| --- | --- | --- |  
| version       | x.x.x         | Will output which version of spoton you use.  |  
| creator       | x - Made by   | Will output the creator of spoton.  |  
| status        | 0             | Spotify is not running. |
| status        | 1             | Spotify is paused. |
| status        | 2             | Spotify is playing advertisement. |
| status        | 3             | Spotify is playing a song.
| song          | artist - title | Will output artist and title. |

### Controlling Spotify from mIRC

Use: /dll pathtospoton\spoton.dll control **command**

| Command       |Description   |
| --- | --- | 
| play | Plays current song in Spotify (If paused). |
| rplay | Play the song from the beginning. |
| pause | Pauses Spotify (If playing). |
| next | Play next Spotify song. |
| prev | Play previous Spotify song. |
| volup | Increase the volume in Spotify. |
| voldown | Decrease the volume in Spotify. |
| volmute | Mute or Unmute Spotify volume. |

# <a id="script">mIRC Script Basic</a>
A script to make a Now Playing with Spoton.  
Please look so Spoton alias **snp** is not triggered by other scripts.  
  
To add this script to mIRC. Click on **Scripts Editor** or **ALT** + **R**, Select Remote. Click on File > New.  
Copy the code below and paste inside the new Script file and save. Now you can use /snp in any channel or private messages.

```mirc
alias snp {
  var %status $dll(spoton.dll,status,)
  if (%status == 1) echo -a Spotify is paused.
  elseif (%status == 2) echo -a Spotify is playing Advertisement.
  elseif (%status == 3) say Spotify » $dll(spoton.dll,song,)
  else echo -a Spotify is not running.
}
```


# <a id="errors">Common Errors</a>

**If you get this error**: `$dll: unable to open 'C:\Users\USERNAME\AppData\Roaming\mIRC\pathtospoton\spoton.dll`  
**This can show up for 2 reasons**:  

1. You have put the DLL-File somewhere else.
2. You need to install [Visual C++ Redistributable 2015-2022 (x86)](https://aka.ms/vs/17/release/vc_redist.x86.exe)  


**If you get this error**: `/echo: insufficient parameters`  
**This can show up for 2 reasons**:  

1. You are trying to announce when Spotify is paused, playing advertisement, or is turned off. (This is fixed in 1.1.4 or later of Spoton).
2. You are using version 1.1.1 of Spoton. You need to upgrade to at least 1.1.2 or later of Spoton.


**If you get this error**: `Artist - ??? ?????? ???`  
You are using an old version of Spoton. UTF8 is only supported in Spoton version 1.1.3 or later.  

# <a id="creds">License and Credits</a>

## Credits

I have learned more about making mIRC reading and writing for DLL-file from [Wikichip](https://en.wikichip.org/wiki/mirc/dynamic-link_library)  
Thanks to [Westor](https://github.com/westor7) for helping me out with fixing vulnerables and other things in the mIRC Beta Addon for Spoton.  

## Licenses

License from the Control of Spotify Media Player.  

```
Copyright 2010 Marcus Lönnberg

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

Code can be found here: 
https://github.com/marcuslonnberg/G930-Spotify-Controller
```
