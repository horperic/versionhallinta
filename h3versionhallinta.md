# h3 Versionhallinta

## Git ja GitHub

Tehtävään kuului tehdä sen raportti MarkDownina GitHub-varastoon. Git on versionhallintajärjestelmä, joka tekee tiedostoihin tehtyjen muutosten seuraamisesta helpompaa. 
Esimerkiksi kun editoidaan tiedostoa, git voi auttaa määrittelemään mikä muuttui, kuka 
muutti sen ja miksi. Se on hyödyllinen työn koordinoinnissa useamman henkilön projekteissa tai edistymisen seuraamisessa tallennuspisteiden avulla. Git ei ole ainoa saatavilla oleva versionhallintajärjestelmä, mutta se on ylivoimaisesti suosituin. 

GitHub taas on verkkosivu projektien hostaamista varten, jotka käyttävät git:iä. GitHub käyttää projektien organisointiin varastoja, yleensä yhtä varastoa käytetään yhden projektin organisointiin. Varastoihin voi kuulua tiedostoja, kuvia, videoita, laskutaulukkoja 
tai mitä vaan projekti tarvitseekaan. Tein GitHub:iin tyhjän varaston 'versionhallinta' tätä tehtävää ja sen tiedostoja varten.

## git log, git diff ja git blame 

Git log on yksinkertainen ja tehokas työkalu, minkä avulla nähdään aiemmat commitit varaston historiassa. Ajoin itse komennon varastossa, minkä olin luonut tätä tehtävää
varten.

	$ git log
	commit 11a65d103e2ec43c6494f82ab7376de504e2cb30 (HEAD -> main, origin/main, origin/HEAD)
	Author: Iiro Juntunen <bga263@myy.haaga-helia.fi>
	Date:   Thu Apr 15 15:44:21 2021 +0300

    Add h3versionhallinta

	commit d5e0a0415e22f263e9d2069c88e63fde42496664
	Author: Iiro Juntunen <bga263@myy.haaga-helia.fi>
	Date:   Thu Apr 15 15:40:54 2021 +0300

    Add h3versionhallinta

	commit 9639f21611e64c970e2649d644981effcf3a7472
	Author: Iiro Juntunen <bga263@myy.haaga-helia.fi>
	Date:   Thu Apr 15 14:39:03 2021 +0300

    UPDATE h3versionhallinta

	commit bbf585719f722581f86997a2b71f5beaee9e1e84
	Author: Iiro Juntunen <bga263@myy.haaga-helia.fi>
	Date:   Thu Apr 15 14:37:16 2021 +0300

    ADD h3versionhallinta

	commit 3876c1c63b616dd1a277f9a13d343415f7130399
	Author: Iiro Juntunen <bga263@myy.haaga-helia.fi>
	Date:   Thu Apr 15 14:30:43 2021 +0300

    Add README

Oletuksena git log listaa kaikki tehdyt muutokset käänteisessä aikajärjestyksessä eli tuorein ensin.
Tulosteesta näkyi varaston jokainen "commit", sen tarkistussumma, tekijän nimi ja sähköposti, 
päivämäärä ja viesti. Komennolle voidaan antaa lukuisia erilaisia optioita määrittämään se antamaan
tarkkaan se tieto mitä halutaan tai miten se esitetään. Kokeilin vielä formatoida komennon tulostetta yksinkertaisemmaksi --pretty optiolla.
Tämä antoi tulosteen, jossa jokainen commit on yhdellä rivillä mikä voi olla hyödyllinen jos tutkitaan suurta joukkoa niitä.
	
	$ git log --pretty=oneline
	9da8e1685537b2345a9efd8f52255686b308226b (HEAD -> main, origin/main, origin/HEAD) Update h3versionhallinta
	293a74aac0d4d2ed2f0127892d5e180b416ebc34 Update h3versionhallinta
	2e5d3aef6a717a77dd784aacbb1d4f0ee4979cf6 Update h3versionhallinta
	36ac58acb9daf1766a86c83ecd19a9c9a47ba37d Update h3versionhallinta
	11a65d103e2ec43c6494f82ab7376de504e2cb30 Add h3versionhallinta
	d5e0a0415e22f263e9d2069c88e63fde42496664 Add h3versionhallinta
	9639f21611e64c970e2649d644981effcf3a7472 UPDATE h3versionhallinta
	bbf585719f722581f86997a2b71f5beaee9e1e84 ADD h3versionhallinta
	3876c1c63b616dd1a277f9a13d343415f7130399 Add README
	3691083fb096cce15690433f17dc568d4560062e Initial commit

Git diff näyttää kahden version väliset erot ja koska git on pohjimmiltaan versionhallintajärjestelmä
on se hyvin keskeinen komento. Diff komento ottaa kaksi syötettä ja peilaa niiden välisiä eroja. Syötteiden ei tarvitse olla välttämättä tiedostoja vaan ne voivat olla committeja, haaroja tai muutakin. Kahden tiedoston välinen ero on kuitenkin
hyvin tyypillinen operaatio niin tein sen itsekin esimerkin vuoksi. Tein muutoksia tyhjään "moi.txt" tiedostoon ja lisäsin sinne jälkeenpäin tekstiä. Sen jälkeen annoin komennon, joka näyttää eron tiedostolle "moi.txt." sen tämänhetkisessä tilassa
ja edellisessä versiossa. Tulosteesta näkyi ensinnäkin syötteeksi annetut tiedostot, komentoon liittyvä metadata, kaksirivinen diff-ylätunnus (---+++), muutoksen yhteenveto (legend) ja muutettu rivi.


	$ git diff HEAD^ HEAD moi.txt
	diff --git a/moi.txt b/moi.txt
	index e69de29..cd62f46 100644
	--- a/moi.txt
	+++ b/moi.txt
	@@ -0,0 +1 @@
	+Moi! Mitä kuuluu?

Git blame on myös usein käytetty komento ja se näyttää kuka on muuttanut ja mitä tietyssä tiedostossa, rivi riviltä. Sitä voidaan käyttää usein jos työskennellään ryhmässä ja esimerkiksi jos jokin koodinpätkä ihmetyttää voidaan
saada selville keneltä asiaa pitää kysyä. Kokeilin itse komentoa perusmuodossaan edellisessä vaiheessa tekemääni tiedostoon mihin olin tehnyt pienen lisäyksen ja tulosteesta siis näkyi ensiksi tiivistefunktio, tekijän nimi, päiväys ja riville tehty muutos.

	$ git blame moi.txt
	d2b8e050 (Iiro Juntunen 2021-04-15 17:19:25 +0300 1) Moi! Mitä kuuluu?
	77f67c67 (Iiro Juntunen 2021-04-16 11:58:25 +0300 2) 
	77f67c67 (Iiro Juntunen 2021-04-16 11:58:25 +0300 3) 
	77f67c67 (Iiro Juntunen 2021-04-16 11:58:25 +0300 4) Oikein hyvää.
	
## Tyhmä muutos - git reset

Jossain tapauksissa voidaan huomata, että muutokset joita on tehty eivät olleetkaan niin hyviä. Jos on vaikka muutettu tiedostoja, lisätty tai poistettu vääriä rivejä ja halutaan palata takaisin on muutosten takaisinpalautukseen olemassa 'git reset' tekniikka. 
Tehtävässä oli tarkoituksena tehdä tyhmä muutos gittiin ilman commit:tia ja tuhota huonot muutokset komennolla 'git reset --hard'. Hard reset on erittäin voimakas mutta myös vaarallinen työkalu, koska se heittää pois kaikki muutokset joita ei ole kommitoitu. 
Tein ei-halutun muutoksen tekstitiedostooni ja sitten tutkin tilannetta ensin 'git status'. 

	$ git status
	On branch main
	Your branch is up to date with 'origin/main'.

	Changes not staged for commit:
  	(use "git add <file>..." to update what will be committed)
  	(use "git checkout -- <file>..." to discard changes in working directory)

	modified:   moi.txt

	no changes added to commit (use "git add" and/or "git commit -a")

Sen tulosteesta näkyi tämä tekemäni muutos mitä en ollut vielä kommitoinut. Sitten tein hard resetin, jotta muutos poistuisi.

	$ git reset --hard
	HEAD is now at 9065c46 Update

Tämä annettu komento poisti pysyvästi muutoksen mitä ei oltu kommitoitu ja kun tarkistin uudestaan tilan 'git status' niin sieltä näin, että puun tila oli puhdas.

	$ git status
	On branch main
	Your branch is up to date with 'origin/main'.

	nothing to commit, working tree clean

## Uusi salt-moduuli

Tehtävänä oli asentaa ja konfiguroida uusi salt-moduuli ja asensin itse yksinkertaisen komentokehotteesta toimivan ohjelman nimeltään figlet, millä voi tehdä ASCII-tekstibannereita normaalista tekstistä. Ensin käsin asennuksen vuoro.

	$ sudo apt-get update
	$ sudo apt-get install figlet

Sen sijaan, että olisin kirjoittanut muutettavan tekstin suoraan komentoriville tein tekstitiedoston mistä se luetaan ja sitten ajoin komennon mikä luki tämän tiedostosta.

	$ echo "Hello" >hello.txt
	$ figlet -p < hello.txt
	 _   _        _  _         
	| | | |  ___ | || |  ___   
	| |_| | / _ \| || | / _ \  
	|  _  ||  __/| || || (_) | 
	|_| |_| \___||_||_| \___/  

Ja komento tulosti halutun ASCII-tekstin oikein. Sitten oli salt-moduulin vuoro, missä käytin apuna edellisestä viikkotehtävästä tuttuja pkg ja file-moduuleita sekä lisäksi tunnilla käsiteltyä cmd-moduulia.

	$ sudoedit /srv/salt/figlet.sls

	figlet:
  	  pkg.installed

	/srv/salt/hello.txt:
  	  file.managed:
   	     - source:  salt://hello.txt

	figlet -p < /srv/salt/hello.txt:
  	  cmd.run

Sitten lisäsin tilan minioneille ja tuloste antoi ilmi sen onnistuneen.

	$ sudo salt '*' state.apply figlet
	minion1:
	----------
          ID: figlet
    	Function: pkg.installed
      	Result: True
     	Comment: All specified packages are already installed
     	Started: 16:01:56.951302
    	Duration: 1133.127 ms
    	 Changes:   
	----------
          ID: /srv/salt/hello.txt
    	Function: file.managed
      	Result: True
     	Comment: File /srv/salt/hello.txt is in the correct state
    	 Started: 16:01:58.087751
   	 Duration: 13.496 ms
    	 Changes:   
	----------
          ID: figlet -p < /srv/salt/hello.txt
    	Function: cmd.run
      	Result: True
    	 Comment: Command "figlet -p < /srv/salt/hello.txt" run
    	 Started: 16:01:58.102215
   	 Duration: 6.557 ms
    	 Changes:   
              ----------
              pid:
                  14794
              retcode:
                  0
              stderr:
              stdout:
                   _   _      _ _        
                  | | | | ___| | | ___   
                  | |_| |/ _ \ | |/ _ \  
                  |  _  |  __/ | | (_) | 
                  |_| |_|\___|_|_|\___/

	Summary for minion1
	------------
	Succeeded: 3 (changed=1)
	Failed:    0
	------------
	Total states run:     3
	Total run time:   1.153 s

## Lähteet

Tero Karvinen: [Publish Your Project with GitHub](http://terokarvinen.com/2016/publish-your-project-with-github/index.html)

Git: [git Documentation](https://git-scm.com/docs/git) 


