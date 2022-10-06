---
title: Filigrana personalizzata nell'anteprima di PDF lettera
seo-title: Custom watermark in letter PDF preview
description: Scopri come creare una filigrana personalizzata nell’anteprima di PDF a lettere.
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

# Filigrana personalizzata nell&#39;anteprima di PDF lettera{#custom-watermark-in-letter-pdf-preview}

## Panoramica {#overview}

Nell’interfaccia utente Crea corrispondenza, gli utenti dell’agente visualizzano in anteprima la corrispondenza nella forma finale in cui viene inviata alla post-elaborazione, ad esempio per l’e-mail o la stampa.

Per evitare l’utilizzo non autorizzato di questi dati, le organizzazioni possono imporre una filigrana al PDF di anteprima. La filigrana predefinita è &quot;ANTEPRIMA&quot;, che viene visualizzata in tutto il PDF.

Per abilitare la filigrana in anteprima PDF, seleziona la **[!UICONTROL Applica filigrana]** Opzione Anteprima in **[!UICONTROL Configurazioni di gestione della corrispondenza]** all&#39;indirizzo https://&#39;[server]:[porta]&#39;/system/console/configMgr.

![filigrana predefinita](assets/default-watermark.png)

Per personalizzare il testo e l’aspetto della filigrana è possibile attenersi alla procedura descritta di seguito.

## Personalizzare la filigrana nell’anteprima di PDF nell’interfaccia utente Crea corrispondenza {#customizewatermark-}

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata **[!UICONTROL filigrana di anteprima]** con percorso/struttura simile alla cartella del filigrana di anteprima nella cartella libs:

   1. Fai clic con il pulsante destro del mouse sul pulsante **filigrana di anteprima** nel seguente percorso e seleziona **Nodo di sovrapposizione**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/configFiles/previewwatermark

      **Posizione sovrapposizione:** /apps/

      **Tipi di nodo di corrispondenza:** Selezionato

      >[!NOTE]
      >
      >Non apportare modifiche al ramo /libs. Eventuali modifiche apportate potrebbero andare perse, in quanto questo ramo è soggetto a modifiche ogni volta che:
      >
      >    
      >    
      >    * Aggiorna l&#39;istanza
      >    * Applicare un hotfix
      >    * Installare un feature pack


   1. Fai clic su **OK** quindi fai clic su **Salva tutto**. La **[!UICONTROL filigrana di anteprima]** viene creata nel percorso specificato.

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

   Per informazioni su come personalizzare l’aspetto, il testo e l’allineamento della filigrana, consulta Aggiunta e rimozione di filigrane e sfondi nella sezione [Servizio di assemblaggio e riferimento DDX](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) documento.

   >[!NOTE]
   >
   >Nel file ddx, i riferimenti a risultato e sorgente devono rimanere inalterati in output.pdf e input.pdf. Anche il nome del file ddx non deve essere modificato.

1. Fai clic su **Salva tutto**.
