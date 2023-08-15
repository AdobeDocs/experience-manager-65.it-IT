---
title: Importare e gestire gli archivi
seo-title: Import and manage archives
description: Scopri come importare e gestire gli archivi.
seo-description: Learn how to import and manage archives.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 0%

---

# Importare e gestire gli archivi {#import-and-manage-archives}

Utilizza la scheda Archivi per importare e gestire gli LCA creati in Workbench.

## Importare un archivio {#import-an-archive}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni, quindi fare clic sulla scheda Archivi.
1. Fai clic su Importa.
1. Fare clic su Sfoglia per individuare l&#39;archivio da importare e quindi fare clic su Anteprima.
1. Esaminare l&#39;elenco delle risorse e degli oggetti che verranno installati con l&#39;archivio. Assicurati che non vi siano conflitti con le risorse, gli oggetti e le configurazioni di servizio esistenti, perché non è disponibile alcuna funzionalità di annullamento.

   Se si sceglie di importare le configurazioni del servizio, i moduli AEM importano tutti i file di configurazione del processo (endpoint, profili di sicurezza e parametri di configurazione del servizio) utilizzati dai processi nell&#39;LCA.

1. Fai clic su Importa.
1. Esaminare i risultati dell&#39;importazione e fare clic su Ignora configurazione per completare il processo di importazione oppure fare clic su Configura per configurare l&#39;archivio.

   >[!NOTE]
   >
   >Se fai clic su Ignora configurazione, puoi configurare l’archivio in un secondo momento.

1. Se si fa clic su Configura, viene visualizzata la pagina Configura endpoint, in cui è possibile apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fare clic su di esso.
   * Per aggiungere un endpoint Task Manager, fare clic su Aggiungi TaskManager. Per ulteriori informazioni sulle impostazioni di Gestione attività, vedere [Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint di tipo Cartella controllata, fare clic su Aggiungi cartella controllata. Per informazioni dettagliate sulle impostazioni della cartella controllata, vedi [Impostazioni endpoint cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fai clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni e-mail, consulta [Impostazioni endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fare clic su Aggiungi EJB e specificare un nome e una descrizione per l&#39;endpoint.
   * Per aggiungere un endpoint SOAP, fare clic su Aggiungi SOAP e specificare un nome e una descrizione per l&#39;endpoint.
   * Per aggiungere un endpoint remoto, fare clic su Aggiungi remoto. Per ulteriori informazioni sulle impostazioni di comunicazione remota, vedere [Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fai clic su Aggiungi REST e specifica un nome e una descrizione per l’endpoint. Osserva l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, selezionare la casella di controllo accanto a esso e fare clic su Rimuovi.

1. Fai clic su Avanti.
1. Se un processo o un servizio nella LCA dispone di parametri di configurazione, viene visualizzata la pagina Configura parametri, in cui è possibile configurare i parametri del servizio e fare clic su Avanti.
1. Nella pagina Configura profilo di sicurezza apportare le modifiche necessarie:

   * **Richiedi autenticazione chiamanti:** Questa impostazione indica se il servizio può essere richiamato con o senza credenziali.

     Se *Al momento è necessario che i chiamanti effettuino l&#39;autenticazione* è visualizzato, il chiamante del servizio deve essere autenticato e l&#39;entità utente principale per quel chiamante deve essere autorizzata a richiamare il servizio; in caso contrario, il tentativo di chiamata verrà rifiutato. Per rimuovere la necessità di autenticazione, fare clic su Consenti chiamanti non autenticati.

     Se *I chiamanti non sono tenuti ad autenticare* , il chiamante del servizio non deve essere autenticato. La chiamata del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione. Per richiedere l&#39;autenticazione, fare clic su Richiedi autenticazione chiamanti.

   * **Esegui come:** Specifica l&#39;identità di runtime utilizzata da un servizio dopo che è stato richiamato. Per modificare questa opzione, fare clic su Cambia. Scegli una delle seguenti opzioni:

     **Non specificato:** Viene utilizzato il comportamento predefinito.

     **Richiamatore:** Utilizza la stessa identità dell’utente che ha richiamato il servizio.

     **Sistema:** Esegue il servizio con privilegi completi. Questa è l&#39;impostazione predefinita per i processi di lunga durata.

     **Utente con nome:** Consente di eseguire il servizio come utente specifico. Questa è l&#39;impostazione predefinita per i processi di breve durata. Quando si seleziona questa opzione, fare clic su Seleziona utente per visualizzare la pagina Seleziona utente principale, in cui è possibile cercare e selezionare l&#39;utente.

   * Per aggiungere un&#39;entità al profilo di sicurezza, fare clic su Aggiungi entità e selezionare l&#39;utente o il gruppo da aggiungere come entità. Fare clic su Avanti e quindi selezionare le autorizzazioni che si desidera assegnare all&#39;entità:

     **INVOKE_PERM:** Per richiamare tutte le operazioni sul servizio

     **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio

     **SUPERVISOR_PERM:** Per visualizzare i dati dell&#39;istanza di processo per un servizio creato da un processo

     **START_STOP_PERM:** Per avviare e arrestare un servizio

     **ADD_REMOVE_ENDPOINTS_PERM:** Per aggiungere, rimuovere e modificare endpoint per un servizio

     **CREATE_VERSION_PERM:** Per creare una nuova versione del servizio

     **DELETE_VERSION_PERM:** Per eliminare una versione del servizio

     **MODIFY_VERSION_PERM:** Per modificare una versione del servizio

     **READ_PERM:** Per visualizzare il servizio

     Fare clic su Fine per aggiungere l&#39;entità al profilo di protezione.

1. Fai clic su Fine per completare la configurazione.

## Configurare i moduli AEM che fanno parte di un file di archivio {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni, quindi fare clic sulla scheda Archivi.
1. Nella pagina Gestione archivio selezionare il file di archivio da configurare.
1. Nella pagina Visualizza archivio selezionare la risorsa di archivio evidenziata.
1. Configurare il file di archivio dei processi importato.

## Utilizzare la configurazione guidata per configurare i moduli AEM che fanno parte di un file di archivio {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni, quindi fare clic sulla scheda Archivi.
1. Fare clic su Configura accanto al file di archivio da configurare.
1. Viene visualizzata la pagina Configura endpoint, in cui è possibile apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fare clic su di esso.
   * Per aggiungere un endpoint Task Manager, fare clic su Aggiungi TaskManager. Per ulteriori informazioni sulle impostazioni di Gestione attività, vedere [Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint di tipo Cartella controllata, fare clic su Aggiungi cartella controllata. Per informazioni dettagliate sulle impostazioni della cartella controllata, vedi [Impostazioni endpoint cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fai clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni e-mail, consulta [Impostazioni endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fare clic su Aggiungi EJB e specificare un nome e una descrizione per l&#39;endpoint.
   * Per aggiungere un endpoint SOAP, fare clic su Aggiungi SOAP e specificare un nome e una descrizione per l&#39;endpoint.
   * Per aggiungere un endpoint remoto, fare clic su Aggiungi remoto. Per ulteriori informazioni sulle impostazioni di comunicazione remota, vedere [Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fai clic su Aggiungi REST e specifica un nome e una descrizione per l’endpoint. Osserva l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, selezionare la casella di controllo accanto a esso e fare clic su Rimuovi.

1. Fai clic su Avanti.
1. Se un processo o un servizio nella LCA dispone di parametri di configurazione, viene visualizzata la pagina Configura parametri, in cui è possibile configurare i parametri del servizio e fare clic su Avanti.
1. Nella pagina Configura profilo di sicurezza è possibile apportare le modifiche necessarie:

   * **Richiedi autenticazione chiamanti:** Questa impostazione indica se il servizio può essere richiamato con o senza credenziali.

     Se *Al momento è necessario che i chiamanti effettuino l&#39;autenticazione* è visualizzato, il chiamante del servizio deve essere autenticato e l&#39;entità utente principale per quel chiamante deve essere autorizzata a richiamare il servizio; in caso contrario, il tentativo di chiamata verrà rifiutato. Per rimuovere la necessità di autenticazione, fare clic su Consenti chiamanti non autenticati.

     Se *I chiamanti non sono tenuti ad autenticare* , il chiamante del servizio potrebbe essere autenticato o meno. La chiamata del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione. Per richiedere l&#39;autenticazione, fare clic su Richiedi autenticazione chiamanti.

   * **Esegui come:** Specifica l&#39;identità di runtime utilizzata da un servizio dopo che è stato richiamato. Per modificare questa opzione, fare clic su Cambia. Scegli una delle seguenti opzioni:

     **Non specificato:** Viene utilizzato il comportamento predefinito.

     **Richiamatore:** Utilizza la stessa identità dell’utente che ha richiamato il servizio.

     **Sistema:** Esegue il servizio con privilegi completi. Questa è l&#39;impostazione predefinita per i processi di lunga durata.

     **Utente con nome:** Consente di eseguire il servizio come utente specifico. Questa è l&#39;impostazione predefinita per i processi di breve durata. Quando si seleziona questa opzione, fare clic su Seleziona utente per visualizzare la pagina Seleziona utente principale, in cui è possibile cercare e selezionare l&#39;utente.

   * Per aggiungere un&#39;entità al profilo di sicurezza, fare clic su Aggiungi entità e selezionare l&#39;utente o il gruppo da aggiungere come entità. Fare clic su Avanti e quindi selezionare le autorizzazioni che si desidera assegnare all&#39;entità:

     **INVOKE_PERM:** Per richiamare tutte le operazioni sul servizio

     **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio

     **SUPERVISOR_PERM:** Per visualizzare i dati dell&#39;istanza di processo per un servizio creato da un processo

     **START_STOP_PERM:** Per avviare e arrestare un servizio

     **ADD_REMOVE_ENDPOINTS_PERM:** Per aggiungere, rimuovere e modificare endpoint per un servizio

     **CREATE_VERSION_PERM:** Per creare una nuova versione del servizio

     **DELETE_VERSION_PERM:** Per eliminare una versione del servizio

     **MODIFY_VERSION_PERM:** Per modificare una versione del servizio

     **READ_PERM:** Per visualizzare il servizio

     Fare clic su Fine per aggiungere l&#39;entità al profilo di protezione.

## Rimuovere un archivio {#remove-an-archive}

>[!NOTE]
>
>Per rimuovere un archivio contenente risorse memorizzate in un repository di terze parti (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager), è necessario eliminare anche i file delle risorse dal repository mediante Workbench.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione archivio.
1. Nella pagina Gestione archivio selezionare la casella di controllo relativa all&#39;archivio da rimuovere e fare clic su Rimuovi.
