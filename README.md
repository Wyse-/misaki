# misaki
> An mkvmerge batch muxing helper.

This tool helps with batch multiplexing multiple files into multiple matroska containers, in an ordered and sequential way.
At the moment, misaki has only been tested under GNU/Linux.

## Description
Personally, I use it to remux anime series and assemble my own releases with the best audio, video and subtitle sources.

Here's a more concrete example, let's say you want to combine the following sources for a 24 episodes long series:
* Video source A
* Audio source B
* Audio source C
* Subtitle source D
* Subtitle source E
Obviously, you would use [MKVToolnix GUI](https://mkvtoolnix.download/). However, since you want to do the same thing for 24 episodes you would either have to:
l. Repeat the process manually with MKVToolnix GUI
l. Figure out how to batch the whole process with mkvmerge
l. Write your own script which relies on MKVToolnix GUI for the initial setup, and automates the whole process afterwards

This tool is my own option 3.

## Dependencies
* Python 3.7+
* MKVToolnix GUI

## Caveats
Make sure all the different source files are placed in their respective folder and named according to the order you want them to be muxed.
For instance, considering the previous example, you would want a setup which looks something like this:

<details>
    <summary>/home/user/series/video-source-A</summary>
l. Video A 01.mkv
l. Video A 02.mkv
l. Video A 03.mkv
l. Video A 04.mkv
l. Video A 05.mkv
l. Video A 06.mkv
l. Video A 07.mkv
l. Video A 08.mkv
l. Video A 09.mkv
l. Video A 10.mkv
l. Video A 11.mkv
l. Video A 12.mkv
l. Video A 13.mkv
l. Video A 14.mkv
l. Video A 15.mkv
l. Video A 16.mkv
l. Video A 17.mkv
l. Video A 18.mkv
l. Video A 19.mkv
l. Video A 20.mkv
l. Video A 21.mkv
l. Video A 22.mkv
l. Video A 23.mkv
l. Video A 24.mkv
</details>

<details>
    <summary>/home/user/series/audio-source-B</summary>
l. Audio B 01.flac
l. Audio B 02.flac
l. Audio B 03.flac
l. Audio B 04.flac
l. Audio B 05.flac
l. Audio B 06.flac
l. Audio B 07.flac
l. Audio B 08.flac
l. Audio B 09.flac
l. Audio B 10.flac
l. Audio B 11.flac
l. Audio B 12.flac
l. Audio B 13.flac
l. Audio B 14.flac
l. Audio B 15.flac
l. Audio B 16.flac
l. Audio B 17.flac
l. Audio B 18.flac
l. Audio B 19.flac
l. Audio B 20.flac
l. Audio B 21.flac
l. Audio B 22.flac
l. Audio B 23.flac
l. Audio B 24.flac
</details>

<details>
    <summary>/home/user/series/audio-source-C</summary>
l. Audio C 01.flac
l. Audio C 02.flac
l. Audio C 03.flac
l. Audio C 04.flac
l. Audio C 05.flac
l. Audio C 06.flac
l. Audio C 07.flac
l. Audio C 08.flac
l. Audio C 09.flac
l. Audio C 10.flac
l. Audio C 11.flac
l. Audio C 12.flac
l. Audio C 13.flac
l. Audio C 14.flac
l. Audio C 15.flac
l. Audio C 16.flac
l. Audio C 17.flac
l. Audio C 18.flac
l. Audio C 19.flac
l. Audio C 20.flac
l. Audio C 21.flac
l. Audio C 22.flac
l. Audio C 23.flac
l. Audio C 24.flac
</details>

<details>
    <summary>/home/user/series/subtitle-source-D</summary>
l. Subtitle D 01.ass
l. Subtitle D 02.ass
l. Subtitle D 03.ass
l. Subtitle D 04.ass
l. Subtitle D 05.ass
l. Subtitle D 06.ass
l. Subtitle D 07.ass
l. Subtitle D 08.ass
l. Subtitle D 09.ass
l. Subtitle D 10.ass
l. Subtitle D 11.ass
l. Subtitle D 12.ass
l. Subtitle D 13.ass
l. Subtitle D 14.ass
l. Subtitle D 15.ass
l. Subtitle D 16.ass
l. Subtitle D 17.ass
l. Subtitle D 18.ass
l. Subtitle D 19.ass
l. Subtitle D 20.ass
l. Subtitle D 21.ass
l. Subtitle D 22.ass
l. Subtitle D 23.ass
l. Subtitle D 24.ass
</details>

<details>
    <summary>/home/user/series/subtitle-source-E</summary>
l. Subtitle E 01.ass
l. Subtitle E 02.ass
l. Subtitle E 03.ass
l. Subtitle E 04.ass
l. Subtitle E 05.ass
l. Subtitle E 06.ass
l. Subtitle E 07.ass
l. Subtitle E 08.ass
l. Subtitle E 09.ass
l. Subtitle E 10.ass
l. Subtitle E 11.ass
l. Subtitle E 12.ass
l. Subtitle E 13.ass
l. Subtitle E 14.ass
l. Subtitle E 15.ass
l. Subtitle E 16.ass
l. Subtitle E 17.ass
l. Subtitle E 18.ass
l. Subtitle E 19.ass
l. Subtitle E 20.ass
l. Subtitle E 21.ass
l. Subtitle E 22.ass
l. Subtitle E 23.ass
l. Subtitle E 24.ass
</details>

Because of the way this script enumerates files in folders, make sure of the following:
* All sources which share the same extension (in the above example B and C, D and E) are in different folders
* There are no extraneous files in the sources' paths which share the same extension (e.g. an extra "Subtitle E 11.5.ass" file in the last folder)

Also, make sure to clear the video title in MKVToolNix GUI (under "Output-> File Title") since this is not supported and will cause trouble.

## How-to
l. Obtain a copy of misaki from this repository
l. (optional) Add misaki to /usr/bin: `sudo cp misaki /usr/bin`
l. Load all your sources under MKVToolNix GUI, as you normally would
l. Configure everything under MKVToolNix GUI, as you normally would
l. Make sure the "Destination file" path is set to a different folder from all the source files, as this will be used by mkvmerge to output your files
l. Get the mkvmerge command corresponding to your current MKVToolNix GUI configuration from "Multiplexer-> Show command line" (make sure "Escape arguments for" is set to "Linux/Unix")
l. Pass the command as parameter to misaki: `misaki "/usr/bin/mkvmerge [...]"`
l. If everything goes correctly misaki should output "Done!" and create a new "misaki.sh" file in your current working directory.
l. Execute "misaki.sh": `./misaki.sh`
l. The folder you set as "Destination file" in MKVToolNix GUI should start getting filled by files produced by the misaki generated bash script, "misaki.sh"
l. Wait for the batch muxing process to complete
l. Done!

If you have to correct something in your muxing process, just go back to step 4 and feed the corrected mkvmerge command to misaki, no need to manually mux multiple files twice.