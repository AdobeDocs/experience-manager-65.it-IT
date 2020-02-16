---
title: Creazione di contenuto accessibile (conformità WCAG 2.0)
seo-title: Creazione di contenuto accessibile (conformità WCAG 2.0)
description: Crea contenuti web accessibili e utilizzabili da utenti disabili
seo-description: Crea contenuti web accessibili e utilizzabili da utenti disabili
uuid: e2653a46-fd55-407b-b331-8a684fbfd041
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 0aa18f7d-76a8-4c51-9e17-da50ae065fe8
docset: aem65
translation-type: tm+mt
source-git-commit: aaabef9d51e333003385709045e2249a10eb34aa

---


# Creazione di contenuto accessibile (conformità WCAG 2.0){#creating-accessible-content-wcag-conformance}

WCAG 2.0 è costituito da un insieme di linee guida tecnologiche indipendenti e di criteri di successo per contribuire a rendere i contenuti web accessibili e utilizzabili da persone con disabilità.

>[!NOTE]
>
>Consulta anche:
>
>* la nostra [Guida rapida a WCAG 2.0](/help/managing/qg-wcag.md) per ulteriori dettagli
>* [Configurazione dell’editor Rich Text per generare contenuto accessibile](/help/sites-administering/rte-accessible-content.md)
>



Il contenuto viene classificato in base a tre livelli di conformità: Livello A (il più basso), livello AA e livello AAA (il più alto). Brevemente, i livelli sono definiti come segue:

* **Livello A:** il sito presenta un livello minimo, basilare, di accessibilità. Per ottenere questo livello, tutti i criteri di successo di livello A devono essere soddisfatti.
* **** Livello AA: Si tratta di un livello di accessibilità ideale a cui tendere, in cui il sito raggiunge un livello di accessibilità superiore, in modo che sia accessibile alla maggior parte delle persone nella maggior parte delle situazioni utilizzando la maggior parte delle tecnologie. Per raggiungere questo livello, tutti i criteri di successo di livello A e AA sono soddisfatti.
* **Livello AAA:** il sito presenta un livello di accessibilità molto elevato. Per ottenere questo livello, devono essere soddisfatti tutti i criteri di successo dei livelli A, AA e AAA.

Quando si crea il sito, è necessario determinare il livello complessivo che si desidera ottenere.

Nella sezione seguente sono incluse le [linee guida WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) e i criteri di successo per i [livelli di conformità](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) A e AA.

>[!NOTE]
>
>Poiché non è possibile soddisfare tutti i criteri di successo di livello AAA per alcuni tipi di contenuti, non è consigliabile prevedere questo livello di conformità come politica generale.

>[!NOTE]
>
>In questo documento stiamo utilizzando:
>
>* i nomi brevi per le [linee guida WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines).
>* la numerazione utilizzata nelle [linee guida WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) per facilitare i riferimenti incrociati al sito web WCAG.
>



## Principio 1: Percepibilità {#principle-perceivable}

[Principio 1, percepibilità: informazioni e componenti dell’interfaccia utente devono essere presentati agli utenti con modalità da loro percepibili.](https://www.w3.org/TR/WCAG20/#perceivable)

### Alternative testuali (1.1) {#text-alternatives}

[Linea guida 1.1; alternative testuali: fornire alternative testuali per qualsiasi contenuto non testuale in modo che possa essere convertito in altri formati richiesti, come la stampa a caratteri grandi, il Braille, la sintesi vocale, i simboli o un linguaggio più semplice.](https://www.w3.org/TR/WCAG20/#text-equiv)

### Contenuto non testuale (1.1.1) {#non-text-content}

* Criterio di successo 1.1.1
* Livello A
* Contenuto non testuale: tutto il contenuto non testuale presentato all’utente dispone di un’alternativa testuale che svolge la finalità equivalente, fatta eccezione per le situazioni elencate di seguito.

#### Finalità: contenuto non testuale (1.1.1) {#purpose-non-text-content}

Le informazioni su una pagina web possono essere fornite in diversi formati non testuali, ad esempio immagini, video, animazioni, tabelle e grafici. Le persone non vedenti o con gravi problemi visivi non sono in grado di vedere il contenuto non testuale, ma possono accedere ai contenuti testuali letti mediante un’utilità per la lettura dello schermo o presentati in forma tattile da un dispositivo Braille. Così, grazie alla disponibilità di alternative testuali al contenuto in formato grafico, i non vedenti possono accedere a una versione equivalente delle informazioni veicolate.

Un ulteriore vantaggio è rappresentato dal fatto che le alternative testuali consentono l’indicizzazione dei contenuti non testuali da parte dei motori di ricerca.

#### Come soddisfare il criterio: contenuto non testuale (1.1.1) {#how-to-meet-non-text-content}

Per gli elementi grafici statici, il requisito fondamentale consiste nel fornire un’alternativa testuale equivalente. Questo può essere fatto nel campo **Testo Alt**:

>[!NOTE]
>
>Alcuni componenti out-of-the-box, come **Carosello** e **Presentazione** , non consentono di aggiungere descrizioni testuali alternative alle immagini. Quando implementate le versioni di questi componenti per l’istanza di AEM, il team di sviluppo dovrà configurarli per supportare l’ `alt` attributo in modo che gli autori possano aggiungerlo al contenuto (consultate [Aggiunta di supporto per elementi e attributi](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)HTML aggiuntivi).

Il campo **Testo alternativo** è disponibile nella finestra di dialogo del componente **Immagine** sulla scheda **Metadati**:

![Finestra di dialogo di modifica del componente Immagine nell’interfaccia touch, con il campo Testo Alt.](assets/screen_shot_2018-03-21at165045.png)

In AEM il campo **Testo alternativo** deve essere compilato per impostazione predefinita. Se l’immagine è solamente decorativa e il testo alternativo non sarebbe appropriato, seleziona l’opzione **L’immagine è decorativa**.

#### Creazione di buone alternative di testo {#creating-good-text-alternatives}

Esistono varie forme di contenuti non testuali, di conseguenza il valore del testo alternativo dipende dal ruolo dell’elemento grafico all’interno della pagina web. Alcune regole generali da seguire:

* Le alternative testuali dovrebbero essere sintetiche ma veicolare chiaramente le informazioni essenziali fornite dal contenuto non testuale.
* È bene evitare descrizioni eccessivamente lunghe (oltre 100 caratteri). Se un testo alternativo richiede una descrizione più dettagliata:

   * fornisci una breve descrizione nel testo alternativo
   * e includi una descrizione più lunga in un altro elemento di testo, nella stessa pagina o in una pagina web separata. Inserisci un collegamento a questa descrizione separata rendendo l’immagine un collegamento o inserendo un collegamento di testo accanto all’immagine.

* Il testo alternativo non dovrebbe replicare il contenuto fornito sotto forma di testo nella stessa pagina. Ricorda che molte immagini sono illustrazioni di punti già trattati nel testo di una pagina, di conseguenza un’alternativa testuale dettagliata potrebbe già esistere.
* Se il contenuto non testuale è un collegamento a un’altra pagina o un altro documento e non esiste altro testo che faccia parte dello stesso collegamento, il testo alternativo per l’immagine non dovrà descrivere l’immagine ma dovrà invece indicare la destinazione del collegamento.
* Se il contenuto non testuale è incluso in un elemento pulsante e non esiste testo che faccia parte dello stesso pulsante, il testo alternativo per l’immagine non dovrà descrivere l’immagine, ma piuttosto indicare la funzionalità del pulsante.
* È perfettamente accettabile che a un’immagine venga assegnato un testo alternativo vuoto (null), ma solo se l’immagine non dispone di testo alternativo (ad esempio, è un elemento grafico puramente decorativo) o se il testo equivalente esiste già nel testo della pagina.

Il documento [Bozza W3C: Tecniche di HTML5 per fornire alternative testuali utili](https://dev.w3.org/html5/alt-techniques/) include maggiori dettagli ed esempi di testi alternativi adeguati ai diversi tipi di immagini.

Tipi specifici di contenuto non testuale che richiedono alternative testuali potrebbero includere:

* Illustrative photos:
These are images of people, objects or places. Think about the role of the photo in the page; an appropriate text equivalent is likely to be *Photo of[object ]*, but may be dependent on the surrounding text.
* Icone: Si tratta di piccoli pittogrammi (immagini) che veicolano informazioni specifiche. Devono essere utilizzati in modo coerente all’interno di una pagina e del sito. Tutte le istanze dell’icona in una pagina o in un sito devono avere lo stesso testo alternativo, breve e sintetico, a meno che questo determini inutili duplicazioni di testo adiacente.
* Charts and graphs:
These typically represent numerical data. So one option for providing a text alternative might be to include a brief summary of the main trends shown in the chart or graphic. If necessary, also provide a more detailed description in text using the **Description** field in the **Advanced** image properties tab. Additionally, you could provide the source data in tabular form elsewhere in the page or site.

   ![Esempio di grafico. Qui di seguito viene esemplificato l’approccio migliore per fornire un’alternativa.](assets/chlimage_1.jpeg)

   Per fornire un’alternativa per questo grafico di esempio, aggiungi all’immagine un testo `alt` sintetico e inserisci un testo alternativo completo dopo l’immagine stessa.

   ```xml
   <p><img src="figure1.gif" alt="Figure 1" ></p>
   <p> Figure 1. Distribution of Articles by Journal Category.
   Pie chart: Language=68%, Education=14% and Science=18%.</p>
   ```

   >[!NOTE]
   >
   >Lo snippet di codice riportato sopra viene utilizzato solo per illustrare l’ordine. Si consiglia di usare il componente **Immagine** (anziché il riferimento `img src` utilizzato sopra).

   In AEM questo è possibile effettuare questa operazione utilizzando una combinazione dei campi **Testo Alt** e **Descrizione** nella finestra di dialogo di configurazione dell’immagine, come in [Come soddisfare il criterio: contenuto non testuale (1.1.1)](#how-to-meet-non-text-content).

* Maps, diagrams, flowcharts:
For graphics providing spatial data (for example. to support describing relationships between objects or a process), ensure that the key message is provided in text format. For maps, providing a full text equivalent is likely to be impractical, but if the map is provided as a way of helping people find their way to a particular location, then the map image’s alternative text can briefly indicate *Map of X*, then provide directions to that location in text elsewhere in the page or through the **Description** field in the **Advanced** tab of the **Image** component.
* CAPTCHA: CAPTCHA è l’acronimo di “*Completely Automated Public Turing test to tell Computers and Humans Apart*” (test di Turing completamente automatizzato per distinguere macchine e persone). Viene utilizzato come controllo di sicurezza nelle pagine web per distinguere esseri umani da software dannosi, ma che può rappresentare un ostacolo all’accessibilità. Si tratta di immagini che richiedono agli utenti di descrivere ciò che vedono, al fine di superare un test di sicurezza. Fornire un testo alternativo per l’immagine non è ovviamente possibile, quindi sarà necessario prendere in considerazione soluzioni alternative non grafiche. Il W3C fornisce una serie di suggerimenti (ciascuno dei quali presenta vantaggi e svantaggi), ad esempio:

   * Puzzle logici
   * L’impiego di output audio anziché di immagini
   * Account a utilizzo limitato e filtri anti-spam.

* Immagini di sfondo: Questi vengono ottenuti utilizzando Cascading Style Sheets (CSS) anziché HTML. Ciò significa che non è possibile specificare un valore di testo alternativo. Pertanto, le immagini di sfondo non devono fornire informazioni testuali importanti, se lo fanno, tali informazioni devono essere fornite anche nel testo della pagina. Tuttavia, è importante che venga visualizzato uno sfondo alternativo quando l&#39;immagine non può essere visualizzata.

   >[!NOTE]
   >
   >Dovrebbe essere previsto un livello adeguato di contrasto tra lo sfondo e il testo in primo piano; questo elemento viene discusso più dettagliatamente in [Contrasto (minimo) (1.4.3)](#contrast-minimum).

#### Ulteriori informazioni: contenuto non testuale (1.1.1) {#more-information-non-text-content}

* [Comprendere i criteri di successo 1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [Come soddisfare i criteri di successo 1.1.1](https://www.w3.org/WAI/WCAG20/quickref/#text-equiv)
* [W3C: Tecniche HTML5 per fornire alternative testuali utili (bozza)](https://dev.w3.org/html5/alt-techniques/)
* [Spiegazione W3C dei CAPTCHA e relative alternative](https://www.w3.org/TR/turingtest/)

### Elementi multimediali temporizzati (1.2) {#time-based-media}

[Linea guida 1.2; elementi multimediali temporizzati: fornire alternative per gli elementi multimediali temporizzati.](https://www.w3.org/TR/WCAG20/#text-equiv)

L’argomento riguarda i contenuti web *temporizzati*. Questi comprendono i contenuti che l’utente può riprodurre (come video, audio e contenuti animati) e che possono essere preregistrati o in streaming.

### Solo audio e solo video (preregistrato) (1.2.1) {#audio-only-and-video-only-pre-recorded}

* Criterio di successo 1.2.1
* Livello A
* Solo audio e solo video (preregistrato): per gli elementi solo video e solo audio preregistrati vale quanto segue, tranne quando l’audio o il video sia un elemento alternativo per il testo, chiaramente indicato come tale:

   * Solo audio preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati che presenti le informazioni equivalenti ai contenuti solo audio preregistrati.
   * Solo video preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati o una traccia audio che presenti le informazioni equivalenti ai contenuti solo video preregistrati.

#### Finalità: solo audio e solo video (preregistrato) (1.2.1) {#purpose-audio-only-and-video-only-pre-recorded}

Problemi di accessibilità per video e audio possono essere riscontrati da:

* Persone con problemi visivi in assenza di audio o quando l’audio non è sufficiente a informarli di ciò che sta accadendo nel video o nell’animazione;
* Persone con disabilità uditive o non udenti, non in grado di sentire l’audio;
* Persone che possono sentire l’audio, ma non comprendono i dialoghi (ad esempio, perché si svolgono in una lingua che non conoscono).

Video o audio possono anche essere non disponibili per chi utilizza browser o dispositivi che non supportano la riproduzione di contenuti in formati multimediali specifici, come Adobe Flash.

Fornire queste informazioni in un formato diverso, ad esempio testo (o audio per i video senza audio) può renderle accessibili alle persone impossibilitate ad accedere al contenuto originale.

#### Come soddisfare il criterio: solo audio e solo video (preregistrato) (1.2.1) {#how-to-meet-audio-only-and-video-only-pre-recorded}

* Se il contenuto è una traccia audio preregistrata senza video (come un podcast):

   * Fornisci un collegamento immediatamente prima o dopo il contenuto, che rimandi a una trascrizione in formato testo del contenuto audio. La trascrizione dovrebbe essere una pagina HTML con un equivalente testuale di tutti i contenuti parlati e non parlati rilevanti, oltre all’indicazione di chi sta parlando, una descrizione dell’ambientazione, le espressioni vocali e una descrizione di qualsiasi altro elemento sonoro significativo.

* Se il contenuto è un’animazione o un video preregistrato senza audio:

   * Fornisci un collegamento immediatamente prima o dopo il contenuto, che rimandi a una descrizione testuale equivalente delle informazioni fornite nel video.
   * Oppure fornisci una descrizione audio equivalente in un formato audio comunemente utilizzato, come MP3.

>[!NOTE]
>
>Se il contenuto audio o video è fornito come alternativa a contenuto già esistente in un altro formato in una pagina web, non è necessario soddisfare i requisiti di cui sopra. Ad esempio, se un video illustra un elenco di istruzioni testuali, non richiede un’alternativa in quanto le istruzioni testuali già fungono da alternativa al video.

L’inserimento di elementi multimediali nelle pagine web AEM, in particolare contenuti Flash, è simile a quello di un’immagine. Tuttavia, dato che i contenuti multimediali sono molto più di un fermo immagine, esistono differenti impostazioni e opzioni per controllarne la riproduzione.

>[!NOTE]
>
>Quando si utilizzano contenuti multimediali con contenuti informativi, è necessario creare anche collegamenti verso alternative. Ad esempio, per includere una trascrizione di testo, create una pagina HTML per visualizzare la trascrizione, quindi aggiungete un collegamento accanto o sotto al contenuto audio.

#### Ulteriori informazioni: solo audio e solo video (preregistrato) (1.2.1) {#more-information-audio-only-and-video-only-pre-recorded}

* [Comprendere i criteri di successo 1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [Come soddisfare i criteri di successo 1.2.1](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)

### Sottotitoli (preregistrati) (1.2.2) {#captions-pre-recorded}

* Criterio di successo 1.2.2
* Livello A
* Sottotitoli (preregistrati): i sottotitoli vengono forniti per tutti i contenuti audio preregistrati negli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo e chiaramente indicato come tale.

#### Finalità: sottotitoli (preregistrati) (1.2.2) {#purpose-captions-pre-recorded}

Le persone non udenti o ipoudenti non saranno in grado di accedere ai contenuti audio, o avranno gravi difficoltà di accesso. I sottotitoli sono equivalenti testuali dell’audio, parlato e non, visualizzati sullo schermo al momento opportuno nel corso del video. Consentono a chi non può udire l’audio di comprendere cosa sta succedendo.

>[!NOTE]
>
>I sottotitoli non sono richiesti quando testo o equivalenti non testuali adeguati (che forniscano informazioni direttamente equivalenti) sono disponibili sulla stessa pagina del video o delle animazioni.

#### Come soddisfare il criterio: sottotitoli (preregistrati) (1.2.2) {#how-to-meet-captions-pre-recorded}

I sottotitoli possono essere:

* Sottotitoli non codificati: sempre visibili durante la riproduzione del video
* Sottotitoli codificati:* *possono essere attivati o disattivati dall&#39;utente

Se possibile, utilizza i sottotitoli codificati allo scopo di consentire agli utenti di scegliere se visualizzarli o meno.

Per i sottotitoli codificati è necessario creare e fornire, unitamente al file video, un file di sottotitoli sincronizzati in un formato appropriato, ad esempio [SMIL](https://www.w3.org/AudioVideo/) (i dettagli su come effettuare questa operazione vanno oltre lo scopo di questa guida, ma abbiamo incluso collegamenti ad alcune esercitazioni nella sezione [Ulteriori informazioni: sottotitoli (preregistrati) (1.2.2)](#more-information-captions-pre-recorded)). Assicurati di includere una nota per indicare agli utenti che per il video sono disponibili sottotitoli.

Se è necessario utilizzare sottotitoli non codificati, inserisci il testo nella traccia video. A questo scopo è possibile utilizzare applicazioni di editing video che consentono di sovrapporre i sottotitoli al video.

#### Ulteriori informazioni: sottotitoli (preregistrati) (1.2.2) {#more-information-captions-pre-recorded}

* [Comprendere i criteri di successo 1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html):
* [Come soddisfare i criteri di successo 1.2.2](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)
* [W3C: File multimediali sincronizzati](https://www.w3.org/AudioVideo/)
* [Sottotitoli, trascrizioni e descrizioni audio, di WebAIM](https://webaim.org/techniques/captions/)

### Descrizione audio o elemento multimediale alternativo (preregistrato) (1.2.3) {#audio-description-or-media-alternative-pre-recorded}

* Criterio di successo 1.2.3
* Livello A
* Descrizione audio o elemento multimediale alternativo (preregistrato): viene fornita un’alternativa per gli elementi multimediali temporizzati o una descrizione audio del contenuto video preregistrato per gli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo, e chiaramente indicato come tale.

#### Finalità: descrizione audio o file multimediale alternativo (preregistrato) (1.2.3) {#purpose-audio-description-or-media-alternative-pre-recorded}

Le persone non vedenti o ipovedenti avranno problemi di accessibilità se le informazioni in un video o in un’animazione vengono fornite solo visivamente, o se l’audio non fornisce informazioni sufficienti per consentire la comprensione di ciò che sta accadendo.

#### Come soddisfare il criterio: descrizione audio o elemento multimediale alternativo (preregistrato) (1.2.3) {#how-to-meet-audio-description-or-media-alternative-pre-recorded}

Gli approcci che è possibile adottare per soddisfare questo criterio di successo sono due. È possibile:

1. Includere una descrizione audio aggiuntiva per il contenuto video. Questo può essere ottenuto in tre modi:

   * In corrispondenza delle pause nella finestra di dialogo, fornisci informazioni sui cambiamenti della scena che non sono inclusi nella traccia audio esistente;
   * Includi una nuova traccia audio, aggiuntiva e facoltativa, contenente l’audio originale, ma anche informazioni audio ulteriori sui cambiamenti della scena.

      * Questo consente agli utenti di passare dalla traccia audio esistente (che *non* contiene una descrizione audio) alla nuova traccia audio (che *contiene* una descrizione audio), e viceversa.

      * In questo modo si evitano interruzioni per gli utenti che non necessitano della descrizione aggiuntiva.
   * Crea una seconda versione del contenuto video per consentire descrizioni audio estese. Questo riduce le difficoltà connesse con la fornitura di descrizioni audio dettagliate all’interno delle pause nella finestra di dialogo esistente, interrompendo temporaneamente audio e video nei momenti adeguati. Come risultato, è possibile fornire una descrizione audio molto più lunga prima che l’azione riprenda. Come nell’esempio precedente, l’ideale, in questo caso, è includere una traccia audio facoltativa per evitare interruzioni agli utenti che non necessitano della descrizione aggiuntiva.


1. Fornisci una trascrizione testuale che rappresenti un equivalente testuale adatto degli elementi sonori e visivi del video o animazione. Questi dovrebbero includere, a seconda del caso, l’indicazione di chi sta parlando, una descrizione dell’ambientazione, espressioni vocali. A seconda della lunghezza, è possibile inserire la trascrizione nella stessa pagina del video o dell’animazione oppure in una pagina separata. Se scegli la seconda opzione, includi un collegamento alla trascrizione accanto al video o all’animazione.

I dettagli esatti su come creare video con descrizione audio vanno oltre lo scopo di questa guida. La creazione di video e descrizioni audio può richiedere molto tempo, ma altri prodotti Adobe possono facilitare l&#39;esecuzione di tali attività. Se create contenuto in Adobe Flash Professional, dovete anche creare uno script per richiedere all&#39;utente di scaricare il plug-in appropriato e fornire un testo alternativo attraverso l&#39; `<noscript>` elemento .

#### Ulteriori informazioni: descrizione audio o elemento multimediale alternativo (preregistrato) (1.2.3) {#more-information-audio-description-or-media-alternative-pre-recorded}

* [Comprendere i criteri di successo 1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html):
* [Come soddisfare i criteri di successo 1.2.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://www.adobe.com/products/premiere/encore/)

### Sottotitoli (dal vivo) (1.2.4)  {#captions-live}

* Criterio di successo 1.2.4
* Livello AA
* Sottotitoli (dal vivo): i sottotitoli vengono forniti per tutti i contenuti audio dal vivo negli elementi multimediali sincronizzati.

#### Finalità: sottotitoli (in tempo reale) (1.2.4) {#purpose-captions-live}

This success criterion is identical to [Captions (Pre-Recorded)](#captionsprerecorded) in that it addresses accessibility barriers experienced by people who are deaf or hearing-impaired, except that this success criterion deals with live presentations such as webcasts.

#### Come soddisfare il criterio: sottotitoli (dal vivo) (1.2.4) {#how-to-meet-captions-live}

Follow the guidance provided for [Captions (Pre-Recorded)](#captionsprerecorded) above. However, due to the live nature of the media, caption provision has to be created as quickly as possible and in response to what is happening. Therefore, you should consider using real time captioning or speech-to-text tools.

Istruzioni dettagliate al riguardo vanno oltre lo scopo di questo documento, ma informazioni utili sono reperibili tramite le risorse seguenti:

* [WebAIM: Aggiunta di sottotitoli in tempo reale](https://www.webaim.org/techniques/captions/realtime.php)
* [AccessIT (University of Washington): i sottotitoli possono essere generati automaticamente utilizzando il riconoscimento vocale?](https://www.washington.edu/accessit/articles?1209)

#### Ulteriori informazioni: sottotitoli (dal vivo) (1.2.4) {#more-information-captions-live}

* [Comprendere i criteri di successo 1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [Come soddisfare i criteri di successo 1.2.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-real-time-captions)

### Descrizione audio (preregistrato) (1.2.5)  {#audio-description-pre-recorded}

* Criterio di successo 1.2.5
* Livello AA
* Descrizione audio (preregistrato): una descrizione audio viene fornita per tutti i contenuti video preregistrati negli elementi multimediali sincronizzati.

#### Finalità: descrizione audio (preregistrato) (1.2.5) {#purpose-audio-description-pre-recorded}

Questo criterio di successo è identico a [Descrizione audio o elemento multimediale alternativo (preregistrato)](#audiodescriptionormediaalternativeprerecorded), tranne per il fatto che gli autori devono fornire una descrizione audio molto più dettagliata per adeguarsi al livello AA.

#### Come soddisfare il criterio: descrizione audio (preregistrato) (1.2.5) {#how-to-meet-audio-description-pre-recorded}

Segui le indicazioni fornite per [Descrizione audio o elemento multimediale alternativo (preregistrato)](#audiodescriptionormediaalternativeprerecorded).

#### Ulteriori informazioni: descrizione audio (preregistrato) (1.2.5) {#more-information-audio-description-pre-recorded}

* [Comprendere i criteri di successo 1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [Come soddisfare i criteri di successo 1.2.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc-only)

### Adattabilità (1.3) {#adaptable}

[Linea guida 1.3, adattabilità: creare contenuti che possano essere rappresentati in modalità differenti (ad esempio con un layout più semplice) senza perdere informazioni o struttura.](https://www.w3.org/TR/WCAG20/#content-structure-separation)

Questa linea guida riguarda i requisiti necessari per supportare le persone che:

* potrebbe non essere in grado di accedere alle informazioni presentate da un autore in un *layout di pagina Web standard *bidimensionale, a più colonne e a colori

* potrebbero utilizzare una visualizzazione solo audio o una alternativa, ad esempio testo di grandi dimensioni e a contrasto elevato.

### Informazioni e correlazioni (1.3.1)  {#info-and-relationships}

* Criterio di successo 1.3.1
* Livello A
* Informazioni e correlazioni: informazioni, struttura e relazioni veicolate attraverso la presentazione possono essere determinate a livello di programmazione o sono disponibili in formato testo.

#### Finalità: informazioni e correlazioni (1.3.1) {#purpose-info-and-relationships}

Molte tecnologie per l’accessibilità utilizzate da persone con disabilità si basano su informazioni strutturali per visualizzare o rappresentare i contenuti in modo efficace. Queste possono assumere la forma di titoli, intestazioni di righe e colonne di tabella, e tipi di elenchi. Ad esempio, un’utilità di lettura dello schermo potrebbe consentire a un utente di spostarsi all’interno di una pagina passando da un’intestazione a un’altra. Tuttavia, quando la struttura del contenuto della pagina dipende esclusivamente da uno stile visivo, anziché dal codice HTML sottostante, non sono presenti informazioni strutturali utilizzabili dalle tecnologie per l’accessibilità, il che ne limita la capacità di supportare la navigazione facilitata.

Questo criterio di successo esiste per fare in modo che tali informazioni strutturali vengano fornite tramite HTML, in modo che i browser e le tecnologie per l’accessibilità possano accedere e sfruttare le informazioni.

#### Come soddisfare il criterio: informazioni e correlazioni (1.3.1) {#how-to-meet-info-and-relationships}

AEM consente di creare in modo semplice pagine web utilizzando gli elementi HTML appropriati. Apri i contenuti della pagina nell’editor Rich Text (un componente testo) e usa il menu **Formato paragrafo** (simbolo di paragrafo) per specificare l’elemento strutturale appropriato (ad esempio paragrafo, intestazione e così via).

L’immagine seguente mostra il testo che è stato formattato come testo paragrafo.

![Un esempio dell’elemento Paragrafo visualizzato in modalità di modifica del sorgente (interfaccia classica).](assets/screen_shot_2018-03-21at165623.png)

È possibile assicurarsi che alle pagine web sia associata la struttura corretta:

* **Utilizzando i titoli:**

   As long as you have the accessibility features of the RTE enabled (see [AEM and Accessibility](#adobeexperiencemanagerandaccessibility)), AEM offers 3 levels of page heading. You can use these to identify sections and subsections of content. Heading 1 is the highest level of heading, Heading 3 the lowest. The system administrator can configure the system to allow the use of more heading levels.

   L’immagine seguente illustra un esempio dei diversi tipi di titolo.

   ![Titoli da Intestazione 1 a Intestazione 3 visualizzati nel selettore a discesa (interfaccia classica).](assets/screen_shot_2018-03-21at165719.png)

* **Testo con enfasi**:

   Utilizza l’elemento &lt;strong> o &lt;em> per indicare l’enfasi. Non utilizzare i titoli per evidenziare il testo all’interno di paragrafi.

   * Evidenzia il testo che desideri mettere in evidenza.
   * Click on the **B** icon (for &lt;strong>) or the **I** icon (for &lt;em>) shown within the **Properties** panel (make sure that HTML is selected).
   >[!NOTE]
   >
   >L’editor Rich Text in un’installazione standard di AEM è configurato per utilizzare:
   >
   >    * &lt;b> per &lt;strong>
   * &lt;i> per &lt;em>
   Si tratta a tutti gli effetti della stessa cosa, ma &lt;strong> e &lt;em> sono preferibili in quanto tag HTML semanticamente corretti. Il team di sviluppo può configurare l’editor Rich Text per utilizzare &lt;strong> e &lt;em> anziché &lt;b> e &lt;i> nello sviluppo dell’istanza di progetto.

* **Utilizzare gli elenchi**: è possibile utilizzare l’HTML per specificare tre diversi tipi di elenchi:

   * L’ `<ul>` elemento viene utilizzato per gli elenchi *non ordinati* (puntati). Le singole voci dell&#39;elenco sono identificate dall&#39; `<li>` elemento .
Nell’editor Rich Text, utilizza l’icona **Elenco puntato**.

   * L&#39; `<ol>` elemento viene utilizzato per gli elenchi *numerati* *. *I singoli elementi dell&#39;elenco sono identificati utilizzando l&#39; `<li>` elemento .
In the RTE, use the **Numbered List** icon.
   Se desideri convertire contenuti esistenti in un determinato tipo di elenco, evidenzia il testo desiderato e seleziona il tipo di elenco. Come nel precedente esempio, che mostra come inserire un testo di paragrafo, gli elementi elenco adeguati verranno aggiunti automaticamente al codice HTML.

   Nella modalità a schermo intero, le singole icone **Elenco puntato** ed **Elenco numerato** sono visibili. Se non sei in modalità schermo intero, le due opzioni sono disponibili dietro l’icona **Elenchi**.

   ![](do-not-localize/screen_shot_2018-03-21at165756.png)

   >[!NOTE]
   `<dl>` non è supportato dall’editor Rich Text.

* **Utilizzare le tabelle**:

   Le tabelle di dati devono essere identificate utilizzando gli elementi di tabella HTML:

   * one `<table>` element
   * a `<tr>` element for each row of the table
   * a `<th>` element for each row and column heading
   * a `<td>` element for every data cell
   >[!NOTE]
   In the classic UI, tables should be realized with the **Table** component.

   In aggiunta, le tabelle accessibili fanno uso dei seguenti elementi e attributi:

   * L&#39; `<caption>` elemento viene utilizzato per fornire una didascalia visibile per la tabella. Per impostazione predefinita, le didascalie vengono visualizzate centrate sopra la tabella, ma possono essere posizionate in modo appropriato utilizzando i CSS. La didascalia è associata alla tabella a livello di programmazione, pertanto è un metodo utile per fornire un&#39;introduzione al contenuto.
   * L’ `<summary>` elemento aiuta gli utenti non vedenti a comprendere più facilmente le informazioni presentate all’interno di una tabella, fornendo una sintesi di ciò che un utente vedente può vedere. Questo è particolarmente utile quando si utilizzano layout di tabella complessi o non convenzionali (questo attributo non viene visualizzato nel browser, ma viene letto solo alle tecnologie di assistenza).
   * L&#39; `scope` attributo dell&#39; `<th>` elemento viene utilizzato per indicare se una cella rappresenta un&#39;intestazione per una particolare riga o per una particolare colonna. Un approccio simile consiste nell’utilizzare gli attributi header e id in tabelle complesse, dove le celle di dati possono essere associate a una o più intestazioni.
   >[!NOTE]
   By default, these elements and attributes are not directly available, though it is possible for the system administrator to add support for these values in the **Table properties** dialog box (see [Adding Support for Additional HTML Elements and Attributes](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)).

   Quando aggiungi una **Tabella**, puoi configurare le **Proprietà tabella** utilizzando:

   ![cac-02](assets/cac-02.png)

   Per aprire la finestra di dialogo **Tabella** in cui puoi selezionare le **Proprietà tabella**:

   * Definisci una **Didascalia** appropriata.
   * È consigliabile rimuovere eventuali valori predefiniti per **Larghezza**, **Altezza**, **Bordo**, **Margine celle** e **Spaziatura celle**, in quanto queste proprietà possono essere impostate in un foglio di stile globale.
   ![cac-01](assets/cac-01.png)

   Puoi quindi utilizzare le **Proprietà cella** per scegliere se la cella contiene dati o intestazione:

   ![cac-03](assets/cac-03.png)

* **Tabelle di dati complesse**:

   In some cases, where there are complex tables with two or more levels of headers, then the basic Table Properties may not be enough to provide all the structural information necessary. For these kinds of complex tables, direct relationships need to be created between the headers and their related cells using the **header** and **id** attributes. For example, in the table below headers and ids are matched to make a programmatic association for assistive technology users.

   >[!NOTE]
   L’attributo id non è disponibile in un’installazione standard. Può essere attivato configurando regole HTML e il serializzatore nell’editor Rich Text.

   >[!NOTE]
   In classic UI, tables should be realized with the **Table** component.

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
   Questa funzionalità non è immediatamente disponibile in un’installazione standard. Richiede la configurazione dell’editor Rich Text, di regole HTML e del serializzatore.

#### Ulteriori informazioni: informazioni e correlazioni (1.3.1) {#more-information-info-and-relationships}

* [Comprendere i criteri di successo 1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [Come soddisfare i criteri di successo 1.3.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-programmatic)

### Caratteristiche sensoriali (1.3.3)  {#sensory-characteristics}

* Criterio di successo 1.3.3
* Livello A
* Caratteristiche sensoriali: le istruzioni fornite per comprendere e intervenire sui contenuti non si basano unicamente su caratteristiche sensoriali dei componenti quali forma, dimensione, ubicazione visiva, orientamento o audio.

#### Finalità: caratteristiche sensoriali (1.3.3) {#purpose-sensory-characteristics}

Nel presentare le informazioni, i designer spesso si concentrano sulle caratteristiche di progettazione visiva come il colore, la forma, lo stile del testo o la posizione assoluta o relativa di un elemento di contenuto. Anche se queste possono essere tecniche di progettazione molto potenti per veicolare le informazioni, le persone non vedenti o ipovedenti potrebbero non essere in grado di accedere alle informazioni che richiedono l’identificazione visiva di attributi come la posizione, il colore o la forma.

Allo stesso modo, le informazioni che richiedono di distinguere tra suoni diversi (ad esempio, contenuti parlati da voci di sesso maschile o femminile) presenteranno problemi di accessibilità per le persone con disabilità uditive, se non vengono incluse in un testo alternativo per il contenuto audio.

>[!NOTE]
Per i requisiti collegati alle alternative ai colori, consulta [Utilizzo del colore](#use-of-color).

#### Come soddisfare il criterio: caratteristiche sensoriali (1.3.3) {#how-to-meet-sensory-characteristics}

Assicurati che tutte le informazioni che si basano su caratteristiche visive del contenuto di pagina siano presentate anche in un formato alternativo.

* Non fare affidamento sulla posizione visiva per fornire informazioni. Ad esempio, se desideri indirizzare gli utenti a un menu sul lato destro della pagina per l’accesso alle informazioni, non fare riferimento al *menu a destra*, ma denomina il menu (ad esempio attraverso un’intestazione) e fai riferimento al nome nel testo.
* Non fare affidamento sullo stile del testo (ad esempio, testo in grassetto o in corsivo) come unico modo per trasmettere le informazioni.

>[!NOTE]
L’utilizzo di termini descrittivi sarà accettabile se questi hanno un significato in un contesto non visivo. Ad esempio, l’utilizzo dei termini *sopra* e *sotto* sarà generalmente accettabile, in quanto si riferiscono rispettivamente al contenuto prima e dopo un particolare elemento di contenuto; questa indicazione continuerà ad avere senso quando il contenuto è parlato.

#### Ulteriori informazioni: caratteristiche sensoriali (1.3.3) {#more-information-sensory-characteristics}

* [Comprendere i criteri di successo 1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [Come soddisfare i criteri di successo 1.3.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-understanding)

### Distinguibilità (1.4) {#distinguishable}

[Linea guida 1.4, distinguibilità: facilitare agli utenti la visione e l’ascolto dei contenuti, separando gli elementi in primo piano dallo sfondo.](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### Utilizzo del colore (1.4.1)  {#use-of-color}

* Criterio di successo 1.4.1
* Livello A
* Utilizzo del colore: il colore non è utilizzato come unica modalità visiva per rappresentare le informazioni, indicare un’azione, richiedere una risposta o distinguere un elemento visivo.

>[!NOTE]
Questo criterio di successo riguarda in particolare la percezione del colore. Altre forme di percezione sono illustrate in [Adattabilità (1.3)](#adaptable); compreso l’accesso programmatico al colore e ad altre codifiche presentazione visiva.

#### Finalità: utilizzo del colore (1.4.1) {#purpose-use-of-color}

Il colore è un modo efficace per valorizzare l’estetica delle pagine web ed è anche utile per trasmettere informazioni. Tuttavia, esistono una serie di problemi visivi, dalla cecità al daltonismo, che rendono alcune persone incapaci di distinguere tra alcuni colori. Questo rende la codifica tramite colori un modo inaffidabile per fornire informazioni.

Ad esempio, un soggetto con un deficit della visione dei colori rosso-verde non sarà in grado di distinguere tra sfumature di verde e di rosso. Potrà percepire entrambi i colori come un terzo (ad esempio, marrone), nel qual caso non sarà in grado di distinguere tra rosso, verde e marrone.

Inoltre, il colore non può essere percepito da persone che utilizzano browser di solo testo, dispositivi di visualizzazione in bianco e nero o una stampa in bianco e nero della pagina.

#### Come soddisfare il criterio: utilizzo del colore (1.4.1) {#how-to-meet-use-of-color}

Qualunque colore sia utilizzato per trasmettere le informazioni, accertati che queste siano disponibili senza che sia necessario vedere il colore stesso.

Ad esempio, assicurati che le informazioni fornite in base al colore siano anche comunicate esplicitamente nel testo. L’illustrazione seguente mostra in che modo colore e testo indicano entrambi la disponibilità di posti a sedere per uno spettacolo:

<table>
 <tbody>
  <tr>
   <td><p><strong>Spettacolo</strong></p> </td>
   <td><p><strong>Disponibilità</strong></p> </td>
  </tr>
  <tr>
   <td><p>Martedì 16<sup></sup> marzo</p> </td>
   <td><p>POSTI DISPONIBILI</p> </td>
  </tr>
  <tr>
   <td><p>Mercoledì 17 marzo</p> </td>
   <td><p>POSTI DISPONIBILI</p> </td>
  </tr>
  <tr>
   <td><p>Giovedì 18<sup></sup> marzo</p> </td>
   <td><p>ESAURITI</p> </td>
  </tr>
 </tbody>
</table>

Se il colore è usato come mezzo per fornire informazioni, è necessario includere un&#39;indicazione visiva aggiuntiva, ad esempio la modifica dello stile (grassetto, corsivo) o del carattere. Questo aiuta le persone con problemi di vista o daltonismo a identificare le informazioni. Non è un metodo completamente affidabile, tuttavia, in quanto non aiuterà chi non può visualizzare del tutto la pagina.

#### Ulteriori informazioni: utilizzo del colore (1.4.1) {#more-information-use-of-color}

* [Comprendere i criteri di successo 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Come soddisfare i criteri di successo 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Indicazioni per ottenere un rapporto di contrasto 3:1, che include un elenco di colori “web safe”](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### Contrasto (minimo) (1.4.3) {#contrast-minimum}

* Criterio di successo 1.4.3
* Livello AA
* Contrasto (minimo): la rappresentazione visiva di testo e immagini di testo ha un rapporto di contrasto pari ad almeno 4,5:1, fatta eccezione per i seguenti elementi:

   * Testo di grandi dimensioni: testo di grandi dimensioni e immagini di testo di grandi dimensioni hanno un rapporto di contrasto di almeno 3:1.
   * Incidentale: per il testo o per le immagini di testo che fanno parte di un componente dell’interfaccia inattivo, che sono puramente decorative, non visibili o che fanno parte di un’immagine che contiene altri contenuti visuali significativi, non è previsto alcun requisito di contrasto.
   * Logotipi: per il testo che fa parte di un logo o di un marchio non è previsto alcun requisito minimo di contrasto.

#### Finalità: contrasto (minimo) (1.4.3) {#purpose-contrast-minimum}

Le persone con determinate disabilità visive possono non essere in grado di distinguere tra alcune coppie di colori a basso contrasto. Queste persone possono riscontrare problemi di accessibilità se:

* Il testo contrasta poco con il relativo colore di sfondo.
* La codifica di colore del testo (come testo di collegamento e testo non di collegamento) è importante per distinguere le informazioni.

>[!NOTE]
Il testo utilizzato esclusivamente per scopi decorativi è escluso da questo criterio di successo.

#### Come soddisfare il criterio: contrasto (minimo) (1.4.3) {#how-to-meet-contrast-minimum}

Assicurati che il testo contrasti a sufficienza con il relativo sfondo. I rapporti di contrasto dipendono dalle dimensioni e dallo stile del testo:

* Per testi con dimensioni inferiori a 18 punti (o 14 se in grassetto), il rapporto di contrasto tra testo/immagini di testo e sfondo deve essere pari ad almeno 4,5:1.
* Per testi con dimensioni almeno pari a 18 punti (o 14 se in grassetto), il rapporto di contrasto deve essere pari ad almeno 3:1.
* Se lo sfondo include un motivo, lo sfondo intorno al testo dovrà essere ombreggiato in modo da mantenere il rapporto di 4,5:1 o 3:1.

Per controllare i rapporti di contrasto, utilizza uno strumento di contrasto del colore, come ad esempio [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) o [l’utilità di controllo del contrasto di colore di WebAIM](https://www.webaim.org/resources/contrastchecker/). Questi strumenti consentono di controllare le coppie di colori ed evidenziano eventuali problemi di contrasto.

In alternativa, se la specificazione dell’aspetto della pagina non è un problema, è possibile scegliere di non specificare colori di sfondo e del testo in primo piano. In questo caso non sarà necessario alcun controllo del contrasto, in quanto sarà il browser dell’utente a determinare i colori del testo e dello sfondo.

Se non è possibile rispettare i livelli di contrasto raccomandati, sarà necessario fornire un collegamento a una versione alternativa ed equivalente della pagina (senza problemi di contrasto di colore) o consentire all’utente di regolare il contrasto dello schema di colore della pagina in base alle proprie esigenze.

#### Ulteriori informazioni: contrasto (minimo) (1.4.3) {#more-information-contrast-minimum}

* [Comprendere i criteri di successo 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [Come soddisfare i criteri di successo 1.4.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-contrast)

### Immagini di testo (1.4.5) {#images-of-text}

* Criterio di successo 1.4.5
* Livello AA
* Immagini di testo: se le tecnologie utilizzate consentono la presentazione visiva, per trasmettere informazioni viene utilizzato il testo, anziché le immagini di testo, con le seguenti eccezioni:

   * Personalizzabile: l’immagine di testo può essere personalizzata visivamente in base alle esigenze dell’utente;
   * Essenziale: una particolare presentazione del testo è essenziale per il tipo di informazioni veicolate.

>[!NOTE]
I logotipi (testo che fa parte di un logo o di un marchio) sono considerati essenziali.

#### Finalità: immagini di testo (1.4.5) {#purpose-images-of-text}

Le immagini di testo vengono spesso utilizzate quando un particolare stile di testo è quello preferenziale (ad esempio un logo) o se il testo è stato generato da un’altra sorgente (ad esempio la scansione di un documento cartaceo). Tuttavia, rispetto al testo presentato in HTML e formattato mediante i CSS, le immagini di testo non hanno la flessibilità necessaria per modificarsi in dimensioni o aspetto nel modo che potrebbe essere necessario per le persone con disabilità visive o difficoltà di lettura.

#### Come soddisfare il criterio: immagini di testo (1.4.5) {#how-to-meet-images-of-text}

Se è necessario utilizzare le immagini di testo, utilizza i CSS per sostituire le immagini di testo con testo equivalente in HTML, in modo che il testo sia disponibile in un modo personalizzabile. Per un esempio su come ottenere questo risultato, fai riferimento a [C30: Utilizzo di CSS per sostituire testo con immagini di testo e fornitura di controlli di interfaccia per eseguire il passaggio](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Ulteriori informazioni: immagini di testo (1.4.5) {#more-information-images-of-text}

* [Comprendere i criteri di successo 1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [Come soddisfare i criteri di successo 1.4.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-text-presentation)

## Principio 2: Operabilità {#principle-operable}

[Principio 2, operabilità: i componenti dell’interfaccia e la navigazione devono essere operabili.](https://www.w3.org/TR/WCAG20/#operable)

### Sospendi, Arresta, Nascondi (2.2.2)  {#pause-stop-hide}

* Criterio di successo 2.2.2
* Livello A
* Sospendi, Arresta, Nascondi: per le informazioni in movimento, lampeggianti, scorrevoli o con aggiornamento automatico, vale quanto segue:

   * Spostamento, lampeggiamento, scorrimento: per qualsiasi informazione in movimento, lampeggiante o scorrevole che (a) parta automaticamente, (b) duri più di cinque secondi, e (c) sia rappresentata in parallelo con altro contenuto, esiste un meccanismo che consente all’utente di mettere in pausa, interrompere o nascondere l’effetto, a meno che questo non sia parte di un’attività per la quale è essenziale;
   * Aggiornamento automatico: per qualsiasi informazione con aggiornamento automatico che (a) parta automaticamente e (b) sia rappresentata in parallelo con altro contenuto, esiste un meccanismo che consente all’utente di mettere in pausa, interrompere o nascondere il contenuto, oppure controllare la frequenza dell’aggiornamento, a meno che questo non sia parte di un’attività per la quale è essenziale;

Elementi da sottolineare:

1. Per i requisiti relativi a contenuti che sfarfallano o lampeggiano, consulta [Non progettare contenuti con modalità che possano causare attacchi epilettici (2.3)](#donotdesigncontentinawaythatisknowntocauseseizures23).
1. Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (utilizzato per soddisfare altri criteri di successo o meno) deve rispondere a questo criterio. Consulta [Requisito di conformità 5: Non interferenza](https://www.w3.org/TR/WCAG20/#cc5).
1. I contenuti aggiornati periodicamente dal software o trasmessi in streaming all’agente dell’utente non sono tenuti a conservare o presentare le informazioni generate o ricevute tra l’inizio della pausa e la ripresa della presentazione, in quanto questo potrebbe non essere tecnicamente possibile e, in molte situazioni, potrebbe essere fuorviante.
1. Un’animazione che si verifica come parte di una fase di precaricamento, o situazione similare, può essere considerata essenziale se l’interazione non può verificarsi durante quella fase per tutti gli utenti e se la mancata indicazione dell’avanzamento potrebbe confondere gli utenti o far loro pensare che il contenuto sia bloccato o guasto.

#### Finalità: Sospendi, Arresta, Nascondi (2.2.2) {#purpose-pause-stop-hide}

Per alcuni utenti i contenuti in movimento potrebbero essere fonte di distrazione e impedire di concentrarsi su altre parti della pagina. Inoltre, tali contenuti possono risultare di difficile lettura per chi abbia difficoltà a tenere il passo con il testo in movimento.

#### Come soddisfare il criterio: Sospendi, Arresta, Nascondi (2.2.2) {#how-to-meet-pause-stop-hide}

In base alla natura del contenuto, è possibile applicare uno o più dei seguenti suggerimenti durante la creazione di pagine web che includono contenuti in movimento, con effetti di sfarfallio o lampeggiamento:

* Fornisci un mezzo per mettere in pausa lo scorrimento dei contenuti, in modo che gli utenti abbiano il tempo di leggerli. Ad esempio, un componente tipo telescrivente o un testo con aggiornamento automatico.
* Assicurati che il contenuto smetta di lampeggiare dopo cinque secondi.
* Utilizza tecnologie appropriate per visualizzare contenuto lampeggiante che possa essere disabilitato dal browser. Ad esempio, file Graphics Interchange Format (GIF) o Animated Portable Network Graphics (APNG).
* Includi un controllo di modulo nella pagina web per consentire all’utente di disattivare tutti i contenuti lampeggianti nella pagina.
* Se nessuno degli accorgimenti di cui sopra è praticabile, fornisci un collegamento a una pagina contenente tutti i contenuti, ma senza effetti di lampeggiamento.

#### Ulteriori informazioni: Sospendi, Arresta, Nascondi (2.2.2) {#more-information-pause-stop-hide}

* [Comprendere il criterio di successo 2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [Come soddisfare il criterio di successo 2.2.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-time-limits-pause)

### Attacchi epilettici (2.3) {#seizures}

[Linea guida 2.3, attacchi epilettici: non progettare contenuti con modalità che possano causare attacchi epilettici.](https://www.w3.org/TR/WCAG20/#seizure)

### Tre lampeggiamenti o sotto la soglia (2.3.1) {#three-flashes-or-below-threshold}

* Criterio di successo 2.3.1
* Livello A
* Tre lampeggiamenti o sotto la soglia: le pagine web non devono contenere alcun elemento che lampeggi per più di tre volte al secondo, oppure il lampeggiamento deve essere inferiore alle soglie di lampeggiamento generale e rosso.

>[!NOTE]
Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (utilizzato per soddisfare altri criteri di successo o meno) deve rispondere a questo criterio. Consulta [Requisito di conformità 5: Non interferenza](https://www.w3.org/TR/WCAG20/#cc5).

#### Finalità: tre lampeggiamenti o sotto la soglia (2.3.1) {#purpose-three-flashes-or-below-threshold}

In alcuni casi i contenuti lampeggianti possono causare crisi epilettiche dovute a fotosensibilità. Questo criterio di successo consente agli utenti a rischio di accedere e utilizzare tutti i contenuti, senza preoccuparsi di eventuali contenuti lampeggianti.

#### Come soddisfare il criterio: tre lampeggiamenti o sotto la soglia (2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

È consigliabile adottare misure per assicurare che siano applicate le seguenti tecniche:

* Assicurati che i componenti non lampeggino per più di tre volte al secondo;
* If the above condition cannot be met, then display flashing content within a *small safe area* in pixels on the screen. This area is calculated using a complex formula, covered in [G176: Keeping the flashing area small enough](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), so this technique should only be followed if flashing content is *absolutely* necessary.

#### Ulteriori informazioni: tre lampeggiamenti o sotto la soglia (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Comprendere il criterio di successo 2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [Come soddisfare il criterio di successo 2.3.1](https://www.w3.org/WAI/WCAG20/quickref/#seizure)

### Pagina con titolo (2.4.2)  {#page-titled}

* Criterio di successo 2.4.2
* Livello A
* Pagina con titolo: alle pagine web sono associati titoli che ne descrivono argomento o finalità.

#### Finalità: pagina con titolo (2.4.2) {#purpose-page-titled}

Questo criterio di successo consente a tutti gli utenti, indipendentemente da eventuali particolari disabilità, di identificare rapidamente il contenuto di una pagina web senza leggere la pagina completa. Questo è particolarmente utile quando più pagine web vengono aperte in altrettante schede del browser, in quanto il titolo della pagina è indicato nella scheda e quindi può essere individuato rapidamente.

#### Come soddisfare il criterio: pagina con titolo (2.4.2) {#how-to-meet-page-titled}

Quando si crea una nuova pagina HTML in AEM, è possibile specificare il titolo della pagina. Assicurati che il titolo descriva adeguatamente il contenuto della pagina, in modo che i visitatori possano verificare velocemente se è effettivamente pertinente alle loro esigenze.

You can also edit the page title when editing a page, which is accessible by **Page Information** - **Properties.**

#### Ulteriori informazioni: pagina con titolo (2.4.2) {#more-information-page-titled}

* [Comprendere il criterio di successo 2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [Come soddisfare il criterio di successo 2.4.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-title)

### Scopo del collegamento (nel contesto) (2.4.4)  {#link-purpose-in-context}

* Criterio di successo 2.4.4
* Livello A
* Scopo del collegamento (nel contesto): lo scopo di ogni collegamento può essere determinato esclusivamente dal testo di collegamento, oppure dal testo di collegamento insieme al suo contesto, determinato a livello di programmazione, a meno che lo scopo del collegamento possa risultare ambiguo per gli utenti in generale.

#### Finalità: scopo del collegamento (nel contesto) (2.4.4) {#purpose-link-purpose-in-context}

Per tutti gli utenti, indipendentemente da un’eventuale disabilità, indicare chiaramente la direzione di un collegamento tramite apposito testo è di vitale importanza. Questo aiuta gli utenti a decidere se vogliono effettivamente seguire un collegamento. Per i normovedenti, un testo di collegamento significativo è estremamente utile laddove in una pagina siano presenti più collegamenti (in particolare se la pagina è molto ricca di testo), in quanto fornisce un’indicazione più chiara delle funzionalità della pagina di destinazione. Gli utenti di tecnologie per l’accessibilità, in grado di generare un elenco di tutti i collegamenti su una sola pagina, dal canto loro potranno comprendere più facilmente il testo di collegamento fuori dal contesto.

#### Come soddisfare il criterio: scopo del collegamento (nel contesto) (2.4.4) {#how-to-meet-link-purpose-in-context}

Soprattutto, fai in modo che lo scopo di un collegamento sia chiaramente descritto all’interno del testo di collegamento.

* Esempio di utilizzo non corretto:

   * Testo: per i dettagli sui nostri corsi serali per l’autunno 2010, fai clic qui.
   * Motivo: non indica in modo chiaro e senza ambiguità la destinazione.

* Esempio di utilizzo corretto:

   * Testo: Corsi serali per l&#39;autunno 2010 - dettagli.
   * Motivo: modificando leggermente il testo e la posizione dell’elemento di collegamento è possibile migliorare il testo di collegamento:

Links should be phrased consistently across pages, especially for navigation bars. For example, if a link to a specific page is named **Publications** on one page, use that text on other pages to ensure consistency.

Al momento in cui scriviamo, tuttavia, l’uso dei titoli pone alcuni problemi:

* Il testo contenuto all’interno dell’attributo title è generalmente disponibile solo a chi utilizza un mouse, sotto forma di pop-up con la descrizione comando, e non è accessibile utilizzando la tastiera.
* Le utilità di lettura dello schermo possono leggere gli attributi title, ma questa funzionalità potrebbe non essere abilitata per impostazione predefinita; è quindi possibile che gli utenti non siano a conoscenza dell’esistenza di un attributo title.
* È difficile modificare l’aspetto del testo del titolo, il che significa che leggerlo può risultare difficile o impossibile per alcuni utenti.

Così, mentre l’attributo title può essere utilizzato per fornire contesto aggiuntivo per un collegamento, è importante essere consapevoli dei suoi limiti e non utilizzarlo come alternativa a un testo collegamento adeguato.

Where the link is made up of an image, make sure that the alternative text for the image describes the destination of the link. For example, if an image of a bookshelf is set as a link to a person’s publications, the alternative text should read **John Smith’s publications** and not **Bookshelf**.

In alternativa, se nell’ancoraggio del collegamento è incluso testo che descrive lo scopo del collegamento in aggiunta all’elemento immagine (e, quindi, il testo viene visualizzato a fianco dell’immagine), utilizza un attributo alt vuoto per l’immagine:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
Il frammento di codice sopra ha esclusivamente scopo illustrativo; si consiglia di utilizzare il componente **Immagine**.

While it’s advisable to provide link text that identifies the purpose of the link without needing additional context, it is recognized that this is not always possible. Context free links can be used in the following cases, HTML examples of which can be found in [How to Meet Success Criterion 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs).

* Qualora il testo di collegamento sia parte di un elenco di collegamenti strettamente correlati, e la voce di elenco che racchiude il collegamento fornisca contesto sufficiente.
* Where the purpose of a link can be clearly identified from the *preceding* (not the following) paragraph text.
* Se il collegamento è contenuto all’interno di una tabella di dati, e quindi la finalità può essere chiaramente identificata a partire dalle intestazioni associate.
* Se un elenco di collegamenti è contenuto all’interno di un insieme di intestazioni e l’intestazione fornisce il contesto adatto.
* Se un elenco di collegamenti è contenuto all’interno di un collegamento nidificato e la voce dell’elenco principale rispetto al collegamento nidificato fornisce il contesto adatto.

In alcuni casi, laddove in una pagina siano presenti diversi collegamenti (ciascuno dei quali fornisca la direzione di un collegamento con dettagli complessi ma necessari), può essere opportuno prevedere una versione alternativa della pagina web che mostri lo stesso contenuto, ma in cui il testo dei collegamenti non sia così dettagliato.

Alternatively, scripts can be used so that a minimal amount of text is provided within the link itself, but on activating an appropriate control positioned towards the top of the page, the link text is *expanded* into further detail. A similar approach is to use CSS to *hide* the full link from sighted users, but still output it in full to screen reader users. This falls outside the scope of this document, but more information on how this can be achieved can be found in the [More Information - Link Purpose (In Context) (2.4.4)](#more-information-link-purpose-in-context) section.

#### Ulteriori informazioni: scopo del collegamento (nel contesto) (2.4.4) {#more-information-link-purpose-in-context}

* [Comprendere il criterio di successo 2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [Come soddisfare il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs)
* [C7: Utilizzo dei CSS per nascondere una parte del testo di collegamento](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## Principio 3: Comprensibilità {#principle-understandable}

[Principio 3, comprensibilità: le informazioni e le operazioni dell’interfaccia devono essere comprensibili.](https://www.w3.org/TR/WCAG20/#understandable)

### Rendere il testo leggibile e comprensibile (3.1) {#make-text-content-readable-and-understandable}

[Linea guida 3.1, leggibilità: rendere il testo leggibile e comprensibile.](https://www.w3.org/TR/WCAG20/#meaning)

### Lingua della pagina (3.1.1) {#language-of-page}

* Criterio di successo 3.1.1
* Livello A
* Lingua della pagina: la lingua predefinita di ogni pagina web può essere determinata a livello di programmazione.

#### Finalità: lingua della pagina (3.1.1) {#purpose-language-of-page}

Lo scopo di questo criterio è fare in modo che il testo e gli altri contenuti linguistici siano resi correttamente. Per gli utenti di utilità di lettura dello schermo, questo garantisce che la pronuncia sia corretta, mentre i browser visivi saranno più propensi a visualizzare certi set di caratteri correttamente.

#### Come soddisfare il criterio: lingua della pagina (3.1.1) {#how-to-meet-language-of-page}

To meet this success criterion, the default language of a web page can be identified using the `lang` attribute within the `<html>` element at the top of the page. Esempio:

* If a page is written in British English, the `<html>` element should read:
   `<html lang = “en-gb”>`

* Mentre una pagina da renderizzare come inglese americano dovrebbe adottare il seguente standard:
   `<html lang = “en-us”>`

**In AEM, la lingua predefinita della pagina è impostata durante la creazione, ma può anche essere modificata durante la modifica di una pagina, accessibile dalla barra** laterale **- scheda** Pagina **- Proprietà** pagina. - scheda **Avanzate** .

#### Ulteriori informazioni: lingua della pagina (3.1.1) {#more-information-language-of-page}

* [Comprendere il criterio di successo 3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [Come soddisfare il criterio di successo 3.1.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-doc-lang-id)
* I codici sono basati su ISO 639-1. Un elenco più completo dei codici per ogni lingua è reperibile sul [sito W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Lingua delle parti (3.1.2)  {#language-of-parts}

* Criterio di successo 3.1.2
* Livello AA
* Lingua delle parti: la lingua di ogni passaggio o frase nel contenuto può essere determinata a livello di programmazione, fatta eccezione per nomi propri, termini tecnici, parole in lingue indeterminate e parole o frasi che sono diventate parte del gergo del testo immediatamente circostante.

#### Finalità: lingua delle parti (3.1.2) {#purpose-language-of-parts}

Lo scopo di questo criterio di successo è simile a quello del criterio [Lingua della pagina](#languageofpage), ma si applica a pagine web con contenuti multilingue all’interno di una singola pagina (ad esempio, a causa di citazioni o prestiti lessicali non comuni).

Le pagine che applicano questo criterio di successo consentono:

* Inserimento di caratteri accentati da parte di software di transizione Braille.
* Pronuncia corretta da parte dell’utilità di lettura dello schermo di quelle parole che non siano nella lingua predefinita.
* Traduzione corretta del contenuto da una lingua all’altra da parte di strumenti di traduzione come Google Translate.

#### Come soddisfare il criterio: lingua delle parti (3.1.2) {#how-to-meet-language-of-parts}

L&#39; `lang` attributo può essere utilizzato per identificare le modifiche nella lingua del contenuto. Ad esempio, una quotazione in tedesco (codice ISO 639-1 &quot;de&quot;) può essere mostrata come segue:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
Gli elementi blockquote non sono supportati in un’istanza standard. Un componente personalizzato può essere sviluppato per supportare la funzione.

Analogamente, il browser può rappresentare correttamente un prestito lessicale non comune o una frase se l’elemento `span` viene utilizzato come segue:

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
Non è necessario seguire questo criterio di successo per nomi o città in lingue diverse, o quando si utilizzano prestiti lessicali o frasi diventati comuni nella lingua predefinita (come *schadenfreude* in inglese).

Per aggiungere l’elemento span, con una lingua appropriata, è possibile modificare manualmente il codice HTML nella modalità di modifica sorgente dell’editor Rich Text in modo che venga letto come sopra. In alternativa, l’ `lang` attributo può essere incluso nell’editor Rich Text da un amministratore di sistema (consultate [Aggiunta di supporto per elementi e attributi](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)HTML aggiuntivi).

#### Ulteriori informazioni: lingua delle parti (3.1.2) {#more-information-language-of-parts}

* [Comprendere il criterio di successo 3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.htm)
* [Come soddisfare il criterio di successo 3.1.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-other-lang-id)

### Aiutare gli utenti a evitare e correggere gli errori (3.3) {#help-users-avoid-and-correct-mistakes}

[Linea guida 3.3, assistenza nell’inserimento: aiutare gli utenti a evitare e correggere gli errori.](https://www.w3.org/TR/WCAG20/#minimize-error)

### Etichette o istruzioni (3.3.2) {#labels-or-instructions}

* Criterio di successo 3.3.2
* Livello A
* Etichette o istruzioni: etichette o istruzioni vengono fornite quando il contenuto richiede l’input dell’utente.

#### Finalità: etichette o istruzioni (3.3.2) {#purpose-labels-or-instructions}

Fornire istruzioni per facilitare la compilazione dei moduli è una parte fondamentale delle buone pratiche nell’ambito dell’usabilità dell’interfaccia. Questo è particolarmente utile per le persone con disabilità visive o cognitive, che altrimenti potrebbero avere difficoltà nel comprendere il layout di un modulo e il tipo di dati da fornire in un particolare campo.

In AEM un’etichetta predefinita viene aggiunta quando si aggiunge alla pagina un componente di modulo, come ad esempio un **Campo testo**. Questo titolo predefinito dipende dal tipo di componente; è possibile aggiungere un titolo personalizzato nella scheda **Titolo e testo** della finestra di dialogo di modifica per quel campo. È importante fare in modo che le etichette consentano agli utenti di comprendere i dati associati a ciascun componente del modulo.

![cac-04](assets/cac-04.png)

Il campo **Titolo** deve essere utilizzato per gli elementi di campo in quanto fornisce un’etichetta che è disponibile per la tecnologia per l’accessibilità. Scrivere semplicemente un’etichetta di testo accanto al campo non è sufficiente.

For some form components it is also possible to visually hide labels using the **Hide Title** checkbox. Labels hidden in this way are still available to assistive technology, but not displayed on the screen. While this can be a good approach in some situations it is usually best to include a visual label wherever possible, as some users may be looking at a very small section of the screen (one field at a time) and need the labels to identify the field correctly.

#### Pulsanti immagine {#image-buttons}

Se si utilizzano i pulsanti immagine (ad esempio, il componente Pulsante **** immagine), il campo **Titolo** nella scheda **Titolo e testo** della finestra di dialogo di modifica fornisce effettivamente il testo alternativo per l’immagine, anziché l’etichetta. Nell’esempio seguente, l’immagine con il testo `Submit` ha testo alternativo `Submit`, aggiunto utilizzando il campo **Titolo** nella finestra di dialogo di modifica.

![cac-05](assets/cac-05.png)

#### Gruppi di campi modulo {#groups-of-form-fields}

Dove è presente un gruppo di controlli correlati, come un **Gruppo pulsanti di scelta**, per il gruppo così come per i singoli controlli può essere necessario un titolo. Quando si aggiunge una serie di pulsanti di scelta in AEM, il campo **Titolo** fornisce questo titolo per il gruppo, mentre i singoli titoli sono specificati alla creazione dei pulsanti di scelta (**Elementi**).

![cac-06](assets/cac-06.png)

Tuttavia, non esiste alcuna associazione programmatica tra il titolo del gruppo e i pulsanti di scelta stessi. Per creare questa associazione, gli editor di modelli dovranno racchiudere il titolo nei `fieldset` tag necessari `legend` e solo modificando il codice sorgente della pagina. In alternativa, un amministratore di sistema può aggiungere il supporto per questi elementi in modo che vengano visualizzati nella finestra di dialogo Proprietà **** campo (consultate [Aggiunta del supporto per elementi e attributi](/help/sites-administering/rte-accessible-content.md#adding-support-for-additional-html-elements-and-attributes)HTML aggiuntivi).

#### Considerazioni aggiuntive relative ai moduli {#additional-considerations-for-forms}

Se i dati devono essere immessi in un formato specifico, specificatelo chiaramente nel testo dell&#39;etichetta. Ad esempio, se una data deve essere inserita nel `DD-MM-YYYY` formato, specificatela come parte dell&#39;etichetta. Ciò significa che quando gli utenti dell&#39;assistente vocale incontrano il campo, l&#39;etichetta viene annunciata automaticamente, insieme alle informazioni aggiuntive sul formato.

Se l&#39;input per un campo modulo è obbligatorio, specificarlo utilizzando la parola obbligatorio come parte dell&#39;etichetta. AEM aggiunge un asterisco quando un campo è obbligatorio, ma sarebbe ideale includere la parola `required`nell’etichetta stessa (nel campo **Titolo** della finestra di dialogo di modifica).

![cac-07](assets/cac-07.png)

Il posizionamento delle etichette è importante anche in quanto aiuta a individuare campi appropriati. Questo è di particolare importanza quando l’utente si trova di fronte a un modulo complesso. Segui la convenzione qui di seguito:

* Caselle di selezione o pulsanti di scelta: Le etichette sono posizionate immediatamente a destra del campo.
* Tutti gli altri componenti del modulo (ad esempio caselle di testo, caselle combinate): Le etichette sono posizionate immediatamente sopra o a sinistra del campo.

Nei moduli semplici con funzionalità molto limitata, l&#39;etichettatura appropriata di un `Submit` pulsante può fungere da etichetta per il campo adiacente (ad esempio `Search`). Ciò è utile in situazioni in cui trovare spazio per il testo dell&#39;etichetta potrebbe essere difficile.

#### Ulteriori informazioni: etichette o istruzioni (3.3.2) {#more-information-labels-or-instructions}

* [Comprendere il criterio di successo 3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [Come soddisfare il criterio di successo 3.3.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-minimize-error-cues)

