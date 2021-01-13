---
title: Miglioramento delle prestazioni dei moduli di grandi dimensioni con caricamento lento
seo-title: Miglioramento delle prestazioni dei moduli di grandi dimensioni con caricamento lento
description: Il caricamento lento migliora notevolmente le prestazioni dei moduli adattivi di grandi dimensioni e complessi, posticipando l'inizializzazione e il caricamento dei frammenti di modulo fino a renderli visibili.
seo-description: Il caricamento lento migliora notevolmente le prestazioni dei moduli adattivi di grandi dimensioni e complessi, posticipando l'inizializzazione e il caricamento dei frammenti di modulo fino a renderli visibili.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
translation-type: tm+mt
source-git-commit: 4d95d0e38acc54e1ebbb9f9e31761205533e99f9
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---


# Miglioramento delle prestazioni dei moduli di grandi dimensioni con caricamento lento{#improve-performance-of-large-forms-with-lazy-loading}

## Introduzione al caricamento pigro {#introduction-to-lazy-loading}

Quando un modulo diventa grande e complesso con centinaia e migliaia di campi, gli utenti finali riscontrano un lungo tempo di risposta durante il rendering dei moduli in fase di esecuzione. Per ridurre al minimo il tempo di risposta, i moduli adattivi consentono di suddividere i moduli in frammenti logici e di configurare in modo da posticipare l&#39;inizializzazione o il caricamento dei frammenti fino a quando il frammento non sia visibile. Si chiama caricamento pigro. Inoltre, i frammenti configurati per il caricamento pigro vengono scaricati non appena l&#39;utente passa ad altre sezioni del modulo e i frammenti non sono più visibili.

Comprendiamo innanzitutto i requisiti e i passaggi preparatori prima di configurare il caricamento pigro.

## Preparazione alla configurazione del caricamento pigro {#preparing-to-configure-lazy-loading}

Prima di configurare il caricamento pigro dei frammenti nel modulo adattivo, è importante definire strategie per la creazione di frammenti, identificare i valori utilizzati negli script o citati in altri frammenti e definire regole per controllare la visibilità dei campi nei frammenti caricati lentamente.

* **Identificare e creare**
i frammentiÈ possibile configurare solo i frammenti di modulo adattivi per il caricamento pigro. Un frammento è un segmento autonomo che si trova al di fuori di un modulo adattivo e può essere riutilizzato nei diversi moduli. Pertanto, il primo passo verso l&#39;implementazione del caricamento pigro è identificare le sezioni logiche di un modulo e convertirle in frammenti. È possibile creare un frammento da zero o salvare come frammento un pannello di moduli esistente.

   Per ulteriori informazioni sulla creazione di frammenti, vedere [Frammenti di moduli adattivi](../../forms/using/adaptive-form-fragments.md).

* **Identificare e contrassegnare**
i valori globaliLe transazioni basate su moduli comportano elementi dinamici per acquisire dati rilevanti dagli utenti ed elaborarli per semplificare la compilazione dei moduli. Ad esempio, nel modulo è presente il campo A nel frammento X il cui valore determina la validità del campo B in un altro frammento. In questo caso, se il frammento X è contrassegnato per il caricamento pigro, il valore del campo A deve essere disponibile per convalidare il campo B anche se il frammento X non è caricato. A tal fine, è possibile contrassegnare il campo A come globale, in modo che il relativo valore sia disponibile per la convalida del campo B quando il frammento X non è caricato.

   Per informazioni su come rendere il valore di un campo globale, vedere [Configurazione del caricamento pigro](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Regole di scrittura per controllare la visibilità dei**
campiI moduli contengono alcuni campi e sezioni che non sono applicabili a tutti gli utenti e in tutte le condizioni. Gli autori e gli sviluppatori di Forms utilizzano regole di visibilità o di visualizzazione per controllarne la visibilità in base agli input degli utenti. Ad esempio, il campo Indirizzo ufficio non viene visualizzato agli utenti che scelgono Disoccupato nel campo Stato occupazione di un modulo. Per ulteriori informazioni sulla scrittura di regole, vedere [Utilizzo dell&#39;editor di regole](../../forms/using/rule-editor.md).

   È possibile utilizzare le regole di visibilità nei frammenti caricati in modo da visualizzare i campi condizionali solo quando sono obbligatori. Inoltre, contrassegnare il campo condizionale come globale per farvi riferimento nell&#39;espressione di visibilità del frammento caricato in modo graduale.

## Configurazione del caricamento lento {#configuring-lazy-loading}

Per abilitare il caricamento lento su un frammento di modulo adattivo, effettuare le operazioni seguenti:

1. Aprire il modulo adattivo in modalità di creazione che contiene il frammento da abilitare per il caricamento pigro.
1. Selezionare il frammento di modulo adattivo e toccare ![cmppr](assets/cmppr.png).
1. Nella barra laterale, abilitare **[!UICONTROL Carica frammento in modo pigro]** e toccare **Fine**.

   ![Abilita caricamento lento per il frammento di modulo adattivo](assets/lazy-loading-fragment.png)

   Il frammento è ora abilitato per il caricamento pigro.

È possibile contrassegnare i valori degli oggetti nel frammento caricato in modo che siano disponibili per l&#39;uso negli script quando il frammento contenitore non è caricato. Effettua le seguenti operazioni:

1. Aprire il frammento di modulo adattivo in modalità di creazione.
1. Toccate il campo di cui desiderate contrassegnare il valore come globale, quindi toccate ![cmppr](assets/cmppr.png).
1. Nella barra laterale, attivare il valore **Usa durante il caricamento pigro**.

   ![Campo di caricamento pigro nella barra laterale](assets/enable-lazy-loading.png)

   Il valore è ora contrassegnato come globale e sarà disponibile per l&#39;uso negli script anche quando il frammento contenitore viene scaricato.

## Considerazioni e procedure ottimali per la configurazione del caricamento pigro {#considerations-and-best-practices-for-configuring-lazy-loading}

Alcune limitazioni, raccomandazioni e punti importanti da tenere a mente quando si lavora con il caricamento pigro sono i seguenti:

* È consigliabile utilizzare moduli adattivi basati sullo schema XSD su moduli adattivi basati su XFA per configurare il caricamento pigro sui moduli di grandi dimensioni. Il guadagno di prestazioni dovuto all&#39;implementazione pigra del caricamento nei moduli adattivi basati su XFA è relativamente inferiore al guadagno nei moduli adattivi basati su XSD.
* Non configurare il caricamento pigro sui frammenti in un modulo adattivo che utilizza **[!UICONTROL Responsive -tutto in una pagina senza il layout]** di navigazione per il pannello principale. A seguito della configurazione di layout reattivo, tutti i frammenti vengono caricati contemporaneamente in un modulo adattivo. Può anche causare un peggioramento delle prestazioni.
* Si consiglia di non configurare il caricamento pigro sul primo frammento in un modulo adattivo.
* Si consiglia di non configurare il caricamento pigro sui frammenti nel primo pannello visualizzato al caricamento del modulo adattivo.
* Il caricamento dei layout è supportato fino a due livelli nella gerarchia dei frammenti.
* Assicurarsi che i campi contrassegnati come globali siano univoci all&#39;interno di un modulo adattivo.
* Valutare la possibilità di scrivere regole di visibilità per i frammenti da mostrare o nascondere in base a una condizione. Ad esempio, è possibile mostrare o nascondere il frammento Dettagli coniuge in base allo stato civile specificato da un utente.
* I componenti Allegati e Termini e Condizioni del file non sono supportati nei frammenti caricati lentamente.

### Best practice di scripting per la configurazione del caricamento pigro {#scripting-best-practices-for-configuring-lazy-loading}

I punti importanti da tenere a mente durante lo sviluppo di script per i pannelli di caricamento pigri sono i seguenti:

* Verificare che gli script di inizializzazione e di calcolo utilizzati nei campi di un frammento caricato pigro siano di natura ottimale. Gli script impotenti sono quelli che hanno lo stesso effetto anche dopo più esecuzioni.
* Utilizzare la proprietà globalmente disponibile dei campi per rendere disponibile il valore dei campi che si trovano in un pannello di caricamento pigro a tutti gli altri pannelli di un modulo.
* Non inoltrare il valore di riferimento di un campo all’interno di un pannello pigro, indipendentemente dal fatto che il campo sia contrassegnato o meno a livello globale tra i frammenti.
* Utilizzate la funzione di ripristino del pannello per ripristinare tutti gli elementi visibili nel pannello utilizzando la seguente espressione di clic.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;})).resetData()

