---
layout: post
title: HEIC Woes
---
The new-ish [High Efficiency Image File Format](https://en.wikipedia.org/wiki/High_Efficiency_Image_File_Format) has a lot of advantages over older formats but compatibility is currently not one of them. 

Apple switched to .heic as the default image format of the iOS Camera app somewhere in 2017 and since then support has lagged. Even in Apple's own iCloud...

![iCloud HEIC Error]({{site.baseurl}}/images/blog_images/icloud_heic_error.png)

<div class="tenor-gif-embed" data-postid="9553858" data-share-method="host" data-width="100%" data-aspect-ratio="1.8253968253968251"><a href="https://tenor.com/view/jonahhill-frustrated-gif-9553858">Jonah Hill Frustrated GIF</a> from <a href="https://tenor.com/search/jonahhill-gifs">Jonahhill GIFs</a></div><script type="text/javascript" async src="https://tenor.com/embed.js"></script>

Windows requires you to [download additional codecs](https://www.microsoft.com/en-us/p/heif-image-extensions/9pmmsr1cgpwg?activetab=pivot:overviewtab) to view them locally.

Quite frankly, for me the advantages aren't currently worth the incompatibilities I've run into with HEIC. So I switched back to Camera.app saving images in JPG again: 
`Settings -> Camera -> Formats -> Most Compatible` 

But not before I unknowingly took a few hundred photos in HEIC. Conversion it is.

Google will return a slew of web-based image conversion sites that purport to support converting HEIC to JPG and I'm sure they work fine. But I don't want to trust my photo library to some random website. So I opted to write a PowerShell script to convert an entire directory of them locally. Most likely using the same tool those websites are using to convert them remotely anyway, ImageMagick. 

ImageMagick is an incredibly robust image manipulation tool used by web apps to convert, edit, and resize images on the fly. 

It also runs on just about anything so I was able to easily install it on Windows for use with my PowerShell script.

Check out the script here:

```powershell
[CmdletBinding()]
param (
    [parameter(mandatory = $true, position = 1)]
    [string]$convertFromDir
)

$files = Get-ChildItem -Path $convertFromDir -Filter *.heic

$convertedDir = New-Item -Name HEIC2JPG -Path $convertFromDir -ItemType directory

foreach($file in $files) {
    $newJPGFile = $file -Replace '\.heic$', '.jpg'
    magick $convertFromDir\$file $convertedDir\$newJPGFile
    Write-Host "Converted $file to HEIC2JPG\$newJPGFile"
}
```
<iframe src="https://ghbtns.com/github-btn.html?user=edewey&repo=Convert-HEIC2JPG&type=fork&count=true&size=large" frameborder="0" scrolling="0" width="170" height="30" title="GitHub"></iframe>

The script takes one argument, provide a directory path containing .heic files you'd like to convert to .jpg. A new directory called HEIC2JPG will be created within the supplied directory where your converted JPGs will be placed.

Make sure you download and install ImageMagick 7+ before you try running the script.

For example:
`./Convert-HEIC2JPG.ps1 c:\users\ethan\downloads\photos\`

![Example output]({{site.baseurl}}/images/blog_images/Convert-HEIC2JPG_usage_example.png)



