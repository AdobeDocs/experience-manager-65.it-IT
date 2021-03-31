---
title: Attività correlate
description: Scopri come mettere in relazione le risorse digitali che condividono alcuni attributi comuni. Crea anche relazioni derivate dall’origine tra le risorse digitali.
contentOwner: AG
role: Professionista
feature: Collaborazione, Gestione risorse
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---


# Risorse correlate {#related-assets}

[!DNL Adobe Experience Manager Assets] consente di collegare manualmente le risorse in base alle esigenze dell’organizzazione utilizzando la funzione relativa alle risorse. Ad esempio, puoi correlare un file di licenza con una risorsa o un&#39;immagine/video su un argomento simile. È possibile correlare le risorse che condividono determinati attributi comuni. È inoltre possibile utilizzare la funzione per creare relazioni sorgente/derivate tra le risorse. Ad esempio, se si dispone di un file PDF generato da un file INDD, è possibile collegare il file PDF al relativo file INDD di origine.

Utilizzando questa funzione, hai la flessibilità di condividere un file PDF o JPG a bassa risoluzione con fornitori o agenzie e rendere il file INDD ad alta risoluzione disponibile solo su richiesta.

>[!NOTE]
>
>Solo gli utenti con autorizzazioni di modifica sulle risorse possono correlare e rimuovere la relazione tra le risorse.

## Relazionare le risorse {#relating-assets}

1. Dall’interfaccia [!DNL Experience Manager], apri la pagina **[!UICONTROL Proprietà]** per una risorsa che desideri correlare.

   ![apri la pagina Proprietà di una risorsa per correlare la risorsa](assets/asset-properties-relate-assets.png)

   *Figura:  [!DNL Assets]  Pagina delle proprietà per correlare le risorse.*

   In alternativa, seleziona la risorsa dalla vista a elenco.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Puoi anche selezionare la risorsa da una raccolta.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. Per correlare un’altra risorsa alla risorsa selezionata, fai clic su **[!UICONTROL Relate]** ![correlate assets](assets/do-not-localize/link-relate.png) nella barra degli strumenti.
1. Effettua una delle operazioni seguenti:

   * Per correlare il file di origine della risorsa, seleziona **[!UICONTROL Origine]** dall’elenco.
   * Per correlare un file derivato, selezionare **[!UICONTROL Derivato]** dall&#39;elenco.
   * Per creare una relazione bidirezionale tra le risorse, seleziona **[!UICONTROL Altri]** dall’elenco.

1. Dalla schermata **[!UICONTROL Seleziona risorsa]** , individua la posizione della risorsa da correlare e selezionala.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Fare clic su **[!UICONTROL Conferma]**.
1. Fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. A seconda della relazione scelta nel passaggio 3, la risorsa correlata è elencata sotto una categoria appropriata nella sezione **[!UICONTROL Correlata]** . Ad esempio, se la risorsa correlata è il file di origine della risorsa corrente, è elencata in **[!UICONTROL Origine]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Per annullare la relazione di una risorsa, fai clic su **[!UICONTROL Annulla relazione]** ![scollega risorse](assets/do-not-localize/link-unrelate-icon.png) nella barra degli strumenti.

1. Seleziona le risorse da rimuovere dalla finestra di dialogo **[!UICONTROL Rimuovi relazioni]** e fai clic su **[!UICONTROL Annulla relazione]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Fare clic su **[!UICONTROL OK]** per chiudere la finestra di dialogo. Le risorse per le quali hai rimosso le relazioni vengono eliminate dall’elenco delle risorse correlate nella sezione **[!UICONTROL Correlate]** .

## Tradurre le risorse correlate {#translating-related-assets}

È utile anche nei flussi di lavoro di traduzione creare relazioni sorgente/derivate tra le risorse utilizzando la relativa funzione. Quando esegui un flusso di lavoro di traduzione su una risorsa derivata, [!DNL Experience Manager Assets] recupera automaticamente tutte le risorse a cui fa riferimento il file di origine e le include per la traduzione. In questo modo, la risorsa a cui fa riferimento la risorsa di origine viene tradotta insieme alle risorse di origine e derivate. Ad esempio, considera uno scenario in cui la copia in lingua inglese include una risorsa derivata e il relativo file di origine come mostrato.

![chlimage_1-281](assets/chlimage_1-281.png)

Se il file di origine è correlato a un’altra risorsa, [!DNL Experience Manager Assets] recupera la risorsa di riferimento e la include per la traduzione.

![la pagina Proprietà risorsa mostra il file di origine della risorsa correlata da includere per la traduzione](assets/asset-properties-source-asset.png)

*Figura: Risorsa di origine delle risorse correlate da includere per la traduzione.*

1. Traduci le risorse nella cartella di origine in una lingua di destinazione seguendo i passaggi descritti in [Crea un nuovo progetto di traduzione](translation-projects.md#create-a-new-translation-project). Ad esempio, in questo caso, traduci le tue risorse in francese.

1. Dalla pagina [!UICONTROL Progetti] , apri la cartella di traduzione.

1. Fai clic sulla sezione del progetto per aprire la pagina dei dettagli.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Fai clic sui puntini di sospensione sotto la scheda Processo di traduzione per visualizzare lo stato della traduzione.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Seleziona la risorsa e fai clic su **[!UICONTROL Mostra in Assets]** nella barra degli strumenti per visualizzare lo stato di traduzione della risorsa.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Per verificare che le risorse correlate all’origine siano state tradotte, fai clic sulla risorsa di origine.

1. Seleziona la risorsa correlata all&#39;origine, quindi fai clic su **[!UICONTROL Mostra in Assets]**. Viene visualizzata la risorsa correlata tradotta.
