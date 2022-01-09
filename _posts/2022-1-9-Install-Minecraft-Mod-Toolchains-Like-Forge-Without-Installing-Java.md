---
layout: post
title: Install Minecraft Mod Toolchains like Forge Without Installing Java
---
I don’t yearn for the days where Java was required software on every computer. So, imagine my dismay when it was suggested that I install Java just to install tools like [Forge](https://files.minecraftforge.net/net/minecraftforge/forge/) or [Fabric](https://fabricmc.net/) for Minecraft. Fear not, as there’s an easy way out of this mess. Minecraft comes with a Java Runtime built-in, which you can use to run Forge or Fabric’s JAR installers. It’s located in the Minecraft Launcher’s install directory under runtime -> java-runtime-beta -> windows-x64 -> java-runtime-beta -> bin -> java.exe. 
Simply open a PowerShell terminal in this directory and run 

`./java.exe -jar <path-to-installer-jar-file>`

Short, sweet, and bloat free. 







