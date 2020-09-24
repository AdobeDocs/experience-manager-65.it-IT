---
title: Tecniche consigliate per MSM
seo-title: Tecniche consigliate per MSM
description: Scopri le best practice compilate dai team di progettazione e consulenza di  Adobe per iniziare a utilizzare il AEM Multi Site Manager.
seo-description: Scopri le best practice compilate dai team di progettazione e consulenza di  Adobe per iniziare a utilizzare il AEM Multi Site Manager.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 1%

---


# Tecniche consigliate per MSM{#msm-best-practices}

## Generale {#general}

MSM è un framework configurabile per l&#39;automazione della distribuzione dei contenuti. Le implementazioni spesso coinvolgono parti importanti di un sito Web e organizzazioni e geografie. Si consiglia quindi vivamente di pianificare le implementazioni MSM con la stessa attenzione con cui pianificate il sito Web:

* Pianificare accuratamente la struttura e i flussi **** di contenuti prima di iniziare l&#39;implementazione.
* **Personalizzare il più possibile, ma il meno possibile.** MSM supporta un elevato grado di personalizzazione (ad es. configurazioni di rollout), ma in genere la best practice per prestazioni, affidabilità e aggiornamento del sito Web è quella di ridurre al minimo la personalizzazione.
* Stabilire un modello di **governance** in tempi brevi e formare gli utenti di conseguenza per garantire il successo. Dal punto di vista della governance, una best practice consiste nel **ridurre al minimo l&#39;autorità che i produttori di contenuti locali devono** allocare/collegare i contenuti ad altri utenti locali e alle rispettive copie dal vivo. Ciò è dovuto al fatto che le eredità concatenate non gestite possono aumentare notevolmente la complessità di una struttura MSM e comprometterne le prestazioni e l&#39;affidabilità.

* Quando esiste un piano per la struttura, i flussi di contenuti, l&#39;automazione e la governance - **prototipo e test completo del sistema**, prima di iniziare l&#39;implementazione live.
* Tenere presente che **Consulenza di Adobe e i principali integratori** di sistema hanno una pianificazione approfondita dell&#39;esperienza e implementano l&#39;automazione dei contenuti con MSM, consentendo di iniziare a utilizzare il progetto MSM e l&#39;intera implementazione.

>[!NOTE]
>
>Ulteriori informazioni sull&#39;utilizzo di MSM sono disponibili negli articoli della Knowledge Base:
>
>* [Domande frequenti su MSM](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [Risoluzione dei problemi relativi a MSM](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>È inoltre possibile utilizzare il componente [](/help/sites-authoring/default-components-foundation.md#reference) Riferimento per riutilizzare una singola pagina o paragrafo. Ricorda tuttavia:
>
>* MSM è più flessibile e consente di controllare con precisione i contenuti sincronizzati e quando.
>* [I componenti](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) core sono ora consigliati rispetto ai componenti di base.

>



## Origini Live Copy e configurazioni Blueprint {#live-copy-sources-and-blueprint-configurations}

È possibile creare una Live Copy utilizzando pagine [](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) normali o una configurazione [di](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)blueprint. Entrambi sono casi di utilizzo validi.

L’utilizzo di una configurazione blueprint comporta inoltre i seguenti vantaggi:

* Consentite all’autore di utilizzare l’opzione **Rollout** su un blueprint, per (in modo esplicito) le modifiche push alle Live Copy che ereditano da questo blueprint.
* Consentire all&#39;autore di utilizzare **Crea sito**; questo consente all&#39;utente di selezionare facilmente le lingue e configurare la struttura della Live Copy.
* Definite una configurazione di rollout predefinita per le copie live che hanno una relazione con il progetto.

Nel caso in cui non venga fatto riferimento a una configurazione di blueprint, i rollout possono essere avviati solo dalle copie live, essenzialmente recuperando il contenuto dall&#39;origine.

Quando si crea un nuovo sito con Live Copy, è vantaggioso creare configurazioni di blueprint per garantire la disponibilità dell&#39;intero set di funzioni MSM.

## Sincronizzazione di componenti e contenitori {#components-and-container-synchronization}

In generale, la regola di implementazione in MSM per quanto riguarda la sincronizzazione dei componenti è:

* I componenti vengono implementati per sincronizzare tutte le risorse contenute nel blueprint.
* I contenitori sincronizzano solo la risorsa corrente.

Ciò significa che i componenti vengono trattati come un aggregato e che in un rollout il componente stesso e tutti i suoi elementi secondari vengono sostituiti con quelli presenti nei progetti. Ciò significa che se una risorsa viene aggiunta localmente a tale componente, andrà persa per il contenuto del blueprint al momento dell’implementazione.

Per supportare la nidificazione di componenti in modo che i componenti aggiunti localmente vengano mantenuti in un rollout, il componente deve essere dichiarato come contenitore. Ad esempio, parsys predefinito viene dichiarato come contenitore in modo da supportare il contenuto aggiunto localmente.

>[!NOTE]
>
>Aggiungete la proprietà `cq:isContainer` al componente per designarlo come contenitore.

## Crea sito {#create-site}

AEM dispone di due approcci principali per la creazione di copie live:

* When [creating a Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Questo può essere considerato un approccio più generico, che consente di creare copie dal vivo da qualsiasi pagina. La struttura del contenuto di una Live Copy corrisponde esattamente all&#39;origine.

* Quando si [crea un sito](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Si tratta di un approccio più specializzato, soprattutto per la creazione di siti web con una struttura multilingue.

Di seguito sono riportate alcune considerazioni da tenere a mente durante la creazione di un sito:

* Per creare un nuovo sito, è necessaria una configurazione [](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)blueprint.
* Per consentire la selezione dei percorsi di lingua da creare in un nuovo sito, nel blueprint (origine) devono essere presenti le radici della lingua corrispondenti.
* Dopo aver creato un [nuovo sito come Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (utilizzando **Crea** e quindi **Sito**), i primi due livelli di questa Live Copy sono *poco* nitidi. Gli elementi figlio della pagina non appartengono alla relazione dal vivo, ma se viene trovata una relazione dal vivo che corrisponde all&#39;attivatore, un rollout continua a scendere.

   Consente di evitare:

   * aggiunta manuale di lingue nel blueprint (sotto il primo livello)
   * aggiungere manualmente il contenuto direttamente sotto la radice della lingua,
   * non comporta il trasferimento automatico del nuovo contenuto alla Live Copy al momento del rollout.

## MSM e siti Web multilingue {#msm-and-multilingual-websites}

MSM può contribuire alla creazione di siti Web multilingue in due modi:

* Quando si creano le pagine master della lingua.

   * Anche se MSM **non fornisce la traduzione** del contenuto, può essere integrato con connettori di traduzione di terze parti che lo fanno. Si noti che:

      * MSM consente di annullare l&#39;ereditarietà a livello di pagina e/o componente. Questo consente di evitare la sovrascrittura del contenuto tradotto (da una Live Copy, con contenuto non ancora tradotto da un blueprint) nel prossimo rollout.
      * Alcuni connettori di traduzione di terze parti automatizzano la gestione delle ereditarietà MSM.

         Per ulteriori informazioni, contattate il vostro provider di servizi di traduzione.

      * Un approccio alternativo per la creazione e la traduzione di master di lingua consiste nell&#39;utilizzare copie di lingua insieme AEM framework di integrazione per la traduzione out-of-the-box.

* Quando si distribuiscono contenuti dalle mastro della lingua.

   * Ad esempio, dal master in lingua francese ai siti specifici per paese, come Francia/francese, Canada/francese, Svizzera/francese.

Per ulteriori informazioni, consultate [Traduzione di contenuti per siti](/help/sites-administering/translation.md) multilingue e [Tecniche consigliate](/help/sites-administering/tc-bp.md)per la traduzione.

## Modifiche alla struttura e rollout {#structure-changes-and-rollouts}

Le modifiche alla struttura del contenuto in una struttura ad albero blueprint/source vengono riportate in modo diverso in una Live Copy. Dipende dal tipo di modifica:

* **La creazione** di nuove pagine in una blueprint comporta la creazione di pagine corrispondenti in Live Copy dopo il rollout con la configurazione di rollout standard.

* **Se eliminate** delle pagine in una blueprint, le pagine corrispondenti verranno eliminate dalle Live Copy dopo il rollout con la configurazione di rollout standard.

* **Lo spostamento** delle pagine in una blueprint **non** comporta lo spostamento delle pagine corrispondenti in Live Copy dopo il rollout con la configurazione di rollout standard:

   * Questo comportamento si basa sul fatto che lo spostamento di una pagina include implicitamente l’eliminazione di una pagina. Ciò potrebbe causare un comportamento imprevisto durante la pubblicazione, in quanto l’eliminazione delle pagine in fase di creazione disattiva automaticamente il contenuto corrispondente al momento della pubblicazione. Questo può anche avere un effetto di trascinamento su elementi correlati come collegamenti, segnalibri e altri.
   * L&#39;ereditarietà dei contenuti nelle rispettive pagine delle Live Copy viene aggiornata per riflettere la nuova posizione delle relative origini nel blueprint.
   * Per realizzare appieno lo spostamento di una pagina da un blueprint a Live Copy, tenete presenti le seguenti procedure ottimali:

>[!NOTE]
>
>Questo funzionerà solo con l&#39;attivatore [](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)On Rollout.

* Crea una configurazione di rollout personalizzata:

   * Questa nuova configurazione deve includere l’azione:

      `PageMoveAction`

      Non aggiungere altre azioni a questa configurazione.

* Posizionare la nuova configurazione:

   * Per distribuire completamente lo spostamento della pagina, eliminando le rispettive pagine nella posizione precedente nella Live Copy:

      * Posizionate la configurazione appena creata prima della configurazione di rollout standard.

         La configurazione di rollout standard si occupa dell’eliminazione delle pagine nella posizione precedente.
   * Per distribuire lo spostamento della pagina mantenendo le rispettive pagine nella posizione precedente nelle Live Copy (essenzialmente duplicando il contenuto):

      * Posizionate la configurazione appena creata dopo la configurazione di rollout standard.

         In questo modo non verrà eliminato alcun contenuto nella Live Copy né verrà disattivato dalla pubblicazione.


## Personalizzazione dei Rollout {#customizing-rollouts}

Le configurazioni di rollout MSM sono altamente personalizzabili. È importante tenere presente che l&#39;automazione dei rollout può avere conseguenze di vasta portata. Come procedura ottimale, devi pianificare *con molta* attenzione prima, ad esempio:

* automatizzare i rollout; ad esempio, con attivatori [onModify](#onmodify),
* personalizzazione dei tipi/delle proprietà [dei](#node-types-properties)nodi,
* avvio di flussi di lavoro successivi,
* e/o attivazione del contenuto come parte dei rollout.

### onModify {#onmodify}

Quando si utilizza l&#39;attivatore [](/help/sites-administering/msm-sync.md#rollout-triggers) rollout `onModify` , tenere presente quanto segue:

* L&#39;automazione dei rollout con `onModify` i trigger potrebbe avere un impatto negativo sulle prestazioni di authoring quando attivano i rollout dopo *ogni* modifica di pagina.

* Il risultato del rollout può essere diverso da quello previsto come:

   * Non è possibile specificare l&#39;ordine degli eventi di modifica risultanti.
   * L&#39;architettura basata sugli eventi non può garantire la sequenza degli eventi passati al Rollout Manager.

* L&#39;utilizzo di tale configurazione di rollout potrebbe causare conflitti se si verificano aggiornamenti simultanei della stessa risorsa.

Pertanto, si consiglia di utilizzare *solo* `onModify` gli attivatori se i vantaggi dell&#39;avvio automatico supera qualsiasi potenziale problema di prestazioni.

### Tipi di nodo/proprietà {#node-types-properties}

Ricorda che:

* Oltre a personalizzare le azioni di rollout, MSM consente anche di personalizzare le proprietà dei nodi in fase di implementazione. La configurazione [MSM OSGi consente di escludere i tipi](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) di nodi dalla copia dall&#39;origine alla Live Copy.

## Ulteriori informazioni {#further-information}

Questa e le pagine seguenti affrontano i problemi correlati:

* [Creazione e sincronizzazione di Live Copy](/help/sites-administering/msm-livecopy.md)
* [Console Panoramica Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configurazione della sincronizzazione di una Live Copy](/help/sites-administering/msm-sync.md)
* [Conflitti tra rollout MSM](/help/sites-administering/msm-rollout-conflicts.md)

