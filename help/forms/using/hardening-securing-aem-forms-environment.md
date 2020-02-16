---
title: Protezione e protezione dei moduli AEM in ambiente OSGi
seo-title: Protezione e protezione dei moduli AEM in ambiente OSGi
description: Scopri le raccomandazioni e le best practice per proteggere AEM Forms dal server OSGi.
seo-description: Scopri le raccomandazioni e le best practice per proteggere AEM Forms dal server OSGi.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Protezione e protezione dei moduli AEM in ambiente OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Scopri le raccomandazioni e le best practice per proteggere AEM Forms dal server OSGi.

La protezione di un ambiente server è di fondamentale importanza per un&#39;organizzazione. Questo articolo descrive raccomandazioni e procedure ottimali per la protezione dei server che eseguono AEM Forms. Non si tratta di un documento completo per l&#39;indurimento dell&#39;host per il sistema operativo in uso. In questo articolo vengono invece descritte diverse impostazioni di protezione da implementare per migliorare la sicurezza dell’applicazione distribuita. Per garantire la sicurezza dei server applicazioni, tuttavia, è necessario implementare anche procedure di monitoraggio, rilevamento e risposta di sicurezza, oltre alle raccomandazioni fornite in questo articolo. Il documento contiene inoltre le best practice e le linee guida per la protezione dei dati personali (PII).

L&#39;articolo è destinato a consulenti, specialisti in sicurezza, architetti di sistemi e professionisti IT responsabili della pianificazione dell&#39;applicazione o dello sviluppo dell&#39;infrastruttura e dell&#39;implementazione di AEM Forms. Tali ruoli includono i seguenti ruoli comuni:

* Tecnici IT e operativi che devono implementare applicazioni e server Web sicuri nelle proprie organizzazioni o nelle organizzazioni dei clienti.
* Architetti e progettisti che sono responsabili della pianificazione degli sforzi architettonici per i clienti nelle loro organizzazioni.
* Specialisti di sicurezza IT che si concentrano sulla fornitura di sicurezza tra le piattaforme all&#39;interno delle loro organizzazioni.
* Consulenti di Adobe e partner che richiedono risorse dettagliate per clienti e partner.

L&#39;immagine seguente mostra i componenti e i protocolli utilizzati in una tipica implementazione di AEM Forms, inclusa la topologia firewall appropriata:

![architettura tipica](assets/typical-architecture.png)

AEM Forms è altamente personalizzabile e può funzionare in molti ambienti diversi. Alcune delle raccomandazioni potrebbero non essere applicabili all&#39;organizzazione.

## Secure Transport Layer {#secure-transport-layer}

Le vulnerabilità relative alla sicurezza dei livelli di trasporto sono tra le prime minacce a qualsiasi server applicazioni rivolto a Internet o Intranet. Questa sezione descrive il processo di indurimento degli host sulla rete rispetto a tali vulnerabilità. Si occupa della segmentazione della rete, del protocollo di controllo della trasmissione/del protocollo Internet (TCP/IP) e dell&#39;uso di firewall per la protezione dell&#39;host.

### Limite endpoint aperti {#limit-open-endpoints}

Un&#39;organizzazione può disporre di un firewall esterno per limitare l&#39;accesso tra un utente finale e un&#39;farm di pubblicazione AEM Forms. L’organizzazione può inoltre disporre di un firewall interno per limitare l’accesso tra una farm di pubblicazione e altri elementi dell’organizzazione (ad esempio, istanza di creazione, istanza di elaborazione, database). Consentire l’accesso a un numero limitato di URL di moduli AEM per gli utenti finali e all’interno degli elementi dell’organizzazione:

#### Configurare il firewall esterno {#configure-external-firewall}

È possibile configurare un firewall esterno per consentire l&#39;accesso a Internet a determinati URL di AEM Forms. Per compilare o inviare un modulo adattivo, HTML5, una lettera di gestione della corrispondenza o per accedere a un server AEM Forms è necessario accedere a tali URL:

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
     <li>/content/forms/formsets/profile/</li> 
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
   <td>Portale Moduli </td> 
   <td>
    <ul> 
     <li>/content/forms/portale/</li> 
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

#### Configurare il firewall interno {#configure-internal-firewall}

Puoi configurare il firewall interno per consentire ad alcuni componenti di AEM Forms (ad esempio, istanza di creazione, istanza di elaborazione, database) di comunicare con la farm di pubblicazione e altri componenti interni menzionati nel diagramma della topologia:

<table> 
 <tbody>
  <tr>
   <td>Host<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Pubblica farm (nodi di pubblicazione)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Server di elaborazione</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Server del componente aggiuntivo Flusso di lavoro moduli (AEM Forms sul server JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Impostazione delle autorizzazioni dell&#39;archivio e degli elenchi di controllo degli accessi (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

Per impostazione predefinita, le risorse disponibili sui nodi di pubblicazione sono accessibili a tutti. L’accesso in sola lettura è abilitato per tutte le risorse. È necessario per abilitare l&#39;accesso anonimo. Se si prevede di limitare la visualizzazione del modulo e di inviare l&#39;accesso solo agli utenti autenticati, utilizzare un gruppo comune per consentire solo agli utenti autenticati di accedere in sola lettura alle risorse disponibili sui nodi di pubblicazione. Le seguenti posizioni/directory contengono risorse di moduli che richiedono protezione (accesso in sola lettura per gli utenti autenticati):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Gestione sicura dei dati dei moduli {#securely-handle-forms-data}

In AEM Forms i dati vengono memorizzati in posizioni e cartelle temporanee predefinite. Proteggere i dati per evitare un uso non autorizzato.

### Imposta pulizia periodica della cartella temporanea {#setup-periodic-cleanup-of-temporary-folder}

Quando si configurano moduli per allegati di file, si verificano o si visualizzano in anteprima componenti, i dati corrispondenti vengono memorizzati nei nodi di pubblicazione in /tmp/fd/. I dati vengono eliminati periodicamente. È possibile modificare il processo di eliminazione dei dati predefinito in modo da renderlo più aggressivo. Per modificare il processo pianificato per eliminare i dati, aprite la console Web AEM, aprite l’attività di pulizia temporanea dell’archiviazione AEM Forms e modificate l’espressione Cron.

Negli scenari di cui sopra, i dati vengono salvati solo per gli utenti autenticati. Inoltre, i dati sono protetti con elenchi di controllo di accesso (ACL, Access Control List). Pertanto, modificare la rimozione dei dati è un passo aggiuntivo per proteggere le informazioni.

### Protezione dei dati salvati tramite l&#39;azione di invio del portale moduli {#secure-data-saved-by-forms-portal-submit-action}

Per impostazione predefinita, l&#39;azione Invia del portale moduli dei moduli adattivi salva i dati nell&#39;archivio locale del nodo di pubblicazione. I dati vengono salvati in /content/forms/fp. **Non è consigliabile memorizzare i dati nell’istanza di pubblicazione.**

È possibile configurare il servizio di storage in modo che venga inviato via cavo al cluster di elaborazione senza salvare nulla localmente sul nodo di pubblicazione. Il cluster di elaborazione risiede in un&#39;area protetta dietro il firewall privato e i dati restano sicuri.

Utilizzate le credenziali del server di elaborazione per il servizio delle impostazioni di AEM DS per inviare i dati dal nodo di pubblicazione al server di elaborazione. Si consiglia di utilizzare le credenziali di un utente non amministrativo con restrizioni con accesso in lettura/scrittura all&#39;archivio del server di elaborazione. Per ulteriori informazioni, consultate [Configurazione dei servizi di archiviazione per bozze e invii](/help/forms/using/configuring-draft-submission-storage.md).

### Proteggere i dati gestiti dal modello dati del modulo (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilizzare account utente con privilegi minimi richiesti per configurare le origini dati per il modello dati del modulo (FDM). L&#39;utilizzo di account amministrativi può fornire l&#39;accesso aperto di entità di metadati e schema a utenti non autorizzati.\
L&#39;integrazione dei dati fornisce anche metodi per autorizzare le richieste di servizi FDM. È possibile inserire meccanismi di autorizzazione pre e post-esecuzione per convalidare una richiesta. Le richieste di servizio vengono generate durante la precompilazione di un modulo, l&#39;invio di un modulo e la chiamata di servizi tramite una regola.

**** Autorizzazione pre-elaborazione: Potete utilizzare l&#39;autorizzazione pre-elaborazione per convalidare l&#39;autenticità di una richiesta prima di eseguirla. Potete utilizzare gli input, il servizio e i dettagli della richiesta per consentire o interrompere l&#39;esecuzione della richiesta. È possibile restituire un&#39;eccezione di integrazione dei dati OPERATION_ACCESS_DENIED se l&#39;esecuzione viene arrestata. Potete inoltre modificare la richiesta del client prima di inviarla per l&#39;esecuzione. Ad esempio, modifica dell’input e aggiunta di informazioni aggiuntive.

**** Autorizzazione post-elaborazione: Potete utilizzare l&#39;autorizzazione post-processo per convalidare e controllare i risultati prima di restituire i risultati al richiedente. Potete anche filtrare, eseguire la potatura e inserire dati aggiuntivi per i risultati.

### Limite accesso utente {#limit-user-access}

Per le istanze di creazione, pubblicazione ed elaborazione sono necessari diversi set di utenti. Non eseguite alcuna istanza con le credenziali di amministratore.

**In un’istanza di pubblicazione:**

* Solo gli utenti del gruppo di utenti di moduli possono visualizzare l&#39;anteprima, creare le bozze e inviare i moduli.
* Solo gli utenti di cm-user-agent Group possono visualizzare in anteprima le lettere di gestione della corrispondenza.
* Disattiva tutti gli accessi anonimi non essenziali.

**In un’istanza di creazione:**

* Esistono diversi gruppi predefiniti con privilegi specifici per ogni persona. Assegnare gli utenti al gruppo.

   * Un utente di un gruppo di utenti form:

      * può creare, compilare, pubblicare e inviare un modulo.
      * impossibile creare un modulo adattivo basato su XDP.
      * non dispongono delle autorizzazioni per scrivere script per i moduli adattivi.
      * impossibile importare XDP o qualsiasi pacchetto contenente XDP
   * Un utente di un gruppo di utenti che utilizza moduli può creare, compilare, pubblicare e inviare tutti i tipi di moduli, scrivere script per i moduli adattivi, importare pacchetti contenenti XDP.
   * Un utente di autori di modelli e un utente che può usare modelli può visualizzare l’anteprima e creare un modello.
   * Un utente di autori di moduli può creare e modificare un modello dati del modulo.
   * Un utente di cm-user-agent Group può creare, visualizzare in anteprima e pubblicare lettere di gestione della corrispondenza.
   * Un utente di un gruppo di editor di workflow può creare un’applicazione inbox e un modello di workflow.


**Durante l&#39;elaborazione dell&#39;autore:**

* Per i casi di utilizzo di salvataggio e invio remoti, create un utente con autorizzazioni di lettura, creazione e modifica del percorso contenuto/modulo/fp dell&#39;archivio crx.
* Aggiungi utente a gruppo workflow-utenti per consentire a un utente di utilizzare le applicazioni inbox AEM.

## Proteggere gli elementi Intranet in un ambiente AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

In generale, il componente aggiuntivo Elaborazione di cluster e Flusso di lavoro moduli (AEM Forms on JEE) viene eseguito dietro un firewall. Questi sono considerati sicuri. È comunque possibile eseguire alcuni passaggi per rendere più rigidi questi ambienti:

### Cluster di elaborazione protetta {#secure-processing-cluster}

Un cluster di elaborazione viene eseguito in modalità di creazione ma non viene utilizzato per attività di sviluppo. Non consentire l&#39;inclusione di un utente normale nei gruppi di autori e utenti di moduli di un cluster di elaborazione.

### Best practice di AEM per proteggere un ambiente AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Questo documento fornisce istruzioni specifiche per l&#39;ambiente AEM Forms. Devi accertarti che l’installazione sottostante di AEM sia sicura quando viene distribuita. Per istruzioni dettagliate, consultate la documentazione sull&#39;elenco di controllo [AEM Security](/help/sites-administering/security-checklist.md) .
