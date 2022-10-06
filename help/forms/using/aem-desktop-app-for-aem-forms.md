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
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# App desktop AEM per AEM Forms {#aem-desktop-app-for-aem-forms}

AEM’app desktop consente di mappare l’archivio di Adobe Experience Manager (AEM) Assets e i file binari AEM Forms in una directory di rete sul sistema. Puoi visualizzare le risorse sincronizzate e i file binari in un file explorer e utilizzare varie app per modificare i file come desiderato. Oltre a visualizzare i file, puoi anche creare, caricare ed eliminare i file binari. È inoltre possibile aprire, modificare e salvare i file direttamente dal software. Ad esempio, è possibile aprire e modificare direttamente un file XDP da Designer. Le modifiche apportate alle risorse localmente si riflettono nell’archivio di AEM Assets e nell’interfaccia utente di AEM Forms.

Puoi scaricare l’app da un’istanza AEM. Per informazioni dettagliate sul download dell’app, vedi [Note sulla versione dell’app desktop AEM](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## Risorse AEM Forms supportate nell’app desktop AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Puoi utilizzare l’app per sincronizzare i file binari AEM Forms dei seguenti tipi: Modelli di modulo (.xdp), Modulo di PDF (.pdf), Documento (.pdf), Immagini, Schema XML (.xsd), fogli di stile (.xfs). L’app elenca tutti gli altri file (file non supportati) come file a 0 byte. L’inserimento di file non supportati come file a 0 byte garantisce che l’utente sia a conoscenza dell’esistenza di altre risorse disponibili sul server AEM Forms.

>[!NOTE]
>
>Un nome file può contenere solo caratteri alfanumerici, trattini o caratteri di sottolineatura.

## Abilitare AEM Forms per l’app desktop AEM {#enable-aem-forms-for-aem-desktop-app}

AEM desktop App utilizza il protocollo WebDAV su Microsoft Windows e SMB1 su Mac OS X per connettersi a un server AEM Forms. Il server AEM Forms non è abilitato per la sincronizzazione di file binari e altre risorse con un client WebDAV o SMB. Esegui i seguenti passaggi per abilitare AEM Forms per AEM app desktop:

1. Accedi ad AEM Forms come amministratore.
1. Nell’istanza di authoring, fai clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Strumenti]** ![martello](assets/hammer.png) **[!UICONTROL > Implementazione > Operazioni > Console web]**. La console Web viene visualizzata in una nuova finestra.
1. Nella finestra della console Web, individuare e aprire **[!UICONTROL Configurazione del componente aggiuntivo FormsManager]** opzione .
1. Nella finestra di dialogo Configurazione AddOn di FormsManager, deselezionare la **[!UICONTROL Sincronizza le risorse in modo asincrono]** e fai clic su **[!UICONTROL Salva]**.
1. Riavvia il server AEM Forms. Dopo il riavvio, il server AEM Forms è abilitato ad accettare e condividere contenuti con AEM’app desktop.
1. Apri l’app e connettiti al server AEM Forms.

   Quando la connessione è riuscita, l&#39;app compila il `content/dam` e `content/dam/formsanddocuments` cartelle. Oltre a spostare file da cartelle precedenti a cartelle locali e viceversa, puoi utilizzare l’app per spostare contenuti tra cartelle popolate automaticamente.
