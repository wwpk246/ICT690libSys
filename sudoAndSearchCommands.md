## Sudo


1.`*sudo apt update*` //runs the ubuntu updater to check for updates

2.`*sudo apt upgrade*'` //applies available updates

3.`*sudo reboot*`  //reboots vm machine in case of a kernel update - still unclear how to tell this was applied

`*cd /usr/games*` //enters the games directory to help with brain stall moments

4.`*apt search "name"*`  //searches for software package name and returns all results

5.`*apt show "name"*`  //shows the relevant package information for the search result

6.`*sudo apt install "name"*`  //installs the software package

7.`*sudo apt autoremove "name"*`  //removes the software package and the dependent packages that were applied with it



## Search


**yaz-client** //allows to interact with library system

`apt search yaz`  //searches for the program
`sudo apt install yaz`  //installs the yaz software

From main command line view, type `yaz-client` which will load `Z>`

Open the library search connection `open saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY`

`find @and @attr 1=4 "information" @attr 1=21 "library science"`  
`find` is the command that sends a search request
`@and` is the operator signifying a Boolean AND search of multiple attributes
`@attr 1=4` instructs the query to search for the term in the Title
`"information"` is the first search term for the Title search
`@attr 1=21` instructs the query to search for the term in the Subject-heading
`"library science"` is the second search term for the subject heading search  

`show 1`  //shows the first record in the referenced search


