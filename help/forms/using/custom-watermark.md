---
title: Filigrana personalizzata nell’anteprima PDF della lettera
description: Scopri come creare una filigrana personalizzata nell’anteprima PDF della lettera.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%
---
# Filigrana personalizzata nell’anteprima PDF della lettera{#custom-watermark-in-letter-pdf-preview}

## Panoramica {#overview}

Nell’interfaccia utente per la creazione di corrispondenza, gli utenti agente visualizzano in anteprima la corrispondenza nella forma finale in cui viene inviata alla post-elaborazione, ad esempio per la posta elettronica o la stampa.

Per evitare l’uso non autorizzato di questi dati, le organizzazioni possono imporre una filigrana sul PDF di anteprima. La filigrana predefinita è &quot;PREVIEW&quot; (ANTEPRIMA), che viene visualizzata in PDF.

Per abilitare la filigrana nell&#39;anteprima di PDF, seleziona l&#39;opzione **[!UICONTROL Applica filigrana]** durante l&#39;anteprima in **[!UICONTROL Configurazioni gestione corrispondenza]** all&#39;indirizzo https://&#39;[server]:[porta]&#39;/system/console/configMgr.

![filigrana predefinita](assets/default-watermark.png)

Per personalizzare il testo e l&#39;aspetto della filigrana, attenersi alla procedura descritta di seguito.

## Personalizzare la filigrana nell’anteprima di PDF nell’interfaccia utente per la creazione di corrispondenza {#customizewatermark-}

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedi come amministratore.
1. Nella cartella delle app, crea una cartella denominata **[!UICONTROL filigrana di anteprima]** con percorso/struttura simile alla cartella filigrana di anteprima nella cartella libs:

   1. Fare clic con il pulsante destro del mouse sulla cartella **anteprima filigrana** nel percorso seguente e selezionare **Sovrapponi nodo**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/configFiles/previewwatermark

      **Posizione sovrapposizione:** /apps/

      **Corrispondenza tipi di nodo:** selezionata

      >[!NOTE]
      >
      >Non apportare modifiche nel ramo /libs. Qualsiasi modifica apportata potrebbe andare persa, poiché questo ramo potrebbe subire modifiche ogni volta che:
      >
      >    
      >    
      >    * Eseguire l’aggiornamento all’istanza
      >    * Applicare un hotfix
      >    * Installare un feature pack
      >    
      >

   1. Fare clic su **OK** e quindi su **Salva tutto**. La cartella **[!UICONTROL anteprima filigrana]** è stata creata nel percorso specificato.

1. Copiare e incollare il file ddx dalla cartella &quot;/libs/fd/cm/configFiles/previewwatermark&quot; alla cartella &quot;/apps/fd/cm/configFiles/previewwatermark&quot; e fare clic su **[!UICONTROL Salva tutto]**.
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

   Per informazioni sulla personalizzazione dell&#39;aspetto della filigrana, del testo e dell&#39;allineamento, vedere Aggiunta e rimozione di filigrane e sfondi nel documento [Servizio assemblatore e Riferimenti DDX](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf).

   >[!NOTE]
   >
   >Nel file ddx, i riferimenti a risultato e origine devono rimanere invariati in output.pdf e input.pdf. Anche il nome del file ddx non deve essere modificato.

1. Fare clic su **Salva tutto**.
