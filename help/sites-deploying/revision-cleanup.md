---
title: Pulizia revisioni
description: Scopri come utilizzare la funzionalità Pulizia revisioni di Adobe Experience Manager 6.5.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
feature: Administering
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: a2d7d82e0d6729e08b464d3843a9b44bcabd154b
workflow-type: tm+mt
source-wordcount: '5696'
ht-degree: 0%

---

# Pulizia revisioni{#revision-cleanup}

## Introduzione {#introduction}

Ogni aggiornamento del repository crea una revisione del contenuto. Di conseguenza, con ogni aggiornamento, le dimensioni dell’archivio aumentano. Le precedenti revisioni devono essere pulite per liberare le risorse su disco. Questo è importante per evitare una crescita incontrollata dell’archivio. Questa funzionalità di manutenzione è denominata Pulizia revisioni. È disponibile come routine offline a partire da Adobe Experience Manager (AEM) 6.0.

Con AEM 6.3 e versioni successive, è stata introdotta una versione online di questa funzionalità chiamata Online Revision Cleanup (Pulizia delle revisioni online). Rispetto alla funzione di pulizia delle revisioni offline, in cui l&#39;istanza AEM deve essere chiusa, la funzione di pulizia delle revisioni online può essere eseguita mentre l&#39;istanza AEM è online. La funzione Pulizia revisioni online è attivata per impostazione predefinita ed è la modalità consigliata per eseguire la pulizia delle revisioni.

**Nota**: [Guarda il video](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/administration/use-online-revision-clean-up.html?lang=it) per un&#39;introduzione e per scoprire come utilizzare la funzione di pulizia delle revisioni in linea.

Il processo di pulizia delle revisioni è costituito da tre fasi: **stima**, **compattazione** e **pulizia**. La stima determina se eseguire la fase successiva (compattazione) o meno in base alla quantità di rifiuti raccolti. Durante la fase di compattazione, i segmenti e i file tar vengono riscritti lasciando fuori il contenuto inutilizzato. La fase di pulizia rimuove quindi i vecchi segmenti, inclusi eventuali rifiuti in essi contenuti. La modalità offline può in genere recuperare più spazio, perché la modalità online deve tenere conto del working set dell’AEM che impedisce la raccolta di segmenti aggiuntivi.

Per ulteriori dettagli sulla pulizia delle revisioni, consulta i seguenti collegamenti:

* [Eseguire la pulizia delle revisioni online](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [Domande frequenti sulla pulizia delle revisioni online](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [Eseguire la pulizia delle revisioni offline](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

Inoltre, puoi leggere la [documentazione ufficiale di Oak](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html).

### Quando utilizzare la pulizia revisioni in linea anziché la pulizia revisioni non in linea? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**Pulizia revisioni in linea è la modalità consigliata per eseguire la pulizia revisioni.** La pulizia delle revisioni offline deve essere utilizzata solo in casi eccezionali, ad esempio prima della migrazione al nuovo formato di archiviazione o se richiesto dall&#39;Assistenza clienti Adobe.

## Eseguire la pulizia delle revisioni online {#how-to-run-online-revision-cleanup}

La funzione di pulizia delle revisioni online è configurata per impostazione predefinita per essere eseguita automaticamente una volta al giorno sia sulle istanze AEM Author che Publish. È sufficiente definire la finestra di manutenzione durante un periodo con l’attività utente meno intensa. È possibile configurare l&#39;attività Pulizia revisioni in linea come indicato di seguito:

1. Nella finestra principale dell&#39;AEM, vai a **Strumenti - Operazioni - Dashboard - Manutenzione** o punta il browser a: `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Passa il puntatore del mouse su **Finestra di manutenzione giornaliera** e fai clic sull&#39;icona **Impostazioni**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. Immettere i valori desiderati (ricorrenza, ora di inizio e di fine) e fare clic su **Salva**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

In alternativa, se si desidera eseguire manualmente l&#39;attività di pulizia delle revisioni, è possibile:

1. Vai a **Strumenti - Operazioni - Dashboard - Manutenzione** o passa direttamente a `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. Fare clic sulla **finestra Manutenzione giornaliera**.
1. Passa il puntatore sull&#39;icona **Pulizia revisioni**.
1. Fare clic su **Esegui**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### Esecuzione della pulizia delle revisioni in linea dopo la pulizia delle revisioni non in linea {#running-online-revision-cleanup-after-offline-revision-cleanup}

Il processo di pulizia delle revisioni consente di recuperare le precedenti revisioni per generazioni. Ciò significa che ogni volta che si esegue la pulizia delle revisioni, viene creata e mantenuta una nuova generazione sul disco. Esiste tuttavia una differenza tra i due tipi di pulizia delle revisioni: la pulizia delle revisioni offline mantiene una generazione mentre la pulizia delle revisioni online ne mantiene due. Pertanto, quando si esegue la pulizia delle revisioni online **dopo** la pulizia delle revisioni offline si verifica quanto segue:

1. Dopo la prima esecuzione della pulizia della revisione online, le dimensioni dell’archivio raddoppiano. Questo accade perché ora ci sono due generazioni che vengono tenute su disco.
1. Durante le esecuzioni successive, l’archivio aumenterà temporaneamente durante la creazione della nuova generazione e quindi si stabilizzerà di nuovo alle dimensioni che aveva dopo la prima esecuzione, mentre il processo di pulizia della revisione online recupera la generazione precedente.

Inoltre, tieni presente che a seconda del tipo e del numero di commit, ogni generazione può variare in termini di dimensioni rispetto alla precedente, pertanto la dimensione finale può variare da un’esecuzione all’altra.

Per questo motivo, si consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione dell&#39;archivio inizialmente stimata.

## Modalità Di Compattazione Completa E Coda  {#full-and-tail-compaction-modes}

**AEM 6.5** introduce **due nuove modalità** per la fase **compattazione** del processo di pulizia revisioni in linea:

* La modalità **compattazione completa** riscrive tutti i segmenti e i file tar nell&#39;intero archivio. La successiva fase di pulizia può quindi rimuovere la quantità massima di oggetti inattivi dall’archivio. Poiché la compattazione completa interessa l&#39;intero archivio, richiede una quantità considerevole di risorse di sistema e tempo per il completamento. La compattazione completa corrisponde alla fase di compattazione nell&#39;AEM 6.3.
* La modalità **compattazione tail** riscrive solo i segmenti e i file tar più recenti nell&#39;archivio. I segmenti e i file tar più recenti sono quelli che sono stati aggiunti dall’ultima esecuzione della compattazione completa o di coda. La successiva fase di pulizia può quindi rimuovere solo i rifiuti contenuti nella parte recente dell’archivio. Poiché la compattazione finale interessa solo una parte dell’archivio, richiede notevolmente meno risorse di sistema e meno tempo rispetto alla compattazione completa.

Queste modalità di compattazione rappresentano un compromesso tra efficienza e consumo di risorse: mentre la compattazione di coda è meno efficace, ha anche un impatto minore sul normale funzionamento del sistema. Al contrario, la compattazione completa è più efficace, ma ha un impatto maggiore sul normale funzionamento del sistema.

AEM 6.5 introduce inoltre un meccanismo di deduplicazione dei contenuti più efficiente durante la compattazione, che riduce ulteriormente l&#39;ingombro su disco dell&#39;archivio.

I due grafici seguenti, presentano i risultati dei test di laboratorio interni che illustrano la riduzione dei tempi medi di esecuzione e l&#39;impronta media su disco nel AEM 6.5 rispetto al AEM 6.3:

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### Come configurare la compattazione completa e finale {#how-to-configure-full-and-tail-compaction}

La configurazione predefinita esegue la compattazione finale nei giorni feriali e la compattazione completa nelle domeniche. È possibile modificare la configurazione predefinita utilizzando il nuovo valore di configurazione `full.gc.days` dell&#39;`RevisionCleanupTask` [attività di manutenzione](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

Quando si configura il valore `full.gc.days`, la compattazione completa viene eseguita nei giorni definiti nel valore e la compattazione finale viene eseguita nei giorni non definiti nel valore. Ad esempio, se configuri la compattazione completa per l’esecuzione la domenica, la compattazione finale viene eseguita dal lunedì al sabato. Ad esempio, se configuri la compattazione completa in modo che venga eseguita ogni giorno della settimana, la compattazione finale non viene eseguita affatto.

Inoltre, considera che:

* **La compattazione della coda** è meno efficace e ha un impatto minore sulle normali operazioni di sistema. Esso è pertanto destinato a essere utilizzato nelle giornate lavorative.
* **La compattazione completa** è più efficace, ma ha anche un impatto maggiore sulle normali operazioni di sistema. Esso deve pertanto essere utilizzato al di fuori dei giorni lavorativi.
* La compattazione della coda e la compattazione completa devono essere programmate per l&#39;esecuzione nelle ore di minore utilizzo.

### Risoluzione dei problemi {#troubleshooting}

Quando utilizzate le nuove modalità di compattazione, tenete presente quanto segue:

* È possibile monitorare l&#39;attività di input/output (I/O), ad esempio: operazioni di I/O, CPU in attesa di I/O, dimensione coda commit. Questo aiuta a determinare se il sistema sta diventando legato all&#39;I/O e richiede un upsize.
* `RevisionCleanupTaskHealthCheck` indica lo stato di integrità complessivo di Pulizia revisioni in linea. Funziona allo stesso modo di AEM 6.3 e non distingue tra compattazione completa e di coda.
* I messaggi di registro contengono informazioni rilevanti sulle modalità di compattazione. Ad esempio, all&#39;avvio di Pulizia revisioni in linea, i messaggi di registro corrispondenti indicano la modalità di compattazione. Inoltre, in alcuni casi d&#39;angolo, il sistema ripristina la compattazione completa quando era pianificata l&#39;esecuzione di una compattazione finale e i messaggi di registro indicano questa modifica. I campioni di log riportati di seguito indicano la modalità di compattazione e il passaggio dalla coda alla compattazione completa:

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### Limitazioni note {#known-limitations}

A volte, l&#39;alternanza tra la modalità di coda e la modalità di compattazione completa ritarda il processo di pulizia. Più precisamente, l’archivio crescerà dopo una compattazione completa (raddoppia in dimensioni). Lo spazio aggiuntivo viene recuperato nella successiva compattazione finale, quando l’archivio scende al di sotto della dimensione di compattazione pre-completa. È inoltre necessario evitare l’esecuzione di attività di manutenzione parallele.

**Si consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione del repository inizialmente stimata.**

## Domande frequenti sulla pulizia delle revisioni online {#online-revision-cleanup-frequently-asked-questions}

### Considerazioni sull’aggiornamento a AEM 6.5 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>Domande </td>
   <td>Risposte</td>
  </tr>
  <tr>
   <td>Cosa devo sapere quando eseguo l’aggiornamento a AEM 6.5?</td>
   <td><p>Il formato di persistenza di TarMK cambia con AEM 6.5. Queste modifiche non richiedono un passaggio di migrazione proattivo. Gli archivi esistenti vengono sottoposti a una migrazione continua, trasparente per l’utente. Il processo di migrazione viene avviato la prima volta che l’AEM 6.5 (o strumenti correlati) accede all’archivio.</p> <p><strong>Una volta avviata la migrazione al formato di persistenza AEM 6.5, l’archivio non può essere ripristinato al precedente formato di persistenza AEM 6.3.</strong></p> </td>
  </tr>
 </tbody>
</table>

### Migrazione a Oak Segment Tar {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Domande</strong></td>
   <td><strong>Risposte</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché devo migrare l’archivio?</strong></td>
   <td><p>Nell’AEM 6.3 erano necessarie modifiche al formato di archiviazione, in particolare per migliorare le prestazioni e l’efficacia di Online Revision Cleanup. Queste modifiche non sono compatibili con le versioni precedenti e gli archivi creati con il vecchio segmento di Oak (AEM 6.2 e precedenti) devono essere migrati.</p> <p>Ulteriori vantaggi derivanti dalla modifica del formato di storage:</p>
    <ul>
     <li>Maggiore scalabilità (dimensioni ottimizzate dei segmenti).</li>
     <li><a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">Raccolta oggetti inattivi dell'archivio dati</a>.<br /> più veloce </li>
     <li>Lavoro di base per i miglioramenti futuri.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Il formato Tar precedente è ancora supportato?</strong></td>
   <td>Solo il nuovo Tar del segmento di Oak è supportato con AEM 6.3 o versione successiva.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>La migrazione dei contenuti è sempre obbligatoria?</strong></td>
   <td>Sì. A meno che tu non inizi con una nuova istanza, dovrai sempre migrare il contenuto.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>È possibile eseguire l’aggiornamento alla versione 6.3 o successiva ed eseguire la migrazione in un secondo momento (ad esempio, utilizzando un’altra finestra di manutenzione)?</strong></td>
   <td>No, come spiegato in precedenza, la migrazione dei contenuti è obbligatoria.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>È possibile evitare i tempi di inattività durante la migrazione?</strong></td>
   <td>No. Questa operazione non può essere eseguita una sola volta in un’istanza in esecuzione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede se eseguo accidentalmente il file nel formato di archivio errato?</strong></td>
   <td>Se tenti di eseguire il modulo oak-segment su un archivio oak-segment-tar (o viceversa), l'avvio non riesce e viene visualizzato il messaggio <em>IllegalStateException</em> con il formato di segmento non valido. I dati non vengono danneggiati.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Sarà necessaria una reindicizzazione degli indici di ricerca?</strong></td>
   <td>No. La migrazione da oak-segment a oak-segment-tar introduce modifiche nel formato del contenitore. I dati contenuti non sono interessati e non verranno modificati.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come calcolare al meglio lo spazio su disco previsto necessario durante e dopo la migrazione?</strong></td>
   <td>La migrazione equivale a ricreare segmentstore nel nuovo formato. Questa può essere utilizzata per stimare lo spazio su disco aggiuntivo necessario durante la migrazione. Dopo la migrazione, il vecchio archivio segmenti può essere eliminato per recuperare spazio.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come stimare al meglio la durata della migrazione?</strong></td>
   <td>È possibile migliorare notevolmente le prestazioni della migrazione se viene eseguita la <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">pulizia della revisione offline</a> prima della migrazione. Si consiglia a tutti i clienti di eseguirlo come prerequisito del processo di aggiornamento. In generale, la durata della migrazione deve essere simile alla durata dell'attività di pulizia revisioni offline, supponendo che l'attività di pulizia revisioni offline sia stata eseguita prima della migrazione.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Esecuzione della pulizia delle revisioni in linea {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Domande</strong></td>
   <td><strong>Risposte</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Con quale frequenza deve essere eseguita la pulizia delle revisioni online?</strong></td>
   <td>Una volta al giorno. Questa è la configurazione predefinita nel dashboard operazioni.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come posso configurare l'ora di inizio dell'attività di manutenzione di Online Revision Cleanup?</strong></td>
   <td>Consulta la sezione <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">Come eseguire la pulizia delle revisioni in linea</a>. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Esiste una frequenza massima che non deve essere superata per la pulizia delle revisioni online?</strong></td>
   <td>È consigliabile eseguire la pulizia delle revisioni in linea una volta al giorno, come configurato per impostazione predefinita.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono gli indicatori chiave che determinano la frequenza con cui deve essere eseguita la pulizia delle revisioni online?</strong></td>
   <td>Non è necessario determinare la frequenza in quanto la funzione di pulizia delle revisioni in linea è configurata come attività di manutenzione ed è eseguita automaticamente ogni giorno.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché la funzione Pulizia revisioni in linea non recupera spazio quando viene eseguita per la prima volta?</strong></td>
   <td>La funzione Pulizia revisioni in linea recupera le precedenti revisioni per generazioni. A ogni esecuzione della pulizia delle revisioni viene generata una nuova generazione. Solo i contenuti che sono vecchi di almeno due generazioni saranno recuperati, il che significa che alla prima esecuzione non c'è nulla da recuperare.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché la prima pulizia delle revisioni online non recupera spazio quando viene eseguita dopo la pulizia delle revisioni offline?</strong></td>
   <td><p>Offline Revision Cleanup recupera tutto tranne l'ultima generazione rispetto alle ultime due generazioni per Online Revision Cleanup. Se è presente un nuovo archivio, la funzione di pulizia delle revisioni online non recupererà spazio quando viene eseguita per la prima volta dopo la pulizia delle revisioni offline, perché non esiste una generazione abbastanza vecchia da poter essere recuperata.</p> <p>Inoltre, leggere la sezione "Esecuzione della pulizia delle revisioni online dopo la pulizia delle revisioni offline" di <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">questo capitolo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>In genere, Autore e Publish hanno finestre di pulizia delle revisioni in linea diverse?</strong></td>
   <td>Questo dipende dalle ore di ufficio e dai modelli di traffico della presenza online del cliente. Le finestre di manutenzione devono essere configurate al di fuori dei tempi di produzione principali per garantire la migliore efficacia della pulizia. Per più istanze di AEM Publish (farm TarMK), le finestre di manutenzione per la pulizia delle revisioni online devono essere scaglionate.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Esistono prerequisiti prima di eseguire la pulizia delle revisioni in linea?</strong></td>
   <td><p>La funzione di pulizia delle revisioni online è disponibile solo con le versioni AEM 6.3 e successive. Inoltre, se utilizzi una versione precedente di AEM, devi migrare al nuovo <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Tar segmento Oak</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono i fattori che determinano la durata della pulizia delle revisioni in linea?</strong></td>
   <td>I fattori sono:<br />
    <ul>
     <li>Dimensione archivio</li>
     <li>Caricare sul sistema (richieste al minuto, in particolare operazioni di scrittura)</li>
     <li>Pattern di attività (letture e scritture)</li>
     <li>Specifiche hardware (prestazioni CPU, memoria, IOPS)</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Gli autori possono ancora lavorare mentre è in esecuzione la pulizia delle revisioni online?</strong></td>
   <td>Sì, la pulizia delle revisioni in linea può gestire scritture simultanee. Tuttavia, la funzione di pulizia delle revisioni in linea funziona in modo più rapido ed efficiente senza transazioni di scrittura simultanee. L'Adobe consiglia di pianificare l'attività di manutenzione di Pulizia revisioni in linea in modo che sia relativamente silenziosa e senza traffico elevato.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono i requisiti minimi per lo spazio su disco e la memoria heap durante l'esecuzione di Online Revision Cleanup?</strong></td>
   <td><p>Lo spazio su disco viene costantemente monitorato durante la pulizia delle revisioni in linea. Se lo spazio su disco disponibile scende al di sotto di un valore critico, il processo viene annullato. Il valore critico è pari al 25% dell'attuale spazio su disco dell'archivio e non è configurabile.</p> <p><strong>L'Adobe consiglia di ridimensionare il disco almeno due o tre volte più grande della dimensione dell'archivio inizialmente stimata.</strong></p> <p>Lo spazio heap libero viene monitorato continuamente durante il processo di pulizia. Se lo spazio heap libero scende al di sotto di un valore critico, il processo viene annullato. Il valore critico viene configurato tramite org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD. Il valore predefinito è 15%.</p> <p>Recommendations per il dimensionamento heap di compattazione minimo non è separato dai consigli per il dimensionamento della memoria AEM. Generalmente: <strong>Se un'istanza AEM è sufficientemente grande da gestire i casi d'uso e il relativo payload previsto, il processo di pulizia ottiene memoria sufficiente.</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Qual è l'impatto previsto sulle prestazioni durante l'esecuzione della pulizia delle revisioni online?</strong></td>
   <td>La pulizia delle revisioni in linea è un processo in background che legge e scrive nel repository contemporaneamente alle normali operazioni di sistema. In particolare, potrebbe dover acquisire l’accesso esclusivo all’archivio per un breve periodo di tempo, impedendo ad altri thread di scrivere nell’archivio.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Per quanto tempo è prevista l'esecuzione di Pulizia revisioni online?</strong></td>
   <td>Non dovrebbero essere necessarie più di due ore per essere eseguiti in base all’Adobe più recente dei test delle prestazioni eseguiti internamente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa fare se la pulizia delle revisioni online richiede più tempo?</strong></td>
   <td>
    <ul>
     <li>Assicurati che venga eseguito ogni giorno.<br /> </li>
     <li>Assicurati che venga eseguito durante le attività minime dell’archivio configurando di conseguenza le finestre di manutenzione nel dashboard operazioni.</li>
     <li>Aumento delle risorse di sistema (CPU, memoria, I/O).</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede se la pulizia delle revisioni in linea supera le finestre di manutenzione configurate?</strong></td>
   <td>Assicurati che altre attività di manutenzione non ne ritardino l’esecuzione. Ciò potrebbe verificarsi se nella stessa finestra di manutenzione vengono eseguite più attività di manutenzione rispetto a Pulizia revisioni online. Le attività di manutenzione vengono eseguite in sequenza senza un ordine configurabile.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Perché viene ignorata la raccolta di oggetti inattivi di revisione?</strong></td>
   <td><p>Pulizia revisioni si basa su una fase di stima per decidere se c'è abbastanza immondizia da pulire. Lo stimatore confronta la dimensione corrente con la dimensione dell’archivio dopo l’ultima compattazione. Se la dimensione supera il delta configurato, viene eseguita la pulizia. Il delta di dimensione è impostato su 1 GB. Ciò significa che se la dimensione dell’archivio non è aumentata di 1 GB dall’ultima esecuzione di pulizia, la nuova iterazione di pulizia della revisione viene ignorata. </p> <p>Di seguito sono riportate le voci di registro pertinenti per la fase di stima:</p>
    <ul>
     <li>Esecuzioni di GC revisioni: <em>Il delta delle dimensioni è N% o N/N (N/N byte), pertanto è in esecuzione la compattazione</em></li>
     <li>Il catalogo globale delle revisioni <strong>non</strong> viene eseguito: <em>Il valore delta delle dimensioni è N% o N/N (N/N byte). La compattazione verrà ignorata per il momento</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>È possibile interrompere in modo sicuro la compattazione automatica se l'impatto sulle prestazioni è troppo elevato?</strong></td>
   <td>Sì. A partire da AEM 6.3, può essere arrestato in modo sicuro tramite la finestra delle attività di manutenzione all’interno del dashboard operazioni o tramite JMX.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Se l'istanza AEM viene chiusa durante un'attività di pulizia pianificata, il processo viene interrotto in modo sicuro oppure l'arresto viene bloccato fino al completamento della compattazione?</strong></td>
   <td>La pulizia delle revisioni viene interrotta e l’archivio viene chiuso in modo sicuro.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede quando il sistema si arresta durante la pulizia delle revisioni in linea?</strong></td>
   <td>In tali casi non vi è alcun rischio di danneggiamento dei dati. Gli avanzi dei rifiuti vengono eliminati da una sequenza successiva.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Qual è l'impatto della mancata esecuzione della pulizia delle revisioni online?</strong></td>
   <td>Riduzione delle prestazioni nel tempo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali revisioni vengono raccolte?</strong></td>
   <td>Per impostazione predefinita, la funzione Pulizia revisioni in linea raccoglie solo le revisioni che hanno almeno 24 ore.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede se si verificano troppe interferenze da scritture simultanee nell’archivio?</strong></td>
   <td><p>Se nel sistema è presente concorrenza in scrittura, la pulizia delle revisioni online potrebbe richiedere l'accesso esclusivo in scrittura per eseguire il commit delle modifiche al termine di un ciclo di compattazione. Il sistema entra in modalità <strong>forceCompact</strong>, come spiegato più dettagliatamente nella <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">documentazione di Oak</a>. Durante la forza di compattazione, viene acquisito un blocco di scrittura esclusivo per eseguire il commit delle modifiche senza interferire con le scritture simultanee. Per limitare l’impatto sui tempi di risposta, è possibile definire un valore di timeout. Questo valore è impostato su un minuto per impostazione predefinita, il che significa che se la compattazione forzata non viene completata entro un minuto, il processo di compattazione viene interrotto a favore di commit simultanei.</p> <p>La durata della forza compatta dipende dai seguenti fattori:</p>
    <ul>
     <li>hardware: in particolare IOPS. La durata diminuisce con più IOPS.</li>
     <li>segment store size: la durata aumenta con le dimensioni dell’archivio segmenti.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Come viene eseguita la pulizia delle revisioni online in un'istanza in standby?</strong></p> </td>
   <td><p>In una configurazione di standby a freddo, è necessario configurare solo l'istanza principale per eseguire la pulizia delle revisioni in linea. Nell’istanza in standby, non è necessario pianificare in modo specifico la pulizia delle revisioni online.</p> <p>L'operazione corrispondente in un'istanza in standby è la pulizia automatica, che corrisponde alla fase di pulizia della pulizia delle revisioni in linea. La pulizia automatica viene eseguita nell'istanza in standby dopo l'esecuzione della pulizia delle revisioni in linea nell'istanza principale.</p> <p>Le fasi di stima e compattazione non verranno eseguite su un'istanza in standby.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Offline Revision Cleanup è in grado di liberare più spazio su disco rispetto a Online Revision Cleanup?</strong></td>
   <td><p>La funzione di pulizia delle revisioni offline può rimuovere immediatamente le precedenti revisioni, mentre la funzione di pulizia delle revisioni online deve tenere conto delle precedenti revisioni a cui fa ancora riferimento lo stack dell'applicazione. Il primo può quindi rimuovere la spazzatura in modo più aggressivo rispetto al secondo, dove l’effetto viene ammortizzato nel corso di alcuni cicli di raccolta della spazzatura.</p> <p>Inoltre, leggere la sezione "Esecuzione della pulizia delle revisioni online dopo la pulizia delle revisioni offline" di <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">questo capitolo</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Considerazioni sulle operazioni dei file mappati in memoria?</td>
   <td>
    <ul>
     <li><strong>Negli ambienti Windows</strong>, l'accesso regolare ai file è sempre imposto, pertanto l'accesso mappato alla memoria non viene utilizzato. Come consiglio generale, tutta la RAM disponibile deve essere allocata all’heap e la dimensione segmentCache deve essere aumentata. Aumenta segmentCache aggiungendo l’opzione segmentCache.size a org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config (ad esempio, segmentCache.size=20480). Ricordarsi di lasciare fuori un po' di RAM per il sistema operativo e altri processi.</li>
     <li><strong>In ambienti non Windows</strong>, aumentare le dimensioni della memoria fisica per migliorare il mapping della memoria dell'archivio.</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Monitoraggio della pulizia delle revisioni online {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Cosa deve essere monitorato durante la pulizia delle revisioni online?</strong></td>
   <td>
    <ul>
     <li>Lo spazio su disco deve essere monitorato quando è abilitata la pulizia delle revisioni in linea. La pulizia non viene eseguita o termina in modo preventivo quando lo spazio su disco è insufficiente.</li>
     <li>Controllare i registri per l'ora di completamento della pulizia delle revisioni in linea. Non dovrebbe richiedere più di 2 ore.</li>
     <li>Numero di punti di controllo. Se durante l’esecuzione della compattazione sono presenti più di 3 punti di controllo, si consiglia di pulirli.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come verificare se la pulizia delle revisioni in linea è stata completata correttamente?</strong></td>
   <td><p>Per verificare se la pulizia delle revisioni in linea è stata completata correttamente, controllare i registri.</p> <p>Ad esempio, "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>" indica che il passaggio di compattazione è stato completato correttamente a meno che non sia preceduto dal messaggio "<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>", il che significa che è stato eseguito un carico concorrente eccessivo.</p> <p>È presente un messaggio "<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>" per il completamento corretto del passaggio di pulizia.</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>Dove è possibile trovare le statistiche delle ultime esecuzioni di pulizia delle revisioni online?</strong></td>
   <td><p>Statistiche relative a stato, avanzamento e stato sono esposte tramite JMX (<code>SegmentRevisionGarbageCollection</code> MBean). Per ulteriori dettagli su <code>SegmentRevisionGarbageCollection</code> MBean, leggere il <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">seguente paragrafo</a>.</p> <p>È possibile tenere traccia dell'avanzamento tramite l'attributo <code>EstimatedRevisionGCCompletion</code> del <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>È possibile ottenere un riferimento di MBean utilizzando <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>Le statistiche sono disponibili solo dall'ultimo avvio del sistema. <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank">È possibile utilizzare strumenti di monitoraggio esterni per mantenere i dati oltre il tempo di attività dell'AEM</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali sono le voci di registro rilevanti?</strong></td>
   <td>
    <ul>
     <li>Pulizia revisioni online avviata/interrotta
      <ul>
       <li>La pulizia delle revisioni in linea è composta da tre fasi: stima, compattazione e pulizia. La stima può forzare la compattazione e la pulizia a saltare se l’archivio non contiene abbastanza oggetti inattivi. Nella versione più recente di AEM, il messaggio "<code>TarMK GC #{}: estimation started</code>" indica l'inizio della stima, "<code>TarMK GC #{}: compaction started, strategy={}</code>" indica l'inizio della compattazione e "T<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>" indica l'inizio della pulizia.</li>
      </ul> </li>
     <li>Spazio su disco ottenuto dalla pulizia della revisione
      <ul>
       <li>Lo spazio viene recuperato solo al termine della fase di pulizia. Il completamento della fase di pulizia è contrassegnato dal messaggio di registro "T<code>arMK GC #{}: cleanup completed in {} ({} ms</code>". Le dimensioni di pulizia di Post sono {} ({} byte) e lo spazio recuperato {} ({} byte). Il peso/profondità della mappa di compattazione è {}/{} ({} byte/{})."</li>
      </ul> </li>
     <li>Si è verificato un problema durante la pulizia della revisione
      <ul>
       <li>Esistono molte condizioni di errore, tutte sono contrassegnate da messaggi di registro WARN o ERROR che iniziano con "TarMK GC".</li>
      </ul> </li>
    </ul> <p>Inoltre, consulta la sezione <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Risoluzione dei problemi in base ai messaggi di errore</a> di seguito.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come verificare quanto spazio è stato recuperato al termine della pulizia delle revisioni online?</strong></td>
   <td>Nel registro alla fine del ciclo di pulizia è presente un messaggio: "<code>TarMK GC #3: cleanup completed</code>" che include le dimensioni dell'archivio e la quantità di rifiuti recuperati.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come verificare l'integrità dell'archivio al termine della pulizia delle revisioni in linea?</strong></td>
   <td><p>Dopo la pulizia delle revisioni in linea non è necessario eseguire un controllo dell'integrità dell'archivio. </p> <p>Tuttavia, è possibile eseguire le azioni seguenti per controllare lo stato dell’archivio dopo la pulizia:</p>
    <ul>
     <li>Un archivio <a href="/help/sites-deploying/consistency-check.md" target="_blank">controllo trasversale</a></li>
     <li>Utilizza lo strumento oak-run al termine del processo di pulizia per verificare la presenza di incoerenze. Per ulteriori informazioni su come eseguire questa operazione, consulta la <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">documentazione di Apache.</a> Per eseguire lo strumento non è necessario arrestare AEM.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Come rilevare se la pulizia delle revisioni online non è riuscita e quali sono i passaggi per ripristinare?</strong></td>
   <td>Le condizioni di errore sono contrassegnate dai messaggi di registro WARN o ERROR che iniziano con "TarMK GC". Inoltre, consulta la sezione <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">Risoluzione dei problemi in base ai messaggi di errore</a> di seguito.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Quali informazioni sono esposte nel controllo dello stato di pulizia delle revisioni? Come e quando contribuiscono ai livelli di stato con codice a colori? </strong></td>
   <td><p>Il controllo stato di pulizia revisioni fa parte del <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">dashboard operazioni</a>.<br /> </p> <p>Lo stato è <strong>VERDE</strong> se l'ultima esecuzione dell'attività di manutenzione di Online Revision Cleanup è stata completata correttamente.</p> <p>È <strong>GIALLO</strong> se l'attività di manutenzione di Online Revision Cleanup è stata annullata una volta.<br /> </p> <p>È <strong>ROSSO</strong> se l'attività di manutenzione di Pulizia revisioni in linea è stata annullata tre volte di seguito. <strong>In questo caso è necessaria l'interazione manuale</strong> oppure è probabile che la pulizia delle revisioni in linea non riesca più. Per ulteriori informazioni, leggere la sezione <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">Risoluzione dei problemi</a> di seguito.<br /> </p> <p>Inoltre, lo stato di Verifica stato viene reimpostato dopo il riavvio del sistema. Pertanto, un'istanza appena riavviata viene visualizzata in verde sul controllo di integrità della pulizia delle revisioni.  <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank">È possibile utilizzare strumenti di monitoraggio esterni per mantenere i dati oltre il tempo di attività dell'AEM</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Come monitorare la pulizia automatica in un'istanza in standby?</strong></p> </td>
   <td><p>Stato, avanzamento e statistiche vengono esposti tramite JMX utilizzando <code>SegmentRevisionGarbageCollection</code> MBean. Consulta anche la <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">documentazione di Oak</a>. </p> <p>È possibile ottenere un riferimento di MBean utilizzando <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>Le statistiche sono disponibili solo dall'ultimo avvio del sistema.  <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-external-services" target="_blank">È possibile utilizzare strumenti di monitoraggio esterni per mantenere i dati oltre il tempo di attività dell'AEM</a>.</p> <p>I file di registro possono essere utilizzati anche per controllare lo stato, l'avanzamento e le statistiche della pulizia automatica.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>Cosa deve essere monitorato durante la pulizia automatica in un’istanza in standby?</strong></p> </td>
   <td>
    <ul>
     <li>Lo spazio su disco deve essere monitorato durante l'esecuzione della pulizia automatica.</li>
     <li>Tempo di completamento (tramite i registri) per garantire che non vengano superate 2 ore.</li>
     <li>Dimensione dell’archivio segmenti dopo l’esecuzione della pulizia automatica. La dimensione dell’archivio segmenti nell’istanza in standby deve essere approssimativamente uguale a quella nell’istanza primaria.</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Risoluzione dei problemi di pulizia delle revisioni online {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Qual è il peggio che può accadere se non si esegue Pulizia revisioni online?</strong></td>
   <td>Lo spazio su disco dell’istanza AEM è esaurito, con conseguenti interruzioni della produzione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Il traffico elevato degli utenti è problematico per l’esecuzione di Pulizia revisioni online in un’istanza di pubblicazione?</strong></td>
   <td>Il traffico elevato degli utenti influisce sul completamento o meno della fase di compattazione.<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>In base alla verifica dello stato e alle voci del registro, la pulizia delle revisioni in linea non è stata completata tre volte di seguito. Cosa è necessario per completare correttamente la pulizia delle revisioni online?</strong></td>
   <td>Puoi eseguire diversi passaggi per trovare e risolvere il problema:<br />
    <ul>
     <li>Controllare innanzitutto le voci del registro<br /> </li>
     <li>A seconda delle informazioni contenute nei registri, adotta le misure appropriate:
      <ul>
       <li>Se i registri mostrano cinque cicli di compattazione saltati e un timeout sul ciclo <code>forceCompact</code>, pianificare la finestra di manutenzione in modo che non intervenga quando la quantità di scritture dell'archivio è bassa. È possibile controllare le scritture del repository nello strumento di monitoraggio delle metriche del repository all'indirizzo <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>Se la pulizia viene interrotta alla fine della finestra di manutenzione, assicurarsi che la configurazione della finestra di manutenzione nell'interfaccia utente Attività di manutenzione sia sufficientemente grande</li>
       <li>Se la memoria heap disponibile non è sufficiente, verificare che l'istanza disponga di memoria sufficiente.</li>
       <li>In caso di reazione tardiva, l’archivio segmenti potrebbe crescere troppo per consentire il completamento della pulizia delle revisioni online anche all’interno di una finestra di manutenzione più lunga. Ad esempio, se nell’ultima settimana non è stata completata correttamente la pulizia delle revisioni online, si consiglia di pianificare una manutenzione offline e di eseguire la pulizia delle revisioni offline per riportare segmenstore a una dimensione gestibile.</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa deve essere fatto quando è attivato l’avviso del controllo di integrità?</strong></td>
   <td>Cfr. il punto precedente.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa succede se la pulizia delle revisioni in linea non viene eseguita correttamente durante la finestra di manutenzione pianificata?</strong></td>
   <td>La pulizia delle revisioni online è stata annullata e gli avanzi rimossi. Si riavvia alla successiva programmazione della finestra di manutenzione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cosa sta causando la registrazione di <code>SegmentNotFoundException</code> istanze in <code>error.log</code> e come posso eseguire il ripristino?</strong></td>
   <td><p><code>SegmentNotFoundException</code> viene registrato da TarMK quando tenta di accedere a un'unità di archiviazione (un segmento) che non è in grado di trovare. Esistono tre scenari che potrebbero causare il problema:</p>
    <ol>
     <li>Applicazione che aggira i meccanismi di accesso consigliati (come Sling e API JCR) e utilizza un’API/SPI di livello inferiore per accedere all’archivio e quindi supera il tempo di conservazione di un segmento. In altre parole, mantiene un riferimento a un’entità oltre il tempo di conservazione consentito dalla funzione di pulizia delle revisioni online (24 ore per impostazione predefinita). Questo caso è transitorio e non causa il danneggiamento dei dati. Per il ripristino, è necessario utilizzare lo strumento oak-run per confermare la natura transitoria dell’eccezione (il controllo oak-run non deve segnalare errori). A questo scopo, l’istanza deve essere messa offline e riavviata in seguito.</li>
     <li>Un evento esterno ha causato il danneggiamento dei dati sul disco. Può trattarsi di un errore del disco, di spazio insufficiente o di una modifica accidentale dei file di dati richiesti. In questo caso, l’istanza deve essere messa offline e ripristinata utilizzando il controllo oak-run. Per ulteriori dettagli su come eseguire il controllo oak-run, leggi la seguente <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">documentazione di Apache</a>.</li>
     <li>Risolvi tutte le altre occorrenze tramite <a href="https://experienceleague.adobe.com/it?support-solution=General&amp;support-tab=homehome?lang=it#support" target="_blank">l'Assistenza clienti Adobe</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Risoluzione Dei Problemi In Base Ai Messaggi Di Errore {#troubleshooting-based-on-error-messages}

Il file error.log è dettagliato se si verificano problemi durante il processo di pulizia delle revisioni online. La seguente matrice mira a spiegare i messaggi più comuni e a fornire possibili soluzioni:

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message does not mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Fase</th>
    <th>Messaggi del registro</th>
    <th>Spiegazione</th>
    <th>Passaggi successivi</th>
  </tr>  
  <tr>
    <td>Stima</td>
    <td>#2 GC di TarMK: stima ignorata perché la compattazione è in pausa.</td>
    <td>La fase di stima viene ignorata quando la compattazione è disabilitata sul sistema dalla configurazione.</td>
    <td>Abilita la pulizia delle revisioni online.</td>
  </td>
  </tr>
  <tr>
    <td>N/D</td>
    <td>#2 GC di TarMK: stima interrotta: ${REASON}. Compattazione ignorata.</td>
    <td>La fase di stima terminò prematuramente. Alcuni esempi di eventi che potrebbero interrompere la fase di stima: memoria o spazio su disco insufficiente nel sistema host.</td>
    <td>Dipende dal motivo specificato.</td>
  </td>
  </tr>
  <tr>
    <td>Compattazione</td>
    <td>#2 GC di TarMK: compattazione sospesa.</td>
    <td>Fintanto che la fase di compattazione è sospesa per configurazione, non si esegue né la fase di stima né quella di compattazione.</td>
    <td>Abilita la pulizia delle revisioni online.</td>
  </td>
  </tr>
   <tr>
    <td>N/D</td>
    <td>#2 GC TarMK: compattazione annullata: ${REASON}.</td>
    <td>La fase di compattazione terminò prematuramente. Alcuni esempi di eventi che potrebbero interrompere la fase di compattazione: memoria o spazio su disco insufficiente nel sistema host. Inoltre, la compattazione può essere annullata anche chiudendo il sistema o annullandolo esplicitamente tramite interfacce amministrative come la finestra Manutenzione all'interno del dashboard operazioni.</td>
    <td>Dipende dal motivo specificato.</td>
  </td>
  </tr>
  <tr>
    <td>N/D</td>
    <td>#2 GC di TarMK: compattazione non riuscita in 32,902 min (1974140 ms), dopo 5 cicli.</td>
    <td>Questo messaggio non indica che si è verificato un errore irreversibile, ma solo che la compattazione è stata terminata dopo alcuni tentativi. Leggi anche il <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">seguente paragrafo.</a></td>
    <td>Leggi la <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">documentazione di Oak</a> e l'ultima domanda della sezione Esecuzione della pulizia delle revisioni online.</a></td>
  </td>
  </tr>
  <tr>
    <td>Pulizia</td>
    <td>#2 GC di TarMK: pulizia interrotta.</td>
    <td>La pulizia è stata annullata arrestando l’archivio. Non si prevede alcun impatto sulla coerenza. Inoltre, è molto probabile che lo spazio su disco non venga recuperato completamente. Verrà recuperato durante il prossimo ciclo di pulizia della revisione.</td>
    <td>Ricercare il motivo per cui l'archivio è stato arrestato e in futuro cercare di evitare di arrestarlo durante le finestre di manutenzione.</td>
  </td>
  </tr>
  </tbody>
</table>

## Eseguire la pulizia delle revisioni offline {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>Utilizza una versione dello strumento eseguita da Oak con un numero di versione (principale e secondario) corrispondente alla versione di base di Oak dell’installazione AEM. Ad esempio, se l’istanza AEM dispone della versione 1.22.x di Oak Core, utilizza la versione più recente dello strumento Oak-run 1.22.x.

L&#39;Adobe fornisce uno strumento denominato **Oak-run** per eseguire la pulizia delle revisioni. Può essere scaricato nella seguente posizione:

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

Lo strumento è un file jar eseguibile che può essere eseguito manualmente per compattare l’archivio. Il processo viene chiamato pulizia revisione offline perché è necessario chiudere l&#39;archivio per eseguire correttamente lo strumento. Assicurati di pianificare la pulizia in base alla finestra di manutenzione.

Per suggerimenti su come migliorare le prestazioni del processo di pulizia, vedere [Aumento delle prestazioni di pulizia revisioni non in linea](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>È inoltre possibile cancellare i punti di controllo precedenti prima che venga eseguita la manutenzione (passaggi 2 e 3 nella procedura seguente). Questa opzione è consigliata solo per le istanze che hanno più di 100 punti di controllo.

1. Assicurati sempre di avere un backup recente dell’istanza AEM.

   Chiudi AEM.

1. (Facoltativo) Usate lo strumento per trovare i punti di controllo precedenti:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. (Facoltativo) Quindi, elimina i punti di controllo senza riferimento:

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. Eseguire la compattazione e attenderne il completamento:

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### Aumento delle prestazioni della pulizia delle revisioni offline {#increasing-the-performance-of-offline-revision-cleanup}

Lo strumento oak-run introduce diverse funzioni che mirano ad aumentare le prestazioni del processo di pulizia delle revisioni e a ridurre il più possibile la finestra di manutenzione.

L’elenco include diversi parametri della riga di comando, come descritto di seguito:

* **-mmap.** È possibile impostarlo come true o false. Se è impostato su true, viene utilizzato l&#39;accesso mappato alla memoria. Se impostato su false, viene utilizzato l’accesso ai file. Se non specificato, l&#39;accesso mappato alla memoria viene utilizzato su sistemi a 64 bit e l&#39;accesso ai file viene utilizzato su sistemi a 32 bit. In Windows, l’accesso regolare ai file viene sempre applicato e questa opzione viene ignorata. **Questo parametro ha sostituito il parametro -Dtar.memoryMapped.**

* **-Dupdate.limit**. Definisce la soglia per lo scaricamento su disco di una transazione temporanea. Il valore predefinito è 10000.

* **-Dcompress-interval**. Numero di voci di mappa di compattazione da mantenere fino alla compressione della mappa corrente. Il valore predefinito è 1000000. Se è disponibile una quantità sufficiente di memoria heap, è necessario aumentare questo valore a un numero ancora più alto per una velocità effettiva più rapida. **Questo parametro è stato rimosso in Oak versione 1.6 e non ha alcun effetto.**

* **-Dcompaction-progress-log**. Numero di nodi compattati registrati. Il valore predefinito è 150000, il che significa che durante l&#39;operazione vengono registrati i primi nodi compattati 150000. Utilizzalo con il parametro successivo documentato di seguito.

* **-Dtar.PersistCompactionMap.** Impostare questo parametro su true per utilizzare spazio su disco anziché memoria heap per la persistenza della mappa di compattazione. Richiede lo strumento oak-run **versioni 1.4** e successive. Per ulteriori dettagli, vedi la domanda 3 nella sezione [Domande frequenti sulla pulizia delle revisioni offline](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions). **Questo parametro è stato rimosso in Oak versione 1.6 e non ha alcun effetto.**

* **—forza.** Forza la compattazione e ignora una versione dell&#39;archivio segmenti non corrispondente.

>[!CAUTION]
>
>Se si utilizza il parametro `--force`, l&#39;archivio segmenti viene aggiornato alla versione più recente, incompatibile con le versioni precedenti di Oak. Inoltre, considera che non è possibile effettuare alcun downgrade. In genere, questi parametri devono essere utilizzati con cautela e solo se si è esperti di come utilizzarli.

Un esempio dei parametri in uso:

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### Metodi aggiuntivi per attivare la pulizia delle revisioni {#additional-methods-of-triggering-revision-cleanup}

Oltre ai metodi descritti in precedenza, puoi anche attivare il meccanismo di pulizia delle revisioni utilizzando la console JMX come segue:

1. Apri la console JMX da [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. Fai clic sull&#39;**RevisionGarbageCollection** MBean.
1. Nella finestra successiva, fai clic su **startRevisionGC()** e quindi su **Invoke** per avviare il processo Revision Garbage Collection.

### Domande frequenti sulla pulizia delle revisioni offline {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>Quali sono i fattori che determinano la durata della pulizia delle revisioni offline?</strong></td>
   <td><p>La dimensione dell’archivio e il numero di revisioni da pulire determinano la durata della pulizia.</p> </td>
  </tr>
  <tr>
   <td><strong>Qual è la differenza tra una revisione e una versione di pagina?</strong></td>
   <td>
    <ul>
     <li><strong>Revisione Oak:</strong> Oak organizza tutto il contenuto in una grande gerarchia ad albero costituita da nodi e proprietà. Ogni snapshot o revisione di questa struttura di contenuto non è modificabile e le modifiche alla struttura vengono espresse come una sequenza di nuove revisioni. In genere, ogni modifica del contenuto attiva una nuova revisione. Vedi anche <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> Segui collegamento</a>.</li>
     <li><strong>Versione pagina:</strong> Il controllo delle versioni crea uno "snapshot" di una pagina in un momento specifico. In genere, quando viene attivata una pagina, viene creata una nuova versione. Per ulteriori informazioni, vedere <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">Utilizzo delle versioni delle pagine</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Come velocizzare l'attività Offline Revision Cleanup se non viene completata entro 8 ore?</strong></td>
   <td>Se l'attività di revisione non viene completata entro 8 ore e le <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">immagini thread</a> rivelano che il punto attivo principale è <code>InMemoryCompactionMap.findEntry</code>, utilizzare il parametro seguente con lo strumento oak-run <strong>versioni 1.4 </strong>o successive: <code>-Dtar.PersistCompactionMap=true</code>. Il parametro <code>-Dtar.PersistCompactionMap</code> è stato rimosso in Oak versione 1.6.</td>
  </tr>
 </tbody>
</table>
