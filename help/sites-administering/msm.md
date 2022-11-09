---
title: "Riutilizzo del contenuto: Multi-Site Manager e Live Copy"
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: Scopri come riutilizzare i contenuti con Live Copy e Multi Site Manager.
seo-description: Learn about reusing content with Live Copies and the Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 34%

---

# Riutilizzo del contenuto: Multi-Site Manager e Live Copy{#reusing-content-multi-site-manager-and-live-copy}

Multi Site Manager (MSM) consente di utilizzare lo stesso contenuto del sito in più posizioni. Per ottenere questo risultato, MSM utilizza la funzionalità Live Copy:

* Con MSM è possibile:

   * Creare contenuto una volta e poi
   * Copia il contenuto in altre aree e riutilizzalo in ([Live Copy](#live-copies)) dello stesso sito o di altri siti.

* MSM mantiene quindi le relazioni (live) tra il contenuto sorgente e le relative Live Copy in modo che:

   * Quando apporti modifiche al contenuto sorgente, le copie sorgente e live vengono sincronizzate (per applicare anche queste modifiche alle Live Copy).
   * È possibile apportare modifiche al contenuto delle Live Copy scollegando la relazione live per le singole sottopagine e/o componenti. In questo modo, le modifiche all’origine non verranno più applicate alla Live Copy.

Queste pagine e le seguenti trattano i problemi correlati:

* [Creazione e sincronizzazione di Live Copy](/help/sites-administering/msm-livecopy.md)
* [Panoramica Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurazione della sincronizzazione di una Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitti di rollout MSM](/help/sites-administering/msm-rollout-conflicts.md)
* [Best practice MSM](/help/sites-administering/msm-best-practices.md)

## Scenari possibili {#possible-scenarios}

Esistono molti casi d’uso per MSM e Live Copy, alcuni scenari includono:

* **Multinazionali: dall’azienda globale a quella locale**

   Un caso d’uso tipico supportato da MSM è quello di riutilizzare i contenuti in diversi siti multinazionali nella stessa lingua. Questo consente il riutilizzo dei contenuti di base, consentendo al contempo l’utilizzo di varianti nazionali.

   Ad esempio, la sezione inglese dell’esempio di sito di riferimento We.Retail viene creata per i clienti degli Stati Uniti. La maggior parte dei contenuti di questo sito può essere utilizzata anche per altri siti We.Retail che si rivolgono a clienti di lingua inglese di diversi paesi e culture. Il contenuto principale rimane lo stesso in tutti i siti, mentre è possibile apportare modifiche regionali.

   La seguente struttura può essere utilizzata per i siti di Stati Uniti, Regno Unito, Canada e Australia:

   ```xml
   /content
       |- we.retail
           |- language-masters
               |- en
       |- we.retail
           |- us
               |- en
       |- we.retail
           |- gb
               |- en
       |- we.retail
           |- ca
               |- en
       |- we.retail
           |- au
               |- en
   ```

   >[!NOTE]
   >
   >MSM non traduce il contenuto. Viene utilizzato per creare la struttura richiesta e distribuire il contenuto.
   >
   >
   >Vedi [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) per estendere un esempio di questo tipo.

* **Nazionale: dalla sede principale alle succursali regionali**

   In alternativa, un&#39;azienda con una rete di dealer potrebbe volere siti web separati per i loro singoli dealer - ciascuno è una variazione del sito principale fornito dalla sede centrale. Potrebbe trattarsi di una singola azienda con più uffici regionali o di un sistema di franchising nazionale composto da un franchisor centrale e da più affiliati locali.

   La sede centrale può fornire le informazioni di base, mentre gli enti regionali possono aggiungere informazioni locali, quali i dati di contatto, gli orari di apertura e gli eventi.

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **Più versioni**

   Oppure è possibile utilizzare MSM per creare versioni di un sottoramo specifico. Ad esempio, un sottosito di supporto contenente i dettagli delle diverse versioni di un prodotto specifico, in cui le informazioni di base rimangono costanti e devono essere modificate solo le funzioni aggiornate:

   ```xml
   /content
       |- support
           |- product X
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!NOTE]
   >
   >In questo scenario c&#39;è sempre la questione se fare una copia diretta o utilizzare copie dal vivo.
   >
   >Esiste un equilibrio tra:
   >
   >  * Quanto contenuto di base dovrà essere aggiornato su più versioni.
   >
   >Contro:
   >
   >  * Quanto delle singole copie dovrà essere regolato.


## MSM dall’interfaccia utente {#msm-from-the-ui}

MSM è direttamente accessibile nell’interfaccia utente utilizzando diverse opzioni dalla console appropriata. Per fornire un’introduzione, vengono elencate le posizioni principali:

* **Crea sito** (**Sites**)

   * MSM consente di gestire più siti web che condividono contenuti comuni; ad esempio, i siti web sono spesso disponibili per il pubblico internazionale in modo tale che la maggior parte dei contenuti sia comune in tutti i paesi, con un sottoinsieme dei contenuti specifici per ogni singolo paese. MSM consente di [crea Live Copy che aggiorna automaticamente uno o più siti in base al sito di origine](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Questo consente anche di applicare una struttura di base comune, utilizzare i contenuti comuni tra più siti, mantenere un aspetto comune e ottimizzare gli sforzi per gestire i contenuti che differiscono effettivamente tra i siti.
   * Richiede una configurazione blueprint predefinita per specificare la sorgente.
   * Crea una Live Copy dell’origine (predefinita).
   * Fornisce all’utente il pulsante di **Rollout**.

* **Crea Live Copy** (**Sites**)

   * MSM consente di [creare una Live Copy ad hoc (una tantum) di una singola pagina o sottosezione di un sito web](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page); ad esempio, duplicare un ramo secondario per fornire informazioni su una versione nuova/aggiornata di un prodotto.
   * Crea una Live Copy ad-hoc (non è richiesta alcuna configurazione blueprint).
   * Può essere utilizzato per creare (immediatamente) una Live Copy di qualsiasi pagina/ramo.
   * Richiede **Sincronizza** (non fornisce il pulsante di **Rollout**).

* **Visualizza proprietà** (**Sites**)

   * Se appropriato, questa opzione ti aiuta a: [monitorare la Live Copy](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) fornendo informazioni sui relativi **Live Copy** y o **Blueprint**.

* **Riferimenti** (**Sites**)

   * La barra [Riferimenti](/help/sites-authoring/basic-handling.md#references) fornisce informazioni sulle **Live Copy** insieme all’accesso alle azioni appropriate.

* **Panoramica delle Live Copy** (**Sites**)

   * Questa console consente di: [visualizzare e gestire il blueprint e le relative Live Copy](/help/sites-administering/msm-livecopy-overview.md).

* **Blueprint** (**Strumenti** - **Sites**)

   * Questa console consente di [creare e gestire le configurazioni della blueprint](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>Gli aspetti della funzionalità MSM sono utilizzati in diverse altre funzioni di AEM (ad esempio, Lanci, Catalogo); in questi casi la Live Copy è gestita da tale funzione.

### Termini utilizzati {#terms-used}

Come introduzione, la seguente tabella fornisce una panoramica dei termini principali utilizzati con MSM; le sezioni e le pagine successive descrivono in dettaglio:

<table>
 <tbody>
  <tr>
   <td><strong>Termine</strong></td>
   <td><strong>Definizione</strong></td>
   <td><strong>Ulteriori dettagli</strong></td>
  </tr>
  <tr>
   <td><strong>Sorgente</strong></td>
   <td>Le pagine originali.</td>
   <td>Sinonimo di pagine blueprint e/o blueprint.</td>
  </tr>
  <tr>
   <td><strong>Live Copy </strong></td>
   <td>La copia (della sorgente), gestita dalle azioni di sincronizzazione definite dalle configurazioni di rollout. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configurazione Live Copy</strong></td>
   <td>Definizione dei dettagli di configurazione per una Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Relazione Live</strong><br /> </td>
   <td>definizione efficace dell'eredità di una determinata risorsa; le connessioni tra la sorgente e le Live Copy.<br /> </td>
   <td>Garantisce che le modifiche all’origine possano essere sincronizzate con la Live Copy.</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>Sinonimo di Origine.</td>
   <td>Può essere definito da una configurazione blueprint.</td>
  </tr>
  <tr>
   <td><strong>Configurazione Blueprint</strong></td>
   <td>Configurazione predefinita che specifica un percorso origine.</td>
   <td>Quando si fa riferimento a una pagina blueprint in una configurazione blueprint, diventa disponibile il comando Rollout.</td>
  </tr>
  <tr>
   <td><strong>Sincronizzazione</strong></td>
   <td>Termine generico per la sincronizzazione del contenuto tra l'origine e le Live Copy (sia per <strong>Rollout</strong> e <strong>Sincronizza</strong>).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Rollout</strong><br /> </td>
   <td>Sincronizza dalla sorgente alla Live Copy.<br /> Può essere attivato da un autore (in una pagina blueprint) o da un evento di sistema (come definito dalla configurazione di rollout).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configurazione rollout</strong></td>
   <td>Regole che determinano le proprietà da sincronizzare, come e quando.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Sincronizza</strong></td>
   <td>Una richiesta manuale di sincronizzazione, effettuata dalle pagine Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Ereditarietà</strong></td>
   <td>Una pagina/componente Live Copy eredita il contenuto dalla pagina/componente sorgente quando si verifica la sincronizzazione.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Sospendi</strong></td>
   <td>Rimuove temporaneamente la relazione live tra una Live Copy e la relativa pagina blueprint.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Stacca</strong></td>
   <td>Rimuove definitivamente la relazione live tra una Live Copy e la relativa pagina blueprint.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Ripristina</strong></td>
   <td><p>Reimposta una pagina Live Copy su:</p>
    <ul>
     <li>Rimuovere tutte le ereditarietà annullate e<br /> </li>
     <li>Restituire alla pagina lo stesso stato della pagina sorgente.</li>
    </ul> <p>La reimpostazione influisce su tutte le modifiche apportate alle proprietà della pagina, al sistema di paragrafi e ai componenti.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Superficiale</strong></td>
   <td>Una Live Copy di una singola pagina.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Profondo</strong></td>
   <td>Una Live Copy di una pagina, insieme alle relative pagine figlie.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vedi [Panoramica dell’API Java](/help/sites-developing/extending-msm.md#overview-of-the-java-api) per i nomi degli oggetti.

## Live Copy {#live-copies}

Una Live Copy MSM è una copia del contenuto specifico del sito per il quale viene mantenuta una relazione live con l’origine originale:

* La Live Copy eredita il contenuto dalla relativa origine.
* La sincronizzazione esegue il trasferimento effettivo del contenuto quando vengono apportate modifiche al sorgente.
* Una Live Copy può essere considerata come:

   * Shallow: una singola pagina
   * Deep: la pagina, insieme alle relative pagine figlie

* Le regole di sincronizzazione, denominate configurazioni di rollout, determinano le proprietà sincronizzate e quando si verifica la sincronizzazione.

Nell&#39;esempio precedente, `/content/we-retail/language-masters/en` è il sito master globale in inglese. Per riutilizzare il contenuto di questo sito, vengono create Live Copy MSM:

* Il contenuto seguente `/content/we-retail/language-masters/en` è la sorgente.

* Di seguito il contenuto `/content/we-retail/language-masters/en` viene copiato sotto il `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en`e `/content/we-retail/au/en` nodi. Queste sono le Live Copy.

* Gli autori possono apportare modifiche alle pagine sottostanti `/content/we-retail/language-masters/en`.
* Quando viene attivato, MSM sincronizza queste modifiche con le Live Copy.

### Live Copy - Composizione {#live-copies-composition}

>[!NOTE]
>
>I diagrammi e le descrizioni di questa sezione rappresentano istantanee di potenziali Live Copy. Non sono complete, ma forniscono una panoramica per evidenziare caratteristiche specifiche.

Quando crei inizialmente una Live Copy, le pagine sorgente selezionate vengono riportate in 1:1 in Live Copy. In seguito, è possibile creare nuove risorse (pagine e/o paragrafi) direttamente all’interno della Live Copy, pertanto è utile essere consapevoli di queste varianti e del loro impatto sulla sincronizzazione. Le possibili composizioni includono:

* [Live Copy con pagine non Live Copy](#live-copy-with-non-live-copy-pages)
* [Live Copy nidificate](#nested-live-copies)

La forma di base della Live Copy è:

* Pagine Live Copy che riflettono le pagine sorgente selezionate su base 1:1.
* Una definizione di configurazione.
* Una relazione live definita per ogni risorsa:

   * Collega la risorsa Live Copy alla relativa blueprint/sorgente.
   * Sono utilizzate per la realizzazione di ereditarietà e rollout.

* Le modifiche possono essere [sincronizzate](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) in base ai requisiti.

![chlimage_1-367](assets/chlimage_1-367.png)

#### Live Copy con pagine non Live Copy {#live-copy-with-non-live-copy-pages}

Quando crei una Live Copy in AEM puoi visualizzare e navigare attraverso il ramo della Live Copy e utilizzare le normali funzionalità AEM sul ramo della Live Copy. Questo significa che puoi creare (o un processo) nuove risorse (pagine e/o paragrafi) all’interno del ramo Live Copy (ad esempio `myCanadaOnlyProduct`).

* Tali risorse non hanno alcuna relazione live con le pagine sorgente/blueprint e non sono sincronizzate.
* Si possono verificare scenari che MSM gestisce come casi speciali. Ad esempio, quando crei una pagina con la stessa posizione e lo stesso nome nei rami sorgente/blueprint e Live Copy. Per tali situazioni vedi [Conflitti di rollout MSM](/help/sites-administering/msm-rollout-conflicts.md) per ulteriori informazioni.

![chlimage_1-368](assets/chlimage_1-368.png)

#### Live Copy nidificate {#nested-live-copies}

Quando crei un [nuova pagina all’interno di una Live Copy esistente](#live-copy-with-non-live-copy-pages) questa nuova pagina può anche essere impostata come Live Copy di un modello diverso. Questa è nota come Live Copy nidificata, in cui il comportamento della seconda Live Copy (interna) è interessato dalla prima Live Copy (esterna) nel modo seguente:

* Un rollout profondo attivato per la Live Copy di livello superiore può essere continuato nella Live Copy nidificata (ad esempio, se il trigger corrisponde).
* Eventuali collegamenti tra le sorgenti verranno riscritti nelle Live Copy.

   Ad esempio, i collegamenti dal secondo al primo blueprint verranno riscritti come collegamenti dalla Live Copy nidificata/seconda alla prima Live Copy.

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>Se sposti o rinomini una pagina all’interno del ramo della Live Copy, questa verrà trattata (internamente) come una Live Copy nidificata per consentire AEM tenere traccia delle relazioni.

#### Live Copy sovrapposte {#stacked-live-copies}

Una Live Copy è nota come Live Copy sovrapposta quando viene creata come elemento figlio di una Live Copy poco profonda. Si comporta nello stesso modo di un [Live Copy nidificata](#nested-live-copies).

### Sorgente, blueprint e configurazioni di blueprint {#source-blueprints-and-blueprint-configurations}

Qualsiasi pagina o ramo di pagine può essere utilizzato come origine di una Live Copy.

Tuttavia, MSM consente anche di definire una configurazione blueprint che specifica un percorso sorgente. I vantaggi dell’utilizzo di una configurazione blueprint sono i seguenti:

* Consenti all&#39;autore di utilizzare il **Rollout** opzione su una blueprint - per (esplicitamente) inviare modifiche push alle Live Copy che ereditano da questa blueprint.
* Consenti all&#39;autore di utilizzare **Crea sito**; questo consente all’utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
* Definisci una configurazione di rollout predefinita per le Live Copy che hanno una relazione con la blueprint.

L’origine di una Live Copy può essere costituita da pagine normali o da pagine incluse in una configurazione blueprint, entrambe casi d’uso validi.

La sorgente forma la blueprint per la Live Copy. La blueprint viene definita quando:

* [Creare una configurazione Blueprint](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   La configurazione definisce (in anticipo) le pagine da utilizzare per creare la Live Copy.

* [Creare una Live Copy di una pagina](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Le pagine utilizzate per creare la Live Copy (le pagine sorgente) sono le pagine blueprint.

   È possibile fare riferimento o meno alla pagina sorgente tramite una configurazione blueprint.

### Rollout e sincronizzazione {#rollout-and-synchronize}

Un rollout è l’azione MSM centrale che sincronizza le Live Copy con la loro origine. Puoi eseguire i rollout manualmente o in automatico:

* Una [configurazione di rollout](#rollout-configurations) può essere definita in modo che [eventi](/help/sites-administering/msm-sync.md#rollout-triggers) specifici possano causare un rollout automatico.
* Quando crei una pagina blueprint puoi utilizzare la [Rollout](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) per inviare le modifiche alla Live Copy.

   **Il comando Rollout** è disponibile in una pagina blueprint a cui fa riferimento una configurazione blueprint.

   ![chlimage_1-370](assets/chlimage_1-370.png)

* Quando crei una pagina Live Copy puoi utilizzare la funzione [Sincronizza](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) per estrarre le modifiche dall’origine alla Live Copy.

   La **Sincronizza** è sempre disponibile nella pagina Live Copy (indipendentemente dal fatto che la pagina sorgente/blueprint sia inclusa in una configurazione blueprint).

   ![chlimage_1-371](assets/chlimage_1-371.png)

### Configurazioni rollout {#rollout-configurations}

Una configurazione di rollout definisce quando e come una Live Copy viene sincronizzata con il contenuto sorgente. Una configurazione di rollout è costituita da un trigger e da una o più azioni di sincronizzazione:

* **Attivatore**

   Un trigger è un evento che causa la sincronizzazione di un’azione live, ad esempio l’attivazione di una pagina sorgente. MSM definisce i trigger utilizzabili.

* **Azioni di sincronizzazione**

   Vengono eseguite sulla Live Copy per sincronizzarla con l’origine. Le azioni di esempio sono la copia del contenuto, l’ordine dei nodi figlio e l’attivazione della pagina Live Copy. MSM fornisce una serie di azioni di sincronizzazione.

   >[!NOTE]
   >
   >Puoi creare azioni personalizzate per la tua istanza utilizzando l’API Java.

Le configurazioni di rollout possono essere riutilizzate, in modo che più di una Live Copy possano utilizzare la stessa configurazione di rollout. In un&#39;installazione standard sono incluse diverse [configurazioni di rollout](/help/sites-administering/msm-sync.md#installed-rollout-configurations).

### Conflitti di rollout {#rollout-conflicts}

I rollout possono diventare complicati, specialmente quando gli autori modificano il contenuto sia nella sorgente che nella Live Copy, per questo è utile sapere come AEM gestisce qualsiasi [conflitti che potrebbero verificarsi durante il rollout](/help/sites-administering/msm-rollout-conflicts.md).

### Sospensione e annullamento dell’ereditarietà e della sincronizzazione {#suspending-and-cancelling-inheritance-and-synchronization}

Ogni pagina e componente di una Live Copy è associato alla relativa pagina sorgente e al relativo componente tramite una relazione live. La relazione live configura la sincronizzazione del contenuto della Live Copy dall’origine.

È possibile **Sospendi** l’ereditarietà Live Copy per una pagina Live Copy in modo da poter modificare le proprietà e i componenti della pagina. Quando sospendi l’ereditarietà, le proprietà e i componenti della pagina non vengono più sincronizzati con il sorgente.

Quando modificano una singola pagina, gli autori possono **Annullare l&#39;ereditarietà** per un componente. Quando l’ereditarietà viene annullata, la relazione live viene sospesa e la sincronizzazione non viene eseguita per quel componente. L’annullamento dell’ereditarietà e della sincronizzazione è utile quando è necessario personalizzare le sottosezioni del contenuto.

### Scollegare una Live Copy {#detaching-a-live-copy}

È inoltre possibile [scollegare una Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) dalla blueprint per rimuovere tutte le connessioni.

>[!CAUTION]
>
>L&#39;azione Scollega è permanente e non reversibile.

Lo scollegamento rimuove in modo permanente la relazione live tra una Live Copy e la relativa pagina blueprint. Tutte le proprietà relative a MSM vengono rimosse dalla Live Copy e le pagine Live Copy diventano una copia autonoma.

>[!NOTE]
>
>Vedi [Scollegamento di una Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) per informazioni complete; compreso l’impatto correlato sulle pagine secondarie e principali.

## Passaggi standard per l&#39;utilizzo di MSM {#standard-steps-for-using-msm}

I passaggi seguenti descrivono la procedura standard per utilizzare MSM per riutilizzare il contenuto e sincronizzare le modifiche alle Live Copy.

1. Sviluppa il contenuto del sito sorgente.
1. Determina la configurazione di rollout da utilizzare.

   1. MSM [installa diverse configurazioni di rollout](/help/sites-administering/msm-sync.md#installed-rollout-configurations) che possono soddisfare una serie di casi d&#39;uso.
   1. Eventualmente puoi [creare una configurazione di rollout](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) se necessario.

1. Determina dove devi [specificare le configurazioni di rollout da utilizzare](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) e configurale correttamente.
1. Se necessario, [creare una configurazione blueprint](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) che identifica il contenuto sorgente della Live Copy.
1. [Creare una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. Apporta le modifiche necessarie al contenuto sorgente. Dovresti utilizzare il normale processo di revisione e approvazione del contenuto stabilito dall&#39;organizzazione.
1. [Abbandono](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) il modello, oppure [sincronizzare la Live Copy](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) con le modifiche.

## Personalizzazione di MSM {#customizing-msm}

MSM fornisce strumenti che consentono all’implementazione di adattarsi alle complessità eccezionali che possono esistere durante la condivisione dei contenuti:

* **Configurazioni di rollout personalizzate**
   [Creare una configurazione di rollout](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) quando le configurazioni di rollout installate non soddisfano le tue esigenze. Puoi utilizzare qualsiasi azione di trigger di rollout e sincronizzazione disponibile.

* **Azioni di sincronizzazione personalizzate**
   [Crea un’azione di sincronizzazione personalizzata](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) quando le azioni installate non soddisfano i requisiti specifici dell&#39;applicazione. MSM fornisce un’API Java per la creazione di azioni di sincronizzazione personalizzate.

## Best practice   {#best-practices}

La pagina [Best practice MSM](/help/sites-administering/msm-best-practices.md) contiene informazioni importanti sull’implementazione.
