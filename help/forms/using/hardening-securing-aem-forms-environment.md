---
title: Indurimento e protezione dei moduli AEM in ambiente OSGi
seo-title: Indurimento e protezione dei moduli AEM in ambiente OSGi
description: Scopri le raccomandazioni e le best practice per proteggere  AEM Forms sul server OSGi.
seo-description: Scopri le raccomandazioni e le best practice per proteggere  AEM Forms sul server OSGi.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---


# Protezione e protezione dei moduli AEM nell&#39;ambiente OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Scopri le raccomandazioni e le best practice per proteggere  AEM Forms sul server OSGi.

La protezione di un ambiente server è di fondamentale importanza per un&#39;organizzazione. Questo articolo descrive raccomandazioni e procedure ottimali per la protezione dei server che eseguono  AEM Forms. Non si tratta di un documento completo per l&#39;indurimento dell&#39;host per il sistema operativo in uso. In questo articolo vengono invece descritte diverse impostazioni di protezione da implementare per migliorare la sicurezza dell’applicazione distribuita. Per garantire che i server delle applicazioni restino protetti, tuttavia, è necessario implementare anche procedure di monitoraggio della sicurezza, rilevamento e risposta oltre alle raccomandazioni fornite in questo articolo. Il documento contiene inoltre le best practice e le linee guida per la protezione dei dati personali (PII).

L&#39;articolo è destinato a consulenti, specialisti della sicurezza, architetti di sistemi e professionisti IT che sono responsabili della pianificazione delle applicazioni o dello sviluppo e della distribuzione dell&#39;infrastruttura di  AEM Forms. Tali ruoli includono i seguenti ruoli comuni:

* Tecnici IT e operativi che devono implementare applicazioni e server Web sicuri nelle proprie organizzazioni o nelle organizzazioni dei clienti.
* Architetti e progettisti che sono responsabili della pianificazione degli sforzi architettonici per i clienti nelle loro organizzazioni.
* Specialisti di sicurezza IT che si concentrano sulla fornitura di sicurezza tra le piattaforme all&#39;interno delle loro organizzazioni.
* Consulenti di  Adobe e partner che richiedono risorse dettagliate per clienti e partner.

Nell’immagine seguente sono visualizzati i componenti e i protocolli utilizzati in una tipica implementazione AEM Forms , inclusa la topologia firewall appropriata:

![architettura tipica](assets/typical-architecture.png)

 AEM Forms è altamente personalizzabile e può funzionare in diversi ambienti. Alcune delle raccomandazioni potrebbero non essere applicabili all&#39;organizzazione.

## Livello di trasporto sicuro {#secure-transport-layer}

Le vulnerabilità relative alla sicurezza dei livelli di trasporto sono tra le prime minacce a qualsiasi server applicazioni rivolto a Internet o Intranet. Questa sezione descrive il processo di indurimento degli host sulla rete rispetto a tali vulnerabilità. Si occupa della segmentazione della rete, del protocollo di controllo della trasmissione/del protocollo Internet (TCP/IP) e dell&#39;uso di firewall per la protezione dell&#39;host.

### Limite punti finali aperti {#limit-open-endpoints}

Un&#39;organizzazione può disporre di un firewall esterno per limitare l&#39;accesso tra un utente finale e  AEM Forms Publish Farm. L’organizzazione può inoltre disporre di un firewall interno per limitare l’accesso tra una farm di pubblicazione e altri elementi dell’organizzazione (ad esempio, istanza di creazione, istanza di elaborazione, database). Consentite ai firewall di consentire l’accesso a un numero limitato di  URL AEM Forms per gli utenti finali e all’interno degli elementi dell’organizzazione:

#### Configurare il firewall esterno {#configure-external-firewall}

È possibile configurare un firewall esterno per consentire l’accesso a Internet a un determinato URL di AEM Forms . Per compilare o inviare un modulo adattivo, HTML5, una lettera di gestione della corrispondenza o per accedere a un server AEM Forms  è necessario accedere a tali URL:

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
   <td>Forms Portal </td> 
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

È possibile configurare il firewall interno per consentire ad alcuni componenti AEM Forms  (ad esempio, istanza di creazione, istanza di elaborazione, database) di comunicare con la farm di pubblicazione e altri componenti interni menzionati nel diagramma della topologia:

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
   <td>Server aggiuntivo di Forms Workflow ( AEM Forms sul server JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Impostazione delle autorizzazioni dell&#39;archivio e degli elenchi di controllo degli accessi (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

Per impostazione predefinita, le risorse disponibili sui nodi di pubblicazione sono accessibili a tutti. L’accesso in sola lettura è abilitato per tutte le risorse. È necessario per abilitare l&#39;accesso anonimo. Se si prevede di limitare la visualizzazione del modulo e di inviare l&#39;accesso solo agli utenti autenticati, utilizzare un gruppo comune per consentire solo agli utenti autenticati di avere accesso in sola lettura alle risorse disponibili sui nodi di pubblicazione. Le seguenti posizioni/directory contengono risorse di moduli che richiedono protezione (accesso in sola lettura per gli utenti autenticati):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Gestione sicura dei dati dei moduli {#securely-handle-forms-data}

 AEM Forms memorizza i dati in posizioni predefinite e cartelle temporanee. Proteggere i dati per evitare un uso non autorizzato.

### Imposta pulizia periodica della cartella temporanea {#setup-periodic-cleanup-of-temporary-folder}

Quando si configurano moduli per allegati di file, si verificano o si visualizzano in anteprima componenti, i dati corrispondenti vengono memorizzati nei nodi di pubblicazione in /tmp/fd/. I dati vengono eliminati periodicamente. È possibile modificare il processo di eliminazione dei dati predefinito in modo da renderlo più aggressivo. Per modificare il processo pianificato per eliminare i dati, aprite AEM console Web, aprite  attività di pulizia memorizzazione temporanea di AEM Forms e modificate l’espressione Cron.

Negli scenari di cui sopra, i dati vengono salvati solo per gli utenti autenticati. Inoltre, i dati sono protetti con elenchi di controllo di accesso (ACL, Access Control List). Pertanto, modificare la rimozione dei dati è un passo aggiuntivo per proteggere le informazioni.

### Proteggere i dati salvati dal portale moduli azione di invio {#secure-data-saved-by-forms-portal-submit-action}

Per impostazione predefinita, l&#39;azione Invia del portale moduli dei moduli adattivi salva i dati nell&#39;archivio locale del nodo di pubblicazione. I dati vengono salvati in /content/forms/fp. **Non è consigliabile memorizzare i dati nell’istanza di pubblicazione.**

È possibile configurare il servizio di storage in modo che venga inviato via cavo al cluster di elaborazione senza salvare nulla localmente sul nodo di pubblicazione. Il cluster di elaborazione risiede in un&#39;area protetta dietro il firewall privato e i dati restano sicuri.

Utilizzare le credenziali del server di elaborazione per AEM servizio impostazioni DS per inviare dati dal nodo di pubblicazione al server di elaborazione. Si consiglia di utilizzare le credenziali di un utente non amministrativo con restrizioni con accesso in lettura/scrittura all&#39;archivio del server di elaborazione. Per ulteriori informazioni, vedere [Configurazione dei servizi di archiviazione per bozze e invii](/help/forms/using/configuring-draft-submission-storage.md).

### Proteggere i dati gestiti dal modello dati del modulo (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilizzare gli account utente con privilegi minimi richiesti per configurare le origini dati per il modello dati del modulo (FDM). L&#39;utilizzo di account amministrativi può fornire l&#39;accesso aperto di entità di metadati e schema a utenti non autorizzati.\
L&#39;integrazione dei dati fornisce anche metodi per autorizzare le richieste di servizi FDM. È possibile inserire meccanismi di autorizzazione pre e post-esecuzione per convalidare una richiesta. Le richieste di servizio vengono generate durante la precompilazione di un modulo, l&#39;invio di un modulo e la chiamata di servizi tramite una regola.

**Autorizzazione pre-elaborazione:** è possibile utilizzare l&#39;autorizzazione pre-elaborazione per convalidare l&#39;autenticità di una richiesta prima di eseguirla. Potete utilizzare gli input, il servizio e i dettagli della richiesta per consentire o interrompere l&#39;esecuzione della richiesta. È possibile restituire un&#39;eccezione di integrazione dei dati OPERATION_ACCESS_DENIED se l&#39;esecuzione viene arrestata. Potete inoltre modificare la richiesta del client prima di inviarla per l&#39;esecuzione. Ad esempio, modifica dell’input e aggiunta di informazioni aggiuntive.

**Autorizzazione post-elaborazione:** è possibile utilizzare l&#39;autorizzazione post-processo per convalidare e controllare i risultati prima di restituire i risultati al richiedente. Potete anche filtrare, eseguire la potatura e inserire dati aggiuntivi per i risultati.

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
   * Un utente di fdm-authors può creare e modificare un modello dati del modulo.
   * Un utente di cm-user-agent Group può creare, visualizzare in anteprima e pubblicare lettere di gestione della corrispondenza.
   * Un utente di un gruppo di editor di workflow può creare un’applicazione inbox e un modello di workflow.


**Durante l&#39;elaborazione dell&#39;autore:**

* Per i casi di utilizzo di salvataggio e invio remoti, create un utente con autorizzazioni di lettura, creazione e modifica del percorso contenuto/modulo/fp dell&#39;archivio crx.
* Aggiungete l’utente al gruppo Workflow-utente per consentire a un utente di utilizzare AEM applicazioni inbox.

## Proteggere gli elementi Intranet di un ambiente AEM Forms  {#secure-intranet-elements-of-an-aem-forms-environment}

In generale, i cluster di elaborazione e il componente aggiuntivo di Forms Workflow ( AEM Forms su JEE) vengono eseguiti dietro un firewall. Questi sono considerati sicuri. È comunque possibile eseguire alcuni passaggi per rendere più rigidi questi ambienti:

### Cluster di elaborazione protetta {#secure-processing-cluster}

Un cluster di elaborazione viene eseguito in modalità di creazione ma non viene utilizzato per attività di sviluppo. Non consentire l&#39;inclusione di un utente normale nei gruppi di autori e utenti di moduli di un cluster di elaborazione.

### Utilizza AEM best practice per proteggere un ambiente AEM Forms  {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Questo documento fornisce istruzioni specifiche per  ambiente AEM Forms. È necessario assicurarsi che l&#39;installazione AEM sottostante sia sicura quando viene distribuita. Per istruzioni dettagliate, consultare la documentazione relativa alla [AEM lista di controllo della sicurezza](/help/sites-administering/security-checklist.md).
