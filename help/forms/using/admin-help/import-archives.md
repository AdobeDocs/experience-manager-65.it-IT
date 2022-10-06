---
title: Importare e gestire archivi
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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Importare e gestire archivi {#import-and-manage-archives}

Utilizza la scheda archivi per importare e gestire gli LCA creati in workbench.

## Importare un archivio {#import-an-archive}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni e fare clic sulla scheda archivi.
1. Fai clic su Importa.
1. Fare clic su Sfoglia per individuare l&#39;archivio da importare, quindi fare clic su Anteprima.
1. Esaminare l&#39;elenco delle risorse e degli oggetti che verranno installati con l&#39;archivio. Assicurati che non ci siano conflitti con le risorse, gli oggetti e le configurazioni di servizio esistenti, perché non è disponibile alcuna funzionalità di annullamento.

   Se si sceglie di importare le configurazioni del servizio, AEM forms importa tutti i file di configurazione del processo (endpoint, profili di sicurezza e parametri di configurazione del servizio) utilizzati dai processi in LCA.

1. Fai clic su Importa.
1. Esamina i risultati dell’importazione e fai clic su Ignora configurazione per completare il processo di importazione oppure fai clic su Configura per configurare l’archivio.

   >[!NOTE]
   >
   >Se fai clic su Ignora configurazione, puoi configurare l&#39;archivio in un secondo momento.

1. Se si fa clic su Configura, viene visualizzata la pagina Configura endpoint, in cui è possibile apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fare clic su di esso.
   * Per aggiungere un endpoint Task Manager, fare clic su Aggiungi TaskManager. Per informazioni dettagliate sulle impostazioni di Gestione attività, consulta [Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint per cartelle controllate, fare clic su Aggiungi cartella osservata. Per informazioni dettagliate sulle impostazioni delle cartelle esaminate, consulta [Impostazioni dell’endpoint della cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fare clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni E-mail, consulta [Impostazioni dell’endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fai clic su Aggiungi EJB e specifica un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint SOAP, fare clic su Aggiungi SOAP e specificare un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint Remoting, fare clic su Aggiungi Remoting. Per informazioni dettagliate sulle impostazioni Remoting, vedere [Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fai clic su Aggiungi REST e specifica un nome e una descrizione per l’endpoint. Osserva l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, selezionare la casella di controllo accanto ad esso e fare clic su Rimuovi.

1. Fai clic su Avanti.
1. Se in un processo o in un servizio LCA sono presenti parametri di configurazione, viene visualizzata una pagina Configura parametri in cui configurare i parametri del servizio e fare clic su Avanti.
1. Nella pagina Configura profilo di protezione , apporta le modifiche necessarie:

   * **Richiedi ai chiamanti di autenticare:** Questa impostazione indica se il servizio può essere richiamato con o senza credenziali.

      Se *I chiamanti sono attualmente tenuti ad autenticarsi* è visualizzato, il chiamante del servizio deve essere autenticato e l&#39;entità utente per tale chiamante deve essere autorizzata a richiamare il servizio; altrimenti, il tentativo di invocazione verrà rifiutato. Per rimuovere la necessità di autenticare, fare clic su Consenti chiamanti non autenticati.

      Se *I chiamanti non sono tenuti ad autenticarsi* non è necessario autenticare il chiamante del servizio. L&#39;invocazione del servizio avrà sempre successo perché non vi è alcun controllo di autorizzazione. Per richiedere l’autenticazione, fare clic su Richiedi ai chiamanti di eseguire l’autenticazione.

   * **Esegui come:** Specifica l&#39;identità di esecuzione utilizzata da un servizio dopo che è stato richiamato. Per modificare questa opzione, fare clic su Cambia. Scegli tra le seguenti opzioni:

      **Non specificato:** Viene utilizzato il comportamento predefinito.

      **Richiedente:** Utilizza la stessa identità dell’utente che ha richiamato il servizio.

      **Sistema:** Esegue il servizio con privilegi completi. Questa è l’impostazione predefinita per i processi a lunga durata.

      **Utente con nome:** Consente di eseguire il servizio come utente specifico. Questa è l’impostazione predefinita per i processi di breve durata. Quando selezioni questa opzione, fai clic su Seleziona utente per visualizzare la pagina Seleziona principale , in cui puoi cercare e selezionare l&#39;utente.

   * Per aggiungere un&#39;entità al profilo di sicurezza, fai clic su Aggiungi entità e seleziona l&#39;utente o il gruppo da aggiungere come entità principale. Fare clic su Avanti, quindi selezionare le autorizzazioni che si desidera assegnare all&#39;entità:

      **INVOKE_PERM:** Per richiamare tutte le operazioni sul servizio

      **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio

      **SUPERVISOR_PERM:** Per visualizzare i dati delle istanze del processo per un servizio creato da un processo

      **START_STOP_PERM:** Per avviare e interrompere un servizio

      **ADD_REMOVE_ENDPOINTS_PERM:** Aggiunta, rimozione e modifica degli endpoint di un servizio

      **CREATE_VERSION_PERM:** Per creare una nuova versione del servizio

      **DELETE_VERSION_PERM:** Per eliminare una versione del servizio

      **MODIFY_VERSION_PERM:** Per modificare una versione del servizio

      **READ_PERM:** Per visualizzare il servizio

      Fai clic su Completato per aggiungere l&#39;entità al profilo di sicurezza.

1. Fai clic su Completato per completare la configurazione.

## Configurare i moduli AEM che fanno parte di un file di archivio {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni e fare clic sulla scheda archivi.
1. Nella pagina Gestione archivio selezionare il file di archivio da configurare.
1. Nella pagina Visualizza archivio , seleziona la risorsa di archivio evidenziata.
1. Configura il file di archivio del processo importato.

## Utilizzare la procedura guidata di configurazione per configurare i moduli AEM che fanno parte di un file di archivio {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni e fare clic sulla scheda archivi.
1. Fai clic su Configura accanto al file di archivio da configurare.
1. Viene visualizzata la pagina Configura endpoint , che consente di apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fare clic su di esso.
   * Per aggiungere un endpoint Task Manager, fare clic su Aggiungi TaskManager. Per informazioni dettagliate sulle impostazioni di Gestione attività, consulta [Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint per cartelle controllate, fare clic su Aggiungi cartella osservata. Per informazioni dettagliate sulle impostazioni delle cartelle esaminate, consulta [Impostazioni dell’endpoint della cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fare clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni E-mail, consulta [Impostazioni dell’endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fai clic su Aggiungi EJB e specifica un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint SOAP, fare clic su Aggiungi SOAP e specificare un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint Remoting, fare clic su Aggiungi Remoting. Per informazioni dettagliate sulle impostazioni Remoting, vedere [Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fai clic su Aggiungi REST e specifica un nome e una descrizione per l’endpoint. Osserva l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, selezionare la casella di controllo accanto ad esso e fare clic su Rimuovi.

1. Fai clic su Avanti.
1. Se in un processo o in un servizio LCA sono presenti parametri di configurazione, viene visualizzata una pagina Configura parametri in cui configurare i parametri del servizio e fare clic su Avanti.
1. Nella pagina Configura profilo di protezione puoi apportare le modifiche necessarie:

   * **Richiedi ai chiamanti di autenticare:** Questa impostazione indica se il servizio può essere richiamato con o senza credenziali.

      Se *I chiamanti sono attualmente tenuti ad autenticarsi* è visualizzato, il chiamante del servizio deve essere autenticato e l&#39;entità utente per tale chiamante deve essere autorizzata a richiamare il servizio; altrimenti, il tentativo di invocazione verrà rifiutato. Per rimuovere la necessità di autenticare, fare clic su Consenti chiamanti non autenticati.

      Se *I chiamanti non sono tenuti ad autenticarsi* viene visualizzato, il chiamante del servizio potrebbe essere autenticato o meno. L&#39;invocazione del servizio avrà sempre successo perché non vi è alcun controllo di autorizzazione. Per richiedere l’autenticazione, fare clic su Richiedi ai chiamanti di eseguire l’autenticazione.

   * **Esegui come:** Specifica l&#39;identità di esecuzione utilizzata da un servizio dopo che è stato richiamato. Per modificare questa opzione, fare clic su Cambia. Scegli tra le seguenti opzioni:

      **Non specificato:** Viene utilizzato il comportamento predefinito.

      **Richiedente:** Utilizza la stessa identità dell’utente che ha richiamato il servizio.

      **Sistema:** Esegue il servizio con privilegi completi. Questa è l’impostazione predefinita per i processi a lunga durata.

      **Utente con nome:** Consente di eseguire il servizio come utente specifico. Questa è l’impostazione predefinita per i processi di breve durata. Quando selezioni questa opzione, fai clic su Seleziona utente per visualizzare la pagina Seleziona principale , in cui puoi cercare e selezionare l&#39;utente.

   * Per aggiungere un&#39;entità al profilo di sicurezza, fai clic su Aggiungi entità e seleziona l&#39;utente o il gruppo da aggiungere come entità principale. Fare clic su Avanti, quindi selezionare le autorizzazioni che si desidera assegnare all&#39;entità:

      **INVOKE_PERM:** Per richiamare tutte le operazioni sul servizio

      **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio

      **SUPERVISOR_PERM:** Per visualizzare i dati delle istanze del processo per un servizio creato da un processo

      **START_STOP_PERM:** Per avviare e interrompere un servizio

      **ADD_REMOVE_ENDPOINTS_PERM:** Aggiunta, rimozione e modifica degli endpoint di un servizio

      **CREATE_VERSION_PERM:** Per creare una nuova versione del servizio

      **DELETE_VERSION_PERM:** Per eliminare una versione del servizio

      **MODIFY_VERSION_PERM:** Per modificare una versione del servizio

      **READ_PERM:** Per visualizzare il servizio

      Fai clic su Completato per aggiungere l&#39;entità al profilo di sicurezza.

## Rimuovere un archivio {#remove-an-archive}

>[!NOTE]
>
>Per rimuovere un archivio contenente risorse archiviate in un archivio di terze parti (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager), è necessario eliminare i file di risorse dal repository utilizzando Workbench.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione archivio.
1. Nella pagina Gestione archivio selezionare la casella di controllo dell&#39;archivio da rimuovere e fare clic su Rimuovi.
