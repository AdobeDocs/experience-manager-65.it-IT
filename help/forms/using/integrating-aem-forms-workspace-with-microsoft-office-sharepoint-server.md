---
title: Integrazione dell’area di lavoro AEM forms con Microsoft Office SharePoint Server
seo-title: Integrating AEM forms workspace with Microsoft Office SharePoint Server
description: È possibile integrare AEM area di lavoro dei moduli con Microsoft Office SharePoint Server.
seo-description: You can integrate AEM forms workspace with Microsoft Office SharePoint Server.
uuid: 69d51bdf-729f-4eea-8fae-1e2b8aacaae6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8990b422-f4f6-4080-871a-33cdf7ca6455
docset: aem65
exl-id: d080932f-d5fb-482d-9329-62da5df10362
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Integrazione dell’area di lavoro AEM forms con Microsoft Office SharePoint Server{#integrating-aem-forms-workspace-with-microsoft-office-sharepoint-server}

**- Requisiti**

**Conoscenze preliminari**
Prima di poter aggiungere AEM Forms Workspace a SharePoint Server, è necessario disporre dell’accesso a SharePoint Server con i privilegi appropriati e conoscere l’URL per accedere a Workspace. I passaggi seguenti presuppongono la conoscenza di SharePoint Server. Per ulteriori informazioni sulle web part in SharePoint Server, vedere web part in Windows SharePoint Services.

**Livello utente**
Inizio

È possibile utilizzare AEM Forms Workspace come web part in Microsoft Office SharePoint Server (ad esempio, Microsoft Office SharePoint Server 2007). Gli utenti possono accedere ad AEM Forms Workspace collegandosi al server SharePoint utilizzando un browser web per fornire un’esperienza unificata. In questo articolo vengono illustrati i passaggi di base per visualizzare AEM Forms Workspace as a Web Part in Microsoft Office SharePoint Server. Puoi eseguire i passaggi descritti in questo articolo per fornire un’esperienza unificata affinché gli utenti che si connettono al server SharePoint possano accedere ad AEM Forms Workspace dalla stessa porta.

>[!NOTE]
>
>I passaggi elencati in questo articolo sono specifici di Microsoft SharePoint Server 2007. È inoltre possibile configurare HTML Workspace con altre versioni supportate di Microsoft SharePoint.

## Integrare AEM Forms Workspace con Microsoft Office SharePoint Server 2007 {#integrate-aem-forms-workspace-with-microsoft-office-sharepoint-server}

Per integrare AEM Forms Workspace in una web part, effettua le seguenti operazioni:

1. In un browser web, accedi al sito SharePoint, ad esempio: `https://[myMOSSserver]:44299/default.aspx` dove `[myMOSSserver]` è il nome o l’indirizzo IP del server Sharepoint.

   >[!NOTE]
   >
   >44299 è il numero di porta predefinito per il server SharePoint. Il numero di porta dipende dall&#39;installazione di SharePoint Server.

1. In alto a destra della pagina web, fai clic su **Azioni sul sito** e seleziona **Modifica pagina**.
1. Fai clic sul pulsante **Aggiungere una web part** pulsante .
1. Nella finestra di dialogo Aggiungi web part - pagina Web, in Varie, selezionare **web part Visualizzatore pagine** quindi fai clic su **Aggiungi**.
1. Nella casella web part Visualizzatore pagina fare clic su **modifica** e seleziona **Modifica web part condivisa**.

   >[!NOTE]
   >
   >La casella web part Visualizzatore pagina viene visualizzata sotto **Aggiungere una web part** pulsante su cui hai fatto clic al punto 3, come illustrato nella figura 1:

   ![Casella web part Visualizzatore pagine nel server SharePoint di Microsoft Office.](assets/page-viewer-web-part-box-in-microsoft-office-sharepoint-server.png)

   Figura 1. - La casella web part Visualizzatore pagina nel server SharePoint di Microsoft Office.

1. Nella pagina Visualizzatore pagina, esegui le seguenti operazioni:

   1. Nella casella Collegamento, digita l’URL di AEM Forms Workspace, ad esempio `https://[AEM_forms_Server]:8080/lc/ws` dove `[AEM_forms_Server]` rappresenta l’IP o il Nome del server dei moduli AEM.
   1. Fai clic su **Aspetto** e modificare l&#39;altezza, la larghezza e il titolo in modo da visualizzare l&#39;intera interfaccia utente di Workspace. Ad esempio, è possibile impostare altezza e larghezza rispettivamente a 6 pollici e 11 pollici.
   1. Fai clic su **Collegamento test**. Viene visualizzata una nuova finestra del browser Web in cui è visualizzato Workspace.
   1. (Facoltativo) Fai clic su **Layout** e modificare il layout di Workspace nella web part.
   1. (Facoltativo) Fai clic su **Avanzate** e modificare altre impostazioni, ad esempio la descrizione e se Workspace può essere ridotto a icona o chiuso nella web part.

      Fai clic su **Applica**.

1. Fai clic su **Esci da modalità Modifica** e verifica di poter accedere a Workspace.

Dopo aver completato i passaggi precedenti, il sito SharePoint si presenta come nella figura 2:

![AEM Forms Workspace integrato con Microsoft Office SharePoint Server](assets/aem-forms-workspace.jpg)

Figura 2 - AEM Forms Workspace integrato con Microsoft Office SharePoint Server
