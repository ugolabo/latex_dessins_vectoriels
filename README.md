# LaTeX; dessins vectoriels

Un complément aux dépôts : **documentations_web_statiques** et **latex_pocket_book**.

## Matriciel vs vectoriel

Une photo, une capture d'écran avec annotations, un logo de logiciel ou d'entreprise, un dessin conceptuel  pour illustrer un projet, une animation avec GIF... ce sont des images matricielles à base de pixels comme les format PNG, JPG, JPEG et autres.

Les images vectorielles comme les formats PDF et SVG sont plutôt faites de points, de segments, de polygones et de formes qui peuvent s'exprimer avec des vecteurs mathématiques.

|   |   |
|---|---|
|  <img src="img/raster_vs_vector.jpg" alt="" > | <img src="img/matricielle_vs_vecteur.jpg" alt="" > |

## Dessins vectoriels

Peu importe le format de la documentation, les dessins ajoutent beaucoup de valeur à une documentation web ou un document :

- diagrammes en tous genres,
- illustration d'un domaine (géométrie, chimie, biologie, etc.),
- schéma de données, de réseaux, de programmes, de projets, etc.

Rendu PDF s'intègre à LaTeX, rendu SVG doit être converti, mais il s'intègre au Markdown. La conversion aussi en PNG, JPG pour Markdown, sites

dans **chaine_pico_streamlit**, diagramme de déploiement, composants

PlantUML, https://www.planttext.com/

```
@startuml
Title "Diagramme de déploiement (WiFi)"
'----------
'NOEUDS
'----------
node "Noeud" {
  ["Capteur \n(température, humidité; caméra)"] #Darkorange/white 
  ["RPi Pico \n(avec WiFi et BLE)"] #Indianred/white
  note right : Analyses \n\n(ou Teensy et \nTinyML potentiel)
  ("de l'ordinateur") #DarkGray
}

node "PC ou autre \nservant de passerelle" {
  ["serveur \nMQTT"] #Khaki/white
}

cloud Internet/Infonuagique #LightCyan {
  ["service \nMQTT"] #DodgerBlue/white
  database "MongoDB Atlas" #Yellowgreen/white {
    collections "Documents" #Greenyellow/white
  }
  database GitHub #Green/white {
    collections "repo Tableau" #Seagreen/white
  }
  cloud "Streamlit Cloud" #Cyan {
    ["Tableau \nde bord"] #Seagreen/white
  }
}

node "Poste de développement" {
  package "Streamlit" #Magenta/white {
    ["projet Tableau"] #Violet/white
  }
  package "Thonny" #Magenta/white {
    ["Programmes \nMicroPython"] #Violet/white
  }
  ("vers le MCU") #DarkGray
  note right: aussi \nEDI et programme C/C++
}
'----------
'LIENS
'----------
["Capteur \n(température, humidité; caméra)"] <--> ["RPi Pico \n(avec WiFi et BLE)"] : GPIO: numérique ou analoqique
("de l'ordinateur") --> ["RPi Pico \n(avec WiFi et BLE)"] : USB
["RPi Pico \n(avec WiFi et BLE)"] <.-> ["serveur \nMQTT"]: WiFi

["serveur \nMQTT"] .-> ["service \nMQTT"] : IP

["service \nMQTT"] .-> "Documents" : IP
"Documents" .-> ["projet Tableau"] : IP
["projet Tableau"] <.-> "repo Tableau" : IP/git
"repo Tableau" .--> ["Tableau \nde bord"]: IP
"Documents" .-> ["Tableau \nde bord"] : API

["Programmes \nMicroPython"] --> ("vers le MCU") : USB

@enduml
```

PNG ici

<img src="img/diagramme_deploiement_wifi.png" alt="" width="300px" >

mais aussi SVG et PDF pour LaTeX

plus dans https://toucan-fortune-streamlit-projet-integrateur-01-accueil-0fsbkp.streamlit.app/


dans **systeme_alarme_rpi**

diagramme d'état

```
@startuml
[*] -down-> DÉSARMÉ

DÉSARMÉ: - toutes DEL éteintes \n- contact brisé est \nsans effet
DÉSARMÉ --> DÉSARMÉ: en contact, \ncontact brisé, \nen contact


DÉSARMÉ -down-> ARMÉ: bouton \npressé \n(ARMER)
ARMÉ -down-> DÉSARMÉ: bouton \npressé \n(DÉSARMER)

ARMÉ: - DEL rouge allumée \n- contact brisé est \nsans effet si \nen contact avant 2s \net arrêt du chrono \n-en contact est \nsans effet si chrono \nest plus de 2s
ARMÉ --> ARMÉ: en contact, \ncontact brisé et \ndépart du chrono \nmoins de 2s, \nen contact

ARMÉ -down-> ALARME: en contact, \ncontact brisé et \ndépart du chrono \nplus de 2s, \nen contact

ALARME: - DEL rouge allumée \n- DEL jaune clignotante \n- courriel envoyé \n- contact brisé et \nen contact sont\nsans effet
ALARME --> ALARME: en contact, \ncontact brisé, \nen contact

ALARME --> DÉSARMÉ: bouton \npressé \n(DÉSARMER)

DÉSARMÉ -left-> [*]
ARMÉ -left-> [*]
ALARME -left-> [*]

@enduml
```

PNG ici

<img src="img/diagramme_etat.jpg" alt="" width="300px" >

dans **bases_donnees_sql_nosql**

BD SQL

| schéma relationel | schéma physique |
|---|---|
| <img src="img/physical_schema.jpg" alt="" > | <img src="img/relational_schema.jpg" alt="" > |


dans **chaine_pico_streamlit**

modèle de données JSON pour une collection sur MongoDB

<img src="img/modele_bd_json.png" alt="" width="300px" >


Fritzing

raster

dans **systeme_alarme_rpi**

schéma de montage

<img src="img/schema_montage_fritzing.jpg" alt="" width="300px" >

schéma de circuit électrique

<img src="img/schema_electrique_fritzing.jpg" alt="" width="300px" >


## Dessiner avec un langage

boostée à l'IAgen parfois

PlantUML
logiciel ou en ligne
https://www.plantuml.com/
https://plantuml.online/
https://www.planttext.com/
doc
exemples plus haut

ou similaire...

Graphviz et langage DOT
logiciel
doc
https://graphviz.org/gallery/
IMG https://graphviz.org/Gallery/neato/ER.html
IMG https://graphviz.org/Gallery/directed/git.html

modules et extensions de modules LaTeX
TikZ/PGF
tikz-cd
chemfig
forest
IMG
IMG

Mermaid et les autres en Markdown
https://mermaid.js.org/
IMG
IMG

## Dessiner avec une interface graphique

boostée à l'IAgen parfois

Fritzing
logiciel
doc
exemples plus haut

liste :

Dia
draw.io
Inkscape
Vectr
Adobe Illustrator
Affinity Designer
CorelDRAW
Microsoft Visio
Lucidchart
Miro
AutoCAD / FreeCAD
bioRender

