---
title: Tipi di endpoint
seo-title: Tipi di endpoint
description: Scopri i diversi tipi di endpoint.
seo-description: Scopri i diversi tipi di endpoint.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Tipi di endpoint {#types-of-endpoints}

Prima di poter utilizzare un servizio, devi configurare e abilitare un endpoint. Un endpoint specifica la modalità di chiamata di un servizio.

>[!NOTE]
>
>In Workbench, gli endpoint sono denominati punti di inizio.

I seguenti tipi di endpoint possono essere aggiunti ai servizi. Non tutti i servizi supportano tutti gli endpoint:

**E-mail:** consente a un utente di richiamare un servizio inviando un messaggio e-mail contenente uno o più file allegati a un account e-mail specificato. Prima di configurare un endpoint e-mail, dovete configurare gli account e-mail richiesti. Consultate Configurazione degli endpoint e-mail.

**Cartella esaminata:** consente a un utente di richiamare un servizio inserendo un file in una cartella, che viene analizzata a un intervallo definito. Consultate Configurazione degli endpoint delle cartelle controllati.

**TaskManager:** consente a un utente di Workspace di richiamare il servizio.

**Remoto:** consente a un&#39;applicazione creata con Flex di richiamare il servizio utilizzando (obsoleto per i moduli AEM) AEM moduli Remoting. Per ogni servizio attivato viene automaticamente creato un endpoint remoto. Una destinazione Flex con lo stesso nome dell&#39;endpoint viene creata e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare le operazioni sul servizio appropriato.

**SOAP:** consente a un&#39;applicazione client sviluppata utilizzando le API di programmazione AEM moduli di richiamare il servizio utilizzando la modalità SOAP. Viene creato automaticamente un endpoint SOAP per ciascun servizio attivato.

**nota**:  *La protezione può essere rimossa dai documenti di protezione quando viene utilizzato l&#39;endpoint SOAP durante la visualizzazione dei documenti in  Adobe Acrobat o  Adobe Reader. Per informazioni dettagliate su come disabilitare gli endpoint SOAP nei documenti LCRM, vedere [Disattivazione degli endpoint SOAP per i documenti di protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** consente a un&#39;applicazione client sviluppata utilizzando le API di programmazione AEM moduli di richiamare il servizio utilizzando la modalità Enterprise JavaBeans (EJB). Viene creato automaticamente un endpoint EJB per ciascun servizio attivato.

**WSDL:** consente a un&#39;applicazione client sviluppata utilizzando le API di programmazione AEM moduli di richiamare il servizio utilizzando il linguaggio WSDL (Web Service Definition Language). La pagina Configurazioni di base contiene un&#39;opzione per abilitare la generazione WSDL per tutti i servizi che fanno parte di moduli AEM. (Vedere Configurare le impostazioni generali AEM moduli.)

**REST:** I processi creati in Workbench possono essere configurati in modo da poterli richiamare tramite richieste REST (Rappresenta State Transfer). Le richieste REST vengono inviate dalle pagine HTML. In altre parole, è possibile richiamare un processo AEM moduli direttamente da una pagina Web utilizzando una richiesta REST.

Gli endpoint E-mail, TaskManager, Cartella esaminata e Remoting mostrano solo un&#39;operazione specifica del servizio. L&#39;aggiunta di questi endpoint richiede un secondo passaggio di configurazione per selezionare un metodo per richiamare il servizio, impostare i parametri di configurazione e specificare le mappature dei parametri di input e output.
