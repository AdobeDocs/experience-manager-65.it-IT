---
title: Preparazione del contenuto per la traduzione
seo-title: Preparazione del contenuto per la traduzione
description: Scopri come preparare i contenuti per la traduzione.
seo-description: Scopri come preparare i contenuti per la traduzione.
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
feature: Language Copy
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---


# Preparazione del contenuto per la traduzione{#preparing-content-for-translation}

I siti web multilingue forniscono generalmente una certa quantità di contenuto in più lingue. Il sito viene creato in una lingua e poi tradotto in altre lingue. In genere, i siti multilingue sono composti da rami di pagine, in cui ogni ramo contiene le pagine del sito in una lingua diversa.

Il sito demo di Geometrixx di esempio include diversi rami di lingua e utilizza la seguente struttura:

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

Ogni ramo linguistico di un sito è denominato copia per lingua. La pagina principale di una copia per lingua, nota come lingua principale, identifica la lingua del contenuto nella copia per lingua. Ad esempio, `/content/geometrixx/fr` è la directory principale della lingua per la copia in lingua francese. Le copie per lingua devono utilizzare una [directory principale lingua configurata correttamente](/help/sites-administering/tc-prep.md#creating-a-language-root) in modo che la lingua corretta sia utilizzata per le traduzioni di un sito di origine.

La copia per lingua per la quale originariamente si è creato il contenuto del sito è la lingua master. Il maestro di lingua è la fonte tradotta in altre lingue.

Utilizza i seguenti passaggi per preparare il sito alla traduzione:

1. Creare la directory principale della lingua della lingua master. Ad esempio, la directory principale della lingua del sito dimostrativo inglese Geometrixx è /content/geometrixx/en. Assicurati che la directory principale della lingua sia configurata correttamente in base alle informazioni contenute in [Creazione di una directory principale della lingua](/help/sites-administering/tc-prep.md#creating-a-language-root).
1. Creare il contenuto della lingua master.
1. Crea la directory principale della lingua di ogni copia per la lingua del sito. Ad esempio, la copia in lingua francese del sito di esempio di Geometrixx è /content/geometrixx/fr.

Dopo aver preparato il contenuto per la traduzione, puoi creare automaticamente le pagine mancanti nelle copie della lingua e nei relativi progetti di traduzione. (Consulta [Creazione di un progetto di traduzione](/help/sites-administering/tc-manage.md).) Per una panoramica del processo di traduzione dei contenuti in AEM, consulta [Traduzione di contenuti per siti web multilingue](/help/sites-administering/translation.md).

## Creazione di una directory principale della lingua {#creating-a-language-root}

Crea una directory principale della lingua come pagina principale di una copia per lingua che identifica la lingua del contenuto. Dopo aver creato la directory principale lingua, puoi creare progetti di traduzione che includono la copia per lingua.

Per creare la directory principale della lingua, creare una pagina e utilizzare un codice della lingua ISO come valore per la proprietà Name. Il codice della lingua deve essere in uno dei seguenti formati:

* `<language-code>`Il codice della lingua supportato è un codice a due lettere come definito, ad esempio, dallo standard ISO-639-1  `en`.

* `<language-code>_<country-code>` o  `<language-code>-<country-code>`il codice del paese supportato è un codice a due lettere minuscolo o superiore, come definito dalla norma ISO 3166, ad esempio  `en_US`,  `en_us`,  `en_GB`,  `en-gb`.

Puoi utilizzare entrambi i formati, in base alla struttura scelta per il sito globale.  Ad esempio, la pagina principale della copia in lingua francese del sito Geometrixx ha `fr` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della pagina nella directory archivio, quindi determina il percorso della pagina. (http://localhost:4502/content/geometrixx/fr.html)

La procedura seguente utilizza l’interfaccia touch per creare una copia in lingua di un sito Web. Per istruzioni sull’utilizzo dell’interfaccia classica, consulta [Creazione di una directory principale della lingua utilizzando l’interfaccia classica](/help/sites-administering/tc-lroot-classic.md).

1. Passa a Sites.
1. Tocca o fai clic sul sito per il quale vuoi creare una copia per lingua.

   Ad esempio, per creare una copia in lingua del sito Geometrixx Outdoors, toccate o fate clic su Sito Geometrixx Outdoors.

1. Tocca o fai clic su Crea , quindi su Crea pagina .

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Seleziona il modello di pagina, quindi tocca o fai clic su Avanti .
1. Nel campo Nome digitare il codice del paese nel formato `<language-code>` o `<language-code>_<country-code>`, ad esempio `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Digita un titolo per la pagina.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. Tocca o fai clic su Crea. Nella finestra di dialogo di conferma, tocca o fai clic su **Fine** per tornare alla console Sites oppure su **Apri** per aprire la copia per lingua.

## Visualizzazione dello stato delle radici della lingua {#seeing-the-status-of-language-roots}

L’interfaccia touch fornisce un pannello Riferimenti che mostra un elenco delle radici della lingua create.

![chlimage_1-23](assets/chlimage_1-23a.png)

La procedura seguente utilizza l’interfaccia touch per aprire il pannello Riferimenti per una pagina.

1. Nella console Sites, seleziona una pagina del sito e quindi tocca o fai clic su **Riferimenti**.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. Nel pannello Riferimenti, tocca o fai clic su **Copie per lingua**. Il pannello Copie per lingua mostra le copie in lingua del sito Web.

