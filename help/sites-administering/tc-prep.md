---
title: Preparazione del contenuto per la traduzione
seo-title: Preparazione del contenuto per la traduzione
description: Scoprite come preparare il contenuto per la traduzione.
seo-description: Scoprite come preparare il contenuto per la traduzione.
uuid: 369630a8-2ed7-48db-973e-bd8213231d49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 8bd67d71-bcb7-4ca0-9751-3ff3ee054011
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---


# Preparazione del contenuto per la traduzione{#preparing-content-for-translation}

I siti Web multilingue forniscono in genere una certa quantità di contenuto in più lingue. Il sito è creato in una lingua e poi tradotto in altre lingue. In genere, i siti multilingue sono composti da rami di pagine, in cui ogni ramo contiene le pagine del sito in una lingua diversa.

Il Geometrixx di esempio Demo Site include diversi rami di lingua e utilizza la struttura seguente:

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

Ciascun ramo lingua di un sito è denominato copia per lingua. La pagina principale di una copia della lingua, nota come radice della lingua, identifica la lingua del contenuto nella copia della lingua. Ad esempio, `/content/geometrixx/fr` è la radice della lingua per la copia in lingua francese. Le copie della lingua devono utilizzare una [radice della lingua configurata correttamente](/help/sites-administering/tc-prep.md#creating-a-language-root) in modo che la lingua corretta sia utilizzata per le traduzioni di un sito di origine.

La copia per lingua per la quale originariamente create il contenuto del sito è il master della lingua. Il master lingua è l&#39;origine tradotta in altre lingue.

Utilizzate i seguenti passaggi per preparare il sito per la traduzione:

1. Creare la radice della lingua del master della lingua. Ad esempio, la radice della lingua del sito dimostrativo in lingua inglese è /content/geometrixx/en. Assicurarsi che la radice della lingua sia configurata correttamente in base alle informazioni in [Creazione di una radice della lingua](/help/sites-administering/tc-prep.md#creating-a-language-root).
1. Creare il contenuto del master lingua.
1. Create la directory principale della lingua di ciascuna copia per il sito. Ad esempio, la copia in lingua francese del sito di Geometrixx è /content/geometrixx/fr.

Dopo aver preparato il contenuto per la traduzione, potete creare automaticamente pagine mancanti nelle copie della lingua e nei relativi progetti di traduzione. (Vedere [Creazione di un progetto di traduzione](/help/sites-administering/tc-manage.md).) Per una panoramica del processo di traduzione dei contenuti in AEM, consultate [Translating Content for Multilingual Websites](/help/sites-administering/translation.md) (Traduzione dei contenuti per siti Web multilingue).

## Creazione di una directory principale {#creating-a-language-root}

Create un livello principale della lingua come pagina principale di una copia per lingua che identifichi la lingua del contenuto. Dopo aver creato la lingua principale, potete creare progetti di traduzione che includono la copia per lingua.

Per creare il livello principale della lingua, creare una pagina e utilizzare un codice della lingua ISO come valore per la proprietà Name. Il codice della lingua deve essere in uno dei seguenti formati:

* `<language-code>`Il codice della lingua supportato è un codice a due lettere, come definito ad esempio dallo standard ISO-639-1  `en`.

* `<language-code>_<country-code>` o  `<language-code>-<country-code>`il codice del paese supportato è un codice di due lettere minuscole o superiori, come definito dallo standard ISO 3166, ad esempio  `en_US`,  `en_us`,  `en_GB`,  `en-gb`.

Potete utilizzare entrambi i formati, in base alla struttura scelta per il sito globale.  Ad esempio, la pagina principale della copia in lingua francese del sito di Geometrixx ha `fr` come proprietà Name. Tenere presente che la proprietà Name viene utilizzata come nome del nodo di pagina nella directory archivio e quindi determina il percorso della pagina. (http://localhost:4502/content/geometrixx/fr.html)

La procedura seguente utilizza l’interfaccia touch per creare una copia in lingua di un sito Web. Per istruzioni sull&#39;utilizzo dell&#39;interfaccia classica, vedere [Creazione di una directory principale della lingua mediante l&#39;interfaccia classica](/help/sites-administering/tc-lroot-classic.md).

1. Vai a Siti.
1. Tocca o fai clic sul sito per il quale vuoi creare una copia per la lingua.

   Ad esempio, per creare una copia in lingua del sito Geometrixx Outdoors, toccate o fate clic su Geometrixx Outdoors Site.

1. Tocca o fai clic su Crea, quindi fai clic o tocca Crea pagina.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Selezionate il modello di pagina, quindi fate clic o toccate Avanti.
1. Nel campo Nome digitare il codice del paese nel formato `<language-code>` o `<language-code>_<country-code>`, ad esempio `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Digitare un titolo per la pagina.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. Tocca o fai clic su Crea. Nella finestra di dialogo di conferma, toccate o fate clic su **Fine** per tornare alla console Siti oppure su **Apri** per aprire la copia della lingua.

## Visualizzazione dello stato delle origini delle lingue {#seeing-the-status-of-language-roots}

L’interfaccia touch fornisce un pannello Riferimenti che mostra un elenco delle origini delle lingue create.

![chlimage_1-23](assets/chlimage_1-23a.png)

La procedura seguente utilizza l’interfaccia touch per aprire il pannello Riferimenti per una pagina.

1. Nella console Siti selezionare una pagina del sito, quindi fare clic o toccare **Riferimenti**.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. Nel pannello dei riferimenti, fare clic o toccare **Copie lingua**. Il pannello Copie lingua mostra le copie in lingua del sito Web.

