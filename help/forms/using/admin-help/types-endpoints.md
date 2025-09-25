---
title: Tipi di endpoint
description: Scopri i diversi tipi di endpoint. Puoi aggiungere ai servizi diversi tipi di endpoint, quali E-mail, Cartella controllata e molti altri ancora.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '455'
ht-degree: 100%

---

# Tipi di endpoint {#types-of-endpoints}

Prima di poter utilizzare un servizio, devi configurare e abilitare un endpoint. Un endpoint specifica la modalità con cui viene richiamato un servizio.

>[!NOTE]
>
>In Workbench, gli endpoint sono denominati punti iniziali.

È possibile aggiungere ai servizi i seguenti tipi di endpoint. Non tutti i servizi supportano tutti gli endpoint:

**E-mail:** consente a un utente di richiamare un servizio inviando un messaggio e-mail con uno o più file allegati a un account e-mail specificato. Prima di configurare un endpoint e-mail, devi configurare gli account e-mail richiesti. Consulta Configurare gli endpoint e-mail.

**Cartella controllata:** consente a un utente di richiamare un servizio inserendo un file in una cartella, che viene analizzata con una cadenza definita. Consulta Configurare gli endpoint cartella controllata.

**TaskManager:** consente a un utente di Workspace di richiamare il servizio.

**Remoting:** consente a un’applicazione generata con Flex di richiamare il servizio utilizzando AEM Forms Remoting (obsoleto per AEM Forms). Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell’endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

**SOAP:** consente a un’applicazione client sviluppata con le API di programmazione di AEM Forms di richiamare il servizio utilizzando la modalità SOAP. Per ogni servizio attivato viene creato automaticamente un endpoint SOAP.

**Nota**: *è possibile rimuovere la protezione dai documenti di protezione dei documenti quando l’endpoint SOAP viene utilizzato durante la visualizzazione dei documenti in Adobe Acrobat o Adobe Reader. Per informazioni dettagliate su come disabilitare gli endpoint SOAP nei documenti LCRM, consulta [Disabilitare gli endpoint SOAP per i documenti di protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** abilita un’applicazione client sviluppata utilizzando le API di programmazione di AEM Forms per richiamare il servizio utilizzando la modalità Enterprise JavaBeans (EJB). Per ogni servizio attivato viene creato automaticamente un endpoint EJB.

**WSDL:** consente a un’applicazione client sviluppata utilizzando le API di programmazione di AEM Forms di richiamare il servizio utilizzando il linguaggio WSDL (Web Service Definition Language). La pagina Configurazioni core contiene un’opzione per abilitare la generazione WSDL per tutti i servizi che fanno parte di AEM Forms. Consulta Configurare le impostazioni generali di AEM Forms.

**REST:** i processi creati in Workbench possono essere configurati per consentirti di richiamarli con richieste Representational State Transfer (REST). Le richieste REST vengono inviate dalle pagine HTML. In altri termini puoi richiamare un processo AEM Forms direttamente da una pagina web utilizzando una richiesta REST.

Gli endpoint E-mail, TaskManager, Cartella controllata e Remoting rendono disponibile solo un’operazione specifica del servizio. L’aggiunta di questi endpoint richiede un secondo passaggio di configurazione, con la selezione di un metodo per richiamare il servizio, impostare i parametri di configurazione e specificare le mappature dei parametri di input e output.
