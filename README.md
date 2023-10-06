
# csv edit v2023-10-06-1
<code> <pre> 
beta

BSD licence, free for use.

Program for editing csv/tsv/m3u (playlist) files on Windows.
can also export to xml (Microsoft SpreadsheetML 2003) beta
suports command line conversion (see below)

import: csv, tsv, m3u, m3u8  xml (Microsoft SpreadsheetML 2003), folder with m3u files
export: csv, tsv, m3u, m3u8, xml (Microsoft SpreadsheetML 2003), folder with m3u files


## Installing: 
right click [here](https://github.com/dbojan/csvEdit_Esmeralda/raw/main/csvEdit.zip), select "Save Link As".
Select save location. Extract zip file, run. 
You can associate it with csv and tsv files.

Settings are in the settings.txt in format:
mpv=
d:/apps/mpv/mpv.exe

Edit if needed to change mpv and ffprobe location.
play.bat is started when single testing channels. Double click on cell or press f1


Made in VB.net (profile4), using Sharpdevelop v.4.4


## M3U:
M3U editing is beta, you might wanna backup your m3u files to another location first.


### Comments in m3u file:
You can add column to m3u table, change its title to Comment,  and add comments in that column
prefixed by #:

add new row, and rename its title to Comment.

your comments in that column have to prefixed with #:
#my comment in line 2
#my comment in line 3

It will be saved with the rest of the table in m3u file.
Dont add comment in the first row with #extm3u... line.
It will be ignored/not saved, per m3u specification on Wikipedia, unless it is part of the
1st cell/tag.


### XML:
First column in spreadsheet program (Calc or Excel) could be wide. Right click on the first 
column header, and select "Column Width". Set it to 2.



### Creating of (m3u) filelist
This will create list of files, with some additional columns.

You probably want to close open list in program first (file/close), or the program will 
ask you to save table first.

Creating of list by drag and drop multiple files:
drag and drop multiple (multimedia: mp3, avi, mp4 ...) files on the program, new m3u filelist 
will be created.
if 'caps lock' key is on program will ask you for group title. By default this is VOD-LOCAL
if 'scroll lock' key is on, regular file list will be created, with just path to filenames

To save an empty m3u list, set column names as you want, and add at least one row using
'Modify' menu. Click on 'File/Save As' or 'File/Save'.

You can also drop single folder with files inside on program.
If you drop single FILE on program, it will try to load it as a text file.


## Conversion notes:
m3u -> csv/tsv/xml: column names will be add as the top row, 
in the displayed/saved csv/tsv/xml files.

csv/tsv -> m3u: top row will be used as header name in m3u displayed/saved files.

all this will work, if the header title is not "Columnxx"

Automatic detection of tags in m3u should work :)









## Command line conversion:
start "" /wait csvEdit.exe import.file output.file. Example:

start "" /wait csvEdit.exe 2.m3u 2.csv

start "" /wait is to wait till the program completes conversion.




### sort by column using command line:
by specifying column name, and using _ , case insensitive:
convert a1.m3u8, sort by 'name' column and save as sortname_mynewlist.m3u. 
Destination filename has to start with 'sortname_' :
start "" /wait csvEdit.exe  a1.m3u8 sortname_mynewlist.m3u

convert a1.m3u8, sort by 8th column and save as sort8_test.m3u. 
Destination filename has to start with 'sort8_' :
start "" /wait csvEdit.exe  a1.m3u8 sort8_test.m3u



convert a1.m3u8 to sorturl_test.xml and sort by 'url' column, 
destination filename has to start with 'sorturl_' :
start "" /wait csvEdit.exe  a1.m3u8 sorturl_test.xml

Note that when converting back from xml to url, changing sort order makes no sense, 
cause it will lose column titles, which were moved to top row. You can convert between xml and csv
back and forth, if they were not previously converted from m3u.
But not from some other format to m3u with sorting.
You could, however, convert from some other format to m3u, and then sort m3u to new m3u file.

If string between sort and _ can be converted to int, then it will be used as column number. 
Otherwise, it will be use as column name. Column names only make sense on m3u lists.



### conversion of multiple files using command line:
if running from the csvedit folder, output files with format name.extension will be in csvedit folder:
convert m3u to csv
`    for %i in ("F:\tmp\*.m3u*") do start "" /wait csvEdit.exe "%i"  "%~nxi.tsv"   `

if running from the files folder, output files will be in the files folder, 
some files might be duplicated if intput extension is the same as the output extension:
`    for %i in (*.m3u*) do start "" /wait "F:\Desktop\csvedit-app\csvEdit.exe" "%i"  "%~nxi.tsv"   `


sort multiple files m3u, running from the csvedit folder:
`    for %i in ("F:\tmp\*.m3u*") do start "" /wait csvEdit.exe "%i"  "sortname_sorted-%~nxi.m3u"   `

sort multiple files m3u, running from the files folder:
```
    for %i in (*.m3u*) do start "" /wait "F:\Desktop\csvedit-app\csvEdit.exe" "%i"  "sortname_sorted-%~nxi.m3u"
```
### playlist to folder conversion:
can also convert m3u list to folder with single m3u files, folder has to exist first, 
or csv file is created:
you can use it create single vod m3u files, only name url, and group title are preserved):
mkdir  d:\media\vodfiles 
start "" /wait csvEdit.exe 1.m3u d:\media\vodfiles


if destination folder is named singles, each file will be saved to folder starting with the 
letter of the file:
start "" /wait csvEdit.exe 1.m3u d:\media\singles
abba in folder singles\a, bryan in folder singles\b ...

if destination folder is named series, each file will be saved to folder of the series:
start "" /wait csvEdit.exe 1.m3u d:\media\series
jack.s01e01,jack.s02e05 will be saved to folder series\jack, marty.s01e03,marty.s02e05 
to folder series\marty ...


you can use those together
start "" /wait csvEdit.exe 1.m3u d:\media\singles+series or start "" /wait csvEdit.exe 1.m3u d:\media\series+singles
files will be always saved to LETTER FIRST, then series: 
singles+series/j/jack/jack.s01e03.. or series+singles/j/jack/jack.s01e03


### folder to playlist conversion
you can also convert path (folder) to m3u list (for example to create mp3 files playlist):
url is path to file on the disk, name is filename without extension.
start "" /wait csvEdit.exe d:\media\music    1.m3u


## Editing all kind of tables:
To remove a row:
 -select one or more cells in the row you wish to remove
 -in menu go to 'modify/remove rows'
Same goes for column. Don't click on column title, unless you want to sort it.


To select multiple cells/rows, use CTRL key. For adjacent use SHIFT. You can mix them.

You can also select full row(s) for deletion, and click on delete key, or use 'remove rows' option.

Program supports utf8 in content.

If not set, default delimiter is tab.
If tsv selected as format type, delimiter is tab.
when converting m3u to csv/tsv default delimiter is tab.


### changes:
 -changes in 2023-08-06-1
 -changed file saving to File.WriteAllText from My.Computer.FileSystem.WriteAllText , 
  so text is saved in utf8, not utf8-bom
 -changed add row numbers to add channel numbers


-changes in v0.91b
 -bugfixes
 -add option to change delimiter. tab ; | , are recognized.

-changes in v2022-12-24-1
 -export to xml (Microsoft Office Excel 2003 SpreadsheetML XML). beware of & in cell value
 -copy
 -paste in selected cells
 -reworked saving

-changes in v2023-01-09-1
 -command line conversion
 -beta handling of m3u/m3u8 files. Make backup first.
 -m3u menu, for playing urls. edit play.bat in program folder first.
 -creating of (m3u) filelist by drag and drop multiple files

-changes v2023-08-06-1
 -minor changes

-changes in v2023-08-14-1
 -search (filter) added. to remove filter, either press ctrl and click on search,
  or enter empty search item and click on search, or use menu to remove markings.
 -You can disable sorting on search results using edit menu, or by holding SHIFT.
  (making rows non-visible in 10k rows is slow, so changing background color+sort was used instead)

-changes in v2023-08-15-1
 -fixed shennanigans with settings.txt. Program adds d:/apps/mpv/mpv.exe and d:/ffmpeg/ffprobe.exe 
  as defaults, if they exist. If settings.txt exist, it loads new values from it. 
 -If programs do not exist on neither locations, csvedit will warn you when you try to play url, 
  or check links.

-changes in v2023-08-16-1
 -to disable search sort, hold shift and click on search.
 -if you hold shift, when drag and drop new file on program window, 
  it will open in another (new) window
 -added 'open in new window' in 'file' menu
 
-changes in v2023-08-18-1
 -minor changes in text messages,

-changes in v2023-08-18-2
 -added timestamp to results in check links column.

-changes in v2023-08-27-1
 -added option to turn off 'http user agent' in edit menu, for m3u 'play' and 'check links' functions
 'mpv' is used for play, 'ffprobe' is used for testing links.
 -added verification for cell values (quotes and such), on save for m3u format.
 -replaced vbNewLine and vbCrLf and with Environment.NewLine in code

-changes in v2023-08-27-1
 -added option to disable 'verification for cell values (quotes and such), on save for m3u format', from edit menu.
  it is not recommended to disable this.
 -added default value for changing column name (and header text), it is the same as the current column name.

-changes in v2023-08-27-2
 -added option to disable 'double click cell to play URL in m3u list' in edit menu

-changes in v2023-08-27-3
 changed verification for #EXTINF: field.

-changes in v2023-09-15-1
 added option to replace special character when converting to and from xml (default: on) :
 `&lt; represents "<"; &gt; represents ">"; &amp; represents "&"; &apos; represents "'"; &quot; represents '"' `

-changes in 2023-10-04-1
 fixed sorting of results ascending, on the top of the table.
 added ability to sort table by column, when converting using command line.

-changes in 2023-10-06-1
 updated readme with info on multiple files conversion from command line.
 switched from using 'shift' and 'ctrl' to 'scroll lock' and 'caps lock' for drag and drop list creation.
 (cause shift and ctrl was already used.)

--
dbojan.github.io
