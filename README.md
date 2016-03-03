# Freie Amateurfunkrufzeichen in Deutschland

Das Script lädt das [“Verzeichnis der zugeteilten deutschen Amateurfunkrufzeichen und
ihrer Inhaber (Rufzeichenliste)”](http://www.bundesnetzagentur.de/SharedDocs/Downloads/DE/Sachgebiete/Telekommunikation/Unternehmen_Institutionen/Frequenzen/Amateurfunk/Rufzeichenliste/Rufzeichenliste_AFU.pdf?__blob=publicationFile&v=10) herunter und extrahiert daraus die vergebenen Rufzeichen.

Zum extrahieren der vergebenen Rufzeichen wird [pdfgrep](https://pdfgrep.org) in mindestens Version 1.4.0 benötigt.

Die Rufzeichenklasse und der Rufzeichentyp können durch Commandline Argumente angegeben werden. Es werden die nicht zuteilbaren Suffixe laut BundesNetzAgentur [Amtsblattverfügung Vfg Nr. 12/2005 geändert durch Vfg Nr. 34/2005](https://www.bundesnetzagentur.de/SharedDocs/Downloads/DE/Sachgebiete/Telekommunikation/Unternehmen_Institutionen/Frequenzen/Amateurfunk/AmtsblattverfuegungenAFu/Vfg122005ge228ndertdurcId1833pdf.pdf?__blob=publicationFile&v=4) berücksichtigt. Weiterhin werden persönliche Rufzeichen nur noch mit zwei und drei Buchstaben-Suffix ausgegeben.

Die ausgegebene Liste ist keine Gewähr darauf, dass ein Rufzeichen tatsächlich verfügbar ist. Nach Rückgabe eines Rufzeichens oder dem Tod des vorherigen Inhabers, ist ein Rufzeichen für eine gewissen Zeit gesperrt. Letzten Endes ist es Ermessenssache der BundesNetzAgentur, ob ein Rufzeichen vergeben werden kann. Die [Dienstleistungzentren Amteurfunkverwaltung](http://www.bundesnetzagentur.de/DE/Sachgebiete/Telekommunikation/Unternehmen_Institutionen/Frequenzen/SpezielleAnwendungen/Amateurfunk/amateurfunk_node.html) geben hier weitere Auskunft.

Die Idee stammt aus der Liste der freien österreichischen Suffixe beim [Metalab](https://metalab.at/wiki/MetaFunk/Rufzeichen).

## Aufruf

Hilfe:
```
$ ./freerfz_dl.py -h
usage: freerfz_dl.py [-h] -k {a,e} -t {p,k,r,a}

Generiere eine Liste mit freien Amateurfunkrufzeichen in Deutschland.

optional arguments:
  -h, --help    show this help message and exit
  -k {a,e}      Klasse: (A) oder (E)
  -t {p,k,r,a}  Typ: (P)ersonenbezogen, (K)lubstation, (R)elais/Funkbake,
                (A)usbildungsrufzeichen
```

Generierung aller freien persönlichen Klasse A Rufzeichen:
```
$ ./freerfz_dl.py -k a -t p
```

Generierung aller freien Ausbildungsrufzeichen Klasse E:
```
$ ./freerfz_dl.py -k e -t a
```

In welche Datei die Liste geschrieben wurde, steht dann in der Ausgabe.

Die Cache-Dateien mit den vergebenen Rufzeichen werden neu generiert, wenn ein neues PDF der gesamten Rufzeichenliste runter geladen wurde. Falls es sonst zu Fehlern kommt, können die ```*.cache```-Dateien alle gelöscht werden.

# Ausbau / TODO

## Code
  - ~~Rufzeichenlisten PDF runterladen~~
  - ~~generierte Textliste der vergebenen Rufzeichen zwischenspeichern und nicht jedes Mal neu aus dem PDF generieren~~
  - ~~bessere Effizienz durch Listencompare statt Iteration mit Regular Expressions~~

## Webseite
  - Suche nach nicht vergebenen Rufzeichen
  - Vorschläge für Initialen oder Abkürzungen
  - Vanity-Rufzeichen
  - 1337 5P34K ([Leetspeak](https://de.wikipedia.org/wiki/Leetspeak)) Rufzeichen
  - Rufzeichen in ITU-Buchstabiertafel anzeigen lassen
  - Rufzeichen in Morsezeichen ausgeben lassen (JavaScript-Generator)

### Verwendete Regular Expressions für Rufzeichensuchen

  - Klasse A Rufzeichen: ``/D([CDGHJ][0-9]|[BFKLM][1-9])[A-Z]{2,3}/``
  - Klasse E Rufzeichen: ``/DO[1-9][A-Z]{2,3}/`` 
  - Klubstationen Klasse A (ohne 4-7-stelliges Suffix): ```D([BCDFGHJKMQR][0-9][A-Z]|[AFKL]0[A-Z]{2,3}|A[023][A-Z]|P[3-9][A-Z])```
  - Klubstationen Klasse E: ```D(A[7-9][A-Z]|N0[A-Z]{2,3}|O0[A-Z])```
  - Ausbildungsrufzeichen Klasse A: ```DN[1-6][A-Z]{2,3}```
  - Ausbildungsrufzeichen Klasse E: ```DN[7-8][A-Z]{2,3}```
  - Relaisfunkstellen/Funkbaken Klasse A: ```D[BM]0[A-Z]{2,3}```
  - Relaisfunkstellen/Funkbaken Klasse E: ```DO0[A-Z]{2,3}```

