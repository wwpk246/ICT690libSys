Grep command is used to find information within the document or text.  
Use grep to search for "words", 
to -i by ignoring case sensitivity, 
to -vi remove certain "words" from the results,
to -vi "^word" remove the word from the results,
to -vic "count" the number of times the word is in the results,
to -i -m1 "locate" use to locate the first mention of the word,
to -Ei "(article|program)" find either word within the text



**//overall grep command for a document or file = **
_willw@wwubuntu-1:~$ grep "^@" scopus.bib
@ARTICLE{Jia20232668,
@CONFERENCE{Sasaki2019563,
@CONFERENCE{Jothi Mary Jenifer20231141,
@ARTICLE{Balasubramanian2023297,
@ARTICLE{Rahman2020932,


**//grep with ignoring case sensitive = **
_willw@wwubuntu-1:~$ grep -i "journal" scopus.bib
journal = {IEEE Transactions on Network and Service Management},
journal = {2019 IEEE 8th Global Conference on Consumer Electronics, GCCE 2019},
journal = {2023 3rd International Conference on Advance Computing and Innovative Technologies in Engineering, ICACITE 2023},
journal = {Lecture Notes in Networks and Systems},
journal = {Indonesian Journal of Electrical Engineering and Computer Science},
journal = {2017 14th International Conference The Experience of Designing and Application of CAD Systems in Microelectronics, CADSM 2017 - Proceedings},
journal = {ASEE Annual Conference and Exposition, Conference Proceedings},


**//grep with removal of documents labeled "journal" = **
_willw@wwubuntu-1:~$ grep -vi "journal" scopus.bib
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


**//grep while removing the word journal from the results = **
_willw@wwubuntu-1:~$ grep -vi "^journal" scopus.bib
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


**//grep locate the number of line items that match the word = **
_willw@wwubuntu-1:~$ grep -vic "article" scopus.bib
388_


**//grep to locate text using strings article & program to return either or = **
willw@wwubuntu-1:~$ grep -Ei "(article|program)" scopus.bib
@ARTICLE{Jia20232668,
	type = {Article},
@ARTICLE{Balasubramanian2023297,
@ARTICLE{Rahman2020932,
	type = {Article},
	affiliations = {Dept. of Industrial Engineering, Lamar University, United States; Department of Professional Pedagogy, Lamar University, United States; Academic Partnerships Program, Lamar University, United States},


**//grep to find the first mention of the quoted word = **
_willw@wwubuntu-1:~$ grep -i -m1 "code" scopus.bib
	title = {Native Mobile Applications UI Code Conversion},_

 
**//grep to find line numbers of the quoted word = **
_willw@wwubuntu-1:~$ grep -in "code" scopus.bib
150:	title = {Native Mobile Applications UI Code Conversion},
294:	coden = {MTAPF},
353:	coden = {CPISD},_


**//how to upload to gcloud from 2nd terminal window = **
gcloud compute scp file_name "server_name":~/ --zone "zone_name" --project "project_name"


**//grep to remove lines \t + the quoted word from search results = **
_willw@wwubuntu-1:~$ grep -P "\tjournal" scopus.bib
	journal = {IEEE Transactions on Network and Service Management},
	journal = {2019 IEEE 8th Global Conference on Consumer Electronics, GCCE 2019},
	journal = {2023 3rd International Conference on Advance Computing and Innovative Technologies in Engineering, ICACITE 2023},
	journal = {Lecture Notes in Networks and Systems},
	journal = {Indonesian Journal of Electrical Engineering and Computer Science},
	journal = {2017 14th International Conference The Experience of Designing and Application of CAD Systems in Microelectronics, CADSM 2017 - Proceedings},
	journal = {ASEE Annual Conference and Exposition, Conference Proceedings},
	journal = {Proceedings - 2021 16th International Conference on Computer Engineering and Systems, ICCES 2021},_



 
