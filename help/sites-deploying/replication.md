---
title: Replica
description: Scopri come configurare e monitorare gli agenti di replica in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3363'
ht-degree: 2%

---

# Replica{#replication}

Gli agenti di replica sono centrali per Adobe Experience Manager (AEM) in quanto il meccanismo utilizzato per:

* [Contenuto Publish (attiva)](/help/sites-authoring/publishing-pages.md#activatingcontent) da un ambiente Author a un ambiente Publish.
* Svuota in modo esplicito il contenuto dalla cache di Dispatcher.
* Restituisce l’input dell’utente (ad esempio, l’input del modulo) dall’ambiente Publish all’ambiente Author (sotto il controllo dell’ambiente Author).

Le richieste sono [in coda](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) per l&#39;agente appropriato per l&#39;elaborazione.

>[!NOTE]
>
>I dati utente (utenti, gruppi di utenti e profili utente) non vengono replicati tra le istanze di Author e Publish.
>
>Per più istanze di Publish, i dati utente sono distribuiti Sling quando [Sincronizzazione utente](/help/sites-administering/sync.md) è abilitato.

## Replica da Author a Publish {#replicating-from-author-to-publish}

La replica, su un’istanza di Publish o Dispatcher, avviene in diversi passaggi:

* l’Autore richiede che determinati contenuti siano pubblicati (attivati); questo può essere avviato da una richiesta manuale o da attivatori automatici preconfigurati.
* la richiesta viene passata all’agente di replica predefinito appropriato; un ambiente può avere diversi agenti predefiniti sempre selezionati per tali azioni.
* l’agente di replica &quot;crea pacchetti&quot; del contenuto e lo inserisce nella coda di replica.
* nella scheda Siti Web l&#39;indicatore di stato [colorato](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) è impostato per le singole pagine.
* il contenuto viene rimosso dalla coda e trasportato nell’ambiente Publish utilizzando il protocollo configurato; in genere si tratta di HTTP.
* un servlet nell&#39;ambiente Publish riceve la richiesta e pubblica il contenuto ricevuto; il servlet predefinito è `https://localhost:4503/bin/receive`.

* è possibile configurare più ambienti Author e Publish.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replica da Publish a Author {#replicating-from-publish-to-author}

Alcune funzioni consentono agli utenti di immettere dati in un’istanza di Publish.

A volte, per restituire i dati all’ambiente di authoring da cui vengono ridistribuiti in altri ambienti Publish, è necessario un tipo di replica noto come replica inversa. Per motivi di sicurezza, il traffico dall’ambiente Publish all’ambiente di authoring deve essere controllato rigorosamente.

La replica inversa utilizza un agente nell’ambiente Publish che fa riferimento all’ambiente di authoring. Questo agente inserisce i dati in una casella in uscita. Questa casella in uscita corrisponde ai listener di replica nell’ambiente di authoring. I listener eseguono il polling delle caselle in uscita per raccogliere i dati immessi e quindi distribuirli in base alle esigenze. In questo modo l’ambiente di authoring controlla tutto il traffico.

In altri casi, come per le funzioni di Communities (ad esempio forum, blog, commenti e recensioni), la quantità di contenuti generati dagli utenti (UGC, User-Generated Content) immessi nell’ambiente Publish è difficile da sincronizzare in modo efficiente tra le istanze AEM utilizzando la replica.

[Communities](/help/communities/overview.md) dell&#39;AEM non utilizza mai la replica per UGC. La distribuzione per Communities richiede invece un archivio comune per UGC (vedi [Archiviazione contenuto community](/help/communities/working-with-srp.md)).

### Replica: funzioni pronte all’uso {#replication-out-of-the-box}

Il sito web we-retail incluso in un&#39;installazione standard di AEM può essere utilizzato per illustrare la replica.

Per seguire questo esempio e utilizzare gli agenti di replica predefiniti, [installa AEM](/help/sites-deploying/deploy.md) con:

* ambiente di authoring sulla porta `4502`
* ambiente Publish sulla porta `4503`

>[!NOTE]
>
>Attivato per impostazione predefinita:
>
>* Agenti per creazione: agente predefinito (pubblicazione)
>
>Effettivamente disabilitati per impostazione predefinita (a partire da AEM 6.1) :
>
>* Agenti per creazione: agente di replica inversa (publish_reverse)
>* Agenti in Publish: replica inversa (casella in uscita)
>
>Per verificare lo stato dell&#39;agente o della coda, utilizzare la console **Strumenti**.
>Consulta [Monitoraggio degli agenti di replica](#monitoring-your-replication-agents).

#### Replica (da authoring a Publish) {#replication-author-to-publish}

1. Passa alla pagina di supporto nell’ambiente di authoring.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Modifica la pagina in modo da poter aggiungere nuovo testo.
1. **Attiva pagina** per pubblicare le modifiche.
1. Apri la pagina Supporto nell’ambiente Publish:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Ora puoi vedere le modifiche inserite al momento dell’authoring.

Questa replica viene eseguita dall’ambiente di authoring in base a:

* **Agente predefinito (pubblicazione)**
Questo agente replica il contenuto nell’istanza predefinita di Publish.
I dettagli di questo (configurazione e registri) sono accessibili dalla console Strumenti dell’ambiente di authoring; oppure:
  `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agenti di replica - Pronti all’uso {#replication-agents-out-of-the-box}

I seguenti agenti sono disponibili in un&#39;installazione standard per AEM:

* [Agente predefinito](#replication-author-to-publish)
Utilizzato per la replica da Author a Publish.

* Svuotamento Dispatcher
Viene utilizzato per la gestione della cache di Dispatcher. Per ulteriori informazioni, vedere [Annullamento della validità della cache di Dispatcher dall&#39;ambiente di authoring](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) e [Annullamento della validità della cache di Dispatcher da un&#39;istanza di pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance).

* [Replica inversa](#reverse-replication-publish-to-author)
Utilizzato per la replica da Publish a Author. La replica inversa non viene utilizzata per le funzioni di Communities, ad esempio forum, blog e commenti. Viene effettivamente disattivata in quanto la casella in uscita non è abilitata. L’utilizzo della replica inversa richiederebbe una configurazione personalizzata.

* Agente statico
Si tratta di un &quot;agente che memorizza una rappresentazione statica di un nodo nel file system&quot;.
Ad esempio, con le impostazioni predefinite, le pagine di contenuto e le risorse DAM vengono memorizzate in `/tmp`, come HTML o nel formato di risorsa appropriato. Vedere le schede `Settings` e `Rules` per la configurazione.
Questa richiesta consentiva di visualizzare il contenuto quando la pagina veniva richiesta direttamente dal server dell’applicazione. Si tratta di un agente specializzato e (probabilmente) non è necessario per la maggior parte delle istanze.

## Agenti di replica - Parametri di configurazione {#replication-agents-configuration-parameters}

Durante la configurazione di un agente di replica dalla console Strumenti, nella finestra di dialogo sono disponibili quattro schede:

### Impostazioni {#settings}

* **Nome**

  Nome univoco dell’agente di replica.

* **Descrizione**

  Una descrizione dello scopo fornito da questo agente di replica.

* **Abilitato**

  Indica se l’agente di replica è abilitato.

  Quando l&#39;agente è **abilitato**, la coda viene visualizzata come:

   * **Attivo** durante l&#39;elaborazione degli elementi.
   * **Inattivo** quando la coda è vuota.
   * **Bloccato** quando gli elementi sono in coda, ma non possono essere elaborati; ad esempio, quando la coda di ricezione è disabilitata.

* **Tipo di serializzazione**

  Tipo di serializzazione:

   * **Predefinito**: imposta se l&#39;agente deve essere selezionato automaticamente.
   * **Svuotamento del Dispatcher**: selezionare questa opzione se l&#39;agente deve essere utilizzato per svuotare la cache di Dispatcher.

* **Ritardo per riprovare**

  Ritardo (tempo di attesa in millisecondi) tra due tentativi, in caso di problema.

  Predefinito: `60000`

* **ID utente agente**

  A seconda dell’ambiente, l’agente utilizza questo account utente per:

   * raccogliere e creare pacchetti di contenuti dall’ambiente di authoring;
   * creare e scrivere contenuti nell’ambiente Publish

  Lascia questo campo vuoto per utilizzare l’account utente di sistema (l’account definito in sling come utente amministratore; per impostazione predefinita è `admin`).

  >[!CAUTION]
  >
  >Per un agente nell&#39;ambiente di authoring questo account *deve* disporre dell&#39;accesso in lettura a tutti i percorsi che si desidera replicare.

  >[!CAUTION]
  >
  >Per un agente nell&#39;ambiente Publish questo account *deve* disporre dell&#39;accesso di creazione/scrittura necessario per replicare il contenuto.

  >[!NOTE]
  >
  >Può essere utilizzato come meccanismo per selezionare contenuti specifici da replicare.

* **Livello registro**

  Specifica il livello di dettaglio da utilizzare per i messaggi di registro.

   * `Error`: vengono registrati solo gli errori
   * `Info`: errori, avvisi e altri messaggi informativi registrati
   * `Debug`: nei messaggi viene utilizzato un livello di dettaglio elevato, principalmente a scopo di debug

  Predefinito: `Info`

* **Usa per replica inversa**

  Indica se questo agente viene utilizzato per la replica inversa; restituisce l&#39;input dell&#39;utente dall&#39;ambiente Publish all&#39;ambiente Author.

* **Aggiornamento alias**

  Selezionando questa opzione si abilitano le richieste di annullamento della validità di un alias o di un percorso personalizzato a Dispatcher. Vedere anche [Configurazione di un agente di svuotamento del Dispatcher](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Trasporto {#transport}

* **URI**

  Specifica il servlet di ricezione nella posizione di destinazione. In particolare, puoi specificare il nome host (o alias) e il percorso contestuale dell’istanza target qui.

  Ad esempio:

   * Un agente predefinito può replicare in `https://localhost:4503/bin/receive`
   * Un agente di Dispatcher Flush può replicarsi in `https://localhost:8000/dispatcher/invalidate.cache`

  Il protocollo qui specificato (HTTP o HTTPS) determina il metodo di trasporto.

  Per gli agenti di Dispatcher Flush, la proprietà URI viene utilizzata solo se utilizzi voci virtualhost basate sul percorso per differenziare le farm. Utilizza questo campo per individuare la farm da invalidare. Ad esempio, la farm n. 1 ha l’host virtuale `www.mysite.com/path1/*` e la farm n. 2 ha l’host virtuale `www.mysite.com/path2/*`. È possibile utilizzare l&#39;URL `/path1/invalidate.cache` per individuare la prima farm e `/path2/invalidate.cache` per individuare la seconda farm.

* **Utente**

  Il nome utente dell’account da utilizzare per accedere alla destinazione.

* **Password**

  Password per l’account da utilizzare per accedere alla destinazione.

* **Dominio NTLM**

  Dominio per autenticazione NTML.

* **Host NTLM**

  Host per autenticazione NTML.

* **Abilita SSL rilassato**

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

  Il nome utente dell’account da utilizzare.

* **Password proxy**

  Password dell’account da utilizzare.

* **Dominio proxy NTLM**

  Dominio proxy NTLM.

* **Host proxy NTLM**

  Dominio proxy NTLM.

#### Esteso {#extended}

* **Interfaccia**

  Qui puoi definire l’interfaccia socket a cui effettuare l’associazione.

  Consente di impostare l&#39;indirizzo locale da utilizzare per la creazione di connessioni. Se non è impostato, viene utilizzato l’indirizzo predefinito. Questo è utile per specificare l&#39;interfaccia da utilizzare su sistemi multi-homed o cluster.

* **Metodo HTTP**

  Il metodo HTTP da utilizzare.

  Per un agente di Dispatcher Flush, questo valore è quasi sempre GET e non deve essere modificato (POST sarebbe un altro valore possibile).

* **Intestazioni HTTP**

  Vengono utilizzati per gli agenti di Dispatcher Flush e specificano gli elementi che devono essere scaricati.

  Per un agente di Dispatcher Flush, non è necessario modificare le tre voci standard:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

  Questi vengono utilizzati, a seconda dei casi, per indicare l&#39;azione da eseguire durante lo scaricamento dell&#39;handle o del percorso. I sottoparametri sono dinamici:

   * `{action}` indica un&#39;azione di replica

   * `{path}` indica un percorso

  Sono sostituite dal percorso/azione pertinente alla richiesta e pertanto non devono essere &quot;hardcoded&quot;:

  >[!NOTE]
  >
  >Se hai installato AEM in un contesto diverso da quello predefinito consigliato, devi registrare il contesto nelle intestazioni HTTP. Ad esempio:
  >`CQ-Handle:/<*yourContext*>{path}`

* **Chiudi connessione**

  Abilita questa opzione in modo da poter chiudere la connessione dopo ogni richiesta.

* **Timeout connessione**

  Timeout (in millisecondi) da applicare quando si tenta di stabilire una connessione.

* **Timeout socket**

  Timeout (in millisecondi) da applicare quando si attende il traffico dopo che è stata stabilita una connessione.

* **Versione protocollo**

  Versione del protocollo. Ad esempio, `1.0` per HTTP/1.0.

#### Trigger {#triggers}

Queste impostazioni vengono utilizzate per definire i trigger per la replica automatizzata:

* **Ignora predefinito**

  Se selezionato, l&#39;agente viene escluso dalla replica predefinita, ovvero non viene utilizzato se un autore di contenuto esegue un&#39;azione di replica.

* **In caso di modifica**

  In questo caso, quando viene modificata una pagina, viene attivata automaticamente una replica da parte di questo agente. Utilizzato per gli agenti di Dispatcher Flush, ma anche per la replica inversa.

* **Alla distribuzione**

  Se selezionato, l&#39;agente replica automaticamente qualsiasi contenuto contrassegnato per la distribuzione quando viene modificato.

* **Ora di attivazione/disattivazione raggiunta**

  Questa funzione attiva la replica automatica (per attivare o disattivare una pagina in base alle esigenze) quando si verificano i tempi di attivazione o disattivazione definiti per una pagina. Viene utilizzato principalmente per gli agenti di Dispatcher Flush.

* **Alla ricezione**

  Se questa opzione è selezionata, le catene di agenti vengono replicate ogni volta che ricevono eventi di replica.

* **Nessun aggiornamento di stato**

  Se questa opzione è selezionata, l’agente non forza un aggiornamento dello stato di replica.

* **Nessun controllo delle versioni**

  Se questa opzione è selezionata, l&#39;agente non forza il controllo delle versioni delle pagine attivate.

## Configurazione degli agenti di replica {#configuring-your-replication-agents}

Per informazioni sulla connessione degli agenti di replica all&#39;istanza di Publish tramite MSSL, vedere [Replica con SSL reciproco](/help/sites-deploying/mssl-replication.md).

### Configurazione degli agenti di replica dall’ambiente di authoring {#configuring-your-replication-agents-from-the-author-environment}

Dalla scheda Strumenti nell&#39;ambiente di authoring è possibile configurare gli agenti di replica che risiedono nell&#39;ambiente di authoring (**Agenti nell&#39;ambiente di authoring**) o nell&#39;ambiente di Publish (**Agenti in Publish**). Le procedure seguenti illustrano la configurazione di un agente per l’ambiente di authoring, ma possono essere utilizzate per entrambi.

>[!NOTE]
>
>Quando un Dispatcher gestisce le richieste HTTP per le istanze Author o Publish, la richiesta HTTP dell’agente di replica deve includere l’intestazione PATH. Oltre alla procedura seguente, è necessario aggiungere l’intestazione PATH all’elenco delle intestazioni client di Dispatcher. Vedere [/clientheaders (Client Headers)](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).
>

1. Accedi alla scheda **Strumenti** in AEM.
1. Fai clic su **Replica** (riquadro a sinistra per aprire la cartella).
1. Fare doppio clic su **Agenti in Author** (nel riquadro sinistro o destro).
1. Fai clic sul nome dell’agente appropriato (che è un collegamento) per visualizzare informazioni dettagliate su tale agente.
1. Fare clic su **Modifica** per aprire la finestra di dialogo di configurazione:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. I valori forniti devono essere sufficienti per un&#39;installazione predefinita. Se si apportano modifiche, fare clic su **OK** per salvarle (vedere [Agenti di replica - Parametri di configurazione](#replication-agents-configuration-parameters) per informazioni sui singoli parametri).

>[!NOTE]
>
>Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali di trasporto all&#39;interno degli agenti di replica predefiniti.
>
>Questo deve essere modificato in un account utente di replica specifico per il sito con i privilegi per replicare i percorsi richiesti.

### Configurazione della replica inversa {#configuring-reverse-replication}

La replica inversa viene utilizzata per restituire il contenuto dell’utente generato in un’istanza di Publish a un’istanza di authoring. Questa funzione è comunemente utilizzata per funzioni quali sondaggi e moduli di registrazione.

Per motivi di sicurezza, la maggior parte delle topologie di rete non consente connessioni *da* alla &quot;zona demilitarizzata&quot; (una sottorete che espone i servizi esterni a una rete non attendibile come Internet).

Poiché l’ambiente Publish si trova in genere nella zona demilitarizzata, per riportare il contenuto nell’ambiente di authoring la connessione deve essere avviata dall’istanza di authoring. Questa operazione viene eseguita con:

* una *casella in uscita* nell&#39;ambiente Publish in cui viene inserito il contenuto.
* un agente (pubblicazione) nell’ambiente di authoring che esegue periodicamente il polling della casella in uscita per i nuovi contenuti.

>[!NOTE]
>
>Per le [community](/help/communities/overview.md) dell&#39;AEM, la replica non viene utilizzata per i contenuti generati dall&#39;utente in un&#39;istanza di Publish. Vedi [Archiviazione dei contenuti della community](/help/communities/working-with-srp.md).

A questo scopo, è necessario:

**Agente di replica inversa nell&#39;ambiente di authoring** - Agisce come componente attivo per raccogliere informazioni dalla cartella Posta in uscita nell&#39;ambiente Publish:

Se desideri utilizzare la replica inversa, assicurati che questo agente sia attivato.

![chlimage_1-23](assets/chlimage_1-23.png)

**Agente di replica inversa nell&#39;ambiente Publish (casella in uscita)** - L&#39;elemento passivo funge da &quot;casella in uscita&quot;. L’input dell’utente viene inserito qui, da dove viene raccolto dall’agente nell’ambiente di authoring.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configurazione della replica per più istanze di Publish {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Viene replicato solo il contenuto, non i dati utente (utenti, gruppi di utenti e profili utente).
>
>Per sincronizzare i dati utente in più istanze di Publish, abilitare [Sincronizzazione utente](/help/sites-administering/sync.md).

Dopo l&#39;installazione, un agente predefinito è già configurato per la replica del contenuto in un&#39;istanza di Publish in esecuzione sulla porta 4503 dell&#39;host locale.

Per configurare la replica dei contenuti per un’ulteriore istanza di Publish, crea e configura un nuovo agente di replica:

1. Apri la scheda **Strumenti** in AEM.
1. Seleziona **Replica**, quindi **Agenti per creazione** nel pannello a sinistra.
1. Seleziona **Nuovo...**.
1. Imposta **Title** e **Name**, quindi seleziona **Replication Agent**.
1. Fai clic su **Crea** per creare l&#39;agente.
1. Fai doppio clic sul nuovo elemento agente per aprire il pannello di configurazione.
1. Fare clic su **Modifica**. Verrà visualizzata la finestra di dialogo **Impostazioni agente**. Il tipo di serializzazione **è già definito come predefinito, ma deve rimanere tale.**

   * Nella scheda **Impostazioni**:

      * Attiva **Abilitato**.
      * Immetti una **Descrizione**.
      * Imposta **Ritardo per riprovare** su `60000`.

      * Lascia **Tipo di serializzazione** come `Default`.

   * Nella scheda **Trasporto**:

      * Immetti l’URI richiesto per la nuova istanza di Publish; ad esempio,
        `https://localhost:4504/bin/receive`.

      * Immettere l&#39;account utente specifico del sito utilizzato per la replica.
      * Se necessario, puoi configurare altri parametri.

1. Fai clic su **OK**.

Puoi quindi verificare l’operazione aggiornando e pubblicando una pagina nell’ambiente di authoring.

Gli aggiornamenti vengono visualizzati in tutte le istanze di Publish configurate come sopra.

In caso di problemi, puoi controllare i registri nell’istanza Autore. A seconda del livello di dettaglio richiesto, è inoltre possibile impostare **Log Level** su `Debug` utilizzando la finestra di dialogo **Agent Settings** come indicato sopra.

>[!NOTE]
>
>Questo può essere combinato con l&#39;uso dell&#39;[ID utente agente](#agentuserid) per selezionare contenuti diversi da replicare nei singoli ambienti Publish. Per ogni ambiente Publish:
>
>1. Configurare un agente di replica per la replica in tale ambiente Publish.
>1. Configurare un account utente con i diritti di accesso necessari per leggere il contenuto replicato in tale ambiente Publish specifico.
>1. Assegnare l&#39;account utente come **ID utente agente** per l&#39;agente di replica.
>

### Configurazione di un agente di Dispatcher Flush {#configuring-a-dispatcher-flush-agent}

Gli agenti predefiniti sono inclusi nell&#39;installazione. Tuttavia, è ancora necessaria una determinata configurazione e lo stesso vale se si sta definendo un nuovo agente:

1. Apri la scheda **Strumenti** in AEM.
1. Fare clic su **Distribuzione**.
1. Selezionare **Replica** e quindi **Agenti in Publish**.
1. Fai doppio clic sull&#39;elemento **Svuotamento del Dispatcher** per aprire la panoramica.
1. Fare clic su **Modifica**. Verrà visualizzata la finestra di dialogo **Impostazioni agente**:

   * Nella scheda **Impostazioni**:

      * Attiva **Abilitato**.
      * Immetti una **Descrizione**.
      * Lasciare **Tipo di serializzazione** come `Dispatcher Flush` o impostarlo come tale se si crea un agente.

      * (facoltativo) Seleziona **Aggiornamento alias** per abilitare le richieste di annullamento della validità di un alias o di un percorso personalizzato in Dispatcher.

   * Nella scheda **Trasporto**:

      * Immetti l’URI richiesto per la nuova istanza di Publish; ad esempio,
        `https://localhost:80/dispatcher/invalidate.cache`.

      * Immettere l&#39;account utente specifico del sito utilizzato per la replica.
      * Se necessario, puoi configurare altri parametri.

   Per gli agenti di Dispatcher Flush, la proprietà URI viene utilizzata solo se utilizzi voci virtualhost basate sul percorso per differenziare le farm. Utilizza questo campo per individuare la farm da invalidare. Ad esempio, la farm n. 1 ha l’host virtuale `www.mysite.com/path1/*` e la farm n. 2 ha l’host virtuale `www.mysite.com/path2/*`. È possibile utilizzare l&#39;URL `/path1/invalidate.cache` per individuare la prima farm e `/path2/invalidate.cache` per individuare la seconda farm.

   >[!NOTE]
   >
   >Se hai installato AEM in un contesto diverso da quello predefinito consigliato, configura le [intestazioni HTTP](#extended) nella scheda **Extended**.

1. Fai clic su **OK**.
1. Torna alla scheda **Strumenti**, da qui puoi **Attivare** l&#39;agente **Dispatcher Flush** (**Agenti in Publish**).

L&#39;agente di replica **Dispatcher Flush** non è attivo nell&#39;istanza di authoring. È possibile accedere alla stessa pagina nell&#39;ambiente Publish utilizzando l&#39;URI equivalente, ad esempio `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Controllo dell’accesso agli agenti di replica {#controlling-access-to-replication-agents}

L&#39;accesso alle pagine utilizzate per configurare gli agenti di replica può essere controllato utilizzando le autorizzazioni per le pagine utente e/o di gruppo nel nodo `etc/replication`.

>[!NOTE]
>
>L’impostazione di tali autorizzazioni non influisce sugli utenti che replicano il contenuto (ad esempio, dalla console Siti web o dall’opzione della barra laterale). Il framework di replica non utilizza la &quot;sessione utente&quot; dell’utente corrente per accedere agli agenti di replica durante la replica delle pagine.

### Configurazione degli agenti di replica da CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>La creazione di agenti di replica è supportata solo nel percorso dell&#39;archivio `/etc/replication`. Questo è necessario per gestire correttamente gli ACL associati. La creazione di un agente di replica in un&#39;altra posizione della struttura potrebbe comportare l&#39;accesso non autorizzato.

Vari parametri degli agenti di replica possono essere configurati utilizzando CRXDE Lite.

Se si passa a `/etc/replication`, è possibile visualizzare i tre nodi seguenti:

* `agents.author`
* `agents.publish`
* `treeactivation`

I due `agents` contengono informazioni di configurazione sull&#39;ambiente appropriato e sono attivi solo quando tale ambiente è in esecuzione. `agents.publish`, ad esempio, viene utilizzato solo nell&#39;ambiente Publish. La schermata seguente mostra l’agente Publish nell’ambiente di authoring, incluso in WCM per AEM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Monitoraggio degli agenti di replica {#monitoring-your-replication-agents}

Per monitorare un agente di replica:

1. Accedi alla scheda **Strumenti** in AEM.
1. Fare clic su **Replica**.
1. Fare doppio clic sul collegamento agli agenti per l&#39;ambiente appropriato (nel riquadro sinistro o destro). Ad esempio, **Agenti su Author**.

   La finestra risultante mostra una panoramica di tutti gli agenti di replica per l’ambiente di authoring, inclusi la destinazione e lo stato.

1. Fai clic sul nome dell’agente appropriato (che è un collegamento) per visualizzare informazioni dettagliate su tale agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Qui puoi effettuare le seguenti operazioni:

   * Verifica se l’agente è abilitato.
   * Visualizza la destinazione di qualsiasi replica.
   * Verifica se la coda di replica è attiva (abilitata).
   * Verifica se sono presenti elementi nella coda.
   * **Aggiorna** o **Cancella** per aggiornare la visualizzazione delle voci della coda. Questo ti aiuta a vedere che gli elementi entrano ed escono dalla coda.

   * **Visualizza registro** per accedere al registro di tutte le azioni eseguite dall&#39;agente di replica.
   * **Verifica connessione** all&#39;istanza di destinazione.
   * **Forza nuovo tentativo** su qualsiasi elemento della coda, se necessario.

   >[!CAUTION]
   >
   >Non utilizzare il collegamento &quot;Prova connessione&quot; per la cartella Posta in uscita di replica inversa in un&#39;istanza di Publish.
   >
   >
   >Se viene eseguito un test di replica per una coda Posta in uscita, tutti gli elementi precedenti alla replica del test vengono rielaborati con ogni replica inversa.
   >
   >
   >Se tali elementi sono presenti in una coda, è possibile trovarli con la seguente query XPath JCR e devono essere rimossi.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replica in batch {#batch-replication}

La replica batch non replica singole pagine o risorse, ma attende l’attivazione della prima soglia delle due, in base al tempo o alle dimensioni.

Tutti gli elementi di replica vengono quindi inseriti in un pacchetto, che viene quindi replicato come un singolo file nel server di pubblicazione.

Il server di pubblicazione decomprime tutti gli elementi, li salva e riporta all&#39;autore.

### Configurazione della replica in batch {#configuring-batch-replication}

1. Vai a `http://serveraddress:serverport/siteadmin`
1. Premi l&#39;icona **[!UICONTROL Strumenti]** nella parte superiore dello schermo
1. Dalla barra di navigazione a sinistra, vai a **[!UICONTROL Replica - Agenti in Author]** e fai doppio clic su **[!UICONTROL Agente predefinito]**.
   * È inoltre possibile raggiungere l&#39;agente di replica predefinito di Publish andando direttamente in `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Premere il pulsante **[!UICONTROL Modifica]** sopra la coda di replica.
1. Nella finestra seguente, passare alla scheda **[!UICONTROL Batch]**:
   ![batchreplication](assets/batchreplication.png)
1. Configura l’agente.

### Parametri {#parameters}

* `[!UICONTROL Enable Batch Mode]` - abilita o disabilita la modalità di replica batch
* `[!UICONTROL Max Wait Time]` - Tempo di attesa massimo per l&#39;avvio di una richiesta batch, in secondi. Il valore predefinito è 2 secondi.
* `[!UICONTROL Trigger Size]` - Avvia la replica batch quando questo limite di dimensioni

## Risorse aggiuntive {#additional-resources}

Per informazioni dettagliate sulla risoluzione dei problemi, leggere la pagina [Risoluzione dei problemi di replica](/help/sites-deploying/troubleshoot-rep.md).
