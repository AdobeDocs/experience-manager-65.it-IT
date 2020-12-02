---
title: Filigrana personalizzata nell'anteprima PDF della lettera
seo-title: Filigrana personalizzata nell'anteprima PDF della lettera
description: Scoprite come creare una filigrana personalizzata nell'anteprima PDF della lettera.
seo-description: Scoprite come creare una filigrana personalizzata nell'anteprima PDF della lettera.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Filigrana personalizzata in anteprima Lettera PDF{#custom-watermark-in-letter-pdf-preview}

## Panoramica {#overview}

Nell’interfaccia utente Crea corrispondenza, gli utenti agente visualizzano un’anteprima della corrispondenza nella forma finale in cui viene inviata alla post-elaborazione, ad esempio per l’e-mail o la stampa.

Per impedire l’uso non autorizzato di tali dati, le organizzazioni possono imporre una filigrana al PDF di anteprima. La filigrana predefinita è &quot;ANTEPRIMA&quot;, che viene visualizzata nel PDF.

Per abilitare la filigrana nell&#39;anteprima PDF, selezionare l&#39;opzione **[!UICONTROL Applica filigrana]** durante l&#39;anteprima in **[!UICONTROL Configurazioni di gestione della corrispondenza]** all&#39;indirizzo https://&#39;[server]:[port]&#39;/system/console/configMgr.

![filigrana predefinita](assets/default-watermark.png)

Per personalizzare il testo e l’aspetto della filigrana è possibile utilizzare i seguenti passaggi:

## Personalizzare la filigrana nell&#39;anteprima PDF nell&#39;interfaccia utente Crea corrispondenza {#customizewatermark-}

1. Andate a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedete come amministratore.
1. Nella cartella delle app, crea una cartella denominata **[!UICONTROL anteprime filigrana]** con percorso/struttura simile alla cartella della filigrana di anteprima nella cartella libs:

   1. Fare clic con il pulsante destro del mouse sulla cartella **anteprime filigrana** nel percorso seguente e selezionare **Overlay Node**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **Percorso:** /libs/fd/cm/configFiles/previewwatermark

      **Posizione overlay:** /apps/

      **Corrispondenza tipi di nodo:** Selezionati

      >[!NOTE]
      >
      >Non apportare modifiche al ramo /libs. Eventuali modifiche apportate potrebbero andare perse, in quanto il ramo potrebbe essere modificato ogni volta che:
      >
      >    
      >    
      >    * Aggiornamento dell’istanza
      >    * Applicazione di una correzione
      >    * Installare un pacchetto di funzioni


   1. Fare clic su **OK**, quindi fare clic su **Salva tutto**. La cartella **[!UICONTROL anteprime filigrana]** viene creata nel percorso specificato.



1. Copiate e incollate il file ddx dalla cartella &quot;/libs/fd/cm/configFiles/previewwatermark&quot; alla cartella &quot;/apps/fd/cm/configFiles/previewwatermark&quot; e fate clic su **[!UICONTROL Save All]** (Salva tutto).
1. Apportate le modifiche desiderate nel file ddx in /apps/fd/cm/configFiles/previewwatermark/.

   ```xml
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   Per informazioni su come personalizzare l&#39;aspetto della filigrana, il testo e l&#39;allineamento, vedere Aggiunta e rimozione di filigrane e sfondi nel documento [Assembler Service e DDX Reference](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf).

   >[!NOTE]
   >
   >Nel file ddx, i riferimenti a risultato e origine devono rimanere invariati in output.pdf e input.pdf. Anche il nome del file ddx non deve essere modificato.

1. Fare clic su **Salva tutto**.

