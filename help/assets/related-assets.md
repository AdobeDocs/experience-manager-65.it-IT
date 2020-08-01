---
title: Risorse correlate
description: Scoprite come collegare risorse digitali che condividono attributi comuni. Create anche relazioni derivate dal codice sorgente tra le risorse digitali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 2%

---


# Risorse correlate {#related-assets}

[!DNL Adobe Experience Manager Assets] consente di collegare manualmente le risorse in base alle esigenze dell’organizzazione mediante la funzione delle risorse correlate. Ad esempio, potete collegare un file di licenza a una risorsa o un&#39;immagine/video su un argomento simile. Potete correlare le risorse che condividono alcuni attributi comuni. Potete anche usare la funzione per creare relazioni sorgente/derivate tra le risorse. Ad esempio, se si dispone di un file PDF generato da un file INDD, è possibile collegare il file PDF al relativo file INDD di origine.

Grazie a questa funzione, potete condividere un file PDF o JPG a bassa risoluzione con fornitori o agenzie e rendere il file INDD ad alta risoluzione disponibile solo su richiesta.

>[!NOTE]
>
>Solo gli utenti con autorizzazioni di modifica per le risorse possono collegare e scollegare le risorse.

## Relate assets {#relating-assets}

1. Dall’ [!DNL Experience Manager] interfaccia, aprite la pagina **[!UICONTROL Proprietà]** di una risorsa da correlare.

   ![aprire la pagina Proprietà di una risorsa per correlare la risorsa](assets/asset-properties-relate-assets.png)

   *Figura:[!DNL Assets][!UICONTROL Pagina delle proprietà]per correlare le risorse.*

   In alternativa, selezionate la risorsa dalla vista a elenco.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Potete anche selezionare la risorsa da una raccolta.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Per mettere in relazione un’altra risorsa con la risorsa selezionata, fate clic su **[!UICONTROL Relate]** ![rapporta risorse](assets/do-not-localize/link-relate.png) dalla barra degli strumenti.
1. Effettua una delle operazioni seguenti:

   * Per correlare il file di origine della risorsa, selezionate **[!UICONTROL Origine]** dall’elenco.
   * Per correlare un file derivato, selezionare **[!UICONTROL Derivato]** dall&#39;elenco.
   * Per creare una relazione bidirezionale tra le risorse, selezionate **[!UICONTROL Altre]** dall’elenco.

   ![chlimage_1-276](assets/chlimage_1-276.png)

1. Dalla schermata **[!UICONTROL Seleziona risorsa]** , individuate la posizione della risorsa da correlare e selezionatela.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Fate clic su **[!UICONTROL Conferma]**.
1. Click **[!UICONTROL OK]** to close the dialog. A seconda della relazione scelta nel passaggio 3, la risorsa correlata è elencata in una categoria appropriata nella sezione **[!UICONTROL correlata]** . Ad esempio, se la risorsa correlata è il file di origine della risorsa corrente, viene elencata in **[!UICONTROL Origine]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Per non correlare una risorsa, fate clic su **[!UICONTROL Annulla relazione]** nella barra degli strumenti.

   ![attività non correlate](assets/do-not-localize/link-unrelate-icon.png)

1. Selezionate le risorse da rimuovere dalla finestra di dialogo **[!UICONTROL Rimuovi relazioni]** e fate clic su **[!UICONTROL Annulla relazione]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Click **[!UICONTROL OK]** to close the dialog. Le risorse per le quali avete rimosso le relazioni vengono eliminate dall’elenco delle risorse correlate nella sezione **[!UICONTROL Correlati]** .

## Tradurre le risorse correlate {#translating-related-assets}

La creazione di relazioni sorgente/derivate tra risorse mediante la funzione delle risorse correlate è utile anche nei flussi di lavoro di traduzione. Quando eseguite un flusso di lavoro di traduzione su una risorsa derivata, recupera [!DNL Experience Manager Assets] automaticamente tutte le risorse a cui fa riferimento il file sorgente e le include per la traduzione. In questo modo, la risorsa a cui fa riferimento la risorsa di origine viene convertita insieme alle risorse sorgente e derivate. Ad esempio, in uno scenario in cui la copia in lingua inglese include una risorsa derivata e il relativo file di origine come mostrato.

![chlimage_1-281](assets/chlimage_1-281.png)

Se il file di origine è correlato a un’altra risorsa, [!DNL Experience Manager Assets] recupera la risorsa di riferimento e la include per la conversione.

![la pagina Proprietà risorsa mostra il file di origine della risorsa correlata da includere per la traduzione](assets/asset-properties-source-asset.png)

*Figura: Risorsa di origine delle risorse correlate da includere per la conversione.*

1. Traducete le risorse presenti nella cartella di origine in una lingua di destinazione seguendo la procedura descritta in [Creazione di un nuovo progetto](translation-projects.md#create-a-new-translation-project)di traduzione. Ad esempio, in questo caso, potete tradurre le risorse in francese.

1. Dalla pagina [!UICONTROL Progetti] , aprite la cartella di traduzione.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Fate clic sulla sezione del progetto per aprire la pagina dei dettagli.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Fate clic sulle ellissi sotto la scheda Processo di traduzione per visualizzare lo stato della traduzione.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Selezionate la risorsa, quindi fate clic su **[!UICONTROL Mostra in risorse]** nella barra degli strumenti per visualizzare lo stato di conversione della risorsa.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Per verificare se le risorse correlate all’origine sono state tradotte, fate clic sulla risorsa sorgente.

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. Selezionate la risorsa correlata all’origine, quindi fate clic su **[!UICONTROL Mostra in risorse]**. Viene visualizzata la risorsa correlata convertita.

   ![chlimage_1-288](assets/chlimage_1-288.png)
