---
title: Importazione ed esportazione delle impostazioni globali
description: Puoi importare ed esportare le definizioni dei modelli di ricerca e le impostazioni globali per l’area di lavoro.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1208'
ht-degree: 100%

---

# Importazione ed esportazione delle impostazioni globali {#importing-and-exporting-global-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi importare ed esportare le definizioni dei modelli di ricerca e le impostazioni globali per l’area di lavoro.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.

Ad esempio, puoi spostarti da un ambiente di sviluppo a un ambiente di produzione esportando le definizioni dei modelli di ricerca e le impostazioni globali da un ambiente e importandole nell’altro.

Dopo aver esportato il file delle impostazioni globali, puoi modificare le impostazioni in un editor XML o di testo. Tuttavia, le uniche impostazioni che è possibile modificare sono le impostazioni JChannelConnectionProperties, formViewOnly e specialRoutes. Per ulteriori informazioni, consulta [Impostazioni globali dell’area di lavoro](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Se modifichi le proprietà dell’evento nel file delle impostazioni globali, è necessario riavviare il server.

## Importare una definizione del modello di ricerca {#import-a-search-template-definition}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Amministrazione globale.
1. Nella casella Importa definizione del modello di ricerca, fai clic su Scegli file e seleziona il modello di ricerca. Puoi importare solo le definizioni dei modelli di ricerca esportate originariamente da un&#39;istanza di Workspace.
1. Fai clic su Importa.

## Esportare una definizione del modello di ricerca {#export-a-search-template-definition}

1. Nella pagina Amministrazione globale, in Esporta definizione del modello di ricerca, fai clic su Elenca tutti.
1. Nell’elenco dei modelli di ricerca, seleziona il modello da esportare.

   >[!NOTE]
   >
   >È possibile selezionare più modelli, ma viene esportato solo l’ultimo modello selezionato.

1. Fai clic su Esporta e quindi salva il file sul computer.

## Importare le impostazioni globali {#import-global-settings}

1. Nella pagina Amministrazione globale, in Importa impostazioni globali, fai clic su Scegli file e seleziona il file delle impostazioni globali. Il file delle impostazioni globali deve essere in formato XML.
1. Fai clic su Importa.

## Esportare le impostazioni globali. {#export-global-settings}

1. Nella pagina Amministrazione globale, in Esporta impostazioni globali, fai clic su Esporta.
1. Salva il file sul computer.

## Impostazioni globali dell’area di lavoro {#workspace-global-settings}

Puoi modificare il file delle impostazioni globali. Tuttavia, le uniche impostazioni che è possibile modificare sono JChannelConnectionProperties, formViewOnly e specialRoutes.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.

Il file delle impostazioni globali dell’area di lavoro include le impostazioni seguenti:

### impostazioni specialRoutes {#specialroutes-settings}

Le impostazioni *specialRoutes* specificano le proprietà dei percorso speciali approvate e negate, in Workspace. In alcune situazioni, i pulsanti per questi percorsi vengono visualizzati sulle schede attività in Workspace e l’utente può selezionarli senza aprire il modulo. È possibile modificare le impostazioni specialRoutes nel file delle impostazioni globali per aggiungere nomi personalizzati per l’approvazione e la negazione o per creare percorsi aggiuntivi.

**client_specialRoutes_route_approve_style:** nome dello stile presente nel tema dell’area di lavoro che identifica le icone del pulsante di approvazione. Lo stile deve includere valori per un’icona attivata e disattivata. Per definire uno stile per un pulsante personalizzato, è necessario utilizzare il modello seguente:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Il file CSS Workspace è incorporato nel file workspace-theme.swf, che si trova nel file adobe-workspace-client.ear > adobe-workspace-client.war. Per modificare l’aspetto dell’area di lavoro, è necessario ricompilare il file workspace-theme.swf.

**client_specialRoutes_route_deny_names:** la varietà di stringhe che un utente di Workbench può utilizzare per essere interpretata come “rifiuta”. Le stringhe fanno distinzione tra maiuscole e minuscole. Ad esempio, il valore predefinito è “rifiuta”. Se l’utente di Workbench utilizza la parola Rifiuta in un processo, la parola non viene riconosciuta. Affinché il pulsante del percorso sia personalizzato e sia applicato lo stile, è necessario aggiungere la parola Rifiuta a questa impostazione.

**client_specialRoutes_route_deny_style:** nome dello stile presente nel file del tema dell’area di lavoro che identifica le icone del pulsante di rifiuto. Lo stile deve includere valori per un’icona attivata e disattivata. Per definire uno stile per un pulsante personalizzato, è necessario utilizzare il modello seguente:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_route_approve_names:** la varietà di stringhe che un utente di Workbench può utilizzare per essere interpretata come “approva”. Le stringhe fanno distinzione tra maiuscole e minuscole. Ad esempio, il valore predefinito è “approva”. Se l’utente di Workbench utilizza la parola Approva in un processo, la parola non viene riconosciuta. La parola Approva deve essere aggiunta a questa impostazione affinché il pulsante per il percorso sia personalizzato e ad esso sia applicato lo stile.

**client_specialRoutes_names:** le chiavi utilizzate per individuare il valore della stringa personalizzato dai file di risorse. Ogni voce di questa impostazione deve includere i valori per i nomi e lo stile.

### Impostazioni Gruppo J {#jgroup-settings}

Queste impostazioni vengono visualizzate solo se è stato eseguito l’aggiornamento da Adobe LiveCycle ES 2.5 o versioni precedenti.

**server_remoteevents_ClientTimeoutMilliseconds:** tempo massimo di attesa dei messaggi dell’evento da parte del Gruppo J. Questa impostazione non deve essere modificata.

**server_remoteevents_ServerTimeoutMilliseconds:** timeout per la ricezione di messaggi del Gruppo J sul server. Questa opzione imposta il ritardo per l’invio dei messaggi dal server al client.

**server_remoteevents_JChannelConnectionProperties:** proprietà di connessione per il gruppo Gruppo J utilizzate per comunicare tra il server (sul quale il servizio RemoteEvent elabora un evento di servizio) e tutte le istanze di Workspace.

Potrebbe essere necessario modificare i valori UDP per l’indirizzo IP multicast (mcast_addr), la porta IP multicast (mcast_port) e il TTL per i pacchetti multicast (ip_ttl). Per impostazione predefinita, i valori dell’indirizzo IP multicast e della porta vengono generati in modo casuale e, in genere, non è necessario modificare i valori. Tuttavia, se la società dispone di criteri di rete relativi a intervalli multicast specifici per indirizzi IP multicast, potrebbe essere necessario modificare i valori.

>[!NOTE]
>
>Il TTL deve essere maggiore del numero di commutatori di rete tra i server del cluster. Tuttavia, se il valore è impostato su un valore troppo alto, i pacchetti multicast potrebbero spostarsi nelle subnet, dove verranno eliminati.

Le proprietà rimanenti in questa impostazione non devono essere modificate.

**server_remoteevents_JGroupName:** nome del Gruppo J utilizzato per la comunicazione remota degli eventi. Questo valore viene generato in modo casuale per evitare conflitti nei cluster. Questo valore non deve essere modificato.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### Impostazioni formView {#formview-settings}

**client_formView_openFormInFullScreen:** per visualizzare tutti i moduli in Workspace in modalità a schermo intero, imposta questa opzione su vero. Per impostazione predefinita, questa opzione è impostata su falso e i moduli non vengono visualizzati in modalità a schermo intero. Il servizio Utente contiene un’opzione per aprire il documento associato a un’attività in modalità a schermo intero. Questo consente di controllare la visualizzazione in base al singolo processo.

**client_route_formViewOnly:** se è impostato su vero, i percorsi non vengono visualizzati nella vista a schede o nella vista a elenco in Workspace. Il valore predefinito è falso, il che significa che i percorsi vengono visualizzati nella vista a schede e nella vista a elenco.

### Altre impostazioni {#other-settings}

**client_mimeTypes_openOutsideBrowser:** il tipo di documenti MIME che viene aperto al di fuori dell’istanza del browser Workspace. Se i processi dell’organizzazione richiedono un tipo MIME aggiuntivo, specificalo qui. I valori predefiniti sono:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** memorizza nella cache un’interfaccia utente dell’attività personalizzata.

**server_debugLevel:** non modificare questa impostazione.

**client_pollingInterval:** imposta l’intervallo di polling (in secondi) utilizzato in (obsoleto per AEM Forms su JEE) Flex Workspace per rilevare le attività nuove e modificate. Il valore predefinito è 3 secondi. Questa operazione non funziona per l’area di lavoro di AEM Forms.

**client_systemContext_name:** specifica un nome personalizzato, ad esempio Cittadino, da visualizzare nel campo Aggiunto da (nella scheda Allegati) per gli allegati di un’attività nell’area di lavoro di AEM Forms.

Per definire il nome personalizzato:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Per l’applicazione Demo, il nome visualizzato predefinito è **Cittadino**. Per un’applicazione personalizzata creata, il nome visualizzato predefinito è **Account contesto di sistema**.
>
>**client_idleTimeout:** quando un utente rimane inattivo per un periodo di tempo specifico, la sessione dell’area di lavoro di AEM Forms scade. Per abilitare la funzione, aggiungi una voce alle Impostazioni globali &lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>. Puoi specificare il valore 0 per disattivare il timeout di inattività. La quantità di tempo è specificata in secondi.
