---
title: Best practice MSM
seo-title: Best practice MSM
description: Trova le best practice compilate dai team di progettazione e consulenza di Adobe per aiutarti a iniziare a usare il AEM Multi Site Manager.
seo-description: Trova le best practice compilate dai team di progettazione e consulenza di Adobe per aiutarti a iniziare a usare il AEM Multi Site Manager.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
feature: Multi Site Manager
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 1%

---


# Best practice MSM{#msm-best-practices}

## Generale {#general}

MSM è un framework configurabile per automatizzare la distribuzione dei contenuti. Le implementazioni spesso coinvolgono parti importanti di un sito web e si estendono su più organizzazioni e aree geografiche. È quindi vivamente consigliato pianificare le implementazioni MSM con la stessa attenzione che pianifichi il tuo sito web:

* Pianifica attentamente **la struttura e i flussi di contenuto** prima di avviare l&#39;implementazione.
* **Mantenere al minimo la quantità di Live Copy.** L’elaborazione delle Live Copy è un’attività che richiede molte risorse. Più Live Copy esistono nel sistema, più prestazioni possono essere influenzate: dall’elaborazione degli indici della Live Copy interna alle operazioni di Live Copy, come i rollout, alle operazioni dell’interfaccia utente, come la visualizzazione delle relazioni Live Copy nella barra dei riferimenti dell’amministratore dei siti. Si consiglia di creare Live Copy di siti o rami di un sito, in cui le relazioni Live Copy vengono ereditate alle pagine del sito o del ramo. Evita di creare singole Live Copy per le pagine di un sito o di un ramo quando l’intera struttura può essere trasformata in una Live Copy.
* **Personalizza il più possibile, ma il meno possibile.** MSM supporta un elevato grado di personalizzazione (ad esempio configurazioni di rollout), ma la best practice per le prestazioni, l’affidabilità e l’aggiornamento del sito web è quella di ridurre al minimo la personalizzazione.
* Stabilire un modello **governance** in anticipo e addestrare gli utenti di conseguenza per garantire il successo. Una best practice dal punto di vista della governance consiste nel **ridurre al minimo l&#39;autorità di cui dispongono i produttori di contenuti locali** per allocare/collegare contenuti ad altri utenti locali e alle rispettive Live Copy. Ciò è dovuto al fatto che le ereditarietà non gestite e incatenate possono aumentare notevolmente la complessità di una struttura MSM e comprometterne le prestazioni e l&#39;affidabilità.

* Una volta che esiste un piano per la struttura, i flussi di contenuto, l&#39;automazione e la governance - **prototipo e test completo del sistema**, prima di avviare l&#39;implementazione live.
* Tieni presente che **Adobe Consulting and Lead System Integrators** dispongono di una pianificazione approfondita dell&#39;esperienza e dell&#39;implementazione dell&#39;automazione dei contenuti con MSM, in modo che possano aiutarti a iniziare con il tuo progetto MSM e l&#39;intera implementazione.

>[!NOTE]
>
>Ulteriori informazioni sull&#39;utilizzo di MSM sono disponibili negli articoli della Knowledge Base:
>
>* [Domande frequenti su MSM](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [Risoluzione dei problemi relativi a MSM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>È inoltre possibile utilizzare il [componente Riferimento](/help/sites-authoring/default-components-foundation.md#reference) per riutilizzare una singola pagina o paragrafo. Ricorda tuttavia:
>
>* MSM è più flessibile e consente un controllo a grana fine su quale contenuto viene sincronizzato e quando.
>* [I ](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html) componenti core sono ora consigliati sui componenti di base.

>



## Origini Live Copy e configurazioni Blueprint {#live-copy-sources-and-blueprint-configurations}

Tieni presente che una Live Copy può essere creata utilizzando le pagine [normali](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) o una [configurazione blueprint](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Entrambi sono casi d’uso validi.

I vantaggi aggiuntivi dell’utilizzo di una configurazione blueprint sono i seguenti:

* Consenti all&#39;autore di utilizzare l&#39;opzione **Rollout** su una blueprint - per (esplicitamente) inviare modifiche alle Live Copy che ereditano da questa blueprint.
* Consenti all&#39;autore di utilizzare **Crea sito**; questo consente all’utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
* Definisci una configurazione di rollout predefinita per le Live Copy che hanno una relazione con la blueprint.

Nel caso in cui non venga fatto riferimento a una configurazione blueprint, i rollout possono essere avviati solo dalle Live Copy stesse, essenzialmente estraendo il contenuto dalla sorgente.

Quando crei un nuovo sito con Live Copy, è vantaggioso creare configurazioni blueprint per garantire la disponibilità dell’intero set di funzioni MSM.

## Componenti e sincronizzazione dei contenitori {#components-and-container-synchronization}

In generale, la regola di rollout in MSM per quanto riguarda la sincronizzazione dei componenti è:

* I componenti vengono implementati per sincronizzare tutte le risorse contenute nel blueprint.
* I contenitori sincronizzano solo la risorsa corrente.

Ciò significa che i componenti sono trattati come un aggregato e in un rollout il componente stesso e tutti i suoi figli vengono sostituiti con quelli nei progetti. Ciò significa che se una risorsa viene aggiunta localmente a tale componente, andrà persa per il contenuto della blueprint al momento del rollout.

Per supportare la nidificazione dei componenti in modo che i componenti aggiunti localmente siano mantenuti in un rollout, il componente deve essere dichiarato come contenitore. Ad esempio, il parsys predefinito viene dichiarato come contenitore in modo che possa supportare il contenuto aggiunto localmente.

>[!NOTE]
>
>Aggiungi la proprietà `cq:isContainer` al componente per designarlo come contenitore.

## Crea sito {#create-site}

AEM dispone di due approcci principali per la creazione di Live Copy:

* Quando [si crea una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Questo può essere considerato l’approccio più generico, che consente di creare Live Copy da qualsiasi pagina. La struttura del contenuto di una Live Copy corrisponde esattamente all’origine.

* Quando [si crea un sito](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Si tratta di un approccio più specializzato, principalmente per la creazione di siti web con una struttura multilingue.

Di seguito sono riportate alcune considerazioni da tenere a mente durante la creazione di un sito:

* Per creare un nuovo sito, è necessaria una [configurazione blueprint](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Per consentire la selezione dei percorsi linguistici da creare in un nuovo sito, le radici della lingua corrispondenti devono esistere nella blueprint (sorgente).
* Una volta creato un [nuovo sito come Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (utilizzando **Crea** e **Sito**), i primi due livelli di questa Live Copy sono *superficiali*. Gli elementi figlio della pagina non appartengono alla relazione in tempo reale, ma se viene trovata una relazione in tempo reale corrispondente al trigger, verrà comunque generato un rollout.

   Aiuta a evitare:

   * aggiunta manuale di lingue nella blueprint (sotto il primo livello)
   * aggiunta manuale di contenuti direttamente sotto la directory principale della lingua,
   * non porta automaticamente questo nuovo contenuto alla Live Copy al momento del rollout.

## Siti web MSM e multilingue {#msm-and-multilingual-websites}

MSM può contribuire alla creazione di siti web multilingue in due modi:

* Durante la creazione di schemi di lingua.

   * Anche se MSM stesso **non fornisce la traduzione dei contenuti**, può essere integrato con i connettori di traduzione di terze parti che lo fanno. Nota che:

      * MSM consente di annullare l’ereditarietà a livello di pagina e/o componente. Questo aiuta a evitare la sovrascrittura dei contenuti tradotti (da una Live Copy, con contenuti non ancora tradotti da una blueprint) al prossimo rollout.
      * Alcuni connettori di traduzione di terze parti automatizzano questa gestione delle ereditarietà MSM.

         Per ulteriori informazioni, rivolgersi al provider di servizi di traduzione.

      * Un approccio alternativo per la creazione e la traduzione di master in lingua consiste nell’utilizzare copie in lingua insieme AEM framework di integrazione della traduzione preconfigurato.

* Quando si esegue il rollout dei contenuti dalle lingue master.

   * Ad esempio, dal master in lingua francese ai siti specifici per paese, come Francia/francese, Canada/francese, Svizzera/francese.

Per ulteriori informazioni, consulta [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md) e [Best practice per la traduzione](/help/sites-administering/tc-bp.md).

## Modifiche alla struttura e rollout {#structure-changes-and-rollouts}

Le modifiche alla struttura del contenuto in una struttura blueprint/source si riflettono in modo diverso in una Live Copy. Dipende dal tipo di modifica:

* **** La creazione di nuove pagine in una blueprint determina la creazione di pagine corrispondenti in Live Copy dopo il rollout con la configurazione di rollout standard.

* **** L’eliminazione delle pagine in una blueprint comporta l’eliminazione delle pagine corrispondenti dalle Live Copy dopo il rollout con configurazione di rollout standard.

* **** Lo spostamento delle pagine in una blueprint  **** non comporta lo spostamento delle pagine corrispondenti nelle Live Copy dopo il rollout con configurazione di rollout standard:

   * Questo comportamento si spiega con il fatto che lo spostamento di una pagina include implicitamente l’eliminazione di una pagina. Questo potrebbe causare un comportamento imprevisto al momento della pubblicazione, in quanto l’eliminazione delle pagine sull’autore disattiva automaticamente il contenuto corrispondente al momento della pubblicazione. Questo può anche avere un effetto di trascinamento su elementi correlati come collegamenti, segnalibri e altri.
   * L’ereditarietà dei contenuti nelle rispettive pagine Live Copy viene aggiornata per riflettere la nuova posizione delle relative origini nella blueprint.
   * Per realizzare completamente lo spostamento di una pagina da una blueprint a Live Copy, considera le seguenti best practice:

>[!NOTE]
>
>Questo funzionerà solo con il [Attivatore di rollout](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

* Crea una configurazione di rollout personalizzata:

   * Questa nuova configurazione deve includere l’azione :

      `PageMoveAction`

      Non aggiungere altre azioni a questa configurazione.

* Posiziona la nuova configurazione:

   * Per eseguire il rollout completo della pagina spostata, eliminando le rispettive pagine nella vecchia posizione nella Live Copy:

      * Posiziona la configurazione appena creata prima della configurazione di rollout standard.

         La configurazione di rollout standard si occuperà di eliminare le pagine nella loro vecchia posizione.
   * Per eseguire il rollout dello spostamento della pagina mantenendo le rispettive pagine nella loro vecchia posizione nelle Live Copy (essenzialmente duplicando il contenuto):

      * Posiziona la configurazione appena creata dopo la configurazione di rollout standard.

         In questo modo nessun contenuto viene eliminato dalla Live Copy o disattivato dalla pubblicazione.


## Personalizzazione dei rollout {#customizing-rollouts}

Le configurazioni di rollout MSM sono altamente personalizzabili. Tieni presente che automatizzare i rollout può avere conseguenze di vasta portata. Come best practice, pianifica *molto* con attenzione prima, ad esempio:

* automatizzare i rollout; ad esempio, con [onModify triggers](#onmodify),
* personalizzazione di [tipi/proprietà di nodo](#node-types-properties),
* avvio dei flussi di lavoro successivi,
* e/o attivazione di contenuti come parte dei rollout.

### onModify {#onmodify}

Quando utilizzi il [trigger di rollout](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`, tieni presente quanto segue:

* L’automazione dei rollout con i trigger `onModify` può avere un impatto negativo sulle prestazioni di authoring in quanto attivano i rollout dopo *ogni* modifica della pagina.

* Il risultato del rollout può differire da quello previsto come:

   * Non è possibile specificare l’ordine degli eventi di modifica risultanti.
   * L&#39;architettura basata su eventi non può garantire la sequenza degli eventi passati al Rollout Manager.

* L’utilizzo di tale configurazione di rollout potrebbe causare conflitti se si verificano aggiornamenti simultanei della stessa risorsa.

Pertanto, si consiglia di attivare *solo* l&#39;utilizzo di `onModify` se i vantaggi dell&#39;avvio automatico di rollout superano eventuali problemi di prestazioni.

### Tipi di nodo/proprietà {#node-types-properties}

Ricorda che:

* Oltre a personalizzare le azioni di rollout, MSM ti consente anche di personalizzare le proprietà dei nodi in fase di rollout. La configurazione [MSM OSGi ti consente di escludere i tipi di nodo](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) dalla copia dal sorgente alla Live Copy.

## Ulteriori informazioni {#further-information}

Queste pagine e le seguenti trattano i problemi correlati:

* [Creazione e sincronizzazione di Live Copy](/help/sites-administering/msm-livecopy.md)
* [Console Panoramica di Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurazione della sincronizzazione di una Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitti di rollout MSM](/help/sites-administering/msm-rollout-conflicts.md)

