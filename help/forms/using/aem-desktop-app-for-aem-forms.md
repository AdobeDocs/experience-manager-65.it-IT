---
title: App desktop Adobe Experience Manager (AEM) per AEM Forms
description: App desktop Adobe Experience Manager (AEM) per AEM Forms
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin,User
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# App desktop Adobe Experience Manager (AEM) per AEM Forms {#aem-desktop-app-for-aem-forms}

L’app desktop AEM consente di mappare l’archivio Assets di Adobe Experience Manager (AEM) e i file binari di AEM Forms in una directory di rete sul sistema. È possibile visualizzare le risorse sincronizzate e i file binari in un Esplora file e utilizzare varie app per modificare i file come desiderato. Oltre a visualizzare i file, puoi anche creare, caricare ed eliminare i file binari. È inoltre possibile aprire, modificare e salvare i file direttamente dal software. Ad esempio, puoi aprire e modificare direttamente un file XDP da Designer. Le modifiche apportate localmente alle risorse si riflettono nell’archivio AEM Assets e nell’interfaccia utente di AEM Forms.

Puoi scaricare l’app da un’istanza AEM. Per informazioni dettagliate sul download dell&#39;app, consulta [Note sulla versione dell&#39;app desktop AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en).

## Risorse AEM Forms supportate nell’app desktop AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Puoi utilizzare l’app per sincronizzare file binari AEM Forms dei seguenti tipi: modelli di modulo (.xdp), modulo PDF (.pdf), documento (.pdf), immagini, schema XML (.xsd), fogli di stile (.xfs). L’app elenca tutti gli altri file (file non supportati) come file a 0 byte. L’elenco dei file non supportati come file a 0 byte assicura che l’utente sia a conoscenza dell’esistenza di altre risorse disponibili sul server AEM Forms.

>[!NOTE]
>
>Un nome file può contenere solo caratteri alfanumerici, trattini o trattini bassi.

## Abilitare l’app desktop AEM Forms for AEM {#enable-aem-forms-for-aem-desktop-app}

L&#39;app desktop AEM utilizza il protocollo WebDAV su Microsoft® Windows e SMB1 su macOS X per connettersi a un server AEM Forms. AEM Forms Server non è abilitato per la sincronizzazione di file binari e altre risorse con un client WebDAV o SMB. Effettua le seguenti operazioni per abilitare l’app desktop AEM Forms for AEM:

1. Accedi ad AEM Forms come amministratore.
1. Nell&#39;istanza di authoring, fare clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Strumenti]** ![hammer](assets/hammer.png) **[!UICONTROL > Distribuzione > Operazioni > Console Web]**. La console Web si apre in una nuova finestra.
1. Nella finestra della console Web individuare e aprire l&#39;opzione **[!UICONTROL Configurazione componente aggiuntivo FormsManager]**.
1. Nella finestra di dialogo Configurazione componente aggiuntivo FormsManager deselezionare la casella di controllo **[!UICONTROL Sincronizza risorse in modo asincrono]** e fare clic su **[!UICONTROL Salva]**.
1. Riavvia il server AEM Forms. Dopo il riavvio, il server AEM Forms è abilitato per accettare e condividere contenuti con l’app desktop AEM.
1. Apri l’app e connettiti al server AEM Forms.

   >[!NOTE]
   >
   > Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

   Una volta stabilita la connessione, l&#39;app popola le cartelle `content/dam` e `content/dam/formsanddocuments`. Oltre a spostare i file dalle cartelle di cui sopra alle cartelle locali e viceversa, puoi utilizzare l’app per spostare i contenuti tra cartelle con popolamento automatico.
