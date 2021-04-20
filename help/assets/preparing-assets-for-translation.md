---
title: Preparare le risorse per la traduzione
description: Crea cartelle principali in lingua per preparare le risorse da tradurre per supportare le risorse multilingue.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Projects
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---


# Preparare le risorse per la traduzione {#preparing-assets-for-translation}

Per risorse multilingue si intendono le risorse con file binari, metadati e tag in più lingue. In genere, i binari, i metadati e i tag delle risorse esistono in una lingua, che vengono poi tradotti in altre lingue per l’utilizzo in progetti multilingue.

In [!DNL Adobe Experience Manager Assets], le risorse multilingue sono incluse nelle cartelle, in cui ogni cartella contiene le risorse in una lingua diversa.

Ogni cartella della lingua è denominata copia della lingua. La cartella principale di una copia per lingua, nota come radice lingua, identifica la lingua del contenuto nella copia per lingua. Ad esempio, */content/dam/it* è la directory principale della lingua italiana per la copia in lingua italiana. Le copie in lingua devono utilizzare una [directory principale della lingua configurata correttamente](preparing-assets-for-translation.md#creating-a-language-root) in modo che la lingua corretta venga utilizzata durante l&#39;esecuzione delle traduzioni delle risorse di origine.

La copia per lingua per la quale hai originariamente aggiunto le risorse è la lingua principale. Il linguaggio primario è la fonte tradotta in altre lingue. Una gerarchia di cartelle di esempio include diverse directory principali della lingua:

```shell
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

Esegui i seguenti passaggi per preparare le risorse per la traduzione:

1. Creare la directory principale lingua della lingua primaria. Ad esempio, la directory principale della lingua della copia in lingua inglese nella gerarchia delle cartelle di esempio è `/content/dam/en`. Assicurati che la directory principale della lingua sia configurata correttamente in base alle informazioni in [Crea una directory principale della lingua](preparing-assets-for-translation.md#creating-a-language-root).

1. Aggiungi le risorse alla tua lingua primaria.
1. Crea la directory principale della lingua di ogni lingua di destinazione per la quale è necessaria una copia della lingua.

## Creare una directory principale della lingua {#creating-a-language-root}

Per creare la directory principale della lingua, creare una cartella e utilizzare un codice della lingua ISO come valore per la proprietà Name. Dopo aver creato la directory principale lingua, è possibile creare una copia della lingua a qualsiasi livello all’interno della directory principale lingua.

Ad esempio, la pagina principale della copia in lingua italiana della gerarchia di esempio ha `it` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della risorsa nell’archivio e quindi determina il percorso delle risorse. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. Dalla console [!DNL Assets], fai clic su **[!UICONTROL Crea]** e scegli **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella](assets/Create-folder.png)

1. Nel campo **[!UICONTROL Nome]** digitare il codice del paese nel formato `<language-code>`.

   ![Aggiungi il codice della lingua nella cartella](assets/Add-language-code-in-folder.png)

1. Fai clic su **[!UICONTROL Crea]**. La directory principale della lingua viene creata nella console [!DNL Assets].

## Visualizza le radici della lingua {#viewing-language-roots}

[!DNL Experience Manager] L’interfaccia fornisce un pannello  **** Riferimenti che visualizza un elenco di radici della lingua create all’interno di  [!DNL Assets].

1. Nella console [!DNL Assets] , seleziona la lingua principale per la quale vuoi creare delle copie per lingua.
1. Dalla barra a sinistra, seleziona l’opzione **[!UICONTROL Riferimenti]** per aprire il riquadro [!UICONTROL Riferimento].

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Nel riquadro Riferimenti, fai clic su **[!UICONTROL Copie per lingua]**. Il pannello [!UICONTROL Copie per lingua] mostra le copie in lingua delle risorse.

   ![copie per lingua](assets/lang-copy2.png)
