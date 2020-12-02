---
title: Pianificazione dell'aggiornamento
seo-title: Pianificazione dell'aggiornamento
description: Questo articolo aiuta a stabilire obiettivi chiari, fasi e risultati finali durante la pianificazione dell'aggiornamento AEM.
seo-description: Questo articolo aiuta a stabilire obiettivi chiari, fasi e risultati finali durante la pianificazione dell'aggiornamento AEM.
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149
workflow-type: tm+mt
source-wordcount: '2447'
ht-degree: 0%

---


# Pianificazione dell&#39;aggiornamento{#planning-your-upgrade}

## Panoramica AEM progetto {#aem-project-overview}

AEM viene spesso utilizzato nelle distribuzioni ad alto impatto che potrebbero servire a milioni di utenti. Nella maggior parte dei casi, esistono applicazioni personalizzate che vengono distribuite sulle istanze, e che aumentano la complessità. Qualsiasi sforzo per aggiornare tale implementazione deve essere gestito in modo metodico.

Questa guida aiuta a stabilire obiettivi chiari, fasi e risultati finali durante la pianificazione dell&#39;aggiornamento. Esso si concentra sull&#39;esecuzione e sugli orientamenti generali del progetto. Fornisce una panoramica dei passaggi effettivi dell&#39;aggiornamento, ma si riferisce alle risorse tecniche disponibili laddove appropriato. Esso dovrebbe essere utilizzato unitamente alle risorse tecniche disponibili di cui al documento.

Il processo di aggiornamento AEM necessita di una gestione accurata delle fasi di pianificazione, analisi ed esecuzione con i risultati finali chiave definiti per ciascuna fase.

È possibile effettuare l&#39;aggiornamento direttamente dalle AEM versioni 6.0 e 6.5. I clienti che eseguono 5.6.x e versioni precedenti devono eseguire l&#39;aggiornamento prima alla versione 6.0 o successiva, con la raccomandazione 6.0(SP3). Inoltre, il nuovo formato OAK Segment Tar è ora utilizzato per il Segment Node Store a partire dalla versione 6.3, e la migrazione del repository a questo nuovo formato è obbligatoria anche per le versioni 6.0, 6.1 e 6.2.

>[!CAUTION]
>
>Se si sta effettuando l&#39;aggiornamento da AEM 6.2 a 6.3, è necessario eseguire l&#39;aggiornamento dalle versioni (**6.2-SP1-CFP1 - -6.2SP1-CFP12.1**) oppure a partire da **6.2SP1-CFP15**. In caso contrario, se si sta effettuando l&#39;aggiornamento da **6.2SP1-CFP13/6.2SP1CFP14** a AEM 6.3, è inoltre necessario eseguire l&#39;aggiornamento ad almeno la versione **6.3.2.2**. In caso contrario,  AEM Sites avrebbe avuto esito negativo dopo l&#39;aggiornamento.

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
   <td>Al momento dell'aggiornamento AEM, potrebbe essere il momento di aggiornare anche il sistema operativo e questo potrebbe avere un impatto.</td>
  </tr>
  <tr>
   <td>Java Runtime</td>
   <td>Impatto moderato</td>
   <td>AEM 6.3 richiede JRE 1.7.x (64 bit) o versione successiva. JRE 1.8 è l'unica versione attualmente supportata da  Oracle.</td>
  </tr>
  <tr>
   <td>Hardware</td>
   <td>Impatto moderato</td>
   <td>Per completare la pulizia online delle revisioni è necessario spazio libero su disco pari al 25% delle dimensioni dell'archivio e al 15% dello spazio libero dell'heap<br />. <br /> Potrebbe essere necessario aggiornare l'hardware per <br /> garantire risorse sufficienti per l'esecuzione della pulizia delle revisioni online fino a <br />. Inoltre, se si esegue l'aggiornamento da una versione precedente alla AEM 6, è possibile che vi siano <br /> requisiti di storage aggiuntivi.</td>
  </tr>
  <tr>
   <td>Repository dei contenuti (CRX o Oak)</td>
   <td>Impatto elevato</td>
   <td>A partire dalla versione 6.1, AEM non supporta CRX2, pertanto è necessaria una migrazione a <br /> Oak (CRX3) se si esegue l'aggiornamento da una versione precedente. AEM 6.3 ha implementato <br /> un nuovo archivio dei nodi dei segmenti che richiede anche una migrazione. Lo strumento <br /> crx2oak è utilizzato a questo scopo.</td>
  </tr>
  <tr>
   <td>Componenti AEM/Contenuto</td>
   <td>Impatto moderato</td>
   <td><code>/libs</code> e <code>/apps</code> sono facilmente gestibili attraverso l'aggiornamento, ma <code>/etc</code> in genere richiede una riapplicazione manuale delle personalizzazioni.</td>
  </tr>
  <tr>
   <td>Servizi AEM</td>
   <td>Basso impatto</td>
   <td>La maggior parte AEM servizi di base sono testati per l'aggiornamento. Questa è un'area di basso impatto.</td>
  </tr>
  <tr>
   <td>Servizi applicazione personalizzati</td>
   <td>Impatto basso-alto</td>
   <td>A seconda dell'applicazione e della personalizzazione, potrebbero esserci dipendenze<br /> da JVM, versioni del sistema operativo e alcune modifiche relative all'indicizzazione<br />, in quanto gli indici non vengono generati automaticamente in Oak.</td>
  </tr>
  <tr>
   <td>Contenuto applicazione personalizzato</td>
   <td>Impatto basso-alto</td>
   <td>I contenuti che non saranno gestiti tramite l'aggiornamento possono essere sottoposti a backup<br /> prima che l'aggiornamento abbia luogo e quindi spostati nuovamente nella directory archivio.<br /> La maggior parte dei contenuti può essere gestita tramite lo strumento di migrazione.</td>
  </tr>
 </tbody>
</table>

È importante verificare che sia in esecuzione un sistema operativo supportato, runtime Java, versione httpd e Dispatcher. Per ulteriori informazioni, vedere la pagina [AEM 6.5 Technical Requirements](/help/sites-deploying/technical-requirements.md). L&#39;aggiornamento di questi componenti dovrà essere incluso nel piano di progetto e dovrebbe avvenire prima dell&#39;aggiornamento AEM.

## Fasi del progetto {#project-phases}

Un sacco di lavoro si occupa di pianificazione ed esecuzione di un AEM aggiornamento. Al fine di chiarire i diversi sforzi intrapresi in questo processo, abbiamo suddiviso gli esercizi di pianificazione ed esecuzione in fasi separate. Nelle sezioni seguenti, ogni fase produce un risultato finale che viene spesso sfruttato da una fase futura del progetto.

### Pianificazione per la formazione sull&#39;autore {#planning-for-author-training}

Con qualsiasi nuova versione, potrebbero essere introdotte modifiche all’interfaccia utente e ai flussi di lavoro degli utenti. Inoltre, le nuove versioni introducono nuove funzioni che potrebbero essere utili per l&#39;azienda per sfruttare. Consigliamo di rivedere le modifiche funzionali introdotte e di organizzare un piano per formare i vostri utenti a sfruttarle efficacemente.

![unu_ritagliato](assets/unu_cropped.png)

Le nuove funzioni di AEM 6.5 si trovano nella sezione [AEM di adobe.com](/help/release-notes/release-notes.md). Assicuratevi di notare eventuali modifiche alle interfacce utente o alle funzionalità dei prodotti comunemente utilizzate nella vostra organizzazione. Osservando le nuove funzioni, prendete nota anche di tutte le funzioni che possono essere di valore per la vostra organizzazione. Dopo aver esaminato le modifiche apportate alla AEM 6.5, sviluppate un piano di formazione per gli autori. Ciò potrebbe comportare l&#39;utilizzo di risorse liberamente disponibili come i video delle funzioni di helpx o la formazione formale offerta tramite [ Adobe Digital Learning Services](https://www.adobe.com/training.html).

### Creazione di un piano di test {#creating-a-test-plan}

L&#39;implementazione di AEM da parte di ogni cliente è unica ed è stata personalizzata per soddisfare le proprie esigenze aziendali. Di conseguenza, è importante determinare tutte le personalizzazioni che sono state effettuate al sistema in modo che possano essere incluse in un piano di test. Questo piano di test alimenterà il processo di QA che eseguiamo sull&#39;istanza aggiornata.

![piano di prova](assets/test-plan.png)

L&#39;ambiente di produzione deve essere duplicato e il test deve essere eseguito dopo l&#39;aggiornamento per essere certi che tutte le applicazioni e il codice personalizzato vengano eseguiti come desiderato. Devi ripristinare tutte le tue personalizzazioni ed eseguire test di prestazioni, carico e sicurezza. Quando organizzate il piano di test, accertatevi di coprire tutte le personalizzazioni effettuate al sistema, oltre alle interfacce utente e ai flussi di lavoro out-of-box che vengono utilizzati nelle operazioni quotidiane. Questi possono includere servizi e servlet OSGI personalizzati, integrazioni per Adobe Marketing Cloud, integrazioni con terze parti tramite connettori AEM, integrazioni di terze parti personalizzate, componenti e modelli personalizzati, sovrapposizioni di interfaccia utente personalizzate in AEM e flussi di lavoro personalizzati. Per i clienti che eseguono la migrazione da una versione precedente alla AEM 6, eventuali query personalizzate devono essere analizzate in quanto potrebbero dover essere indicizzate. Per i clienti che dispongono già di una versione AEM 6.x, queste query devono essere ancora testate per garantire che i loro indici continuino a funzionare efficacemente dopo l&#39;aggiornamento.

### Determinazione dei cambiamenti di architettura e infrastruttura necessari {#determining-architectural-and-infrastructure-changes-needed}

Durante l&#39;aggiornamento, è possibile che sia necessario aggiornare anche altri componenti nello stack tecnico, come il sistema operativo o JVM. Inoltre, è possibile che a causa delle modifiche nella struttura del repository sia necessario hardware aggiuntivo. In genere questo problema si verifica solo per i clienti che eseguono la migrazione da istanze precedenti alla 6.x, ma è importante tenerne conto. Infine, potrebbero essere necessarie modifiche alle procedure operative, inclusi i processi di monitoraggio, manutenzione, backup e disaster recovery.

![doi_ritagliato](assets/doi_cropped.png)

Esaminate i requisiti tecnici per AEM 6.5 e assicuratevi che l&#39;hardware e il software attuali siano sufficienti. Per le potenziali modifiche ai processi operativi, consulta i documenti seguenti:

**Monitoraggio e manutenzione:**

[Dashboard operazioni](/help/sites-administering/operations-dashboard.md)

[Tecniche consigliate per il monitoraggio delle risorse](/help/assets/assets-monitoring-best-practices.md)

[Risorse di Monitoring Server tramite la console JMX](/help/sites-administering/jmx-console.md)

[Pulizia revisioni](/help/sites-deploying/revision-cleanup.md)

**Backup/ripristino e disaster recovery:**

[Backup e ripristino](/help/sites-administering/backup-and-restore.md)

[Prestazioni e scalabilità](/help/sites-deploying/performance.md)

[Come eseguire AEM con TarMK Cold Standby](/help/sites-deploying/tarmk-cold-standby.md)

#### Considerazioni sulla ristrutturazione dei contenuti {#content-restructuring-considerations}

AEM ha introdotto modifiche alla struttura del repository che aiuteranno a rendere gli aggiornamenti più semplici. Le modifiche comportano lo spostamento del contenuto dalla cartella /etc a cartelle quali /libs, /apps e /content, a seconda che  Adobe o un cliente sia proprietario del contenuto, limitando così le possibilità di sovrascrivere il contenuto durante le release. La ristrutturazione dell&#39;archivio è stata effettuata in modo tale da non richiedere modifiche di codice al momento dell&#39;aggiornamento 6.5, anche se si consiglia di rivedere i dettagli in [Ristrutturazione dell&#39;archivio in AEM](/help/sites-deploying/repository-restructuring.md) durante la pianificazione di un aggiornamento.

### Valutazione della complessità dell&#39;aggiornamento {#assessing-upgrade-complexity}

A causa dell&#39;ampia varietà di personalizzazioni che i nostri clienti applicano ai loro ambienti AEM, è importante dedicare un po&#39; di tempo per determinare il livello generale di impegno che ci si dovrebbe aspettare nell&#39;aggiornamento.

Per valutare la complessità dell&#39;aggiornamento è possibile adottare due approcci: una fase preliminare può semplicemente utilizzare il nuovo Rilevatore di pattern, disponibile per l&#39;esecuzione sulle istanze AEM 6.1, 6.2 e 6.3. Il rilevatore di pattern è il modo più semplice per valutare la complessità complessiva dell&#39;aggiornamento da attendersi utilizzando i pattern riportati. Il rapporto del rilevatore di pattern include pattern per identificare le API non disponibili utilizzate dalla base di codice personalizzata (ciò è stato fatto utilizzando i controlli di compatibilità pre-aggiornamento in 6.3).

Dopo la valutazione iniziale, un passo successivo più completo potrebbe essere quello di eseguire un aggiornamento su un&#39;istanza di prova ed eseguire alcune prove di fumo di base.  Adobe fornisce anche alcuni . Inoltre, l&#39;elenco di [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) deve essere rivisto non solo per la versione in cui si sta effettuando l&#39;aggiornamento, ma anche per qualsiasi versione tra le versioni di origine e di destinazione. Ad esempio, se si esegue l&#39;aggiornamento da AEM 6.2 a 6.5, è importante rivedere le funzioni AEM 6.3 obsolete e rimosse oltre a quelle per AEM 6.5.

![trei_ritagliato](assets/trei_cropped.png)

Il rilevamento dei pattern introdotto di recente dovrebbe fornire una stima abbastanza precisa di cosa aspettarsi durante un aggiornamento per la maggior parte dei casi. Tuttavia, per le personalizzazioni e le distribuzioni più complesse in cui si verificano modifiche incompatibili, è possibile aggiornare un&#39;istanza di sviluppo a AEM 6.5 in base alle istruzioni riportate in [Esecuzione di un aggiornamento locale](/help/sites-deploying/in-place-upgrade.md). Una volta completato, eseguire alcuni test di fumo ad alto livello su questo ambiente. L&#39;obiettivo di questo esercizio non è di completare esaustivamente l&#39;inventario dei casi di test e produrre un inventario formale dei difetti, ma di darci una stima approssimativa della quantità di lavoro che sarà richiesto per aggiornare il codice per la compatibilità 6.5. In combinazione con le [Rilevamento pattern](/help/sites-deploying/pattern-detector.md) e le modifiche architettoniche determinate nella sezione precedente, è possibile fornire al team di gestione del progetto una stima approssimativa per la pianificazione dell&#39;aggiornamento.

### Creazione del Runbook di aggiornamento e ripristino {#building-the-upgrade-and-rollback-runbook}

Sebbene  Adobe abbia documentato il processo di aggiornamento di un&#39;istanza AEM, il layout di rete, l&#39;architettura di distribuzione e le personalizzazioni di ciascun cliente richiederanno una messa a punto e una personalizzazione di questo approccio. Per questo motivo, ti invitiamo a consultare tutta la documentazione fornita e a utilizzarla per informare un runbook specifico per il progetto che delinea le procedure di aggiornamento e ripristino specifiche che seguirai nel tuo ambiente. Se si esegue l&#39;aggiornamento da CRX2, assicurarsi di valutare quanto tempo impiegherà la migrazione dei contenuti per passare da CRX2 a Oak. Per i grandi repository, potrebbe essere sostanziale.

![organigramma](assets/runbook-diagram.png)

Abbiamo fornito procedure di aggiornamento e ripristino in [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md), nonché istruzioni dettagliate per l&#39;applicazione dell&#39;aggiornamento in Esecuzione di un [Aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md). Queste istruzioni devono essere riviste e prese in considerazione con l&#39;architettura del sistema, le personalizzazioni e la tolleranza di inattività per determinare le procedure di switch-over e rollback appropriate che verranno eseguite durante l&#39;aggiornamento. Eventuali modifiche all&#39;architettura o alle dimensioni del server devono essere incluse nella progettazione del runbook personalizzato. E&#39; importante notare che questo dovrebbe essere trattato come un primo progetto. Quando il team completa i cicli di QA e di sviluppo e implementa l&#39;aggiornamento nell&#39;ambiente di pre-produzione, è probabile che sia necessaria la necessità di alcuni passaggi aggiuntivi. Idealmente, il presente documento dovrebbe contenere informazioni sufficienti affinché, se consegnato a un membro del personale operativo, possa completare l&#39;aggiornamento completamente dalle informazioni contenute all&#39;interno.

### Sviluppo di un piano di progetto {#developing-a-project-plan}

Possiamo utilizzare l&#39;output degli esercizi precedenti per creare un piano di progetto che copra le tempistiche previste per i nostri sforzi di test o sviluppo, formazione e l&#39;esecuzione effettiva dell&#39;aggiornamento.

![piano di sviluppo](assets/develop-project-plan.png)

Un piano di progetto globale dovrebbe includere:

* Completamento dei piani di sviluppo e di collaudo
* Aggiornamento di ambienti di sviluppo e di controllo della qualità
* Aggiornamento della base di codice personalizzata per AEM 6.5
* Un ciclo di verifica e correzione della qualità
* Aggiornamento dell&#39;ambiente di gestione temporanea
* Integrazione, prestazioni e test del carico
* Certificazione ambientale
* Vai live

### Esecuzione di sviluppo e QA {#performing-development-and-qa}

Abbiamo fornito procedure per [Aggiornamento del codice e delle personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md) compatibili con AEM 6.5. Poiché questo processo iterativo viene eseguito, è necessario apportare modifiche al runbook in base alle esigenze. Consultare anche [Compatibilità con le versioni precedenti nella AEM 6.5](/help/sites-deploying/backward-compatibility.md) per informazioni su come le personalizzazioni possono rimanere compatibili con le versioni precedenti nella maggior parte dei casi senza richiedere lo sviluppo subito dopo l&#39;aggiornamento.

![patru_cropped](assets/patru_cropped.png)

Il processo di sviluppo e test è in genere iterativo. A causa delle personalizzazioni, le modifiche apportate durante l&#39;aggiornamento potrebbero rendere inutilizzabile un&#39;intera sezione del prodotto. Una volta che gli sviluppatori hanno affrontato la causa principale del problema e che il team di test ha accesso per testare queste funzionalità, è possibile che vengano individuati ulteriori problemi. Poiché vengono rilevati problemi che richiedono modifiche al processo di aggiornamento, accertati di aggiungerli al runbook di aggiornamento personalizzato. Dopo diverse fasi di test e correzione, la base di codice deve essere completamente convalidata e pronta per la distribuzione nell&#39;ambiente di gestione temporanea.

### Test finale {#final-testing}

Consigliamo di eseguire un ciclo finale di test dopo che la base di codice è stata certificata dal team di controllo qualità dell&#39;organizzazione. Questo ciclo di test comporterà la convalida del runbook in un ambiente di verifica, seguita da cicli di accettazione, prestazioni e test di protezione da parte dell&#39;utente.

![cinci_ritagliato](assets/cinci_cropped.png)

Questo passaggio è fondamentale, in quanto è l&#39;unico momento in cui è possibile convalidare i passaggi del runbook rispetto a un ambiente di produzione. Una volta aggiornato l&#39;ambiente, è importante concedere agli utenti finali un certo tempo di tempo per accedere e svolgere le attività che svolgono quando utilizzano il sistema nelle loro attività quotidiane. Non è raro che gli utenti utilizzino una parte del sistema che non era stata considerata in precedenza. Trovare e correggere i problemi in queste aree prima del live può aiutare a prevenire costose interruzioni di produzione. Poiché una nuova versione di AEM contiene modifiche significative alla piattaforma sottostante, è importante eseguire test di prestazioni, carico e sicurezza sul sistema come se lo stessimo avviando per la prima volta.

### Esecuzione dell&#39;aggiornamento {#performing-the-upgrade}

Una volta ricevuta la firma finale da parte di tutte le parti interessate, è il momento di eseguire le procedure del runbook che sono state definite. Abbiamo fornito i passaggi per l&#39;aggiornamento e il ripristino in [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md) e i passaggi di installazione in Esecuzione di un [Aggiornamento in loco](/help/sites-deploying/in-place-upgrade.md) come punto di riferimento.

![execute-upgrade](assets/perform-upgrade.png)

Nelle istruzioni per la convalida dell&#39;ambiente sono stati forniti alcuni passaggi. Questi includono controlli di base come la scansione dei registri di aggiornamento e la verifica che tutti i bundle OSGi siano stati avviati correttamente, ma consigliamo anche la convalida con i vostri casi di test basati sui vostri processi aziendali. Consigliamo inoltre di controllare la pianificazione di AEM pulizia revisioni online e le relative routine per assicurarsi che si verifichino durante un periodo di inattività della società. Queste routine sono essenziali per le prestazioni a lungo termine della AEM.
