---
title: Pianificazione dell'aggiornamento
seo-title: Planning Your Upgrade
description: Questo articolo aiuta a stabilire obiettivi chiari, fasi e risultati finali durante la pianificazione dell'aggiornamento AEM.
seo-description: This article helps establish clear goals, phases and deliverables when planning the AEM upgrade.
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
feature: Upgrading
exl-id: 0dea2b3e-fd7c-4811-a04a-6852ffc1e6d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 0%

---

# Pianificazione dell&#39;aggiornamento{#planning-your-upgrade}

## Panoramica del progetto AEM {#aem-project-overview}

AEM viene spesso utilizzato in implementazioni ad alto impatto che potrebbero servire milioni di utenti. Nella maggior parte dei casi, ci sono applicazioni personalizzate che vengono distribuite sulle istanze, che aggiungono alla complessità. Qualsiasi sforzo per aggiornare tale implementazione deve essere gestito in modo metodico.

Questa guida aiuta a stabilire obiettivi chiari, fasi e risultati finali durante la pianificazione dell&#39;aggiornamento. Si concentra sull&#39;esecuzione complessiva del progetto e sulle linee guida. Offre una panoramica dei passaggi effettivi dell’aggiornamento, ma si riferisce alle risorse tecniche disponibili, se del caso. Esso deve essere utilizzato congiuntamente alle risorse tecniche disponibili di cui al documento.

Il processo di aggiornamento AEM deve essere gestito con cura le fasi di pianificazione, analisi ed esecuzione con i principali risultati finali definiti per ogni fase.

È possibile effettuare l’aggiornamento direttamente dalle versioni 6.0 e 6.5 di AEM. I clienti che eseguono 5.6.x e versioni precedenti devono prima eseguire l’aggiornamento alla versione 6.0 o successiva, con la raccomandazione 6.0(SP3). Inoltre, il nuovo formato OAK Segment Tar viene ora utilizzato per il Segment Node Store a partire dalla versione 6.3 e la migrazione dell&#39;archivio a questo nuovo formato è obbligatoria anche per le versioni 6.0, 6.1 e 6.2.

>[!CAUTION]
>
>Se esegui l’aggiornamento da AEM 6.2 a 6.3, effettua l’aggiornamento dalle versioni (**6.2-SP1-CFP1 - -6.2SP1-CFP12.1**) o **6.2SP1-CFP15** a partire da . In caso contrario, se esegui l’aggiornamento da **6.2SP1-CFP13/6.2SP1CFP14** a AEM 6.3, devi anche effettuare l&#39;aggiornamento ad almeno la versione **6.3.2.2**. In caso contrario, dopo l’aggiornamento AEM Sites avrebbe avuto esito negativo.

## Ambito e requisiti dell&#39;aggiornamento {#upgrade-scope-requirements}

Di seguito è riportato un elenco delle aree interessate da un tipico progetto di aggiornamento AEM:

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Impatto</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>Effetti incerti ma sottili</td>
   <td>Al momento dell'aggiornamento AEM, potrebbe essere il momento di aggiornare anche il sistema operativo e questo potrebbe avere un certo impatto.</td>
  </tr>
  <tr>
   <td>Java Runtime</td>
   <td>Impatto moderato</td>
   <td>AEM 6.3 richiede JRE 1.7.x (64 bit) o versione successiva. JRE 1.8 è l’unica versione attualmente supportata da Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Impatto moderato</td>
   <td>Pulizia revisioni online richiede gratuitamente<br /> spazio su disco pari al 25% delle dimensioni dell'archivio e al 15% dello spazio libero heap<br /> per il completamento. Potrebbe essere necessario aggiornare l'hardware a<br /> garantire risorse sufficienti per il cleanup delle revisioni online<br /> esegui. Inoltre, se si esegue l’aggiornamento da una versione precedente a AEM 6, è possibile<br /> possono essere requisiti di storage aggiuntivi.</td>
  </tr>
  <tr>
   <td>Archivio dei contenuti (CRX o Oak)</td>
   <td>Impatto elevato</td>
   <td>A partire dalla versione 6.1, AEM non supporta CRX2, quindi una migrazione a<br /> Oak (CRX3) è necessario se si esegue l'aggiornamento da una versione precedente. AEM 6.3<br /> implementato un nuovo archivio dei nodi di segmento che richiede anche una migrazione. La<br /> lo strumento crx2oak è utilizzato a questo scopo.</td>
  </tr>
  <tr>
   <td>Componenti/contenuti AEM</td>
   <td>Impatto moderato</td>
   <td><code>/libs</code> e <code>/apps</code> sono facilmente gestite tramite l'aggiornamento, ma <code>/etc</code> di solito richiede una riapplicazione manuale delle personalizzazioni.</td>
  </tr>
  <tr>
   <td>Servizi AEM</td>
   <td>Basso impatto</td>
   <td>La maggior parte dei servizi di base AEM viene testata per l’aggiornamento. Questa è un'area a basso impatto.</td>
  </tr>
  <tr>
   <td>Servizi applicativi personalizzati</td>
   <td>Impatto basso-alto</td>
   <td>A seconda dell'applicazione e della personalizzazione, potrebbe essere<br /> dipendenze da JVM, versioni del sistema operativo e alcune relative all'indicizzazione<br /> cambia, in quanto gli indici non vengono generati automaticamente in Oak.</td>
  </tr>
  <tr>
   <td>Contenuto applicazione personalizzato</td>
   <td>Impatto basso-alto</td>
   <td>È possibile eseguire il backup dei contenuti che non verranno gestiti tramite l’aggiornamento<br /> prima che l’aggiornamento abbia luogo e quindi spostato nuovamente nell’archivio.<br /> La maggior parte dei contenuti può essere gestita tramite lo strumento di migrazione.</td>
  </tr>
 </tbody>
</table>

È importante assicurarsi di eseguire un sistema operativo supportato, Java Runtime, httpd e la versione di Dispatcher. Per ulteriori informazioni, consulta la sezione [Pagina Requisiti tecnici di AEM 6.5](/help/sites-deploying/technical-requirements.md). L’aggiornamento di questi componenti dovrà essere preso in considerazione nel piano di progetto e avvenire prima dell’aggiornamento AEM.

## Fasi del progetto {#project-phases}

Un sacco di lavoro va nella pianificazione ed esecuzione di un aggiornamento AEM. Al fine di chiarire i diversi sforzi intrapresi in questo processo, abbiamo suddiviso gli esercizi di pianificazione ed esecuzione in fasi separate. Nelle sezioni seguenti, ogni fase determina un risultato finale che viene spesso sfruttato da una fase futura del progetto.

### Pianificazione della formazione sull’autore {#planning-for-author-training}

Con qualsiasi nuova versione, potrebbero essere introdotte modifiche all’interfaccia utente e ai flussi di lavoro degli utenti. Inoltre, le nuove versioni introducono nuove funzionalità che potrebbero risultare vantaggiose per l’azienda per l’utilizzo. Consigliamo di rivedere le modifiche funzionali introdotte e di organizzare un piano per addestrare gli utenti a sfruttarle in modo efficace.

![unu_cropped](assets/unu_cropped.png)

Le nuove funzioni di AEM 6.5 si trovano in [la sezione AEM di adobe.com](/help/release-notes/release-notes.md). Assicurati di notare eventuali modifiche alle interfacce utente o alle funzionalità dei prodotti comunemente utilizzate nella tua organizzazione. Osservando le nuove funzioni, prendi anche nota di tutte le funzioni che possono essere di valore per la tua organizzazione. Dopo aver esaminato le modifiche apportate alla AEM 6.5, sviluppa un piano di formazione per i tuoi autori. Ciò potrebbe comportare l&#39;utilizzo di risorse disponibili liberamente, come i video delle funzioni helpx o la formazione formale offerta tramite [Adobe Digital Learning Services](https://www.adobe.com/training.html).

### Creazione di un piano di test {#creating-a-test-plan}

L&#39;implementazione di AEM da parte di ogni cliente è unica ed è stata personalizzata per soddisfare le proprie esigenze aziendali. Di conseguenza, è importante determinare tutte le personalizzazioni apportate al sistema in modo che possano essere incluse in un piano di test. Questo piano di test alimenterà il processo di controllo qualità eseguito sull&#39;istanza aggiornata.

![piano di prova](assets/test-plan.png)

L&#39;ambiente di produzione deve essere duplicato e il test deve essere eseguito dopo l&#39;aggiornamento per assicurarsi che tutte le applicazioni e il codice personalizzato vengano eseguiti come desiderato. È necessario ripristinare tutte le personalizzazioni ed eseguire test di prestazioni, carico e sicurezza. Quando organizzi il tuo piano di test, assicurati di includere tutte le personalizzazioni che sono state apportate al sistema, oltre alle UI e ai flussi di lavoro preconfigurati che vengono utilizzati nelle operazioni quotidiane. Questi possono includere servizi e servlet OSGI personalizzati, integrazioni a Adobe Marketing Cloud, integrazioni con terze parti tramite connettori AEM, integrazioni personalizzate di terze parti, componenti e modelli personalizzati, sovrapposizioni personalizzate dell’interfaccia utente in AEM e flussi di lavoro personalizzati. Per i clienti che eseguono la migrazione da una versione precedente alla AEM 6, eventuali query personalizzate devono essere analizzate in quanto potrebbero dover essere indicizzate. Per i clienti che dispongono già di una versione 6.x di AEM, queste query devono ancora essere testate per garantire che i loro indici continuino a funzionare efficacemente dopo l’aggiornamento.

### Determinazione dei cambiamenti di architettura e di infrastruttura necessari {#determining-architectural-and-infrastructure-changes-needed}

Durante l&#39;aggiornamento, potrebbe essere necessario aggiornare anche altri componenti nello stack tecnico, come il sistema operativo o JVM. Inoltre, è possibile che a causa di modifiche nel trucco del repository possa essere necessario hardware aggiuntivo. Questo di solito si verifica solo per i clienti che eseguono la migrazione da istanze precedenti alla 6.x, ma è importante tenerne conto. Infine, potrebbero essere necessarie modifiche alle procedure operative, inclusi i processi di monitoraggio, manutenzione e backup e disaster recovery.

![doi_ritagliato](assets/doi_cropped.png)

Esamina i requisiti tecnici per AEM 6.5 e assicurati che l&#39;hardware e il software correnti siano sufficienti. Per potenziali modifiche ai processi operativi, consulta i seguenti documenti:

**Monitoraggio e manutenzione:**

[Dashboard operazioni](/help/sites-administering/operations-dashboard.md)

[Best practice per il monitoraggio in Assets](/help/assets/assets-monitoring-best-practices.md)

[Risorse del server di monitoraggio tramite la console JMX](/help/sites-administering/jmx-console.md)

[Pulizia revisioni](/help/sites-deploying/revision-cleanup.md)

**Backup/ripristino e disaster recovery:**

[Backup e ripristino](/help/sites-administering/backup-and-restore.md)

[Prestazioni e scalabilità](/help/sites-deploying/performance.md)

[Come eseguire AEM con lo standby a freddo TarMK](/help/sites-deploying/tarmk-cold-standby.md)

#### Considerazioni sulla ristrutturazione dei contenuti {#content-restructuring-considerations}

AEM introdotto modifiche alla struttura dell&#39;archivio che contribuiranno a rendere gli aggiornamenti più diretti. Le modifiche comportano lo spostamento del contenuto dalla cartella /etc a cartelle quali /libs, /apps e /content, in base al fatto che il contenuto sia di proprietà di un Adobe o di un cliente, limitando così le possibilità di sovrascrivere il contenuto durante le versioni. La ristrutturazione dell’archivio è stata effettuata in modo tale da non richiedere modifiche al codice al momento dell’aggiornamento 6.5, anche se è consigliabile rivedere i dettagli in [Ristrutturazione dell’archivio in AEM](/help/sites-deploying/repository-restructuring.md) durante la pianificazione di un aggiornamento.

### Valutazione della complessità dell&#39;aggiornamento {#assessing-upgrade-complexity}

A causa dell’ampia varietà di personalizzazioni che i nostri clienti applicano ai loro ambienti di AEM, è importante dedicare un po’ di tempo prima di determinare il livello generale di impegno che dovrebbe essere previsto nell’aggiornamento.

Esistono due approcci possibili per valutare la complessità dell’aggiornamento: una fase preliminare può semplicemente utilizzare il rilevatore pattern introdotto di recente, che può essere eseguito sulle istanze 6.1, 6.2 e 6.3 di AEM. Il rilevatore di pattern è il modo più semplice per valutare la complessità complessiva dell’aggiornamento da attendersi utilizzando i pattern riportati. Il rapporto del rilevatore di pattern include pattern per identificare le API non disponibili utilizzate dalla codebase personalizzata (questa operazione è stata eseguita utilizzando i controlli di compatibilità precedenti all’aggiornamento nella versione 6.3).

Dopo la valutazione iniziale, un passo successivo più completo potrebbe essere quello di eseguire un aggiornamento su un&#39;istanza di prova ed eseguire alcune prove di fumo di base. Adobe fornisce anche alcuni . Inoltre, l&#39;elenco di [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) deve essere rivisto non solo per la versione a cui stai eseguendo l’aggiornamento, ma anche per tutte le versioni tra la versione sorgente e quella di destinazione. Ad esempio, se esegui l’aggiornamento da AEM 6.2 a 6.5, è importante rivedere le funzioni obsolete e rimosse di AEM 6.3 oltre a quelle di AEM 6.5.

![trei_cropped](assets/trei_cropped.png)

Il rilevatore pattern introdotto di recente dovrebbe fornire una stima abbastanza precisa di cosa aspettarsi durante un aggiornamento per la maggior parte dei casi. Tuttavia, per personalizzazioni e implementazioni più complesse in cui si verificano modifiche incompatibili, è possibile aggiornare un’istanza di sviluppo a AEM 6.5 in base alle istruzioni in [Esecuzione di un aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md). Una volta completato, eseguire alcuni test di fumo ad alto livello su questo ambiente. L&#39;obiettivo di questo esercizio non è completare in modo esaustivo l&#39;inventario dei casi di test e produrre un inventario formale dei difetti, ma fornirci una stima approssimativa della quantità di lavoro che sarà necessario per aggiornare il codice per la compatibilità 6.5. Se combinato con [Rilevamento pattern](/help/sites-deploying/pattern-detector.md) e le modifiche dell&#39;architettura determinate nella sezione precedente, è possibile fornire una stima approssimativa al team di gestione del progetto per la pianificazione dell&#39;aggiornamento.

### Creazione del Runbook di aggiornamento e ripristino {#building-the-upgrade-and-rollback-runbook}

Sebbene Adobe abbia documentato il processo di aggiornamento di un&#39;istanza AEM, il layout di rete, l&#39;architettura di distribuzione e le personalizzazioni di ciascun cliente richiedono una regolazione precisa e un&#39;impostazione personalizzata di questo approccio. Per questo motivo, ti invitiamo a rivedere tutta la documentazione fornita e a utilizzarla per informare un runbook specifico per il progetto che delinea le specifiche procedure di aggiornamento e ripristino che seguirai nel tuo ambiente. Se esegui l’aggiornamento da CRX2, assicurati di valutare quanto tempo impiegherà la migrazione dei contenuti quando passi da CRX2 a Oak. Per i grandi archivi, potrebbe essere sostanziale.

![diagramma di runbook](assets/runbook-diagram.png)

Abbiamo fornito procedure di aggiornamento e ripristino in [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md) nonché istruzioni dettagliate per l&#39;applicazione dell&#39;aggiornamento in Esecuzione di un [Aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md). Queste istruzioni devono essere riviste e prese in considerazione con l&#39;architettura del sistema, le personalizzazioni e la tolleranza al downtime per determinare le procedure appropriate di switch-over e rollback che verranno eseguite durante l&#39;aggiornamento. Eventuali modifiche all&#39;architettura o alle dimensioni del server devono essere incluse nella redazione del proprio runbook personalizzato. E&#39; importante notare che questo dovrebbe essere trattato come una prima bozza. Quando il team completa i propri cicli di QA e di sviluppo e distribuisce l’aggiornamento all’ambiente di staging, potrebbe essere necessaria una serie di passaggi aggiuntivi. Idealmente, questo documento dovrebbe contenere informazioni sufficienti affinché, se consegnato a un membro del personale operativo, possa completare l&#39;aggiornamento completamente dalle informazioni contenute all&#39;interno.

### Sviluppo di un piano di progetto {#developing-a-project-plan}

Possiamo utilizzare l&#39;output degli esercizi precedenti per creare un piano di progetto che copra i tempi previsti per i test o le attività di sviluppo, la formazione e l&#39;esecuzione effettiva dell&#39;aggiornamento.

![piano di sviluppo](assets/develop-project-plan.png)

Un piano globale di progetto dovrebbe comprendere:

* Completamento dei piani di sviluppo e di collaudo
* Aggiornamento di ambienti di sviluppo e controllo qualità
* Aggiornamento della base di codice personalizzata per AEM 6.5
* Un test di controllo qualità e un ciclo di correzione
* Aggiornamento dell’ambiente di staging
* Integrazione, prestazioni e test del carico
* Certificazione ambientale
* Viva

### Esecuzione di attività di sviluppo e controllo qualità {#performing-development-and-qa}

Abbiamo fornito procedure per [Aggiornamento di codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) per essere compatibile con AEM 6.5. Poiché questo processo iterativo viene eseguito, le modifiche al runbook devono essere apportate secondo necessità. Vedi anche [Compatibilità con le versioni precedenti in AEM 6.5](/help/sites-deploying/backward-compatibility.md) informazioni su come le personalizzazioni possono rimanere compatibili con le versioni precedenti nella maggior parte dei casi senza richiedere lo sviluppo subito dopo l’aggiornamento.

![patru_cropped](assets/patru_cropped.png)

Il processo di sviluppo e test di solito è iterativo. A causa delle personalizzazioni, le modifiche apportate durante l’aggiornamento potrebbero rendere potenzialmente inutilizzabile un’intera sezione del prodotto. Una volta che gli sviluppatori hanno affrontato la causa principale del problema e il team di test ha accesso per testare queste funzionalità, è possibile individuare ulteriori problemi. Poiché vengono rilevati problemi che richiedono adeguamenti del processo di aggiornamento, assicurati di aggiungerli al runbook di aggiornamento personalizzato. Dopo diverse iterazioni di test e correzione, la base di codice deve essere completamente convalidata e pronta per la distribuzione nell&#39;ambiente di staging.

### Test finale {#final-testing}

Consigliamo un ciclo finale di test dopo che la base di codice è stata certificata dal team QA della tua organizzazione. Questo ciclo di test richiederà la convalida del runbook in un ambiente di staging seguito da turni di accettazione, prestazioni e test di sicurezza degli utenti.

![cinci_ritagliato](assets/cinci_cropped.png)

Questo passaggio è fondamentale in quanto è l&#39;unico momento in cui si è in grado di convalidare i passaggi nel runbook rispetto a un ambiente simile alla produzione. Una volta aggiornato l’ambiente, è importante concedere agli utenti finali un certo tempo di accesso ed esecuzione delle attività che svolgono quando utilizzano il sistema nelle loro attività quotidiane. Non è raro che gli utenti utilizzino una parte del sistema che non era stata considerata in precedenza. Trovare e correggere i problemi in queste aree prima del go-live può aiutare a prevenire costose interruzioni di produzione. Poiché una nuova versione di AEM contiene modifiche significative alla piattaforma sottostante, è importante anche eseguire test di prestazioni, carico e sicurezza sul sistema come se lo stessimo avviando per la prima volta.

### Esecuzione dell&#39;aggiornamento {#performing-the-upgrade}

Una volta che tutte le parti interessate avranno ricevuto il discarico finale, è il momento di eseguire le procedure del runbook definite. Sono stati forniti passaggi per l&#39;aggiornamento e il ripristino [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md) e i passaggi di installazione in Esecuzione di un [Aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md) come punto di riferimento.

![upgrade](assets/perform-upgrade.png)

Abbiamo fornito alcuni passaggi nelle istruzioni di aggiornamento per la convalida dell’ambiente. Questi includono controlli di base come la scansione dei registri di aggiornamento e la verifica che tutti i bundle OSGi siano stati avviati correttamente, ma si consiglia anche la convalida con i tuoi casi di test basati sui tuoi processi aziendali. Si consiglia inoltre di controllare la pianificazione di AEM Pulizia revisioni online e le relative routine per garantire che si verifichino durante un periodo di inattività per la tua azienda. Queste routine sono essenziali per le prestazioni a lungo termine di AEM.
