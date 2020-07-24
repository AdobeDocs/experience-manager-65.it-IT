---
title: Preparare le risorse per la traduzione
description: Create le cartelle principali della lingua per preparare le risorse da tradurre e supportare le risorse multilingue.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---


# Preparare le risorse per la traduzione {#preparing-assets-for-translation}

Per risorse in più lingue si intendono risorse con file binari, metadati e tag in più lingue. In genere, i file binari, i metadati e i tag delle risorse esistono in una lingua, che vengono poi tradotti in altre lingue per l’utilizzo in progetti multilingue.

In  risorse di Adobe Experience Manager, le risorse in più lingue sono incluse nelle cartelle, in cui ciascuna cartella contiene le risorse in un’altra lingua.

Ogni cartella lingua è denominata copia per lingua. La cartella principale di una copia della lingua, nota come radice della lingua, identifica la lingua del contenuto nella copia della lingua. Ad esempio, */content/dam/it* è la radice della lingua italiana per la copia in lingua italiana. Le copie della lingua devono utilizzare una radice [della lingua configurata](preparing-assets-for-translation.md#creating-a-language-root) correttamente, in modo che venga utilizzata la lingua corretta quando vengono eseguite le traduzioni delle risorse di origine.

La copia per la lingua per la quale avete aggiunto originariamente le risorse è la lingua principale. La lingua primaria è l&#39;origine tradotta in altre lingue. Una gerarchia di cartelle di esempio include diverse origini di lingua:

```
 /content
  /- dam
   |- en
   |- fr
   |- de
   |- es
   |- it
   |- ja
   |- zh
```

Per preparare le risorse alla conversione, effettuate le seguenti operazioni:

1. Creare la radice della lingua della lingua principale. Ad esempio, la radice della lingua della copia in lingua inglese nella gerarchia delle cartelle di esempio è `/content/dam/en`. Verificare che la radice della lingua sia configurata correttamente in base alle informazioni contenute in [Creare una radice](preparing-assets-for-translation.md#creating-a-language-root)della lingua.

1. Aggiungere risorse alla lingua principale.
1. Create la radice della lingua di ciascuna lingua di destinazione per la quale è necessaria una copia della lingua.

## Creare una radice della lingua {#creating-a-language-root}

Per creare la directory principale della lingua, create una cartella e utilizzate un codice della lingua ISO come valore per la proprietà Name. Dopo aver creato la lingua principale, è possibile creare una copia della lingua a qualsiasi livello all&#39;interno della lingua principale.

Ad esempio, la pagina principale della copia in lingua italiana della gerarchia di esempi ha `it` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della risorsa nella directory archivio e pertanto determina il percorso delle risorse. (`https://[aem_server]:[port]/assets.html/content/dam/it/`)

1. From the Assets console, click **[!UICONTROL Create]** and choose **[!UICONTROL Folder]** from the menu.

   ![Crea cartella](assets/Create-folder.png)

1. Nel campo **[!UICONTROL Nome]** digitare il codice del paese nel formato di `<language-code>`.

   ![Aggiungi il codice della lingua nella cartella](assets/Add-language-code-in-folder.png)

1. Fai clic su **[!UICONTROL Crea]**. L’elemento principale della lingua viene creato nella console Risorse.

## Visualizzare le origini della lingua {#viewing-language-roots}

&#39;interfaccia Experience Manager fornisce un pannello **[!UICONTROL Riferimenti]** che visualizza un elenco delle origini delle lingue create all&#39;interno di Risorse.

1. Nella console Risorse, selezionate la lingua principale per la quale desiderate creare delle copie in lingua.
1. Dalla barra a sinistra, selezionate l’opzione **[!UICONTROL Riferimenti]** per aprire il riquadro [!UICONTROL Riferimento] .

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Nel riquadro Riferimenti, fare clic su Copie **[!UICONTROL lingua]**. Il pannello Copie  lingua mostra le copie in lingua delle risorse.

   ![copie per lingua](assets/lang-copy2.png)
