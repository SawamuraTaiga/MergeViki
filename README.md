# MergeViki
A small bash script that combines youtube-dl and mkvmerge for downloading from Viki in a pretty mkv file

***
## What is MergeViki?

An application for easily download video content from Crunchyroll combining youtube-dl and mkvmerge. Build a fancy-mkv file with subtitles and fonts attached.

## Features

 - Choose between softsub or hardsub (no transcoding!)
 - Choose as you want to download: individual episode, several episodies or full series
 - Choose which quality you want to get (from 240p to 1080p)
 - On softsubbing, attach only one subtitle track or all subtitles track
 - On softsubbing, attach your own fonts to the mkv file
 - On softsubbing, warn if there are fonts missing
 - Spoof your user-agent and cookies file for logging with your account

## Usage

In this section, I will illustrate how to use the application with examples:

**Basic example (argument -i):**

Input URL using argument -i. Episode will be downloaded with max resolution in the current directory.

```sh
./mergeviki.sh -i URL_CRUNCH_HERE
```

**Playlist selection (append # character in input URL):**

For playlist selection, you must append the # character in input URL. After, use selection syntax:

- "N-M" for selecting inclusive range from N to M.
- "N" for simple selection.
- "," as separator for multiple selections.

Example #1. Select IDs items from 12 to 20.
```sh
./mergeviki.sh -i URL_PLAYLIST_CRUNCH_HERE#12-20
```

Example #2. Select ID item 5.
```sh
./mergeviki.sh -i URL_PLAYLIST_VIKI_HERE#5
```

Example #3. Select IDs items from 12 to 20 and also 2, 5, 23 to 30.
```sh
./mergeviki.sh -i URL_PLAYLIST_VIKI_HERE#12-20,2,5,23-30
```

**Output file name (argument -o):**

In this example, output file will renamed as "Sket Dance 01 [CRC32_HERE].mkv"

```sh
./mergeviki.sh -i URL_VIKI_HERE -o 'Sket Dance 01.mkv'
```

**CRC32 example (argument -x):**

In this example, CRC32 will be calculated and stored in the filename.

```sh
./mergeviki.sh -i URL_CRUNCH_HERE -x
```

**Preferred language (argument -s) + Only one language (argument --one):**

Using a preferred language, you set a default subtitle track in your mkv. In this example, set spanish subtitle track as preferred. If you append the --one argument, then esES subtitle track will merged exclusively.

```sh
./mergecrunch.sh -i URL_CRUNCH_HERE -x -f 720p --one -s esES
```

Language | Description
-------- | -----------
en     | Forces American English
fr     | Forces Français
it     | Forces Italiano
pt     | Forces Brazilian Português
de     | Forces Deutsch
ar     | Forces العربية
ru     | Forces Русский
jp     | Forces 日本語

**Hardsubbing switch (argument --hard):**

If you wish download a hardsub video instead of merging a soft subtitle track, you can append the --hard argument. Require -s argument and implies --one argument.

```sh
./mergeviki.sh -i URL_VIKI_HERE -x --hard -s en
```

## For manual install without docker: Dependencies

==Manual install is not recommended way. Only for Debian an derivates. Just for testing purposes==

Install youtube-dl, python3, fontconfig, mkvmerge and rhash

For getting this dependencies, execute the classic sudo apt-get install.

```sh
sudo apt-get install youtube-dl python3 fontconfig mkvtoolnix rhash
```

Note 1. Latest version of youtube-dl on [all-in-on binary](https://ytdl-org.github.io/youtube-dl/download.html)

Note 2. Latest version of mkvmerge on [custom Bunkus' repository](https://mkvtoolnix.download/downloads.html#debian)

Fontconfig is the engine to search for fonts in your system. If the applicationg warns you about missing fonts, create a folder in your home path called ~/.fonts and put in here the missing fonts

## DEPRECATED OPTIONS

**Premium account (argument -u and -p):**

In this example, I am logging in my premium account. **Deprecated by Crunchyroll’s new verifications.** The console will prompt for username's password.

```sh
./mergeviki.sh -i URL_VIKI_HERE -x -f 720p -s esES -o 'Sket Dance 01.mkv' -u sawamura
```

However, you may specific your password by command line.

```sh
./mergeviki.sh -i URL_VIKI_HERE -x -f 720p -s en -o 'Sket Dance 01.mkv' -u sawamura -p mysecretpassword
```

**Spoof location (argument -g):**

Similar to choose your preferred language, you can spoof your location in order to download videos from foreign locations. The following example shows a spoof location to Russia and preferred language to American Spanish. **Deprecated by Crunchyroll's new verifications.**

```sh
./mergeviki.sh -i URL_VIKI_HERE -x -f 720p -s en -g pt
```

## FEEDBACK, BUGS OR CONTRIBUTION

Open an issue in this repository or fork this

## LICENSE
GNU General Public License v2.0
