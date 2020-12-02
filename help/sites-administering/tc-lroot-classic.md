---
title: Creazione di una directory principale della lingua mediante l’interfaccia classica
seo-title: Creazione di una directory principale della lingua mediante l’interfaccia classica
description: Scoprite come creare una radice della lingua utilizzando l’interfaccia classica.
seo-description: Scoprite come creare una radice della lingua utilizzando l’interfaccia classica.
uuid: 62e40d39-2868-4d3d-9af7-c60a1a658be0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: b88edad4-2a2e-429b-86a2-cc68ba69697e
docset: aem65
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 2%

---


# Creazione di una directory principale della lingua mediante l&#39;interfaccia classica{#creating-a-language-root-using-the-classic-ui}

La procedura seguente utilizza l’interfaccia classica per creare una directory principale della lingua di un sito. Per ulteriori informazioni, vedere [Creazione di una directory principale della lingua](/help/sites-administering/tc-prep.md#creating-a-language-root).

1. Nella console Siti Web, nella struttura Siti Web, selezionate la pagina principale del sito. ([http://localhost:4502/siteadmin#](http://localhost:4502/siteadmin#))
1. Aggiungete una nuova pagina figlia che rappresenta la versione in lingua del sito:

   1. Fate clic su Nuova > Nuova pagina.
   1. Nella finestra di dialogo, specificate il Titolo e il Nome. Il nome deve essere nel formato `<language-code>` o `<language-code>_<country-code>`, ad esempio en, en_US, en_us, en_GB, en_gb.

      * Il codice della lingua supportato è un codice di due lettere minuscoli, come definito dallo standard ISO-639-1
      * Il codice del paese supportato è un codice di due lettere minuscolo o superiore, come definito dallo standard ISO 3166
   1. Selezionate il modello e fate clic su Crea.

   ![newpage](assets/newpagefr.png)

1. Nella console Siti Web, nella struttura Siti Web, selezionate la pagina principale del sito.
1. Dal menu Strumenti, selezionare Copia lingua.

   ![toolslanguage agecopy](assets/toolslanguagecopy.png)

   Nella finestra di dialogo Copia lingua viene visualizzata una matrice di versioni disponibili delle lingue e delle pagine Web. Una x in una colonna della lingua indica che la pagina è disponibile in quella lingua.

   ![languagecopydialog](assets/languagecopydialog.png)

1. Per copiare una pagina o una struttura ad albero di pagina esistente in una versione della lingua, selezionare la cella per tale pagina nella colonna della lingua. Fate clic sulla freccia e selezionate il tipo di copia da creare.

   Nell&#39;esempio seguente, la pagina attrezzatura/occhiali da sole/irian viene copiata nella versione in lingua francese.

   ![languagecopydilogdropdown](assets/languagecopydilogdropdown.png)

   | Tipo di copia della lingua | Descrizione |
   |---|---|
   | auto | Utilizza il comportamento delle pagine padre |
   | ignore | Non crea una copia di questa pagina e dei relativi elementi secondari |
   | `<language>+` (ad esempio, francese+) | Copia la pagina e tutti i relativi elementi secondari da tale lingua |
   | `<language>` (ad esempio francese) | Copia solo la pagina da tale lingua |

1. Fate clic su OK per chiudere la finestra di dialogo.
1. Nella finestra di dialogo successiva, fate clic su Sì per confermare la copia.

