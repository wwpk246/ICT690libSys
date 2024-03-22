**Searching with grep**

We have available some powerful utilities and programs to process, manipulate, and analyze text files. In this section, we will focus on the grep utility, which offers some advanced methods for searching the contents of text files.

Grep

The grep command is one of my most often used commands. The purpose of grep is to "print lines that match patterns" (see man grep). In other words, it searches text, and it's super powerful.

grep works line by line. So when we use it to search a file for a string of text, it will return the whole line that matches the string. This line by line idea is part of the history of Unix-like operating systems, and it's important to remember that most utilities and programs that we use on the commandline are line oriented.

"A string is any series of characters that are interpreted literally by a script. For example, 'hello world' and 'LKJH019283' are both examples of strings." -- Computer Hope. More generally, it's a type of data structure.

To visualize how grep works, let's consider a file called operating-systems.csv with content as seen below:

OS, License, Year
Chrome OS, Proprietary, 2009
FreeBSD, BSD, 1993
Linux, GPL, 1991
macOS, Proprietary, 2001
Windows NT, Proprietary, 1993
Android, Apache, 2008
We can use grep to search for anything in that file. Let's start with a search for the string Chrome. Notice that even though the string Chrome only appears once, and in one part of a line, grep returns the entire line.

Command:

grep "Chrome" operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
Case Matching
Be aware that, by default, grep is case-sensitive, which means a search for the string chrome, with a lower case c, would return no results. However, many Linux command line utilities can have their functionality extended through command line options. grep has an -i option that can be used to to ignore the case of the search string. In the following examples, grep returns nothing in the first search since we do not capitalize the string chrome. However, adding the -i option results in success since grep is instructed to ignore case:

Command:

grep "chrome" operating-systems.csv
Output:

None.

Command:

grep -i "chrome" operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
Invert Matching
grep can do inverse searching. That is, we can search for lines that do not match our string using the -v option. Options can often be combined for additional functionality. We can combine -v to inverse search with -i to ignore the case. In the following example, we search for all lines that do not contain the string chrome:

Command:

grep -vi "chrome" operating-systems.csv
Output:

FreeBSD, BSD, 1993
Linux, GPL, 1991
iOS, Proprietary, 2007
macOS, Proprietary, 2001
Windows NT, Proprietary, 1993
Android, Apache, 2008
Regular Expressions
Sometimes data files, like spreadsheets, contain header columns in the first row. We can use grep to remove the first line of a file by inverting our search and selecting all lines not matching "OS" at the start of a line. Here the carat key ^ is a regex indicating the start of a line. Again, this grep command returns all lines that do not match the string os at the start of a line, ignoring case:

Command:

grep -vi "^os" operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
FreeBSD, BSD, 1993
Linux, GPL, 1991
iOS, Proprietary, 2007
macOS, Proprietary, 2001
Windows NT, Proprietary, 1993
Android, Apache, 2008
Alternatively, since we know that the string Year comes at the end of the first line, we can use grep to invert search for that. Here the dollar sign key $ is a regex indicating the end of a line. Like the above, this grep command returns all lines that do not match the string year at the end of a line, ignoring case. The result, in this specific instance, is exactly the same as the last command:

Command:

grep -vi "year$" operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
FreeBSD, BSD, 1993
Linux, GPL, 1991
iOS, Proprietary, 2007
macOS, Proprietary, 2001
Windows NT, Proprietary, 1993
Android, Apache, 2008
The man grep page lists other options, but a couple of other good ones include:

Count Matches
Get a count of the matching lines with the -c option. For example, let's get a total count of rows in our file excluding the header by adding the -c option:

grep -vic "year$" operating-systems.csv
Alternate Matching
We separate the strings with a vertical bar | (the infix operator) to match any string on either side. This is similar to a Boolean OR search. Since there's at least one match in the following string, there is at least one result.

Here is an example where only one string returns a true value since the file contains bsd but not atari:

Command:

grep -Ei "(bsd|atari)" operating-systems.csv
Output:

FreeBSD, BSD, 1993
Here's an example where both strings evaluate to true:

Command:

grep -Ei "(bsd|gpl)" operating-systems.csv
Output:

FreeBSD, BSD, 1993
Linux, GPL, 1991
Whole Word Matching
By default, grep will return results where the string appears within a larger word, like OS in macOS.

Command:

grep -i "os" operating-systems.csv
Output:

OS, License, Year
Chrome OS, Proprietary, 2009
iOS, Proprietary, 2007
macOS, Proprietary, 2001
However, we might want to limit results so that we only return results where OS is a complete word. To do that, we can surround the string with special characters:

Command:

grep -i "\<os\>" operating-systems.csv
Output:

OS, License, Year
Chrome OS, Proprietary, 2009
Sometimes I find it hard to remember the backslash and angle bracket combinations because they're too much alike HTML syntax but not exactly like HTML syntax. Fortunately, grep has a -w option to match whole words:

Command:

grep -wi "os" operating-systems.csv
Output:

OS, License, Year
Chrome OS, Proprietary, 2009
Context Matches
Sometimes we want the context for a result; that is, we might want to print lines that surround our matches. For example, to print the matching line plus the two lines after the matching line using the -A NUM option, where NUM equals the number of lines to return after the matching line:

Command:

grep -i "linux" -A2 operating-systems.csv
Output:

Linux, GPL, 1991
macOS, Proprietary, 2001
Windows NT, Proprietary, 1993
Or, print the matching line plus the two lines before the matching line using the -B NUM option:

Command

grep -i "linux" -B2 operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
FreeBSD, BSD, 1993
Linux, GPL, 1991
We can combine many of the variations. Here I search for the whole word BSD, case insensitive, and print the line before and the line after the match:

Command:

grep -iw -C1 "bsd" operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
FreeBSD, BSD, 1993
Linux, GPL, 1991
Halt Matching
We can use another option to stop returning results after some number of hits. Here I use grep to return a search for the string "proprietary" and stop after the first hit:

Command:

grep -i -m1 "proprietary" operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
Returning Line Numbers
We can add the -n option to instruct grep to tell us the line number for each hit. Below we see that the string "proprietary" is found on lines 2, 5, and 6.

Command:

grep -in "proprietary" operating-systems.csv
Output:

2:Chrome OS, Proprietary, 2009
5:macOS, Proprietary, 2001
6:Windows NT, Proprietary, 1993
Character Class Matching
We can use grep to search for patterns in strings instead of literal words. Here we use what's called character classes and repetition to search for five letter words that contain any English character a through z:

Command:

grep -Eiw "[a-z]{5}" operating-systems.csv
Output:

Linux, GPL, 1991
macOS, Proprietary, 2001
Or four letter numbers, which highlights the years:

Command:

grep -Eiw "[0-9]{4}" operating-systems.csv
Output:

Chrome OS, Proprietary, 2009
FreeBSD, BSD, 1993
Linux, GPL, 1991
macOS, Proprietary, 2001
Windows NT, Proprietary, 1993
Android, Apache, 2008
grep can also search for words that begin with some letter and end with some letter and with a specified number of letters between. Here we search for words that start with m, end with s, and have three letters in the middle:

Command:

grep -Eiw "m.{3}s" operating-systems.csv
Output:

macOS, Proprietary, 2001
Practice
Let's use the grep command to investigate bibliographic data. Our task is to:

Search Scopus.
Download a BibTeX file from Scopus as a .bib file.
Use the grep command to search the downloaded BibTeX file, which should be named scopus.bib.
Download Data
I'm using Scopus data in this example, but other bibliographic data can be downloaded from other databases.

From your university's website, find Scopus.
In Scopus, perform a search.
Select the documents you want to download.
Click on the Export button.
Click on BibTeX under the listed file types.
Select all Citation Information and Bibliographic Information. Select more in interested.
Click on Export.
The file should be saved to your Downloads folder and titled scopus.bib.

Upload to gcloud
To upload to gcloud, you use a similar command as the gcloud compute ssh command that you use to connect to your servers.

However, there are some differences. The gcloud copy command uses scp instead of ssh and then specifies the local file to transfer and the remote location. The following command copies the local file titled file_name to the remote server. Simply replace the file name, server, zone, and project names with those specific to your virtual instances.

gcloud compute scp file_name "server_name":~/ --zone "zone_name" --project "project_name"
There are other ways to transfer files to the virtual instance from your local computer, but they raise some complications. If interested, see Transfer files to Linux VMs.

Investigate
Now that the file is uploaded, the first task is to to get an understanding of the structure of the data. BibTeX (.bib) files are structured files that contain bibliographic data. It's important to understand how files are structured if we want to search them efficiently.

The scopus.bib file begins with information about the source (Scopus) of the records and the date the records were exported. These two lines and the empty line after them can be safely deleted or ignored.

Each bibliographic record in the file begins with an entry type (or document type) preceded by an at @ sign. Example entry types include: article, book, booklet, conference, and more. There is a opening curly brace after the entry or document type. These curly braces mark the beginning and ending of each record.

The cite key follows the opening curly brace. The cite key is an identifier that often refers to the author's name and includes publication date information. For example, a cite key might look as follows and would stand for the author Budd and the date 2020-11-23.

Budd20201123
The rows below the entry type contain the metadata for the record. Each row begins with a tag or field name followed by an equal sign, which is then followed by the values or content for that tag. For example, there's an author tag, an equal sign, and then a list of authors. There is a standard list of BibTeX fields. Example fields include: author, doi, publisher, title, journal, year, and more. The fields are standardized because some programs use BibTeX records to manage and generate bibliographies, in-text citations, footnotes, etc..

The content of each field is enclosed in additional curly braces. Each line ends with a comma, except for the last line. The record ends with a closing curly brace.

Document Types
We can use grep to examine the types of documents the records point to. In the following command, I use the carat key ^, which is a regular expression to signify the start of a line, to search for lines beginning with the at @ symbol. The following grep command therefore means: return all lines that begin with the at @ symbol:

grep "^@" scopus.bib
The results show, for this particular data, that I have BOOK and ARTICLE entry types. The data I'm using does not contain many records, but if it contained thousands or more, then it would be helpful to filter these results.

Thus, below I use the -E option to extend grep's regular expression engine. I use the (A|B) to tell grep to search for letters after the at sign @ that start with either A or B, for ARTICLE or BOOK. Then I use regular expression character class matching with [A-Z]* to match any letters after the initial A or B characters. The -i option turns off case sensitivity, and the -o option returns only matching results from the lines. I pipe the output of the grep command to the sort command to sort the results alphabetically:

grep -Eio "^@(A|B)[A-Z]*" scopus.bib | sort
Tip: Without using the sort command, the grep command returns the results in the order it finds them. To see this, run the above command with and without piping to the sort command to examine how the output changes.

Now let's get a frequency of the document types. Here I pipe | the output from the grep command to the sort command, in order to sort the output alphabetically. Then I pipe the output from the sort command to the uniq command. The uniq command will deduplicate the results, and the -c option will count the number of duplicates. As a result, it will provide an overall count of the document or entry types we searched.

grep -Eio "^@(A|B)[A-Z]*" scopus.bib | sort | uniq -c
Journal Titles
We can parse the data for other information. For example, we can get a list of journal titles by querying for the journal tag:

grep "journal" scopus.bib
Even though that works, the data contains the word Journal in the name of some journals. If we were searching thousands or more records, we might want to construct a more unique grep search.

To rectify this, we can modify our grep search in two ways. First, the rows of data fields begin with a tab character. The regular expression for the tab character is \t. Therefore, we can search the file using this expression with the -P option:

grep -P "\tjournal" scopus.bib
Second, we can simply add more unique terms to our grep search. Since each tag includes a space, an equal sign, followed by another space, we can use that in our grep query:

grep "journal =" scopus.bib
Using either method above, we can extract the journal title information. Here I use two new commands, cut and sed. The cut command takes the results of the grep command, removes the first column based on the comma as the column delimiter. In the first sed command, I remove the space and opening curly brace and replace it with nothing. In the second sed command, I remove the closing curly brace and the comma and replace it with nothing. The result is list of only the journal titles without any extraneous characters. I then pipe the output to the sort command, which sorts the list alphabetically, to the uniq -c command, which deduplicates and counts the results, and again to the sort command, which sorts numerically, since the first character is a number:

grep "journal =" scopus.bib | cut -d"=" -f2 | \
    sed 's/ {//' | sed 's/},//' | \
    sort | uniq -c | sort
Total Citations
There are other things we can do if we want to learn more powerful technologies. While I will not cover awk, I do want to introduce it to you. With the awk command, based on the BibTeX tag that includes citation counts at the time of the download (e.g., note = {Cited by: 2}), we can extract the number from that field for each record and sum the total citations for the records in the file:

 grep -o "Cited by: [0-9]*" scopus.bib | \
    awk -F":" \
    'BEGIN { printf "Total Citations: "} \
    { sum += $2; } \
    END { print sum }'
In the above command, we use the pipe operator to connect a series of commands to each other:

use grep to search for the string "Cited by: " and to include any number of digits
use awk to use the colon as the column or field delimiter
use the awk BEGIN statement to print the words "Total Citations: "
instruct awk to sum the second column, which is the citation numbers
use the awk END statement to print the sum.
If you want to learn more about sed and awk, please see my text processing chapter for my Linux Systems Administration. There are also many tutorials on the web.

Conclusion
grep is very powerful, and there are more options listed in its man page.

The Linux (and other Unix-like OSes) command line offers a lot of utilities to examine data. It's fun to learn and practice these. Despite this, you do not have to become an advanced grep user. For most cases, simple grep searches work well.

There are many grep tutorials on the web if you want to see other examples.



-------------------------------------------------------------------------

# Grep examples

Grep command is used to find information within the document or text.  
Use grep to search for "words":

- to -i by ignoring case sensitivity,
- to -vi remove certain "words" from the results,
- to -vi "^word" remove the word from the results,
- to -vic "count" the number of times the word is in the results,
- to -i -m1 "locate" use to locate the first mention of the word,
- to -Ei "(article|program)" find either word within the text

## Overall grep command for a document or file =

```
grep "^@" scopus.bib
```

Results in:

```
@ARTICLE{Jia20232668,
@CONFERENCE{Sasaki2019563,
@CONFERENCE{Jothi Mary Jenifer20231141,
@ARTICLE{Balasubramanian2023297,
@ARTICLE{Rahman2020932,
```

## Grep with ignoring case sensitive =

```
grep -i "journal" scopus.bib
```

Results in:

```
journal = {IEEE Transactions on Network and Service Management},
journal = {2019 IEEE 8th Global Conference on Consumer Electronics, GCCE 2019},
journal = {2023 3rd International Conference on Advance Computing and Innovative Technologies in Engineering, ICACITE 2023},
journal = {Lecture Notes in Networks and Systems},
journal = {Indonesian Journal of Electrical Engineering and Computer Science},
journal = {2017 14th International Conference The Experience of Designing and Application of CAD Systems in Microelectronics, CADSM 2017 - Proceedings},
journal = {ASEE Annual Conference and Exposition, Conference Proceedings},
```

## grep with removal of documents labeled "journal" =

```
grep -vi "journal" scopus.bib
```

Results in:

```
Scopus
EXPORT DATE: 17 February 2024

@ARTICLE{Jia20232668,
	author = {Jia, Zhixuan and Fan, Yushun and Zhang, Jia},
	title = {MGMASR: Multi-Graph and Multi-Aspect Neural Network for Service Recommendation in Internet of Services},
	year = {2023},
	volume = {20},
	number = {3},
	pages = {2668 – 2681},
	doi = {10.1109/TNSM.2023.3239847},
	url = {https://www.scopus.com/inward/record.uri?eid=2-s2.0-85148468240&doi=10.1109%2fTNSM.2023.3239847&partnerID=40&md5=8698f61c7c6574d62b4e99c2c9926a05},
	affiliations = {Tsinghua University, Beijing National Research Center for Information Science and Technology, Department of Automation, Beijing, 100084, China; Southern Methodist University, Department of Computer Science, Dallas, 75205, TX, United States},
	correspondence_address = {Y. Fan; Tsinghua University, Beijing National Research Center for Information Science and Technology, Department of Automation, Beijing, 100084, China; email: fanyus@tsinghua.edu.cn},
	publisher = {Institute of Electrical and Electronics Engineers Inc.},
	issn = {19324537},
	language = {English},
	abbrev_source_title = {IEEE Trans. Netw. Serv. Manage.},
	type = {Article},
	publication_stage = {Final},
	source = {Scopus},
	note = {Cited by: 0}
}

@CONFERENCE{Sasaki2019563,
	author = {Sasaki, Yuji and Fukui, Masanori and Hirashima, Tsukasa},
	title = {Development of iOS software n-queens problem for education and its application for promotion of computational thinking},
	year = {2019},
	pages = {563 – 565},
	doi = {10.1109/GCCE46687.2019.9015331},
	url = {https://www.scopus.com/inward/record.uri?eid=2-s2.0-85081986375&doi=10.1109%2fGCCE46687.2019.9015331&partnerID=40&md5=c28f23af181a9bce8703a14ad5de5aa1},_
```

## Grep while removing the word journal from the results =

```
grep -vi "^journal" scopus.bib
```

Resuts in:

```
Scopus
EXPORT DATE: 17 February 2024

@ARTICLE{Jia20232668,
	author = {Jia, Zhixuan and Fan, Yushun and Zhang, Jia},
	title = {MGMASR: Multi-Graph and Multi-Aspect Neural Network for Service Recommendation in Internet of Services},
	year = {2023},
	journal = {IEEE Transactions on Network and Service Management},
	volume = {20},
	number = {3},
	pages = {2668 – 2681},
	doi = {10.1109/TNSM.2023.3239847},
	url = {https://www.scopus.com/inward/record.uri?eid=2-s2.0-85148468240&doi=10.1109%2fTNSM.2023.3239847&partnerID=40&md5=8698f61c7c6574d62b4e99c2c9926a05},
	affiliations = {Tsinghua University, Beijing National Research Center for Information Science and Technology, Department of Automation, Beijing, 100084, China; Southern Methodist University, Department of Computer Science, Dallas, 75205, TX, United States},
	correspondence_address = {Y. Fan; Tsinghua University, Beijing National Research Center for Information Science and Technology, Department of Automation, Beijing, 100084, China; email: fanyus@tsinghua.edu.cn},
	publisher = {Institute of Electrical and Electronics Engineers Inc.},
	issn = {19324537},
	language = {English},
	abbrev_source_title = {IEEE Trans. Netw. Serv. Manage.},
	type = {Article},
	publication_stage = {Final},
	source = {Scopus},
	note = {Cited by: 0}
}
```

## Ggrep locate the number of line items that match the word =

```
grep -vic "article" scopus.bib
```

Results in:

```
388_
```


## Grep to locate text using strings article & program to return either or =

```
grep -Ei "(article|program)" scopus.bib
```

Results in:

```
@ARTICLE{Jia20232668,
	type = {Article},
@ARTICLE{Balasubramanian2023297,
@ARTICLE{Rahman2020932,
	type = {Article},
	affiliations = {Dept. of Industrial Engineering, Lamar University, United States; Department of Professional Pedagogy, Lamar University, United States; Academic Partnerships Program, Lamar University, United States},
```

## Grep to find the first mention of the quoted word =

```
Grep -i -m1 "code" scopus.bib
```

Results in:

```
title = {Native Mobile Applications UI Code Conversion},_
```

## Grep to find line numbers of the quoted word =

```
Grep -in "code" scopus.bib
```

Results in:

```
150:	title = {Native Mobile Applications UI Code Conversion},
294:	coden = {MTAPF},
353:	coden = {CPISD},_
```

## How to upload to gcloud from 2nd terminal window =

```
gcloud compute scp file_name "server_name":~/ --zone "zone_name" --project "project_name"
```

## Grep to remove lines \t + the quoted word from search results =

```
grep -P "\tjournal" scopus.bib
```

```
	journal = {IEEE Transactions on Network and Service Management},
	journal = {2019 IEEE 8th Global Conference on Consumer Electronics, GCCE 2019},
	journal = {2023 3rd International Conference on Advance Computing and Innovative Technologies in Engineering, ICACITE 2023},
	journal = {Lecture Notes in Networks and Systems},
	journal = {Indonesian Journal of Electrical Engineering and Computer Science},
	journal = {2017 14th International Conference The Experience of Designing and Application of CAD Systems in Microelectronics, CADSM 2017 - Proceedings},
	journal = {ASEE Annual Conference and Exposition, Conference Proceedings},
	journal = {Proceedings - 2021 16th International Conference on Computer Engineering and Systems, ICCES 2021},_
```
