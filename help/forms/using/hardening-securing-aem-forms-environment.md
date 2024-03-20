---
title: Protezione e protezione dei moduli AEM nell’ambiente OSGi
description: Scopri consigli e best practice per proteggere AEM Forms sul server OSGi.
topic-tags: Security
role: Admin
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Protezione e protezione dei moduli AEM nell’ambiente OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Scopri consigli e best practice per proteggere AEM Forms sul server OSGi.

La protezione di un ambiente server è di fondamentale importanza per un&#39;organizzazione. Questo articolo descrive consigli e best practice per la protezione dei server che eseguono AEM Forms. Non si tratta di un documento completo di protezione avanzata dell&#39;host per il sistema operativo. In questo articolo vengono invece descritte varie impostazioni di protezione avanzata che è necessario implementare per migliorare la protezione dell&#39;applicazione distribuita. Per garantire la protezione degli application server, è tuttavia necessario implementare anche procedure di monitoraggio, rilevamento e risposta di protezione, oltre alle raccomandazioni fornite in questo articolo. Il documento contiene anche best practice e linee guida per la protezione dei dati PII (personalmente identificabili).

L&#39;articolo è destinato a consulenti, specialisti della sicurezza, architetti di sistemi e professionisti IT responsabili della pianificazione dello sviluppo di applicazioni o infrastrutture e della distribuzione di AEM Forms. Questi ruoli includono i seguenti ruoli comuni:

* Ingegneri IT e operativi che devono implementare applicazioni web e server sicuri all&#39;interno delle proprie organizzazioni o di quelle dei clienti.
* Architetti e pianificatori responsabili della pianificazione degli sforzi architettonici per i clienti nelle loro organizzazioni.
* Esperti di sicurezza IT che si concentrano sulla fornitura di sicurezza attraverso le piattaforme all&#39;interno delle loro organizzazioni.
* Consulenti di Adobi e partner che richiedono risorse dettagliate per clienti e partner.

Nell’immagine seguente sono illustrati i componenti e i protocolli utilizzati in una tipica distribuzione AEM Forms, inclusa la topologia del firewall appropriata:

![architettura tipica](assets/typical-architecture.png)

AEM Forms è altamente personalizzabile e può funzionare in molti ambienti diversi. Alcuni consigli potrebbero non essere applicabili alla tua organizzazione.

## Livello di trasporto sicuro {#secure-transport-layer}

Le vulnerabilità relative alla sicurezza del livello di trasporto sono tra le prime minacce per qualsiasi server applicazioni che si affaccia su Internet o su Intranet. Questa sezione descrive il processo di protezione degli host della rete da queste vulnerabilità. Affronta la segmentazione della rete, l&#39;irrigidimento dello stack TCP/IP (Transmission Control Protocol/Internet Protocol) e l&#39;uso di firewall per la protezione dell&#39;host.

### Limita endpoint aperti  {#limit-open-endpoints}

Un’organizzazione può disporre di un firewall esterno per limitare l’accesso tra un utente finale e una farm di pubblicazione di AEM Forms. L’organizzazione può anche disporre di un firewall interno per limitare l’accesso tra una farm di pubblicazione e altri elementi all’interno dell’organizzazione (ad esempio, istanza di authoring, istanza di elaborazione, database). Consenti ai firewall di consentire l’accesso a un numero limitato di URL di AEM Forms per gli utenti finali e all’interno di elementi delle organizzazioni:

#### Configurare il firewall esterno  {#configure-external-firewall}

Puoi configurare un firewall esterno per consentire a un determinato URL di AEM Forms di accedere a Internet. L’accesso a questi URL è necessario per compilare o inviare un modulo adattivo, HTML5, una lettera di gestione della corrispondenza o per accedere a un server AEM Forms:

<table> 
 <tbody>
  <tr>
   <td>Componente</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Moduli adattivi</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Moduli HTML5</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Gestione della corrispondenza </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Forms Portal </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> App AEM Forms</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### Configurare il firewall interno  {#configure-internal-firewall}

Puoi configurare il firewall interno in modo che alcuni componenti di AEM Forms (ad esempio, istanza di authoring, istanza di elaborazione, database) possano comunicare con la farm di pubblicazione e altri componenti interni menzionati nel diagramma della topologia:

<table> 
 <tbody>
  <tr>
   <td>Host<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Farm di pubblicazione (nodi di pubblicazione)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Server di elaborazione</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Server del componente aggiuntivo Forms Workflow (AEM Forms sul server JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configurare le autorizzazioni dell’archivio e gli elenchi di controllo di accesso (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

Per impostazione predefinita, le risorse disponibili sui nodi di pubblicazione sono accessibili a tutti. L’accesso in sola lettura è abilitato per tutte le risorse. È necessario per abilitare l’accesso anonimo. Se prevedi di limitare l’accesso alla visualizzazione modulo e all’invio solo agli utenti autenticati, utilizza un gruppo comune per consentire solo agli utenti autenticati di avere accesso in sola lettura alle risorse disponibili sui nodi di pubblicazione. Le seguenti posizioni/directory contengono risorse di Forms che richiedono protezione avanzata (accesso in sola lettura per gli utenti autenticati):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Gestione sicura dei dati dei moduli  {#securely-handle-forms-data}

AEM Forms memorizza i dati in posizioni predefinite e cartelle temporanee. È necessario proteggere i dati per evitare un utilizzo non autorizzato.

### Imposta la pulizia periodica della cartella temporanea {#setup-periodic-cleanup-of-temporary-folder}

Quando configuri i moduli per gli allegati, i componenti di verifica o anteprima, i dati corrispondenti vengono memorizzati nei nodi di pubblicazione in /tmp/fd/. I dati vengono eliminati periodicamente. Puoi modificare il processo di eliminazione dei dati predefinito in modo che risulti più aggressivo. Per modificare il processo pianificato per l’eliminazione dei dati, apri la console web AEM, apri l’attività di pulizia della memoria temporanea di AEM Forms e modifica l’espressione Cron.

Negli scenari sopra indicati, i dati vengono salvati solo per gli utenti autenticati. Inoltre, i dati sono protetti da elenchi di controllo di accesso (ACL, Access Control List). Pertanto, la modifica dell’eliminazione dei dati rappresenta un ulteriore passo avanti per la protezione delle informazioni.

### Protezione dei dati salvati dall&#39;azione di invio del portale dei moduli {#secure-data-saved-by-forms-portal-submit-action}

Per impostazione predefinita, l’azione di invio Forms Portal dei moduli adattivi salva i dati nell’archivio locale del nodo di pubblicazione. I dati vengono salvati in /content/forms/fp. **Si sconsiglia di memorizzare i dati nell’istanza di pubblicazione.**

È possibile configurare il servizio di archiviazione per l&#39;invio al cluster di elaborazione senza salvare nulla localmente sul nodo di pubblicazione. Il cluster di elaborazione risiede in una zona protetta dietro il firewall privato e i dati rimangono sicuri.

Utilizzare le credenziali del server di elaborazione per il servizio delle impostazioni di Servizi di dominio AEM per inviare i dati dal nodo di pubblicazione al server di elaborazione. Utilizzare le credenziali di un utente non amministrativo con accesso in lettura/scrittura all&#39;archivio del server di elaborazione. Per ulteriori informazioni, consulta [Configurazione dei servizi di archiviazione per le bozze e gli invii](/help/forms/using/configuring-draft-submission-storage.md).

### Protezione dei dati gestita dal modello dati modulo (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilizza account utente con i privilegi minimi richiesti per configurare le origini dati per il modello dati modulo (FDM). L’utilizzo di un account amministrativo può fornire l’accesso aperto a entità di metadati e schemi a utenti non autorizzati.\
L’integrazione dei dati fornisce anche metodi per autorizzare le richieste di servizio FDM. Puoi inserire meccanismi di autorizzazione pre e post-esecuzione per convalidare una richiesta. Le richieste di servizio vengono generate durante la precompilazione di un modulo, l’invio di un modulo e la chiamata di servizi tramite una regola.

**Autorizzazione pre-elaborazione:** Puoi utilizzare l’autorizzazione pre-elaborazione per convalidare l’autenticità di una richiesta prima di eseguirla. Puoi utilizzare input, servizi e dettagli della richiesta per consentire o interrompere l’esecuzione della richiesta. È possibile restituire un&#39;eccezione di integrazione dei dati OPERATION_ACCESS_DENIED se l&#39;esecuzione viene interrotta. Puoi anche modificare la richiesta del client prima di inviarla per l’esecuzione. Ad esempio, modificando l’input e aggiungendo ulteriori informazioni.

**Autorizzazione post-elaborazione:** È possibile utilizzare l&#39;autorizzazione post-elaborazione per convalidare e controllare i risultati prima di restituirli al richiedente. Puoi anche filtrare, eliminare e inserire dati aggiuntivi nei risultati.

### Limita l’accesso degli utenti {#limit-user-access}

Per le istanze di authoring, pubblicazione ed elaborazione è necessario un set diverso di utenti tipo. Non eseguire alcuna istanza con credenziali di amministratore.

**In un’istanza di pubblicazione:**

* Solo gli utenti del gruppo utenti moduli possono visualizzare in anteprima, creare bozze e inviare moduli.
* Solo gli utenti del gruppo cm-user-agent possono visualizzare in anteprima le lettere di gestione della corrispondenza.
* Disattiva tutti gli accessi anonimi non essenziali.

**In un’istanza Autore:**

* Esistono diversi gruppi predefiniti con privilegi specifici per ogni utente tipo. Assegna utenti al gruppo.

   * Un utente del gruppo utenti di forms:

      * può creare, compilare, pubblicare e inviare un modulo.
      * non può creare un modulo adattivo basato su XDP.
      * non dispongono delle autorizzazioni necessarie per scrivere script per i moduli adattivi.
      * impossibile importare XDP o un pacchetto contenente XDP

   * Un utente di forms-power-user group crea, compila, pubblica e invia tutti i tipi di moduli, scrive script per i moduli adattivi e importa pacchetti contenenti XDP.
   * Un utente di template-author e template-power-user può visualizzare in anteprima e creare un modello.
   * Un utente di autori di moduli fdm può creare e modificare un modello di dati modulo.
   * Un utente del gruppo cm-user-agent può creare, visualizzare in anteprima e pubblicare lettere di gestione della corrispondenza.
   * Un utente del gruppo di editor dei flussi di lavoro può creare un&#39;applicazione casella in entrata e un modello di flusso di lavoro.

**Durante l’elaborazione dell’autore:**

* Per i casi di utilizzo di salvataggio e invio remoti, crea un utente con autorizzazioni di lettura, creazione e modifica per il percorso di contenuto/modulo/fp dell’archivio crx.
* Aggiungere un utente al gruppo di utenti del flusso di lavoro per consentire a un utente di utilizzare le applicazioni della casella in entrata AEM.

## Proteggere gli elementi intranet di un ambiente AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

In generale, i cluster di elaborazione e il componente aggiuntivo Forms Workflow (AEM Forms su JEE) vengono eseguiti dietro un firewall. Quindi, questi sono considerati sicuri. Puoi comunque eseguire alcuni passaggi per irrigidire questi ambienti:

### Cluster di elaborazione protetto {#secure-processing-cluster}

Un cluster di elaborazione viene eseguito in modalità di creazione ma non viene utilizzato per attività di sviluppo. Non consentire a un utente normale di essere incluso nei gruppi di autori di contenuti e utenti di moduli di un cluster di elaborazione.

### Utilizzare le best practice per l’AEM per proteggere un ambiente AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Questo documento fornisce istruzioni specifiche per l’ambiente AEM Forms. Al momento dell’implementazione, assicurati che l’installazione AEM sottostante sia sicura. Per istruzioni dettagliate, consulta [Elenco di controllo della sicurezza AEM](/help/sites-administering/security-checklist.md) documentazione.
