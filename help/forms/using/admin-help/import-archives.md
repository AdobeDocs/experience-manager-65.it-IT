---
title: Importare e gestire gli archivi
description: Scopri come importare e gestire gli archivi. Gli archivi importano e gestiscono gli LCA creati in Workbench. Puoi importare, configurare, utilizzare ed eliminare un archivio.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 100%
---
# Importare e gestire gli archivi {#import-and-manage-archives}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizza la scheda Archivi per importare e gestire gli LCA creati in Workbench.

## Importare un archivio {#import-an-archive}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni, quindi fai clic sulla scheda Archivi.
1. Fai clic su Importa.
1. Fai clic su Sfoglia per individuare l’archivio da importare e quindi fai clic su Anteprima.
1. Rivedi l’elenco delle risorse e degli oggetti che verranno installati con l’archivio. Assicurati che non vi siano conflitti con le risorse, gli oggetti e le configurazioni di servizio esistenti, perché non è disponibile alcuna funzionalità di annullamento.

   Se scegli di importare le configurazioni del servizio, AEM Forms importa tutti i file di configurazione del processo (endpoint, profili di sicurezza e parametri di configurazione del servizio) utilizzati dai processi in LCA.

1. Fai clic su Importa.
1. Rivedi i risultati dell’importazione e fai clic su Ignora configurazione per completare il processo di importazione, oppure fai clic su Configura per configurare l’archivio.

   >[!NOTE]
   >
   >Se fai clic su Ignora configurazione, puoi configurare l’archivio in un secondo momento.

1. Se fai clic su Configura, viene visualizzata la pagina Configura endpoint, in cui è possibile apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fai clic su di esso.
   * Per aggiungere un endpoint di Gestione attività, fai clic su Aggiungi TaskManager. Per informazioni dettagliate sulle impostazioni di Gestione attività, consulta [Configurazione degli endpoint delle Gestione attività](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint di tipo Cartella controllata, fai clic su Aggiungi WatchedFolder. Per informazioni dettagliate sulle impostazioni della cartella controllata, consulta [Impostazioni dell’endpoint della cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fai clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni e-mail, consulta [Impostazioni dell’endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fai clic su Aggiungi EJB e specifica un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint SOAP, fai clic su Aggiungi SOAP e specifica un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint remoto, fai clic su Aggiungi remoto. Per informazioni dettagliate sulle impostazioni remote, consulta [Impostazioni dell’endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fai clic su Aggiungi REST e specifica un nome e una descrizione per l’endpoint. Osserva l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, seleziona la casella di controllo accanto a esso e fai clic su Rimuovi.

1. Fai clic su Avanti.
1. Se un processo o un servizio nella LCA dispone di parametri di configurazione, viene visualizzata la pagina Configura parametri, in cui è possibile configurare i parametri del servizio e fare clic su Avanti.
1. Nella pagina Configura profilo di sicurezza apporta le modifiche necessarie:

   * **Richiedi ai chiamanti di autenticarsi:** questa impostazione indica se il servizio può essere richiamato con o senza credenziali.

     Se viene visualizzato *Attualmente ai chiamanti è richiesto di autenticarsi*, il chiamante del servizio deve essere autenticato e l’entità principale dell’utente di tale chiamante deve essere autorizzata a richiamare il servizio; in caso contrario, il tentativo di chiamata verrà rifiutato. Per rimuovere la necessità di autenticazione, fai clic su Consenti chiamanti non autenticati.

     Se viene visualizzato *Ai chiamanti non è richiesto di autenticarsi*, non è necessario che il chiamante del servizio sia autenticato. La chiamata del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione. Per richiedere l’autenticazione, fai clic su Richiedi ai chiamanti di autenticarsi.

   * **Esegui come:** specifica l’identità di runtime utilizzata da un servizio dopo che è stato richiamato. Per modificare questa opzione, fai clic su Cambia. Scegli una delle seguenti opzioni:

     **Non specificato:** viene utilizzato il comportamento predefinito.

     **Chiamante:** utilizza la stessa identità dell’utente che ha richiamato il servizio.

     **Sistema:** esegue il servizio con privilegi completi. Questa è l’impostazione predefinita per i processi di lunga durata.

     **Utente con nome:** consente di eseguire il servizio come utente specifico. Questa è l’impostazione predefinita per i processi di breve durata. Quando selezioni questa opzione, fai clic su Seleziona utente per visualizzare la pagina Seleziona entità principale, in cui è possibile cercare e selezionare l’utente.

   * Per aggiungere un’entità principale al profilo di sicurezza, fai clic su Aggiungi entità principale e seleziona l’utente o il gruppo da aggiungere come entità principale. Fai clic su Avanti, quindi seleziona le autorizzazioni che desideri assegnare all’entità principale:

     **INVOKE_PERM:** per richiamare tutte le operazioni nel servizio

     **MODIFY_CONFIG_PERM:** per modificare la configurazione di un servizio

     **SUPERVISOR_PERM:** per visualizzare i dati dell’istanza di processo per un servizio creato da un processo

     **START_STOP_PERM:** per avviare e interrompere un servizio

     **ADD_REMOVE_ENDPOINTS_PERM:** per aggiungere, rimuovere e modificare endpoint per un servizio

     **CREATE_VERSION_PERM:** per creare una versione del servizio

     **DELETE_VERSION_PERM:** per eliminare una versione del servizio

     **MODIFY_VERSION_PERM:** per modificare una versione del servizio

     **READ_PERM:** per visualizzare il servizio

     Fai clic su Fine per aggiungere l’entità principale al profilo di sicurezza.

1. Fai clic su Fine per completare la configurazione.

## Configurare i moduli AEM che fanno parte di un file di archivio {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni, quindi fai clic sulla scheda Archivi.
1. Nella pagina Gestione archivio seleziona il file di archivio da configurare.
1. Nella pagina Visualizza archivio seleziona la risorsa di archivio evidenziata.
1. Configura il file di archivio dei processi importato.

## Utilizzare la procedura guidata di configurazione per configurare i moduli di AEM che fanno parte di un file di archivio {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni, quindi fai clic sulla scheda Archivi.
1. Fai clic su Configura accanto al file di archivio da configurare.
1. Viene visualizzata la pagina Configura endpoint, in cui è possibile apportare le modifiche necessarie:

   * Per rinominare un endpoint o modificarne la descrizione, fai clic su di esso.
   * Per aggiungere un endpoint di Gestione attività, fai clic su Aggiungi TaskManager. Per informazioni dettagliate sulle impostazioni di Gestione attività, consulta [Configurazione degli endpoint delle Gestione attività](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Per aggiungere un endpoint di tipo Cartella controllata, fai clic su Aggiungi WatchedFolder. Per informazioni dettagliate sulle impostazioni della cartella controllata, consulta [Impostazioni dell’endpoint della cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Per aggiungere un endpoint e-mail, fai clic su Aggiungi e-mail. Per informazioni dettagliate sulle impostazioni e-mail, consulta [Impostazioni dell’endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Per aggiungere un endpoint EJB, fai clic su Aggiungi EJB e specifica un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint SOAP, fai clic su Aggiungi SOAP e specifica un nome e una descrizione per l’endpoint.
   * Per aggiungere un endpoint remoto, fai clic su Aggiungi remoto. Per informazioni dettagliate sulle impostazioni remote, consulta [Impostazioni dell’endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Per aggiungere un endpoint REST, fai clic su Aggiungi REST e specifica un nome e una descrizione per l’endpoint. Osserva l’URL di chiamata REST visualizzato nella pagina Aggiungi endpoint REST.
   * Per rimuovere un endpoint, seleziona la casella di controllo accanto a esso e fai clic su Rimuovi.

1. Fai clic su Avanti.
1. Se un processo o un servizio nella LCA dispone di parametri di configurazione, viene visualizzata la pagina Configura parametri, in cui è possibile configurare i parametri del servizio e fare clic su Avanti.
1. Nella pagina Configura profilo di sicurezza è possibile apportare le modifiche necessarie:

   * **Richiedi ai chiamanti di autenticarsi:** questa impostazione indica se il servizio può essere richiamato con o senza credenziali.

     Se viene visualizzato *Attualmente ai chiamanti è richiesto di autenticarsi*, il chiamante del servizio deve essere autenticato e l’entità principale dell’utente di tale chiamante deve essere autorizzata a richiamare il servizio; in caso contrario, il tentativo di chiamata verrà rifiutato. Per rimuovere la necessità di autenticazione, fai clic su Consenti chiamanti non autenticati.

     Se viene visualizzato *Ai chiamanti non è richiesto di autenticarsi*, il chiamante del servizio potrebbe essere autenticato o meno. La chiamata del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione. Per richiedere l’autenticazione, fai clic su Richiedi ai chiamanti di autenticarsi.

   * **Esegui come:** specifica l’identità di runtime utilizzata da un servizio dopo che è stato richiamato. Per modificare questa opzione, fai clic su Cambia. Scegli una delle seguenti opzioni:

     **Non specificato:** viene utilizzato il comportamento predefinito.

     **Chiamante:** utilizza la stessa identità dell’utente che ha richiamato il servizio.

     **Sistema:** esegue il servizio con privilegi completi. Questa è l’impostazione predefinita per i processi di lunga durata.

     **Utente con nome:** consente di eseguire il servizio come utente specifico. Questa è l’impostazione predefinita per i processi di breve durata. Quando selezioni questa opzione, fai clic su Seleziona utente per visualizzare la pagina Seleziona entità principale, in cui è possibile cercare e selezionare l’utente.

   * Per aggiungere un’entità principale al profilo di sicurezza, fai clic su Aggiungi entità principale e seleziona l’utente o il gruppo da aggiungere come entità principale. Fai clic su Avanti, quindi seleziona le autorizzazioni che desideri assegnare all’entità principale:

     **INVOKE_PERM:** per richiamare tutte le operazioni nel servizio

     **MODIFY_CONFIG_PERM:** per modificare la configurazione di un servizio

     **SUPERVISOR_PERM:** per visualizzare i dati dell’istanza di processo per un servizio creato da un processo

     **START_STOP_PERM:** per avviare e interrompere un servizio

     **ADD_REMOVE_ENDPOINTS_PERM:** per aggiungere, rimuovere e modificare endpoint per un servizio

     **CREATE_VERSION_PERM:** per creare una versione del servizio

     **DELETE_VERSION_PERM:** per eliminare una versione del servizio

     **MODIFY_VERSION_PERM:** per modificare una versione del servizio

     **READ_PERM:** per visualizzare il servizio

     Fai clic su Fine per aggiungere l’entità principale al profilo di sicurezza.

## Rimuovere un oggetto {#remove-an-archive}

>[!NOTE]
>
>Per rimuovere un archivio contenente risorse memorizzate in un archivio di terze parti (server di gestione dei contenuti EMC Documentum, IBM FileNet Content Manager o IBM Content Manager), è necessario eliminare anche i file delle risorse dall’archivio mediante Workbench.

1. Nella console di amministrazione fai clic su Servizi > Applicazioni e servizi > Gestione archivio.
1. Nella pagina Gestione archivio seleziona la casella di controllo relativa all’archivio da rimuovere e fai clic su Rimuovi.
