---
title: Replica
seo-title: Replication
description: Scopri come configurare e monitorare gli agenti di replica nell’AEM.
seo-description: Learn how to configure and monitor replication agents in AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '3425'
ht-degree: 4%

---

# Replica{#replication}

Gli agenti di replica sono centrali per Adobe Experience Manager (AEM) in quanto il meccanismo utilizzato per:

* [Pubblica (attiva)](/help/sites-authoring/publishing-pages.md#activatingcontent) contenuti da un ambiente di authoring a uno di pubblicazione.
* Svuota esplicitamente il contenuto dalla cache di Dispatcher.
* Restituisce l’input dell’utente (ad esempio, l’input del modulo) dall’ambiente di pubblicazione all’ambiente di authoring (sotto il controllo dell’ambiente di authoring).

Le richieste sono [in coda](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) all’agente incaricato dell’elaborazione.

>[!NOTE]
>
>I dati utente (utenti, gruppi di utenti e profili utente) non vengono replicati tra le istanze di authoring e pubblicazione.
>
>Per più istanze di pubblicazione, i dati utente sono distribuiti tramite Sling quando [Sincronizzazione utente](/help/sites-administering/sync.md) è abilitato.

## Replica da authoring a pubblicazione {#replicating-from-author-to-publish}

La replica in un’istanza di pubblicazione o in un dispatcher si svolge in diversi passaggi:

* l’autore richiede la pubblicazione (attivazione) di determinati contenuti; questa operazione può essere avviata tramite una richiesta manuale o tramite attivatori automatici preconfigurati.
* la richiesta viene passata all’agente di replica predefinito appropriato; un ambiente può avere diversi agenti predefiniti che verranno sempre selezionati per tali azioni.
* l’agente di replica &quot;crea pacchetti&quot; del contenuto e lo inserisce nella coda di replica.
* nella scheda Siti Web [indicatore di stato colorato](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) è impostato per le singole pagine.
* il contenuto viene rimosso dalla coda e trasportato nell’ambiente di pubblicazione utilizzando il protocollo configurato; in genere si tratta di HTTP.
* un servlet nell’ambiente di pubblicazione riceve la richiesta e pubblica il contenuto ricevuto; il servlet predefinito è `https://localhost:4503/bin/receive`.

* è possibile configurare più ambienti di authoring e pubblicazione.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replica dalla pubblicazione all’authoring {#replicating-from-publish-to-author}

Alcune funzioni consentono agli utenti di immettere dati in un’istanza Publish.

In alcuni casi, è necessario un tipo di replica noto come replica inversa per restituire i dati all’ambiente di authoring da dove vengono ridistribuiti ad altri ambienti di pubblicazione. Per motivi di sicurezza, qualsiasi traffico dall’ambiente di pubblicazione a quello di authoring deve essere controllato rigorosamente.

La replica inversa utilizza un agente nell’ambiente di pubblicazione che fa riferimento all’ambiente di authoring. Questo agente inserisce i dati in una casella in uscita. Questa casella in uscita corrisponde ai listener di replica nell’ambiente di authoring. I listener eseguono il polling delle caselle in uscita per raccogliere i dati immessi e quindi distribuirli in base alle esigenze. In questo modo l’ambiente di authoring controlla tutto il traffico.

In altri casi, come per le funzioni di Communities (ad esempio forum, blog, commenti e recensioni), è difficile sincronizzare in modo efficiente la quantità di contenuti generati dagli utenti (UGC, User Generated Content) immessi nell’ambiente di pubblicazione tra le istanze AEM utilizzando la replica.

AEM [Community](/help/communities/overview.md) non utilizza mai la replica per UGC. Al contrario, la distribuzione per Communities richiede un archivio comune per UGC (vedi [Archiviazione contenuti community](/help/communities/working-with-srp.md)).

### Replica: funzioni pronte all’uso {#replication-out-of-the-box}

Il sito web we-retail incluso in un&#39;installazione standard di AEM può essere utilizzato per illustrare la replica.

Per seguire questo esempio e utilizzare gli agenti di replica predefiniti è necessario [Installare AEM](/help/sites-deploying/deploy.md) con:

* ambiente di authoring sulla porta `4502`
* ambiente di pubblicazione sulla porta `4503`

>[!NOTE]
>
>Opzione attivata per impostazione predefinita :
>
>* Agenti sull&#39;autore : agente predefinito (pubblicazione)
>
>Effettivamente disabilitati per impostazione predefinita (a partire da AEM 6.1) :
>
>* Agenti sull&#39;autore : agente di replica inversa (publish_reverse)
>* Agenti in pubblicazione : Replica inversa (casella in uscita)
>
>Per verificare lo stato dell&#39;agente o della coda, utilizzare **Strumenti** console.
>Consulta [Monitoraggio degli agenti di replica](#monitoring-your-replication-agents).

#### Replica (da autore a pubblicazione) {#replication-author-to-publish}

1. Passa alla pagina di supporto nell’ambiente di authoring.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Modifica la pagina per aggiungere del nuovo testo.
1. **Attiva pagina** per pubblicare le modifiche.
1. Apri la pagina di supporto nell’ambiente di pubblicazione:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Ora puoi visualizzare le modifiche inserite durante l’authoring.

Questa replica viene eseguita dall’ambiente di authoring da:

* **Agente predefinito (pubblicazione)**
Questo agente replica il contenuto nell’istanza di pubblicazione predefinita.
I dettagli di questo (configurazione e registri) sono accessibili dalla console Strumenti dell’ambiente di authoring; oppure:
  `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agenti di replica - Pronti all’uso {#replication-agents-out-of-the-box}

I seguenti agenti sono disponibili in un&#39;installazione standard per AEM:

* [Agente predefinito](#replication-author-to-publish)
Utilizzato per replicare da authoring a pubblicazione.

* Svuotamento del Dispatcher Viene utilizzato per gestire la cache di Dispatcher. Consulta [Invalidazione della cache di Dispatcher dall’ambiente di authoring](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) e [Annullamento della validità della cache di Dispatcher da un’istanza Publish](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) per ulteriori informazioni.

* [Replica inversa](#reverse-replication-publish-to-author)
Utilizzato per replicare da pubblicazione a authoring. La replica inversa non viene utilizzata per le funzioni di Communities, ad esempio forum, blog e commenti. Viene effettivamente disattivata in quanto la casella in uscita non è abilitata. L’utilizzo della replica inversa richiederebbe una configurazione personalizzata.

* Agente statico &quot;Agente che memorizza una rappresentazione statica di un nodo nel file system&quot;.
Ad esempio, con le impostazioni predefinite, le pagine di contenuto e le risorse DAM vengono memorizzate in `/tmp`, come HTML o nel formato risorsa appropriato. Consulta la `Settings` e `Rules` schede per la configurazione.
Questa richiesta consentiva di visualizzare il contenuto quando la pagina veniva richiesta direttamente dal server dell’applicazione. Si tratta di un agente specializzato e (probabilmente) non sarà necessario per la maggior parte delle istanze.

## Agenti di replica - Parametri di configurazione {#replication-agents-configuration-parameters}

Durante la configurazione di un agente di replica dalla console Strumenti, nella finestra di dialogo sono disponibili quattro schede:

### Impostazioni {#settings}

* **Nome**

  Nome univoco dell’agente di replica.

* **Descrizione**

  Descrizione dello scopo che verrà fornito da questo agente di replica.

* **abilitato**

  Indica se l’agente di replica è attualmente abilitato.

  Quando l&#39;agente è **abilitato** la coda verrà visualizzata come:

   * **Attivo** quando gli elementi vengono elaborati.
   * **Inattivo** quando la coda è vuota.
   * **Bloccato** quando gli elementi sono in coda ma non possono essere elaborati, ad esempio quando la coda di ricezione è disabilitata.

* **Tipo di serializzazione**

  Tipo di serializzazione:

   * **Predefinito**: imposta se l’agente deve essere selezionato automaticamente.
   * **Scaricamento del Dispatcher**: selezionalo se l’agente deve essere utilizzato per scaricare la cache del dispatcher.

* **Ritardo per riprovare**

  Ritardo (tempo di attesa in millisecondi) tra due tentativi, in caso di problema.

  Predefiniti: `60000`

* **ID utente agente**

  A seconda dell’ambiente, l’agente utilizzerà questo account utente per:

   * raccogliere e creare pacchetti di contenuti dall’ambiente di authoring
   * creare e scrivere contenuti nell’ambiente di pubblicazione

  Lascia questo campo vuoto per utilizzare l’account utente di sistema (l’account definito in sling come utente amministratore); per impostazione predefinita è `admin`).

  >[!CAUTION]
  >
  >Per un agente nell’ambiente di authoring, questo account *deve* disporre dell&#39;accesso in lettura a tutti i percorsi che si desidera replicare.

  >[!CAUTION]
  >
  >Per un agente nell’ambiente di pubblicazione, questo account *deve* disporre dell&#39;accesso di creazione/scrittura necessario per replicare il contenuto.

  >[!NOTE]
  >
  >Può essere utilizzato come meccanismo per selezionare contenuti specifici da replicare.

* **Livello registro**

  Specifica il livello di dettaglio da utilizzare per i messaggi di registro.

   * `Error`: verranno registrati solo gli errori
   * `Info`: verranno registrati errori, avvisi e altri messaggi informativi
   * `Debug`: nei messaggi verrà utilizzato un livello di dettaglio elevato, principalmente a scopo di debug

  Predefiniti: `Info`

* **Usa per replica inversa**

  Indica se questo agente verrà utilizzato per la replica inversa; restituisce l&#39;input dell&#39;utente dall&#39;ambiente di pubblicazione a quello di authoring.

* **Aggiornamento alias**

  Se si seleziona questa opzione, in Dispatcher vengono abilitate le richieste di annullamento della validità di un alias o di un percorso personalizzato. Vedi anche [Configurazione di un agente di svuotamento del Dispatcher](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Trasporto {#transport}

* **URI**

  Specifica il servlet di ricezione nella posizione di destinazione. In particolare, puoi specificare il nome host (o alias) e il percorso contestuale dell’istanza target qui.

  Ad esempio:

   * Un agente predefinito può replicare in `https://localhost:4503/bin/receive`
   * Un agente di Dispatcher Flush può replicarsi in `https://localhost:8000/dispatcher/invalidate.cache`

  Il protocollo qui specificato (HTTP o HTTPS) determinerà il metodo di trasporto.

  Per gli agenti di Dispatcher Flush, la proprietà URI viene utilizzata solo se utilizzi voci virtualhost basate sul percorso per differenziare le farm. Questo campo viene utilizzato per individuare la farm da invalidare. Ad esempio, la farm n. 1 ha l’host virtuale `www.mysite.com/path1/*` e la farm n. 2 ha l’host virtuale `www.mysite.com/path2/*`. Puoi utilizzare l’URL `/path1/invalidate.cache` per individuare la prima farm e `/path2/invalidate.cache` per individuare la seconda farm.

* **User**

  Nome utente dell’account da utilizzare per accedere alla destinazione.

* **Password**

  Password per l’account da utilizzare per accedere alla destinazione.

* **Dominio NTLM**

  Dominio per autenticazione NTML.

* **Host NTLM**

  Host per autenticazione NTML.

* **Abilita SSL relaxed**

  Abilita questa opzione se desideri che i certificati SSL autocertificati vengano accettati.

* **Consenti certificati scaduti**

  Abilita questa opzione se desideri che vengano accettati i certificati SSL scaduti.

#### Proxy {#proxy}

Le seguenti impostazioni sono necessarie solo se è necessario un proxy:

* **Host proxy**

  Nome host del proxy utilizzato per il trasporto.

* **Porta proxy**

  Porta del proxy.

* **Utente proxy**

  Nome utente dell’account da utilizzare.

* **Password proxy**

  Password dell’account da utilizzare.

* **Dominio proxy NTLM**

  Dominio proxy NTLM.

* **Host proxy NTLM**

  Dominio proxy NTLM.

#### Esteso {#extended}

* **Interfaccia**

  Qui puoi definire l’interfaccia socket a cui effettuare l’associazione.

  Consente di impostare l&#39;indirizzo locale da utilizzare per la creazione di connessioni. Se non è impostato, verrà utilizzato l’indirizzo predefinito. Questo è utile per specificare l&#39;interfaccia da utilizzare su sistemi multi-homed o cluster.

* **Metodo HTTP**

  Il metodo HTTP da utilizzare.

  Per un agente di Dispatcher Flush, questo è quasi sempre un valore GET e non deve essere modificato (POST sarebbe un altro valore possibile).

* **Intestazioni HTTP**

  Vengono utilizzati per gli agenti di Dispatcher Flush e specificano gli elementi che devono essere scaricati.

  Per un agente di Dispatcher Flush, non è necessario modificare le tre voci standard:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

  Questi vengono utilizzati, a seconda dei casi, per indicare l&#39;azione da eseguire durante lo scaricamento dell&#39;handle o del percorso. I sottoparametri sono dinamici:

   * `{action}` indica un’azione di replica

   * `{path}` indica un percorso

  Sono sostituite dal percorso/azione pertinente alla richiesta e pertanto non devono essere &quot;hardcoded&quot;:

  >[!NOTE]
  >
  >Se hai installato AEM in un contesto diverso da quello predefinito consigliato, dovrai registrare il contesto nelle intestazioni HTTP. Ad esempio:
  >`CQ-Handle:/<*yourContext*>{path}`

* **Chiudi connessione**

  Abilita questa opzione per chiudere la connessione dopo ogni richiesta.

* **Timeout di connessione**

  Timeout (in millisecondi) da applicare quando si tenta di stabilire una connessione.

* **Timeout socket**

  Timeout (in millisecondi) da applicare quando si attende il traffico dopo che è stata stabilita una connessione.

* **Versione protocollo**

  Versione del protocollo; ad esempio `1.0` per HTTP/1.0.

#### Attivatori {#triggers}

Queste impostazioni vengono utilizzate per definire i trigger per la replica automatizzata:

* **Ignora predefinito**

  Se selezionato, l&#39;agente è escluso dalla replica predefinita; ciò significa che non verrà utilizzato se un autore di contenuto richiede un&#39;azione di replica.

* **In caso di modifica**

  In questo caso, quando si modifica una pagina, viene attivata automaticamente una replica da parte di questo agente. Viene utilizzato principalmente per gli agenti di Dispatcher Flush, ma anche per la replica inversa.

* **Al momento della distribuzione**

  Se selezionato, l&#39;agente replicherà automaticamente qualsiasi contenuto contrassegnato per la distribuzione quando viene modificato.

* **Ora di attivazione/disattivazione raggiunta**

  In questo modo viene attivata la replica automatica (per attivare o disattivare una pagina in base alle esigenze) quando si verificano i tempi di attivazione o disattivazione definiti per una pagina. Viene utilizzato principalmente per gli agenti di Dispatcher Flush.

* **Al ricevimento**

  Se selezionato, l&#39;agente effettuerà la replica a catena ogni volta che riceve eventi di replica.

* **Nessun aggiornamento di stato**

  Se questa opzione è selezionata, l’agente non forzerà un aggiornamento dello stato di replica.

* **Nessun controllo delle versioni**

  Se questa opzione è selezionata, l&#39;agente non forzerà il controllo delle versioni delle pagine attivate.

## Configurazione degli agenti di replica {#configuring-your-replication-agents}

Per informazioni sulla connessione degli agenti di replica all’istanza di pubblicazione tramite MSSL, consulta [Replica tramite SSL reciproco](/help/sites-deploying/mssl-replication.md).

### Configurazione degli agenti di replica dall’ambiente di authoring {#configuring-your-replication-agents-from-the-author-environment}

Dalla scheda Strumenti nell’ambiente di authoring è possibile configurare gli agenti di replica che risiedono nell’ambiente di authoring (**Agenti per creazione**) o l’ambiente di pubblicazione (**Agenti per pubblicazione**). Le procedure seguenti illustrano la configurazione di un agente per l’ambiente di authoring, ma possono essere utilizzate per entrambi.

>[!NOTE]
>
>Quando un dispatcher gestisce le richieste HTTP per le istanze di authoring o pubblicazione, la richiesta HTTP dall’agente di replica deve includere l’intestazione PATH. Oltre alla procedura seguente, devi aggiungere l’intestazione PATH all’elenco delle intestazioni client di Dispatcher. (vedere [/clientheaders (intestazioni client)](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).
>

1. Accedere a **Strumenti** nell’AEM.
1. Clic **Replica** (riquadro sinistro per aprire la cartella).
1. Doppio clic **Agenti per creazione** (riquadro sinistro o destro).
1. Fai clic sul nome dell’agente appropriato (che è un collegamento) per visualizzare informazioni dettagliate su tale agente.
1. Clic **Modifica** per aprire la finestra di dialogo di configurazione:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. I valori forniti devono essere sufficienti per un&#39;installazione predefinita. Se si apportano modifiche, fare clic su **OK** per salvarli (vedere [Agenti di replica - Parametri di configurazione](#replication-agents-configuration-parameters) per maggiori dettagli sui singoli parametri).

>[!NOTE]
>
>Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali trasporto all’interno degli agenti di replica predefiniti.
>
>Questo deve essere modificato in un account utente di replica specifico per il sito con i privilegi per replicare i percorsi richiesti.

### Configurazione della replica inversa {#configuring-reverse-replication}

La replica inversa viene utilizzata per riportare il contenuto dell’utente generato in un’istanza Publish a un’istanza Autore. Questa funzione è comunemente utilizzata per funzioni quali sondaggi e moduli di registrazione.

Per motivi di sicurezza, la maggior parte delle topologie di rete non consente connessioni *da* la &quot;zona demilitarizzata&quot; (una sottorete che espone i servizi esterni a una rete non attendibile come Internet).

Poiché l’ambiente di pubblicazione si trova in genere nella zona demilitarizzata, per riportare il contenuto nell’ambiente di authoring la connessione deve essere avviata dall’istanza di authoring. Questa operazione viene eseguita con:

* un *posta in uscita* nell’ambiente di pubblicazione in cui viene inserito il contenuto.
* un agente (pubblicazione) nell’ambiente di authoring che esegue periodicamente il polling della casella in uscita per i nuovi contenuti.

>[!NOTE]
>
>Per AEM [Community](/help/communities/overview.md), la replica non viene utilizzata per i contenuti generati dall’utente in un’istanza di pubblicazione. Consulta [Archiviazione contenuti community](/help/communities/working-with-srp.md).

A questo scopo è necessario:

**Agente di replica inversa nell’ambiente di authoring** Agisce come componente attivo per raccogliere informazioni dalla casella in uscita nell’ambiente di pubblicazione:

Se desideri utilizzare la replica inversa, assicurati che questo agente sia attivato.

![chlimage_1-23](assets/chlimage_1-23.png)

**Agente di replica inversa nell’ambiente di pubblicazione (casella in uscita)** Questo è l’elemento passivo in quanto funge da &quot;casella in uscita&quot;. L’input dell’utente viene inserito qui, da dove viene raccolto dall’agente nell’ambiente di authoring.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configurazione della replica per più istanze di pubblicazione {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Viene replicato solo il contenuto, non i dati utente (utenti, gruppi di utenti e profili utente).
>
>Per sincronizzare i dati utente su più istanze di pubblicazione, abilita [Sincronizzazione utente](/help/sites-administering/sync.md).

Al momento dell’installazione, un agente predefinito è già configurato per la replica del contenuto in un’istanza Publish in esecuzione sulla porta 4503 dell’host locale.

Per configurare la replica dei contenuti per un’ulteriore istanza di pubblicazione è necessario creare e configurare un nuovo agente di replica:

1. Apri **Strumenti** nell’AEM.
1. Seleziona **Replica**, quindi **Agenti per creazione** nel pannello a sinistra.
1. Seleziona **Nuovo...**.
1. Imposta il **Titolo** e **Nome**, quindi seleziona **Agente di replica**.
1. Clic **Crea** per creare il nuovo agente.
1. Fai doppio clic sul nuovo elemento agente per aprire il pannello di configurazione.
1. Clic **Modifica** - il **Impostazioni agente** si aprirà la finestra di dialogo: il **Tipo di serializzazione** è già definito come predefinito, questo deve rimanere tale.

   * In **Impostazioni** scheda:

      * Attiva **Abilitato**.
      * Immetti un **Descrizione**.
      * Imposta il **Ritardo per riprovare** a `60000`.

      * Lascia **Tipo di serializzazione** as `Default`.

   * In **Trasporto** scheda:

      * Immetti l’URI richiesto per la nuova istanza di pubblicazione; ad esempio,
        `https://localhost:4504/bin/receive`.

      * Immettere l&#39;account utente specifico del sito utilizzato per la replica.
      * Se necessario, puoi configurare altri parametri.

1. Clic **OK** per salvare le impostazioni.

Puoi quindi verificare l’operazione aggiornando e pubblicando una pagina nell’ambiente di authoring.

Gli aggiornamenti verranno visualizzati su tutte le istanze di pubblicazione configurate come sopra.

In caso di problemi, puoi controllare i registri nell’istanza di authoring. A seconda del livello di dettaglio richiesto, è inoltre possibile impostare **Livello registro** a `Debug` utilizzando **Impostazioni agente** come sopra.

>[!NOTE]
>
>Questo può essere combinato con l&#39;uso del [ID utente agente](#agentuserid) per selezionare contenuti diversi da replicare nei singoli ambienti di pubblicazione. Per ogni ambiente di pubblicazione:
>
>1. Configura un agente di replica per la replica nell’ambiente di pubblicazione.
>1. Configurare un account utente con i diritti di accesso necessari per leggere il contenuto che verrà replicato in tale ambiente di pubblicazione specifico.
>1. Assegna l’account utente come **ID utente agente** per l’agente di replica.
>

### Configurazione di un agente di Dispatcher Flush {#configuring-a-dispatcher-flush-agent}

Gli agenti predefiniti sono inclusi nell&#39;installazione. Tuttavia, è ancora necessaria una determinata configurazione e lo stesso vale se si sta definendo un nuovo agente:

1. Apri **Strumenti** nell’AEM.
1. Clic **Distribuzione**.
1. Seleziona **Replica** e poi **Agenti per pubblicazione**.
1. Fai doppio clic sul pulsante **Scaricamento del Dispatcher** per aprire la panoramica.
1. Clic **Modifica** - il **Impostazioni agente** viene aperta una finestra di dialogo:

   * In **Impostazioni** scheda:

      * Attiva **Abilitato**.
      * Immetti un **Descrizione**.
      * Lascia **Tipo di serializzazione** as `Dispatcher Flush`o impostarlo come tale se si crea un nuovo agente.

      * (facoltativo) Seleziona **Aggiornamento alias** per abilitare le richieste di annullamento della validità di alias o percorsi personalizzati in Dispatcher.

   * In **Trasporto** scheda:

      * Immetti l’URI richiesto per la nuova istanza di pubblicazione; ad esempio,
        `https://localhost:80/dispatcher/invalidate.cache`.

      * Immettere l&#39;account utente specifico del sito utilizzato per la replica.
      * Se necessario, puoi configurare altri parametri.

   Per gli agenti di Dispatcher Flush, la proprietà URI viene utilizzata solo se utilizzi voci virtualhost basate sul percorso per differenziare le farm. Questo campo viene utilizzato per individuare la farm da invalidare. Ad esempio, la farm n. 1 ha l’host virtuale `www.mysite.com/path1/*` e la farm n. 2 ha l’host virtuale `www.mysite.com/path2/*`. Puoi utilizzare l’URL `/path1/invalidate.cache` per individuare la prima farm e `/path2/invalidate.cache` per individuare la seconda farm.

   >[!NOTE]
   >
   >Se hai installato AEM in un contesto diverso da quello predefinito consigliato, devi configurare [Intestazioni HTTP](#extended) nel **Esteso** scheda.

1. Clic **OK** per salvare le modifiche.
1. Torna a **Strumenti** , da qui è possibile **Attiva** il **Scaricamento del Dispatcher** agente (**Agenti per pubblicazione**).

Il **Scaricamento del Dispatcher** l’agente di replica non è attivo nell’ambiente di authoring. Puoi accedere alla stessa pagina nell’ambiente di pubblicazione utilizzando l’URI equivalente; ad esempio, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Controllo dell’accesso agli agenti di replica {#controlling-access-to-replication-agents}

L’accesso alle pagine utilizzate per configurare gli agenti di replica può essere controllato utilizzando le autorizzazioni per le pagine utente e/o gruppo in `etc/replication` nodo.

>[!NOTE]
>
>L’impostazione di tali autorizzazioni non influirà sugli utenti che replicano il contenuto (ad esempio, dalla console Siti web o dall’opzione della barra laterale). Il framework di replica non utilizza la &quot;sessione utente&quot; dell’utente corrente per accedere agli agenti di replica durante la replica delle pagine.

### Configurazione degli agenti di replica da CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>La creazione di agenti di replica è supportata solo nel `/etc/replication` posizione archivio. Questo è necessario per gestire correttamente gli ACL associati. La creazione di un agente di replica in un&#39;altra posizione della struttura potrebbe comportare l&#39;accesso non autorizzato.

Vari parametri degli agenti di replica possono essere configurati utilizzando CRXDE Lite.

Se si passa a `/etc/replication` puoi visualizzare i tre nodi seguenti:

* `agents.author`
* `agents.publish`
* `treeactivation`

I due `agents` contengono informazioni di configurazione sull’ambiente appropriato e sono attivi solo quando tale ambiente è in esecuzione. Ad esempio: `agents.publish` sarà utilizzato solo nell’ambiente di pubblicazione. La schermata seguente mostra l’agente di pubblicazione nell’ambiente di authoring, incluso in WCM per AEM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Monitoraggio degli agenti di replica {#monitoring-your-replication-agents}

Per monitorare un agente di replica:

1. Accedere a **Strumenti** nell’AEM.
1. Clic **Replica**.
1. Fare doppio clic sul collegamento agli agenti per l&#39;ambiente appropriato (il riquadro sinistro o destro); ad esempio **Agenti per creazione**.

   La finestra risultante mostra una panoramica di tutti gli agenti di replica per l’ambiente di authoring, inclusi la destinazione e lo stato.

1. Fai clic sul nome dell’agente appropriato (che è un collegamento) per visualizzare informazioni dettagliate su tale agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   È possibile:

   * Verifica se l’agente è abilitato.
   * Visualizza la destinazione di qualsiasi replica.
   * Verifica se la coda di replica è attualmente attiva (abilitata).
   * Verifica se sono presenti elementi nella coda.
   * **Aggiorna** o **Cancella** per aggiornare la visualizzazione delle voci della coda; in questo modo è possibile vedere gli elementi che entrano ed escono dalla coda.

   * **Visualizza registro** per accedere al registro di tutte le azioni eseguite dall’agente di replica.
   * **Verifica connessione** all’istanza di destinazione.
   * **Forza nuovo tentativo** su qualsiasi elemento della coda, se necessario.

   >[!CAUTION]
   >
   >Non utilizzare il collegamento &quot;Prova connessione&quot; per la cartella Posta in uscita di replica inversa in un&#39;istanza pubblicata.
   >
   >
   >Se viene eseguito un test di replica per una coda Posta in uscita, tutti gli elementi precedenti alla replica di test verranno rielaborati con ogni replica inversa.
   >
   >
   >Se tali elementi esistono già in una coda, è possibile trovarli con la seguente query XPath JCR e devono essere rimossi.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replica in batch {#batch-replication}

La replica batch non replica singole pagine o risorse, ma attende l’attivazione della prima soglia delle due, in base al tempo o alle dimensioni.

Quindi racchiude tutti gli elementi di replica in un pacchetto, che viene poi replicato come un singolo file per l’editore.

L’editore decomprime tutti gli elementi, li salva e riferisce nuovamente all’autore.

### Configurazione della replica in batch {#configuring-batch-replication}

1. Passa a `http://serveraddress:serverport/siteadmin`
1. Premere il tasto **[!UICONTROL Strumenti]** nella parte superiore dello schermo
1. Dalla barra di navigazione a sinistra, vai a **[!UICONTROL Replica - Agenti per creazione]** e doppio clic **[!UICONTROL Agente predefinito]**.
   * Puoi anche raggiungere l’agente di replica di pubblicazione predefinito andando direttamente in `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Premere il tasto **[!UICONTROL Modifica]** sopra la coda di replica.
1. Nella finestra seguente, vai a **[!UICONTROL Batch]** scheda:
   ![batchreplication](assets/batchreplication.png)
1. Configura l’agente.

### Parametri {#parameters}

* `[!UICONTROL Enable Batch Mode]` - abilita o disabilita la modalità di replica in batch
* `[!UICONTROL Max Wait Time]` - Tempo di attesa massimo, in secondi, per l&#39;avvio di una richiesta batch. Il valore predefinito è 2 secondi.
* `[!UICONTROL Trigger Size]` - Avvia la replica batch quando questo limite di dimensioni

## Risorse aggiuntive {#additional-resources}

Per informazioni dettagliate sulla risoluzione dei problemi, consultare [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md) pagina.
