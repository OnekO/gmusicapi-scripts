Usage
=====

## General

``script.py [options] [input/output]``

During the first run of the scripts, you will be given a link to authorize the application with Google Music if necessary. Paste that link in your browser and click Allow. Enter the given code into the terminal prompt.

## Output pattern replacements

Pattern       | Field
--------------|--------
%artist%      | artist
%title%       | title
%track%       | tracknumber
%track2%      | tracknumber (zero padded)
%album%       | album
%date%        | date
%genre%       | genre
%albumartist% | albumartist
%disc%        | discnumber
%suggested%   | Filename suggested by Google


## gmsearch

```
gmsearch.py [options] [-f FILTER]...
```

Options                      | Description
-----------------------------|--------------
-h, --help                   | Show help message
-u USERNAME, --user USERNAME | Your Google username or e-mail address
-p PASSWORD, --pass PASSWORD | Your Google or app-specific password
-l, --log                    | Enable gmusicapi logging
-q, --quiet                  | Don't output status messages<br>With -l,--log will display gmusicapi warnings
-f, --filter                 | Filter Google songs by field:value pair (e.g. "artist:Muse")*<br>Values can be any valid [Python regex pattern](http://docs.python.org/2/library/re.html)<br>This option can be set multiple times
-a, -all                     | Songs must match all filter criteria<br>(Default: Songs can match any filter criteria)
-y, --yes                    | Display results without asking for confirmation


## gmdelete

```
gmdelete.py [options] [-f FILTER]...
```

Options                      | Description
-----------------------------|--------------
-h, --help                   | Show help message
-u USERNAME, --user USERNAME | Your Google username or e-mail address
-p PASSWORD, --pass PASSWORD | Your Google or app-specific password
-l, --log                    | Enable gmusicapi logging
-d, --dry-run                | Output list of songs that would be uploaded and excluded
-q, --quiet                  | Don't output status messages<br>With -l,--log will display gmusicapi warnings
-f, --filter                 | Filter Google songs by field:value pair (e.g. "artist:Muse")*<br>Values can be any valid [Python regex pattern](http://docs.python.org/2/library/re.html)<br>This option can be set multiple times
-a, -all                     | Songs must match all filter criteria<br>(Default: Songs can match any filter criteria)
-y, --yes                    | Display results without asking for confirmation


## gmsync

```
gmsync.py up [-e PATTERN]... [-f FILTER]... [options] [<input>]...
gmsync.py down [-f FILTER]... [options] [<output>]
gmsync.py [-e PATTERN]... [-f FILTER]... [options] [<input>]...
```

Supports **.mp3**, **.flac**, **.m4a**, **.ogg**  
_Non-MP3 files are transcoded with avconv to 320kbps MP3 for uploading_

Options                | Description
-----------------------|--------------
-h, --help             | Show help message
-c, --cred             | Specify oauth credential file name to use/create<br>(Default: "oauth")
-U ID --uploader-id ID | A unique id given as a MAC address (e.g. '00:11:22:33:AA:BB').<br>This should only be provided when the default does not work.
-l, --log              | Enable gmusicapi logging
-m, --match            | Enable scan and match
-d, --dry-run          | Output list of songs that would be uploaded and excluded
-q, --quiet            | Don't output status messages<br>With -l,--log will display gmusicapi warnings<br>With -d,--dry-run will display song list
-e, -exclude           | Exclude file paths matching a Python regex pattern<br>This option can be set multiple times
-f, --filter           | Filter Google songs (download) or local songs (upload) by field:pattern pair (e.g. "artist:Muse").*<br>Values can be any valid [Python regex pattern](http://docs.python.org/2/library/re.html)<br>This option can be set multiple times
-a, -all               | Songs must match all filter criteria<br>(Default: Songs can match any filter criteria)
input                  | Files, directories, or glob patterns to upload<br>Defaults to current directory if omitted
output                 | Output file or directory name which can include template patterns<br>Defaults to name suggested by Google Music in your current directory

\* *Filter fields can be any of artist, title, album, or albumartist/album_artist*

Commands | Description
---------|-------------
up       | Sync local songs to Google Music. This is the default behavior.
down     | Sync Google Music songs to local computer.

**Examples:**

```
gmsync.py -m "/path/to/music" "/other/path/to/music.mp3" "/another/path/to/*.flac"
gmsync.py up -e 'MyFolderName' "/path/to/music"
gmsync.py up -f 'artist:Muse' "/path/to/music" 
gmsync.py down -a -f 'artist:Muse' -f 'album:Black Holes' "/path/to/%artist%/%album%/%title%"
gmsync.py down -f 'artist:Muse|Modest Mouse' "/path/to/%artist%/%album%/%title%"
```


## gmupload

```
gmupload.py [-e PATTERN]... [-f FILTER]... [options] [<input>]...
```

Supports **.mp3**, **.flac**, **.m4a**, **.ogg**  
_Non-MP3 files are transcoded with avconv to 320kbps MP3 for uploading_

Options                | Description
-----------------------|--------------
-h, --help             | Show help message
-c, --cred             | Specify oauth credential file name to use/create<br>(Default: "oauth")
-U ID --uploader-id ID | A unique id given as a MAC address (e.g. '00:11:22:33:AA:BB').<br>This should only be provided when the default does not work.
-l, --log              | Enable gmusicapi logging
-m, --match            | Enable scan and match
-d, --dry-run          | Output list of songs that would be uploaded and excluded
-q, --quiet            | Don't output status messages<br>With -l,--log will display gmusicapi warnings<br>With -d,--dry-run will display song list
-e, -exclude           | Exclude file paths matching a Python regex pattern<br>This option can be set multiple times
-f, --filter           | Filter local songs by field:pattern pair (e.g. "artist:Muse").*<br>Values can be any valid [Python regex pattern](http://docs.python.org/2/library/re.html)<br>This option can be set multiple times
-a, -all               | Songs must match all filter criteria<br>(Default: Songs can match any filter criteria)
input                  | Files, directories, or glob patterns to upload<br>Defaults to current directory if omitted

\* *Filter fields can be any of artist, title, album, or albumartist/album_artist*

**Examples:**

```
gmupload.py "/path/to/music" "/other/path/to/music.mp3" "/another/path/to/*.flac"
gmupload.py -e 'MyFolderName' "/path/to/music"
gmupload.py -f 'artist:Muse' "/path/to/music" 
```


## gmdownload

```
gmdownload.py [-f FILTER]... [options] [<output>]
```

Options                | Description
-----------------------|--------------
-h, --help             | Show help message
-c, --cred             | Specify oauth credential file name to use/create<br>(Default: "oauth")
-U ID --uploader-id ID | A unique id given as a MAC address (e.g. '00:11:22:33:AA:BB').<br>This should only be provided when the default does not work.
-l, --log              | Enable gmusicapi logging
-d, --dry-run          | Output list of songs that would be uploaded and excluded
-q, --quiet            | Don't output status messages<br>With -l,--log will display gmusicapi warnings<br>With -d,--dry-run will display song list
-f, --filter           | Filter Google songs by field:value pair (e.g. "artist:Muse")*<br>Values can be any valid [Python regex pattern](http://docs.python.org/2/library/re.html)<br>This option can be set multiple times
-a, -all               | Songs must match all filter criteria<br>(Default: Songs can match any filter criteria)
output                 | Output file or directory name which can include template patterns<br>Defaults to name suggested by Google Music in your current directory

\* *Filter fields can be any of artist, title, album, or albumartist/album_artist*

**Examples:**

```
gmdownload.py -a -f 'artist:Muse' -f 'album:Black Holes' "/path/to/%artist%/%album%/%title%"
gmdownload.py -f 'artist:Muse|Modest Mouse' "/path/to/%artist%/%album%/%title%"
```

