---
title: Tipi di endpoint
description: Scopri i diversi tipi di endpoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Tipi di endpoint {#types-of-endpoints}

Prima di poter utilizzare un servizio, è necessario configurare e abilitare un endpoint. Un endpoint specifica la modalità di chiamata di un servizio.

>[!NOTE]
>
>In Workbench, gli endpoint sono denominati punti iniziali.

Ai servizi è possibile aggiungere i seguenti tipi di endpoint. Non tutti i servizi supportano tutti gli endpoint:

**E-mail:** Consente a un utente di richiamare un servizio inviando un messaggio e-mail con uno o più file allegati a un account e-mail specificato. Prima di configurare un endpoint e-mail, è necessario configurare gli account e-mail richiesti. Consulta Configurazione degli endpoint e-mail.

**Cartella controllata:** Consente a un utente di richiamare un servizio inserendo un file in una cartella che viene analizzata a un intervallo definito. Consulta Configurazione degli endpoint per cartelle controllate.

**TaskManager:** Consente a un utente di Workspace di richiamare il servizio.

**Remoting:** Consente a un’applicazione creata con Flex di richiamare il servizio utilizzando i moduli AEM Remoting (obsoleti per i moduli AEM). Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

**SOAP:** Consente a un&#39;applicazione client sviluppata utilizzando le API di programmazione dei moduli AEM di richiamare il servizio utilizzando la modalità SOAP. Per ogni servizio attivato viene creato automaticamente un endpoint SOAP.

**nota**: *La protezione può essere rimossa dai documenti di protezione dei documenti quando si utilizza l’endpoint SOAP durante la visualizzazione dei documenti in Adobe Acrobat o Adobe Reader. Per informazioni dettagliate su come disattivare gli endpoint SOAP nei documenti LCRM, vedi [Disabilita endpoint SOAP per documenti di protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** Consente a un’applicazione client sviluppata utilizzando le API di programmazione dei moduli AEM di richiamare il servizio utilizzando la modalità Enterprise JavaBeans (EJB). Per ogni servizio attivato viene creato automaticamente un endpoint EJB.

**WSDL:** Consente a un&#39;applicazione client sviluppata utilizzando le API di programmazione dei moduli AEM di richiamare il servizio utilizzando WSDL (Web Service Definition Language). La pagina Configurazioni di base contiene un’opzione per abilitare la generazione WSDL per tutti i servizi che fanno parte dei moduli AEM. Consulta Configurare le impostazioni generali dei moduli AEM.

**REST:** I processi creati in Workbench possono essere configurati in modo da poterli richiamare tramite richieste REST (Managational State Transfer). Le richieste REST vengono inviate dalle pagine di HTML. In altre parole, è possibile richiamare un processo di moduli AEM direttamente da una pagina web utilizzando una richiesta REST.

Gli endpoint E-mail, TaskManager, Cartella controllata e Remoting espongono solo un’operazione specifica del servizio. L&#39;aggiunta di questi endpoint richiede un secondo passaggio di configurazione per selezionare un metodo per richiamare il servizio, impostare i parametri di configurazione e specificare le mappature dei parametri di input e output.
