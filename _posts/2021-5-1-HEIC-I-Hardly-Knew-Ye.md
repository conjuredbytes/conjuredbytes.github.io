---
layout: post
title: HEIC I Hardly Knew Ye
---
I’d be amiss if I told you I knew exactly how the HEIC image format worked. It’s higher quality with a smaller file size or something, but I digress. I’m sure it has its benefits, but for me, your average guy who just sends you a picture of his dog every now and then, I don’t really see them. I’m also not a guy who gets pedantic about what file format he stores his dog pictures in; I don’t think about it. And that’s where HEIC crossed me: it made me think about it. 

You see, the iPhone camera app defaults to saving images and videos in HEIC formats nowadays, which isn’t that big of a deal until you try and do something complex, like, I don’t know, try and upload an HEIC image you took on your iPhone to iCloud on the web. 

![iCloud HEIC Error]({{site.baseurl}}/images/blog_images/icloud_heic_error.png)

This kind of pissed me off as I was trying to upload a few hundred photos I pulled off an old iPhone to iCloud. This process turned out to be kind of a headache, which, to be fair, is more a failing of Apple than HEIC, but it was caught in the crossfire anyway. Ragging on Apple aside, Windows 10 also requires you install some codecs from the Microsoft Store for HEIC photos and videos to properly integrate with the operating system. 

For future reference, if you want to avoid this headache and just bypass HEIC until it’s garnered more software support you can change the tell your iPhone to just save in JPG and MOV again by going to Settings -> Camera -> Formats -> Most Compatible. But, if you’re like me, and have already taken an annoying number of photos that were saved in HEIC format, I have a PowerShell script for you. 

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

You’ll need to have ImageMagick installed and in your path to do the conversions. The script takes one argument: a directory path containing the .heic files you’d like to convert. Once run the script will find all .heic files in the provided directory, convert them to JPG with ImageMagick, and put them in an “HEIC2JPG” folder. 

For example:
`./Convert-HEIC2JPG.ps1 c:\users\ethan\downloads\photos\`

Hopefully, this saves you some headache.



