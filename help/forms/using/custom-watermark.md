---
title: Filigrana personalizzata nell’anteprima di Letter PDF
seo-title: Custom watermark in letter PDF preview
description: Scopri come creare una filigrana personalizzata nell’anteprima di Letter PDF.
seo-description: Learn how to create custom watermark in letter PDF preview.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Filigrana personalizzata nell’anteprima di Letter PDF{#custom-watermark-in-letter-pdf-preview}

## Panoramica {#overview}

Nell’interfaccia utente per la creazione di corrispondenza, gli utenti agente visualizzano in anteprima la corrispondenza nella forma finale in cui viene inviata alla post-elaborazione, ad esempio per la posta elettronica o la stampa.

Per evitare l’uso non autorizzato di questi dati, le organizzazioni possono imporre una filigrana sul PDF di anteprima. La filigrana predefinita è &quot;PREVIEW&quot; (ANTEPRIMA), che viene visualizzata nel PDF.

Per abilitare la filigrana in preview PDF, seleziona la **[!UICONTROL Applica filigrana]** Opzione Periodo anteprima in **[!UICONTROL Configurazioni gestione corrispondenza]** in https://&#39;[server]:[porta]&#39;/system/console/configMgr.

![default-watermark](assets/default-watermark.png)

Per personalizzare il testo e l&#39;aspetto della filigrana, attenersi alla procedura descritta di seguito.

## Personalizzare la filigrana nell’anteprima PDF nell’interfaccia utente per la creazione di corrispondenza {#customizewatermark-}

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedere come amministratore.
1. Nella cartella delle app, crea una cartella denominata **[!UICONTROL filigrana anteprima]** con un percorso/struttura simile alla cartella filigrana di anteprima nella cartella libs:

   1. Fare clic con il pulsante destro del mouse **filigrana anteprima** cartella nel percorso seguente e selezionare **Sovrapponi nodo**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/configFiles/previewwatermark

      **Posizione sovrapposizione:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

      >[!NOTE]
      >
      >Non apportare modifiche nel ramo /libs. Qualsiasi modifica apportata potrebbe andare persa, poiché questo ramo potrebbe subire modifiche ogni volta che:
      >
      >    
      >    
      >    * Eseguire l’aggiornamento all’istanza
      >    * Applicare un hotfix
      >    * Installare un feature pack


   1. Clic **OK** e quindi fare clic su **Salva tutto**. Il **[!UICONTROL filigrana anteprima]** viene creata nel percorso specificato.

1. Copia e incolla il file ddx dalla cartella &quot;/libs/fd/cm/configFiles/previewwatermark&quot; alla cartella &quot;/apps/fd/cm/configFiles/previewwatermark&quot; e fai clic su **[!UICONTROL Salva tutto]**.
1. Apporta le modifiche desiderate nel file ddx in /apps/fd/cm/configFiles/previewwatermark/.

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

   Per informazioni sulla personalizzazione dell&#39;aspetto della filigrana, del testo e dell&#39;allineamento, vedere Aggiunta e rimozione di filigrane e sfondi nella [Servizio assemblatore e riferimento DDX](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) documento.

   >[!NOTE]
   >
   >Nel file ddx, i riferimenti a risultato e origine devono rimanere invariati in output.pdf e input.pdf. Anche il nome del file ddx non deve essere modificato.

1. Clic **Salva tutto**.
