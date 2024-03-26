**Library Search**

-Installing yaz
Use the apt install

apt search yaz

apt show yaz

sudo apt install yaz

Yaz documentation:
man yaz-client
man bib1-attr

yaz-client webpage and much more in depth doc:

https://www.indexdata.com/resources/software/yaz/

Open yaz-client:

yaz-client

Launches a new commandline prompt as shown:
Z>

Connect to OPAC service:
open saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY

"Query Examples
Example:
To find title with word 'information' and the Library of Congress Subject Heading 'library science', we use the following query:

find @and @attr 1=4 "information" @attr 1=21 "library science"
In the above:

find is the command that sends a search request
@and is the operator signifying a Boolean AND search of multiple attributes
@attr 1=4 instructs the query to search for the term in the Title
"information" is the first search term for the Title search
@attr 1=21 instructs the query to search for the term in the Subject-heading
"library science" is the second search term for the subject heading search
The search does not reveal the results. To peruse the results, we use the show command. To show the first record:

show 1
Example:
Find with subject headings "library science" and "philosophy"

f @and @attr 1=21 "library science" @attr 1=21 "philosophy"
Example:
Find where personal name is "mcmurtry, larry"

f @attr 1=1 "mcmurtry, larry"
Example:
Find any for "c programming language"

f @attr 1=1016 "c programming language""
