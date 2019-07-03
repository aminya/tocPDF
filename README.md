# tocPDF
*by Amin Yahyaabadi*

Generates bookmarks from the table of contents already available at the beginning of pdf files.

 The plan is to automate the whole procedure. Until then here is the manual procedure:

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

### Step 3: Preparing the text of table of content

Open tocText (txt or csv) with a spreadsheet editor (MS Excel or Google Sheet) or using a text edit.

Edit the text such that each page number is at the beginning of a line, e.g.
```
1 Cover
2 Table of Contents
5 Chapter 1
6 +Subchapter1
7 ++Sub-Subchapter1
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
