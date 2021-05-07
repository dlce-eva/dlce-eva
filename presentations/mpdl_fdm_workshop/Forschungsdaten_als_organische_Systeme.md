---

title: Forschungsdaten als organische Systeme? 
description: Forschungsdaten als organische Systeme?
type: slide
slideOptions:
  theme: moon
  progress: true
  transition: fade
  slideNumber: true
  
---

## Forschungsdaten als organische Systeme?

Christoph Rzymski, Robert Forkel, Johann-Mattis List

Max-Planck-Institut für Menschheitsgeschichte
Abteilung Sprach- und Kulturevolution (DLCE)

---

## Ausgangsthese

----

Der konventionelle Lebenszyklus von Forschungsdaten sieht Daten an ihrem Endpunkt vor allem als Ausgangspunkt für die Generierung und Erhebung neuer Daten.

Note:
  Was meine ich mit dem Titel?

----

![](https://pad.gwdg.de/uploads/upload_26e35b4900c2b05ec97a7243fe468570.png =350x)

(https://www.ianus-fdz.de/lebenszyklus)

Note:
  Der Datenlebenszyklus ist sicher bekannt.

----

In unserer täglichen Arbeit mit stark vernetzten, reichhaltig annotierten, lexikalischen Daten zeigt sich, dass diese monolithische bzw. starre Sicht auf Daten, die einen Anfang und ein Ende haben (sollen), nicht unserem wissenschaftlichen Alltag entspricht.

----

![](https://pad.gwdg.de/uploads/upload_63ae3c1040c184532570e4bb61d2d2ca.png)

(Tableaux phonétiques des patois suisses romands)

----

![](https://pad.gwdg.de/uploads/upload_d16290763d3dd15175faf89b680418eb.png)

(Tableaux phonétiques des patois suisses romands)

----

![](https://pad.gwdg.de/uploads/upload_ddb4d745e25ad5dd935f50b8d9b1707c.png)

(Linguistic Survey of India)

----

![](https://pad.gwdg.de/uploads/upload_ad476f0f9bbffc9691d88957e1d834f1.png)

(STEDT)

----

![](https://pad.gwdg.de/uploads/upload_435e1ed52f60af225812e26424e52af4.PNG)

(StarLing/Tower of Babel)

----

Und vor allem auch:

- (Feldforschungs-)Daten Forschender am Institut
- Daten und Materialien von weltweit verteilten Beitragenden und Mitwirkenden

----

Durch eine Reihe von Umständen wird fast jeder Abschnitt des Datenlebenszkylus zu einem *moving target*:

- **Erstellung**: permanenter input neuer Daten, *lifting* historischer Daten, Anreicherung alter Daten, variable Klassifizierungen
- **Verarbeitung**: Anforderungsprofile sind permanent im Wandel, siehe **Erstellung**
- **Analyse**: neue Anforderungen an Daten führen zu neuen und verbesserten Analyseschritten, siehe **Verarbeitung**

----

Durch eine Reihe von Umständen wird fast jeder Abschnitt des Datenlebenszkylus zu einem *moving target*:

- **Archivierung**: neue Zwischenergebnisse müssen vorgehalten werden, siehe **Analyse**
- **Zugang**: Zugriff auf Zwischenschritte muss flexibel und konfigurierbar sein, siehe **Archivierung**
- **Nachnutzung**: welche Konfiguration welcher Versionen verwendet worden ist, muss transparent und nachnutzbar sein, siehe **Zugang**

Note:
  Anders als dies beispielsweise in naturwissenschaftlichen Disziplinen.

----

### Zusammenfassung

----

- Daten befinden sich während ihrer gesamten Lebensphase in einem Kontinuum
- klar definierte Anfangs- und Endpunkte sind durch sich stets ändernde Datenlagen schwer bis gar nicht zu definieren

**Fazit:** Verschiedene Bausteine und Komponenten sind nötig, um diesen Umständen im Sinne der guten wissenschaftlichen Praxis zu begegnen.

----

![](https://pad.gwdg.de/uploads/upload_253e0835b4fa7487a57717a49c864e25.jpg)

----

![](https://pad.gwdg.de/uploads/upload_9ddf0e0d8d1afb6157fd8a7ea21057ee.jpg)

----

![](https://pad.gwdg.de/uploads/upload_1193c3e69cda6abc47a9dddcd2239804.jpg)

----

![](https://pad.gwdg.de/uploads/upload_785fe3d462e420391f339abd94acf2ee.jpg)

----

![](https://pad.gwdg.de/uploads/upload_331e69dec9bfca7c472b1f5cde4b6b08.jpg)

----

![](https://pad.gwdg.de/uploads/upload_78c7365d7c66093ad42470fab2c7cd21.jpg)

----

![](https://pad.gwdg.de/uploads/upload_da4b4fa6f04535880060e8179ed39321.jpg)

---

## Bausteine

----

1. CLDF, menschen- und maschinenlesbare Formate
2. Versionskontrolle für Daten
3. Referenzkataloge, verteilte Daten, Metadaten
4. Testsuiten für Daten
5. Nutzbarkeit von Daten während ihres gesamten Lebenszykluses

----

### (1) CLDF, menschen- und maschinenlesbare Formate

----

CLDF (Cross-Linguistic Data Formats, https://doi.org/10.1038/sdata.2018.205) ist ein Paketformat zur Beschreibung linguistischer bzw., allgemeiner, tabellarischer Daten.

CLDF orientiert sich stark an den W3C Spezifikationen zu [CSV on the Web](https://www.w3.org/TR/tabular-data-primer/).

----

Ein CLDF Datensatz besteht im Kern aus:

- einer Menge von UTF-8 kodierten Dateien
- einer [CSVW TableGroup](https://w3c.github.io/csvw/metadata/#table-groups) (Metadaten)
- einer `dc:conformsTo`-Eigenschaft für die einzelnen Komponenten welche ihre Semantik aus der CLDF-Ontologie beziehen

----

![](https://pad.gwdg.de/uploads/upload_3cb08f966a1d8123a232e5365098016f.png)

----

![](https://pad.gwdg.de/uploads/upload_049d4812cd6aee2ed4428b6e63a41402.png)

(https://theodi.github.io/presentations/2014-07-15-csv-wg.html)

----

CLDF steht damit im Zentrum:

----

![](https://pad.gwdg.de/uploads/upload_877d525d8cb775a03954f7edcf09f920.png =650x)

----

CLDF bedient sich dabei der üblichen Bausteine der W3C zu Daten die im *semantic web* existieren:

* CSV(W): CSV on the web
* JSON-LD: JavaScript Object Notation for Linked Data
* RDF: Resource Description Framework
* Vokabularen wie dem Dublin Core Schema
* eine Ontologie

**FAIR**ness ist damit in CLDF nicht nur ein Ziel sondern fundamentaler Bestandteil des Designs sowie der einzelnen Komponenten.

----

CLDF bietet somit:

* ein CSV-basiertes Paketformat mit Semantik über die CLDF-Ontologie, verschiedenen Modulen für verschiedene Anwendungsszenarien, eingebauter Unterstützung für Referenzkataloge
* wiederverwendbare und stabile *Identifiers* für Sprachinformationen, semantische Konzepte, Transkriptionssystemen und Strukturfeatures

----

CLDF bietet somit:

* textbasierte und relationale Daten die nicht auf externe Software angewiesen sind (davon aber profitieren können)
* eine vielzahl von Interfaces, Werkzeugen, und APIs

----

![](https://pad.gwdg.de/uploads/upload_df189a482c939860775e1ea813be440b.png =500x)

----

### (2) Versionskontrolle für Daten

----

Um Daten als moving target greifbar zu machen, sollten:

- Zwischenresultate eindeutig identifizerbar sein:
    - Versionsnummern, Releases, Zenodo
- Daten einfach zugänglich sein:
    - Daten als installierbare Pythonpakete
- Daten mittels üblicher Arbeitsschritte von Versionskontrolle kuratiert werden
    - pull requests, commits, issues

----

[Releases](https://github.com/tupian-language-resources/tuled/releases):

![](https://pad.gwdg.de/uploads/upload_c52280435add9e22fa1bcd87da332081.png)

----

[Zenodo](https://zenodo.org/record/4629306):

![](https://pad.gwdg.de/uploads/upload_41ae891a6db554ab6cb4ff90d1948a4c.PNG =600x)

----

[Git und GitHub](https://github.com/tupian-language-resources/tuled):

![](https://pad.gwdg.de/uploads/upload_ae05d3413310e5a8644c35604a054091.png)

----

[Daten als (installierbare) Pakete](https://github.com/clics/clics3/blob/master/datasets.txt):

![](https://pad.gwdg.de/uploads/upload_a877249eb6da05b0ea79d5b024e291af.png)

----

### (3) Referenzkataloge, verteilte Daten, Metadaten

----

Daten stehen selten allein sondern sind auf externe Quellen bzw. Metadaten angewiesen.

Stabile (unter den vorangegangen Punkten kuratierte) Referenzkataloge erlauben mittels persistenter Referenzen (Identifier) das Einspeisen dieser Metadaten in sich in der Entwicklung befindliche Datensätze.

----

![](https://pad.gwdg.de/uploads/upload_877d525d8cb775a03954f7edcf09f920.png =650x)

----

- Glottolog
    - [Website](https://glottolog.org/), [Datengrundlage](https://github.com/glottolog/glottolog/)
- Concepticon
    - [Website](https://concepticon.clld.org/), [Datengrundlage](https://github.com/concepticon/concepticon-data/)
- CLTS
    - [Website](https://clts.clld.org/), [Datengrundlage](https://github.com/cldf-clts/clts)

----

Das gewählte Paketformat muss die Referenz auf diese Kataloge unterstützen und direkt einbetten.

----

![](https://pad.gwdg.de/uploads/upload_39620711d32a2a1cb6c4dbec3ac3701a.png =500x)

----

![](https://pad.gwdg.de/uploads/upload_bb3b24e7b1dd0754b970c015167cf39e.png)

----

![](https://pad.gwdg.de/uploads/upload_74ccd5e671343abab1cfdeef602760a8.png)

----

### (4) Testsuiten für Daten

----

Ausgehend von der Grundannahme, dass Daten sich während ihrer Lebensphase stets wandeln können, bieten Tests (Modultests, Integrationstests, Validierungstests) ein sehr hilfreiches Werkzeug, um Fehler in Daten vorzubeugen bzw. Auswirkungen von Änderungen abschätzen zu können.

Dies kann in verschiedenen Granularitäten passieren, ist aber stets möglich und wertvoll.

----

Bewährt haben sich hier Dienste wie [Travis CI](https://travis-ci.org/) oder aktuell [GitHub Actions](https://github.com/features/actions).

Je nach gewünschtem Schärfegrad der Tests kann die Einbettung auch in komplexeren System wie [Buildbot](https://buildbot.net/) oder [Jenkins](https://www.jenkins.io/) stattfinden.

----

![](https://pad.gwdg.de/uploads/upload_71879dc798fa2bc50b43eb50bdb9b0e6.png)

----

![](https://pad.gwdg.de/uploads/upload_876c001ee581ed03c000cdc8475268f9.png)

----

![](https://pad.gwdg.de/uploads/upload_ad0e904c9182c91d611921c8d4895726.png)

----

### (5) Nutzbarkeit von Daten während ihres gesamten Lebenszykluses

----

Datenerhebung und Datenanalyse ist ein iterativer Prozess.

All die vorgestellten Bausteine sind vor allem in einem Kontext sinnvoll, in dem Daten während ihres gesamten Lebenszykluses nutzbar sind (im Kontrast zu Daten die ein finales Artefakt darstellen sollen).

----

Ausgangspunkt dafür ist, dass das Erstellen bzw. Generieren **validen CLDFs** an erster Stelle steht.

Dadurch wird der iterative Prozess (einbinden und analysieren von CLDF in bestehende Pipelines, Verbesserung, Fehlersuche, neue Generierung, Versionierung, ...) erst ermöglicht.

Durch CLDF als menschen- und maschinenlesbares Format ist dies in jeder Phase möglich.

----

CLDF ist als tabellarisches Format einfach zu bearbeiten und zu sichten und kann gleichermassen aus einer Vielzahl von Formaten heraus erzeugt bzw. in eine Vielzahl von Formaten (SQL!) überführt werden.

----

![](https://pad.gwdg.de/uploads/upload_8994d7ab86b2cef435911e968ee7189f.PNG)

---

## Links und Ressourcen

----

- CLDF:
    - https://cldf.clld.org/
    - https://github.com/cldf
    - https://github.com/cldf/cookbook
    - https://doi.org/10.1038/sdata.2018.205

- Zenodo:
    - https://zenodo.org/communities/cldf-datasets/
    - https://zenodo.org/communities/clics/
    - https://zenodo.org/communities/lexibank/

----

- Reproduzierbare Analysen mit CLDF:
    - https://doi.org/10.1038/s41597-019-0341-x
    - https://codeocean.com/capsule/7201165/tree/v2

- GitHub Organisationen:
    - https://github.com/clld
    - https://github.com/concepticon
    - https://github.com/glottolog
    - https://github.com/lingpy
    - https://github.com/clics


























