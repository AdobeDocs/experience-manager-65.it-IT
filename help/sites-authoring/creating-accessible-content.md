---
title: Creazione di contenuto accessibile per Adobe Experience Manager (conformità WCAG 2.1)
description: Utilizzare AEM per rendere i contenuti web accessibili e utilizzabili da persone con disabilità
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '13956'
ht-degree: 99%

---

# Creazione di contenuto accessibile (conformità WCAG 2.1) {#creating-accessible-content-wcag-conformance}

Le [linee guida per l’accessibilità dei contenuti web (WCAG) 2.1](https://www.w3.org/TR/WCAG/), preparate da [un gruppo di lavoro del World Wide Wec Consortium](https://www.w3.org/Consortium/activities#Accessibility_Guidelines_Working_Group), sono costituite da un insieme di criteri di successo e linee guida che non dipendono dalla tecnologia in uso e hanno l’obiettivo di rendere i contenuti web accessibili e utilizzabili dalle persone con disabilità.

Come introduzione, viene fornito un elenco di sezioni e documenti di supporto:

* [Nuove funzioni nelle linee guida WCAG 2.1](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [Come soddisfare le linee guida WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Informazioni sulle linee guida WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [Tecniche per WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/)
* [Documentazione delle linee guida WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

Inoltre, vedi:
* [Guida rapida alle linee guida WCAG 2.1](/help/managing/qg-wcag.md).
* [Rapporti sulla conformità per l’accessibilità relativi alle soluzioni Adobe](https://www.adobe.com/accessibility/compliance.html).
* [Configurazione dell’editor Rich Text per produrre contenuti accessibili](/help/sites-administering/rte-accessible-content.md)

Le linee guida sono classificate in base a tre livelli di conformità: livello A (il più basso), livello AA e livello AAA (il più alto). Brevemente, i livelli sono definiti come segue:

* **Livello A**: il sito ha raggiunto un livello minimo di accessibilità di base. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A.
* **Livello AA**: si tratta di un livello di accessibilità ideale da porsi come obiettivo, in cui il sito raggiunge un livello di accessibilità di base, affinché sia accessibile al maggior numero di persone nella gran parte delle situazioni e con l’utilizzo di più tecnologie possibili. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A e livello AA.
* **Livello AAA**: il sito ha raggiunto un livello molto alto di accessibilità. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A, AA e AAA.

Quando si crea un sito, è necessario determinare il livello complessivo che si desidera ottenere.

Nella sezione seguente sono illustrate le [basi delle linee guida WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance), oltre ai criteri di successo correlati per i [livelli di conformità](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) A e AA.

>[!NOTE]
>
>In questo documento vengono utilizzati:
>
>* I [nomi brevi per le linee guida WCAG 2.1](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance).
>* La [numerazione utilizzata nelle linee guida WCAG 2.1](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1) per facilitare i riferimenti incrociati al sito web WCAG.


## Principio 1: Percepibile  {#principle-perceivable}

[Principio 1: Percepibile - Informazioni e componenti dell’interfaccia utente devono essere presentati agli utenti con modalità da loro percepibili.](https://www.w3.org/TR/WCAG/#perceivable)

### Alternative testuali (1.1)  {#text-alternatives}

[Linea guida 1.1 - Alternative testuali: fornire alternative testuali per qualsiasi contenuto non testuale in modo che possa essere convertito in altri formati richiesti, come la stampa a caratteri grandi, il Braille, la sintesi vocale, i simboli o un linguaggio più semplice.](https://www.w3.org/TR/WCAG/#text-alternatives)

### Contenuto non testuale (1.1.1)  {#non-text-content}

* Criterio di successo 1.1.1
* Livello A
* Contenuto non testuale: tutto il contenuto non testuale presentato all’utente dispone di un’alternativa testuale che svolge la finalità equivalente, fatta eccezione per le situazioni elencate di seguito.

#### Finalità: contenuto non testuale (1.1.1) {#purpose-non-text-content}

Le informazioni su una pagina web possono essere fornite in diversi formati non testuali, ad esempio immagini, video, animazioni, tabelle e grafici. Le persone non vedenti o con gravi problemi visivi non sono in grado di vedere il contenuto non testuale, ma possono accedere ai contenuti testuali letti mediante un’utilità per la lettura dello schermo o presentati in forma tattile da un dispositivo Braille. Così, grazie alla disponibilità di alternative testuali al contenuto in formato grafico, i non vedenti possono accedere a una versione equivalente delle informazioni veicolate.

Un ulteriore vantaggio è rappresentato dal fatto che le alternative testuali consentono l’indicizzazione dei contenuti non testuali da parte dei motori di ricerca.

#### Come soddisfare il criterio - Contenuto non testuale (1.1.1)  {#how-to-meet-non-text-content}

Per gli elementi grafici statici, il requisito fondamentale consiste nel fornire un&#39;alternativa testuale equivalente. Ciò può essere effettuato tramite il campo **Testo alternativo**, vedi ad esempio l’**[Immagine](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/components/image.html)** del componente di base.

>[!NOTE]
>
>Alcuni componenti di base predefiniti, come il **[carosello](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)**, non forniscono un campo di **testo alternativo** per l’aggiunta di descrizioni testuali alternative alle singole immagini, anche se il campo **Etichetta** è disponibile nella scheda per l’**[accessibilità](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/components/carousel.html#accessibility-tab)** dell’intero componente.
>
>Quando implementi le versioni di questi componenti per l’istanza AEM, il team di sviluppo dovrà configurarli per supportare l’attributo `alt`, affinché gli autori possano aggiungerlo al contenuto (consulta [Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

In AEM il campo **Testo alternativo** deve essere compilato per impostazione predefinita. Se l’immagine è puramente decorativa e un testo alternativo sarebbe superfluo, seleziona l’opzione **L’immagine è decorativa**.

#### Creazione di buone alternative di testo {#creating-good-text-alternatives}

Esistono varie forme di contenuti non testuali, di conseguenza il valore del testo alternativo dipende dal ruolo dell’elemento grafico all’interno della pagina web. Alcune regole generali da seguire:

* Le alternative testuali dovrebbero essere sintetiche ma veicolare chiaramente le informazioni essenziali fornite dal contenuto non testuale.
* È bene evitare descrizioni eccessivamente lunghe (oltre 100 caratteri). Se un testo alternativo richiede una descrizione più dettagliata:
   * fornisci una breve descrizione nel testo alternativo
   * e includi una descrizione più lunga in un altro elemento di testo, nella stessa pagina o in una pagina web separata. Inserisci un collegamento a questa descrizione separata rendendo l’immagine un collegamento o inserendo un collegamento di testo accanto all’immagine.
* Il testo alternativo non dovrebbe replicare il contenuto fornito sotto forma di testo nella stessa pagina. Ricorda che molte immagini sono illustrazioni di punti già trattati nel testo di una pagina, di conseguenza un’alternativa testuale dettagliata potrebbe già esistere.
* Se il contenuto non testuale è un collegamento a un’altra pagina o un altro documento e non esiste altro testo che faccia parte dello stesso collegamento, il testo alternativo per l’immagine non dovrà descrivere l’immagine ma dovrà invece indicare la destinazione del collegamento.
* Se il contenuto non testuale è incluso in un elemento pulsante e non esiste testo che faccia parte dello stesso pulsante, il testo alternativo per l’immagine non dovrà descrivere l’immagine, ma piuttosto indicare la funzionalità del pulsante.
* È perfettamente accettabile associare a un’immagine un testo alternativo vuoto (null), ma solo se l’immagine non richiede testo alternativo (ad esempio, se si tratta di un elemento grafico puramente decorativo) o se il testo equivalente è già incluso nel testo della pagina.

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

Tipi specifici di contenuto non testuale che richiedono alternative testuali potrebbero includere:

* Foto illustrative: queste sono immagini di persone, oggetti o luoghi. È importante considerare il ruolo della foto nella pagina. In genere, è consigliabile descrivere il contenuto dell’immagine, in quanto la tecnologia per l’accessibilità annuncia il tipo di elemento (ad esempio, `graphic` o `image`). Per maggiore chiarezza, è possibile utilizzare `screenshot` o `illustration` nelle descrizioni di testo alternative, ma questo dipende dal contesto. La coerenza è un fattore essenziale ed è quindi importante che la decisione venga presa per un intero team di authoring e applicata uniformemente in tutta l’esperienza utente.
* Icone: Si tratta di piccoli pittogrammi (immagini) che veicolano informazioni specifiche. Devono essere utilizzati in modo coerente all’interno di una pagina e del sito. Tutte le istanze dell’icona in una pagina o in un sito devono avere lo stesso testo alternativo, breve e sintetico, a meno che questo determini inutili duplicazioni di testo adiacente.
* Grafici e diagrammi: solitamente rappresentano dati numerici. Di conseguenza, un possibile testo alternativo potrebbe consistere in una breve sintesi delle principali tendenze indicate nel diagramma o grafico. Se necessario, fornisci anche una descrizione più dettagliata nel testo utilizzando il campo **Descrizione** nella scheda **Avanzate** delle proprietà dell’immagine. In aggiunta, è possibile fornire i dati di origine in formato tabellare altrove nella pagina o nel sito.
* Mappe, diagrammi, diagrammi di flusso: per gli elementi grafici che forniscono dati spaziali (ad esempio, per la descrizione di relazioni tra oggetti o un processo), assicurati che il messaggio principale venga comunicato in formato testuale e che tali informazioni testuali vengano posizionate in prossimità di ciascun punto di dati associato. Per le mappe, potrebbe non risultare pratico fornire un equivalente di testo completo. Se la mappa ha lo scopo di aiutare le persone a individuare una posizione particolare, il testo alternativo dell’immagine della mappa può indicare brevemente *Mappa di X*, fornendo poi le indicazioni per tale posizione in un altro testo della pagina o attraverso il campo **Descrizione**, disponibile nella scheda **Avanzate** del componente **Immagine**.
* CAPTCHA: è l’acronimo di “*Completely Automated Public Turing test to tell Computers and Humans Apart*” (test di Turing completamente automatizzato per distinguere macchine e persone). Viene utilizzato come controllo di sicurezza nelle pagine web per distinguere esseri umani da software dannosi, ma che può rappresentare un ostacolo all’accessibilità. Si tratta di immagini che richiedono agli utenti di descrivere ciò che vedono, al fine di superare un test di sicurezza. Fornire un testo alternativo per l’immagine non è ovviamente possibile, quindi sarà necessario prendere in considerazione soluzioni alternative non grafiche. Il W3C fornisce una serie di suggerimenti (ciascuno dei quali presenta vantaggi e svantaggi), ad esempio:
   * Puzzle logici
   * L’impiego di output audio anziché di immagini
   * Account a utilizzo limitato e filtri anti-spam.
* Immagini di sfondo: sono ottenute utilizzando i CSS (Cascading Style Sheets, fogli di stile a cascata) anziché in HTML, e non è quindi possibile specificare un valore di testo alternativo. Pertanto le immagini di sfondo non dovrebbero includere informazioni testuali importanti, a meno che non siano incluse anche nel testo della pagina. Tuttavia, è importante utilizzare uno sfondo alternativo per i casi in cui l’immagine non possa essere visualizzata.

>[!NOTE]
>
>Dovrebbe essere previsto un livello adeguato di contrasto tra lo sfondo e il testo in primo piano; questo elemento viene discusso più dettagliatamente in [Contrasto (minimo) (1.4.3)](#contrast-minimum).

#### Ulteriori informazioni - Contenuto non testuale (1.1.1)  {#more-information-non-text-content}

* [Comprendere i criteri di successo 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [Come soddisfare i criteri di successo 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [Spiegazione W3C dei CAPTCHA e relative alternative](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### Media temporizzati (1.2)  {#time-based-media}

[Linea guida 1.2 - Media temporizzati: fornire alternative per gli elementi multimediali temporizzati.](https://www.w3.org/TR/WCAG/#time-based-media)

Questo argomento riguarda i contenuti web *temporizzati*, ossia contenuti che l’utente può riprodurre (come video, audio e contenuti animati) e che possono essere preregistrati o in streaming.

### Solo audio e solo video (preregistrati) (1.2.1) {#audio-only-and-video-only-prerecorded}

* Criterio di successo 1.2.1
* Livello A
* Solo audio e solo video (preregistrati): per gli elementi solo video e solo audio preregistrati vale quanto segue, tranne quando l’audio o il video sia un elemento alternativo per il testo, chiaramente indicato come tale:
   * Solo audio preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati che presenti le informazioni equivalenti ai contenuti solo audio preregistrati.
   * Solo video preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati o una traccia audio che presenti le informazioni equivalenti ai contenuti solo video preregistrati.

#### Finalità - Solo audio e solo video (preregistrati) (1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

Problemi di accessibilità per video e audio possono essere riscontrati da:

* Persone con problemi visivi in assenza di audio o quando l’audio non è sufficiente a informarli di ciò che sta accadendo nel video o nell’animazione;
* Persone con disabilità uditive o non udenti, non in grado di sentire l’audio;
* Persone che possono sentire l’audio, ma non comprendono i dialoghi (ad esempio, perché si svolgono in una lingua che non conoscono).

Video o audio possono anche essere non disponibili per chi utilizza browser o dispositivi che non supportano la riproduzione di contenuti in formati multimediali specifici, come Adobe Flash.

Fornire queste informazioni in un formato diverso, ad esempio testo (o audio per i video senza audio) può renderle accessibili alle persone impossibilitate ad accedere al contenuto originale.

#### Come soddisfare il criterio - Solo audio e solo video (preregistrati) (1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* Se il contenuto è una traccia audio preregistrata senza video (come un podcast):
   * Fornisci un collegamento immediatamente prima o dopo il contenuto, che rimandi a una trascrizione in formato testo del contenuto audio. La trascrizione dovrebbe essere una pagina HTML con un equivalente testuale di tutti i contenuti parlati e non parlati rilevanti, oltre all’indicazione di chi sta parlando, una descrizione dell’ambientazione, le espressioni vocali e una descrizione di qualsiasi altro elemento sonoro significativo.
* Se il contenuto è un’animazione o un video preregistrato senza audio:
   * Fornisci un collegamento immediatamente prima o dopo il contenuto, che rimandi a una descrizione testuale equivalente delle informazioni fornite nel video.
   * Oppure fornisci una descrizione audio equivalente in un formato audio comunemente utilizzato, come MP3.

>[!NOTE]
>
>Se il contenuto audio o video è fornito come alternativa a contenuto già esistente in un altro formato nella stessa pagina web, potrebbe non essere necessario specificare un’ulteriore alternativa.
>
>Le linee guida [Comprendere WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html) forniscono ulteriori informazioni.

L’inserimento di contenuti multimediali nelle pagine web AEM è simile a quello di un’immagine. Tuttavia, dato che i contenuti multimediali sono molto più di un fermo immagine, esistono differenti impostazioni e opzioni per controllarne la riproduzione.

>[!NOTE]
>
>Quando utilizzi elementi multimediali con contenuti informativi, è necessario creare anche collegamenti a contenuti alternativi. Ad esempio, per includere una trascrizione testuale, crea una pagina HTML per visualizzare la trascrizione e quindi aggiungi un collegamento accanto o sotto al contenuto audio.

#### Ulteriori informazioni - Solo audio e solo video (preregistrati) (1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [Comprendere i criteri di successo 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [Come soddisfare i criteri di successo 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### Sottotitoli (preregistrati) (1.2.2) {#captions-prerecorded}

* Criterio di successo 1.2.2
* Livello A
* Sottotitoli (preregistrati): i sottotitoli vengono forniti per tutti i contenuti audio preregistrati negli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo e chiaramente indicato come tale.

#### Finalità - Sottotitoli (preregistrati) (1.2.2) {#purpose-captions-prerecorded}

Le persone non udenti o ipoudenti non saranno in grado di accedere ai contenuti audio o avranno gravi difficoltà di accesso. I sottotitoli sono equivalenti testuali dell’audio, parlato e non, visualizzati sullo schermo al momento opportuno nel corso del video. Consentono a chi non può udire l’audio di comprendere cosa sta succedendo.

#### Come soddisfare il criterio - Sottotitoli (preregistrati) (1.2.2) {#how-to-meet-captions-prerecorded}

I sottotitoli possono essere:

* Sottotitoli non codificati: sempre visibili durante la riproduzione del video
* Sottotitoli codificati: possono essere attivati o disattivati dall’utente

Se possibile, utilizza i sottotitoli codificati in modo da consentire agli utenti di scegliere se visualizzarli o meno.

Per i sottotitoli codificati è necessario creare e fornire, unitamente al file video, un file di sottotitoli sincronizzati in un formato appropriato, ad esempio [SMIL](https://www.w3.org/AudioVideo/). I dettagli su come effettuare questa operazione vanno oltre lo scopo di questa guida, ma abbiamo incluso collegamenti ad alcune esercitazioni nella sezione [Ulteriori informazioni - Sottotitoli (preregistrati) (1.2.2)](#more-information-captions-prerecorded). Assicurati di includere una nota o di attivare la funzione dei sottotitoli nel lettore video per informare gli utenti che per il video sono disponibili i sottotitoli.

Se è necessario utilizzare sottotitoli non codificati, inserisci il testo nella traccia video. A questo scopo è possibile utilizzare applicazioni di editing video che consentono di sovrapporre i sottotitoli al video.

#### Ulteriori informazioni - Sottotitoli (preregistrati) (1.2.2) {#more-information-captions-prerecorded}

* [Comprendere i criteri di successo 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [Come soddisfare i criteri di successo 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### Audiodescrizione o tipo di media alternativo (preregistrato) (1.2.3) {#audio-description-or-media-alternative-prerecorded}

* Criterio di successo 1.2.3
* Livello A
* Audiodescrizione o tipo di media alternativo (preregistrato): viene fornita un’alternativa per gli elementi multimediali temporizzati o una descrizione audio del contenuto video preregistrato per gli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo, e chiaramente indicato come tale.

#### Finalità - Audiodescrizione o tipo di media alternativo (preregistrato) (1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

Se le informazioni in un video o in un’animazione vengono fornite solo visivamente oppure se l’audio non fornisce informazioni sufficienti per consentire la comprensione di ciò che viene visualizzato, le persone non vedenti o ipovedenti dovranno superare ostacoli di accessibilità.

#### Come soddisfare il criterio - Audiodescrizione o tipo di media alternativo (preregistrato) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

Gli approcci che è possibile adottare per soddisfare questo criterio di successo sono due. È possibile:

1. Includere una descrizione audio aggiuntiva per il contenuto video. Questo può essere ottenuto in tre modi:
   * In corrispondenza delle pause nella finestra di dialogo, fornisci informazioni sui cambiamenti della scena che non sono inclusi nella traccia audio esistente;
   * Includi una nuova traccia audio, aggiuntiva e facoltativa, contenente l’audio originale, ma anche informazioni audio ulteriori sui cambiamenti della scena.
      * Questo consente agli utenti di passare dalla traccia audio esistente (che *non* contiene una descrizione audio) alla nuova traccia audio (che *contiene* una descrizione audio), e viceversa.
      * In questo modo si evitano interruzioni per gli utenti che non necessitano della descrizione aggiuntiva.
   * Crea una seconda versione del contenuto video per consentire descrizioni audio estese. Questo riduce le difficoltà connesse con la fornitura di descrizioni audio dettagliate all’interno delle pause nella finestra di dialogo esistente, interrompendo temporaneamente audio e video nei momenti adeguati. Come risultato, è possibile fornire una descrizione audio molto più lunga prima che l’azione riprenda. Come nell’esempio precedente, l’ideale, in questo caso, è includere una traccia audio facoltativa per evitare interruzioni agli utenti che non necessitano della descrizione aggiuntiva.
1. Fornisci una trascrizione testuale che rappresenti un equivalente testuale adatto per gli elementi sonori e visivi del video o dell’animazione. Questi dovrebbero includere, a seconda del caso, l’indicazione di chi sta parlando, una descrizione dell’ambientazione eventuali eventi o informazioni presentate visivamente ed espressioni vocali. A seconda della lunghezza, è possibile inserire la trascrizione nella stessa pagina del video o dell’animazione oppure in una pagina separata; se scegli la seconda opzione, includi un collegamento alla trascrizione accanto al video o all’animazione.

La descrizione dettagliata delle modalità di creazione di video con descrizione audio esula dallo scopo di questa guida. La creazione di video e descrizioni audio può richiedere parecchio tempo, ma puoi ricorrere ad altri prodotti Adobe per facilitare l’esecuzione di tali attività.

#### Ulteriori informazioni - Audiodescrizione o tipo di media alternativo (preregistrato) (1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [Comprendere i criteri di successo 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [Come soddisfare i criteri di successo 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### Sottotitoli (in tempo reale) (1.2.4)    {#captions-live}

* Criterio di successo 1.2.4
* Livello AA
* Sottotitoli (in tempo reale): i sottotitoli vengono forniti per tutti i contenuti audio dal vivo negli elementi multimediali sincronizzati.

#### Finalità - Sottotitoli (in tempo reale) (1.2.4)  {#purpose-captions-live}

Questo criterio di successo è identico a [Sottotitoli (preregistrati)](#captions-prerecorded), in quanto riguarda la rimozione degli ostacoli di accessibilità per persone non udenti o ipoudenti. Tuttavia questo criterio di successo è relativo a presentazioni in tempo reale, come i webcast.

#### Come soddisfare il criterio - Sottotitoli (in tempo reale) (1.2.4) {#how-to-meet-captions-live}

Segui le indicazioni fornite sopra per [Sottotitoli (preregistrati)](#captions-prerecorded). Dato che l’elemento multimediale è in tempo reale, tuttavia, i sottotitoli dovranno essere creati il più rapidamente possibile e in modo dinamico. Pertanto, dovresti considerare l’utilizzo di strumenti per la creazione di sottotitoli in tempo reale o di speech-to-text.

Istruzioni dettagliate al riguardo vanno oltre lo scopo di questo documento, ma informazioni utili sono reperibili tramite le risorse seguenti:

* [WebAIM: aggiunta di sottotitoli in tempo reale](https://www.webaim.org/techniques/captions/realtime.php)

* [Progetto AccessComputing (University of Washington): i sottotitoli possono essere generati automaticamente utilizzando il riconoscimento vocale?](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### Ulteriori informazioni - Sottotitoli (in tempo reale) (1.2.4)  {#more-information-captions-live}

* [Comprendere i criteri di successo 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [Come soddisfare i criteri di successo 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### Audiodescrizione (preregistrata) (1.2.5)   {#audio-description-prerecorded}

* Criterio di successo 1.2.5
* Livello AA
* Descrizione audio (preregistrato): una descrizione audio viene fornita per tutti i contenuti video preregistrati negli elementi multimediali sincronizzati.

#### Finalità: Audiodescrizione (preregistrata) (1.2.5) {#purpose-audio-description-prerecorded}

Questo criterio di successo è identico a [Audiodescrizione o tipo di media alternativo (preregistrato)](#audio-description-or-media-alternative-prerecorded), tranne per il fatto che gli autori devono fornire una descrizione audio molto più dettagliata per adeguarsi al livello AA.

#### Come soddisfare il criterio - Audiodescrizione (preregistrata) (1.2.5) {#how-to-meet-audio-description-prerecorded}

Segui le indicazioni fornite per [Audiodescrizione o tipo di media alternativo (preregistrato)](#audio-description-or-media-alternative-prerecorded).

#### Ulteriori informazioni - Audiodescrizione (preregistrata) (1.2.5) {#more-information-audio-description-prerecorded}

* [Comprendere i criteri di successo 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [Come soddisfare i criteri di successo 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### Adattabile (1.3)  {#adaptable}

[Linea guida 1.3 - Adattabile: creare contenuti che possano essere rappresentati in modalità differenti (ad esempio con un layout più semplice), senza perdere informazioni o struttura.](https://www.w3.org/TR/WCAG/#adaptable)

Questa linea guida riguarda i requisiti necessari per supportare le persone che:

* potrebbero non essere in grado di accedere alle informazioni proposte da un autore in una presentazione predefinita del contenuto, ad esempio in un layout a più colonne oppure in una pagina in cui viene fatto un notevole utilizzo di colore e/o immagini;

* potrebbero utilizzare una visualizzazione solo audio o alternativa, ad esempio con testo di grandi dimensioni e a contrasto elevato.

### Informazioni e correlazioni (1.3.1)    {#info-and-relationships}

* Criterio di successo 1.3.1
* Livello A
* Informazioni e correlazioni: informazioni, struttura e relazioni veicolate attraverso la presentazione possono essere determinate a livello di programmazione o sono disponibili in formato testo.

#### Finalità - Informazioni e correlazioni (1.3.1)  {#purpose-info-and-relationships}

Molte tecnologie per l’accessibilità utilizzate da persone con disabilità si basano su informazioni strutturali per visualizzare o *comprendere* i contenuti in modo efficace. Queste possono assumere la forma di titoli, intestazioni di righe e colonne di tabella, e tipi di elenchi. Ad esempio, un’utilità di lettura dello schermo potrebbe consentire a un utente di spostarsi all’interno di una pagina passando da un’intestazione a un’altra. Tuttavia, quando la struttura del contenuto della pagina dipende esclusivamente da uno stile visivo, anziché dal codice HTML sottostante, non sono presenti informazioni strutturali utilizzabili dalle tecnologie per l’accessibilità, il che ne limita la capacità di supportare la navigazione facilitata.

Questo criterio di successo esiste affinché tali informazioni strutturali vengano fornite a livello di programmazione tramite HTML o con altre tecniche di scrittura del codice, in modo che i browser e le tecnologie per l’accessibilità possano accedervi e sfruttarle.

#### Come soddisfare il criterio - Informazioni e correlazioni (1.3.1)  {#how-to-meet-info-and-relationships}

AEM consente di creare facilmente contenuti web significativi dal punto di vista semantico utilizzando gli elementi HTML appropriati. Apri i contenuti della pagina nell’editor Rich Text (un componente testo) e usa il menu **Formato paragrafo** (simbolo di paragrafo) per specificare l’elemento strutturale appropriato (ad esempio paragrafo, intestazione e così via).

Puoi assicurarti che alle pagine web sia associata la struttura corretta utilizzando, se necessario, i seguenti elementi:

* **Titoli**: se le funzioni di accessibilità dell’editor Rich Text sono abilitate, AEM offre 3 livelli di intestazione di pagina. Puoi utilizzarli per identificare sezioni e sottosezioni di contenuto. Titolo 1 rappresenta il livello di intestazione più alto, Titolo 3 quello più basso. L’amministratore di sistema può configurare il sistema per consentire l’utilizzo di più livelli di intestazione.

* **Elenchi**: è possibile utilizzare l’HTML per specificare tre diversi tipi di elenchi:
   * L’elemento `<ul>` viene utilizzato per gli elenchi *non ordinati* (puntati). Le singole voci di elenco sono identificate dall’elemento `<li>`. Nell’editor Rich Text, utilizza l’icona **Elenco puntato**.
   * L’elemento `<ol>`viene utilizzato per gli elenchi *numerati*. Le singole voci dell’elenco sono identificate dall’elemento `<li>`. Nell’editor Rich Text, utilizza l’icona **Elenco numerato**.

   Se desideri convertire contenuti esistenti in un determinato tipo di elenco, evidenzia il testo desiderato e seleziona il tipo di elenco. Come nel precedente esempio, che mostra come inserire un testo di paragrafo, gli elementi elenco adeguati verranno aggiunti automaticamente al codice HTML.

   In modalità a tutto schermo, sono visibili le singole icone **Elenco puntato** ed **Elenco numerato**. Se non è attiva la modalità a tutto schermo, le due opzioni sono disponibili dietro la singola icona **Elenchi**.

* **Tabelle**: le tabelle di dati devono essere identificate utilizzando gli elementi di tabella HTML:
   * un elemento `<table>`
   * un elemento `<tr>` per ogni riga della tabella
   * un elemento `<th>` per ogni intestazione di riga e colonna
   * un elemento `<td>` per ogni cella di dati

   In aggiunta, le tabelle accessibili fanno uso dei seguenti elementi e attributi:

   * L’elemento `<caption>` viene utilizzato per fornire una didascalia visibile per la tabella. Per impostazione predefinita, le didascalie vengono visualizzate centrate sopra la tabella, ma possono essere posizionate in modo appropriato utilizzando gli stili CSS. La didascalia è associata alla tabella a livello di programmazione, pertanto è un metodo utile per fornire un’introduzione al contenuto.
   * L’elemento `<summary>` aiuta gli utenti non vedenti a comprendere più facilmente le informazioni presentate all’interno di una tabella, fornendo una sintesi di ciò che un utente vedente può vedere. Risulta particolarmente utile quando si utilizzano layout di tabella complessi o non convenzionali (l’attributo non viene visualizzato nel browser, ma viene letto solo alle tecnologie per l’accessibilità).
   * L’attributo `scope` dell’elemento `<th>` viene utilizzato per indicare se una cella rappresenta un’intestazione per una particolare riga o colonna. Un approccio simile consiste nell’utilizzare gli attributi header e id in tabelle complesse, dove le celle di dati possono essere associate a una o più intestazioni.

   >[!NOTE]
   >
   >Per impostazione predefinita questi elementi e attributi non sono direttamente disponibili, anche se l’amministratore di sistema può aggiungere supporto per questi valori nella finestra di dialogo **Proprietà tabella** (consulta [Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

   Per aprire la finestra di dialogo **Tabella** in cui puoi selezionare le **Proprietà tabella**:

   * Definisci una **Didascalia** appropriata.
   * È consigliabile rimuovere eventuali valori predefiniti per **Larghezza**, **Altezza**, **Bordo**, **Margine celle**, **Spaziatura celle**. dato che queste proprietà possono essere impostate in un foglio di stile globale.

   Puoi quindi utilizzare le **Proprietà cella** per scegliere se la cella contiene dati o intestazione:

* **Enfasi**: utilizza l’elemento `<strong>` o `<em>` per indicare l’enfasi. Non utilizzare le intestazioni per evidenziare il testo all’interno dei paragrafi.
   * Evidenzia il testo che desideri mettere in evidenza.
   * Fai clic sull’icona **B** (per `<strong>`) oppure **I** (per `<em>`) nel pannello **Proprietà**, assicurandoti che sia selezionato HTML.

      >[!NOTE]
      >
      >L’editor Rich Text in un’installazione standard di AEM è configurato per utilizzare:
      >
      >* `<b>` per `<strong>`
      >* `<i>` per `<em>`

      >
      >L’efficacia è la medesima, ma `<strong>` e `<em>` sono preferibili in quanto rappresentano un html corretto dal punto di vista semantico. Il tuo team di sviluppo può configurare l’editor Rich Text in modo che utilizzi `<strong>` e `<em>` (anziché `<b>` e `<i>`) durante lo sviluppo dell’istanza di progetto.

* **Tabelle dati complesse**: in alcuni casi, in presenza di tabelle complesse con due o più livelli di intestazioni, le proprietà della tabella di base potrebbero non essere sufficienti a fornire tutte le informazioni strutturali necessarie. Per questo tipo di tabelle complesse, è necessario creare relazioni dirette tra le intestazioni e le celle correlate mediante gli attributi **header** e **id**.

   >[!NOTE]
   >
   >L’attributo id non è disponibile in un’installazione standard. Può essere attivato configurando regole HTML e il serializzatore nell’editor Rich Text.

   Ad esempio, nella tabella seguente le intestazioni e gli ID vengono abbinati per creare un’associazione programmatica per gli utenti di tecnologie per l’accessibilità.

   ```xml
     <table>
       <tr>
         <th rowspan="2" id="h">Homework</th>
         <th colspan="3" id="e">Exams</th>
         <th colspan="3" id="p">Projects</th>
       </tr>
       <tr>
         <th id="e1" headers="e">1</th>
         <th id="e2" headers="e">2</th>
         <th id="ef" headers="e">Final</th>
         <th id="p1" headers="p">1</th>
         <th id="p2" headers="p">2</th>
         <th id="pf" headers="p">Final</th>
       </tr>
       <tr>
         <td headers="h">15%</td>
         <td headers="e e1">15%</td>
         <td headers="e e2">15%</td>
         <td headers="e ef">20%</td>
         <td headers="p p1">10%</td>
         <td headers="p p2">10%</td>
         <td headers="p pf">15%</td>
       </tr>
     </table>
   ```

   A questo scopo, in AEM è necessario aggiungere il codice utilizzando direttamente la modalità di modifica sorgente.

   >[!NOTE]
   >
   >Questa funzionalità non è immediatamente disponibile in un’installazione standard. Richiede la configurazione dell’editor Rich Text, di regole HTML e del serializzatore.

#### Ulteriori informazioni - Informazioni e correlazioni (1.3.1)  {#more-information-info-and-relationships}

* [Comprendere i criteri di successo 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [Come soddisfare i criteri di successo 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### Sequenza significativa (1.3.2)   {#meaningful-sequence}

* Criterio di successo 1.3.2
* Livello A
* Sequenza significativa: quando la sequenza in cui il contenuto è presentato influisce sul suo significato, la corretta sequenza di lettura può essere determinata programmaticamente.

#### Finalità - Sequenza significativa (1.3.2) {#purpose-meaningful-sequence}

Lo scopo di questo criterio di successo è quello di consentire a un agente utente di fornire una presentazione alternativa del contenuto, conservando l’ordine di lettura necessario per comprendere il significato. È importante che sia possibile determinare programmaticamente almeno una sequenza del contenuto significativa. I contenuti che non soddisfano questo criterio di successo possono confondere o disorientare gli utenti se le tecnologie per l’accessibilità leggono il contenuto in ordine errato o se vengono applicati fogli di stile alternativi o altre modifiche di formattazione.

#### Come soddisfare il criterio - Sequenza significativa (1.3.2) {#how-to-meet-meaningful-sequence}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence).

#### Ulteriori informazioni - Sequenza significativa (1.3.2) {#more-information-meaningful-sequence}

* [Comprendere i criteri di successo 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [Come soddisfare i criteri di successo 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### Caratteristiche sensoriali (1.3.3)    {#sensory-characteristics}

* Criterio di successo 1.3.3
* Livello A
* Caratteristiche sensoriali: le istruzioni fornite per comprendere e intervenire sui contenuti non si basano unicamente su caratteristiche sensoriali dei componenti quali forma, dimensione, ubicazione visiva, orientamento o audio.

#### Finalità - Caratteristiche sensoriali (1.3.3)  {#purpose-sensory-characteristics}

Nel presentare le informazioni, i designer spesso si concentrano sulle caratteristiche di progettazione visiva come il colore, la forma, lo stile del testo o la posizione assoluta o relativa di un elemento di contenuto. Anche se queste possono essere tecniche di progettazione molto potenti per veicolare le informazioni (e possono migliorare l’accessibilità complessiva per normovedenti ma con particolari esigenze di accessibilità cognitive), le persone non vedenti o ipovedenti potrebbero non essere in grado di accedere alle informazioni che richiedono l’identificazione visiva di attributi come la posizione, il colore o la forma.

Allo stesso modo, le informazioni che richiedono di distinguere tra suoni diversi (ad esempio, contenuti parlati da voci di sesso maschile o femminile) presenteranno problemi di accessibilità per le persone con disabilità uditive, se non vengono incluse in un testo alternativo per il contenuto audio.

>[!NOTE]
>
>Per i requisiti collegati alle alternative ai colori, consulta [Utilizzo del colore](#use-of-color).

#### Come soddisfare il criterio - Caratteristiche sensoriali (1.3.3)  {#how-to-meet-sensory-characteristics}

Assicurati che tutte le informazioni che si basano su caratteristiche visive del contenuto di pagina siano presentate anche in un formato alternativo.

* Non fare affidamento sulla posizione visiva per fornire informazioni. Ad esempio, se desideri indirizzare gli utenti a un menu sul lato destro della pagina per l’accesso alle informazioni, non fare riferimento al *menu a destra*, ma denomina il menu (ad esempio attraverso un’intestazione) e fai riferimento al nome nel testo.
* Non fare affidamento sullo stile del testo (ad esempio, testo in grassetto o in corsivo) come unico modo per trasmettere le informazioni.

>[!NOTE]
>
>L’utilizzo di termini descrittivi sarà accettabile se questi hanno un significato in un contesto non visivo. Ad esempio, l’utilizzo dei termini *sopra* e *sotto* sarà generalmente accettabile, in quanto si riferiscono rispettivamente al contenuto prima e dopo un particolare elemento di contenuto; questa indicazione continuerà ad avere senso quando il contenuto è parlato.

#### Ulteriori informazioni - Caratteristiche sensoriali (1.3.3)  {#more-information-sensory-characteristics}

* [Comprendere i criteri di successo 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [Come soddisfare i criteri di successo 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### Distinguibile (1.4)  {#distinguishable}

[Linea guida 1.4 - Distinguibile: facilitare agli utenti la visione e l’ascolto dei contenuti, separando gli elementi in primo piano dallo sfondo.](https://www.w3.org/TR/WCAG/#distinguishable)

### Uso del colore (1.4.1)    {#use-of-color}

* Criterio di successo 1.4.1
* Livello A
* Utilizzo del colore: il colore non è utilizzato come unica modalità visiva per rappresentare le informazioni, indicare un’azione, richiedere una risposta o distinguere un elemento visivo.

>[!NOTE]
>
>Questo criterio di successo riguarda in particolare la percezione del colore. Altre forme di percezione sono illustrate in [Adattabilità (1.3)](#adaptable); compreso l’accesso programmatico al colore e ad altre codifiche presentazione visiva.

#### Finalità: utilizzo del colore (1.4.1) {#purpose-use-of-color}

Il colore è un modo efficace per valorizzare l’estetica delle pagine web ed è anche utile per trasmettere informazioni. Tuttavia, esistono una serie di problemi visivi, dalla cecità al daltonismo, che rendono alcune persone incapaci di distinguere tra alcuni colori. Questo rende la codifica tramite colori un modo inaffidabile per fornire informazioni.

Ad esempio, un soggetto con un deficit della visione dei colori rosso-verde non sarà in grado di distinguere tra sfumature di verde e di rosso. Potrà percepire entrambi i colori come un terzo (ad esempio, marrone), nel qual caso non sarà in grado di distinguere tra rosso, verde e marrone.

Inoltre, il colore non può essere percepito da persone che utilizzano browser di solo testo, dispositivi di visualizzazione in bianco e nero o una stampa in bianco e nero della pagina.

Un ulteriore aspetto da considerare è lo stato *selezionato* di un elemento dell’interfaccia, ad esempio schede e pulsanti di attivazione/disattivazione. Tale stato deve essere veicolato in un modo diverso rispetto al solo colore e a una semplice presentazione visiva. Per questi elementi può essere utile aggiungere pattern, forme e informazioni a livello di programmazione per creare un’esperienza completa, non basata su un senso specifico.

#### Come soddisfare il criterio - Uso del colore (1.4.1)  {#how-to-meet-use-of-color}

Qualunque colore sia utilizzato per trasmettere le informazioni, accertati che queste siano disponibili senza che sia necessario vedere il colore stesso.

Ad esempio, accertati che le informazioni fornite dal colore siano presenti in modo esplicito anche nel testo.

Se il colore viene usato come spunto per fornire informazioni, è necessario dare un ulteriore segnale visivo, ad esempio la modifica dello stile (grassetto, corsivo) o del font. Tutto questo favorisce l’identificazione delle informazioni da parte delle persone con problemi di vista o affette da daltonismo. Tuttavia, non vi si può fare completo affidamento, in quanto non aiuterà le persone che non possono vedere affatto la pagina. Per veicolare tali informazioni a utenti non vedenti, è in alcuni casi utile fornire testo nascosto o utilizzare soluzioni a livello di programmazione, come la [suite di standard web Accessible Rich Internet Applications (ARIA)](https://www.w3.org/WAI/standards-guidelines/aria/).

#### Ulteriori informazioni - Uso del colore (1.4.1) {#more-information-use-of-color}

* [Comprendere i criteri di successo 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [Come soddisfare i criteri di successo 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### Controllo del sonoro (1.4.2)   {#audio-control}

* Criterio di successo 1.4.2
* Livello A
* Controllo del sonoro: se un contenuto audio all’interno di una pagina web è eseguito automaticamente per più di tre secondi, occorre fornire una funzionalità per metterlo in pausa o interromperlo, oppure una modalità per il controllo dell’audio che sia indipendente dal controllo predefinito del sistema.

#### Finalità - Controllo del sonoro (1.4.2) {#purpose-audio-control}

Se contemporaneamente al sonoro del software per la lettura dello schermo è presente un’altra riproduzione audio, gli utenti che utilizzano tecnologie per l’accessibilità potrebbero avere difficoltà di ascolto dell’output sonoro. Questa difficoltà è accentuata quando l’output sonoro della lettura dello schermo è basato su software (come nel caso della maggior parte dei dispositivi attuali) ed è controllato tramite il medesimo controllo del volume per l’audio. Inoltre, alcune persone con disabilità cognitive e i soggetti neurodivergenti possono presentare una certa sensibilità al suono. Per questi utenti l’impossibilità di modificare il livello del volume dei contenuti audio può causare disturbi di una certa rilevanza.

Pertanto, è importante che l’utente abbia la possibilità di disattivare l’audio di sottofondo.

>[!NOTE]
>
>Nel controllo del volume è inclusa la possibilità di ridurre il livello a zero.

#### Come soddisfare il criterio - Controllo del sonoro (1.4.2) {#how-to-meet-audio-control}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control).

#### Ulteriori informazioni - Controllo del sonoro (1.4.2) {#more-information-audio-control}

* [Comprendere i criteri di successo 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [Come soddisfare i criteri di successo 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### Contrasto (minimo) (1.4.3)  {#contrast-minimum}

* Criterio di successo 1.4.3
* Livello AA
* Contrasto (minimo): la rappresentazione visiva di testo e immagini di testo ha un rapporto di contrasto pari ad almeno 4,5:1, fatta eccezione per i seguenti elementi:
   * Testo di grandi dimensioni: testo di grandi dimensioni e immagini di testo di grandi dimensioni hanno un rapporto di contrasto di almeno 3:1.
   * Incidentale: per il testo o per le immagini di testo che fanno parte di un componente dell’interfaccia inattivo, che sono [puramente decorative](https://www.w3.org/TR/WCAG/#dfn-pure-decoration), non visibili o che fanno parte di un’immagine che contiene altri contenuti visuali significativi, non è previsto alcun requisito di contrasto.
   * Logotipi: per il testo che fa parte di un logo o di un marchio non è previsto alcun requisito minimo di contrasto.

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta [Comprensione: Contrasto in contenuti non testuali](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html), per essere certo che i lettori comprendano meglio i requisiti aggiuntivi relativi agli elementi non testuali, tra cui icone ed elementi dell’interfaccia.

#### Finalità - Contrasto (minimo) (1.4.3)  {#purpose-contrast-minimum}

Le persone con determinate disabilità visive possono non essere in grado di distinguere tra alcune coppie di colori a basso contrasto. Queste persone possono riscontrare problemi di accessibilità se:

* Il testo contrasta poco con il relativo colore di sfondo.
* La codifica di colore del testo (come testo di collegamento e testo non di collegamento) è importante per distinguere le informazioni.

>[!NOTE]
>
>Il testo utilizzato esclusivamente per scopi decorativi è escluso da questo criterio di successo.

#### Come soddisfare il criterio - Contrasto (minimo) (1.4.3)  {#how-to-meet-contrast-minimum}

Assicurati che il testo contrasti a sufficienza con il relativo sfondo. I rapporti di contrasto dipendono dalle dimensioni e dallo stile del testo:

* Per testi con dimensioni inferiori a 18 punti (o 14 se in grassetto), il rapporto di contrasto tra testo/immagini di testo e sfondo deve essere pari ad almeno 4,5:1.
* Per testi con dimensioni almeno pari a 18 punti (o 14 se in grassetto), il rapporto di contrasto deve essere pari ad almeno 3:1.
* Se lo sfondo include un motivo, lo sfondo intorno al testo dovrà essere ombreggiato in modo da mantenere il rapporto di 4,5:1 o 3:1.

>[!NOTE]
>
>Ricorda che il rendering dei font varia a seconda delle dimensioni PT/PX/EM equivalenti.
>
>Ti consigliamo di seguire il buon senso e di privilegiare leggibilità e usabilità nella scelta di font e dimensioni appropriati per i contenuti web.

>[!NOTE]
>
>I seguenti siti possono esserti utili per le conversioni in altre unità:
>
>* [Px to Em Calculator - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [Font size conversion: pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com: PX to EM conversion made simple](http://pxtoem.com)


Per controllare i rapporti di contrasto, utilizza uno strumento di contrasto del colore, come ad esempio [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) o [l’utilità di controllo del contrasto di colore di WebAIM](https://www.webaim.org/resources/contrastchecker/). Questi strumenti consentono di controllare le coppie di colori ed evidenziano eventuali problemi di contrasto.

In alternativa, se la specificazione dell’aspetto della pagina non è un problema, è possibile scegliere di non specificare colori di sfondo e del testo in primo piano. In questo caso non sarà necessario alcun controllo del contrasto, in quanto sarà il browser dell’utente a determinare i colori del testo e dello sfondo.

Se non è possibile rispettare i livelli di contrasto raccomandati, sarà necessario fornire un collegamento a una versione alternativa ed equivalente della pagina (senza problemi di contrasto di colore) o consentire all’utente di regolare il contrasto dello schema di colore della pagina in base alle proprie esigenze.

#### Ulteriori informazioni - Contrasto (minimo) (1.4.3)  {#more-information-contrast-minimum}

* [Comprendere i criteri di successo 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [Come soddisfare i criteri di successo 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### Ridimensionamento del testo (1.4.4)   {#resize-text}

* Criterio di successo 1.4.4
* Livello A
* Ridimensionamento del testo: il testo, ad eccezione dei sottotitoli e delle immagini contenenti testo, può essere ridimensionato fino al 200 percento senza l’ausilio di tecnologie per l’accessibilità e senza perdita di contenuto e funzionalità.

#### Finalità - Ridimensionamento del testo (1.4.4) {#purpose-resize-text}

Lo scopo di questo criterio di successo è garantire che il rendering visivo di un testo (compresi i controlli basati sul testo, ovvero i caratteri di testo visualizzati in formato visivo [rispetto ai caratteri di testo ancora in formato dati, ad esempio ASCII]) possa essere ridimensionato in modo da consentire a persone con disabilità visive di lieve entità di leggere direttamente il testo senza utilizzare tecnologie per l’accessibilità, come una lente di ingrandimento dello schermo. Gli utenti possono trarre vantaggio dal ridimensionamento di tutto il contenuto della pagina web, ma il testo è l’elemento più importante.

#### Come soddisfare il criterio - Ridimensionamento del testo (1.4.4) {#how-to-meet-resize-text}

Oltre a seguire le linee guida in [Come soddisfare i criteri di successo 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text), puoi incoraggiare gli autori di contenuti a utilizzare larghezze e altezze fluide e flessibili per le strutture di pagina e le dimensioni dei font (ad esempio, design responsive) per consentire ai lettori di ridimensionare il testo.

#### Ulteriori informazioni - Ridimensionamento del testo (1.4.4) {#more-information-resize-text}

* [Comprendere i criteri di successo 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [Come soddisfare i criteri di successo 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### Immagini di testo (1.4.5)  {#images-of-text}

* Criterio di successo 1.4.5
* Livello AA
* Immagini di testo: se le tecnologie utilizzate consentono la presentazione visiva, per trasmettere informazioni viene utilizzato il testo, anziché le immagini di testo, con le seguenti eccezioni:
   * Personalizzabile: l’immagine di testo può essere personalizzata visivamente in base alle esigenze dell’utente;
   * Essenziale: una particolare presentazione del testo è essenziale per il tipo di informazioni veicolate.

>[!NOTE]
>
>I logotipi (testo che fa parte di un logo o di un marchio) sono considerati essenziali.

#### Finalità - Immagini di testo (1.4.5)  {#purpose-images-of-text}

Le immagini di testo vengono spesso utilizzate quando un particolare stile di testo è quello preferenziale (ad esempio un logo) o se il testo è stato generato da un’altra sorgente (ad esempio la scansione di un documento cartaceo). Tuttavia, rispetto al testo presentato in HTML e formattato mediante i CSS, le immagini di testo non hanno la flessibilità necessaria per modificarsi in dimensioni o aspetto nel modo che potrebbe essere necessario per le persone con disabilità visive o difficoltà di lettura.

#### Come soddisfare il criterio - Immagini di testo (1.4.5)  {#how-to-meet-images-of-text}

Se è necessario utilizzare le immagini di testo, utilizza CSS per sostituirle con testo equivalente in HTML, in modo che sia possibile personalizzare il testo. Per visualizzare un esempio di come ottenere questo risultato, consulta [C30: Utilizzare CSS per sostituire il testo con immagini di testo e fornire i comandi dell’interfaccia utente per effettuare il passaggio](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Ulteriori informazioni - Immagini di testo (1.4.5) {#more-information-images-of-text}

* [Comprendere i criteri di successo 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [Come soddisfare i criteri di successo 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## Principio 2: Utilizzabile  {#principle-operable}

[Principio 2: Utilizzabile - I componenti dell’interfaccia e la navigazione devono essere operabili.](https://www.w3.org/TR/WCAG/#operable)

### Accessibile da tastiera (2.1) {#keyboard-accessible}

[Linea guida 2.1 - Accessibile da tastiera: rendere disponibili tutte le funzionalità tramite tastiera.](https://www.w3.org/TR/WCAG/#keyboard-accessible)

È necessario che gli utenti possano accedere a tutte le funzionalità utilizzando una tastiera.

### Tastiera (2.1.1)   {#keyboard}

* Criterio di successo 2.1.1
* Livello A
* Tastiera: tutte le funzionalità del contenuto sono utilizzabili tramite un’interfaccia di tastiera senza richiedere tempi specifici per la pressione dei singoli tasti, salvo il caso in cui sia la funzionalità di fondo a richiedere un input che dipende dal percorso del movimento dell’utente e non solo dai suoi punti d’arrivo.

#### Finalità - Tastiera (2.1.1) {#purpose-keyboard}

Lo scopo di questo criterio di successo è garantire che, laddove possibile, il contenuto possa essere utilizzato tramite una tastiera o un’interfaccia per tastiera (che consenta l’utilizzo di una tastiera alternativa). Il contenuto gestibile tramite una tastiera o una tastiera alternativa può essere utilizzato da persone non vedenti (che non possono utilizzare dispositivi come il mouse, che richiede coordinazione occhio-mano), nonché da persone che devono utilizzare tastiere alternative o dispositivi di input che fungono da emulatori di tastiera. Gli emulatori di tastiera includono software di input vocale, software a soffio Sip/Puff, tastiere su schermo, software di scansione e una varietà di tecnologie per l’accessibilità e tastiere alternative. Gli utenti ipovedenti potrebbero avere difficoltà anche nel seguire un puntatore e trovare l’uso del software molto più semplice o possibile solo se controllabile tramite tastiera.

#### Come soddisfare il criterio - Tastiera (2.1.1) {#how-to-meet-keyboard}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard).

#### Ulteriori informazioni - Tastiera (2.1.1) {#more-information-keyboard}

* [Comprendere i criteri di successo 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Come soddisfare i criteri di successo 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### Nessun impedimento all’uso della tastiera (2.1.2)   {#no-keyboard-trap}

* Criterio di successo 2.1.2
* Livello A
* Nessun impedimento all’uso della tastiera: se tramite un’interfaccia di tastiera è possibile passare dalla tastiera a un componente della pagina, deve essere possibile anche il passaggio inverso mediante la stessa interfaccia di tastiera. Inoltre, se a tal fine non fosse sufficiente l’uso dei normali tasti freccia o Tab o l’uso di altri metodi di uscita standard, l’utente deve essere informato del metodo necessario per eseguire tale operazione.

#### Finalità - Nessun impedimento all’uso della tastiera (2.1.2) {#purpose-no-keyboard-trap}

Lo scopo di questo criterio di successo è garantire che il contenuto non *impedisca* di usare la tastiera all’interno di sottosezioni di contenuto su una pagina web. Si tratta di un problema comune se in una pagina sono combinati più formati riprodotti tramite plug-in o applicazioni incorporate.

In alcuni casi, la funzionalità della pagina web limita lo stato attivo a una sottosezione del contenuto, ad esempio una finestra di dialogo modale. In tali casi, devi fornire un metodo che consenta a un utente di uscire da tale sottosezione di contenuto, ad esempio il tasto ESC o un pulsante Chiudi per chiudere la finestra di dialogo modale.

#### Come soddisfare il criterio - Nessun impedimento all’uso della tastiera (2.1.2) {#how-to-meet-no-keyboard-trap}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap).

#### Ulteriori informazioni - Nessun impedimento all’uso della tastiera (2.1.2) {#more-information-no-keyboard-trap}

* [Comprendere i criteri di successo 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [Come soddisfare i criteri di successo 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### Adeguata disponibilità di tempo (2.2) {#enough-time}

[Linea guida 2.2 - Adeguata disponibilità di tempo: fornire agli utenti tempo sufficiente per leggere e utilizzare i contenuti.](https://www.w3.org/TR/WCAG/#enough-time)

L’obiettivo di questo criterio è garantire agli utenti tempo sufficiente per leggere e utilizzare i contenuti.

### Regolazione tempi di esecuzione (2.2.1)   {#timing-adjustable}

* Criterio di successo 2.2.1
* Livello A
* Tastiera: fornire agli utenti tempo sufficiente per leggere e utilizzare i contenuti.

#### Finalità - Regolazione tempi di esecuzione (2.2.1) {#purpose-timing-adjustable}

Lo scopo di questo criterio di successo è garantire che gli utenti disabili abbiano il tempo necessario per interagire con i contenuti web tutte le volte che è possibile. Le persone con disabilità quali cecità, ipovisione, limitazioni della destrezza o cognitive potrebbero avere bisogno di più tempo per leggere il contenuto o per eseguire azioni come la compilazione di moduli online. Se le funzioni web sono dipendenti dai tempi di esecuzione, per alcuni utenti sarà difficile eseguire l’azione richiesta entro i tempi stabiliti. Ciò potrebbe rendere il servizio inaccessibile. La progettazione di funzioni indipendenti dai tempi di esecuzione consente alle persone con disabilità di completare queste operazioni con successo. Le opzioni che consentono di disattivare il limite di tempo, personalizzarlo e regolarlo prima di raggiungerlo oppure estenderlo prima dello scadere permettono di completare le attività anche agli utenti che hanno bisogno di tempi più lunghi. Le opzioni sono elencate secondo l’ordine più utile per l’utente. La disattivazione dei limiti di tempo è migliore rispetto alla personalizzazione e quest’ultima, a sua volta, è migliore della richiesta di estensione prima dello scadere.

#### Come soddisfare il criterio - Regolazione tempi di esecuzione (2.2.1) {#how-to-meet-timing-adjustable}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable).

#### Ulteriori informazioni - Regolazione tempi di esecuzione (2.2.1) {#more-information-timing-adjustable}

* [Comprendere i criteri di successo 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [Come soddisfare i criteri di successo 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### Pausa, stop, nascondi (2.2.2)    {#pause-stop-hide}

* Criterio di successo 2.2.2
* Livello A
* Pausa, stop, nascondi: per le informazioni in movimento, lampeggianti, scorrevoli o con aggiornamento automatico, vale quanto segue:
   * Spostamento, lampeggiamento, scorrimento: per qualsiasi informazione in movimento, lampeggiante o scorrevole che (a) parta automaticamente, (b) duri più di cinque secondi, e (c) sia rappresentata in parallelo con altro contenuto, esiste un meccanismo che consente all’utente di mettere in pausa, interrompere o nascondere l’effetto, a meno che questo non sia parte di un’attività per la quale è essenziale;
   * Aggiornamento automatico: per qualsiasi informazione con aggiornamento automatico che (a) parta automaticamente e (b) sia rappresentata in parallelo con altro contenuto, esiste un meccanismo che consente all’utente di mettere in pausa, interrompere o nascondere il contenuto, oppure controllare la frequenza dell’aggiornamento, a meno che questo non sia parte di un’attività per la quale è essenziale;

Elementi da sottolineare:

1. Per i requisiti relativi a contenuti che sfarfallano o lampeggiano, consulta Non progettare contenuti con modalità che possano causare attacchi epilettici (2.3).
1. Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (utilizzato per soddisfare altri criteri di successo o meno) deve rispondere a questo criterio. Consulta [Requisito di conformità 5: Non interferenza](https://www.w3.org/TR/WCAG20/#cc5).
1. I contenuti aggiornati periodicamente dal software o trasmessi in streaming all’agente dell’utente non sono tenuti a conservare o presentare le informazioni generate o ricevute tra l’inizio della pausa e la ripresa della presentazione, in quanto questo potrebbe non essere tecnicamente possibile e, in molte situazioni, potrebbe essere fuorviante.
1. Un’animazione che si verifica come parte di una fase di precaricamento, o situazione similare, può essere considerata essenziale se l’interazione non può verificarsi durante quella fase per tutti gli utenti e se la mancata indicazione dell’avanzamento potrebbe confondere gli utenti o far loro pensare che il contenuto sia bloccato o guasto.

#### Finalità - Pausa, stop, nascondi (2.2.2)  {#purpose-pause-stop-hide}

Per alcuni utenti i contenuti in movimento potrebbero essere fonte di distrazione o persino di dolore fisico, impedendo loro di concentrarsi su altre parti della pagina. Inoltre, tali contenuti possono risultare di difficile lettura per chi abbia difficoltà a tenere il passo con il testo in movimento.

#### Come soddisfare il criterio - Pausa, stop, nascondi (2.2.2)  {#how-to-meet-pause-stop-hide}

In base alla natura del contenuto, è possibile applicare uno o più dei seguenti suggerimenti durante la creazione di pagine web che includono contenuti in movimento, con effetti di sfarfallio o lampeggiamento:

* Fornisci un mezzo per mettere in pausa lo scorrimento dei contenuti, in modo che gli utenti abbiano il tempo di leggerli, ad esempio un componente tipo news ticker, un testo con aggiornamento automatico e caroselli di immagini con avanzamento automatico.
* Assicurati che il contenuto smetta di lampeggiare dopo cinque secondi.
* Utilizza tecnologie appropriate per visualizzare contenuto mobile o lampeggiante che possa essere disabilitato dal browser, ad esempio file Graphics Interchange Format (GIF) o Animated Portable Network Graphics (APNG).
* Includi un controllo di modulo nella pagina web per consentire all’utente di disattivare tutti i contenuti mobili o lampeggianti nella pagina.
* Se nessuno degli accorgimenti di cui sopra è praticabile, fornisci un collegamento a una pagina contenente tutti i contenuti, ma senza effetti di spostamento o lampeggiamento.

#### Ulteriori informazioni - Pausa, stop, nascondi (2.2.2)  {#more-information-pause-stop-hide}

* [Comprendere il criterio di successo 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [Come soddisfare il criterio di successo 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### Convulsioni e reazioni fisiche (2.3) {#seizures-and-physcial-reactions}

[Linea guida 2.3 - Convulsioni e reazioni fisiche: non sviluppare contenuti con tecniche che sia noto causino attacchi epilettici o reazioni fisiche.](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### Tre lampeggiamenti o inferiore alla soglia (2.3.1)  {#three-flashes-or-below-threshold}

* Criterio di successo 2.3.1
* Livello A
* Tre lampeggiamenti o inferiore alla soglia: le pagine web non devono contenere alcun elemento che lampeggi per più di tre volte al secondo, oppure il lampeggiamento deve essere inferiore alle soglie di lampeggiamento generale e rosso.

>[!NOTE]
>
>Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (utilizzato per soddisfare altri criteri di successo o meno) deve rispondere a questo criterio. Consulta [Requisito di conformità 5: Non interferenza](https://www.w3.org/TR/WCAG/#cc5).

#### Finalità - Tre lampeggiamenti o inferiore alla soglia (2.3.1) {#purpose-three-flashes-or-below-threshold}

In alcuni casi i contenuti lampeggianti possono causare crisi epilettiche dovute a fotosensibilità. Questo criterio di successo consente agli utenti a rischio di accedere e utilizzare tutti i contenuti, senza preoccuparsi di eventuali contenuti lampeggianti.

#### Come soddisfare il criterio - Tre lampeggiamenti o inferiore alla soglia (2.3.1)  {#how-to-meet-three-flashes-or-below-threshold}

È consigliabile adottare misure per assicurare che siano applicate le seguenti tecniche:

* Assicurati che i componenti non lampeggino per più di tre volte al secondo.
* Se la condizione di cui sopra non può essere soddisfatta, visualizza il contenuto lampeggiante all’interno di *una piccola area di sicurezza* in pixel sullo schermo. Quest’area è calcolata utilizzando una formula complessa, illustrata in [G176: Mantenere l’area lampeggiante sufficientemente piccola](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), di conseguenza questa tecnica dovrebbe essere applicata solo se il contenuto lampeggiante è *assolutamente* necessario.

#### Ulteriori informazioni - Tre lampeggiamenti o inferiore alla soglia (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Comprendere il criterio di successo 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [Come soddisfare il criterio di successo 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### Navigabile (2.4) {#navigable}

[Linea guida 2.4 - Navigabile: fornire all’utente delle funzionalità di supporto per navigare, trovare contenuti e determinare la propria posizione.](https://www.w3.org/TR/WCAG/#navigable)

In questo modo si garantisce che il contenuto sia semplice e intuitivo per la navigazione degli utenti.

### Salto di blocchi (2.4.1)   {#bypass-blocks}

* Criterio di successo 2.4.1
* Livello A
* Salto di blocchi: è disponibile un meccanismo che consente di saltare i blocchi di contenuti che si ripetono su più pagine web.

#### Finalità - Salto di blocchi (2.4.1) {#purpose-bypass-blocks}

Lo scopo di questo criterio di successo è consentire agli utenti che navigano in sequenza nel contenuto di accedere in modo più diretto al contenuto principale della pagina web. Le pagine web e le applicazioni presentano spesso contenuti che vengono ripetuti su altre pagine o schermate. Esempi di blocchi di contenuto ripetuti includono collegamenti di navigazione, elementi grafici di intestazione, menu e frame pubblicitari. Ai fini di questo criterio, le sezioni ripetute di piccole dimensioni, quali singole parole, frasi o singoli collegamenti, non sono considerate blocchi.

#### Come soddisfare il criterio - Salto di blocchi (2.4.1) {#how-to-meet-bypass-blocks}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks).

#### Ulteriori informazioni - Salto di blocchi (2.4.1) {#more-information-bypass-blocks}

* [Comprendere i criteri di successo 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [Come soddisfare i criteri di successo 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### Titolazione della pagina (2.4.2)    {#page-titled}

* Criterio di successo 2.4.2
* Livello A
* Titolazione della pagina: alle pagine web sono associati titoli che ne descrivono argomento o finalità.

#### Finalità - Titolazione della pagina (2.4.2)  {#purpose-page-titled}

Questo criterio di successo consente a tutti gli utenti, indipendentemente da eventuali particolari disabilità, di identificare rapidamente il contenuto di una pagina web senza leggere la pagina completa. Questo è particolarmente utile quando più pagine web vengono aperte in altrettante schede del browser, in quanto il titolo della pagina è indicato nella scheda e quindi può essere individuato rapidamente.

#### Come soddisfare il criterio - Titolazione della pagina (2.4.2)  {#how-to-meet-page-titled}

Quando crei una nuova pagina HTML in AEM, puoi specificare il titolo della pagina. Assicurati che il titolo descriva adeguatamente il contenuto e lo scopo della pagina e le eventuali particolarità, in modo che i visitatori possano verificare velocemente se i contenuti sono effettivamente pertinenti per le proprie esigenze.

È inoltre possibile modificare il titolo della pagina quando la si modifica, attraverso: **Informazioni pagina** > **Proprietà.**

#### Ulteriori informazioni - Titolazione della pagina (2.4.2) {#more-information-page-titled}

* [Comprendere il criterio di successo 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [Come soddisfare il criterio di successo 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### Ordine del focus (2.4.3)   {#focus-order}

* Criterio di successo 2.4.3
* Livello A
* Ordine del focus: se è possibile navigare in una pagina web in modo sequenziale e le sequenze di navigazione influiscono sul suo significato e sul suo funzionamento, gli oggetti che possono essere attivati (portati in focus) devono rispettare un ordine di attivazione che ne mantenga il senso e l’operatività.

#### Finalità - Ordine del focus (2.4.3) {#purpose-focus-order}

L’obiettivo di questo criterio di successo è garantire che quando gli utenti navigano in sequenza nel contenuto, le informazioni vengano visualizzate in un ordine coerente con il significato del contenuto e possano essere utilizzate tramite la tastiera. Questo riduce la confusione e consente agli utenti di creare un modello mentale coerente del contenuto. Possono essere presenti ordini diversi che riflettono le relazioni logiche del contenuto. Ad esempio, lo spostamento tra i componenti di un modulo online composto da più campi e/o passaggi rispecchia le relazioni logiche presenti nel contenuto.

#### Come soddisfare il criterio - Ordine del focus (2.4.3) {#how-to-meet-focus-order}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order).

#### Ulteriori informazioni - Ordine del focus (2.4.3) {#more-information-focus-order}

* [Comprendere i criteri di successo 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [Come soddisfare i criteri di successo 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### Scopo del collegamento (nel contesto) (2.4.4)    {#link-purpose-in-context}

* Criterio di successo 2.4.4
* Livello A
* Scopo del collegamento (nel contesto): lo scopo di ogni collegamento può essere determinato esclusivamente dal testo di collegamento, oppure dal testo di collegamento insieme al suo contesto, determinato a livello di programmazione, a meno che lo scopo del collegamento possa risultare ambiguo per gli utenti in generale.

#### Finalità - Scopo del collegamento (nel contesto) (2.4.4)  {#purpose-link-purpose-in-context}

Per tutti gli utenti, indipendentemente da un’eventuale disabilità, è fondamentale indicare chiaramente la direzione di un collegamento tramite un apposito testo, per aiutare gli utenti a decidere se vogliono effettivamente seguire un collegamento. Per i normovedenti, un testo di collegamento significativo è estremamente utile laddove in una pagina siano presenti più collegamenti (in particolare se la pagina è molto ricca di testo), in quanto fornisce un’indicazione più chiara delle funzionalità della pagina di destinazione. Gli utenti di alcune tecnologie per l’accessibilità, in grado di generare un elenco di tutti i collegamenti su una sola pagina, dal canto loro potranno comprendere più facilmente il testo di collegamento fuori dal contesto se tale testo è sia univoco che informativo. Tuttavia, i normovedenti con disabilità cognitive possono confondersi se le informazioni di un collegamento non sono sufficienti a descrivere con precisione quale sarà la destinazione.

#### Come soddisfare il criterio - Scopo del collegamento (nel contesto) (2.4.4)  {#how-to-meet-link-purpose-in-context}

Soprattutto, fai in modo che lo scopo di un collegamento sia chiaramente descritto all’interno del testo di collegamento.

* Esempio di utilizzo non corretto:
   * Testo: per i dettagli sui nostri corsi serali per l’autunno 2010, fai clic qui.
   * Motivo: non indica in modo chiaro e senza ambiguità la destinazione.
* Esempio di utilizzo corretto:
   * Testo: I nostri corsi serali per l’autunno 2010 - Dettagli.
   * Motivo: modificando leggermente il testo e la posizione dell’elemento di collegamento è possibile migliorare il testo di collegamento:

I collegamenti dovrebbero essere formulati in modo coerente tra le pagine, in particolare per le barre di navigazione. Ad esempio, se un collegamento a una pagina specifica è denominato **Pubblicazioni** in una pagina, utilizza lo stesso testo anche nelle altre pagine per garantire la coerenza.

Al momento in cui scriviamo, l’uso degli attributi title per garantire che collegamenti simili presentati in una pagina forniscano informazioni univoche sulla destinazione (ad esempio, “Ulteriori informazioni” spesso fa riferimento a una serie di destinazioni diverse) implica alcuni problemi:

* Il testo contenuto all’interno dell’attributo title è generalmente disponibile solo a chi utilizza un mouse, sotto forma di pop-up con la descrizione comando, e non è accessibile utilizzando la tastiera o agli utenti di dispositivi mobili.
* Le utilità di lettura dello schermo possono leggere gli attributi title, ma questa funzionalità potrebbe non essere abilitata per impostazione predefinita; è quindi possibile che gli utenti non siano a conoscenza dell’esistenza di un attributo title.
* È difficile modificare l’aspetto del testo del titolo, il che significa che leggerlo può risultare difficile o impossibile per alcuni utenti.

Così, mentre l’attributo title può essere utilizzato per fornire contesto aggiuntivo per un collegamento, è importante essere consapevoli dei suoi limiti e non utilizzarlo come alternativa a un testo collegamento adeguato.

Se il collegamento è costituito da un’immagine, accertati che il testo alternativo per l’immagine descriva la destinazione del collegamento. Ad esempio, se come collegamento alle pubblicazioni di un autore è impostata l’immagine di una libreria, il testo alternativo dovrebbe riportare **Pubblicazioni di John Smith** e non **Libreria**.

In alternativa, se nell’ancoraggio del collegamento è incluso testo che descrive lo scopo del collegamento in aggiunta all’elemento immagine (e, quindi, il testo viene visualizzato a fianco dell’immagine), utilizza un attributo alt vuoto per l’immagine:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>Il frammento di codice sopra ha esclusivamente scopo illustrativo; si consiglia di utilizzare il componente **Immagine**.

Mentre è opportuno fornire un testo di collegamento che identifichi lo scopo del collegamento senza necessità di ulteriore contesto, questo effettivamente non è sempre possibile. I collegamenti senza contesto possono essere utilizzati nei casi seguenti, di cui è possibile trovare alcuni esempi HTML in [Come soddisfare il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context).

* Qualora il testo di collegamento sia parte di un elenco di collegamenti strettamente correlati, e la voce di elenco che racchiude il collegamento fornisca contesto sufficiente.
* Laddove lo scopo di un collegamento possa essere chiaramente identificato dal testo di paragrafo *che lo precede* (non che lo segue).
* Se il collegamento è contenuto all’interno di una tabella di dati, e quindi la finalità può essere chiaramente identificata a partire dalle intestazioni associate.
* Se un elenco di collegamenti è contenuto all’interno di un insieme di intestazioni e l’intestazione fornisce il contesto adatto.
* Se un elenco di collegamenti è contenuto all’interno di un collegamento nidificato e la voce dell’elenco principale rispetto al collegamento nidificato fornisce il contesto adatto.

In alcuni casi, laddove in una pagina siano presenti diversi collegamenti (ciascuno dei quali fornisca la direzione di un collegamento con dettagli complessi ma necessari), può essere opportuno prevedere una versione alternativa della pagina web che mostri lo stesso contenuto, ma in cui il testo dei collegamenti non sia così dettagliato.

In alternativa, puoi utilizzare script in modo da fornire una quantità minima di testo nel collegamento, ma consentendo, all’attivazione di un controllo adeguato posizionato nella parte superiore della pagina, *l’espansione* del testo di collegamento per specificare maggiori dettagli. Un approccio simile consiste nell’utilizzare i CSS per *nascondere* il collegamento completo agli utenti normovedenti, ma mostrarlo agli utenti di utilità di lettura dello schermo. Questo esula dallo scopo di questo documento, ma ulteriori informazioni su come ottenere questo risultato sono reperibili nella sezione [Ulteriori informazioni - Scopo del collegamento (nel contesto) (2.4.4)](#more-information-link-purpose-in-context).

#### Ulteriori informazioni - Scopo del collegamento (nel contesto) (2.4.4) {#more-information-link-purpose-in-context}

* [Comprendere il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [Come soddisfare il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### Differenti modalità (2.4.5)   {#multiple-ways}

* Criterio di successo 2.4.5
* Livello AA
* Differenti modalità: rendere disponibili più modalità per identificare una pagina web all’interno di un insieme di pagine web, salvo il caso in cui una pagina web sia il risultato o un passaggio di un’azione.

#### Finalità - Differenti modalità (2.4.5) {#purpose-multiple-ways}

L’obiettivo di questo criterio di successo è di consentire agli utenti di individuare il contenuto nel modo più adatto alle loro esigenze. Gli utenti possono utilizzare una tecnica più semplice o immediata di un’altra.

Anche i siti di piccole dimensioni dovrebbero fornire agli utenti alcuni strumenti di orientamento. Per un sito di tre o quattro pagine, con tutte le pagine collegate dalla home page, può essere sufficiente fornire i collegamenti da e verso la home page. Nella home page, i collegamenti possono fungere anche da mappa del sito.

#### Come soddisfare il criterio - Differenti modalità (2.4.5) {#how-to-meet-multiple-ways}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways).

#### Ulteriori informazioni - Differenti modalità (2.4.5) {#more-information-multiple-ways}

* [Comprendere i criteri di successo 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [Come soddisfare i criteri di successo 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### Intestazioni ed etichette (2.4.6)   {#headings-and-labels}

* Criterio di successo 2.4.6
* Livello AA
* Intestazioni ed etichette: utilizzare intestazioni ed etichette per descrivere argomenti o finalità.

#### Finalità - Intestazioni ed etichette (2.4.6) {#purpose-headings-and-labels}

Lo scopo di questo criterio di successo è aiutare gli utenti a comprendere quali informazioni sono contenute nelle pagine web e il modo in cui tali informazioni sono organizzate. Se le intestazioni sono chiare e descrittive, gli utenti possono trovare le informazioni che cercano più facilmente e possono comprendere più facilmente le relazioni tra le diverse parti del contenuto. Le etichette descrittive consentono agli utenti di identificare componenti specifici all’interno del contenuto.

#### Come soddisfare il criterio - Intestazioni ed etichette (2.4.6) {#how-to-meet-headings-and-labels}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels).

#### Ulteriori informazioni - Intestazioni ed etichette (2.4.6) {#more-information-headings-and-labels}

* [Comprendere i criteri di successo 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [Come soddisfare i criteri di successo 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### Focus visibile (2.4.7)   {#focus-visible}

* Criterio di successo 2.4.7
* Livello AA
* Focus visibile: qualsiasi interfaccia utente utilizzabile da tastiera deve avere una modalità operativa in cui sia visibile un indicatore che identifichi l’elemento attivo (o in focus), ossia quello su cui agisce la tastiera.

#### Finalità - Focus visibile (2.4.7) {#purpose-focus-visible}

Lo scopo di questo criterio di successo è aiutare l’utente a individuare l’elemento attivo su cui agisce la tastiera.

In presenza di più elementi, l’utente deve poter individuare con facilità l’elemento attivo. Se sullo schermo è presente un solo controllo utilizzabile da tastiera, il criterio di successo sarà soddisfatto perché la progettazione visiva presenta un solo elemento utilizzabile da tastiera.

Dove il criterio di successo indica &quot;modalità operativa&quot;, questo significa tenere conto delle piattaforme che potrebbero non sempre mostrare un indicatore di messa a fuoco. Nella maggior parte dei casi, è disponibile una sola modalità operativa, pertanto questo criterio di successo è già soddisfatto.

#### Come soddisfare il criterio - Focus visibile (2.4.7) {#how-to-meet-focus-visible}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible).

#### Ulteriori informazioni - Focus visibile (2.4.7) {#more-information-focus-visible}

* [Comprendere i criteri di successo 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [Come soddisfare i criteri di successo 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## Principio 3: Comprensibile  {#principle-understandable}

[Principio 3: Comprensibile - Le informazioni e le operazioni dell’interfaccia devono essere comprensibili.](https://www.w3.org/TR/WCAG/#understandable)

### Rendere il testo leggibile e comprensibile (3.1)  {#make-text-content-readable-and-understandable}

[Linea guida 3.1 - Leggibile: rendere il testo leggibile e comprensibile.](https://www.w3.org/TR/WCAG/#readable)

### Lingua della pagina (3.1.1)  {#language-of-page}

* Criterio di successo 3.1.1
* Livello A
* Lingua della pagina: la lingua predefinita di ogni pagina web può essere determinata a livello di programmazione.

#### Finalità - Lingua della pagina (3.1.1)  {#purpose-language-of-page}

Lo scopo di questo criterio è fare in modo che il testo e gli altri contenuti linguistici siano resi correttamente. Per gli utenti di utilità di lettura dello schermo, questo garantisce che la pronuncia sia corretta, mentre i browser visivi saranno più propensi a visualizzare certi set di caratteri correttamente.

#### Come soddisfare il criterio - Lingua della pagina (3.1.1)  {#how-to-meet-language-of-page}

Per soddisfare questo criterio di successo, la lingua predefinita di una pagina web può essere identificata mediante l’attributo `lang` all’interno dell’elemento `<html>` nella parte superiore della pagina. Esempio:

* Se una pagina è scritta in inglese, l’elemento `<html>` dovrebbe riportare:
   `<html lang = "en">`

* Una pagina che deve essere resa in spagnolo dovrebbe invece adottare il seguente standard:
   `<html lang = "es">`

In AEM, la lingua predefinita della pagina viene impostata durante la creazione, ma può anche essere cambiata durante la modifica di [Proprietà pagina](/help/sites-authoring/editing-page-properties.md).

>[!NOTE]
>
>AEM offre un’ulteriore ottimizzazione per le varianti di una lingua principale, ad esempio en-us per l’inglese americano, en-gb per inglese britannico e en-ca per l’inglese canadese. Questo livello di dettaglio è spesso superfluo nel caso delle tecnologie per l’accessibilità, ma può essere utilizzato per varianti regionali nel contenuto delle pagine.

#### Ulteriori informazioni - Lingua della pagina (3.1.1) {#more-information-language-of-page}

* [Comprendere il criterio di successo 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [Come soddisfare il criterio di successo 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* I codici sono basati su ISO 639-1. Un elenco più completo dei codici per ogni lingua è reperibile sul [sito W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Parti in lingua (3.1.2)    {#language-of-parts}

* Criterio di successo 3.1.2
* Livello AA
* Parti in lingua: la lingua di ogni passaggio o frase nel contenuto può essere determinata a livello di programmazione, fatta eccezione per nomi propri, termini tecnici, parole in lingue indeterminate e parole o frasi che sono diventate parte del gergo del testo immediatamente circostante.

#### Finalità - Parti in lingua (3.1.2)  {#purpose-language-of-parts}

Lo scopo di questo criterio di successo è simile a quello del criterio [Lingua della pagina](#language-of-page), ma si applica a pagine web con contenuti multilingue all’interno di una singola pagina (ad esempio, a causa di citazioni o prestiti lessicali non comuni).

Le pagine che applicano questo criterio di successo consentono:

* Inserimento di caratteri accentati da parte di software di transizione Braille.
* Pronuncia corretta da parte dell’utilità di lettura dello schermo di quelle parole che contengono caratteri speciali o non siano nella lingua predefinita identificata a livello di pagina.
* Traduzione corretta del contenuto da una lingua all’altra da parte di strumenti di traduzione come Google Traduttore.

#### Come soddisfare il criterio - Parti in lingua (3.1.2)  {#how-to-meet-language-of-parts}

L’attributo `lang` può essere utilizzato per identificare le modifiche nella lingua del contenuto. Ad esempio, una citazione in tedesco (codice ISO 639-1 &quot;de&quot;) può essere mostrata come segue:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>Gli elementi blockquote non sono supportati in un’istanza standard. Un componente personalizzato può essere sviluppato per supportare la funzione.

Analogamente, il browser può rappresentare correttamente un prestito lessicale non comune o una frase se l’elemento `span` viene utilizzato come segue:

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>Non è necessario seguire questo criterio di successo per nomi o città in lingue diverse, o quando si utilizzano prestiti lessicali o frasi diventati comuni nella lingua predefinita (come *schadenfreude* in inglese).

Per aggiungere l’elemento span con una lingua appropriata, è possibile modificare manualmente il codice HTML nella modalità di modifica sorgente dell’editor Rich Text, affinché venga letto come sopra indicato. In alternativa, l’attributo `lang` può essere incluso nell’editor Rich Text da un amministratore di sistema (consulta [ Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Ulteriori informazioni - Parti in lingua (3.1.2) {#more-information-language-of-parts}

* [Comprendere il criterio di successo 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [Come soddisfare il criterio di successo 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### Prevedibile (3.2) {#predictable}

[Linea guida 3.2 - Prevedibile: creare pagine web che abbiano aspetto e funzionamento prevedibili.](https://www.w3.org/TR/WCAG/#predictable)

In questo modo si garantisce che le pagine web siano coerenti nell’aspetto e nel funzionamento.

### Al focus (3.2.1)   {#on-focus}

* Criterio di successo 3.2.1
* Livello A
* Al focus: quando un componente dell’interfaccia utente viene attivato (viene portato in focus), non deve innescare un cambiamento del contesto.

#### Finalità - Al focus (3.2.1) {#purpose-on-focus}

L’obiettivo di questo criterio di successo è garantire prevedibilità durante la navigazione in un documento. Un componente che, se attivato, possa innescare un evento non dovrà determinare un cambiamento del contesto. Esempi di cambiamento del contesto quando un componente diventa attivo:

* moduli inviati automaticamente quando un componente diventa attivo;
* nuove finestre aperte quando un componente diventa attivo;
* stato di attivazione che passa a un altro componente quando un componente diventa attivo.

Lo stato di attivazione può essere passato a un altro controllo tramite la tastiera (ad esempio, tasto Tab per passare da un controllo all’altro) o il mouse (ad esempio, clic su un campo di testo). Lo spostamento del mouse su un controllo non ne determina l’attivazione, a meno che questo comportamento non venga implementato mediante script. Tieni presente che alcuni tipi di controlli usano il clic per attivare il controllo (ad esempio, un pulsante), che a sua volta determina un cambiamento del contesto.

#### Come soddisfare il criterio - Al focus (3.2.1) {#how-to-meet-on-focus}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus).

#### Ulteriori informazioni - Al focus (3.2.1) {#more-information-on-focus}

* [Comprendere i criteri di successo 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [Come soddisfare i criteri di successo 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### All’input (3.2.2)   {#on-input}

* Criterio di successo 3.2.2
* Livello A
* All’input: cambiare l’impostazione di un componente nell’interfaccia non provoca automaticamente un cambiamento di contesto, a meno che l’utente non sia stato informato del comportamento prima di utilizzare il componente.

#### Finalità - All’input (3.2.2) {#purpose-on-input}

L’obiettivo di questo criterio di successo è garantire che l’immissione dei dati o la selezione di un controllo di un modulo produca un effetto prevedibile. La modifica dell’impostazione di qualsiasi componente dell’interfaccia comporta la modifica di alcuni aspetti del controllo che persistono quando l’utente non interagisce più con il componente. Ad esempio, se l’utente seleziona una casella di controllo, immette del testo in un campo di testo o modifica un’opzione selezionata in un elenco, modifica l’impostazione del componente. Tuttavia, se l’utente attiva un collegamento o un pulsante, non viene modificata alcuna impostazione. I cambiamenti di contesto possono confondere gli utenti che non percepiscono facilmente il cambiamento o che sono facilmente distratti dai cambiamenti. Il cambiamento di contesto è appropriato solo nei casi in cui è chiaro che tale modifica viene eseguita in risposta all’azione dell’utente.

#### Come soddisfare il criterio - All’input (3.2.2) {#how-to-meet-on-input}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input).

#### Ulteriori informazioni - All’input (3.2.2) {#more-information-on-input}

* [Comprendere i criteri di successo 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [Come soddisfare i criteri di successo 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### Navigazione coerente (3.2.3)   {#consistent-navigation}

* Criterio di successo 3.2.3
* Livello AA
* Navigazione coerente: i meccanismi di navigazione che sono ripetuti su più pagine all’interno di un insieme di pagine web, appaiono nello stesso ordine relativo ogni volta che si ripetono, a meno che un cambiamento sia stato avviato da un utente.

#### Finalità - Navigazione coerente (3.2.3) {#purpose-consistent-navigation}

L’obiettivo di questo criterio di successo è incoraggiare l’uso di presentazioni e layout coerenti per gli utenti che interagiscono con contenuti ripetuti all’interno di un insieme di pagine web e che devono individuare informazioni o funzionalità specifiche più di una volta. Le persone ipovedenti che utilizzano l’ingrandimento dello schermo per visualizzare una piccola parte dello schermo alla volta spesso utilizzano riferimenti visivi o i margini della pagina per individuare rapidamente contenuti ripetuti. Presentare contenuti ripetuti nello stesso ordine è importante anche per gli utenti che si basano su elementi visivi e utilizzano la memoria spaziale o indicazioni visive all’interno del layout per individuare contenuti ripetuti.

È importante notare che l’uso dell’espressione “stesso ordine” in questa sezione non implica l’impossibilità di utilizzare i menu o i blocchi di navigazione secondaria, né la struttura della pagina. Questo criterio di successo ha lo scopo di aiutare gli utenti che interagiscono con contenuti ripetuti in più pagine web a prevedere la posizione del contenuto che stanno cercando e a trovarlo più rapidamente quando lo incontrano di nuovo.

Gli utenti possono avviare una modifica dell’ordine utilizzando agenti utente adattivi o impostando le preferenze in modo che le informazioni vengano presentate nel modo più utile per loro.

#### Come soddisfare il criterio - Navigazione coerente (3.2.3) {#how-to-meet-consistent-navigation}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation).

#### Ulteriori informazioni - Navigazione coerente (3.2.3) {#more-information-consistent-navigation}

* [Comprendere i criteri di successo 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [Come soddisfare i criteri di successo 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### Identificazione coerente (3.2.4)   {#consistent-identification}

* Criterio di successo 3.2.4
* Livello A
* Identificazione coerente: i componenti che hanno la stessa funzionalità all’interno di un insieme di pagine web sono identificati in modo coerente.

#### Finalità - Identificazione coerente (3.2.4) {#purpose-consistent-identification}

L’obiettivo di questo criterio di successo è garantire un’identificazione coerente dei componenti funzionali che vengono visualizzati ripetutamente all’interno di un insieme di pagine web. Una strategia sfruttata dagli utenti che usano utilità per la lettura dello schermo per l’utilizzo di un sito web è quella di fare affidamento sulla familiarità con le funzioni che possono apparire in diverse pagine web. Se funzioni identiche hanno etichette diverse (o, più in generale, un nome accessibile diverso) in pagine web diverse, il sito sarà molto più difficile da usare. Questa situazione potrebbe confondere o aumentare il carico cognitivo anche per le persone con limitazioni cognitive. Di conseguenza, l’utilizzo di etichette in modo coerente sarà di aiuto.

La coerenza va estesa anche alle alternative testuali. Se le icone o altri elementi non testuali hanno la stessa funzionalità, anche le alternative testuali devono essere coerenti.

Se in una pagina web sono presenti due componenti entrambi con le stesse funzionalità di un componente in un’altra pagina di un insieme di pagine web, tutti e tre i componenti devono essere coerenti. Pertanto, i due componenti nella stessa pagina saranno coerenti.

La best practice consigliata è la coerenza all’interno di una singola pagina web, il criterio di successo 3.2.4 richiede la coerenza all’interno di un insieme di pagine web solo nel caso in cui un componente sia ripetuto in più pagine dell’insieme.

#### Come soddisfare il criterio - Identificazione coerente (3.2.4) {#how-to-meet-consistent-identification}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification).

#### Ulteriori informazioni - Identificazione coerente (3.2.4) {#more-information-consistent-identification}

* [Comprendere i criteri di successo 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [Come soddisfare i criteri di successo 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### Assistenza nell’inserimento (3.3) {#input-assistance}

[Linea guida 3.3 - Assistenza nell’inserimento: aiutare gli utenti a evitare gli errori e agevolarli nella loro correzione.](https://www.w3.org/TR/WCAG/#input-assistance)

### Identificazione di errori (3.3.1)   {#error-identification}

* Criterio di successo 3.3.1
* Livello A
* Identificazione di errori: se viene rilevato automaticamente un errore di inserimento, l’elemento in errore viene identificato e l’errore viene descritto tramite testo.

#### Finalità - Identificazione di errori (3.3.1) {#purpose-error-identification}

L’obiettivo di questo criterio di successo è garantire che gli utenti siano informati della presenza di un errore e possano comprendere quale sia l’anomalia. Il messaggio di errore deve essere il più specifico possibile. In caso di un invio non riuscito di un modulo, la visualizzazione ripetuta del modulo e l’indicazione dei campi che presentano l’errore non sono sufficienti per consentire a tutti gli utenti di comprendere che si è verificato un errore. Le persone che usano un’utilità di lettura dello schermo, ad esempio, non potranno sapere che si è verificato un errore finché non incontrano uno degli indicatori di errore. È possibile che abbandonino completamente il modulo prima di incontrare l’indicatore di errore, ritenendo che la pagina semplicemente non funzioni. In WCAG, per [errore di inserimento](https://www.w3.org/TR/WCAG/#dfn-input-error) si intende un errore causato da informazioni fornite dall’utente che non vengono accettate dal sistema. Ciò include:

informazioni richieste dalla pagina web ma omesse dall’utente oppure dati forniti dall’utente non conformi al formato richiesto o che non rientrano nei valori consentiti.
Esempi:

* l’utente immette un’abbreviazione non corretta nei campi Stato, Provincia, Regione o in un altro campo;
* l’utente immette nel campo Stato un’abbreviazione che non corrisponde a uno stato valido;
* l’utente immette un codice postale inesistente;
* l’utente immette una data di nascita collocata nel futuro;
* l’utente immette caratteri alfabetici o parentesi nel campo relativo al numero di telefono che accetta solo numeri;
* l’utente immette un’offerta inferiore all’offerta precedente o all’incremento dell’offerta minima.

#### Come soddisfare il criterio - Identificazione di errori (3.3.1) {#how-to-meet-error-identification}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification).

#### Ulteriori informazioni - Identificazione di errori (3.3.1) {#more-information-error-identification}

* [Comprendere i criteri di successo 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [Come soddisfare i criteri di successo 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### Etichette o istruzioni (3.3.2)  {#labels-or-instructions}

* Criterio di successo 3.3.2
* Livello A
* Etichette o istruzioni: etichette o istruzioni vengono fornite quando il contenuto richiede l’input dell’utente.

#### Finalità - Etichette o istruzioni (3.3.2)  {#purpose-labels-or-instructions}

Fornire istruzioni per facilitare la compilazione dei moduli è una parte fondamentale delle buone pratiche nell’ambito dell’usabilità dell’interfaccia. Questo è particolarmente utile per le persone con disabilità visive o cognitive, che altrimenti potrebbero avere difficoltà nel comprendere il layout di un modulo e il tipo di dati da fornire in un particolare campo.

##### Forms

Nel progetto demo AEM WKND viene aggiunta un&#39;etichetta predefinita quando si aggiunge alla pagina un componente modulo, ad esempio un **campo di testo**. Questo titolo predefinito dipende dal tipo di componente. È possibile aggiungere un titolo personalizzato nelle schede per **titolo e testo** della finestra di dialogo di modifica per tale campo. È importante assicurarsi che le etichette aiutino gli utenti a comprendere i dati associati a ciascun componente del modulo.

Il campo **Titolo** deve essere utilizzato per gli elementi di campo in quanto fornisce un’etichetta che è disponibile per la tecnologia per l’accessibilità. Scrivere semplicemente un’etichetta di testo accanto al campo non è sufficiente.

Per alcuni componenti di modulo è anche possibile nascondere visivamente le etichette utilizzando la casella di selezione **Nascondi titolo**. Le etichette nascoste in questo modo sono ancora disponibili per le tecnologie per l’accessibilità, ma non vengono visualizzate sullo schermo. Questo può essere un buon approccio in alcune situazioni, ma solitamente è meglio includere un’etichetta visiva ove possibile, in quanto alcuni utenti potrebbero stare guardando una sezione molto piccola dello schermo (un campo alla volta) e necessitare delle etichette per identificare il campo in modo corretto.

###### Pulsanti immagine {#image-buttons}

Se si utilizzano i pulsanti immagine (ad esempio, il componente per il pulsante immagine **Image Button** del progetto WKND) il campo per il **titolo** della scheda per **titolo e testo** della finestra di dialogo di modifica fornisce effettivamente il testo alternativo per l’immagine, anziché l’etichetta. Nell’esempio seguente, l’immagine con il testo `Submit` presenta il testo alt `Submit`, aggiunto dal campo **Titolo** della finestra di dialogo di modifica.

###### Gruppi di campi modulo {#groups-of-form-fields}

Nel progetto WKND, se esiste un gruppo di controlli correlati, ad esempio il gruppo pulsanti di scelta **Radio Group**, può essere necessario assegnargli un titolo, nonché controlli specifici. Quando si aggiunge un set di pulsanti di scelta in AEM, il campo **Titolo** fornisce il titolo del gruppo, mentre i singoli titoli vengono specificati durante la creazione dei pulsanti di scelta (**Elementi**).

Tuttavia, non esiste alcuna associazione programmatica tra il titolo del gruppo e i pulsanti di scelta. Per creare tale associazione, gli editor di modelli dovranno eseguire il wrapping del titolo tra i tag necessari `fieldset` e `legend`, semplicemente modificando il codice sorgente della pagina. In alternativa, un amministratore di sistema può aggiungere il supporto di questi elementi affinché vengano visualizzati nella finestra di dialogo **Proprietà campo** (consulta [Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

###### Considerazioni aggiuntive relative ai moduli {#additional-considerations-for-forms}

Se i dati devono essere immessi in un formato specifico, specificalo chiaramente nel testo dell’etichetta. Ad esempio, se una data deve essere inserita nel formato `DD-MM-YYYY`, indicala chiaramente come parte dell’etichetta. Ciò significa che, quando chi usa un’utilità di lettura dello schermo arriva al campo, l’etichetta viene annunciata automaticamente, insieme alle informazioni aggiuntive relative al formato.

Se l’input di un campo modulo è obbligatorio, specificalo integrando la parola “obbligatorio” nell’etichetta. AEM aggiunge un asterisco quando un campo è obbligatorio, ma sarebbe ideale includere la parola `required` nell’etichetta stessa (nel campo **Titolo** della finestra di dialogo di modifica).

Il posizionamento delle etichette è importante anche in quanto aiuta a individuare campi appropriati. Questo è di particolare importanza quando l’utente si trova di fronte a un modulo complesso. Segui la convenzione qui di seguito:

* Caselle di selezione o pulsanti di scelta:
Le etichette sono posizionate immediatamente a destra del campo.
* Tutti gli altri componenti del modulo (ad esempio caselle di testo, caselle combinate):
Le etichette sono posizionate immediatamente sopra o a sinistra del campo.

Nei moduli semplici con funzionalità molto limitata, l’etichettatura appropriata di un pulsante `Submit` può fungere da etichetta per il campo adiacente (ad esempio `Search`). Ciò è utile in situazioni in cui potrebbe risultare difficile trovare spazio per il testo dell’etichetta.

#### Ulteriori informazioni - Etichette o istruzioni (3.3.2) {#more-information-labels-or-instructions}

* [Comprendere il criterio di successo 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [Come soddisfare il criterio di successo 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### Suggerimenti per gli errori (3.3.3)   {#error-suggestion}

* Criterio di successo 3.3.3
* Livello AA
* Tastiera: se viene identificato un errore di inserimento e sono noti dei suggerimenti per correggerlo, tali suggerimenti vengono forniti all’utente, a meno che ciò non pregiudichi la sicurezza o la finalità del contenuto.

#### Finalità - Suggerimenti per gli errori (3.3.3) {#purpose-error-suggestion}

L’obiettivo di questo criterio di successo è garantire che gli utenti ricevano suggerimenti appropriati per la correzione di un errore di inserimento, se possibile. La definizione WCAG di [errore di inserimento](https://www.w3.org/TR/WCAG/#dfn-input-error) indica che si tratta di informazioni fornite dall’utente che non sono accettate dal sistema. Alcuni esempi di informazioni non accettate includono informazioni obbligatorie ma omesse dall’utente e informazioni fornite dall’utente ma che non rientrano nel formato dati richiesto o nei valori consentiti.

Il criterio di successo 3.3.1 prevede la notifica degli errori. Tuttavia, le persone con limitazioni cognitive potrebbero avere difficoltà a capire come correggere gli errori. Le persone con disabilità visive potrebbero non essere in grado di capire esattamente come correggere l’errore. In caso di invio non riuscito del modulo, gli utenti potrebbero abbandonare il modulo perché non sanno come correggere l’errore, anche se sono consapevoli che si è verificato un problema.

L’autore del contenuto può fornire la descrizione dell’errore oppure l’agente utente può fornire la descrizione dell’errore in base a informazioni specifiche per la tecnologia e determinate a livello di programmazione.

#### Come soddisfare il criterio - Suggerimenti per gli errori (3.3.3) {#how-to-meet-error-suggestion}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion).

#### Ulteriori informazioni - Suggerimenti per gli errori (3.3.3) {#more-information-error-suggestion}

* [Comprendere i criteri di successo 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [Come soddisfare i criteri di successo 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### Prevenzione degli errori (legali, finanziari, dati) (3.3.4)   {#error-prevention-legal-financial-data}

* Criterio di successo 3.3.4
* Livello AA
* Prevenzione degli errori (legali, finanziari, dati): per le pagine web che contengono vincoli di tipo giuridico o transazioni finanziarie per l’utente che gestiscono la modifica o la cancellazione e gestione di dati controllabili dall’utente in un sistema di archiviazione oppure che inoltrano le risposte degli utenti a test, è soddisfatta almeno una delle seguenti condizioni:

   * Reversibilità
Le azioni sono reversibili.
   * Controllo
I dati inseriti dall’utente vengono verificati e all’utente viene data l’opportunità di correggere gli errori.
   * Conferma
È disponibile un meccanismo per la revisione, conferma e correzione delle informazioni prima del loro invio definitivo.

#### Finalità - Prevenzione degli errori (legali, finanziari, dati) (3.3.4) {#purpose-error-prevention-legal-financial-data}

L’obiettivo di questo criterio di successo è aiutare gli utenti con disabilità a evitare gravi conseguenze in seguito a un errore durante l’esecuzione di un’azione che non può essere annullata. Ad esempio, l’acquisto di biglietti aerei non rimborsabili o l’invio di un ordine per l’acquisto di azioni in un conto di intermediazione sono transazioni finanziarie con conseguenze importanti. Se un utente commette un errore nella data del viaggio aereo, potrebbe acquistare un biglietto non modificabile per il giorno sbagliato. Se commette un errore nell’indicare il numero di azioni da acquistare, potrebbe acquistare un numero di azioni superiori al previsto. Entrambi questi tipi di errori implicano transazioni immediate, che non possono essere successivamente modificate e che possono avere conseguenze molto costose. In modo simile, può essere considerato errore irreversibile la modifica o l’eliminazione accidentale da parte dell’utente di dati memorizzati in un database a cui potrebbe avere bisogno di accedere successivamente, ad esempio l’intero profilo di viaggio in un sito web dei servizi di viaggio. Con il riferimento alla modifica o all’eliminazione di dati “controllabili dall’utente” si intende evitare la perdita di massa di dati, ad esempio a causa dell’eliminazione di un file o un record. Non si intende chiedere conferma per ogni comando Salva o per la semplice creazione o modifica di documenti, record o altri dati.

Per gli utenti con disabilità, la probabilità di commettere degli errori è maggiore. Le persone con disabilità di lettura potrebbero scambiare numeri e lettere, le persone con disabilità motorie potrebbero premere un tasto accidentalmente. La possibilità di annullare le azioni consente agli utenti di correggere un errore che potrebbe causare gravi conseguenze. La possibilità di rivedere e correggere le informazioni offre all’utente l’opportunità di rilevare un errore prima di intraprendere un’azione che comporta gravi conseguenze.

I dati controllabili dall’utente sono dati visualizzabili dall’utente che possono essere modificati e/o eliminati mediante un’azione intenzionale dell’utente stesso. Esempi di operazioni che interessano tali dati sono l’aggiornamento del numero di telefono e dell’indirizzo dell’account dell’utente o l’eliminazione di un record di fatture precedenti in un sito web. Non si fa riferimento a elementi quali log di Internet o dati di monitoraggio dei motori di ricerca che l’utente non può visualizzare o con cui non può interagire direttamente.

#### Come soddisfare il criterio - Prevenzione degli errori (legale, finanziario, dati) (3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data).

#### Ulteriori informazioni - Prevenzione degli errori (legali, finanziari, dati) (3.3.4) {#more-information-error-prevention-legal-financial-data}

* [Comprendere i criteri di successo 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [Come soddisfare i criteri di successo 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## Principio 4: Robusto {#principle-robust}

[Principio 4 - Robusto: il contenuto deve essere abbastanza robusto per essere interpretato in maniera affidabile da una grande varietà di programmi utente, comprese le tecnologie per l’accessibilità.](https://www.w3.org/TR/WCAG/#robust)

### Compatibile (4.1) {#compatible}

[Linea guida 4.1 - Compatibile: garantire la massima compatibilità con i programmi utente attuali e futuri, comprese le tecnologie per l’accessibilità.](https://www.w3.org/TR/WCAG/#compatible)

Garantire la massima compatibilità con i programmi utente attuali e futuri, comprese le tecnologie per l’accessibilità.

### Analisi sintattica (parsing) (4.1.1)   {#parsing}

* Criterio di successo 4.1.1
* Livello A
* Analisi sintattica (parsing): nel contenuto implementato utilizzando linguaggi di marcatura, gli elementi possiedono tag di apertura e chiusura completi, sono annidati in conformità alle proprie specifiche, non contengono attributi duplicati e tutti gli ID sono univoci, salvo i casi in cui le specifiche permettano eccezioni.

#### Finalità - Analisi sintattica (parsing) (4.1.1) {#purpose-parsing}

Lo scopo di questo criterio di successo è garantire che gli agenti utente, comprese le tecnologie per l’accessibilità, possano interpretare e analizzare in modo preciso il contenuto. Se non è possibile eseguire il parsing del contenuto in una struttura di dati, agenti utente diversi potrebbero presentarlo in modo diverso o non essere in grado di analizzarlo in modo completo. Alcuni agenti utente utilizzano “tecniche di correzione” per eseguire il rendering di contenuto codificato in modo limitato.

Poiché le tecniche di correzione variano nei diversi agenti utente, gli autori non possono essere certi che il contenuto venga analizzato in modo preciso in una struttura di dati o che ne venga eseguito in rendering corretto da parte di agenti utente specializzati, incluse le tecnologie per l’accessibilità, a meno che il contenuto non venga creato in base alle regole definite nella grammatica formale per tale tecnologia. Nei linguaggi di marcatura, gli errori nella sintassi di elementi e attributi e la mancata fornitura di tag di apertura e chiusura nidificati in modo corretto generano errori che impediscono agli agenti utente di analizzare il contenuto in modo affidabile. Pertanto, il criterio di successo richiede che il contenuto possa essere analizzato utilizzando solo le regole della grammatica formale.

#### Come soddisfare il criterio - Analisi sintattica (parsing) (4.1.1) {#how-to-meet-parsing}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing).

#### Ulteriori informazioni - Analisi sintattica (parsing) (4.1.1) {#more-information-parsing}

* [Comprendere i criteri di successo 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [Come soddisfare i criteri di successo 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### Nome, ruolo, valore (4.1.2)   {#name-role-value}

* Criterio di successo 4.1.2
* Livello A
* Nome, ruolo, valore: per tutti i componenti dell’interfaccia utente (inclusi ma non limitati a: elementi di un modulo, collegamenti e componenti generati da script), nome e ruolo possono essere determinati programmaticamente; stati, proprietà e valori che possono essere impostati dall’utente possono essere impostabili da programma; e le notifiche sui cambi di stato di questi elementi sono rese disponibili ai programmi utente, incluse le tecnologie per l’accessibilità.

#### Finalità - Nome, ruolo, valore (4.1.2) {#purpose-ame-role-value}

Lo scopo di questo criterio di successo è garantire che le tecnologie per l’accessibilità (AT, Assistive Technologies) possano raccogliere informazioni sullo stato, nonché attivare (o impostare) e tenere aggiornato lo stato dei controlli dell’interfaccia utente nel contenuto.

Quando si utilizzano controlli standard tramite tecnologie accessibili, questo processo è semplice. Se gli elementi dell’interfaccia utente vengono utilizzati in base alle specifiche, le condizioni di questa indicazione saranno soddisfatte (vedi gli esempi di criteri di successo 4.1.2 di seguito).

Tuttavia, se vengono creati controlli personalizzati o se gli elementi dell’interfaccia sono programmati (tramite codice o script) in modo da avere un ruolo e/o una funzione diversi rispetto al normale, è necessario adottare ulteriori misure per garantire che i controlli forniscano informazioni importanti alle tecnologie per l’accessibilità e possano essere a loro volta controllati tramite tali tecnologie.

Uno stato particolarmente importante di un controllo dell’interfaccia utente è quello di attivazione. Lo stato di attivazione di un controllo può essere determinato a livello di programmazione e le notifiche sul passaggio a un altro elemento attivo vengono inviate agli agenti utente e alla tecnologia per l’accessibilità. Altri esempi di stato del controllo dell’interfaccia utente sono la selezione o meno di una casella di controllo o di un pulsante di scelta, nonché la compressione o espansione di una struttura ad albero o di un nodo di struttura comprimibili.

#### Come soddisfare il criterio - Nome, ruolo, valore (4.1.2) {#how-to-meet-ame-role-value}

Seguire le linee guida illustrate in [Come soddisfare i criteri di successo 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value).

#### Ulteriori informazioni - Nome, ruolo, valore (4.1.2 {#more-information-ame-role-value}

* [Comprendere i criteri di successo 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [Come soddisfare i criteri di successo 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
