---
title: Procedure ottimali per i moduli HTML5
seo-title: Procedure ottimali per i moduli HTML5
description: Ottimizzate le prestazioni del vostro Forms HTML5 basato su XFA.
seo-description: Scoprite come ottimizzare il Forms HTML5 basato su XFA per ottenere prestazioni ottimali.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
translation-type: tm+mt
source-git-commit: b6c013a31b70166cba80fea53dffc3794ffee5b8
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 1%

---


# Procedure ottimali per i moduli HTML5{#best-practices-for-html-forms}

## Panoramica {#overview}

 AEM Forms dispone di un componente denominato moduli HTML5. Consente di eseguire il rendering degli PDF forms XFA esistenti (file XDP) in formato HTML5. Questo documento contiene linee guida e consigli per ridurre i tempi di caricamento e migliorare le prestazioni dei moduli HTML5 sui dispositivi mobili.

La maggior parte dei dispositivi mobili dispone di una potenza di elaborazione limitata e di capacità di memoria limitate. Consente di migliorare il tempo di standby dei dispositivi mobili. I browser Web in esecuzione su un dispositivo mobile hanno accesso a risorse limitate (memoria limitata e capacità di elaborazione). Una volta raggiunto il limite, il comportamento del browser diventa lento. Questo documento contiene raccomandazioni per mantenere sotto controllo le dimensioni di un modulo HTML5. Un modulo più piccolo non viola i limiti di memoria e potenza di elaborazione di un dispositivo e offre un&#39;esperienza più semplice.

Anche se le raccomandazioni discusse in questo articolo sono indirizzate ai moduli HTML5, anche se sono ugualmente applicabili ai PDF forms basati su XFA. Queste best practice contribuiscono collettivamente alle prestazioni complessive dei moduli HTML5. È necessaria un&#39;attenta pianificazione per sviluppare forme efficienti e produttive. Cominciamo:

## I nodi sono una valuta dei moduli HTML5, che possono essere utilizzati {#nodes-are-currency-of-html-forms-spend-them-wisely} in modo saggio

In genere, un modulo XFA ha più elementi. Ad esempio, tabella, campo di testo e immagini. Ogni elemento ha una serie di proprietà per controllare il comportamento e l&#39;aspetto dell&#39;elemento. Quando viene eseguito il rendering di un modulo XFA in formato HTML5, tutti gli elementi XFA e le proprietà corrispondenti vengono convertiti in nodi DOM modello o HTML. Questi nodi si aggiungono alle dimensioni e alla complessità di un DOM. Rendering lento del modulo HTML5.

È più semplice per i browser eseguire il rendering di un DOM più snello. Pertanto, è possibile eseguire le seguenti ottimizzazioni su un modulo XFA per ridurre il numero di nodi. Di conseguenza, generate una struttura DOM snella:

* Utilizzare la proprietà caption per aggiungere un&#39;etichetta a un campo. Non utilizzate un elemento Testo separato per aggiungere un&#39;etichetta. Aiuta a perdere peso aggiuntivo, portando a guadagni di prestazioni. Consente inoltre di evitare problemi di layout.
* Ridurre al minimo il numero di elementi di testo Disegno di un modulo. Gli elementi di disegno sono utili per migliorare la leggibilità e l’aspetto, ma non dispongono di funzionalità di memorizzazione delle informazioni. È consigliabile unire più elementi di testo Disegno in un singolo elemento di testo Disegno. Non lasciate nulla di pietra rovesciata per rendere un modulo più snello.

## Le prestazioni dei moduli di liite sono migliori, mantenere le risorse compresse {#lite-forms-perform-better-keep-the-resources-compressed}

Un modulo HTML5 può contenere più risorse esterne, ad esempio file immagine, JavaScript e CSS. Ogni volta che un browser richiede un modulo, le risorse esterne vengono inviate attraverso la rete. Il tempo necessario per viaggiare in rete è direttamente proporzionale alle dimensioni dei file.

Pertanto, ridurre le dimensioni delle risorse esterne e utilizzare solo risorse assolutamente necessarie è il metodo migliore per migliorare le prestazioni dei moduli. In un modulo XFA è possibile eseguire le seguenti ottimizzazioni per ridurre le dimensioni delle risorse esterne di un modulo:

* Utilizzare [immagini compresse](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Riduce l&#39;attività di rete e la quantità di memoria necessaria per eseguire il rendering di un modulo. Di conseguenza, il tempo di caricamento del modulo diminuisce notevolmente.
* Utilizzate l&#39;opzione Riduci in AEM Configuration Manager (Gestione libreria HTML Day CQ) per comprimere i file JavaScript e CSS. Per informazioni dettagliate, consultate [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Abilita compressione Web. Riduce la dimensione delle richieste e delle risposte originate da un modulo. Per informazioni dettagliate, vedere [Ottimizzazione delle prestazioni del server AEM moduli](https://helpx.adobe.com/it/aem-forms/6-3/performance-tuning-aem-forms.html).

## Mantenere vivo l&#39;interesse, mostrare solo i campi obbligatori {#keep-the-interest-alive-show-only-required-fields}

Un modulo HTML5 può essere eseguito su centinaia di pagine. Il caricamento di un modulo con un numero elevato di campi risulta lento nel browser. In un modulo XFA è possibile eseguire le seguenti ottimizzazioni per ottimizzare i moduli con un gran numero di campi e pagine:

* Valutare la suddivisione dei moduli di grandi dimensioni in più moduli. È inoltre possibile utilizzare un set di moduli per raggruppare tutti i moduli più piccoli e presentarli come un&#39;unica unità. Un set di moduli carica solo i moduli richiesti. Inoltre, in un set di moduli è possibile configurare campi comuni in diversi moduli per condividere i binding dei dati. I binding dei dati consentono agli utenti di compilare le informazioni comuni una sola volta; le informazioni vengono compilate automaticamente nei moduli successivi, migliorando notevolmente le prestazioni. Per ulteriori dettagli sui set di moduli, vedere [Set di moduli in AEM moduli](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* È consigliabile suddividere le sezioni e spostare ciascuna sezione in un&#39;altra pagina. I moduli HTML5 caricano in modo dinamico ciascuna pagina nella richiesta di scorrimento della pagina. Solo la pagina scorrevole (la pagina visualizzata e le pagine che la precedono) sono memorizzate; le altre pagine vengono caricate su richiesta. La divisione e lo spostamento di una sezione in una pagina consente quindi di ridurre il tempo necessario per caricare un modulo. È inoltre possibile utilizzare la prima pagina del modulo come pagina di destinazione. È simile al sommario di un libro. Una pagina di destinazione del modulo contiene solo collegamenti alle altre sezioni del modulo. Migliora notevolmente il tempo di caricamento della prima pagina del modulo e migliora l&#39;esperienza dell&#39;utente.
* Per impostazione predefinita, le sezioni condizionali devono essere nascoste. Rendere queste sezioni visibili solo quando viene soddisfatta una determinata condizione. Consente di mantenere al minimo le dimensioni del DOM. Potete anche utilizzare la navigazione con schede per visualizzare una sola sezione alla volta.

## Minore è più, ridurre il numero di pagine {#less-is-more-reduce-the-number-of-pages}

I moduli HTML5 possono contenere campi basati sui dati (tabelle e sottomoduli). Questi campi consentono di espandere le dimensioni del modulo in fase di esecuzione. Ad esempio, una tabella basata sui dati in un modulo HTML5 può estendersi su migliaia di righe. Tali tabelle possono causare un peggioramento del layout e delle prestazioni. Le ottimizzazioni suggerite di seguito consentono di ridurre i tempi di caricamento dei moduli HTML5 con campi basati sui dati:

* Utilizzare gli script XFA per eseguire la navigazione tra le pagine per visualizzare i campi basati sui dati (tabelle e sottomoduli). Nella navigazione tra pagine, su una pagina vengono visualizzati solo dati specifici. Limita l&#39;operazione di colorazione del browser ai campi visualizzati alla volta e semplifica la navigazione all&#39;interno del modulo. Inoltre, gli utenti dei dispositivi mobili sono interessati solo a un sottoinsieme di dati. Consente di offrire un&#39;ottima esperienza utente e di ridurre il tempo necessario per caricare i dati richiesti. Ci sono due soluzioni per il prezzo di una.  Inoltre, la navigazione tra le pagine non è disponibile. È possibile utilizzare gli script XFA per sviluppare la navigazione tra le pagine.

* Valutare l&#39;unione di più colonne di sola lettura in un&#39;unica colonna. Riduce la memoria necessaria per visualizzare il modulo. Inoltre, evitate di visualizzare le colonne che non richiedono input da parte degli utenti.
* Valutare la suddivisione del modulo basato sui dati in un set di moduli [](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html), se i suggerimenti di cui sopra non apportano molti miglioramenti. Ad esempio, se una tabella ha più di 1000 righe, spostare ogni 100 righe in un modulo diverso. In questo modo si migliorerebbero i tempi di caricamento e le prestazioni dei moduli.  Tenere presente che un set di moduli genera un XML di invio consolidato per tutti i moduli. Per distinguere i dati di ogni modulo, utilizzare origini dati diverse. Per ulteriori informazioni, vedere [Set di moduli in  AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## Potenza di due per il documento di registrazione (DOR) {#power-of-two-for-document-of-record-dor}

Un modulo XFA può contenere un numero elevato di sezioni dedicate solo al DOR (Document of Record). Per ridurre il numero di nodi e migliorare le prestazioni di un modulo di questo tipo, è possibile conservare diverse copie del modulo, una per compilare il modulo e un&#39;altra per generare il documento di registrazione sul server. Nella copia per compilare il modulo XFA sono visualizzati i campi richiesti solo per acquisire i dati. Nel file XFA di generazione del documento di registrazione da, mantenere i campi obbligatori solo nell&#39;output di stampa del modulo. Prima di scegliere l&#39;approccio suggerito, valutare il guadagno in termini di prestazioni e il sovraccarico di manutenzione.

## Letture consigliate {#recommended-reads}

I moduli Adobe Experience Manager (AEM) consentono di trasformare transazioni complesse in esperienze digitali semplici e coinvolgenti. Tuttavia, esso richiede uno sforzo concertato per sviluppare forme efficienti e produttive. Oltre a HTML5 Forms, per le best practice generali AEM si consiglia di effettuare le seguenti letture:

* [Best practice per la distribuzione e la manutenzione di AEM](/help/sites-deploying/best-practices.md)
* [Procedure ottimali per la creazione di contenuti](/help/sites-authoring/best-practices.md)
* [Best practice per l’amministrazione di AEM](/help/sites-administering/administer-best-practices.md)
* [Best practice per lo sviluppo di soluzioni](/help/sites-developing/best-practices.md)
* [Procedure consigliate per l&#39;utilizzo dei moduli adattivi](/help/forms/using/adaptive-forms-best-practices.md) 
* [ server AEM Forms non incorpora i font in un modulo PDF dinamico](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Scheda di riferimento rapido {#quick-reference-card}

Potete stampare la seguente scheda (fate clic sulla scheda per scaricare una versione ad alta risoluzione) e tenerla sulla scrivania per un riferimento rapido:
[ ![Best practice HTML5 Forms scheda di riferimento rapido](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
