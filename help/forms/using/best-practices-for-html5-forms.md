---
title: Best practice per i moduli HTML5
seo-title: Best practices for HTML5 forms
description: Ottimizza il tuo Forms HTML5 basato su XFA per ottenere prestazioni migliori.
seo-description: Learn how to tune your XFA-based HTML5 Forms for best performance.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 1%

---

# Best practice per i moduli HTML5{#best-practices-for-html-forms}

## Panoramica {#overview}

AEM Forms ha un componente chiamato HTML5 forms. Consente di eseguire il rendering dei PDF forms basati su XFA (file XDP) esistenti in formato HTML5. Questo documento fornisce linee guida e raccomandazioni per ridurre il tempo di caricamento e migliorare le prestazioni dei moduli HTML5 sui dispositivi mobili.

La maggior parte dei dispositivi mobili dispone di una potenza di elaborazione e di capacità di memoria limitate. Aiuta a migliorare il tempo di standby dei dispositivi mobili. I browser web in esecuzione su un dispositivo mobile hanno accesso a risorse limitate (memoria limitata e funzionalità di elaborazione). Una volta raggiunto il limite, il comportamento del browser diventa lento. In questo documento vengono fornite raccomandazioni per mantenere sotto controllo le dimensioni di un modulo HTML5. Un modulo più piccolo non viola i limiti di memoria ed elaborazione di un dispositivo e fornisce un&#39;esperienza fluida.

Sebbene le raccomandazioni discusse in questo articolo siano mirate ai moduli HTML5, sono ugualmente applicabili ai PDF forms basati su XFA. Queste best practice contribuiscono collettivamente alle prestazioni complessive dei moduli HTML5. È necessaria un&#39;attenta pianificazione per sviluppare forme efficienti e produttive. Cominciamo:

## I nodi sono valuta delle forme di HTML5, spenderli con saggezza {#nodes-are-currency-of-html-forms-spend-them-wisely}

In genere, un modulo XFA ha più elementi. Ad esempio, tabella, campo di testo e immagini. Ogni elemento dispone di una serie di proprietà per controllare il comportamento e l’aspetto dell’elemento. Quando si esegue il rendering di un modulo XFA in formato HTML5, tutti gli elementi XFA e le proprietà corrispondenti vengono convertiti in nodi DOM Model o HTML. Questi nodi si aggiungono alle dimensioni e alla complessità di un DOM. Rendering del modulo HTML5 lento.

Il rendering di un DOM più snello è più semplice per i browser. È quindi possibile eseguire le seguenti ottimizzazioni su un modulo XFA per ridurre il numero di nodi. Pertanto, genera una struttura DOM snella:

* Utilizzare la proprietà caption per aggiungere un&#39;etichetta a un campo. Non utilizzare un elemento Testo separato per aggiungere un’etichetta. Aiuta a perdere peso extra, portando a guadagni di prestazioni. Aiuta anche ad evitare problemi di layout.
* Mantenere al minimo il numero di elementi di testo Disegno presenti in un modulo. Gli elementi di disegno sono utili per migliorare la leggibilità e l’aspetto, ma non dispongono di funzionalità di archiviazione delle informazioni. Si consiglia di unire più elementi di testo Disegno in un unico elemento di testo Disegno. Non lasciare nessuna pietra involta per rendere un modulo più snello.

## Le prestazioni dei moduli liti sono migliori, le risorse vengono compresse {#lite-forms-perform-better-keep-the-resources-compressed}

Un modulo HTML5 può contenere più risorse esterne, ad esempio file immagine, JavaScript e CSS. Ogni volta che un browser richiede un modulo, le risorse esterne vengono inviate tramite la rete. Il tempo necessario per viaggiare in rete è direttamente proporzionale alle dimensioni dei file.

Pertanto, ridurre le dimensioni delle risorse esterne e utilizzare solo le risorse assolutamente necessarie è il metodo migliore per migliorare le prestazioni dei moduli. È possibile eseguire le seguenti ottimizzazioni su un modulo XFA per ridurre le dimensioni delle risorse esterne di un modulo:

* Utilizzo [immagini compresse](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Riduce l’attività di rete e la quantità di memoria necessaria per eseguire il rendering di un modulo. Pertanto, il tempo di caricamento del modulo diminuisce notevolmente.
* Utilizza l’opzione minimizza in AEM Configuration Manager (Day CQ HTML Library Manager) per comprimere i file JavaScript e CSS. Per maggiori dettagli, vedi [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Abilita la compressione web. Riduce le dimensioni delle richieste e delle risposte provenienti da un modulo. Per maggiori dettagli, vedi [Ottimizzazione delle prestazioni del server AEM forms](https://helpx.adobe.com/it/aem-forms/6-3/performance-tuning-aem-forms.html).

## Mantenere vivo l&#39;interesse, mostrare solo i campi obbligatori  {#keep-the-interest-alive-show-only-required-fields}

Un modulo HTML5 può essere eseguito su centinaia di pagine. Il caricamento di un modulo con un numero elevato di campi nel browser è lento. È possibile eseguire le seguenti ottimizzazioni in un modulo XFA per ottimizzare i moduli con un gran numero di campi e pagine:

* Valutare la suddivisione dei moduli di grandi dimensioni in più moduli. È inoltre possibile utilizzare un set di moduli per raggruppare tutti i moduli più piccoli e presentarli come un’unica unità. Un set di moduli carica solo i moduli richiesti. Inoltre, in un set di moduli è possibile configurare campi comuni in diversi moduli per condividere i binding dei dati. I binding dei dati consentono agli utenti di compilare le informazioni comuni una sola volta; le informazioni vengono compilate automaticamente nei moduli successivi, con conseguente miglioramento delle prestazioni. Per ulteriori dettagli sui set di moduli, vedere [Set di moduli AEM moduli](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* Prendi in considerazione la suddivisione delle sezioni e lo spostamento di ciascuna sezione in una pagina diversa. I moduli di HTML5 vengono caricati in modo dinamico ogni pagina nella richiesta di scorrimento della pagina. Solo la pagina scorrevole (la pagina visualizzata e le pagine che la precedono) sono memorizzate nella memoria; le altre pagine vengono caricate su richiesta. La suddivisione e lo spostamento di una sezione su una pagina consente di ridurre il tempo necessario per caricare un modulo. È inoltre possibile utilizzare la prima pagina del modulo come pagina di destinazione. È simile al sommario di un libro. Una pagina di destinazione del modulo contiene solo collegamenti alle altre sezioni del modulo. Migliora notevolmente il tempo di caricamento della prima pagina del modulo e migliora l’esperienza utente.
* Mantieni le sezioni condizionali nascoste, per impostazione predefinita. Rendere queste sezioni visibili solo quando viene soddisfatta una determinata condizione. Aiuta a mantenere al minimo le dimensioni del DOM. È inoltre possibile utilizzare la navigazione a schede per visualizzare una sola sezione alla volta.

## Minore è di più, riduci il numero di pagine {#less-is-more-reduce-the-number-of-pages}

I moduli di HTML5 possono contenere campi basati sui dati (tabelle e sottomoduli). Questi campi espandono le dimensioni del modulo in fase di esecuzione. Ad esempio, una tabella basata sui dati in un modulo HTML5 può essere suddivisa in migliaia di righe. Tali tabelle possono causare un deterioramento del layout e delle prestazioni. Le ottimizzazioni suggerite di seguito consentono di ridurre il tempo di caricamento dei moduli di HTML5 con campi basati sui dati:

* Utilizzare gli script XFA per ottenere la navigazione tra pagine per visualizzare campi basati sui dati (tabelle e sottomoduli). Nella navigazione in pagine, su una pagina vengono visualizzati solo dati specifici. Limita l’operazione di disegno del browser ai campi visualizzati alla volta e semplifica la navigazione in un modulo. Inoltre, gli utenti dei dispositivi mobili sono interessati solo a un sottoinsieme di dati. Consente di fornire un’esperienza utente straordinaria e di ridurre il tempo necessario per caricare i dati richiesti. Hai due soluzioni al prezzo di una.  Inoltre, la navigazione tra pagine non è disponibile come funzionalità integrata. È possibile utilizzare gli script XFA per sviluppare la navigazione tra pagine.

* Valutare l’unione di più colonne di sola lettura in un’unica colonna. Riduce la memoria necessaria per visualizzare il modulo. Inoltre, evita di visualizzare le colonne che non richiedono input da parte degli utenti.
* Valutare la suddivisione del modulo basato su dati in un [set di moduli](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html), se i suggerimenti di cui sopra non producono molti miglioramenti. Ad esempio, se una tabella ha più di 1000 righe, spostare ogni 100 righe in un modulo diverso. Ciò contribuirebbe a migliorare il tempo di caricamento e le prestazioni dei moduli.  Tenere presente inoltre che un set di moduli produce un XML di invio consolidato per tutti i moduli. Per differenziare i dati di ogni modulo, utilizzare origini dati diverse. Per ulteriori informazioni, consulta [Set di moduli in AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## Potenza di due per il documento di registrazione (DOR) {#power-of-two-for-document-of-record-dor}

Un modulo XFA può avere un numero elevato di sezioni dedicate solo al DOR (Document of Record). Per ridurre il numero di nodi e migliorare le prestazioni di un modulo di questo tipo, è possibile mantenere copie diverse del modulo, una copia per compilare il modulo e un&#39;altra per generare documenti di record sul server. Nella copia per compilare il modulo XFA vengono visualizzati i campi necessari solo per acquisire i dati. Nel file XFA di generazione del documento di record, conservare i campi richiesti solo nell’output stampato del modulo. Prima di scegliere l&#39;approccio suggerito, valutare il guadagno di prestazioni e il sovraccarico di manutenzione.

## Letture consigliate  {#recommended-reads}

I moduli di Adobe Experience Manager (AEM) consentono di trasformare transazioni complesse in esperienze digitali semplici e accattivanti. Tuttavia, esso richiede uno sforzo concertato per sviluppare forme efficienti e produttive. Oltre a HTML5 Forms, di seguito sono riportate alcune letture consigliate per le best practice generali AEM:

* [Best practice per la distribuzione e la manutenzione dei AEM](/help/sites-deploying/best-practices.md)
* [Best practice per l’authoring dei contenuti](/help/sites-authoring/best-practices.md)
* [Best practice per l’amministrazione di AEM](/help/sites-administering/administer-best-practices.md)
* [Best practice per lo sviluppo di soluzioni](/help/sites-developing/best-practices.md)
* [Procedure consigliate per l&#39;utilizzo dei moduli adattivi ](/help/forms/using/adaptive-forms-best-practices.md)
* [Il server AEM Forms non incorpora i font in un modulo Dynamic PDF](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Scheda di riferimento rapido {#quick-reference-card}

È possibile stampare la seguente scheda (fare clic su una scheda per scaricare una versione ad alta risoluzione) e tenerla sulla scrivania per un riferimento rapido:
[ ![Scheda di riferimento rapido sulle best practice per HTML5 Forms](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
