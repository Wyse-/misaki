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
1. Repeat the process manually with MKVToolnix GUI
1. Figure out how to batch the whole process with mkvmerge
1. Write your own script which relies on MKVToolnix GUI for the initial setup, and automates the whole process afterwards

This tool is my own option 3.

## Dependencies
* Python 3.7+
* MKVToolnix GUI

## Caveats
Make sure all the different source files are placed in their respective folder and named according to the order you want them to be muxed.
For instance, considering the previous example, you would want a setup which looks something like this:

<details>
    <summary>/home/user/series/video-source-A</summary>

1. Video A 01.mkv
2. Video A 02.mkv
3. Video A 03.mkv
4. Video A 04.mkv
5. Video A 05.mkv
6. Video A 06.mkv
7. Video A 07.mkv
8. Video A 08.mkv
9. Video A 09.mkv
10. Video A 10.mkv
11. Video A 11.mkv
12. Video A 12.mkv
13. Video A 13.mkv
14. Video A 14.mkv
15. Video A 15.mkv
16. Video A 16.mkv
17. Video A 17.mkv
18. Video A 18.mkv
19. Video A 19.mkv
20. Video A 20.mkv
21. Video A 21.mkv
22. Video A 22.mkv
23. Video A 23.mkv
24. Video A 24.mkv

</details>

<details>
    <summary>/home/user/series/audio-source-B</summary>

1. Audio B 01.flac
2. Audio B 02.flac
3. Audio B 03.flac
4. Audio B 04.flac
5. Audio B 05.flac
6. Audio B 06.flac
7. Audio B 07.flac
8. Audio B 08.flac
9. Audio B 09.flac
10. Audio B 10.flac
11. Audio B 11.flac
12. Audio B 12.flac
13. Audio B 13.flac
14. Audio B 14.flac
15. Audio B 15.flac
16. Audio B 16.flac
17. Audio B 17.flac
18. Audio B 18.flac
19. Audio B 19.flac
20. Audio B 20.flac
21. Audio B 21.flac
22. Audio B 22.flac
23. Audio B 23.flac
24. Audio B 24.flac

</details>

<details>
    <summary>/home/user/series/audio-source-C</summary>

1. Audio C 01.flac
2. Audio C 02.flac
3. Audio C 03.flac
4. Audio C 04.flac
5. Audio C 05.flac
6. Audio C 06.flac
7. Audio C 07.flac
8. Audio C 08.flac
9. Audio C 09.flac
10. Audio C 10.flac
11. Audio C 11.flac
12. Audio C 12.flac
13. Audio C 13.flac
14. Audio C 14.flac
15. Audio C 15.flac
16. Audio C 16.flac
17. Audio C 17.flac
18. Audio C 18.flac
19. Audio C 19.flac
20. Audio C 20.flac
21. Audio C 21.flac
22. Audio C 22.flac
23. Audio C 23.flac
24. Audio C 24.flac

</details>

<details>
    <summary>/home/user/series/subtitle-source-D</summary>

1. Subtitle D 01.ass
2. Subtitle D 02.ass
3. Subtitle D 03.ass
4. Subtitle D 04.ass
5. Subtitle D 05.ass
6. Subtitle D 06.ass
7. Subtitle D 07.ass
8. Subtitle D 08.ass
9. Subtitle D 09.ass
10. Subtitle D 10.ass
11. Subtitle D 11.ass
12. Subtitle D 12.ass
13. Subtitle D 13.ass
14. Subtitle D 14.ass
15. Subtitle D 15.ass
16. Subtitle D 16.ass
17. Subtitle D 17.ass
18. Subtitle D 18.ass
19. Subtitle D 19.ass
20. Subtitle D 20.ass
21. Subtitle D 21.ass
22. Subtitle D 22.ass
23. Subtitle D 23.ass
24. Subtitle D 24.ass

</details>

<details>
    <summary>/home/user/series/subtitle-source-E</summary>

1. Subtitle E 01.ass
2. Subtitle E 02.ass
3. Subtitle E 03.ass
4. Subtitle E 04.ass
5. Subtitle E 05.ass
6. Subtitle E 06.ass
7. Subtitle E 07.ass
8. Subtitle E 08.ass
9. Subtitle E 09.ass
10. Subtitle E 10.ass
11. Subtitle E 11.ass
12. Subtitle E 12.ass
13. Subtitle E 13.ass
14. Subtitle E 14.ass
15. Subtitle E 15.ass
16. Subtitle E 16.ass
17. Subtitle E 17.ass
18. Subtitle E 18.ass
19. Subtitle E 19.ass
20. Subtitle E 20.ass
21. Subtitle E 21.ass
22. Subtitle E 22.ass
23. Subtitle E 23.ass
24. Subtitle E 24.ass

</details>

Because of the way this script enumerates files in folders, make sure of the following:
* All sources which share the same extension (in the above example B and C, D and E) are in different folders
* There are no extraneous files in the sources' paths which share the same extension (e.g. an extra "Subtitle E 11.5.ass" file in the last folder)

Also, make sure to clear the video title in MKVToolNix GUI (under "Output-> File Title") since this is not supported and will cause trouble.

## How-to
1. Obtain a copy of misaki from this repository
2. (optional) Add misaki to /usr/bin: `sudo cp misaki /usr/bin`
3. Load all your sources under MKVToolNix GUI, as you normally would
4. Configure everything under MKVToolNix GUI, as you normally would
5. Make sure the "Destination file" path is set to a different folder from all the source files, as this will be used by mkvmerge to output your files
6. Get the mkvmerge command corresponding to your current MKVToolNix GUI configuration from "Multiplexer-> Show command line" (make sure "Escape arguments for" is set to "Linux/Unix")
7. Pass the command as parameter to misaki: `misaki "/usr/bin/mkvmerge [...]"`
8. If everything goes correctly misaki should output "Done!" and create a new "misaki.sh" file in your current working directory
9. (optional) If you need different, episode dependant delays for any of the tracks you will need to edit the "misaki.sh" file and manually add them
10. Execute "misaki.sh": `./misaki.sh`
12. The folder you set as "Destination file" in MKVToolNix GUI should start getting filled by files produced by the misaki generated bash script, "misaki.sh"
13. Wait for the batch muxing process to complete
14. Done!

If you have to correct something in your muxing process, just go back to step 4 and feed the corrected mkvmerge command to misaki, no need to manually mux multiple files twice.
