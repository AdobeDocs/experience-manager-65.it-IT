---
title: Integrazione dell'area di lavoro AEM moduli con Microsoft Office SharePoint Server
seo-title: Integrazione dell'area di lavoro AEM moduli con Microsoft Office SharePoint Server
description: 'È possibile integrare AEM area di lavoro moduli con Microsoft Office SharePoint Server. '
seo-description: 'È possibile integrare AEM area di lavoro moduli con Microsoft Office SharePoint Server. '
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
translation-type: tm+mt
source-git-commit: 21623c615ebe69226cfaf84baf4cfb1717b449f4
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---


# Integrazione dell&#39;area di lavoro AEM moduli con Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Requisiti**

**Conoscenza**
dei prerequisitiPer poter aggiungere  AEM Forms Workspace a SharePoint Server, è necessario disporre dell&#39;accesso a SharePoint Server con i privilegi appropriati e conoscere l&#39;URL per accedere a Workspace. I passaggi seguenti presuppongono la conoscenza di SharePoint Server. Per ulteriori informazioni sulle web part in SharePoint Server, vedere web part in Windows SharePoint Services.

**Livello**
utenteInizio

È possibile utilizzare  AEM Forms Workspace come web part in Microsoft Office SharePoint Server (ad esempio, Microsoft Office SharePoint Server 2007). Gli utenti possono accedere  AEM Forms Workspace collegandosi a SharePoint Server utilizzando un browser Web per fornire un&#39;esperienza unificata. In questo articolo vengono illustrati i passaggi di base per visualizzare  AEM Forms Workspace come web part in Microsoft Office SharePoint Server. È possibile eseguire i passaggi descritti in questo articolo per fornire un&#39;esperienza unificata in modo che gli utenti che si connettono al server di SharePoint possano accedere  AEM Forms Workspace dalla stessa porta.

>[!NOTE]
>
>I passaggi elencati in questo articolo sono specifici di Microsoft SharePoint Server 2007. È inoltre possibile configurare HTML Workspace con altre versioni supportate di Microsoft SharePoint.

## Integrare  AEM Forms Workspace con Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Effettuare le seguenti operazioni per integrare  AEM Forms Workspace in una web part:

1. In un browser Web, andate al sito di SharePoint, ad esempio, `https://[myMOSSserver]:44299/default.aspx` in cui `[myMOSSserver]` è il nome o l&#39;indirizzo IP del server di SharePoint.

   >[!NOTE]
   >
   >44299 è il numero di porta predefinito per il server SharePoint. Il numero di porta dipende dall&#39;installazione di SharePoint Server.

1. In alto a destra nella pagina Web, fare clic su **Azioni del sito** e selezionare **Modifica pagina**.
1. Fare clic sul pulsante **Aggiungi una web part**.
1. Nella finestra di dialogo Aggiungi web part - pagina Web, in Varie, selezionare la web part **Visualizzatore pagina**, quindi fare clic su **Aggiungi**.
1. Nella casella web part Visualizzatore pagina, fare clic su **modifica** e selezionare **Modifica web part condivisa**.

   >[!NOTE]
   >
   >La casella web part Visualizzatore pagina viene visualizzata sotto il pulsante **Aggiungi una web part** su cui si è fatto clic nel passaggio 3, come illustrato nella figura 1:

   ![Casella web part Visualizzatore pagina nel server Microsoft Office SharePoint.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figura 1. - La casella web part Visualizzatore pagina nel server Microsoft Office SharePoint.

1. Nella pagina Visualizzatore pagina, eseguite le seguenti operazioni:

   1. Nella casella Collegamento, digitare l&#39;URL di  AEM Forms Workspace, ad esempio `https://[AEM_forms_Server]:8080/lc/ws` dove `[AEM_forms_Server]` rappresenta l&#39;IP o il nome del server AEM moduli.
   1. Fare clic su **Aspetto** e modificare l&#39;altezza, la larghezza e il titolo in modo da visualizzare l&#39;intera interfaccia utente di Workspace. Ad esempio, potete impostare rispettivamente l&#39;altezza e la larghezza su 6 pollici e 11 pollici.
   1. Fare clic su **Test Link**. Viene visualizzata una nuova finestra del browser Web con Workspace.
   1. (Facoltativo) Fare clic su **Layout** e modificare il layout di Workspace nella web part.
   1. (Facoltativo) Fare clic su **Avanzate** e modificare altre impostazioni, ad esempio la descrizione e se Workspace può essere ridotto a icona o chiuso nella web part.

      Fare clic su **Applica**.

1. Fare clic su **Esci da modalità di modifica** e verificare di poter accedere a Workspace.

Dopo aver completato i passaggi precedenti, il sito di SharePoint si presenta come illustrato di seguito (figura 2):

![ AEM Forms Workspace integrato con Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Figura 2 -  AEM Forms Workspace integrato con Microsoft Office SharePoint Server

