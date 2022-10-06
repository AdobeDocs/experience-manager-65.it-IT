---
title: Preparare le risorse per la traduzione
description: Crea cartelle principali in lingua per preparare le risorse da tradurre per supportare le risorse multilingue.
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# Preparare le risorse per la traduzione {#preparing-assets-for-translation}

Per risorse multilingue si intendono le risorse con file binari, metadati e tag in più lingue. In genere, i binari, i metadati e i tag delle risorse esistono in una lingua, che vengono poi tradotti in altre lingue per l’utilizzo in progetti multilingue.

In [!DNL Adobe Experience Manager Assets], le risorse multilingue sono incluse nelle cartelle, in cui ogni cartella contiene le risorse in una lingua diversa.

Ogni cartella della lingua è denominata copia della lingua. La cartella principale di una copia per lingua, nota come radice lingua, identifica la lingua del contenuto nella copia per lingua. Ad esempio: */content/dam/it* è la radice della lingua italiana per la copia in lingua italiana. Le copie per lingua devono utilizzare un [directory principale della lingua configurata correttamente](preparing-assets-for-translation.md#creating-a-language-root) in modo che venga usata la lingua corretta quando vengono eseguite le traduzioni delle risorse di origine.

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

Per preparare le risorse per la traduzione, effettua le seguenti operazioni:

1. Creare la directory principale lingua della lingua primaria. Ad esempio, la directory principale della lingua della copia in lingua inglese nella gerarchia delle cartelle di esempio è `/content/dam/en`. Assicurati che la directory principale della lingua sia configurata correttamente in base alle informazioni in [Creare una directory principale della lingua](preparing-assets-for-translation.md#creating-a-language-root).

1. Aggiungi le risorse alla tua lingua primaria.
1. Crea la directory principale della lingua di ogni lingua di destinazione per la quale è necessaria una copia della lingua.

## Creare una directory principale della lingua {#creating-a-language-root}

Per creare la directory principale della lingua, creare una cartella e utilizzare un codice della lingua ISO come valore per la proprietà Name. Dopo aver creato la directory principale lingua, è possibile creare una copia della lingua a qualsiasi livello all’interno della directory principale lingua.

Ad esempio, la pagina principale della copia in lingua italiana della gerarchia dei campioni ha `it` come proprietà Name. La proprietà Name viene utilizzata come nome del nodo della risorsa nell’archivio e quindi determina il percorso delle risorse. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. Da [!DNL Assets] console, fai clic su **[!UICONTROL Crea]** e scegli **[!UICONTROL Cartella]** dal menu.

   ![Crea cartella](assets/Create-folder.png)

1. In **[!UICONTROL Nome]** digitare il codice del paese nel formato di `<language-code>`.

   ![Aggiungi il codice della lingua nella cartella](assets/Add-language-code-in-folder.png)

1. Fai clic su **[!UICONTROL Crea]**. La radice della lingua viene creata nella [!DNL Assets] console.

## Visualizzare le radici della lingua {#viewing-language-roots}

[!DNL Experience Manager] l&#39;interfaccia fornisce **[!UICONTROL Riferimenti]** pannello che visualizza un elenco delle radici della lingua create all&#39;interno di [!DNL Assets].

1. In [!DNL Assets] nella console selezionare la lingua principale per la quale si desidera creare le copie per lingua.
1. Dalla barra a sinistra, seleziona **[!UICONTROL Riferimenti]** per aprire [!UICONTROL Riferimento] riquadro.

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Nel riquadro Riferimenti, fai clic su **[!UICONTROL Copie per lingua]**. La [!UICONTROL Copie per lingua] mostra le copie in lingua delle risorse.

   ![copie per lingua](assets/lang-copy2.png)
