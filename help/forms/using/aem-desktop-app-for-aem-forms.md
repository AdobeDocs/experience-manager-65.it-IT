---
title: App desktop AEM per AEM Forms
seo-title: AEM desktop app for AEM Forms
description: App desktop AEM per AEM Forms
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# App desktop AEM per AEM Forms {#aem-desktop-app-for-aem-forms}

L’app desktop AEM consente di mappare l’archivio Adobe Experience Manager (AEM) Assets e i file binari di AEM Forms in una directory di rete sul sistema. È possibile visualizzare le risorse sincronizzate e i file binari in un Esplora file e utilizzare varie app per modificare i file come desiderato. Oltre a visualizzare i file, puoi anche creare, caricare ed eliminare i file binari. È inoltre possibile aprire, modificare e salvare i file direttamente dal software. È ad esempio possibile aprire e modificare direttamente un file XDP da Designer. Le modifiche apportate localmente alle risorse si riflettono nell’archivio di AEM Assets e nell’interfaccia utente di AEM Forms.

Puoi scaricare l’app da un’istanza AEM. Per informazioni dettagliate sul download dell’app, consulta [Note sulla versione dell’app desktop AEM](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## Risorse AEM Forms supportate nell’app desktop AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Puoi utilizzare l’app per sincronizzare file binari AEM Forms dei seguenti tipi: modelli di modulo (.xdp), modulo PDF (.pdf), documento (.pdf), immagini, schema XML (.xsd), fogli di stile (.xfs). L’app elenca tutti gli altri file (file non supportati) come file a 0 byte. L’elenco dei file non supportati come file a 0 byte assicura che l’utente sia a conoscenza dell’esistenza di altre risorse disponibili sul server di AEM Forms.

>[!NOTE]
>
>Un nome file può contenere solo caratteri alfanumerici, trattini o trattini bassi.

## Abilitare l’app desktop AEM Forms for AEM {#enable-aem-forms-for-aem-desktop-app}

L&#39;app desktop AEM utilizza il protocollo WebDAV su Microsoft Windows e SMB1 su Mac OS X per connettersi a un server AEM Forms. Per impostazione predefinita, il server AEM Forms non è abilitato alla sincronizzazione di file binari e altre risorse con un client WebDAV o SMB. Per abilitare l’app desktop AEM Forms for AEM, effettua le seguenti operazioni:

1. Accedi ad AEM Forms come amministratore.
1. Nell’istanza di authoring, fai clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Strumenti]** ![martello](assets/hammer.png) **[!UICONTROL > Distribuzione > Operazioni > Console web]**. La console Web si apre in una nuova finestra.
1. Nella finestra della console Web, individua e apri il **[!UICONTROL Configurazione componente aggiuntivo FormsManager]** opzione.
1. Nella finestra di dialogo Configurazione componente aggiuntivo FormsManager, deselezionare **[!UICONTROL Sincronizza risorse in modo asincrono]** e fare clic su **[!UICONTROL Salva]**.
1. Riavvia il server AEM Forms. Dopo il riavvio, il server AEM Forms è abilitato ad accettare e condividere contenuti con l’app desktop AEM.
1. Apri l’app e connettiti al server AEM Forms.

   Una volta stabilita la connessione, l’app popola `content/dam` e `content/dam/formsanddocuments` cartelle. Oltre a spostare i file dalle cartelle di cui sopra alle cartelle locali e viceversa, puoi utilizzare l’app per spostare i contenuti tra cartelle con popolamento automatico.
