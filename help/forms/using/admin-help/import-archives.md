---
title: Importare e gestire gli archivi
seo-title: Importare e gestire gli archivi
description: Scopri come importare e gestire gli archivi.
seo-description: Scopri come importare e gestire gli archivi.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 0%

---


# Importazione e gestione di archivi {#import-and-manage-archives}

Utilizzare la scheda archivi per importare e gestire gli LCA creati in Workbench.

## Importa un archivio {#import-an-archive}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazione e fare clic sulla scheda archivi.
1. Fai clic su Importa.
1. Fate clic su Sfoglia per individuare l’archivio da importare, quindi fate clic su Anteprima.
1. Esaminare l&#39;elenco delle risorse e degli oggetti che verranno installati con l&#39;archivio. Verificare che non vi siano conflitti con le risorse, gli oggetti e le configurazioni di servizio esistenti, poiché non è disponibile alcuna funzionalità di annullamento.

   Se si sceglie di importare le configurazioni del servizio, AEM moduli importa tutti i file di configurazione del processo (endpoint, profili di sicurezza e parametri di configurazione del servizio) utilizzati dai processi in LCA.

1. Fai clic su Importa.
1. Controllate i risultati dell&#39;importazione e fate clic su Ignora configurazione per completare il processo di importazione oppure fate clic su Configura per configurare l&#39;archivio.

   >[!NOTE]
   >
   >Se fate clic su Ignora configurazione, potete configurare l&#39;archivio in un secondo momento.

1. Se si fa clic su Configura, viene visualizzata la pagina Configura endpoint, in cui è possibile apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fate clic su di esso.
   * Per aggiungere un endpoint di Task Manager, fare clic su Aggiungi TaskManager. Per informazioni dettagliate sulle impostazioni di Task Manager, vedere [Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint cartella esaminata, fate clic su Aggiungi cartella esaminata. Per informazioni dettagliate sulle impostazioni delle cartelle esaminate, consultate [Impostazioni endpoint cartella esaminata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fate clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni E-mail, vedere [Impostazioni endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fate clic su Aggiungi EJB e specificate un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint SOAP, fare clic su Aggiungi SOAP e specificare un nome e una descrizione per l&#39;endpoint.
   * Per aggiungere un endpoint remoto, fare clic su Aggiungi remoto. Per informazioni dettagliate sulle impostazioni Remoto, vedere [Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fate clic su Aggiungi REST e specificate un nome e una descrizione per l’endpoint. Osservate l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, selezionate la casella di controllo accanto ad esso e fate clic su Rimuovi.

1. Fai clic su Avanti.
1. Se un processo o un servizio in LCA dispone di parametri di configurazione, viene visualizzata una pagina Configura parametri, in cui si configurano i parametri del servizio e si fa clic su Avanti.
1. Nella pagina Configura profilo di protezione, apportate le modifiche necessarie:

   * **Richiedi che i chiamanti autenticino:** questa impostazione indica se il servizio può essere invocato con o senza credenziali.

      Se *i chiamanti sono attualmente richiesti per l&#39;autenticazione* viene visualizzato, il chiamante del servizio deve essere autenticato e l&#39;entità utente per tale chiamante deve essere autorizzata a richiamare il servizio; in caso contrario, il tentativo di chiamata verrà rifiutato. Per rimuovere la necessità di autenticazione, fare clic su Consenti chiamanti non autenticati.

      Se *I chiamanti non sono richiesti per l&#39;autenticazione* viene visualizzato, il chiamante del servizio non deve essere autenticato. L&#39;invocazione del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione. Per richiedere l&#39;autenticazione, fai clic su Richiedi ai chiamanti di eseguire l&#39;autenticazione.

   * **Esecuzione come:** specifica l&#39;identità di esecuzione utilizzata da un servizio dopo che questo è stato richiamato. Per modificare questa opzione, fate clic su Cambia. Scegliete tra le seguenti opzioni:

      **Non specificato:** viene utilizzato il comportamento predefinito.

      **Invoker:** utilizza la stessa identità dell&#39;utente che ha richiamato il servizio.

      **Sistema:** esegue il servizio con privilegi completi. Questa è l&#39;impostazione predefinita per i processi di lunga durata.

      **Utente denominato:** consente di eseguire il servizio come utente specifico. Questa è l&#39;impostazione predefinita per i processi di breve durata. Quando selezionate questa opzione, fate clic su Seleziona utente per visualizzare la pagina Seleziona principale, in cui potete cercare e selezionare l&#39;utente.

   * Per aggiungere un&#39;entità al profilo di sicurezza, fate clic su Aggiungi entità e selezionate l&#39;utente o il gruppo da aggiungere come entità. Fate clic su Avanti, quindi selezionate le autorizzazioni da assegnare all&#39;entità:

      **INVOKE_PERM:** Richiamare tutte le operazioni sul servizio

      **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio

      **SUPERVISOR_PERM:** Per visualizzare i dati dell&#39;istanza di processo per un servizio creato da un processo

      **START_STOP_PERM:** Per avviare e arrestare un servizio

      **ADD_REMOVE_ENDPOINTS_PERM:** Aggiunta, rimozione e modifica di endpoint per un servizio

      **CREATE_VERSION_PERM:** Per creare una nuova versione del servizio

      **DELETE_VERSION_PERM:** Per eliminare una versione del servizio

      **MODIFY_VERSION_PERM:** Per modificare una versione del servizio

      **READ_PERM:** Visualizzazione del servizio

      Fare clic su Finito per aggiungere l&#39;entità al profilo di protezione.

1. Fate clic su Completato per completare la configurazione.

## Configurare i moduli AEM che fanno parte di un file di archivio {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazione e fare clic sulla scheda archivi.
1. Nella pagina Gestione archivio, selezionare il file di archivio da configurare.
1. Nella pagina Visualizza archivio, selezionare la risorsa di archivio evidenziata.
1. Configurare il file di archivio del processo importato.

## Utilizzare la procedura guidata di configurazione per configurare i moduli AEM che fanno parte di un file di archivio {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazione e fare clic sulla scheda archivi.
1. Fare clic su Configura accanto al file di archivio da configurare.
1. Viene visualizzata la pagina Configura endpoint, in cui è possibile apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fate clic su di esso.
   * Per aggiungere un endpoint di Task Manager, fare clic su Aggiungi TaskManager. Per informazioni dettagliate sulle impostazioni di Task Manager, vedere [Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint cartella esaminata, fate clic su Aggiungi cartella esaminata. Per informazioni dettagliate sulle impostazioni delle cartelle esaminate, consultate [Impostazioni endpoint cartella esaminata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fate clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni E-mail, vedere [Impostazioni endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fate clic su Aggiungi EJB e specificate un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint SOAP, fare clic su Aggiungi SOAP e specificare un nome e una descrizione per l&#39;endpoint.
   * Per aggiungere un endpoint remoto, fare clic su Aggiungi remoto. Per informazioni dettagliate sulle impostazioni Remoto, vedere [Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fate clic su Aggiungi REST e specificate un nome e una descrizione per l’endpoint. Osservate l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, selezionate la casella di controllo accanto ad esso e fate clic su Rimuovi.

1. Fai clic su Avanti.
1. Se un processo o un servizio in LCA dispone di parametri di configurazione, viene visualizzata una pagina Configura parametri, in cui si configurano i parametri del servizio e si fa clic su Avanti.
1. Nella pagina Configura profilo di protezione, puoi apportare le modifiche necessarie:

   * **Richiedi che i chiamanti autenticino:** questa impostazione indica se il servizio può essere invocato con o senza credenziali.

      Se *i chiamanti sono attualmente richiesti per l&#39;autenticazione* viene visualizzato, il chiamante del servizio deve essere autenticato e l&#39;entità utente per tale chiamante deve essere autorizzata a richiamare il servizio; in caso contrario, il tentativo di chiamata verrà rifiutato. Per rimuovere la necessità di autenticazione, fare clic su Consenti chiamanti non autenticati.

      Se *I chiamanti non sono tenuti ad autenticare* viene visualizzato, il chiamante del servizio potrebbe essere autenticato o meno. L&#39;invocazione del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione. Per richiedere l&#39;autenticazione, fai clic su Richiedi ai chiamanti di eseguire l&#39;autenticazione.

   * **Esecuzione come:** specifica l&#39;identità di esecuzione utilizzata da un servizio dopo che questo è stato richiamato. Per modificare questa opzione, fate clic su Cambia. Scegliete tra le seguenti opzioni:

      **Non specificato:** viene utilizzato il comportamento predefinito.

      **Invoker:** utilizza la stessa identità dell&#39;utente che ha richiamato il servizio.

      **Sistema:** esegue il servizio con privilegi completi. Questa è l&#39;impostazione predefinita per i processi di lunga durata.

      **Utente denominato:** consente di eseguire il servizio come utente specifico. Questa è l&#39;impostazione predefinita per i processi di breve durata. Quando selezionate questa opzione, fate clic su Seleziona utente per visualizzare la pagina Seleziona principale, in cui potete cercare e selezionare l&#39;utente.

   * Per aggiungere un&#39;entità al profilo di sicurezza, fate clic su Aggiungi entità e selezionate l&#39;utente o il gruppo da aggiungere come entità. Fate clic su Avanti, quindi selezionate le autorizzazioni da assegnare all&#39;entità:

      **INVOKE_PERM:** Richiamare tutte le operazioni sul servizio

      **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio

      **SUPERVISOR_PERM:** Per visualizzare i dati dell&#39;istanza di processo per un servizio creato da un processo

      **START_STOP_PERM:** Per avviare e arrestare un servizio

      **ADD_REMOVE_ENDPOINTS_PERM:** Aggiunta, rimozione e modifica di endpoint per un servizio

      **CREATE_VERSION_PERM:** Per creare una nuova versione del servizio

      **DELETE_VERSION_PERM:** Per eliminare una versione del servizio

      **MODIFY_VERSION_PERM:** Per modificare una versione del servizio

      **READ_PERM:** Visualizzazione del servizio

      Fare clic su Finito per aggiungere l&#39;entità al profilo di protezione.

## Rimuovere un archivio {#remove-an-archive}

>[!NOTE]
>
>Per rimuovere un archivio contenente le risorse archiviate in un archivio di terze parti (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager), è inoltre necessario eliminare i file di risorse dal repository utilizzando Workbench.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione archivio.
1. Nella pagina Gestione archivio, selezionate la casella di controllo dell&#39;archivio da rimuovere e fate clic su Rimuovi.

