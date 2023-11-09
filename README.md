# NSIS
A ready-to-use NSIS with 8k strings support and ModernUI


When creating a Windows installer for OpenMS, the current default NSIS only supports string of length 1024.
This makes NSIS effectively unusable when fiddling with the user's $PATH during installation -- any Win10 with only a small number of programms installed will have a PATH larger than 1k.
There is a 'special-build' () available providing large-string support (up to 8k-length strings), but this is not what is by default installed on GitHub runners (which use Chocolatey as package manager).
See https://github.com/mkevenaar/chocolatey-packages/issues/221 for details.

We also make use of the UltraModernUI plugin, which needs extra installation as NSIS plugin.

This repo thus combines all three, as an ready-to-use archive (just untar NSIS.tar.gz and use it).

To update this project, run the following commands on a MinGW shell on Windows to create the final NSIS.tar.gz file:
```
  mkdir NSIS_OpenMS

  ## NSIS (default)
  curl --no-progress-meter -L -o nsis-3.zip  https://sourceforge.net/projects/nsis/files/NSIS%203/3.09/nsis-3.09.zip/download
  ## attention the ZIP file contains a subfolder 'nsis-3.09'
  unzip -o nsis-3.zip -d ./NSIS_OpenMS/

  # NSIS 8k (copy on top, since it's not a full NSIS and would result in : error '!include: could not find: "MUIEx.nsh"' if used alone)
  curl --no-progress-meter -L -o nsis-3-8k.zip  https://sourceforge.net/projects/nsis/files/NSIS%203/3.09/nsis-3.09-strlen_8192.zip/download
  unzip -o nsis-3-8k.zip -d ./NSIS_OpenMS/nsis-3.09

  # And finally the UltraModernUI plugin:
  curl --no-progress-meter -L -o UltraModernUI_2.0b6.zip  https://github.com/SuperPat45/UltraModernUI/releases/download/2.0b6/UltraModernUI_2.0b6.zip
  unzip -o UltraModernUI_2.0b6.zip -d ./NSIS_OpenMS/nsis-3.09
  
  tar -zcvf NSIS.tar.gz -C NSIS_OpenMS/nsis-3.09/ .

```