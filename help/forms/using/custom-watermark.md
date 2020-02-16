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
source-git-commit: 5a586758da84f467e075adcc33cdcede2fbf09c7

---


# Filigrana personalizzata nell&#39;anteprima PDF della lettera{#custom-watermark-in-letter-pdf-preview}

## Panoramica {#overview}

Nell’interfaccia utente Crea corrispondenza, gli utenti agente visualizzano un’anteprima della corrispondenza nella forma finale in cui viene inviata alla post-elaborazione, ad esempio per l’e-mail o la stampa.

Per impedire l’uso non autorizzato di tali dati, le organizzazioni possono imporre una filigrana al PDF di anteprima. La filigrana predefinita è &quot;ANTEPRIMA&quot;, che viene visualizzata nel PDF.

Per abilitare la filigrana nell&#39;anteprima PDF, selezionare l&#39;opzione **[!UICONTROL Applica filigrana]** durante l&#39;anteprima in **[!UICONTROL Correspondence Management Configurations]** all&#39;indirizzo https://[server]:[porta]/sistema/console/configMgr.

![filigrana predefinita](assets/default-watermark.png)

Per personalizzare il testo e l’aspetto della filigrana è possibile effettuare le seguenti operazioni:

## Personalizzare la filigrana nell’anteprima PDF nell’interfaccia utente Crea corrispondenza {#customizewatermark-}

1. Accedete a `https://[server]:[port]/[ContextPath]/crx/de` e accedete come amministratore.
1. Nella cartella delle app, create una cartella denominata **[!UICONTROL previewwatermark]** con percorso/struttura simile alla cartella della filigrana di anteprima nella cartella libs:

   1. Fate clic con il pulsante destro del mouse sulla cartella della filigrana **di** anteprima nel percorso seguente e selezionate Nodo **** sovrapposizione:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **** Percorso: /libs/fd/cm/configFiles/previewwatermark

      **** Posizione overlay: /apps/

      **** Corrispondenza tipi di nodo: Selezionato

      >[!NOTE]
      >
      >Non apportare modifiche al ramo /libs. Eventuali modifiche apportate potrebbero andare perse, in quanto il ramo potrebbe essere modificato ogni volta che:
      >
      >    
      >    
      >    * Aggiornamento dell’istanza
      >    * Applicazione di una correzione
      >    * Installare un pacchetto di funzioni


   1. Fate clic su **OK** , quindi su **Salva tutto**. La cartella **[!UICONTROL della filigrana]** di anteprima viene creata nel percorso specificato.



1. Copiate e incollate il file ddx dalla cartella &quot;/libs/fd/cm/configFiles/previewwatermark&quot; alla cartella &quot;/apps/fd/cm/configFiles/previewwatermark&quot; e fate clic su **[!UICONTROL Salva tutto]**.
1. Apportate le modifiche desiderate nel file ddx in /apps/fd/cm/configFiles/previewwatermark/.

   ```
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

   Per informazioni su come personalizzare l’aspetto della filigrana, il testo e l’allineamento, consultate Aggiunta e rimozione di filigrane e sfondi nel documento [Assembler Service e DDX Reference](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) .

   >[!NOTE]
   >
   >Nel file ddx, i riferimenti a risultato e origine devono rimanere invariati in output.pdf e input.pdf. Anche il nome del file ddx non deve essere modificato.

1. Fate clic su **Salva tutto**.

