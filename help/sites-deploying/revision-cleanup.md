---
title: Pulizia revisioni
seo-title: Pulizia revisioni
description: Scoprite come utilizzare la funzionalità Revision Cleanup (Pulizia delle revisioni) in AEM 6.3.
seo-description: Scoprite come utilizzare la funzionalità Revision Cleanup (Pulizia delle revisioni) in AEM 6.3.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '5916'
ht-degree: 0%

---


# Revision Cleanup{#revision-cleanup}

## Introduzione {#introduction}

Ogni aggiornamento al repository crea una nuova revisione del contenuto. Di conseguenza, con ogni aggiornamento le dimensioni del repository aumentano. Per evitare una crescita incontrollata del repository, le vecchie revisioni devono essere pulite per liberare risorse su disco. Questa funzionalità di manutenzione è denominata Revision Cleanup (Pulizia revisioni). È disponibile come routine offline dal AEM 6.0.

Con AEM 6.3 è stata introdotta una versione online di questa funzionalità denominata Pulizia revisioni online. Rispetto alla funzione di pulizia revisioni offline, in cui l&#39;istanza AEM deve essere chiusa, è possibile eseguire la pulizia revisioni online mentre l&#39;istanza AEM è online. Pulizia revisioni online è attivata per impostazione predefinita ed è il metodo consigliato per eseguire una pulizia revisioni.

**Nota**:  [Per un’introduzione al ](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) video e come utilizzare la funzione Pulizia revisioni online, consultate il video.

Il processo di pulizia della revisione è costituito da tre fasi: **stima**, **compazione** e **pulizia**. La stima determina se eseguire o meno la fase successiva (compazione) in base alla quantità di rifiuti che potrebbe essere raccolta. Durante la fase di compattazione i segmenti e i file tar vengono riscritti, lasciando fuori qualsiasi contenuto inutilizzato. La fase di pulizia in seguito rimuove i vecchi segmenti, inclusi eventuali rifiuti che potrebbero contenere. In genere, la modalità offline può recuperare più spazio, perché la modalità online deve tenere conto AEM set di lavoro, che conserva ulteriori segmenti da raccogliere.

Per ulteriori dettagli sulla pulizia delle revisioni, consultate i seguenti collegamenti:

* [Come eseguire la pulizia delle revisioni online](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [Pulizia della revisione online - Domande frequenti](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [Come eseguire la pulizia revisioni offline](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

È inoltre possibile leggere la [documentazione ufficiale Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### Quando utilizzare la funzione di pulizia revisioni online invece della funzione di pulizia revisioni offline? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**Pulizia revisioni online è il metodo consigliato per eseguire la pulizia revisioni.** La pulizia della revisione offline deve essere utilizzata solo in modo eccezionale, ad esempio prima di eseguire la migrazione al nuovo formato di storage o se l&#39;Assistenza clienti  Adobe lo richiede.

## Come eseguire la pulizia delle revisioni online {#how-to-run-online-revision-cleanup}

Per impostazione predefinita, la funzione Pulizia revisioni online è configurata per essere eseguita automaticamente una volta al giorno sia nelle istanze di AEM Author che Publish. È sufficiente definire la finestra di manutenzione durante un periodo con la minore attività utente. È possibile configurare l&#39;attività Pulizia revisioni online come segue:

1. Nella finestra principale della AEM, andate a **Strumenti - Operazioni - Dashboard - Manutenzione** oppure indirizzate il browser a: `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Passa il cursore del mouse su **Finestra di manutenzione giornaliera** e fai clic sull&#39;icona **Impostazioni**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Immettete i valori desiderati (ricorrenza, ora di inizio e ora di fine) e fate clic su **Salva**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

In alternativa, se si desidera eseguire manualmente l&#39;attività di pulizia revisioni, è possibile:

1. Vai a **Strumenti - Operazioni - Dashboard - Manutenzione** oppure passa direttamente a `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. Fare clic su **Finestra di manutenzione giornaliera**.
1. Passa il cursore del mouse sull&#39;icona **Revision Cleanup**.
1. Fare clic su **Esegui**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### Esecuzione della pulizia della revisione online dopo la pulizia della revisione offline {#running-online-revision-cleanup-after-offline-revision-cleanup}

Il processo di pulizia revisioni richiama le precedenti revisioni per generazioni. Ciò significa che ogni volta che si esegue la pulizia revisioni viene creata e mantenuta sul disco una nuova generazione. Esiste tuttavia una differenza tra i due tipi di pulizia revisioni: la pulizia delle revisioni offline consente di mantenere una sola generazione mentre la pulizia delle revisioni online consente di mantenere due generazioni. Pertanto, quando si esegue la pulizia delle revisioni online **dopo** la pulizia delle revisioni offline avviene quanto segue:

1. Dopo la prima esecuzione della pulizia della revisione online, la dimensione del repository raddoppierà. Ciò accade perché ora ci sono due generazioni che vengono conservate sul disco.
1. Durante le esecuzioni successive, il repository crescerà temporaneamente durante la creazione della nuova generazione e quindi stabilizzerà nuovamente le dimensioni che aveva dopo la prima esecuzione, in quanto il processo di pulizia della revisione online rireclama la generazione precedente.

Inoltre, tenete presente che, a seconda del tipo e del numero di commit, ogni generazione può variare in dimensione rispetto a quella precedente, in modo che la dimensione finale possa variare da un&#39;esecuzione all&#39;altra.

Per questo motivo, si consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione del repository inizialmente stimata.

## Modalità Di Compattazione Completa E Coda {#full-and-tail-compaction-modes}

**AEM 6.5** introduce  **due nuovi** modelli per la fase di  **** confronto del processo di pulizia delle revisioni online:

* La modalità **compattazione completa** riscrive tutti i segmenti e i file tar nell&#39;intero repository. La successiva fase di pulizia può quindi rimuovere la quantità massima di rifiuti nel repository. Poiché la compattazione completa interessa l&#39;intero repository, richiede una notevole quantità di risorse di sistema e tempo per il completamento. La compattazione completa corrisponde alla fase di compattazione della AEM 6.3.
* La modalità **compattazione coda** riscrive solo i segmenti e i file tar più recenti nella directory archivio. I segmenti e i file tar più recenti sono quelli aggiunti dall’ultima esecuzione della compattazione completa o coda. La successiva fase di pulizia può quindi rimuovere solo i rifiuti contenuti nella parte recente del repository. Poiché la compattazione di coda interessa solo una parte del repository, richiede molto meno risorse di sistema e tempo per il completamento rispetto alla compattazione completa.

Queste modalità di compattazione costituiscono un compromesso tra efficienza e consumo delle risorse: mentre la compattazione della coda è meno efficace ha anche un minore impatto sul normale funzionamento del sistema. Al contrario, la compattazione completa è più efficace ma ha un impatto maggiore sul normale funzionamento del sistema.

AEM 6.5 introduce anche un meccanismo di deduplicazione dei contenuti più efficiente durante la compattazione, che riduce ulteriormente l&#39;impatto sul disco del repository.

I due grafici riportati di seguito illustrano i risultati dei test di laboratorio interni che illustrano la riduzione dei tempi di esecuzione medi e l&#39;impronta media su disco nel AEM 6.5 rispetto a AEM 6.3:

![onrc-durata-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### Come configurare la compattazione completa e dettagliata {#how-to-configure-full-and-tail-compaction}

La configurazione predefinita esegue la compattazione della coda nei giorni della settimana e la compattazione completa la domenica. La configurazione predefinita può essere modificata utilizzando il nuovo valore di configurazione `full.gc.days` dell&#39; `RevisionCleanupTask` [attività di manutenzione](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

Quando si configura il valore `full.gc.days`, tenere presente che la compattazione completa verrà eseguita nei giorni definiti nel valore e la compattazione coda verrà eseguita nei giorni non definiti nel valore. Ad esempio, se configuri la compattazione completa per l&#39;esecuzione di domenica, la compattazione della coda verrà eseguita dal lunedì al sabato. Se, ad esempio, si configura la compattazione completa per l&#39;esecuzione ogni giorno della settimana, la compattazione coda non verrà eseguita affatto.

Inoltre, prendere in considerazione che:

* **La** compattazione della coda è meno efficace e ha un minore impatto sulle normali operazioni del sistema. Essa è pertanto destinata ad essere eseguita durante le giornate lavorative.
* **La** compattazione completa è più efficace, ma ha anche un impatto maggiore sulle normali operazioni del sistema. Esso è pertanto destinato ad essere utilizzato fuori dei giorni lavorativi.
* Sia la compattazione della coda che la compattazione completa dovrebbero essere programmate per funzionare durante le ore di punta.

### Risoluzione dei problemi {#troubleshooting}

Quando si utilizzano le nuove modalità di compattazione, tenere presente quanto segue:

* È possibile monitorare l&#39;attività di ingresso/uscita (I/O), ad esempio: Operazioni I/O, CPU in attesa di IO, dimensione della coda di commit. Questo consente di determinare se il sistema sta diventando un binding di I/O e richiede il ridimensionamento.
* La `RevisionCleanupTaskHealthCheck` indica lo stato di integrità generale della pulizia delle revisioni online. Funziona come nel AEM 6.3 e non fa distinzione tra compattazione completa e coda.
* I messaggi di registro contengono informazioni rilevanti sulle modalità di compattazione. Ad esempio, all&#39;avvio della funzione Pulizia revisioni online, i messaggi di registro corrispondenti indicheranno la modalità di compattazione. Inoltre, in alcuni casi d&#39;angolo, il sistema tornerà alla compattazione completa quando era pianificato per eseguire una compattazione coda e i messaggi di registro indicheranno questa modifica. I seguenti esempi di registro indicano la modalità di compattazione e il passaggio dalla coda alla compattazione completa:

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### Limitazioni note {#known-limitations}

In alcuni casi, l&#39;alternanza tra la coda e le modalità di compattazione completa ritarda il processo di pulizia. Più precisamente, il repository crescerà dopo una compattazione completa (raddoppierà le dimensioni). Lo spazio aggiuntivo verrà riutilizzato nella successiva compattazione della coda, quando il repository scenderà al di sotto della dimensione di compattazione precompleta. È inoltre necessario evitare l&#39;esecuzione parallela delle attività di manutenzione.

**Si consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione del repository inizialmente stimata.**

## Ripulisci revisioni online Domande frequenti {#online-revision-cleanup-frequently-asked-questions}

### Considerazioni sull&#39;aggiornamento di AEM 6.5 {#aem-upgrade-considerations}

<table>
 <tbody>
  <tr>
   <td>Domande </td>
   <td>Risposte</td>
  </tr>
  <tr>
   <td>Cosa devo sapere quando eseguo l'aggiornamento a AEM 6.5?</td>
   <td><p>Il formato di persistenza di TarMK cambierà con AEM 6.5. Queste modifiche non richiedono un passaggio di migrazione proattiva. I repository esistenti passeranno attraverso una migrazione continua, trasparente per l'utente. Il processo di migrazione viene avviato la prima volta AEM 6.5 (o strumenti correlati) accede al repository.</p> <p><strong>Una volta avviata la migrazione al formato di persistenza AEM 6.5, l'archivio non può essere ripristinato al precedente formato di persistenza AEM 6.3.</strong></p> </td>
  </tr>
 </tbody>
</table>

### Migrazione all&#39;indicatore del segmento Oak {#migrating-to-oak-segment-tar}

<table>
 <tbody>
  <tr>
   <td><strong>Domande</strong></td>
   <td><strong>Risposte</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché è necessario migrare il repository?</strong></td>
   <td><p>In AEM 6.3 erano necessarie modifiche al formato di storage, in particolare per migliorare le prestazioni e l'efficacia della pulizia della revisione online. Queste modifiche non sono compatibili con le versioni precedenti e i repository creati con il vecchio segmento Oak (AEM 6.2 e versioni precedenti) devono essere migrati.</p> <p>Ulteriori vantaggi della modifica del formato di storage:</p>
    <ul>
     <li>Migliore scalabilità (dimensione del segmento ottimizzata).</li>
     <li><a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">Raccolta dei dati archiviati più rapidamente</a>.<br /> </li>
     <li>Lavoro di terra per miglioramenti futuri.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Il formato Tar precedente è ancora supportato?</strong></td>
   <td>Con AEM 6.3 è supportata solo la nuova ar segmento Oak.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>La migrazione dei contenuti è sempre obbligatoria?</strong></td>
   <td>Sì. Se non iniziate con una nuova istanza, dovrete sempre migrare il contenuto.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Posso effettuare l’aggiornamento alla versione 6.3 ed eseguire la migrazione in un secondo momento (ad esempio, utilizzando un’altra finestra di manutenzione)?</strong></td>
   <td>No, come spiegato in precedenza, la migrazione dei contenuti è obbligatoria.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>È possibile evitare i tempi di inattività durante la migrazione?</strong></td>
   <td>No. Si tratta di uno sforzo una tantum che non può essere eseguito su un'istanza in esecuzione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede se si esegue accidentalmente un'esecuzione in base al formato di repository errato?</strong></td>
   <td>Se si tenta di eseguire il modulo del segmento di rovere su un repository di catrame segmento di quercia (o viceversa), l'avvio non riuscirà con un <em>IllegalStateException</em> con il messaggio "Formato segmento non valido". Nessun danneggiamento dei dati.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Sarà necessario reindicizzare gli indici di ricerca?</strong></td>
   <td>No. La migrazione dal segmento di quercia al segmento di quercia introduce modifiche nel formato contenitore. I dati contenuti non vengono modificati.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come calcolare al meglio lo spazio su disco necessario durante e dopo la migrazione?</strong></td>
   <td>La migrazione equivale a ricreare l'archivio segmenti nel nuovo formato. Questo può essere utilizzato per stimare lo spazio su disco aggiuntivo necessario durante la migrazione. Dopo la migrazione, il vecchio store di segmenti può essere eliminato per recuperare spazio.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come stimare al meglio la durata della migrazione?</strong></td>
   <td>Le prestazioni di migrazione possono essere notevolmente migliorate se <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">pulizia revisioni offline</a> viene eseguita prima della migrazione. Tutti i clienti sono invitati a eseguirla come prerequisito del processo di aggiornamento. In generale, la durata della migrazione deve essere simile alla durata dell'attività di pulizia della revisione offline, partendo dal presupposto che l'attività di pulizia della revisione offline sia stata eseguita prima della migrazione.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Esecuzione pulizia revisioni online {#running-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>Domande</strong></td>
   <td><strong>Risposte</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Con quale frequenza deve essere eseguita la pulizia delle revisioni online?</strong></td>
   <td>Una volta al giorno. Questa è la configurazione predefinita nel dashboard delle operazioni.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come posso configurare l'ora di inizio dell'attività di manutenzione Pulizia revisioni online?</strong></td>
   <td>Vedere la sezione <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">Modalità di esecuzione della pulizia delle revisioni online</a>. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Esiste una frequenza massima che non deve essere superata per la pulizia delle revisioni online?</strong></td>
   <td>Si consiglia di eseguire la pulizia delle revisioni online una volta al giorno, come configurato per impostazione predefinita.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono gli indicatori chiave che determinano la frequenza con cui deve essere eseguita la pulizia delle revisioni online?</strong></td>
   <td>Non è necessario determinare la frequenza, in quanto la funzione di pulizia revisioni online è configurata come attività di manutenzione e viene eseguita automaticamente ogni giorno.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché la pulizia della revisione online non recupera spazio se eseguita per la prima volta?</strong></td>
   <td>Pulizia revisioni online recupera le vecchie revisioni per generazioni. Viene generata una nuova generazione ogni volta che viene eseguita la pulizia della revisione. Solo il contenuto che ha almeno due generazioni di età sarà riutilizzato, il che significa che in una prima fase non c'è nulla da recuperare.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché la prima Pulizia revisioni online non recupera spazio se eseguita dopo la pulizia revisioni offline?</strong></td>
   <td><p>Pulizia revisioni offline sta recuperando tutto tranne l'ultima generazione rispetto alle ultime due generazioni per la pulizia revisioni online. Nel caso di un nuovo repository, la funzione di pulizia revisioni online non recupererà alcuno spazio se eseguita per la prima volta dopo la pulizia revisioni offline, perché non esiste una generazione abbastanza grande per essere rigenerata.</p> <p>Inoltre, leggere la sezione "Running Online Revision Cleanup after Offline Revision Cleanup" di <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">questo capitolo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>In genere, Author e Publish dispongono di diverse finestre di pulizia revisioni online?</strong></td>
   <td>Questo dipende dalle ore di ufficio e dai percorsi di traffico della presenza online del cliente. Le finestre di manutenzione devono essere configurate al di fuori dei principali tempi di produzione per garantire la migliore efficacia di pulizia. Per più istanze di AEM Publish (farm TarMK), le finestre di manutenzione per la pulizia delle revisioni online devono essere barrate.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Esistono dei prerequisiti prima di eseguire la pulizia revisioni online?</strong></td>
   <td><p>La pulizia delle revisioni online è disponibile solo con AEM 6.3 e versioni successive. Inoltre, se si utilizza una versione precedente di AEM è necessario eseguire la migrazione alla nuova <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">ar segmento Oak</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono i fattori che determinano la durata della pulizia della revisione online?</strong></td>
   <td>I fattori sono:<br />
    <ul>
     <li>Dimensione archivio</li>
     <li>Carica sul sistema (richieste al minuto, in particolare operazioni di scrittura)</li>
     <li>Pattern di attività (letture e scrittura)</li>
     <li>Specifiche hardware (prestazioni CPU, memoria, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Gli autori possono continuare a funzionare mentre è in esecuzione la pulizia delle revisioni online?</strong></td>
   <td>Sì, Online Revision Cleanup può gestire le scritture simultanee. Tuttavia, la funzione di pulizia revisioni online funziona in modo più rapido ed efficiente senza transazioni di scrittura simultanee. Si consiglia di pianificare l'attività di manutenzione Pulizia revisioni online per un tempo relativamente tranquillo senza traffico eccessivo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono i requisiti minimi per lo spazio su disco e la memoria heap durante l'esecuzione della pulizia delle revisioni online?</strong></td>
   <td><p>Lo spazio su disco viene monitorato continuamente durante la pulizia delle revisioni online. Se lo spazio disponibile su disco scende al di sotto di un valore critico, il processo verrà annullato. Il valore critico è il 25% dell'attuale spazio su disco del repository e non è configurabile.</p> <p><strong>Si consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione del repository inizialmente stimata.</strong></p> <p>Durante il processo di pulizia, lo spazio libero dell'heap viene monitorato in modo continuo. Se lo spazio di heap gratuito si riduce al di sotto di un valore critico, il processo viene annullato. Il valore critico è configurato tramite org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD. Il valore predefinito è 15%.</p> <p>Le dimensioni minime dell'heap della compattazione Recommendations non sono separate dalle raccomandazioni di ridimensionamento della memoria AEM. Come regola generale: <strong>Se un'istanza AEM ha dimensioni sufficienti per far fronte ai casi di utilizzo e al relativo payload previsto, il processo di pulizia otterrà memoria sufficiente.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Qual è l'impatto previsto sulle prestazioni durante l'esecuzione della pulizia delle revisioni online?</strong></td>
   <td>Pulizia revisioni online è un processo in background che legge e scrive nel repository contemporaneamente alle normali operazioni di sistema. In particolare, potrebbe essere necessario acquisire l'accesso esclusivo al repository per un breve periodo di tempo, impedendo ad altri thread di scrivere nel repository.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Per quanto tempo è prevista l'esecuzione di Online Revision Cleanup?</strong></td>
   <td>L'esecuzione non dovrebbe richiedere più di 2 ore in base agli ultimi test di prestazioni eseguiti internamente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa fare se la pulizia della revisione online richiede più tempo?</strong></td>
   <td>
    <ul>
     <li>Assicurarsi che venga eseguito ogni giorno.<br /> </li>
     <li>Assicurarsi che venga eseguito durante le attività minime del repository configurando di conseguenza le finestre di manutenzione in Operations Dashboard.</li>
     <li>Scalabilità delle risorse di sistema (CPU, memoria, I/O).</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede se la funzione di pulizia revisioni online supera le finestre di manutenzione configurate?</strong></td>
   <td>Assicuratevi che le altre attività di manutenzione non rallentino l’esecuzione. Ciò potrebbe verificarsi se all'interno della stessa finestra di manutenzione vengono eseguite più attività di manutenzione rispetto a Pulizia revisioni online. Le attività di manutenzione vengono eseguite in sequenza senza un ordine configurabile.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché il processo di garbage collection delle revisioni viene ignorato?</strong></td>
   <td><p>Revision Cleanup si basa su una fase di stima per decidere se ci sono abbastanza rifiuti da pulire. Lo stimatore confronta la dimensione corrente con quella dell'archivio dopo l'ultima compattazione. Se la dimensione supera il delta configurato, la pulizia viene eseguita. La dimensione delta è impostata su 1 GB. Questo significa che se la dimensione del repository non è cresciuta di 1 GB dall'ultima esecuzione della pulizia, la nuova iterazione di pulizia della revisione verrà saltata. </p> <p>Di seguito sono riportate le voci di registro rilevanti per la fase di stima:</p>
    <ul>
     <li>Verrà eseguito il GC di revisione: <em>Il delta delle dimensioni è N% o N/N (N/N byte), quindi la compattazione in esecuzione</em></li>
     <li>La revisione GC <strong>non</strong> verrà eseguita: <em>Il delta delle dimensioni è N% o N/N (N/N byte), pertanto la compattazione per il momento viene ignorata</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>È possibile interrompere in modo sicuro la compattazione automatica se l'impatto delle prestazioni è troppo alto?</strong></td>
   <td>Sì. A partire dal AEM 6.3 può essere arrestato in modo sicuro tramite la finestra Attività di manutenzione all'interno del Pannello operazioni o tramite JMX.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Se l'istanza AEM viene chiusa durante un'attività di pulizia pianificata, il processo si interrompe in modo sicuro oppure l'arresto viene bloccato fino al completamento della compattazione?</strong></td>
   <td>La pulizia delle revisioni verrà interrotta e la directory archivio verrà chiusa in modo sicuro.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede quando il sistema si arresta in modo anomalo durante la pulizia delle revisioni online?</strong></td>
   <td>In tali casi non vi è alcun rischio di corruzione dei dati. Gli avanzi della spazzatura verranno ripuliti da un'esecuzione successiva.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Qual è l'impatto dell'assenza di pulizia revisioni online?</strong></td>
   <td>Diminuzione delle prestazioni nel tempo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali revisioni vengono raccolte?</strong></td>
   <td>Per impostazione predefinita, la funzione Pulizia revisioni online raccoglie solo le revisioni risalenti almeno a 24 ore prima.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede in caso di troppa interferenza da scritture simultanee al repository?</strong></td>
   <td><p>In presenza di concorrenza di scrittura nel sistema, la pulizia della revisione online potrebbe richiedere l'accesso in scrittura esclusivo per poter eseguire il commit delle modifiche alla fine di un ciclo di compattazione. Il sistema entrerà in <strong>forceCompact mode</strong>, come spiegato più in dettaglio nella <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">documentazione di rovere</a>. Durante la forza compatta, viene acquisito un blocco di scrittura esclusivo per eseguire finalmente le modifiche senza interferenze di scrittura simultanee. Per limitare l'impatto sui tempi di risposta è possibile definire un valore di timeout. Questo valore è impostato su 1 minuto per impostazione predefinita, il che significa che se la forza compatta non viene completata entro 1 minuto, il processo di compattazione verrà interrotto in favore di commit simultanei.</p> <p>La durata della forza compatta dipende dai seguenti fattori:</p>
    <ul>
     <li>hardware: IOPS. La durata diminuisce con più IOPS.</li>
     <li>dimensione dell'archivio segmenti: la durata aumenta con la dimensione dell'archivio segmenti.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>In che modo viene eseguita la pulizia delle revisioni online in un'istanza in standby?</strong></p> </td>
   <td><p>In una configurazione in standby freddo, solo l'istanza principale deve essere configurata per eseguire la pulizia revisioni online. Nell’istanza standby, la funzione Pulizia revisioni online non deve essere pianificata in modo specifico.</p> <p>L'operazione corrispondente in un'istanza in standby è la Pulizia automatica, corrispondente alla fase di pulizia della Pulizia revisioni online. La pulizia automatica viene eseguita nell'istanza standby dopo l'esecuzione della pulizia della revisione online sull'istanza principale.</p> <p>Le fasi di stima e compattazione non verranno eseguite in un'istanza in standby.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>La funzione di pulizia revisioni offline è in grado di liberare più spazio su disco rispetto alla funzione di pulizia revisioni online?</strong></td>
   <td><p>Pulizia revisioni offline può rimuovere immediatamente le vecchie revisioni mentre Pulizia revisioni online deve tenere conto delle precedenti revisioni a cui lo stack dell'applicazione fa ancora riferimento. Il primo può quindi rimuovere i rifiuti in modo più aggressivo rispetto al secondo in cui l'effetto viene ammortizzato nel corso di alcuni cicli di raccolta dei rifiuti.</p> <p>Inoltre, leggere la sezione "Running Online Revision Cleanup after Offline Revision Cleanup" di <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">questo capitolo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Considerazioni sulle operazioni dei file mappati sulla memoria?</td>
   <td>
    <ul>
     <li><strong>Negli ambienti</strong> Windows, l'accesso regolare ai file viene sempre imposto, pertanto l'accesso mappato alla memoria non viene utilizzato. Come consiglio generale, tutta la RAM disponibile deve essere assegnata all'heap e la dimensione segmentCache deve essere aumentata. Puoi aumentare la cache segmento aggiungendo l'opzione segmentCache.size all'org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config (ad esempio, segmentCache.size=20480). Ricordate di lasciare una parte di RAM per il sistema operativo e altri processi.</li>
     <li><strong>Negli ambienti</strong> non Windows, aumentare la dimensione della memoria fisica per migliorare la mappatura della memoria del repository.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Monitoraggio pulizia revisioni online {#monitoring-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>Cosa è necessario monitorare durante la pulizia delle revisioni online?</strong></td>
   <td>
    <ul>
     <li>Lo spazio su disco deve essere monitorato quando è abilitata la funzione di pulizia revisioni online. La pulizia non verrà eseguita o verrà terminata in modo preventivo quando lo spazio su disco non è sufficiente.</li>
     <li>Controllate i registri per verificare l’ora di completamento della pulizia revisioni online. Non dovrebbe richiedere più di due ore.</li>
     <li>Numero di checkpoint. Se durante l'esecuzione della compattazione sono presenti più di 3 checkpoint, si consiglia di pulire i checkpoint.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come verificare se la pulizia delle revisioni online è stata completata correttamente?</strong></td>
   <td><p>È possibile verificare se la pulizia della revisione online è stata completata correttamente controllando i registri.</p> <p>Ad esempio, "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>" indica il passaggio di compattazione completato correttamente, a meno che non sia preceduto dal messaggio "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>", il che significa che il carico simultaneo è stato eccessivo.</p> <p>Di conseguenza, viene visualizzato il messaggio "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>" per completare correttamente il passaggio di pulizia.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>Dove è possibile trovare le statistiche delle ultime esecuzioni Online Revision Cleanup?</strong></td>
   <td><p>Stato, avanzamento e statistiche sono esposti tramite JMX (<code>SegmentRevisionGarbageCollection</code> MBean). Per ulteriori dettagli su <code>SegmentRevisionGarbageCollection</code> MBean, leggere il <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">seguente paragrafo</a>.</p> <p>I progressi possono essere tracciati tramite l'attributo <code>EstimatedRevisionGCCompletion</code> del <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>È possibile ottenere un riferimento di MBean utilizzando la variabile <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>.</p> <p>Le statistiche sono disponibili solo dall'ultimo avvio del sistema. Gli strumenti di monitoraggio esterni potrebbero essere utilizzati per mantenere i dati oltre AEM tempo di attività. Vedere <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">la documentazione AEM per allegare controlli dello stato a Nagios come esempio per uno strumento di monitoraggio esterno</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono le voci di registro rilevanti?</strong></td>
   <td>
    <ul>
     <li>Pulizia revisioni online avviata/interrotta
      <ul>
       <li>La pulizia della revisione online è composta da tre fasi: stima, compattazione e pulizia. La stima può forzare la compattazione e la pulizia a saltare se il repository non contiene abbastanza rifiuti. Nell'ultima versione di AEM, il messaggio "<code>TarMK GC #{}: estimation started</code>" indica l'inizio della stima, "<code>TarMK GC #{}: compaction started, strategy={}</code>" indica l'inizio della compattazione e "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>" indica l'inizio della pulizia.</li>
      </ul> </li>
     <li>Spazio su disco ottenuto dalla pulizia della revisione
      <ul>
       <li>Lo spazio viene recuperato solo al termine della fase di pulizia. Il completamento della fase di pulizia è contrassegnato dal messaggio di registro "T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>". La dimensione della pulizia del post è {} ({} byte) e lo spazio è stato recuperato {} ({} byte). Peso/profondità della mappa di compattazione: {}/{} ({} byte/{})."</li>
      </ul> </li>
     <li>Si è verificato un problema durante la pulizia della revisione
      <ul>
       <li>Ci sono molte condizioni di errore, tutte sono contrassegnate da messaggi di log WARN o ERROR con "TarMK GC".</li>
      </ul> </li>
    </ul> <p>Consultare anche la sezione <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Risoluzione dei problemi in base ai messaggi di errore</a> di seguito.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come controllare quanto spazio è stato recuperato dopo il completamento della pulizia delle revisioni online?</strong></td>
   <td>Nel registro è presente un messaggio alla fine del ciclo di pulizia: "<code>TarMK GC #3: cleanup completed</code>" che include le dimensioni del repository e la quantità di rifiuti recuperati.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come verificare l'integrità del repository dopo il completamento della pulizia delle revisioni online?</strong></td>
   <td><p>Una verifica dell'integrità dell'archivio non è necessaria dopo la pulizia delle revisioni online. </p> <p>Tuttavia, potete eseguire le azioni seguenti per verificare lo stato dell’archivio dopo la pulizia:</p>
    <ul>
     <li>Un repository <a href="/help/sites-deploying/consistency-check.md" target="_blank">controllo traversal</a></li>
     <li>Dopo il completamento del processo di pulizia, usate lo strumento di esecuzione della quercia per verificare la presenza di incoerenze. Per ulteriori informazioni su come eseguire questa operazione, consultare la <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Documentazione Apache.</a> Non è necessario arrestare AEM per eseguire lo strumento.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come rilevare se la pulizia della revisione online non è riuscita e quali sono i passaggi da ripristinare?</strong></td>
   <td>Le condizioni di errore sono contrassegnate dai messaggi di registro AVVERTENZA o ERRORE che iniziano con "TarMK GC". Consultare anche la sezione <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Risoluzione dei problemi in base ai messaggi di errore</a> di seguito.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali informazioni sono disponibili nel controllo integrità pulizia revisioni? Come e quando contribuiscono ai livelli di stato dei colori codificati? </strong></td>
   <td><p>Il controllo dello stato di pulizia delle revisioni fa parte del <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">pannello operativo</a>.<br /> </p> <p>Lo stato sarà <strong>GREEN</strong> se l'ultima esecuzione dell'attività di manutenzione Pulizia revisioni online è stata completata correttamente.</p> <p>Sarà <strong>YELLOW</strong> se l'attività di manutenzione per la pulizia delle revisioni online è stata annullata una volta.<br /> </p> <p>Sarà <strong>RED</strong> se l'attività di manutenzione per la pulizia delle revisioni online è stata annullata tre volte di seguito. <strong>In questo caso è </strong> necessaria l'interazione manuale oppure è probabile che la pulizia della revisione online restituisca un errore. Per ulteriori informazioni, consultare la sezione <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">Risoluzione dei problemi</a> di seguito.<br /> </p> <p>Inoltre, lo stato del controllo dello stato verrà ripristinato dopo il riavvio del sistema. Di conseguenza, un'istanza appena riavviata mostrerà uno stato verde nel controllo dello stato di pulizia revisioni. Gli strumenti di monitoraggio esterni potrebbero essere utilizzati per mantenere i dati oltre AEM tempo di attività. Vedere <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">la documentazione AEM per allegare controlli dello stato a Nagios come esempio per uno strumento di monitoraggio esterno</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Come monitorare la pulizia automatica in un'istanza in standby?</strong></p> </td>
   <td><p>Lo stato, l'avanzamento e le statistiche sono esposti tramite JMX utilizzando il supporto MBean <code>SegmentRevisionGarbageCollection</code>. Vedere anche la seguente <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">documentazione Oak</a>. </p> <p>È possibile ottenere un riferimento di MBean utilizzando la variabile <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection”</code>.</p> <p>Le statistiche sono disponibili solo dall'ultimo avvio del sistema. È possibile utilizzare strumenti di monitoraggio esterni per mantenere i dati al di là del tempo AEM. Vedere anche la <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">documentazione AEM per allegare controlli dello stato a Nagios come esempio per uno strumento di monitoraggio esterno</a>.</p> <p>I file di registro possono essere utilizzati anche per verificare lo stato, l’avanzamento e le statistiche della pulizia automatica.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Cosa è necessario monitorare durante la pulizia automatica in un'istanza in standby?</strong></p> </td>
   <td>
    <ul>
     <li>Durante l'esecuzione della pulizia automatica è necessario controllare lo spazio su disco.</li>
     <li>Tempo di completamento (tramite i registri) per garantire che non vengano superate 2 ore.</li>
     <li>Dimensione dell’archivio segmenti dopo l’esecuzione della pulizia automatica. La dimensione dell'archivio segmenti nell'istanza standby deve essere approssimativamente uguale a quella dell'istanza principale.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Risoluzione dei problemi di pulizia delle revisioni online {#troubleshooting-online-revision-cleanup}

<table>
 <tbody>
  <tr>
   <td><strong>Qual è il peggio che può accadere se non si esegue la pulizia delle revisioni online?</strong></td>
   <td>Lo spazio su disco dell'istanza AEM risulta insufficiente, con conseguente interruzione della produzione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Il traffico degli utenti è problematico per l’esecuzione della pulizia delle revisioni online in un’istanza di pubblicazione?</strong></td>
   <td>L'elevato traffico degli utenti ha un impatto sulla fase di compattazione che può essere completata o meno correttamente.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>In base al controllo dello stato e alle voci di registro, la pulizia della revisione online non è stata completata con successo tre volte di seguito. Cosa è necessario per completare la pulizia della revisione online?</strong></td>
   <td>Per trovare e risolvere il problema è possibile effettuare diverse operazioni:<br />
    <ul>
     <li>Innanzitutto, controllare le voci di registro<br /> </li>
     <li>A seconda delle informazioni contenute nei registri, intraprendere le azioni appropriate:
      <ul>
       <li>Se i registri mostrano cinque cicli compatti persi e un timeout nel ciclo <code>forceCompact</code>, pianificare la finestra di manutenzione a un tempo di inattività quando la quantità di scritture repository è bassa. È possibile controllare le scritture del repository nello strumento di monitoraggio delle metriche di repository, disponibile all'indirizzo <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>Se la pulizia viene interrotta alla fine della finestra di manutenzione, accertatevi che la configurazione della finestra di manutenzione nell’interfaccia utente Attività di manutenzione sia sufficientemente grande</li>
       <li>Se la memoria heap disponibile non è sufficiente, assicurarsi che l'istanza disponga di memoria sufficiente.</li>
       <li>In caso di reazione tardiva, l'archivio segmenti potrebbe crescere troppo per il completamento della pulizia delle revisioni online anche entro una finestra di manutenzione più lunga. Ad esempio, se non è stata completata la pulizia delle revisioni online con esito positivo nell'ultima settimana, si consiglia di pianificare una manutenzione offline ed eseguire la pulizia delle revisioni offline per riportare il segmentstore a una dimensione gestibile.</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa fare una volta attivato l'allarme Healthcheck?</strong></td>
   <td>Vedere il punto precedente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede se la funzione di pulizia revisioni online non ha più tempo a disposizione durante la finestra di manutenzione programmata?</strong></td>
   <td>La pulizia delle revisioni online verrà annullata e gli avanzi verranno rimossi. Verrà riavviata la prossima volta che la finestra di manutenzione sarà pianificata.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono le cause per cui le istanze <code>SegmentNotFoundException</code> vengono registrate nella <code>error.log</code> e come posso ripristinarle?</strong></td>
   <td><p>Un <code>SegmentNotFoundException</code> viene registrato da TarMK quando tenta di accedere a un'unità di archiviazione (un segmento) che non riesce a trovare. Esistono tre scenari che potrebbero causare il problema:</p>
    <ol>
     <li>Un'applicazione che aggira i meccanismi di accesso consigliati (come Sling e l'API JCR) e utilizza un API/SPI di livello inferiore per accedere all'archivio e quindi supera il tempo di conservazione di un segmento. In altre parole, mantiene un riferimento a un'entità più lungo del tempo di conservazione consentito dalla pulizia della revisione online (per impostazione predefinita, 24 ore). Questo caso è transitorio e non porta alla corruzione dei dati. Per recuperare, l'utensile di rovere deve essere utilizzato per confermare la natura transitoria dell'eccezione (il controllo di esecuzione della quercia non deve segnalare errori). A tal fine, l'istanza deve essere portata offline e riavviata successivamente.</li>
     <li>Un evento esterno ha causato il danneggiamento dei dati presenti sul disco. Può trattarsi di un errore del disco, di una mancanza di spazio su disco o di una modifica accidentale dei file di dati richiesti. In questo caso, l'istanza deve essere portata offline e riparata utilizzando il controllo di esecuzione della quercia. Per ulteriori dettagli su come eseguire il controllo di esecuzione della quercia, consultare la seguente <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">documentazione Apache</a>.</li>
     <li>Tutte le altre occorrenze devono essere risolte tramite l'Assistenza clienti <a href="https://helpx.adobe.com/it/marketing-cloud/contact-support.html" target="_blank"> Adobe</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Risoluzione dei problemi in base ai messaggi di errore {#troubleshooting-based-on-error-messages}

Il file error.log sarà dettagliato se si verificano degli incidenti durante il processo di pulizia della revisione online. La seguente matrice ha lo scopo di spiegare i messaggi più comuni e fornire possibili soluzioni:

| **Fase** | **Messaggi del registro** | **Spiegazione** | **Passaggi successivi** |
|---|---|---|---|
|  |  |  |  |
| Stima | TarMK GC #2: stima ignorata perché la compattazione è in pausa | La fase di stima viene saltata quando la compattazione viene disabilitata nel sistema dalla configurazione. | Abilita pulizia revisioni online. |
|  | TarMK GC #2: stima interrotta: ${REASON}. Salta la compattazione. | La fase di stima è terminata prematuramente. Alcuni esempi di eventi che potrebbero interrompere la fase di stima: memoria o spazio su disco insufficiente nel sistema host. | Dipende dal motivo dato. |
| Compaction | TarMK GC #2: compattazione in pausa | Finché la fase di compattazione viene messa in pausa dalla configurazione, non verrà eseguita né la fase di stima né la fase di compattazione. | Abilita pulizia revisioni online. |
|  | TarMK GC #2: compattazione annullata: ${REASON}. | La fase di compattazione è terminata prematuramente. Alcuni esempi di eventi che potrebbero interrompere la fase di compattazione: memoria o spazio su disco insufficiente nel sistema host. Inoltre, la compattazione può essere annullata anche chiudendo il sistema o annullandolo esplicitamente tramite interfacce amministrative come la finestra di manutenzione all&#39;interno del dashboard delle operazioni. | Dipende dal motivo dato. |
|  | TarMK GC #2: compattazione non riuscita in 32.902 min (1974140 ms), dopo 5 cicli | Questo messaggio non indica un errore irreversibile, ma solo che la compattazione è stata terminata dopo un certo numero di tentativi. Inoltre, leggere il [seguente paragrafo](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). | Leggete la seguente [documentazione Oak](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes) e l&#39;ultima domanda della sezione [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup). |
| Pulizia | TarMK GC #2: pulizia interrotta | La pulizia è stata annullata chiudendo la directory archivio. Non è previsto alcun impatto sulla coerenza. Inoltre, è probabile che lo spazio su disco non venga recuperato completamente. Verrà recuperato durante il prossimo ciclo di pulizia revisioni. | Verificare il motivo per cui il repository è stato chiuso e continuare a cercare di evitare la chiusura del repository durante le finestre di manutenzione. |

## Come eseguire la pulizia revisioni offline {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>È necessario utilizzare diverse versioni dello strumento Oak-run a seconda della versione Oak utilizzata con l&#39;installazione AEM. Prima di utilizzare lo strumento, controllare l&#39;elenco dei requisiti di versione riportato di seguito:
>
>* Per le versioni Oak **1.0.0 - 1.0.11** o **1.1.0 - 1.1.6**, utilizzare la versione di esecuzione Oak** 1.0.11**
   >
   >
* Per le versioni di Oak **più recenti rispetto a quanto indicato sopra**, utilizzare la versione di esecuzione Oak che corrisponde al nucleo Oak dell&#39;installazione AEM.

>



 Adobe fornisce uno strumento denominato **Esecuzione di Oak** per eseguire la pulizia delle revisioni. Può essere scaricato nel seguente percorso:

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

Lo strumento è un barattolo eseguibile che può essere eseguito manualmente per comprimere il repository. Il processo è denominato pulizia revisioni offline perché l&#39;archivio deve essere chiuso per poter eseguire correttamente lo strumento. Pianificare la pulizia in base alla finestra di manutenzione.

Per suggerimenti su come migliorare le prestazioni del processo di pulizia, vedere [Incremento delle prestazioni della pulizia delle revisioni offline](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>È inoltre possibile cancellare i vecchi checkpoint prima che venga effettuata la manutenzione (passaggi 2 e 3 nella procedura seguente). Questa opzione è consigliata solo per le istanze con più di 100 punti di controllo.

1. Accertatevi sempre di disporre di un backup recente dell&#39;istanza AEM.

   AEM.

1. (Facoltativo) Utilizzate lo strumento per individuare i vecchi checkpoint:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (Facoltativo) Quindi, eliminate i punti di controllo senza riferimento:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. Eseguire la compattazione e attendere il completamento:

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### Incremento delle prestazioni della pulizia delle revisioni offline {#increasing-the-performance-of-offline-revision-cleanup}

Lo strumento di esecuzione della quercia introduce diverse funzioni che mirano ad aumentare le prestazioni del processo di pulizia della revisione e ridurre il più possibile la finestra di manutenzione.

L&#39;elenco include diversi parametri della riga di comando, come descritto di seguito:

* **-mmap.** È possibile impostare questo valore su true o false. Se impostato su true, viene utilizzato l&#39;accesso mappato alla memoria. Se è impostato su false, viene utilizzato l&#39;accesso ai file. Se non viene specificato, l&#39;accesso mappato alla memoria viene utilizzato sui sistemi a 64 bit e l&#39;accesso ai file viene utilizzato sui sistemi a 32 bit. In Windows, l&#39;accesso regolare ai file viene sempre applicato e questa opzione viene ignorata. **Questo parametro ha sostituito il parametro -Dtar.memoryMapped.**

* **-Dupdate.limit**. Definisce la soglia per lo scaricamento su disco di una transazione temporanea. Il valore predefinito è 10000.

* **-Dcompress-interval**. Numero di voci della mappa di compattazione da mantenere fino alla compressione della mappa corrente. Il valore predefinito è 1000000. Se è disponibile una quantità sufficiente di memoria heap, è consigliabile aumentare questo valore fino a un numero ancora più elevato. **Questo parametro è stato rimosso nella versione 1.6 di Oak e non ha alcun effetto.**

* **-Dcompaction-progress-log**. Il numero di nodi compatti che verranno registrati. Il valore predefinito è 150000, il che significa che i primi 150000 nodi compatti verranno registrati durante l&#39;operazione. Utilizzate questo insieme al parametro successivo descritto di seguito.

* **-Dtar.PersistCompactionMap.** Impostate questo parametro su true per utilizzare lo spazio su disco invece della memoria heap per la persistenza della mappa di compattazione. Richiede lo strumento di esecuzione della quercia **versioni 1.4** e successive. Per ulteriori dettagli, vedere la domanda 3 nella sezione [Pulizia revisioni offline Domande frequenti](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions). **Questo parametro è stato rimosso nella versione 1.6 di Oak e non ha alcun effetto.**

* **—force.** Forza la compattazione e ignora una versione dell’archivio segmenti non corrispondente.

>[!CAUTION]
>
>L&#39;utilizzo del parametro `--force` consente di aggiornare l&#39;archivio segmenti alla versione più recente, il che è incompatibile con le versioni precedenti di Oak. Inoltre, tenete in considerazione che non è possibile eseguire il downgrade. Come regola generale, è necessario utilizzare questi parametri con cautela e solo se si è esperti su come utilizzarli.

Esempio dei parametri in uso:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### Metodi aggiuntivi per attivare la pulizia della revisione {#additional-methods-of-triggering-revision-cleanup}

Oltre ai metodi descritti qui sopra, è anche possibile attivare il meccanismo di pulizia revisioni utilizzando la console JMX come segue:

1. Aprite la console JMX scegliendo [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. Fare clic su **RevisionGarbageCollection** MBean.
1. Nella finestra successiva, fare clic su **startRevisionGC()**, quindi su **Invoke** per avviare il processo di raccolta dei rifiuti di revisione.

### Pulizia revisioni offline Domande frequenti {#offline-revision-cleanup-frequently-asked-questions}

<table>
 <tbody>
  <tr>
   <td><strong>Quali sono i fattori che determinano la durata della pulizia delle revisioni offline?</strong></td>
   <td><p>La dimensione del repository e la quantità di revisioni da pulire determinano la durata della pulizia.</p> </td>
  </tr>
  <tr>
   <td><strong>Qual è la differenza tra una revisione e una versione di pagina?</strong></td>
   <td>
    <ul>
     <li><strong>Revisione quercia: </strong> Oak organizza tutto il contenuto in una grande gerarchia ad albero che consiste di nodi e proprietà. Ogni istantanea o revisione di questa struttura del contenuto è immutabile e le modifiche alla struttura sono espresse come una sequenza di nuove revisioni. In genere, ogni modifica di contenuto attiva una nuova revisione. Vedere anche <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> Seguire il collegamento</a>.</li>
     <li><strong>Versione pagina:</strong> se si crea una versione, viene creata un’istantanea di una pagina in un momento specifico. In genere, quando si attiva una pagina viene creata una nuova versione. Per ulteriori informazioni, vedere <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">Utilizzo delle versioni di pagina</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Come velocizzare l'attività di pulizia revisioni offline se non viene completata entro 8 ore?</strong></td>
   <td>Se l'attività di revisione non viene completata entro 8 ore e i <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">thread dumps</a> rivelano che il punto di attivazione principale è <code>InMemoryCompactionMap.findEntry</code>, utilizzare il seguente parametro con lo strumento di esecuzione della quercia <strong>versioni 1.4 </strong>o successive: <code>-Dtar.PersistCompactionMap=true</code>. Il parametro <code>-Dtar.PersistCompactionMap</code> è stato rimosso nella versione 1.6 di Oak.</td>
  </tr>
 </tbody>
</table>

