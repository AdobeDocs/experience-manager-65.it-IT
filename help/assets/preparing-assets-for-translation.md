---
title: Preparare le risorse per la traduzione
description: Crea cartelle directory principale della lingua per preparare le risorse per la traduzione in modo da supportare le risorse multilingue.
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# Preparare le risorse per la traduzione {#preparing-assets-for-translation}

Risorse multilingue significa risorse con binari, metadati e tag in più lingue. In genere, i file binari, i metadati e i tag per le risorse esistono in una lingua e vengono quindi tradotti in altre lingue per l’utilizzo in progetti multilingue.

In [!DNL Adobe Experience Manager Assets], le risorse multilingue sono incluse nelle cartelle, dove ogni cartella contiene le risorse in una lingua diversa.

Ogni cartella della lingua è denominata copia per lingua. La cartella principale di una copia per lingua, nota come directory principale della lingua, identifica la lingua del contenuto nella copia per lingua. Ad esempio, */content/dam/it* è la directory principale della lingua italiana per la copia in lingua italiana. Le copie per lingua devono utilizzare una [directory principale lingua configurata correttamente](preparing-assets-for-translation.md#creating-a-language-root) in modo che la lingua corretta venga utilizzata quando vengono eseguite le traduzioni delle risorse di origine.

La copia per lingua per la quale originariamente hai aggiunto le risorse è la lingua principale. La lingua primaria è la fonte che viene tradotta in altre lingue. Una gerarchia di cartelle di esempio include diverse directory principali della lingua:

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

Per preparare le risorse per la traduzione, effettua le seguenti operazioni:

1. Crea la directory principale della lingua primaria. Ad esempio, la directory principale della lingua della copia in lingua inglese nella gerarchia delle cartelle di esempio è `/content/dam/en`. Verificare che la directory principale della lingua sia configurata correttamente in base alle informazioni in [Creare una directory principale della lingua](preparing-assets-for-translation.md#creating-a-language-root).

1. Aggiungere risorse alla lingua principale.
1. Crea la directory principale della lingua di ogni lingua di destinazione per la quale hai bisogno di una copia per lingua.

## Creare una directory principale lingua {#creating-a-language-root}

Per creare la directory principale della lingua, è necessario creare una cartella e utilizzare un codice della lingua ISO come valore per la proprietà Name. Dopo aver creato la directory principale della lingua, puoi creare una copia per lingua a qualsiasi livello all’interno della directory principale della lingua.

Ad esempio, la pagina principale della copia in lingua italiana della gerarchia di esempio ha `it` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della risorsa nell’archivio e quindi determina il percorso delle risorse. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. Dalla console [!DNL Assets], fai clic su **[!UICONTROL Crea]** e scegli **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella](assets/Create-folder.png)

1. Nel campo **[!UICONTROL Nome]** digitare il codice del paese nel formato `<language-code>`.

   ![Aggiungi codice lingua nella cartella](assets/Add-language-code-in-folder.png)

1. Fai clic su **[!UICONTROL Crea]**. La directory principale della lingua viene creata nella console [!DNL Assets].

## Visualizza directory principali della lingua {#viewing-language-roots}

L&#39;interfaccia [!DNL Experience Manager] fornisce un pannello **[!UICONTROL Riferimenti]** che visualizza un elenco di directory principali della lingua create in [!DNL Assets].

1. Nella console [!DNL Assets] selezionare la lingua principale per la quale si desidera creare copie per lingua.
1. Dalla barra a sinistra, seleziona **[!UICONTROL Riferimenti]** per aprire il riquadro [!UICONTROL Riferimenti].

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Nel riquadro Riferimenti fare clic su **[!UICONTROL Copie per lingua]**. Il pannello [!UICONTROL Copie per lingua] mostra le copie per lingua delle risorse.

   ![copie per lingua](assets/lang-copy2.png)
