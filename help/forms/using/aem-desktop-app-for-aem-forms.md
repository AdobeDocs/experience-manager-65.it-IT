---
title: App desktop AEM per AEM Forms
seo-title: App desktop AEM per AEM Forms
description: 'null'
seo-description: 'null'
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
translation-type: tm+mt
source-git-commit: 6fa293028332596bb93013119b4339c7721eb536

---


# App desktop AEM per AEM Forms {#aem-desktop-app-for-aem-forms}

L’app desktop AEM consente di mappare l’archivio delle risorse di Adobe Experience Manager (AEM) e i file binari di AEM Forms in una directory di rete del sistema. Potete visualizzare le risorse sincronizzate e i file binari in un file Explorer e utilizzare diverse app per modificare i file come desiderate. Oltre a visualizzare i file, potete anche creare, caricare ed eliminare i file binari. È inoltre possibile aprire, modificare e salvare i file direttamente dal software. Ad esempio, è possibile aprire e modificare direttamente un file XDP da Designer. Le modifiche apportate localmente alle risorse si riflettono nell’archivio di Risorse AEM e nell’interfaccia utente di AEM Forms.

Potete scaricare l&#39;app da un&#39;istanza di AEM. Per informazioni dettagliate sul download dell&#39;app, consultate Note sulla versione dell&#39;app desktop [AEM](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## Risorse AEM Forms supportate nell’app desktop AEM {#aem-forms-assets-supported-in-aem-desktop-app}

È possibile utilizzare l&#39;app per sincronizzare i file binari di AEM Forms del seguente tipo: Modelli di modulo (.xdp), Modulo PDF (.pdf), Documento (.pdf), Immagini, Schema XML (.xsd), fogli di stile (.xfs). L&#39;app elenca tutti gli altri file (file non supportati) come file a 0 byte. L&#39;elencazione di file non supportati come file a 0 byte garantisce che l&#39;utente sia a conoscenza dell&#39;esistenza di altre risorse disponibili nel server AEM Forms.

>[!NOTE]
>
>Un nome file può contenere solo caratteri alfanumerici, trattini o caratteri di sottolineatura.

## Abilita AEM Forms per l&#39;app desktop AEM {#enable-aem-forms-for-aem-desktop-app}

L’app desktop AEM utilizza il protocollo WebDAV su Microsoft Windows e SMB1 su Mac OS X per connettersi a un server AEM Forms. Il server AEM Forms non è abilitato per la sincronizzazione di file binari e altre risorse con un client WebDAV o SMB. Per abilitare AEM Forms per l’app desktop AEM, effettuate le seguenti operazioni:

1. Accedi ad AEM Forms come amministratore.
1. Nell’istanza di creazione, fate clic su ![adobeexperienceemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Strumenti **![martello](assets/hammer.png)**> Distribuzione > Operazioni > Console]**Web. La console Web si apre in una nuova finestra.
1. Nella finestra Console Web individuare e aprire l&#39;opzione di configurazione **[!UICONTROL del componente aggiuntivo]** FormsManager.
1. Nella finestra di dialogo Configurazione AddOn di FormsManager, deselezionare la casella di controllo **[!UICONTROL Sincronizza risorse]** in modo asincrono e fare clic su **[!UICONTROL Salva]**.
1. Riavviate il server AEM Forms. Dopo il riavvio, il server AEM Forms è abilitato per accettare e condividere il contenuto con l&#39;app desktop AEM.
1. Aprire l&#39;app e connettersi al server AEM Forms.

   Una volta stabilita la connessione, l&#39;app compila le cartelle `content/dam` e `content/dam/formsanddocuments` . Oltre a spostare i file da cartelle superiori a cartelle locali e viceversa, potete utilizzare l&#39;app per spostare il contenuto tra cartelle popolate automaticamente.

