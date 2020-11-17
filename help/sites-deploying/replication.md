---
title: Replica
seo-title: Replica
description: Scoprite come configurare e monitorare gli agenti di replica in AEM.
seo-description: Scoprite come configurare e monitorare gli agenti di replica in AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
translation-type: tm+mt
source-git-commit: 480e1f62e34783295133d10451ec409cf3a8bb0b
workflow-type: tm+mt
source-wordcount: '3661'
ht-degree: 3%

---


# Replica{#replication}

Gli agenti di replica sono fondamentali per Adobe Experience Manager (AEM) come meccanismo utilizzato per:

* [Pubblicare (attivare)](/help/sites-authoring/publishing-pages.md#activatingcontent) il contenuto da un autore a un ambiente di pubblicazione.
* Elimina esplicitamente il contenuto dalla cache del dispatcher.
* Restituire l’input dell’utente (ad esempio, l’input del modulo) dall’ambiente di pubblicazione all’ambiente di authoring (controllato dall’ambiente di authoring).

Le richieste vengono [messe in coda](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) all&#39;agente appropriato per l&#39;elaborazione.

>[!NOTE]
>
>I dati utente (utenti, gruppi di utenti e profili utente) non vengono replicati tra le istanze di creazione e pubblicazione.
>
>Per più istanze di pubblicazione, i dati utente sono distribuiti Sling quando è abilitata la sincronizzazione [](/help/sites-administering/sync.md) utente.

## Replica da Author a Publish {#replicating-from-author-to-publish}

La replica in un’istanza di pubblicazione o in un dispatcher avviene in diversi passaggi:

* l’autore richiede che alcuni contenuti vengano pubblicati (attivati); questo può essere avviato da una richiesta manuale o da attivatori automatici preconfigurati.
* la richiesta viene trasmessa all&#39;agente di replica predefinito appropriato; un ambiente può avere diversi agenti predefiniti che saranno sempre selezionati per tali azioni.
* l&#39;agente di replica &quot;crea un pacchetto&quot; del contenuto e lo inserisce nella coda di replica.
* nella scheda Siti Web l’indicatore [di stato](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) colorato è impostato per le singole pagine.
* il contenuto viene sollevato dalla coda e trasportato all&#39;ambiente di pubblicazione utilizzando il protocollo configurato; in genere si tratta di HTTP.
* un servlet nell’ambiente di pubblicazione riceve la richiesta e pubblica il contenuto ricevuto; il servlet predefinito è `https://localhost:4503/bin/receive`.

* è possibile configurare più ambienti di creazione e pubblicazione.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replica da Pubblica a Autore {#replicating-from-publish-to-author}

Alcune funzioni consentono agli utenti di inserire i dati in un’istanza di pubblicazione.

In alcuni casi, per restituire questi dati all’ambiente di authoring da cui vengono redistribuiti ad altri ambienti di pubblicazione è necessario un tipo di replica noto come replica inversa. Per motivi di sicurezza, il traffico dall’ambiente di pubblicazione all’ambiente di authoring deve essere rigorosamente controllato.

La replica inversa utilizza un agente nell&#39;ambiente di pubblicazione che fa riferimento all&#39;ambiente di authoring. Questo agente inserisce i dati in una casella in uscita. Questa casella in uscita viene associata ai listener di replica nell&#39;ambiente di authoring. I listener eseguono il polling delle caselle di posta in uscita per raccogliere i dati immessi e quindi distribuirli secondo necessità. In questo modo l’ambiente di authoring controlla tutto il traffico.

In altri casi, ad esempio per le funzioni Community (ad esempio, forum, blog, commenti e revisioni), la quantità di contenuto generato dall’utente (UGC) immesso nell’ambiente di pubblicazione è difficile da sincronizzare efficacemente tra AEM istanze utilizzando la replica.

AEM [Communities](/help/communities/overview.md) non utilizza mai la replica per UGC. Al contrario, la distribuzione per Communities richiede uno store comune per UGC (consultate [Community Content Storage](/help/communities/working-with-srp.md)).

### Replica - Out of the Box {#replication-out-of-the-box}

Il sito Web Web di vendita al dettaglio incluso in un&#39;installazione standard di AEM può essere utilizzato per illustrare la replica.

Per seguire questo esempio e utilizzare gli agenti di replica predefiniti è necessario [installare AEM](/help/sites-deploying/deploy.md) con:

* l’ambiente di authoring sulla porta `4502`
* l&#39;ambiente di pubblicazione sulla porta `4503`

>[!NOTE]
>
>Opzione attivata per impostazione predefinita :
>
>* Agenti sull&#39;autore : Agente predefinito (pubblicazione)
>
>
Effettivamente disattivato per impostazione predefinita (a partire dal AEM 6.1):
>
>* Agenti sull&#39;autore : Agente replica inversa (publish_reverse)
>* Agenti in pubblicazione : Replica inversa (in uscita)

>
>
Per verificare lo stato dell’agente o della coda, utilizzate la console **Strumenti** .
>Vedere [Monitoraggio degli agenti](#monitoring-your-replication-agents)di replica.

#### Replica (autore per la pubblicazione) {#replication-author-to-publish}

1. Passate alla pagina del supporto nell’ambiente di authoring.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Modificate la pagina per aggiungere del nuovo testo.
1. **Attivate Pagina** per pubblicare le modifiche.
1. Aprite la pagina del supporto nell’ambiente di pubblicazione:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. È ora possibile visualizzare le modifiche immesse durante l’authoring.

Questa replica viene eseguita dall’ambiente di authoring tramite:

* **Agente predefinito (pubblicazione)**Questo agente replica il contenuto nell’istanza di pubblicazione predefinita.
Per informazioni dettagliate, consultate la console Strumenti dell’ambiente di authoring (configurazione e registri); oppure:

   `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agenti di replica - Out of the Box {#replication-agents-out-of-the-box}

I seguenti agenti sono disponibili in un&#39;installazione standard AEM:

* [Agente](#replication-author-to-publish)predefinito utilizzato per la replica dall&#39;autore alla pubblicazione.

* Dispatcher FlushViene utilizzato per gestire la cache del Dispatcher. Per ulteriori informazioni, consulta [Invalidazione della cache del dispatcher dall’ambiente](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) di authoring e [Invalidazione della cache del dispatcher da un’istanza](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) di pubblicazione.

* [Replica inversa](#reverse-replication-publish-to-author)utilizzata per la replica dalla pubblicazione all’authoring. La replica inversa non viene utilizzata per le funzioni Community, come forum, blog e commenti. È effettivamente disattivato perché la casella in uscita non è abilitata. L&#39;utilizzo della replica inversa richiede una configurazione personalizzata.

* Agente statico: &quot;Agente che memorizza una rappresentazione statica di un nodo nel file system.&quot;
Ad esempio, con le impostazioni predefinite, le pagine di contenuto e le risorse DAM sono memorizzate in `/tmp`, come HTML o nel formato di risorsa appropriato. Vedere le schede `Settings` e `Rules` la configurazione.
Questo è stato richiesto in modo che, quando la pagina viene richiesta direttamente dal server applicazioni, il contenuto possa essere visualizzato. Si tratta di un agente specializzato e (probabilmente) non sarà richiesto per la maggior parte dei casi.

## Agenti di replica - Parametri di configurazione {#replication-agents-configuration-parameters}

Quando si configura un agente di replica dalla console Strumenti, nella finestra di dialogo sono disponibili quattro schede:

### Impostazioni {#settings}

* **Nome**

   Un nome univoco per l&#39;agente di replica.

* **Descrizione**

   Descrizione della funzione che verrà utilizzata dall&#39;agente di replica.

* **Abilitato**

   Indica se l&#39;agente di replica è attualmente abilitato.

   Quando l&#39;agente è **abilitato** , la coda viene visualizzata come:

   * **Attivo** quando gli elementi vengono elaborati.
   * **Inattivo** quando la coda è vuota.
   * **Bloccato** quando gli elementi sono in coda, ma non possono essere elaborati; ad esempio, quando la coda di ricezione è disabilitata.

* **Tipo di serializzazione**

   Tipo di serializzazione:

   * **Predefinito**: Impostare se l&#39;agente deve essere selezionato automaticamente.
   * **Dispatcher Flush**: Selezionare questa opzione se l&#39;agente deve essere utilizzato per cancellare la cache del dispatcher.

* **Ritardo per riprovare**

   Il ritardo (in millisecondi) tra due tentativi, in caso di problemi.

   Impostazione predefinita: `60000`

* **ID utente agente**

   A seconda dell&#39;ambiente, l&#39;agente utilizzerà questo account utente per:

   * raccogliere e creare pacchetti di contenuti dall’ambiente di authoring
   * creare e scrivere il contenuto nell’ambiente di pubblicazione

   Lasciate questo campo vuoto per usare l’account utente del sistema (l’account definito in sling come utente amministratore); per impostazione predefinita, è `admin`).

   >[!CAUTION]
   >
   >Per un agente nell’ambiente di authoring questo account *deve* disporre dell’accesso in lettura a tutti i percorsi che si desidera replicare.

   >[!CAUTION]
   >
   >Per un agente nell’ambiente di pubblicazione, questo account *deve* disporre dell’accesso in scrittura e creazione necessario per replicare il contenuto.

   >[!NOTE]
   >
   >Può essere utilizzato come meccanismo per selezionare contenuti specifici per la replica.

* **Livello registro**

   Specifica il livello di dettaglio da utilizzare per i messaggi di registro.

   * `Error`: verranno registrati solo gli errori
   * `Info`: verranno registrati errori, avvisi e altri messaggi informativi
   * `Debug`: nei messaggi verrà utilizzato un elevato livello di dettaglio, principalmente a scopo di debug

   Impostazione predefinita: `Info`

* **Usa per replica inversa**

   Indica se questo agente verrà utilizzato per la replica inversa; restituisce l’input dell’utente dall’ambiente di pubblicazione all’ambiente di creazione.

* **Aggiornamento alias**

   Selezionando questa opzione, le richieste di annullamento convalida di alias o percorso vanità vengono abilitate al dispatcher. Consultate anche [Configurazione di un agente](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent)di scaricamento del dispatcher.

#### Trasporto {#transport}

* **URI**

   Indica il servlet di ricezione nella posizione di destinazione. In particolare, è possibile specificare il nome host (o alias) e il percorso contestuale dell&#39;istanza di destinazione.

   Esempio:

   * Un agente predefinito può replicare `https://localhost:4503/bin/receive`
   * Un agente Dispatcher Flush può replicare in `https://localhost:8000/dispatcher/invalidate.cache`

   Il protocollo specificato qui (HTTP o HTTPS) determinerà il metodo di trasporto.

   Per gli agenti Dispatcher Flush, la proprietà URI viene utilizzata solo se si utilizzano voci virtualhost basate sul percorso per distinguere tra le farm, è possibile utilizzare questo campo per eseguire il targeting della farm per annullare la validità. Ad esempio, la farm n. 1 ha un host virtuale di `www.mysite.com/path1/*` e la farm n. 2 ha un host virtuale di `www.mysite.com/path2/*`. Potete utilizzare un URL di per `/path1/invalidate.cache` eseguire il targeting della prima farm e `/path2/invalidate.cache` della seconda farm.

* **User**

   Nome utente dell’account da utilizzare per accedere alla destinazione.

* **Password**

   Password per l&#39;account da utilizzare per accedere alla destinazione.

* **Dominio NTLM**

   Dominio per l’autenticazione NTML.

* **Host NTLM**

   Host per l&#39;autenticazione NTML.

* **Abilita SSL relaxed**

   Abilitate questa opzione se desiderate che i certificati SSL autocertificati vengano accettati.

* **Consenti certificati scaduti**

   Abilitate questa opzione se desiderate che i certificati SSL scaduti vengano accettati.

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

   Il dominio NTLM proxy.

* **Host proxy NTLM**

   Il dominio NTLM proxy.

#### Esteso {#extended}

* **Interfaccia**

   Qui è possibile definire l&#39;interfaccia del socket a cui eseguire il binding.

   Imposta l&#39;indirizzo locale da utilizzare per la creazione delle connessioni. Se non è impostato, verrà utilizzato l&#39;indirizzo predefinito. Questo è utile per specificare l&#39;interfaccia da utilizzare su sistemi multihomed o cluster.

* **Metodo HTTP**

   Il metodo HTTP da utilizzare.

   Per un agente Dispatcher Flush questo è quasi sempre GET e non deve essere modificato (POST sarebbe un altro valore possibile).

* **Intestazioni HTTP**

   Questi vengono utilizzati per gli agenti Dispatcher Flush e specificano gli elementi che devono essere scaricati.

   Per un agente Dispatcher Flush le tre voci standard non devono essere modificate:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   Questi vengono utilizzati, se del caso, per indicare l’azione da utilizzare per lo scarico della maniglia o del tracciato. I sottoparametri sono dinamici:

   * `{action}` indica un&#39;azione di replica

   * `{path}` indica un percorso

   Essi sono sostituiti dal percorso/azione pertinente alla richiesta e pertanto non devono essere &quot;hardcoded&quot;:

   >[!NOTE]
   >
   >Se avete installato AEM in un contesto diverso da quello predefinito consigliato, dovrete registrare il contesto nelle intestazioni HTTP. Esempio:
   >`CQ-Handle:/<*yourContext*>{path}`

* **Chiudi connessione**

   Consente di chiudere la connessione dopo ogni richiesta.

* **Timeout connessione**

   Timeout (in millisecondi) da applicare durante il tentativo di stabilire una connessione.

* **Timeout socket**

   Timeout (in millisecondi) da applicare in attesa del traffico dopo la connessione.

* **Versione protocollo**

   Versione del protocollo; ad esempio `1.0` per HTTP/1.0.

#### Attivatori {#triggers}

Queste impostazioni vengono utilizzate per definire i trigger per la replica automatizzata:

* **Ignora predefinito**

   Se questa opzione è selezionata, l&#39;agente è escluso dalla replica predefinita; ciò significa che non sarà utilizzato se un autore di contenuto emette un&#39;azione di replica.

* **In caso di modifica**

   In questo caso, la replica di questo agente verrà attivata automaticamente quando una pagina viene modificata. Questo viene utilizzato principalmente per gli agenti Dispatcher Flush, ma anche per la replica inversa.

* **Al momento della distribuzione**

   Se questa opzione è selezionata, l&#39;agente replicherà automaticamente qualsiasi contenuto contrassegnato per la distribuzione al momento della modifica.

* **Raggiunto On/Offtime**

   Questo attiverà la replica automatica (per attivare o disattivare una pagina, come appropriato) quando si verificano gli orari o gli orari definiti per una pagina. Viene utilizzato principalmente per gli agenti Dispatcher Flush.

* **Al ricevimento**

   Se questa opzione è selezionata, l&#39;agente eseguirà la catena di replica ogni volta che riceve gli eventi di replica.

* **Nessun aggiornamento di stato**

   Se questa opzione è selezionata, l&#39;agente non forzerà l&#39;aggiornamento dello stato di replica.

* **Nessun controllo delle versioni**

   Se questa opzione è selezionata, l&#39;agente non forzerà il controllo delle versioni delle pagine attivate.

## Configurazione degli agenti di replica {#configuring-your-replication-agents}

Per informazioni sulla connessione degli agenti di replica all’istanza di pubblicazione tramite MSSL, vedere [Replica mediante SSL](/help/sites-deploying/mssl-replication.md)reciproco.

### Configurazione degli agenti di replica dall&#39;ambiente Authoring {#configuring-your-replication-agents-from-the-author-environment}

Dalla scheda Strumenti nell’ambiente di authoring è possibile configurare gli agenti di replica che risiedono nell’ambiente di authoring (**Agenti per l’autore**) o nell’ambiente di pubblicazione (**Agenti per la pubblicazione**). Le procedure seguenti illustrano la configurazione di un agente per l’ambiente di authoring, ma possono essere utilizzate per entrambi.

>[!NOTE]
>
>Quando un dispatcher gestisce le richieste HTTP per le istanze di creazione o pubblicazione, la richiesta HTTP dell’agente di replica deve includere l’intestazione PATH. Oltre alla procedura seguente, è necessario aggiungere l’intestazione PATH all’elenco del dispatcher delle intestazioni client. (Vedere [/clientheaders (intestazioni client)](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders). [](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)


1. Accedere alla scheda **Strumenti** in AEM.
1. Fare clic su **Replica** (riquadro a sinistra per aprire la cartella).
1. Fate doppio clic su **Agenti sull’autore** (nel riquadro a sinistra o a destra).
1. Fate clic sul nome agente appropriato (collegamento) per visualizzare informazioni dettagliate su tale agente.
1. Fate clic su **Modifica** per aprire la finestra di dialogo di configurazione:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. I valori forniti devono essere sufficienti per un&#39;installazione predefinita. Se si apportano modifiche, fare clic su **OK** per salvarle (vedere Agenti [replica - Parametri](#replication-agents-configuration-parameters) di configurazione per ulteriori dettagli sui singoli parametri).

>[!NOTE]
>
>Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali di trasporto all&#39;interno degli agenti di replica predefiniti.
>
>Deve essere modificato in un account utente di replica specifico per il sito con i privilegi necessari per replicare i percorsi richiesti.

### Configurazione della replica inversa {#configuring-reverse-replication}

La replica inversa viene utilizzata per riportare il contenuto generato dall’utente in un’istanza di pubblicazione a un’istanza di creazione. Questa funzione è comunemente utilizzata per funzioni quali sondaggi e moduli di registrazione.

Per motivi di sicurezza, la maggior parte delle topologie di rete non consente connessioni *dalla* &quot;Zona Demilitarizzata&quot; (una sottorete che espone i servizi esterni a una rete non affidabile come Internet).

Poiché l’ambiente di pubblicazione si trova solitamente nella rete perimetrale, per riportare il contenuto nell’ambiente di authoring è necessario avviare la connessione dall’istanza di creazione. A questo scopo:

* una *casella in uscita* nell’ambiente di pubblicazione in cui è collocato il contenuto.
* un agente (pubblicare) nell’ambiente di authoring che esegue periodicamente il polling della casella in uscita per il nuovo contenuto.

>[!NOTE]
>
>Per AEM [community](/help/communities/overview.md), la replica non viene utilizzata per il contenuto generato dall’utente in un’istanza di pubblicazione. Consultate Archiviazione [dei contenuti](/help/communities/working-with-srp.md)della community.

A tal fine, è necessario:

**Agente di replica inversa nell’ambiente** di creazione Questo agisce come componente attivo per raccogliere informazioni dalla casella in uscita nell’ambiente di pubblicazione:

Se si desidera utilizzare la replica inversa, assicurarsi che l&#39;agente sia attivato.

![chlimage_1-23](assets/chlimage_1-23.png)

**Agente di replica inversa nell&#39;ambiente di pubblicazione (una casella in uscita)** Questo è l&#39;elemento passivo in quanto agisce come una &quot;casella in uscita&quot;. L’input dell’utente viene inserito qui, da dove viene raccolto dall’agente nell’ambiente di authoring.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configurazione della replica per più istanze di pubblicazione {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Viene replicato solo il contenuto; i dati utente no (utenti, gruppi di utenti e profili utente).
>
>Per sincronizzare i dati utente tra più istanze di pubblicazione, abilitate Sincronizzazione [](/help/sites-administering/sync.md)utente.

Al momento dell&#39;installazione, un agente predefinito è già configurato per la replica del contenuto in un&#39;istanza di pubblicazione in esecuzione sulla porta 4503 dell&#39;host locale.

Per configurare la replica del contenuto per un&#39;istanza di pubblicazione aggiuntiva è necessario creare e configurare un nuovo agente di replica:

1. Aprite la scheda **Strumenti** in AEM.
1. Selezionate **Replica**, quindi **Agenti sull’autore** nel pannello a sinistra.
1. Seleziona **nuovo...**.
1. Impostare **Titolo** e **Nome**, quindi selezionare Agente **** replica.
1. Fate clic su **Crea** per creare il nuovo agente.
1. Fate doppio clic sul nuovo elemento agente per aprire il pannello di configurazione.
1. Fai clic su **Modifica** : verrà visualizzata la finestra di dialogo Impostazioni **** agente. Il tipo **di** serializzazione è già definito come Predefinito. Deve restare tale.

   * Nella scheda **Impostazioni** :

      * Attiva **abilitata**.
      * Inserire una **descrizione**.
      * Impostate **Ritardo** su `60000`.

      * Lasciate il Tipo **di** serializzazione impostato su `Default`.
   * Nella scheda **Trasporto** :

      * Immettete l’URI richiesto per la nuova istanza di pubblicazione; ad esempio,
         `https://localhost:4504/bin/receive`.

      * Immettere l&#39;account utente specifico del sito utilizzato per la replica.
      * Puoi configurare altri parametri come necessario.


1. Click **OK** to save the settings.

Potete quindi testare l’operazione aggiornando e pubblicando una pagina nell’ambiente di authoring.

Gli aggiornamenti verranno visualizzati su tutte le istanze di pubblicazione configurate come sopra.

In caso di problemi, potete controllare i registri nell’istanza di creazione. A seconda del livello di dettaglio richiesto, potete anche impostare il livello **di** registro su `Debug` mediante la finestra di dialogo Impostazioni **** agente come indicato sopra.

>[!NOTE]
>
>Questo può essere combinato con l&#39;ID [utente](#agentuserid) agente per selezionare contenuti diversi per la replica nei singoli ambienti di pubblicazione. Per ciascun ambiente di pubblicazione:
>
>1. Configurate un agente di replica per la replica in tale ambiente di pubblicazione.
>1. Configurare un account utente; con i diritti di accesso necessari per leggere il contenuto che verrà replicato in tale ambiente di pubblicazione specifico.
>1. Assegnate l&#39;account utente come ID **utente** agente per l&#39;agente di replica.

>



### Configurazione di un agente Dispatcher Flush {#configuring-a-dispatcher-flush-agent}

Gli agenti predefiniti sono inclusi nell&#39;installazione. Tuttavia, è comunque necessaria una certa configurazione e lo stesso vale per la definizione di un nuovo agente:

1. Aprite la scheda **Strumenti** in AEM.
1. Fate clic su **Distribuzione**.
1. Selezionare **Replica** , quindi **Agenti al momento della pubblicazione**.
1. Fate doppio clic sull’elemento **Dispatcher Flush** per aprire la panoramica.
1. Fate clic su **Modifica** . Viene visualizzata la finestra di dialogo Impostazioni **** agente:

   * Nella scheda **Impostazioni** :

      * Attiva **abilitata**.
      * Inserire una **descrizione**.
      * Lasciate Tipo **di** serializzazione come `Dispatcher Flush`utente o impostatelo come tale se create un nuovo agente.

      * (Facoltativo) Selezionare Aggiornamento **** alias per abilitare le richieste di annullamento convalida di alias o percorso vanità al dispatcher.
   * Nella scheda **Trasporto** :

      * Immettete l’URI richiesto per la nuova istanza di pubblicazione; ad esempio,
         `https://localhost:80/dispatcher/invalidate.cache`.

      * Immettere l&#39;account utente specifico del sito utilizzato per la replica.
      * Puoi configurare altri parametri come necessario.

   Per gli agenti Dispatcher Flush, la proprietà URI viene utilizzata solo se si utilizzano voci virtualhost basate sul percorso per distinguere tra le farm, è possibile utilizzare questo campo per eseguire il targeting della farm per annullare la validità. Ad esempio, la farm n. 1 ha un host virtuale di `www.mysite.com/path1/*` e la farm n. 2 ha un host virtuale di `www.mysite.com/path2/*`. Potete utilizzare un URL di per `/path1/invalidate.cache` eseguire il targeting della prima farm e `/path2/invalidate.cache` della seconda farm.

   >[!NOTE]
   >
   >Se avete installato AEM in un contesto diverso da quello predefinito consigliato, dovete configurare le intestazioni [](#extended) HTTP nella scheda **Estese** .

1. Fate clic su **OK** per salvare le modifiche.
1. Tornate alla scheda **Strumenti** , da qui potete **attivare** l’agente **Dispatcher Flush** (**Agenti al momento della pubblicazione**).

L&#39;agente di replica **Dispatcher Flush** non è attivo sull&#39;autore. È possibile accedere alla stessa pagina nell’ambiente di pubblicazione utilizzando l’URI equivalente; ad esempio, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Controllo dell&#39;accesso agli agenti di replica {#controlling-access-to-replication-agents}

L&#39;accesso alle pagine utilizzate per configurare gli agenti di replica può essere controllato utilizzando le autorizzazioni delle pagine utente e/o gruppo sul `etc/replication` nodo.

>[!NOTE]
>
>L’impostazione di tali autorizzazioni non influisce sugli utenti che replicano il contenuto (ad esempio, dalla console Siti Web o dall’opzione della barra laterale). Il framework di replica non utilizza la &quot;sessione utente&quot; dell&#39;utente corrente per accedere agli agenti di replica durante la replica delle pagine.

### Configurazione degli agenti di replica dal CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>La creazione di agenti di replica è supportata solo nel percorso del `/etc/replication` repository. Questa operazione è necessaria per la corretta gestione degli ACL associati. La creazione di un agente di replica in un&#39;altra posizione della struttura potrebbe causare accessi non autorizzati.

È possibile configurare diversi parametri degli agenti di replica tramite CRXDE Lite.

Se vi spostate per `/etc/replication` visualizzare i seguenti tre nodi:

* `agents.author`
* `agents.publish`
* `treeactivation`

I due `agents` contengono informazioni di configurazione sull&#39;ambiente appropriato e sono attivi solo quando l&#39;ambiente è in esecuzione. Ad esempio, `agents.publish` verrà utilizzato solo nell’ambiente di pubblicazione. La schermata seguente mostra l’agente di pubblicazione nell’ambiente di authoring, come incluso in AEM WCM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Monitoraggio degli agenti di replica {#monitoring-your-replication-agents}

Per monitorare un agente di replica:

1. Accedere alla scheda **Strumenti** in AEM.
1. Fate clic su **Replica**.
1. Fare doppio clic sul collegamento agli agenti per l&#39;ambiente appropriato (il riquadro a sinistra o a destra); ad esempio **Agenti sull’autore**.

   Nella finestra visualizzata viene visualizzata una panoramica di tutti gli agenti di replica per l’ambiente di authoring, inclusi il target e lo stato.

1. Fate clic sul nome agente appropriato (collegamento) per visualizzare informazioni dettagliate su tale agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   È possibile:

   * Verificare se l&#39;agente è abilitato.
   * Visualizzare la destinazione di qualsiasi replica.
   * Verificare se la coda di replica è attualmente attiva (abilitata).
   * Verificare se sono presenti elementi nella coda.
   * **Aggiorna** o **Cancella** per aggiornare la visualizzazione delle voci della coda; questo consente di vedere gli elementi entrare e uscire dalla coda.

   * **Visualizzare il registro** per accedere al registro di eventuali azioni dell&#39;agente di replica.
   * **Verificare la connessione** all&#39;istanza di destinazione.
   * **Se necessario, forza il tentativo** su qualsiasi elemento della coda.

   >[!CAUTION]
   >
   >Non utilizzate il collegamento &quot;Test Connection&quot; per la replica inversa in uscita in un&#39;istanza pubblicata.
   >
   >
   >Se viene eseguito un test di replica per una coda in uscita, tutti gli elementi che sono più vecchi della replica di test verranno rielaborati con ogni replica inversa.
   >
   >
   >Se tali elementi esistono già in una coda, possono essere trovati con la seguente query XPath JCR e devono essere rimossi.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replica batch {#batch-replication}

La replica batch non replica singole pagine o risorse, ma attende che venga attivata la prima soglia dei due elementi, in base all&#39;ora o alla dimensione.

Vengono quindi raggruppati tutti gli elementi di replica in un pacchetto, che viene quindi replicato come un singolo file all&#39;editore.

L&#39;editore decomprimerà tutti gli elementi, li salverà e riferirà all&#39;autore.

### Configurazione della replica batch {#configuring-batch-replication}

1. Passa a `http://serveraddress:serverport/siteadmin`
1. Premere l&#39;icona **[!UICONTROL Strumenti]** nella parte superiore dello schermo
1. Dalla barra di navigazione a sinistra, andate a **[!UICONTROL Replica - Agenti in Autore]** e fate doppio clic su Agente **** predefinito.
   * Potete inoltre contattare l&#39;agente di replica di pubblicazione predefinito accedendo direttamente a `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Premere il pulsante **[!UICONTROL Modifica]** sopra la coda di replica.
1. Nella finestra seguente, passare alla scheda **[!UICONTROL Batch]** :
   ![replica batch](assets/batchreplication.png)
1. Configurare l&#39;agente.

### Parametri {#parameters}

* `[!UICONTROL Enable Batch Mode]` - abilita o disabilita la modalità di replica batch
* `[!UICONTROL Max Wait Time]` - Tempo massimo di attesa per l&#39;avvio di una richiesta batch, in secondi. Il valore predefinito è 2 secondi.
* `[!UICONTROL Trigger Size]` - Avvia la replica batch quando questo limite di dimensioni

## Risorse aggiuntive {#additional-resources}

Per informazioni dettagliate sulla risoluzione dei problemi, vedere la pagina [Risoluzione dei problemi relativi alla replica](/help/sites-deploying/troubleshoot-rep.md) .

Per ulteriori informazioni,  Adobe dispone di una serie di articoli Knowledge Base relativi alla replica:

[https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html](https://helpx.adobe.com/experience-manager/kb/ReplicationSiblingReordering.html)[https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html](https://helpx.adobe.com/experience-manager/kb/ReplicationFailureAfterNewIP.html)[https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html](https://helpx.adobe.com/experience-manager/kb/LimitAccessToReplicationAgents.html)[https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html](https://helpx.adobe.com/experience-manager/kb/PagePermissionsNotReplicatedWithUser.html)https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html[](https://helpx.adobe.com/experience-manager/kb/HowToUseReverseReplication.html)[](https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.html)[](https://helpx.adobe.com/experience-manager/kb/ReplicationListener.html)[](https://helpx.adobe.com/experience-manager/kb/replication-stuck.html)[](https://helpx.adobe.com/experience-manager/kb/replication-privileges-missing-after-upgrade-to-cq-5-5.html)[](https://helpx.adobe.com/experience-manager/kb/CQ53UnableToCreateJobQueueDueToMaxQueues.html)[](https://helpx.adobe.com/experience-manager/kb/ACLReplication.html)[](https://helpx.adobe.com/experience-manager/kb/content-grow-due-reverse-replication.html)[](https://helpx.adobe.com/experience-manager/kb/ReplicationAgentUsingAnonUser.html)https://helpx.adobe.com/experience-manager/kb/CQ5ReplicateToSpecificAgents.htmlhttps://helpx.adobe.com/experience-manager/kb/ReplicationListener.htmlhttps://helpx.adobe.com/experience-manager/kb/replication-stuck.htmlmaiuscolo
