# csvEdit Esmeralda
```

	Dim stProgramAndVersion As String ="csvEdit Esmeralda, v2022-12-24-1"
	Dim stWebSite As String = "dbojan.github.io"


Program for editing csv/tsv files on windows.
BSD licence, free for use.

Installing: click on zip file, then on download on the right. Extract zip file, run. You can associate it with csv 
and tsv files.

Made in VB.net (profile4), using Sharpdevelop v.4.4

To remove row:
 -select one or more cells in the row you wish to remove
 -in menu go to 'modify/remove rows'
Same goes for column.

To select multiple cells/rows, use CTRL key. For adjacent use SHIFT. You can mix them.

You can also select full row(s) for deletion, and click on delete key, or use 'remove rows' option.

Program supports utf8 in content.

If not set, default delimiter is tab.
If tsv selected as format type, delimiter is tab.

-changes in v0.91b
 bugfixes
 add option to change delimiter. tab ; | , are recognized.

-changes in v2022-12-24-1
 -export to xml (Microsoft Office Excel 2003 SpreadsheetML XML). Libre Office Calc cannot open XML file properly, 
  if there is & in any cell. (Bug). Excel can open it.
 -copy
 -paste in selected cells
 -reworked saving part
 -using double buffering for faster scrolling

--
dbojan.github.io

Who is Esmeralda?
https://disneyheroines.fandom.com/wiki/Esmeralda
