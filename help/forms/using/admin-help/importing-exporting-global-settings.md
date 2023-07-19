---
title: Importazione ed esportazione di impostazioni globali
seo-title: Importing and exporting global settings
description: Puoi importare ed esportare le definizioni dei modelli di ricerca e le impostazioni globali per Workspace.
seo-description: You can import and export search template definitions and global settings for Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
exl-id: cdb7ff54-7891-45b1-a921-10b01ef5188d
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# Importazione ed esportazione di impostazioni globali {#importing-and-exporting-global-settings}

Puoi importare ed esportare le definizioni dei modelli di ricerca e le impostazioni globali per Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per il rilascio di moduli AEM.

Ad esempio, puoi passare da un ambiente di sviluppo a un ambiente di produzione esportando le definizioni dei modelli di ricerca e le impostazioni globali da un ambiente e importandole nell’altro.

Dopo aver esportato il file delle impostazioni globali, è possibile modificare le impostazioni in un editor XML o di testo. Le uniche impostazioni che è possibile modificare sono le impostazioni JChannelConnectionProperties, formViewOnly e specialRoutes. Per ulteriori informazioni, consulta [Impostazioni globali di Workspace](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Se si modificano le proprietà dell&#39;evento nel file delle impostazioni globali, è necessario riavviare il server.

## Importare una definizione di modello di ricerca {#import-a-search-template-definition}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Amministrazione globale.
1. Nella casella Importa definizione modello di ricerca fare clic su Scegli file e selezionare il modello di ricerca. Puoi importare solo le definizioni dei modelli di ricerca esportate originariamente da un’istanza di Workspace.
1. Fai clic su Importa.

## Esportare una definizione di modello di ricerca {#export-a-search-template-definition}

1. Nella pagina Amministrazione globale, in Esporta definizione modello di ricerca fare clic su Elenca tutto.
1. Nell’elenco dei modelli di ricerca, seleziona il modello da esportare.

   >[!NOTE]
   >
   >È possibile selezionare più modelli, ma viene esportato solo l&#39;ultimo modello selezionato.

1. Fare clic su Esporta e quindi salvare il file nel computer.

## Importa impostazioni globali {#import-global-settings}

1. Nella pagina Amministrazione globale, in Importa impostazioni globali, fare clic su Scegli file e selezionare il file delle impostazioni globali. Il file delle impostazioni globali deve essere in formato XML.
1. Fai clic su Importa.

## Esporta impostazioni globali {#export-global-settings}

1. Nella pagina Amministrazione globale, in Esporta impostazioni globali, fare clic su Esporta.
1. Salva il file sul computer.

## Impostazioni globali di Workspace {#workspace-global-settings}

È possibile modificare il file delle impostazioni globali. Tuttavia, le uniche impostazioni che è possibile modificare sono JChannelConnectionProperties, formViewOnly e specialRoutes.

>[!NOTE]
>
>Flex Workspace è obsoleto per il rilascio di moduli AEM.

Il file delle impostazioni globali di Workspace include le impostazioni seguenti:

### impostazioni specialRoutes {#specialroutes-settings}

Il *specialRoutes* Le impostazioni specificano le proprietà dei percorsi speciali, approva e Nega, in Workspace. In determinate situazioni, i pulsanti per questi percorsi vengono visualizzati nelle schede delle attività in Workspace e l’utente può selezionarli senza aprire il modulo. È possibile modificare le impostazioni specialRoutes nel file delle impostazioni globali per aggiungere nomi personalizzati per l&#39;approvazione e la negazione o per creare percorsi aggiuntivi.

**client_specialRoutes_route_approve_style:** Il nome dello stile che si trova nel tema dell’area di lavoro, che identifica le icone dei pulsanti di approvazione. Lo stile deve includere valori per un&#39;icona attivata e un&#39;icona disattivata. Per definire uno stile per un pulsante personalizzato, è necessario utilizzare il modello seguente:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Il file CSS Workspace è incorporato nel file workspace-theme.swf, che si trova nel file adobe-workspace-client.ear > adobe-workspace-client.war. Per modificare l&#39;aspetto di Workspace, è necessario ricompilare il file workspace-theme.swf.

**client_specialRoutes_route_deny_names:** La varietà di stringhe che un utente di Workbench può utilizzare per essere interpretata come &quot;nega&quot;. Le stringhe fanno distinzione tra maiuscole e minuscole. Ad esempio, il valore predefinito è nega. Se l’utente di Workbench utilizza la parola Rifiuta in un processo, la parola non viene riconosciuta. Affinché il pulsante di instradamento sia personalizzato e sia applicato lo stile, è necessario aggiungere la parola Nega a questa impostazione.

**client_specialRoutes_route_deny_style:** Il nome dello stile che si trova nel file del tema Workspace, che identifica le icone del pulsante Nega. Lo stile deve includere valori per un&#39;icona attivata e un&#39;icona disattivata. Per definire uno stile per un pulsante personalizzato, è necessario utilizzare il modello seguente:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_route_approve_names:** La varietà di stringhe che un utente di Workbench può utilizzare per essere interpretato come &quot;approva&quot;. Le stringhe fanno distinzione tra maiuscole e minuscole. Ad esempio, il valore predefinito è approva. Se l’utente di Workbench utilizza la parola Approve (Approva) in un processo, la parola non viene riconosciuta. Affinché il pulsante di instradamento sia personalizzato e sia applicato lo stile, è necessario aggiungere la parola Approve a questa impostazione.

**client_specialRoutes_names:** Chiavi utilizzate per individuare il valore della stringa personalizzata dai file di risorse. Ogni voce di questa impostazione deve includere i valori per i nomi e lo stile.

### Impostazioni gruppo {#jgroup-settings}

Queste impostazioni vengono visualizzate solo se è stato eseguito l&#39;aggiornamento da Adobe LiveCycle ES 2.5 o versioni precedenti.

**server_remoteevents_ClientTimeoutMilliseconds:** Tempo massimo di attesa dei messaggi dell&#39;evento da parte del gruppo di lavoro. Questa impostazione non deve essere modificata.

**server_remoteevents_ServerTimeoutMilliseconds:** Timeout per la ricezione di messaggi del gruppo di lavoro sul server. Questa opzione imposta il ritardo per l&#39;invio dei messaggi dal server al client.

**server_remoteevents_JChannelConnectionProperties:** Le proprietà di connessione del gruppo JG utilizzate per comunicare tra il server (sul quale il servizio RemoteEvent elabora un evento del servizio) e tutte le istanze di Workspace.

Potrebbe essere necessario modificare i valori UDP per l&#39;indirizzo IP multicast (mcast_addr), la porta IP multicast (mcast_port) e il TTL per i pacchetti multicast (ip_ttl). Per impostazione predefinita, i valori dell&#39;indirizzo IP multicast e della porta vengono generati in modo casuale e, in genere, non è necessario modificare i valori. Tuttavia, se la società dispone di criteri di rete relativi a intervalli multicast specifici per indirizzi IP multicast, potrebbe essere necessario modificare i valori.

>[!NOTE]
>
>Il valore TTL deve essere maggiore del numero di switch di rete tra i server del cluster. Tuttavia, se il valore è impostato su un valore troppo alto, i pacchetti multicast potrebbero spostarsi nelle subnet, dove verranno eliminati.

Le proprietà rimanenti in questa impostazione non devono essere modificate.

**server_remoteevents_JGroupName:** Nome del gruppo JG utilizzato per la comunicazione remota degli eventi. Questo valore viene generato in modo casuale per evitare conflitti nei cluster. Questo valore non deve essere modificato.

<!--

For additional information on JGroups and Workspace, see [JGroups and AEM forms Workspace - Explained](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

-->

### impostazioni formView {#formview-settings}

**client_formView_openFormInFullScreen:** Per visualizzare tutti i moduli in Workspace in modalità a schermo intero, imposta questa opzione su true. Per impostazione predefinita, questa opzione è impostata su false e i moduli non vengono visualizzati in modalità a schermo intero. Si noti che il servizio User contiene un&#39;opzione per aprire il documento associato a un&#39;attività in modalità a schermo intero. Questo consente di controllare la visualizzazione in base al singolo processo.

**client_route_formViewOnly:** Se è impostato su True, le route non vengono visualizzate nella vista a schede o nella vista a elenco in Workspace. Il valore predefinito è False, il che significa che le route vengono visualizzate nella vista a schede e nella vista a elenco.

### Altre impostazioni {#other-settings}

**client_mimeTypes_openOutsideBrowser:** Tipo MIME di documenti che verranno aperti al di fuori dell’istanza del browser Workspace. Se i processi dell’organizzazione richiedono un tipo MIME aggiuntivo, specificalo qui. I valori predefiniti sono:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** Memorizza nella cache un&#39;interfaccia utente per attività personalizzata.

**server_debugLevel:** Non modificare questa impostazione.

**client_pollingInterval:** Imposta l’intervallo di polling (in secondi) utilizzato nell’area di lavoro Flex (obsoleto per i moduli AEM su JEE) per rilevare le attività nuove o modificate. Il valore predefinito è 3 secondi. Questa operazione non funziona per AEM Forms Workspace.

**client_systemContext_name:** Specifica un nome personalizzato (ad esempio Cittadino) da visualizzare nel campo Aggiunto da (nella scheda Allegati) per gli allegati di un’attività in AEM Forms Workspace.

Per definire il nome personalizzato:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Per l’applicazione Demo, il nome visualizzato predefinito è **Cittadino**. Per un&#39;applicazione personalizzata creata, il nome visualizzato predefinito è **Account contesto di sistema**.
>
>**client_idleTimeout:** Quando un utente rimane inattivo per un periodo di tempo specifico, la sessione di AEM Forms Workspace scade. Per abilitare questa funzione, aggiungi una voce alle Impostazioni globali &lt;client_idletimeout>*IDLE_TIMEOUT_IN_SECONDI*&lt;/client_idletimeout>. È possibile specificare il valore 0 per disattivare il timeout di inattività. La quantità di tempo è specificata in secondi.
