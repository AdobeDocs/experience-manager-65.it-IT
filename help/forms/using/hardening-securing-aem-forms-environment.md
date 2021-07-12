---
title: Hardening e protezione dei moduli AEM in ambiente OSGi
seo-title: Hardening e protezione dei moduli AEM in ambiente OSGi
description: Scopri i consigli e le best practice per proteggere AEM Forms sul server OSGi.
seo-description: Scopri i consigli e le best practice per proteggere AEM Forms sul server OSGi.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: Admin
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---

# Hardening e protezione dei moduli AEM in ambiente OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Scopri i consigli e le best practice per proteggere AEM Forms sul server OSGi.

La protezione di un ambiente server è di fondamentale importanza per un&#39;organizzazione. Questo articolo descrive raccomandazioni e best practice per la protezione dei server che eseguono AEM Forms. Non si tratta di un documento completo per l&#39;indurimento degli host per il sistema operativo in uso. Questo articolo descrive invece diverse impostazioni di protezione che devi implementare per migliorare la sicurezza dell’applicazione distribuita. Per garantire la sicurezza dei server applicazioni, tuttavia, è necessario implementare anche le procedure di monitoraggio, rilevamento e risposta di sicurezza oltre alle raccomandazioni fornite in questo articolo. Il documento contiene inoltre best practice e linee guida per la protezione dei dati personali (Personally Identifiable Information).

L&#39;articolo è destinato a consulenti, esperti di sicurezza, architetti di sistemi e professionisti IT responsabili della pianificazione delle applicazioni o dello sviluppo e della distribuzione delle infrastrutture AEM Forms. Questi ruoli includono i seguenti ruoli comuni:

* Tecnici IT e operativi che devono implementare applicazioni e server web sicuri nelle proprie organizzazioni o clienti.
* Architetti e progettisti responsabili della pianificazione degli sforzi architettonici per i clienti nelle loro organizzazioni.
* Specialisti in sicurezza IT che si concentrano sulla sicurezza delle piattaforme all&#39;interno delle loro organizzazioni.
* Consulenti di Adobi e partner che richiedono risorse dettagliate per clienti e partner.

L’immagine seguente mostra i componenti e i protocolli utilizzati in una tipica implementazione AEM Forms, inclusa la topologia firewall appropriata:

![architettura tipica](assets/typical-architecture.png)

AEM Forms è altamente personalizzabile e può funzionare in molti ambienti diversi. Alcuni dei consigli potrebbero non essere applicabili all’organizzazione.

## Livello di trasporto sicuro {#secure-transport-layer}

Le vulnerabilità relative alla sicurezza dei livelli di trasporto sono una delle prime minacce per qualsiasi server applicativo rivolto a Internet o Intranet. Questa sezione descrive il processo di indurimento degli host sulla rete rispetto a queste vulnerabilità. Si occupa della segmentazione della rete, dell&#39;indurimento dello stack del protocollo di controllo della trasmissione/protocollo Internet (TCP/IP) e dell&#39;uso di firewall per la protezione dell&#39;host.

### Limitare gli endpoint aperti  {#limit-open-endpoints}

Un&#39;organizzazione può disporre di un firewall esterno per limitare l&#39;accesso tra un utente finale e AEM Forms Publish Farm. L’organizzazione può inoltre disporre di un firewall interno per limitare l’accesso tra una farm di pubblicazione e altri elementi dell’organizzazione (ad esempio, istanza di authoring, istanza di elaborazione, database). Consenti ai firewall di abilitare l’accesso a un numero limitato di URL AEM Forms per gli utenti finali e all’interno degli elementi dell’organizzazione:

#### Configurare un firewall esterno  {#configure-external-firewall}

È possibile configurare un firewall esterno per consentire a un determinato URL di AEM Forms di accedere a Internet. L’accesso a questi URL è necessario per compilare o inviare un modulo adattivo, un HTML5, una lettera di gestione della corrispondenza o per accedere a un server AEM Forms:

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
     <li>/content/forms/formset/profiles/</li> 
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
   <td>Portale Forms </td> 
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

#### Configurare un firewall interno  {#configure-internal-firewall}

Puoi configurare il firewall interno per consentire ad alcuni componenti di AEM Forms (ad esempio, istanza di authoring, istanza di elaborazione, database) di comunicare con la farm di pubblicazione e altri componenti interni menzionati nel diagramma della topologia:

<table> 
 <tbody>
  <tr>
   <td>Host<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Publish Farm (nodi di pubblicazione)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Server di elaborazione</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Server aggiuntivo di Forms Workflow (AEM Forms sul server JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Impostazione delle autorizzazioni dell&#39;archivio e degli elenchi di controllo degli accessi (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

Per impostazione predefinita, le risorse disponibili sui nodi di pubblicazione sono accessibili a tutti. L’accesso in sola lettura è abilitato per tutte le risorse. È necessario per abilitare l&#39;accesso anonimo. Se si prevede di limitare la visualizzazione del modulo e di inviare l’accesso solo agli utenti autenticati, utilizzare un gruppo comune per consentire solo agli utenti autenticati l’accesso in sola lettura alle risorse disponibili sui nodi di pubblicazione. Le posizioni/directory seguenti contengono risorse dei moduli che richiedono protezione (accesso in sola lettura per gli utenti autenticati):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Gestione sicura dei dati dei moduli  {#securely-handle-forms-data}

AEM Forms memorizza i dati in posizioni predefinite e cartelle temporanee. È necessario proteggere i dati per evitare un uso non autorizzato.

### Imposta la pulizia periodica della cartella temporanea {#setup-periodic-cleanup-of-temporary-folder}

Quando si configurano i moduli per allegati di file, si verificano o si visualizzano in anteprima i componenti, i dati corrispondenti vengono memorizzati sui nodi di pubblicazione in /tmp/fd/. I dati vengono eliminati periodicamente. È possibile modificare il processo di eliminazione dei dati predefinito in modo che sia più aggressivo. Per modificare il processo pianificato per eliminare i dati, aprire AEM console Web, aprire l&#39;attività di pulizia di archiviazione temporanea di AEM Forms e modificare l&#39;espressione Cron.

Negli scenari di cui sopra, i dati vengono salvati solo per gli utenti autenticati. Inoltre, i dati sono protetti con elenchi di controllo accessi (ACL). Quindi, modificare l&#39;eliminazione dei dati è un ulteriore passo per proteggere le informazioni.

### Azione di invio dei dati protetti salvati dal portale moduli {#secure-data-saved-by-forms-portal-submit-action}

Per impostazione predefinita, l’azione Invia portale moduli dei moduli adattivi salva i dati nell’archivio locale del nodo di pubblicazione. I dati vengono salvati in /content/forms/fp. **Si sconsiglia di archiviare i dati nell’istanza di pubblicazione.**

È possibile configurare il servizio di archiviazione in modo che invii il materiale al cluster di elaborazione senza salvare nulla localmente sul nodo di pubblicazione. Il cluster di elaborazione risiede in un&#39;area protetta dietro il firewall privato e i dati rimangono sicuri.

Utilizzare le credenziali del server di elaborazione per AEM servizio impostazioni DS per inviare i dati dal nodo di pubblicazione al server di elaborazione. Si consiglia di utilizzare le credenziali di un utente non amministrativo con restrizioni con accesso in lettura e scrittura all&#39;archivio del server di elaborazione. Per ulteriori informazioni, consulta [Configurazione dei servizi di archiviazione per bozze e invii](/help/forms/using/configuring-draft-submission-storage.md).

### Protezione dei dati gestita dal modello dati del modulo (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilizzare gli account utente con privilegi minimi richiesti per configurare le origini dati per il modello dati del modulo (FDM). L&#39;utilizzo di account amministrativo può fornire accesso aperto di metadati ed entità dello schema a utenti non autorizzati.\
L’integrazione dei dati fornisce anche metodi per autorizzare le richieste di servizi FDM. Puoi inserire meccanismi di autorizzazione pre e post-esecuzione per convalidare una richiesta. Le richieste di servizio vengono generate durante la precompilazione di un modulo, l’invio di un modulo e la chiamata di servizi tramite una regola.

**Autorizzazione preliminare:** puoi utilizzare l’autorizzazione preliminare per convalidare l’autenticità di una richiesta prima di eseguirla. Puoi utilizzare input, servizi e dettagli della richiesta per consentire o interrompere l’esecuzione della richiesta. È possibile restituire un&#39;eccezione di integrazione dei dati OPERATION_ACCESS_DENIED se l&#39;esecuzione viene interrotta. Puoi anche modificare la richiesta del client prima di inviarla per l’esecuzione. Ad esempio, modifica dell’input e aggiunta di informazioni aggiuntive.

**Autorizzazione post-elaborazione:** è possibile utilizzare l&#39;autorizzazione post-elaborazione per convalidare e controllare i risultati prima di restituire i risultati al richiedente. È inoltre possibile filtrare, perfezionare e inserire dati aggiuntivi ai risultati.

### Limitare l&#39;accesso degli utenti {#limit-user-access}

Per le istanze di authoring, pubblicazione ed elaborazione sono necessari diversi set di utenti tipo . Non eseguire alcuna istanza con le credenziali di amministratore.

**In un&#39;istanza di pubblicazione:**

* Solo gli utenti del gruppo utenti dei moduli possono visualizzare in anteprima, creare bozze e inviare moduli.
* Solo gli utenti del gruppo di agenti cm-user-agent possono visualizzare in anteprima le lettere di gestione della corrispondenza.
* Disabilita tutti gli accessi anonimi non essenziali.

**Su un&#39;istanza dell&#39;autore:**

* Esiste un diverso set di gruppi predefiniti con privilegi specifici per ogni utente tipo. Assegna utenti al gruppo.

   * Utente di un gruppo di utenti di forms:

      * può creare, compilare, pubblicare e inviare un modulo.
      * impossibile creare un modulo adattivo basato su XDP.
      * non dispongono delle autorizzazioni necessarie per scrivere script per i moduli adattivi.
      * impossibile importare XDP o qualsiasi pacchetto contenente XDP
   * Utente di gruppi di utenti di forms-power: creazione, compilazione, pubblicazione e invio di tutti i tipi di moduli, scrittura di script per i moduli adattivi, importazione di pacchetti contenenti XDP.
   * Un utente di autori di modelli e di modelli-power-user può visualizzare in anteprima e creare un modello.
   * Un utente di fdm-authors può creare e modificare un modello di dati modulo.
   * Un utente di cm-user-agent gruppo può creare, visualizzare in anteprima e pubblicare lettere di gestione della corrispondenza.
   * Un utente del gruppo editor-workflow può creare un&#39;applicazione inbox e un modello di workflow.


**Al momento dell’elaborazione dell’autore:**

* Per i casi d’uso di salvataggio e invio in remoto, crea un utente con autorizzazioni di lettura, creazione e modifica sul percorso di contenuto/modulo/fp dell’archivio crx.
* Aggiungi l’utente al gruppo di utenti del flusso di lavoro per consentire a un utente di utilizzare AEM applicazioni della casella in entrata.

## Proteggere gli elementi Intranet di un ambiente AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

In generale, i cluster di elaborazione e il componente aggiuntivo di Forms Workflow (AEM Forms su JEE) vengono eseguiti dietro un firewall. Quindi, questi sono considerati sicuri. È comunque possibile eseguire alcuni passaggi per rendere più rigorosi questi ambienti:

### Cluster di elaborazione protetto {#secure-processing-cluster}

Un cluster di elaborazione viene eseguito in modalità di authoring ma non viene utilizzato per le attività di sviluppo. Non consentire l’inclusione di un utente normale nei gruppi di autori di contenuti e utenti di moduli di un cluster di elaborazione.

### Utilizzare AEM best practice per proteggere un ambiente AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Questo documento fornisce istruzioni specifiche per l’ambiente AEM Forms. Assicurati che l&#39;installazione AEM sottostante sia sicura quando distribuita. Per istruzioni dettagliate, consulta la documentazione [AEM Lista di controllo protezione](/help/sites-administering/security-checklist.md) .
