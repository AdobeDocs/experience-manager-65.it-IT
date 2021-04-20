---
title: Miglioramento delle prestazioni dei moduli di grandi dimensioni con caricamento lento
seo-title: Miglioramento delle prestazioni dei moduli di grandi dimensioni con caricamento lento
description: Il caricamento lento migliora notevolmente le prestazioni dei moduli adattivi grandi e complessi posticipando l’inizializzazione e il caricamento dei frammenti di modulo fino a quando non saranno visibili.
seo-description: Il caricamento lento migliora notevolmente le prestazioni dei moduli adattivi grandi e complessi posticipando l’inizializzazione e il caricamento dei frammenti di modulo fino a quando non saranno visibili.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---


# Migliorare le prestazioni dei moduli di grandi dimensioni con caricamento lento{#improve-performance-of-large-forms-with-lazy-loading}

## Introduzione al caricamento lento {#introduction-to-lazy-loading}

Quando il modulo diventa grande e complesso con centinaia e migliaia di campi, gli utenti finali riscontrano un lungo tempo di risposta durante il rendering dei moduli in fase di esecuzione. Per ridurre al minimo il tempo di risposta, i moduli adattivi consentono di suddividere i moduli in frammenti logici e configurarli per posticipare l’inizializzazione o il caricamento dei frammenti fino a quando il frammento non deve essere visibile. Viene definito carico pigro. Inoltre, i frammenti configurati per il caricamento lento vengono scaricati quando l’utente passa ad altre sezioni del modulo e i frammenti non sono più visibili.

Prima di configurare il caricamento lento, comprendiamo i requisiti e i passaggi preparatori.

## Preparazione alla configurazione del caricamento lento {#preparing-to-configure-lazy-loading}

Prima di configurare il caricamento lento dei frammenti nel modulo adattivo, è importante definire strategie per creare frammenti, identificare i valori utilizzati negli script o a cui si fa riferimento in altri frammenti e definire regole per controllare la visibilità dei campi nei frammenti caricati in modo lento.

* **Identificare e creare**
i frammentiÈ possibile configurare solo frammenti di modulo adattivi per il caricamento lento. Un frammento è un segmento autonomo che si trova al di fuori di un modulo adattivo e può essere riutilizzato nei diversi moduli. Quindi, il primo passo verso l&#39;implementazione del caricamento pigro è quello di identificare le sezioni logiche in un modulo e convertirle in frammenti. È possibile creare un frammento da zero o salvare come frammento un pannello di modulo esistente.

   Per ulteriori informazioni sulla creazione dei frammenti, vedere [Frammenti di modulo adattivo](../../forms/using/adaptive-form-fragments.md).

* **Identificare e contrassegnare**
i valori globaliLe transazioni basate su moduli coinvolgono elementi dinamici per acquisire dati rilevanti dagli utenti ed elaborarli per semplificare l’esperienza di compilazione dei moduli. Ad esempio, nel modulo è presente il campo A nel frammento X il cui valore determina la validità del campo B in un altro frammento. In questo caso, se il frammento X è contrassegnato per il caricamento lento, il valore del campo A deve essere disponibile per convalidare il campo B anche quando il frammento X non è caricato. A questo scopo, è possibile contrassegnare il campo A come globale, in modo che il relativo valore sia disponibile per la convalida del campo B quando il frammento X non è caricato.

   Per informazioni su come rendere globale un valore di campo, consulta [Configurazione del caricamento lento](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Regole di scrittura per controllare la visibilità dei**
campiI moduli includono alcuni campi e sezioni non applicabili a tutti gli utenti e in tutte le condizioni. Gli autori e gli sviluppatori di Forms utilizzano regole di visibilità o di visualizzazione per controllarne la visibilità in base agli input degli utenti. Ad esempio, il campo Indirizzo ufficio non viene visualizzato agli utenti che scelgono Disoccupato nel campo Stato impiego di un modulo. Per ulteriori informazioni sulla scrittura delle regole, consulta [Utilizzo dell&#39;editor di regole](../../forms/using/rule-editor.md).

   Puoi sfruttare le regole di visibilità nei frammenti caricati in modo che i campi condizionali vengano visualizzati solo quando sono obbligatori. Inoltre, contrassegna il campo condizionale globale per farvi riferimento nell’espressione di visibilità del frammento caricato in modo lento.

## Configurazione del caricamento lento {#configuring-lazy-loading}

Esegui i seguenti passaggi per abilitare il caricamento lento su un frammento di modulo adattivo:

1. Apri il modulo adattivo in modalità di authoring contenente il frammento che desideri abilitare per il caricamento lento.
1. Seleziona il frammento di modulo adattivo e tocca ![cmppr](assets/cmppr.png).
1. Nella barra laterale, abilita **[!UICONTROL Carica frammento in modo lento]** e tocca **Fine**.

   ![Abilita caricamento lento per il frammento di modulo adattivo](assets/lazy-loading-fragment.png)

   Il frammento è ora abilitato per il caricamento lento.

È possibile contrassegnare come globali i valori degli oggetti contenuti nel frammento caricato in modo che siano disponibili per l’uso negli script quando il frammento contenitore non viene caricato. Effettua le seguenti operazioni:

1. Apri il frammento di modulo adattivo in modalità di authoring.
1. Toccare il campo di cui si desidera contrassegnare il valore come globale, quindi toccare ![cmppr](assets/cmppr.png).
1. Nella barra laterale, abilita **Usa valore durante il caricamento lento**.

   ![Campo di carico pigro nella barra laterale](assets/enable-lazy-loading.png)

   Il valore è ora contrassegnato come globale e sarà disponibile per l’uso negli script anche quando il frammento contenitore viene scaricato.

## Considerazioni e best practice per la configurazione del caricamento lento {#considerations-and-best-practices-for-configuring-lazy-loading}

Alcune limitazioni, raccomandazioni e punti importanti da tenere a mente quando si lavora con il caricamento lento sono i seguenti:

* Si consiglia di utilizzare moduli adattivi basati su schema XSD su moduli adattivi basati su XFA per configurare il caricamento lento su moduli di grandi dimensioni. Il guadagno di prestazioni dovuto all&#39;implementazione lenta del caricamento nei moduli adattivi basati su XFA è relativamente inferiore rispetto al guadagno nei moduli adattivi basati su XSD.
* Non configurare il caricamento lento sui frammenti in un modulo adattivo che utilizza **[!UICONTROL Responsive -all&#39;interno di una pagina senza il layout di navigazione]** per il pannello principale. A seguito della configurazione del layout reattivo, tutti i frammenti vengono caricati contemporaneamente in un modulo adattivo. Può anche causare prestazioni degradate.
* Si consiglia di non configurare il caricamento lento sul primo frammento in un modulo adattivo.
* Si consiglia di non configurare il caricamento lento sui frammenti nel primo pannello che esegue il rendering al caricamento del modulo adattivo.
* Nella gerarchia dei frammenti è supportato un massimo di due livelli.
* Assicurati che i campi contrassegnati come globali siano univoci all&#39;interno di un modulo adattivo.
* È consigliabile scrivere regole di visibilità per i frammenti che devono essere visualizzati o nascosti in base a una condizione. Ad esempio, è possibile mostrare o nascondere il frammento Dettagli coniuge in base allo stato civile specificato da un utente.
* I componenti Allegati file e Termini e condizioni non sono supportati nei frammenti caricati in modo lento.

### Best practice di scripting per la configurazione del caricamento lento {#scripting-best-practices-for-configuring-lazy-loading}

I punti importanti da tenere a mente durante lo sviluppo di script per pannelli di caricamento lenti sono i seguenti:

* Assicurati che gli script di inizializzazione e di calcolo utilizzati nei campi di un frammento caricato con layout siano idempotenti in natura. Gli script impotenti sono quelli che hanno lo stesso effetto anche dopo più esecuzioni.
* Utilizzare la proprietà disponibile a livello globale dei campi per rendere disponibile il valore dei campi situati in un pannello di caricamento lento a tutti gli altri pannelli di un modulo.
* Non inoltrare il valore di riferimento di un campo all’interno di un pannello pigro indipendentemente dal fatto che il campo sia contrassegnato o meno a livello globale tra i frammenti.
* Utilizza la funzione di reimpostazione del pannello per reimpostare tutti gli elementi visibili nel pannello utilizzando la seguente espressione di clic.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;}).resetData()

