# tocPDF
*by Amin Yahyaabadi*

Generates bookmarks from the table of contents already available at the beginning of pdf files.

 The plan is to automate the whole procedure (https://github.com/aminya/tocPDF#automated).


 Until then here is the manual procedure:
## Manual:
### Step 1:  Extraction of toc pages from PDF:
Use Chrome or software that you already have to extract the pages that contain the table of contents.

Tutorial for extracting pages using Chrome
https://www.techadvisor.co.uk/how-to/software/how-extract-pages-from-pdf-3679232/

We refer to this file as tocPDF.

### Step 2: Extract table of content text
Here we extract the text from tocPDF.

Even if your pdf file is searchable, usually when you copy the text the result is not in proper format (like a table).

Preferred Methods:

* ####  Tabula technology
for searchable PDF only -  https://tabula.technology/

	* Download and run the software
	* Select table of content and do this for each page
	* Hit preview and export extracted data
	* Export to csv format

* #### Using OCR.space
for both scanned and searchable PDF -  https://ocr.space/

	* Upload tocPDF
	* Check "Do receipt scanning and/or table recognition" option
	* Use "Just extract text and show overlay (fastest option)" option.
	* download or copy paste the generated text.


We refer to generated text as tocText.


## For the following steps instead you can check my other repository which does a similar thing but with a GUI 
https://github.com/aminya/pdf-bookmark-English

### Step 3: Preparing the text of table of content

Open tocText (txt or csv) with a spreadsheet editor (MS Excel or Google Sheet) or using a text edit.

Edit the text such that each page number is at the beginning of a line, e.g.
```
1 Cover
2 Table of Contents
5 Chapter 1
+6 Subchapter1
++7 Sub-Subchapter1
25 Chapter 2
```
Don't forget to add the offset to page number (usually the page numbers in pdf have an offset compared to printed document).

### Step 4: Download k2pdfoptdoes:
http://willus.com/k2pdfopt/download/

### Step 5: (only for Windows) Disabling the GUI :

Disabling the GUI using this tutorial
http://willus.com/k2pdfopt/help/nogui.shtml

Then drag original pdf file into your shortcut.


### Step 6: Run the command:
#### Windows:
copy toc.txt and source pdf file in the folder of your shortcut for convenience.

Copy paste the following command in the terminal and press enter.
```
-mode copy -n -toclist toc.txt srcfile.pdf -o outfile.pdf
```
Press enter again to start bookmarking.

#### OSX or Linux:
```
k2pdfopt -mode copy -n -toclist toc.txt srcfile.pdf -o outfile.pdf
```


## Automated:

For now, I plan to start using available software (e.g. k2pdfoptdoes), and then later make the functionality Julia native (when [PDFIO.jl](https://github.com/sambitdash/PDFIO.jl/issues/66) adds pdf write capability).

Current algorithm plan:
* The user will provide page numbers that contain the table of content.
* Those pages are read from pdf by Julia
* Julia will extract these pages (here user can be called to do the cropping of the borders)
* Julia will send the extracted pages to https://ocr.space/ to do OCR, and then it gets the text from the table of content (using the [available APIs (Python, C++, etc)](https://ocr.space/ocrapi))
* Julia will edit the received text to make it a specified format. (here user can be called to do a review). The prepared text file will be saved.
* A software is called from Julia (e.g. k2pdfoptdoes from the command line). That software will read the original pdf file and text file and will generate the bookmarks for the pdf and will save it.


* Also, if the pdf file is searchable, Julia can check the fonts in the whole pdf, and for example, get the text of Bold fonts. ([Infix PDF Editor](https://www.iceni.com/blog/how-to-bookmark-pages-in-a-pdf/) does this.) Manual font providing by the user also can be done ( The expensive [Evermap AutoBookmark ](https://www.evermap.com/autobookmark.asp) plugin for Adobe and [Nitro PDF](https://www.gonitro.com/) do this.)


## Other Manual Methods:
#### Other method using Jpdfbookmark
https://sourceforge.net/projects/jpdfbookmarks/

from https://ebooks.stackexchange.com/a/7763/12921

    Prepare the tocText file such that

    Chapter 1. The Beginning/23
        Para 1.1 Child of The Beginning/25,FitWidth,96
            Para 1.1.1 Child of Child of The Beginning/26,FitHeight,43
    Chapter 2. The Continue/30,TopLeft,120,42
        Para 2.1 Child of The Beginning/32,FitPage

    You can OCR the TOC and use regex to fix it.

    Load that TOC

    Expand all bookmarks (Ctrl + E), select all of them, then go to Tools > Apply Page Offset

    Enter the first pages that outmatch the page number in the TOC

Your can read its manual (http://jpdfbookmarks.altervista.org/InsertBookmarks.html#1_3_1) or watch a quick video tutorial (https://youtu.be/7DUkvH7_wII?t=30). It has command line mode and can work on Linux, Mac.

#### Other Methods for step 2:

* Tesseract OCR:
	https://github.com/tesseract-ocr/tesseract

	Three is good tutorial for Extracting Table Data From PDFs with Tesseract OCR:
	https://web.archive.org/web/20141022033241/http://craiget.com/extracting-table-data-from-pdfs-with-ocr/

* Using OnlineOCR.net - Free up to a limit:
https://www.onlineocr.net/

	* Register in the website (to remove page number limitation) and login
	* Select txt file option, Upload tocPDF, Convert your file

* A related Stack overflow question:
https://stackoverflow.com/questions/6173439/can-ocr-software-reliably-read-values-from-a-table

#### References:

https://www.willus.com/k2pdfopt/help/k2menu.shtml

https://www.willus.com/k2pdfopt/help/options.shtml


https://ebooks.stackexchange.com/questions/107/how-to-create-clickable-table-of-contents-in-a-pdf
