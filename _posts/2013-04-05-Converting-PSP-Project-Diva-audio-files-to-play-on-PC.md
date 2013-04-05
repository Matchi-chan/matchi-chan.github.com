---
layout: post
author: Matchi-chan
title: 'Converting PSP Project Diva audio files to play on PC'
---

So today I found out how to find and listen to the audio files in Project Diva 2nd.

<!--break-->

And I'm going to tell you how to do it. This method should work for Extend too (not sure about Diva 1st)

1. Acquire an ISO somehow. I used the ISO I made of my UMD copy of 2nd#.
2. Open the ISO in an archive program that opens ISOs like 7zip.
3. Navigate to PSP_GAME\USRDIR\media\afs\, Diva2Sound.cpk is the file you want for this. (Diva2Data.cpk contains the data for the 3D models, which you'll want if you're planning to rig them for MMD)
4. Extract Diva2Sound into a folder somewhere. Now we need to unpack it.
5. For unpacking we use [utf_tab 0.7 b3](http://hcs64.com/files/utf_tab07b3.zip) from [here](http://hcs64.com/vgm_ripping.html) which is a commandline program.
6. Open cmd and cd to the directory where both cpk_unpack.exe and Diva2Sound.cpk are. (They need to be in the same folder, of course)
7. In commandline, simply type cpk_unpack.exe Diva2Sound.cpk and press enter, now wait for all the files to extract.
8. The files you're left with are .aix format, which I don't think you can directly play, so for me to be able to play them in foobar2000 we will need to convert them. We will be converting them to .adx which foobar can play with the [foo_adpcm](http://www.foobar2000.org/components/view/foo_adpcm) component.
9. Download [aix2adx.exe](http://wikiwiki.jp/koyayasen/?aix2adx.exe%20%A5%C0%A5%A6%A5%F3%A5%ED%A1%BC%A5%C9) and put it in the same folder as your .aix files (cpk_unpack should've made a Diva2Sound.cpk_unpacked folder) 
10. Use [this](https://gist.github.com/Matchi-chan/5319228] batch file I made to convert all the .aix files in batch. This takes about 5 minutes.
11. (Optional) then use move.bat on the above page to move all the adx files to their own folder (called adx)
12. Open the files in foobar2000 and you can now listen to them, and convert them to mp3. (Beware though, .adx is a lossy format, but converting to 320k mp3 doesn't degrade the quality too much.)

Filenames for what each audio file is should be somewhat explanatory, but here's a table I've made.

<table>
<thead>
<tr>
<th>Filename</th>
<th>What it is</th>
</tr>
</thead>
<tbody>
<tr>
<td>BGM_EDIT_00.aix - BGM_EDIT_08.aix</td>
<td>These are edit mode-only songs.</td>
</tr>
<tr>
<td>BGM_PV_01.aix - BGM_PV_66.aix</td>
<td>These are the actual songs you play in the rhythm game mode. Order of the songs seems to be random or the order that Sega decided they were going to be in the game (which would explain why World is Mine and Melt are 01 and 02)</td>
</tr>
<tr>
<td>BGM_GALLERY_00.aix, BGM_HOME_00.aix, BGM_HOME_01.aix, BGM_PLAYSTATUS_00.aix, BGM_ROOM_00.aix, BGM_SHOP_00.aix, BGM_STAFFROLL_00.aix, BGM_TITLE_00.aix</td>
<td>These are the game menu BGMs.</td>
</tr>
<tr>
<td>result_haku01.aix - result_saki06.aix</td>
<td>These are the little sound clips for each Vocaloid that play after you finish playing a song with them, and change depending on what rank you get or if you fail.</td>
</tr>
<tr>
<td>SEGA_006.aix - SEGA_020.aix</td>
<td>These seem to be sound clips of Miku, Rin and Len that could've been early unused versions of the result sounds that I found in my 2nd.</td>
</tr>
</table>

So, there you go, you now have access to the audio files of the Project Diva PSP games.