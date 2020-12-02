---
title: Importazione ed esportazione di impostazioni globali
seo-title: Importazione ed esportazione di impostazioni globali
description: Puoi importare ed esportare le definizioni dei modelli di ricerca e le impostazioni globali per Workspace.
seo-description: Puoi importare ed esportare le definizioni dei modelli di ricerca e le impostazioni globali per Workspace.
uuid: 8f1f210d-e850-4b2c-bb5a-942fa8299791
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 72fe5749-2fa2-442f-b679-7889faeafcac
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---


# Importazione ed esportazione di impostazioni globali {#importing-and-exporting-global-settings}

Puoi importare ed esportare le definizioni dei modelli di ricerca e le impostazioni globali per Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM rilascio di moduli.

Ad esempio, potete passare da un ambiente di sviluppo a un ambiente di produzione esportando le definizioni dei modelli di ricerca e le impostazioni globali da un ambiente e importandole nell&#39;altro.

Dopo aver esportato il file delle impostazioni globali, potete modificare le impostazioni in un editor XML o di testo. Tuttavia, le uniche impostazioni che è possibile modificare sono le impostazioni JChannelConnectionProperties, formViewOnly e specialRoutes. Per ulteriori informazioni, vedere [Impostazioni globali dell&#39;area di lavoro](importing-exporting-global-settings.md#workspace-global-settings).


>[!NOTE]
>
>Se modificate le proprietà dell&#39;evento nel file delle impostazioni globali, è necessario riavviare il server.

## Importare una definizione di modello di ricerca {#import-a-search-template-definition}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Amministrazione globale.
1. Nella casella Importa definizione modello di ricerca fare clic su Scegli file e selezionare il modello di ricerca. Potete importare solo le definizioni dei modelli di ricerca originariamente esportate da un’istanza di Workspace.
1. Fai clic su Importa.

## Esportare la definizione di modello di ricerca {#export-a-search-template-definition}

1. Nella pagina Amministrazione globale, in Definizione modello di ricerca Esporta, fate clic su Elenca tutto.
1. Nell’elenco dei modelli di ricerca, selezionate il modello da esportare.

   >[!NOTE]
   >
   >Potete selezionare più modelli, ma viene esportato solo l’ultimo modello selezionato.

1. Fate clic su Esporta e salvate il file sul computer.

## Importa impostazioni globali {#import-global-settings}

1. Nella pagina Amministrazione globale, in Importa impostazioni globali, fate clic su Scegli file e selezionate il file delle impostazioni globali. Il file di impostazioni globali deve essere in formato XML.
1. Fai clic su Importa.

## Esporta impostazioni globali {#export-global-settings}

1. Nella pagina Amministrazione globale, in Esporta impostazioni globali, fate clic su Esporta.
1. Salvare il file sul computer.

## Impostazioni globali dell&#39;area di lavoro {#workspace-global-settings}

È possibile modificare il file di impostazioni globali; tuttavia, è possibile modificare solo le impostazioni JChannelConnectionProperties, formViewOnly e specialRoutes.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM rilascio di moduli.

Il file delle impostazioni globali di Workspace include le seguenti impostazioni:

### impostazioni dei cicli speciali {#specialroutes-settings}

Le impostazioni *specialRoutes* specificano le proprietà delle route speciali, approvate e rifiutate, in Workspace. In alcune situazioni, i pulsanti per queste route vengono visualizzati sulle schede attività in Workspace e l&#39;utente può selezionarli senza aprire il modulo. È possibile modificare le impostazioni specialRoutes nel file delle impostazioni globali per aggiungere nomi personalizzati da approvare e negare o per creare percorsi aggiuntivi.

**client_specialRoutes_route_authorized_style:** Il nome dello stile che si trova nel tema Workspace, che identifica le icone dei pulsanti di approvazione. Lo stile deve includere valori per un&#39;icona abilitata e un&#39;icona disattivata. Per definire uno stile per un pulsante personalizzato, è necessario utilizzare il modello seguente:
` .buttonApprove {  icon: Embed('images/LC_DirectApprove_Sm_N.png');  disabledIcon: Embed('images/LC_DirectApprove_Sm_D.png');  paddingLeft: 5;  }` Il file CSS di Workspace è incorporato nel file workspace-tema.swf, che si trova nel file adobe-workspace-client.ear > adobe-workspace-client.war. Per modificare l’aspetto di Workspace, è necessario ricompilare il file workspace-tema.swf.

**client_specialRoutes_route_Negative_names:** La varietà di stringhe che un utente di Workbench può utilizzare per essere interpretato come &quot;negazione&quot;. Le stringhe seguono la distinzione tra maiuscole e minuscole. Ad esempio, il valore predefinito è Rifiuta. Se l&#39;utente di Workbench utilizza la parola Rifiuta in un processo, la parola non verrà riconosciuta. Per personalizzare il pulsante di route, è necessario aggiungere la parola Rifiuta e applicare lo stile al pulsante.

**client_specialRoutes_route_negare_stile:** il nome dello stile che si trova nel file del tema Workspace, che identifica le icone del pulsante di rifiuto. Lo stile deve includere valori per un&#39;icona abilitata e un&#39;icona disattivata. Per definire uno stile per un pulsante personalizzato, è necessario utilizzare il modello seguente:
`  .buttonDeny {   icon: Embed('images/LC_DirectDeny_Sm_N.png');   disabledIcon: Embed('images/LC_DirectDeny_Sm_D.png');   paddingLeft: 0;   }` **client_specialRoutes_route_authorized_names:** La varietà di stringhe che un utente di Workbench può utilizzare per essere interpretato come &quot;approvato&quot;. Le stringhe seguono la distinzione tra maiuscole e minuscole. Ad esempio, il valore predefinito è approva. Se l&#39;utente di Workbench utilizza la parola Approva in un processo, la parola non verrà riconosciuta. Per personalizzare il pulsante di route, è necessario aggiungere la parola Approva a questa impostazione e applicare lo stile al pulsante.

**client_specialRoutes_names:** chiavi utilizzate per individuare il valore stringa personalizzato dai file delle risorse. Ogni voce in questa impostazione deve includere i valori per i nomi e lo stile.

### Impostazioni JGroup {#jgroup-settings}

Queste impostazioni vengono visualizzate solo se sono stati aggiornati dall&#39;LiveCycle  Adobe ES 2.5 o versioni precedenti.

**server_remoteevents_ClientTimeoutMilliseconds:** Tempo massimo di attesa dei messaggi dell&#39;evento da parte del gruppo JGroup. Questa impostazione non deve essere modificata.

**server_remoteevents_ServerTimeoutMilliseconds:** timeout per la ricezione dei messaggi JGroup sul server. Questa opzione imposta il ritardo per l&#39;invio di messaggi dal server al client.

**server_remoteevents_JChannelConnectionProperties:** Le proprietà di connessione del gruppo JGroup utilizzate per comunicare tra il server (in cui un evento di servizio viene elaborato dal servizio RemoteEvent) e tutte le istanze di Workspace.

Potrebbe essere necessario modificare i valori UDP per l&#39;indirizzo IP multicast (mcast_addr), la porta IP multicast (mcast_port) e il TTL per i pacchetti multicast (ip_ttl). Per impostazione predefinita, l&#39;indirizzo IP multicast e i valori delle porte vengono generati in modo casuale e, in genere, non è necessario modificare i valori. Tuttavia, se la società dispone di criteri di rete relativi a intervalli multicast specifici per gli indirizzi IP multicast, potrebbe essere necessario modificare i valori.

>[!NOTE]
>
>Il TTL deve essere maggiore del numero di switch di rete tra i server del cluster; tuttavia, se il valore è impostato su un valore troppo elevato, i pacchetti multicast potrebbero essere inseriti nelle subnet, dove verranno scartati.

Le proprietà rimanenti in questa impostazione non devono essere modificate.

**server_remoteevents_JGroupName:** il nome del gruppo JG utilizzato per la comunicazione degli eventi remoti. Questo valore viene generato in modo casuale per evitare conflitti nei cluster. Questo valore non deve essere modificato.

Per ulteriori informazioni su gruppi JG e Workspace, vedere [Gruppi di lavoro e moduli AEM Area di lavoro - Spiegato](https://blogs.adobe.com/livecycle/2011/03/jgroups-and-livecycle-workspace-explained.html).

### impostazioni di formView {#formview-settings}

**client_formView_openFormInFullScreen:** per visualizzare tutti i moduli in Workspace in modalità a schermo intero, impostare questa opzione su true. Per impostazione predefinita, questa opzione è impostata su false e i moduli non vengono visualizzati in modalità a schermo intero. Il servizio Utente contiene un&#39;opzione per aprire il documento associato a un&#39;attività in modalità a schermo intero. Questo consente di controllare la visualizzazione in base al processo.

**client_route_formViewOnly:** se è impostata su True, le route non vengono visualizzate nella vista a schede o elenco di Workspace. Il valore predefinito è False, ovvero le route vengono visualizzate nelle viste a schede e a elenco.

### Altre impostazioni {#other-settings}

**client_mimeTypes_openOutsideBrowser:** Il tipo MIME di documenti che si aprirà all’esterno dell’istanza del browser Workspace. Se i processi aziendali richiedono un tipo MIME aggiuntivo, specificatelo qui. I valori predefiniti sono:

* `application/msword`
* `application/msexcel`
* `application/ms-powerpoint`

**client_customUI_caching:** esegue la cache di un&#39;interfaccia utente dell&#39;attività personalizzata.

**server_debugLevel:** Non modificare questa impostazione.

**client_pollingInterval:** imposta l&#39;intervallo di polling (in secondi) utilizzato in Flex Workspace (obsoleto per AEM moduli su JEE) per rilevare attività nuove e modificate. Il valore predefinito è 3 secondi. Questo non funziona per  AEM Forms Workspace.

**client_systemContext_name:** specifica un nome personalizzato (ad es. Cittadino) da visualizzare nel campo Aggiunto da (nella scheda Allegati) per gli allegati di un’attività in  AEM Forms Workspace.

Per definire il nome personalizzato:

`<client_systemContext_name>[custom name to display]</client_systemContext_name>`

>[!NOTE]
>
>Per l&#39;applicazione Demo, il nome visualizzato predefinito è **Citizen**. Per un&#39;applicazione personalizzata creata, il nome visualizzato predefinito è **Account contesto di sistema**.
>
>**client_idleTimeout:** quando un utente rimane inattivo per un periodo di tempo specifico,  scadenza della sessione di AEM Forms Workspace. Per abilitare la funzione, aggiungete una voce alle impostazioni globali &lt;client_idleTimeout>*IDLE_TIMEOUT_IN_SECONDS*&lt;/client_idleTimeout>. Potete specificare il valore 0 per disattivare il timeout di inattività. Il tempo viene specificato in secondi.
