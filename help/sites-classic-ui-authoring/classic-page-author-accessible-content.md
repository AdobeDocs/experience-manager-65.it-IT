---
title: Creazione di contenuto accessibile (conformità WCAG 2.0)
description: Le linee guida WCAG 2.0 sono costituite da un insieme di criteri di successo e linee guida che non dipendono dalla tecnologia in uso e hanno l’obiettivo di rendere i contenuti web accessibili e utilizzabili da persone con disabilità.
page-status-flag: de-activated
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 01c69aa9-2623-42dc-9e2d-62bc5e01cf0e
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '9070'
ht-degree: 59%

---

# Creazione di contenuto accessibile (conformità WCAG 2.0){#creating-accessible-content-wcag-conformance}

>[!CAUTION]
>
>Poiché l’interfaccia classica è stata rimossa in AEM 6.4, il contenuto di questa pagina non è stato aggiornato per WCAG 2.1.
>
>Per informazioni dettagliate relative a AEM e WCAG 2.1, consulta le pagine seguenti:
>
>* [AEM e le linee guida per l&#39;accessibilità dei contenuti web](/help/managing/web-accessibility.md)
>* [Guida rapida alle linee guida WCAG 2.1](/help/managing/qg-wcag.md)
>* [Creazione di contenuto accessibile (conformità WCAG 2.1)](/help/sites-authoring/creating-accessible-content.md)

Le linee guida WCAG 2.0 sono costituite da un insieme di criteri di successo e linee guida che non dipendono dalla tecnologia in uso e hanno l’obiettivo di rendere i contenuti web accessibili e utilizzabili da persone con disabilità.

>[!NOTE]
>
>Consulta anche:
>
>* [Guida rapida a WCAG 2.0](/help/managing/qg-wcag.md)
>* [Configurazione dell&#39;editor Rich Text per la produzione di contenuto accessibile](/help/sites-administering/rte-accessible-content.md)
>

Queste linee guida sono classificate in base a tre livelli di conformità: livello A (il più basso), livello AA e livello AAA (il più alto). Brevemente, i livelli sono definiti come segue:

* **Livello A**: il sito ha raggiunto un livello minimo di accessibilità di base. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A.
* **Livello AA:** il livello di accessibilità ideale da porsi come obiettivo, in cui il sito raggiunge un livello di accessibilità avanzato, affinché sia accessibile al maggior numero di persone nella gran parte delle situazioni e con l&#39;utilizzo di più tecnologie possibili. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A e livello AA.
* **Livello AAA:** il sito ha raggiunto un livello molto alto di accessibilità. Per arrivare a questo livello sono stati soddisfatti tutti i criteri di successo di livello A, AA e AAA.

Quando si crea un sito, è necessario determinare il livello complessivo che si desidera ottenere.

Nella sezione seguente sono incluse le [linee guida WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) e i criteri di successo per i [livelli di conformità](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) A e AA.

>[!NOTE]
>
>Poiché non è possibile soddisfare tutti i criteri di successo AAA per alcuni tipi di contenuto, si sconsiglia di richiedere questo livello di conformità come criterio generale.

>[!NOTE]
>
>Questo documento utilizza quanto segue:
>
>* i nomi brevi per le [linee guida WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines).
>* la numerazione utilizzata nelle [linee guida WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) per facilitare i riferimenti incrociati al sito web WCAG.
>

## Principio 1: Percepibilità  {#principle-perceivable}

[Principio 1: Percepibile - Informazioni e componenti dell’interfaccia utente devono essere presentati agli utenti con modalità da loro percepibili.](https://www.w3.org/TR/WCAG20/#perceivable)

### Alternative testuali (1.1)  {#text-alternatives}

[Linea guida 1.1 - Alternative testuali: fornire alternative testuali per qualsiasi contenuto non testuale in modo che possa essere convertito in altri formati richiesti, come la stampa a caratteri grandi, il Braille, la sintesi vocale, i simboli o un linguaggio più semplice.](https://www.w3.org/TR/WCAG20/#text-equiv)

### Contenuto non testuale (1.1.1) {#non-text-content}

* Criterio di successo 1.1.1
* Livello A
* Contenuto non testuale: tutto il contenuto non testuale presentato all’utente dispone di un’alternativa testuale che svolge la finalità equivalente, fatta eccezione per le situazioni elencate di seguito.

#### Finalità - Contenuto non testuale (1.1.1) {#purpose-non-text-content}

Le informazioni su una pagina web possono essere fornite in diversi formati non testuali, ad esempio immagini, video, animazioni, grafici e grafici. Le persone non vedenti o con gravi disabilità visive non sono in grado di vedere contenuti non testuali, ma possono accedere a contenuti testuali facendoli leggere da un assistente vocale o presentati in forma tattile da un dispositivo di visualizzazione Braille. Pertanto, fornendo alternative testuali al contenuto in formato grafico, gli utenti che non possono vedere tale contenuto possono accedere a una versione equivalente delle informazioni fornite dal contenuto.

Un ulteriore vantaggio utile riguarda le alternative testuali, le quali consentono l’indicizzazione dei contenuti non testuali da parte della tecnologia dei motori di ricerca.

#### Come soddisfare il criterio - Contenuto non testuale (1.1.1) {#how-to-meet-non-text-content}

Per gli elementi grafici statici, il requisito fondamentale consiste nel fornire un’alternativa testuale equivalente. Questo metodo viene eseguito nel campo **Testo alternativo**:

>[!NOTE]
>
>Alcuni componenti pronti per l’uso, come **Carosello** e **Presentazione**, non consentono di aggiungere descrizioni di testo alternativo alle immagini. Quando implementi le versioni di questi componenti per l&#39;istanza AEM, il team di sviluppo dovrà configurarli per supportare l&#39;attributo `alt`. In questo modo gli autori potranno aggiungerlo al contenuto (vedi [Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

Il campo **Testo alternativo** è disponibile nella scheda **Avanzate** delle proprietà dell&#39;immagine della finestra di dialogo del componente **Immagine**:

![Finestra di dialogo per modifica del componente Immagine nell&#39;interfaccia classica; mostra il campo Testo alternativo.](assets/chlimage_1-17a.png)

Per impostazione predefinita, AEM aggiunge **Testo alternativo** alle immagini. Nell&#39;interfaccia classica sono disponibili due scenari diversi per la creazione dell&#39;attributo predefinito, anche se il valore predefinito potrebbe non essere sufficiente come alternativa e probabilmente dovrà essere modificato nella scheda **Avanzate** delle proprietà dell&#39;immagine:

* File:

  Un&#39;immagine viene caricata dal disco rigido dell&#39;utente. Se aggiungi un componente immagine a una pagina e scegli un&#39;immagine dal disco rigido o da un&#39;altra origine, il valore predefinito per **Testo alternativo** è `file`. Questo valore deve essere modificato nella scheda delle proprietà dell&#39;immagine **Avanzate**. Anche in questo caso, questo valore non viene visualizzato nel campo **Testo alternativo**, ma quando viene modificato, il nuovo valore viene visualizzato nel campo.

* Risorsa:

  Un’immagine viene aggiunta dall’archivio delle risorse digitali. Se trascini un&#39;immagine dal repository di risorse digitali a una pagina Web, i valori **Title** e **Alt Text** per tale immagine vengono ricavati dai metadati per tale immagine.

>[!NOTE]
>
>In entrambi gli scenari precedenti, il valore predefinito **Testo alternativo** non è visibile nella scheda **Proprietà immagine avanzate**. Per modificare il valore predefinito, immettere un nuovo valore nel campo **Testo alternativo**.

>[!NOTE]
>
>Se l&#39;immagine è puramente decorativa (vedere [Creazione di buone alternative di testo](#creating-good-text-alternatives)), è possibile immettere uno spazio nel campo **Testo alternativo** utilizzando la barra spaziatrice. In questo modo viene creato un attributo `alt` vuoto che richiede a un assistente vocale di ignorare l&#39;immagine.

#### Creazione di buone alternative testuali  {#creating-good-text-alternatives}

Esistono varie forme di contenuti non testuali, di conseguenza il valore del testo alternativo dipende dal ruolo dell’elemento grafico all’interno della pagina Web. Alcune regole generali includono:

* Le alternative testuali dovrebbero essere concise ma acquisire chiaramente le informazioni essenziali fornite dal contenuto non testuale.
* Le descrizioni lunghe (più di 100 caratteri) devono essere evitate. Se un testo alternativo richiede ulteriori dettagli:

   * fornisci una breve descrizione nel testo alternativo
   * e fornisci una descrizione testuale più lunga sulla stessa pagina o in una pagina web a parte. Collega questa descrizione separata creando un collegamento nell’immagine o inserendo un collegamento di testo accanto all’immagine.

* Il testo alternativo non deve replicare il contenuto vicino, fornito sotto forma di testo sulla stessa pagina. Tieni presente che molte immagini sono illustrazioni di punti già trattati nel testo di una pagina, pertanto potrebbe già esistere un testo alternativo dettagliato.
* Se il contenuto non testuale è un collegamento a un&#39;altra pagina o a un altro documento e non è presente altro testo che fa parte dello stesso collegamento, il testo alternativo per l&#39;immagine deve indicare la destinazione del collegamento. Non dovrà descrivere l’immagine.
* Se il contenuto non testuale è contenuto in un elemento pulsante e non è presente testo che fa parte dello stesso pulsante, il testo alternativo dell’immagine deve indicare la funzionalità del pulsante e non descrivere l’immagine.
* È accettabile che a un’immagine venga assegnato testo alternativo vuoto (null), ma solo se l’immagine non ha testo alternativo. Si tratta ad esempio di un elemento grafico puramente decorativo. Oppure, se il testo equivalente è già presente nel testo della pagina.

[Bozza W3C: tecniche HTML5 per fornire alternative testuali utili](https://html.spec.whatwg.org/multipage/images.html#alt) contiene ulteriori dettagli ed esempi di disposizioni testuali alternative appropriate per immagini di tipi diversi.

Tipi specifici di contenuto non testuale che richiedono alternative testuali potrebbero includere:

* Foto illustrative:

  Queste sono immagini di persone, oggetti o luoghi. Pensa al ruolo della foto nella pagina; un equivalente testuale appropriato sarà probabilmente *Foto di [oggetto]*, ma potrebbe dipendere dal testo circostante.

* Icone:

  Piccoli pittogrammi (grafici) che veicolano informazioni specifiche. Devono essere utilizzati in modo coerente all’interno di una pagina e di un sito. Tutte le istanze dell’icona in una pagina o in un sito devono avere lo stesso testo alternativo breve e sintetico, a meno che questo non determini una duplicazione inutile del testo adiacente.

* Grafici:

  In genere rappresentano dati numerici. Pertanto, un&#39;opzione per fornire un testo alternativo potrebbe essere quella di includere un breve riepilogo delle principali tendenze mostrate nel grafico o grafico. Se necessario, fornisci anche una descrizione più dettagliata nel testo utilizzando il campo **Description** nella scheda **Advanced** delle proprietà dell&#39;immagine. Inoltre, è possibile fornire i dati di origine in formato tabulare altrove nella pagina o nel sito.

  ![Esempio di grafico. Di seguito è riportato l&#39;approccio migliore per fornire un&#39;alternativa.](assets/chlimage_1-2a.jpeg)

  Per fornire un&#39;alternativa per questo grafico di esempio, aggiungere un testo `alt` conciso all&#39;immagine stessa, quindi seguire l&#39;immagine con un&#39;alternativa di testo completo.

  ```xml
  <p><img src="figure1.gif" alt="Figure 1" ></p>
  <p> Figure 1. Distribution of Articles by Journal Category.
  Pie chart: Language=68%, Education=14% and Science=18%.</p>
  ```

  >[!NOTE]
  >
  >Lo snippet di cui sopra viene utilizzato solo per illustrare l’ordine. Utilizza il componente **Immagine** anziché il riferimento a `img src` utilizzato in precedenza.

  In AEM è possibile utilizzare una combinazione dei campi **Testo alternativo** e **Descrizione** nella finestra di dialogo di configurazione dell&#39;immagine, come in [Come soddisfare il criterio - Contenuto non testuale (1.1.1)](#how-to-meet-non-text-content).

* Mappe, diagrammi, diagrammi di flusso:

  Per gli elementi grafici che forniscono dati spaziali (ad esempio. per descrivere le relazioni tra gli oggetti o un processo), assicurati che il messaggio chiave sia fornito in formato testo.  Per le mappe, potrebbe non risultare pratico fornire un equivalente di testo completo. Se la mappa ha lo scopo di aiutare le persone a individuare una posizione particolare, il testo alternativo dell’immagine della mappa può indicare brevemente *Mappa di X*, fornendo poi le indicazioni per tale posizione in un altro testo della pagina o attraverso il campo **Descrizione**, disponibile nella scheda **Avanzate** del componente **Immagine**.

* CAPTCHA:

  Un CAPTCHA è un *test di Turing pubblico completamente automatizzato per distinguere computer e persone*. Si tratta di un controllo di sicurezza utilizzato sulle pagine web per distinguere gli esseri umani da software dannosi, ma che può creare barriere di accessibilità. Si tratta di immagini che richiedono agli utenti di descrivere ciò che visualizzano, per poter superare un test di sicurezza. Non è possibile fornire un’alternativa testuale all’immagine, pertanto è necessario prendere in considerazione soluzioni alternative non grafiche.

  Il W3C fornisce diversi suggerimenti, ad esempio i seguenti. Ognuno di questi approcci presenta pro e contro.

   * Rompicapi logici
   * L&#39;uso dell&#39;output sonoro invece delle immagini
   * Account a utilizzo limitato e filtri anti-spam.

* Immagini di sfondo:

  Queste immagini vengono ottenute utilizzando Cascading Style Sheets (CSS) anziché in HTML. Non è possibile specificare un valore di testo alternativo. Pertanto, le immagini di sfondo non devono fornire informazioni testuali importanti; in tal caso, tali informazioni devono essere incluse anche nel testo della pagina.

  Tuttavia, è importante che, quando l’immagine non può essere visualizzata, venga visualizzato uno sfondo alternativo.

  >[!NOTE]
  >
  >Dovrebbe essere previsto un livello adeguato di contrasto tra lo sfondo e il testo in primo piano. Questo contrasto viene discusso più dettagliatamente in [Contrasto (minimo) (1.4.3)](#contrast-minimum).

#### Ulteriori informazioni - Contenuto non testuale (1.1.1) {#more-information-non-text-content}

* [Comprendere i criteri di successo 1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [Come soddisfare i criteri di successo 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#text-alternatives)
* [W3C: tecniche HTML5 per fornire alternative testuali utili](https://html.spec.whatwg.org/multipage/images.html#alt)
* [Spiegazione W3C dei CAPTCHA e relative alternative](https://www.w3.org/TR/turingtest/)

### Media temporizzati (1.2) {#time-based-media}

[Linea guida 1.2 - Media temporizzati: fornire alternative per gli elementi multimediali temporizzati.](https://www.w3.org/TR/WCAG20/#text-equiv)

Queste informazioni sono relative al contenuto Web *basato sul tempo*. In questa sezione sono inclusi i contenuti che l&#39;utente può riprodurre (come video, audio e contenuti animati) e che possono essere preregistrati o in streaming.

### Solo audio e solo video (preregistrato) (1.2.1)  {#audio-only-and-video-only-pre-recorded}

* Criterio di successo 1.2.1
* Livello A
* Solo audio e solo video (preregistrati): per gli elementi solo video e solo audio preregistrati vale quanto segue, tranne quando l’audio o il video sia un elemento alternativo per il testo, chiaramente indicato come tale:

   * Solo audio preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati che presenta informazioni equivalenti per contenuti solo audio preregistrati.
   * Solo video preregistrato: viene fornita un’alternativa per gli elementi multimediali temporizzati o una traccia audio che presenta informazioni equivalenti per i contenuti solo video preregistrati.

#### Finalità - Solo audio e solo video (preregistrato) (1.2.1)  {#purpose-audio-only-and-video-only-pre-recorded}

Problemi di accessibilità per audio e video possono essere riscontrati da:

* persone con disabilità visive in caso di assenza di audio o quando non sufficiente per essere informati su ciò che sta accadendo nel video o nell’animazione;
* persone con disabilità uditive o non udenti, che non sono in grado di sentire l’audio;
* persone che possono sentire l’audio, ma non capiscono cosa si sta dicendo (per esempio, perché non conoscono la lingua utilizzata).

Video o audio potrebbero non essere disponibili per le persone che utilizzano browser o dispositivi che non supportano la riproduzione di contenuto in formati multimediali specifici, come Adobe Flash.

Fornire queste informazioni in un formato diverso, ad esempio testo (o audio per video senza audio) può renderle accessibili alle persone che non possono accedere al contenuto originale.

#### Come soddisfare il criterio - Solo audio e solo video (preregistrato) (1.2.1)  {#how-to-meet-audio-only-and-video-only-pre-recorded}

* Se il contenuto è una traccia audio preregistrata senza video (come un podcast):

   * Fornisci un collegamento immediatamente prima o dopo il contenuto a una trascrizione testuale del contenuto audio.

     La trascrizione deve essere una pagina HTML con un equivalente testuale di tutti i contenuti parlati e importanti non parlati. Dovrebbe anche indicare chi sta parlando, una descrizione dell&#39;ambientazione, espressioni vocali e una descrizione di qualsiasi altro audio significativo.

* Se il contenuto è un’animazione o un video preregistrato senza audio:

   * Fornisci un collegamento ad una descrizione testuale equivalente alle informazioni fornite dal video ed immediatamente prima o dopo il contenuto
   * oppure una descrizione audio equivalente in un formato audio comunemente utilizzato come MP3.

>[!NOTE]
>
>Se il contenuto audio o video viene fornito come alternativa a contenuto esistente in un altro formato su una pagina web, non è necessario seguire i requisiti di cui sopra. Ad esempio, se un video illustra un elenco di istruzioni di testo, questo video non richiede un’alternativa in quanto le istruzioni di testo già agiscono come un’alternativa al video.

Inserire contenuti multimediali, in particolare contenuti di Flash, nelle pagine Web AEM è simile a inserire un’immagine. Tuttavia, poiché i contenuti multimediali sono molto più di un fermo immagine, esistono varie impostazioni e opzioni diverse per controllare la riproduzione dei contenuti multimediali.

>[!NOTE]
>
>Quando utilizzi elementi multimediali con contenuti informativi, è necessario creare anche collegamenti a contenuti alternativi. Ad esempio, per includere una trascrizione testuale, crea una pagina HTML per visualizzare la trascrizione e quindi aggiungi un collegamento accanto o sotto al contenuto audio.

#### Ulteriori informazioni - Solo audio e solo video (preregistrato) (1.2.1) {#more-information-audio-only-and-video-only-pre-recorded}

* [Comprendere i criteri di successo 1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [Come soddisfare i criteri di successo 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#time-based-media)

### Sottotitoli (preregistrati) (1.2.2)  {#captions-pre-recorded}

* Criterio di successo 1.2.2
* Livello A
* Sottotitoli (preregistrati): i sottotitoli vengono forniti per tutti i contenuti audio preregistrati negli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo e chiaramente indicato come tale.

#### Finalità - Sottotitoli (preregistrati) (1.2.2)  {#purpose-captions-pre-recorded}

Le persone non udenti o ipoudenti non sono in grado di accedere ai contenuti audio o hanno grandi difficoltà di accesso. I sottotitoli sono equivalenti testuali di elementi audio verbali e non, visualizzati sullo schermo al momento opportuno durante il video. Permettono alle persone che non possono ascoltare l’audio di capire cosa sta succedendo.

>[!NOTE]
>
>I sottotitoli non sono necessari se sulla stessa pagina del video o dell&#39;animazione sono disponibili testo appropriato o contenuti equivalenti non testuali (che forniscono informazioni direttamente equivalenti).

#### Come soddisfare il criterio - Sottotitoli (preregistrati) (1.2.2)  {#how-to-meet-captions-pre-recorded}

I sottotitoli possono essere:

* Sottotitoli non codificati: sempre visibili durante la riproduzione del video
* Sottotitoli codificati: possono essere attivati o disattivati dall’utente

Se possibile, utilizza i sottotitoli codificati. Consente agli utenti di scegliere se visualizzare o meno i sottotitoli.

Per i sottotitoli codificati, crea e fornisci un file di sottotitoli sincronizzati in un formato appropriato, ad esempio [SMIL](https://www.w3.org/AudioVideo/), insieme al file video.

Consulta i tutorial in [Ulteriori informazioni - Sottotitoli (preregistrati) (1.2.2)](#more-information-captions-pre-recorded). Assicurati di includere una nota per informare gli utenti che per il video sono disponibili i sottotitoli.

Se è necessario utilizzare sottotitoli aperti, incorporare il testo nella traccia video. Questo metodo viene ottenuto utilizzando applicazioni di editing video che consentono la sovrapposizione dei titoli sul video.

#### Ulteriori informazioni - Sottotitoli (preregistrati) (1.2.2)  {#more-information-captions-pre-recorded}

* [Comprendere i criteri di successo 1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html):
* [Come soddisfare i criteri di successo 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#time-based-media)
* [W3C: File multimediali sincronizzati](https://www.w3.org/AudioVideo/)
* [Sottotitoli, trascrizioni e descrizioni audio, di WebAIM](https://webaim.org/techniques/captions/)

### Descrizione audio o elemento multimediale alternativo (preregistrato) (1.2.3)  {#audio-description-or-media-alternative-pre-recorded}

* Criterio di successo 1.2.3
* Livello A
* Audiodescrizione o tipo di media alternativo (preregistrato): viene fornita un’alternativa per gli elementi multimediali temporizzati o una descrizione audio del contenuto video preregistrato per gli elementi multimediali sincronizzati, fatta eccezione per il caso in cui l’elemento multimediale sia alternativo al testo, e chiaramente indicato come tale.

#### Finalità - Descrizione audio o file multimediale alternativo (preregistrato) (1.2.3)  {#purpose-audio-description-or-media-alternative-pre-recorded}

Se le informazioni in un video o in un’animazione vengono fornite solo visivamente, le persone non vedenti o ipovedenti riscontrano ostacoli di accessibilità. Oppure, se l&#39;audio non fornisce informazioni sufficienti per consentire la comprensione di ciò che sta accadendo visivamente.

#### Come soddisfare il criterio - Descrizione audio o elemento multimediale alternativo (preregistrato) (1.2.3)  {#how-to-meet-audio-description-or-media-alternative-pre-recorded}

Per soddisfare questo criterio di successo è possibile adottare due approcci. Entrambi sono accettabili:

1. Includere una descrizione audio aggiuntiva per i contenuti video. Puoi eseguire questa operazione in uno dei tre modi seguenti:

   * Durante le pause nella finestra di dialogo esistente, fornisci informazioni sulle modifiche della scena che non vengono presentate come parte della traccia audio esistente;
   * Fornisci una nuova traccia audio, aggiuntiva e facoltativa, contenente l’audio originale, ma anche informazioni audio ulteriori sui cambiamenti nella scena.

      * Gli utenti possono passare dalla traccia audio esistente (che *non* contiene una descrizione audio) alla nuova traccia audio (che *contiene* una descrizione audio) e viceversa.
      * Questo metodo impedisce l’interruzione delle attività agli utenti che non necessitano della descrizione aggiuntiva.

   * Creare una seconda versione dei contenuti video per consentire descrizioni audio estese. In questo modo si riducono le difficoltà associate alla fornitura di descrizioni audio dettagliate negli spazi tra le finestre di dialogo esistenti, mettendo temporaneamente in pausa l’audio e il video nei punti appropriati. Di conseguenza, è possibile fornire una descrizione audio molto più lunga prima che l’azione ricominci. Come nell’esempio precedente, questa funzione è fornita come traccia audio aggiuntiva opzionale, per evitare interruzioni agli utenti che non necessitano della descrizione aggiuntiva.

1. Fornisci una trascrizione testuale che rappresenti un equivalente testuale adatto per gli elementi sonori e visivi del video o dell’animazione. Dovrebbe includere, se del caso, un&#39;indicazione di chi sta parlando, una descrizione dell&#39;ambientazione, espressioni vocali. A seconda della lunghezza, è possibile inserire la trascrizione nella stessa pagina del video o dell’animazione oppure in una pagina separata. Se scegli la seconda opzione, includi un collegamento alla trascrizione accanto al video o all’animazione.

I dettagli precisi sulle modalità di creazione di video con descrizione audio vanno oltre lo scopo di questa guida. La creazione di video e descrizioni audio può richiedere parecchio tempo, ma puoi ricorrere ad altri prodotti Adobe per facilitare l’esecuzione di tali attività. Se crei contenuto in Adobe Flash Professional, devi anche creare uno script per richiedere all’utente di scaricare il plug-in appropriato e fornire un testo alternativo attraverso l’elemento `<noscript>`.

#### Ulteriori informazioni - Descrizione audio o elemento multimediale alternativo (preregistrato) (1.2.3) {#more-information-audio-description-or-media-alternative-pre-recorded}

* [Comprendere i criteri di successo 1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html):
* [Come soddisfare i criteri di successo 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://helpx.adobe.com/it/premiere-pro/using/whats-new.html)

### Sottotitoli (dal vivo) (1.2.4)    {#captions-live}

* Criterio di successo 1.2.4
* Livello AA
* Sottotitoli (in tempo reale): i sottotitoli vengono forniti per tutti i contenuti audio dal vivo negli elementi multimediali sincronizzati.

#### Finalità - Sottotitoli (in tempo reale) (1.2.4)  {#purpose-captions-live}

Questo criterio di successo è identico a [Sottotitoli (preregistrati)](#captions-pre-recorded), in quanto riguarda la rimozione degli ostacoli di accessibilità per persone non udenti o ipoudenti, tranne per il fatto che questo criterio di successo è relativo a presentazioni in tempo reale, come i webcast.

#### Come soddisfare il criterio - Sottotitoli (in tempo reale) (1.2.4) {#how-to-meet-captions-live}

Segui le indicazioni fornite per [Sottotitoli (preregistrati)](#captions-pre-recorded) qui sopra. Tuttavia, data la natura live dei media, i sottotitoli dovranno essere creati il più rapidamente possibile e in risposta a ciò che sta accadendo. Pertanto, è consigliabile utilizzare strumenti per la creazione di sottotitoli in tempo reale o di sintesi vocale.

Istruzioni dettagliate al riguardo vanno oltre l&#39;ambito di questo documento, ma informazioni utili sono reperibili tramite le risorse seguenti:

* [WebAIM: aggiunta di sottotitoli in tempo reale](https://webaim.org/techniques/captions/realtime)
* [AccessIT (University of Washington): i sottotitoli possono essere generati automaticamente utilizzando il riconoscimento vocale?](https://www.washington.edu/doit/programs/accessit?1209)

#### Ulteriori informazioni - Sottotitoli (dal vivo) (1.2.4)  {#more-information-captions-live}

* [Comprendere i criteri di successo 1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [Come soddisfare i criteri di successo 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-real-time-captions)

### Descrizione audio (preregistrato) (1.2.5)    {#audio-description-pre-recorded}

* Criterio di successo 1.2.5
* Livello AA
* Descrizione audio (preregistrato): la descrizione audio viene fornita per tutti i contenuti video preregistrati negli elementi multimediali sincronizzati.

#### Finalità - Descrizione audio (preregistrato) (1.2.5)  {#purpose-audio-description-pre-recorded}

Questo criterio di successo è identico a [Descrizione audio o elemento multimediale alternativo (preregistrato)](#audio-description-or-media-alternative-pre-recorded), tranne per il fatto che gli autori devono fornire una descrizione audio molto più dettagliata per adeguarsi al livello AA.

#### Come soddisfare il criterio - Descrizione audio (preregistrato) (1.2.5)  {#how-to-meet-audio-description-pre-recorded}

Segui le indicazioni fornite per [Descrizione audio o elemento multimediale alternativo (preregistrato)](#audio-description-or-media-alternative-pre-recorded).

#### Ulteriori informazioni - Descrizione audio (preregistrato) (1.2.5)  {#more-information-audio-description-pre-recorded}

* [Comprendere i criteri di successo 1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [Come soddisfare i criteri di successo 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-audio-desc-only)

### Adattabile (1.3)  {#adaptable}

[Linea guida 1.3 - Adattabile: creare contenuti che possano essere rappresentati in modi diversi (ad esempio con un layout più semplice), senza perdere informazioni o struttura.](https://www.w3.org/TR/WCAG20/#content-structure-separation)

Questa linea guida copre i requisiti necessari per supportare le persone che:

* potrebbe non essere in grado di accedere alle informazioni come presentate da un autore in un layout *standard* di pagina Web bidimensionale, a più colonne e colorato

* potrebbero utilizzare una visualizzazione solo audio o una alternativa, ad esempio testo di grandi dimensioni e a contrasto elevato.

### Informazioni e correlazioni (1.3.1)    {#info-and-relationships}

* Criterio di successo 1.3.1
* Livello A
* Informazioni e correlazioni: le informazioni, la struttura e le correlazioni veicolate attraverso la presentazione possono essere determinate a livello di programmazione o sono disponibili nel testo.

#### Finalità - Informazioni e correlazioni (1.3.1)  {#purpose-info-and-relationships}

Molte tecnologie per l’accessibilità utilizzate da persone con disabilità si basano su informazioni strutturali per visualizzare o generare in modo efficace i contenuti. Queste informazioni strutturali possono assumere la forma di intestazioni di pagina, intestazioni di riga e colonna di una tabella e tipi di elenco. Ad esempio, un’utilità di lettura dello schermo potrebbe consentire a un utente di spostarsi all’interno di una pagina passando da un’intestazione a un’altra. Tuttavia, quando la struttura del contenuto della pagina dipende esclusivamente da uno stile visivo, anziché dal codice HTML sottostante, non sono presenti informazioni strutturali utilizzabili dalle tecnologie per l’accessibilità, il che ne limita la capacità di supportare la navigazione facilitata.

Questo criterio di successo esiste per garantire che tali informazioni strutturali siano fornite tramite HTML, in modo che i browser e le tecnologie per l’accessibilità possano accedervi e sfruttarle.

#### Come soddisfare il criterio - Informazioni e correlazioni (1.3.1)  {#how-to-meet-info-and-relationships}

L’AEM semplifica la creazione di pagine web utilizzando gli elementi HTML appropriati. Apri il contenuto della pagina nell&#39;editor Rich Text (un componente testo) e utilizza il menu **Formato** per specificare l&#39;elemento strutturale appropriato (ad esempio paragrafo e intestazione).

Nell&#39;immagine seguente viene illustrato il testo a cui è stato applicato lo stile di testo paragrafo. Nella vista del codice sorgente in uso vengono visualizzati i tag di apertura e chiusura &lt;p> e &lt;/p> corretti.

![Esempio dell&#39;elemento Paragraph visualizzato nella modalità di modifica dell&#39;origine (interfaccia classica).](assets/chlimage_1-18a.png)

Assicurati che alle pagine web sia associata la struttura appropriata:

* **Utilizzando i titoli:**  

  Se le funzioni di accessibilità dell&#39;editor Rich Text sono abilitate (vedere [AEM e accessibilità](/help/sites-administering/rte-accessible-content.md)), l&#39;AEM offre tre livelli di intestazione di pagina. Puoi utilizzarli per identificare sezioni e sottosezioni di contenuto. Titolo 1 rappresenta il livello di intestazione più alto, Titolo 3 quello più basso. L’amministratore di sistema può configurare il sistema per consentire l’utilizzo di più livelli di intestazione.

  Nell&#39;immagine seguente viene illustrato un esempio dei diversi tipi di intestazione.

  ![Titoli da H1 a H3 visualizzati nel selettore a discesa (interfaccia classica).](assets/chlimage_1-19a.png)

* **Testo evidenziato**:

  Utilizza l’elemento &lt;strong> o &lt;em> per indicare l’enfasi. Non utilizzare le intestazioni per evidenziare il testo all’interno dei paragrafi.

   * Evidenzia il testo che desideri mettere in evidenza.
   * Fai clic sull&#39;icona **B** (per &lt;strong>) o sull&#39;icona **I** (per &lt;em>) visualizzata nel pannello **Proprietà** (accertati che HTML sia selezionato).

  >[!NOTE]
  >
  >L’editor Rich Text in un’installazione standard di AEM è configurato per utilizzare:
  >
  >* &lt;b> per &lt;strong>
  >* &lt;i> per &lt;em>
  >
  >L’efficacia è la stessa, ma &lt;strong> e &lt;em> sono preferibili in quanto rappresentano un html corretto dal punto di vista semantico. Il team di sviluppo può configurare l’editor Rich Text in modo che utilizzi &lt;strong> e &lt;em> (anziché &lt;b> e &lt;i>) durante lo sviluppo dell’istanza di progetto.

* **Utilizzare gli elenchi**: è possibile utilizzare l’HTML per specificare tre diversi tipi di elenchi:

   * L&#39;elemento `<ul>` viene utilizzato per *elenchi non ordinati* (puntati). Le singole voci dell&#39;elenco sono identificate dall&#39;elemento `<li>`.

     nell&#39;editor Rich Text, utilizzare l&#39;icona **Elenco puntato**.

   * L’elemento `<ol>`viene utilizzato per gli elenchi *numerati*. Le singole voci dell&#39;elenco sono identificate dall&#39;elemento `<li>`.

     Nell’editor Rich Text, utilizza l’icona **Elenco numerato**.

  Per modificare il contenuto esistente in un tipo di elenco specifico, evidenzia il testo appropriato e seleziona il tipo di elenco pertinente. Come nell&#39;esempio precedente che mostra come viene immesso il testo di paragrafo, gli elementi di elenco appropriati vengono aggiunti automaticamente al HTML, ma è possibile visualizzarli nella visualizzazione di modifica dell&#39;origine.

  >[!NOTE]
  >
  >Elemento `<dl>` non supportato dall&#39;editor Rich Text.

* **Usa tabelle**:

  Le tabelle di dati devono essere identificate utilizzando gli elementi di tabella HTML:

   * un elemento `<table>`
   * un elemento `<tr>` per ogni riga della tabella
   * un elemento `<th>` per ogni intestazione di riga e colonna
   * un elemento `<td>` per ogni cella di dati

  >[!NOTE]
  >
  >Le tabelle devono essere realizzate con il componente **Tabella**. È possibile creare tabelle nel componente Testo, ma questa operazione non è consigliata.

  Inoltre, le tabelle accessibili utilizzano gli elementi e gli attributi seguenti:

   * L’elemento `<caption>` viene utilizzato per fornire una didascalia visibile per la tabella. Per impostazione predefinita, le didascalie vengono visualizzate centrate sopra la tabella, ma possono essere posizionate in modo appropriato utilizzando gli stili CSS. La didascalia è associata alla tabella a livello di programmazione, pertanto è un metodo utile per fornire un’introduzione al contenuto.
   * L’elemento `<h3 class="summary">` aiuta gli utenti non vedenti a comprendere più facilmente le informazioni presentate all’interno di una tabella, fornendo una sintesi di ciò che un utente vedente può vedere. Risulta particolarmente utile quando si utilizzano layout di tabella complessi o non convenzionali (l’attributo non viene visualizzato nel browser, ma viene letto solo alle tecnologie per l’accessibilità).
   * L’attributo `scope` dell’elemento `<th>` viene utilizzato per indicare se una cella rappresenta un’intestazione per una particolare riga o colonna. Un approccio simile consiste nell’utilizzare gli attributi header e id in tabelle complesse, dove le celle di dati possono essere associate a una o più intestazioni.

  >[!NOTE]
  >
  >Per impostazione predefinita questi elementi e attributi non sono direttamente disponibili, anche se l’amministratore di sistema può aggiungere supporto per questi valori nella finestra di dialogo **Proprietà tabella** (consulta [Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

  Quando si aggiunge una **Tabella**, è possibile configurare **Proprietà tabella** utilizzando la finestra di dialogo.

   * **Didascalia** appropriata.
   * È consigliabile rimuovere eventuali valori predefiniti per **Larghezza**, **Altezza**, **Bordo**, **Margine celle**, **Spaziatura celle**. dato che queste proprietà possono essere impostate in un foglio di stile globale.

  ![Finestra di dialogo delle proprietà della tabella.](assets/chlimage_1-20a.png)

  È quindi possibile utilizzare le **proprietà cella** per scegliere se la cella è una cella di dati o di intestazione e, se si tratta di una cella di intestazione, se si riferisce a una riga o a una colonna o a entrambe:

  ![Finestra di dialogo delle proprietà di chiamata; impostazione di una riga (in genere la prima) come riga di intestazione.](assets/chlimage_1-21a.png)

* **Tabelle dati complesse:**

  Talvolta, in presenza di tabelle complesse con due o più livelli di intestazioni, le proprietà della tabella di base potrebbero non essere sufficienti a fornire tutte le informazioni strutturali necessarie. Per questo tipo di tabelle complesse, è necessario creare relazioni dirette tra le intestazioni e le celle correlate utilizzando gli attributi **header** e **id**. Ad esempio, nella tabella seguente le intestazioni e gli ID vengono abbinati per creare un’associazione programmatica per gli utenti di tecnologie per l’accessibilità.

  >[!NOTE]
  >
  >L’attributo id non è disponibile in un’installazione standard. Può essere attivato configurando regole HTML e il serializzatore nell’editor Rich Text.

  >[!NOTE]
  >
  >Le tabelle devono essere realizzate con il componente **Tabella**. È possibile creare tabelle nel componente Testo, ma questa operazione non è consigliata.

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

  Per ottenere questo risultato in AEM, devi aggiungere il markup direttamente utilizzando la modalità di modifica sorgente.

  >[!NOTE]
  >
  >Questa funzionalità non è immediatamente disponibile in un’installazione standard. Richiede la configurazione dell’editor Rich Text, delle regole HTML e del serializzatore.

#### Ulteriori informazioni - Informazioni e correlazioni (1.3.1)  {#more-information-info-and-relationships}

* [Comprendere i criteri di successo 1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [Come soddisfare i criteri di successo 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-programmatic)

### Caratteristiche sensoriali (1.3.3)    {#sensory-characteristics}

* Criterio di successo 1.3.3
* Livello A
* Caratteristiche sensoriali: le istruzioni fornite per comprendere e intervenire sui contenuti non si basano unicamente su caratteristiche sensoriali dei componenti quali forma, dimensione, ubicazione visiva, orientamento o audio.

#### Finalità - Caratteristiche sensoriali (1.3.3)  {#purpose-sensory-characteristics}

Nel presentare le informazioni, i designer spesso si concentrano sulle caratteristiche di progettazione visiva come il colore, la forma, lo stile del testo o la posizione assoluta o relativa di un elemento di contenuto. Queste possono essere tecniche di progettazione potenti per la trasmissione delle informazioni, ma le persone non vedenti o ipovedenti potrebbero non essere in grado di accedere alle informazioni che richiedono l’identificazione visiva di attributi come la posizione, il colore o la forma.

Allo stesso modo, le informazioni che richiedono di distinguere tra suoni diversi (ad esempio, contenuti parlati da voci di sesso maschile o femminile) presentano ostacoli di accessibilità per le persone con disabilità uditive, se non vengono riportate in alcun testo alternativo per il contenuto audio.

>[!NOTE]
>
>Per requisiti relativi alle alternative di colore, consulta [Utilizzo del colore](#use-of-color).

#### Come soddisfare il criterio: caratteristiche sensoriali (1.3.3)  {#how-to-meet-sensory-characteristics}

Assicurati che anche tutte le informazioni che si basano sulle caratteristiche visive del contenuto della pagina siano presentate in un formato alternativo.

* Non fare affidamento alla posizione visiva per dare informazioni. Ad esempio, se desideri indirizzare gli utenti a un menu sul lato destro della pagina per accedere a ulteriori informazioni, non fare riferimento a *il menu sul lato destro*; invece, denomina il menu (ad esempio, tramite un&#39;intestazione) e fai riferimento a tale nome nel testo.
* Non fare affidamento sullo stile del testo (ad esempio, testo in grassetto o in corsivo) come unico modo per trasmettere le informazioni.

>[!NOTE]
>
>L’uso di termini descrittivi è accettabile se si ritiene che abbiano un significato in un contesto non visivo. Ad esempio, l&#39;utilizzo di *sopra* e *sotto* sarebbe generalmente accettabile, in quanto implicano rispettivamente contenuti prima e dopo un particolare elemento di contenuto. Avrebbe comunque senso quando il contenuto viene parlato ad alta voce.

#### Ulteriori informazioni - Caratteristiche sensoriali (1.3.3) {#more-information-sensory-characteristics}

* [Comprendere i criteri di successo 1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [Come soddisfare i criteri di successo 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-understanding)

### Distinguibile (1.4)  {#distinguishable}

[Linea guida 1.4 - Distinguibile: facilitare agli utenti la visione e l’ascolto dei contenuti, separando gli elementi in primo piano dallo sfondo.](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### Uso del colore (1.4.1)    {#use-of-color}

* Criterio di successo 1.4.1
* Livello A
* Uso del colore: il colore non è utilizzato come unica modalità visiva per rappresentare le informazioni, indicare un’azione, richiedere una risposta o distinguere un elemento visivo.

>[!NOTE]
>
>Questo criterio di successo riguarda in particolare la percezione del colore. Altre forme di percezione sono trattate in [Adattabilità (1.3)](#adaptable), incluso l’accesso programmatico al colore e ad altre codifiche di presentazione visiva.

#### Finalità - Uso del colore (1.4.1)  {#purpose-use-of-color}

Il colore è un modo efficace per migliorare l’aspetto estetico delle pagine web ed è utile anche per trasmettere informazioni. Tuttavia esistono diverse disabilità visive, dalla cecità al daltonismo, che impediscono ad alcune persone di distinguere determinati colori. Questo problema rende la codifica a colori un modo inaffidabile di fornire informazioni.

Ad esempio, una persona con deficit di visione dei colori rosso-verde non è in grado di distinguere tra le tonalità di verde e quelle di rosso. Può vedere entrambi i colori come un terzo colore (ad esempio, il marrone), ma non è in grado di distinguere tra rosso, verde e marrone.

Inoltre, il colore non può essere percepito da persone che utilizzano browser di solo testo, dispositivi di visualizzazione in bianco e nero o una stampa in bianco e nero della pagina.

#### Come soddisfare il criterio - Uso del colore (1.4.1)  {#how-to-meet-use-of-color}

Qualunque colore sia utilizzato per trasmettere le informazioni, accertati che queste siano disponibili senza che sia necessario vedere il colore stesso.

Ad esempio, assicurati che le informazioni fornite dal colore siano presenti esplicitamente anche nel testo. L’illustrazione seguente mostra come il colore e il testo indicano entrambi la disponibilità di posti a sedere per una prestazione:

<table>
 <tbody>
  <tr>
   <td><p><strong>Prestazioni</strong></p> </td>
   <td><p><strong>Disponibilità</strong></p> </td>
  </tr>
  <tr>
   <td><p>martedì 16 marzo</p> </td>
   <td><p>POSTI DISPONIBILI</p> </td>
  </tr>
  <tr>
   <td><p>Mercoledì 17 marzo</p> </td>
   <td><p>POSTI DISPONIBILI</p> </td>
  </tr>
  <tr>
   <td><p>Giovedì 18 marzo</p> </td>
   <td><p>TUTTO ESAURITO</p> </td>
  </tr>
 </tbody>
</table>

Se il colore viene utilizzato come spunto per fornire informazioni, è necessario fornire un ulteriore segnale visivo, come la modifica dello stile (ad esempio grassetto o corsivo) o del font. Questo aiuta le persone con problemi di vista o daltonismo a identificare le informazioni. Tuttavia, non ci si può basare interamente su di esso, in quanto non aiuta le persone che non possono vedere affatto la pagina.

#### Ulteriori informazioni - Uso del colore (1.4.1) {#more-information-use-of-color}

* [Comprendere i criteri di successo 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Come soddisfare i criteri di successo 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Indicazioni per ottenere un rapporto di contrasto 3:1, contenente un elenco di colori &quot;web safe&quot;](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### Contrasto (minimo) (1.4.3)  {#contrast-minimum}

* Criterio di successo 1.4.3
* Livello AA
* Contrasto (minimo): la presentazione visiva di testo e immagini di testo ha un rapporto di contrasto di almeno 4,5:1, fatta eccezione per quanto segue:

   * Testo di grandi dimensioni: testo di grandi dimensioni e immagini di testo di grandi dimensioni hanno un rapporto di contrasto di almeno 3:1.
   * Incidentale: per il testo o per le immagini di testo che fanno parte di un componente dell’interfaccia inattivo e che sono puramente decorative o non visibili o che fanno parte di un’immagine che contiene altri contenuti visivi significativi, non è previsto alcun requisito di contrasto.
   * Logotipi: per il testo che fa parte di un logo o di un marchio non è previsto alcun requisito minimo di contrasto.

#### Finalità - Contrasto (minimo) (1.4.3)  {#purpose-contrast-minimum}

Le persone con determinate disabilità visive possono non essere in grado di distinguere tra alcune coppie di colori a basso contrasto. Queste persone possono riscontrare problemi di accessibilità se:

* Il testo contrasta poco con il relativo colore di sfondo.
* La codifica a colori del testo (ad esempio, per differenziare il testo normale dal testo dei collegamenti) è importante per distinguere i diversi tipi di informazioni.

>[!NOTE]
>
>Il testo utilizzato esclusivamente a scopo decorativo è escluso da questo criterio di successo.

#### Come soddisfare il criterio - Contrasto (minimo) (1.4.3)  {#how-to-meet-contrast-minimum}

Assicurati che il testo contrasti a sufficienza con il relativo sfondo. I rapporti di contrasto dipendono dalle dimensioni e dallo stile del testo:

* Per testi con dimensioni inferiori a 18 punti (o 14 se in grassetto), il rapporto di contrasto tra testo/immagini di testo e sfondo deve essere pari ad almeno 4,5:1.
* Per il testo con dimensioni almeno pari a 18 punti (o 14 se in grassetto), il rapporto di contrasto deve essere pari ad almeno 3:1.
* Se lo sfondo include una texture, lo sfondo intorno al testo dovrà essere ombreggiato in modo da mantenere il rapporto di 4,5:1 o 3:1.

Per controllare i rapporti di contrasto, utilizza uno strumento di contrasto del colore, ad esempio [Color Contrast Analyzer di The Paciello Group](https://www.paciellogroup.com/resources/contrast-analyser.html) o [Color Contrast Checker di WebAIM](https://webaim.org/resources/contrastchecker/). Questi strumenti consentono di controllare coppie di colori e segnalare eventuali problemi di contrasto.

In alternativa, se non desiderI specificare l’aspetto della pagina, puoi scegliere di non definire i colori del testo di sfondo e in primo piano. Non è richiesto alcun controllo del contrasto, in quanto il browser dell’utente determina i colori del testo e dello sfondo.

Se non è possibile soddisfare i livelli di contrasto consigliati, fornisci un collegamento a una versione alternativa equivalente della pagina (che non presenta problemi di contrasto dei colori). In alternativa, l’utente può regolare il contrasto della combinazione di colori della pagina in base alle proprie esigenze.

#### Ulteriori informazioni - Contrasto (minimo) (1.4.3)  {#more-information-contrast-minimum}

* [Comprendere i criteri di successo 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [Come soddisfare i criteri di successo 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-visual-audio-contrast-contrast)

### Immagini di testo (1.4.5)  {#images-of-text}

* Criterio di successo 1.4.5
* Livello AA
* Immagini di testo: se le tecnologie utilizzate consentono la presentazione visiva, per trasmettere informazioni viene utilizzato il testo, anziché le immagini di testo, con le seguenti eccezioni:

   * Personalizzabile: l&#39;immagine del testo può essere personalizzata visivamente in base alle esigenze dell&#39;utente;
   * Essenziale: una presentazione del testo specifica è essenziale per le informazioni trasmesse.

>[!NOTE]
>
>I logotipi (testo che fa parte di un logo o di un marchio) sono considerati essenziali.

#### Finalità - Immagini di testo (1.4.5)  {#purpose-images-of-text}

Le immagini di testo vengono spesso utilizzate quando si preferisce un particolare stile di testo; ad esempio un logotipo, o se il testo è stato generato da un’altra origine, ad esempio la scansione di un documento cartaceo. Tuttavia, rispetto al testo presentato in HTML e formattato tramite CSS, le immagini di testo non hanno la flessibilità di modificare le dimensioni o l’aspetto che potrebbe essere necessario per le persone con disabilità visive o difficoltà di lettura.

#### Come soddisfare il criterio - Immagini di testo (1.4.5) {#how-to-meet-images-of-text}

Se è necessario utilizzare le immagini di testo, utilizza CSS per sostituirle con testo equivalente in HTML, in modo che sia possibile personalizzare il testo. Per un esempio, vedere [C30: utilizzo di CSS per sostituire il testo con immagini di testo e fornitura di controlli dell&#39;interfaccia utente per passare a un altro elemento](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Ulteriori informazioni - Immagini di testo (1.4.5) {#more-information-images-of-text}

* [Comprendere i criteri di successo 1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [Come soddisfare i criteri di successo 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-visual-audio-contrast-text-presentation)

## Principio 2: Utilizzabile  {#principle-operable}

[Principio 2: Utilizzabile - I componenti dell’interfaccia e la navigazione devono essere operabili.](https://www.w3.org/TR/WCAG20/#operable)

### Sospendi, Arresta, Nascondi (2.2.2)    {#pause-stop-hide}

* Criterio di successo 2.2.2
* Livello A
* Pausa, stop, nascondi: per le informazioni in movimento, lampeggianti, scorrevoli o con aggiornamento automatico, vale quanto segue:

   * Spostamento, lampeggiamento, scorrimento: per qualsiasi informazione in movimento, lampeggiante o scorrevole che
      * a) si avvia automaticamente;
      * b) dura più di cinque secondi; e
      * c) è presentato parallelamente ad altri contenuti;
esiste un meccanismo che consente all’utente di metterlo in pausa, fermarlo o nasconderlo, a meno che il movimento, il lampeggiamento o lo scorrimento non facciano parte di un’attività in cui sia essenziale;
   * Auto-update (Aggiornamento automatico): per qualsiasi informazione che viene aggiornata automaticamente
      * a) si avvii automaticamente; e
      * b) è presentato parallelamente ad altri contenuti;
esiste un meccanismo che consente all’utente di metterlo in pausa, interromperlo o nasconderlo oppure di controllare la frequenza dell’aggiornamento, a meno che l’aggiornamento automatico non faccia parte di un’attività in cui è essenziale.

Elementi da sottolineare:

1. Per i requisiti relativi a contenuti che sfarfallano o lampeggiano, vedere [Non progettare contenuti con modalità che possano causare attacchi epilettici (2.3)](#seizures).
1. Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (utilizzato per soddisfare altri criteri di successo o meno) deve soddisfare questo criterio. Consulta [Requisito di conformità 5: non interferenza](https://www.w3.org/TR/WCAG20/#cc5).
1. I contenuti aggiornati periodicamente dal software o trasmessi in streaming all’agente utente non sono tenuti a conservare o presentare le informazioni generate o ricevute tra l’inizio della pausa e la ripresa della presentazione, in quanto ciò potrebbe non essere tecnicamente possibile e in molte situazioni potrebbe risultare fuorviante.
1. Un&#39;animazione che si verifica come parte di una fase di precaricamento o situazione simile può essere considerata essenziale se non si possono verificare interazioni durante quella fase per tutti gli utenti e, se non viene indicato l&#39;avanzamento, potrebbe confondere l’utente o indurre a pensare che il contenuto sia bloccato o interrotto.

#### Finalità - Pausa, stop, nascondi (2.2.2)  {#purpose-pause-stop-hide}

Per alcuni utenti i contenuti in movimento potrebbero essere fonte di distrazione e rendere difficile concentrarsi su altre parti della pagina. Inoltre, tali contenuti possono risultare di difficile lettura per chi ha difficoltà a stare al passo con il testo in movimento.

#### Come soddisfare il criterio - Pausa, stop, nascondi (2.2.2)  {#how-to-meet-pause-stop-hide}

In base alla natura del contenuto, è possibile applicare uno o più dei seguenti suggerimenti durante la creazione di pagine web che includono contenuti in movimento, con effetti di sfarfallio o lampeggiamento:

* Fornisci un mezzo per mettere in pausa lo scorrimento dei contenuti in modo che gli utenti abbiano tempo sufficiente per leggerli. Ad esempio, un componente tipo news ticker o un testo con aggiornamento automatico.
* Assicurati che il contenuto smetta di lampeggiare dopo cinque secondi.
* Utilizza tecnologie appropriate per visualizzare contenuto lampeggiante che possa essere disabilitato dal browser. Ad esempio, file Graphics Interchange Format (GIF) o Animated Portable Network Graphics (APNG).
* Fornisci un controllo modulo nella pagina web per consentire all’utente di disabilitare tutti i contenuti lampeggianti nella pagina.
* Se non è possibile eseguire una delle operazioni precedenti, fornisci un collegamento a una pagina contenente tutti i contenuti, ma senza lampeggiare.

#### Ulteriori informazioni - Pausa, stop, nascondi (2.2.2)  {#more-information-pause-stop-hide}

* [Comprendere il criterio di successo 2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [Come soddisfare il criterio di successo 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-time-limits-pause)

### Attacchi epilettici (2.3)  {#seizures}

[Linea guida 2.3 - Attacchi epilettici: non progettare contenuti con modalità che possano causare attacchi epilettici.](https://www.w3.org/TR/WCAG20/#seizure)

### Tre lampeggiamenti o inferiore alla soglia (2.3.1)  {#three-flashes-or-below-threshold}

* Criterio di successo 2.3.1
* Livello A
* Tre lampeggiamenti o al di sotto della soglia: le pagine web non devono contenere alcun elemento che lampeggi per più di tre volte al secondo, oppure il lampeggiamento deve essere inferiore alle soglie di lampeggiamento generale e rosso.

>[!NOTE]
>
>Dal momento che qualsiasi contenuto che non soddisfi questo criterio di successo può interferire con la capacità di un utente di utilizzare l’intera pagina, tutto il contenuto della pagina web (che sia utilizzato per soddisfare altri criteri di successo o meno) deve rispondere a questo criterio. Consulta [Requisito di conformità 5: non interferenza](https://www.w3.org/TR/WCAG20/#cc5).

#### Finalità - Tre lampeggiamenti o inferiore alla soglia (2.3.1) {#purpose-three-flashes-or-below-threshold}

In alcuni casi i contenuti lampeggianti possono causare crisi epilettiche dovute a fotosensibilità. Questo criterio di successo consente agli utenti a rischio di accedere e utilizzare tutti i contenuti, senza preoccuparsi di eventuali contenuti lampeggianti.

#### Come soddisfare il criterio - Tre lampeggiamenti o inferiore alla soglia (2.3.1)  {#how-to-meet-three-flashes-or-below-threshold}

Adotta misure per assicurare che siano applicate le seguenti tecniche:

* Assicurati che i componenti non lampeggino per più di tre volte al secondo.
* Se la condizione precedente non può essere soddisfatta, visualizza il contenuto lampeggiante all’interno di una *piccola area di sicurezza* in pixel sullo schermo. Quest’area è calcolata utilizzando una formula complessa, trattata in [G176: mantenere l’area lampeggiante sufficientemente piccola](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), pertanto questa tecnica deve essere applicata solo se il contenuto lampeggiante è necessario.

#### Ulteriori informazioni - Tre lampeggiamenti o inferiore alla soglia (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Comprendere il criterio di successo 2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [Come soddisfare il criterio di successo 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#seizure)

### Pagina con titolo (2.4.2)    {#page-titled}

* Criterio di successo 2.4.2
* Livello A
* Titolazione della pagina: alle pagine web sono associati titoli che ne descrivono argomento o finalità.

#### Finalità - Titolazione della pagina (2.4.2)  {#purpose-page-titled}

Questo criterio di successo consente a tutti gli utenti, indipendentemente da eventuali disabilità, di identificare rapidamente il contenuto di una pagina web senza leggere la pagina per intero. Questa struttura è utile quando diverse pagine web vengono aperte in schede del browser, in quanto il titolo della pagina viene visualizzato nella scheda e può quindi essere individuato rapidamente.

#### Come soddisfare il criterio - Titolazione della pagina (2.4.2)  {#how-to-meet-page-titled}

Quando crei una nuova pagina HTML in AEM, puoi specificare il titolo della pagina. Assicurati che il titolo descriva adeguatamente il contenuto della pagina, in modo che i visitatori possano identificare rapidamente se il contenuto è pertinente alle loro esigenze.

È inoltre possibile modificare il titolo della pagina durante la modifica, accessibile da **Sidekick** - **Scheda Pagina** - **Proprietà pagina...**

#### Ulteriori informazioni - Titolazione della pagina (2.4.2) {#more-information-page-titled}

* [Comprendere il criterio di successo 2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [Come soddisfare il criterio di successo 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-title)

### Scopo del collegamento (nel contesto) (2.4.4)    {#link-purpose-in-context}

* Criterio di successo 2.4.4
* Livello A
* Scopo del collegamento (nel contesto): lo scopo di ogni collegamento può essere determinato dal testo del collegamento stesso o dal testo del collegamento insieme al relativo contesto di collegamento determinato a livello di programmazione. L’eccezione è la situazione in cui lo scopo del collegamento è ambiguo per gli utenti in generale.

#### Finalità - Scopo del collegamento (nel contesto) (2.4.4)  {#purpose-link-purpose-in-context}

Per tutti gli utenti, indipendentemente da eventuali disabilità, è fondamentale indicare chiaramente la direzione di un collegamento tramite apposito testo. Questa progettazione consente agli utenti di decidere se vogliono effettivamente seguire un collegamento. Per gli utenti vedenti, un testo di collegamento significativo è utile quando in una pagina sono presenti più collegamenti (in particolare se la pagina è molto ricca di testo), in quanto fornisce un’indicazione più chiara delle funzionalità della pagina di destinazione. Mentre gli utenti delle tecnologie per l’accessibilità, in grado di generare un elenco di tutti i collegamenti su una singola pagina, possono comprendere più facilmente il testo del collegamento fuori dal contesto.

#### Come soddisfare il criterio - Scopo del collegamento (nel contesto) (2.4.4)  {#how-to-meet-link-purpose-in-context}

Soprattutto, fai in modo che lo scopo di un collegamento sia chiaramente descritto all’interno del testo di collegamento.

* Esempio di utilizzo non corretto:

   * Testo: per i dettagli sui nostri corsi serali per l’autunno 2010, fare clic qui.
   * Motivo: non indica in modo chiaro e senza ambiguità la destinazione.

* Esempio di utilizzo corretto:

   * Testo: I nostri corsi serali per l’autunno 2010 - Dettagli.
   * Motivo: modificando leggermente il testo e la posizione dell’elemento di collegamento è possibile migliorare il testo di collegamento:

I collegamenti dovrebbero essere formulati in modo coerente tra le pagine, in particolare per le barre di navigazione. Ad esempio, se un collegamento a una pagina specifica è denominato **Pubblicazioni** in una pagina, utilizza il testo nelle altre pagine per garantire la coerenza.

Tuttavia, al momento della stesura di questo articolo, l&#39;uso dei titoli solleva alcuni problemi:

* Il testo contenuto all&#39;interno dell&#39;attributo title è disponibile solo per gli utenti del mouse come elemento a comparsa con la descrizione comando e non è accessibile utilizzando la tastiera.
* Gli assistenti vocali possono leggere gli attributi del titolo, ma questa funzionalità potrebbe non essere abilitata per impostazione predefinita; gli utenti potrebbero ignorare l’esistenza di un attributo title.
* È difficile modificare l’aspetto del testo del titolo, il che significa che per alcune persone può essere difficile o impossibile da leggere.

Pertanto, anche se l’attributo title può essere utilizzato per fornire contesto aggiuntivo a un collegamento, è importante essere consapevoli dei suoi limiti e non utilizzarlo come alternativa al testo di collegamento appropriato.

Se il collegamento è costituito da un’immagine, accertati che il testo alternativo per l’immagine descriva la destinazione del collegamento. Ad esempio, se l&#39;immagine di una libreria è impostata come collegamento alle pubblicazioni di un utente, il testo alternativo dovrebbe essere **Pubblicazioni di John Smith** e non **Libreria**.

In alternativa, se l’ancoraggio del collegamento contiene testo che descrive lo scopo del collegamento in aggiunta all’elemento immagine (e quindi il testo viene visualizzato accanto all’immagine), utilizza un attributo alt vuoto per l’immagine:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
>
>Lo snippet di cui sopra è un&#39;illustrazione, si consiglia di utilizzare il componente **Immagine**.

Mentre è opportuno fornire un testo di collegamento che identifichi lo scopo del collegamento senza necessità di ulteriore contesto, questo effettivamente non è sempre possibile. I collegamenti senza contesto possono essere utilizzati nei casi seguenti, di cui è possibile trovare alcuni esempi HTML in [Come soddisfare il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-refs).

* Qualora il testo di collegamento sia parte di un elenco di collegamenti strettamente correlati, e la voce di elenco che racchiude il collegamento fornisca contesto sufficiente.
* Laddove lo scopo di un collegamento possa essere chiaramente identificato dal testo di paragrafo *che lo precede* (non che lo segue).
* Se il collegamento è contenuto all’interno di una tabella di dati e quindi lo scopo può essere chiaramente identificato dalle relative intestazioni.
* Se un elenco di collegamenti è contenuto all’interno di un insieme di intestazioni e l’intestazione stessa fornisce un contesto adeguato.
* Se un elenco di collegamenti è contenuto all’interno di un collegamento nidificato e la voce principale al di sopra del collegamento nidificato fornisce il contesto appropriato.

In alcuni casi, laddove in una pagina siano presenti diversi collegamenti (ciascuno dei quali fornisce la direzione di un collegamento con dettagli complessi ma necessari), può essere opportuno prevedere una versione alternativa della pagina web che mostri lo stesso contenuto, ma in cui il testo dei collegamenti non sia così dettagliato.

In alternativa, puoi utilizzare script in modo da fornire una quantità minima di testo all’interno del collegamento stesso. Tuttavia, quando si attiva un controllo appropriato posizionato nella parte superiore della pagina, il testo del collegamento viene *espanso* per fornire ulteriori dettagli. Un approccio simile consiste nell&#39;utilizzare CSS per *nascondere* il collegamento completo agli utenti normovedenti, ma mostrarlo agli utenti di utilità di lettura dello schermo. Questo non rientra nell&#39;ambito di questo documento, ma ulteriori informazioni su come ottenere questo risultato sono disponibili nella sezione [Ulteriori informazioni - Scopo del collegamento (nel contesto) (2.4.4)](#more-information-link-purpose-in-context).

#### Ulteriori informazioni - Scopo del collegamento (nel contesto) (2.4.4) {#more-information-link-purpose-in-context}

* [Comprendere il criterio di successo 2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [Come soddisfare il criterio di successo 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-refs)
* [C7: Utilizzo dei CSS per nascondere una parte del testo di collegamento](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## Principio 3: Comprensibilità  {#principle-understandable}

[Principio 3: Comprensibile - Le informazioni e le operazioni dell’interfaccia devono essere comprensibili.](https://www.w3.org/TR/WCAG20/#understandable)

### Rendere il testo leggibile e comprensibile (3.1)  {#make-text-content-readable-and-understandable}

[Linea guida 3.1 - Leggibile: rendere il testo leggibile e comprensibile.](https://www.w3.org/TR/WCAG20/#meaning)

### Lingua della pagina (3.1.1)  {#language-of-page}

* Criterio di successo 3.1.1
* Livello A
* Lingua della pagina: la lingua predefinita di ogni pagina web può essere determinata a livello di programmazione.

#### Finalità - Lingua della pagina (3.1.1)  {#purpose-language-of-page}

Lo scopo di questo criterio è fare in modo che il testo e gli altri contenuti linguistici siano resi correttamente. Per gli utenti di utilità di lettura dello schermo, questo garantisce che la pronuncia sia corretta, mentre i browser visivi saranno più propensi a visualizzare certi set di caratteri correttamente.

#### Come soddisfare il criterio - Lingua della pagina (3.1.1)  {#how-to-meet-language-of-page}

Per soddisfare questo criterio di successo, la lingua predefinita di una pagina web può essere identificata mediante l’attributo `lang` all’interno dell’elemento `<html>` nella parte superiore della pagina. Esempio:

* Se una pagina è scritta in inglese britannico, l’elemento `<html>` dovrebbe riportare:

  `<html lang = "en-gb">`

* Una pagina che deve essere resa in inglese americano dovrebbe invece adottare il seguente standard:

  `<html lang = "en-us">`

In AEM, la lingua predefinita della pagina è impostata durante la creazione, ma può anche essere modificata quando apporti cambiamenti alla pagina. Questa funzione è accessibile dal percorso **barra laterale** > scheda **Pagina** > **Proprietà pagina** > scheda **Avanzate**.

#### Ulteriori informazioni - Lingua della pagina (3.1.1) {#more-information-language-of-page}

* [Comprendere il criterio di successo 3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [Come soddisfare il criterio di successo 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-meaning-doc-lang-id)
* I codici sono basati sulla norma ISO 639-1. Un elenco più completo dei codici per ogni lingua è disponibile nel sito [W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Parti in lingua (3.1.2)    {#language-of-parts}

* Criterio di successo 3.1.2
* Livello AA
* Parti in lingua: la lingua di ogni passaggio o frase nel contenuto può essere determinata a livello di programmazione, fatta eccezione per nomi propri, termini tecnici, parole in lingue indeterminate e parole o frasi che sono diventate parte del gergo del testo immediatamente circostante.

#### Finalità - Parti in lingua (3.1.2)  {#purpose-language-of-parts}

Lo scopo di questo criterio di successo è simile al criterio di successo [Lingua della pagina](#language-of-page), tranne per le pagine web che contengono contenuti in più lingue su una singola pagina (ad esempio, a causa di citazioni o prestiti lessicali non comuni).

Le pagine in cui viene applicato questo criterio di successo consentono quanto segue:

* Inserimento di caratteri accentuati da parte di software di traduzione Braille.
* Lettori di schermo per pronunciare correttamente le parole non nella lingua predefinita.
* Traduzione corretta del contenuto da una lingua all’altra da parte di strumenti di traduzione come Google Traduttore.

#### Come soddisfare il criterio - Parti in lingua (3.1.2)  {#how-to-meet-language-of-parts}

L’attributo `lang` può essere utilizzato per identificare le modifiche nella lingua del contenuto. Ad esempio, una citazione in tedesco (codice ISO 639-1 “de”) può essere mostrata come segue:

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
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</span>.</p>
```

>[!NOTE]
>
>Non è necessario seguire questo criterio di successo per nomi o città in lingue diverse, o quando si utilizzano prestiti lessicali o frasi diventati comuni nella lingua predefinita (come *schadenfreude* in inglese).

Per aggiungere l’elemento span con una lingua appropriata, è possibile modificare manualmente il codice HTML nella modalità di modifica sorgente dell’editor Rich Text, affinché venga letto come sopra indicato. In alternativa, l’attributo `lang` può essere incluso nell’editor Rich Text da un amministratore di sistema (consulta [ Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Ulteriori informazioni - Parti in lingua (3.1.2) {#more-information-language-of-parts}

* [Comprendere il criterio di successo 3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html)
* [Come soddisfare il criterio di successo 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-meaning-other-lang-id)

### Aiutare gli utenti a evitare e correggere gli errori (3.3)  {#help-users-avoid-and-correct-mistakes}

[Linea guida 3.3 - Assistenza nell’inserimento: aiutare gli utenti a evitare e correggere gli errori.](https://www.w3.org/TR/WCAG20/#minimize-error)

### Etichette o istruzioni (3.3.2)  {#labels-or-instructions}

* Criterio di successo 3.3.2
* Livello A
* Etichette o istruzioni: le etichette o le istruzioni vengono fornite quando il contenuto richiede l’input dell’utente.

#### Finalità - Etichette o istruzioni (3.3.2)  {#purpose-labels-or-instructions}

Fornire istruzioni per aiutare le persone a completare i moduli è una parte fondamentale della buona prassi nell’usabilità dell’interfaccia. È utile per le persone con disabilità visive o cognitive che altrimenti potrebbero avere difficoltà a comprendere il layout di un modulo e il tipo di dati da fornire in un particolare campo del modulo.

In AEM viene aggiunta un&#39;etichetta predefinita quando si aggiunge alla pagina un componente modulo, ad esempio un **Campo di testo**. Questo titolo predefinito dipende dal tipo di componente. Puoi aggiungere un titolo personalizzato nella sezione **Titolo e testo** della finestra di dialogo per la modifica del campo. È importante assicurarsi che le etichette aiutino gli utenti a comprendere i dati associati a ciascun componente del modulo.

![Scheda Titolo e testo (finestra di dialogo di modifica); il titolo &#39;Descrizione&#39; è stato aggiunto.](assets/chlimage_1-22a.png)

Il campo **Titolo** deve essere utilizzato per gli elementi di campo in quanto fornisce un’etichetta che è disponibile per la tecnologia per l’accessibilità. Scrivere semplicemente un’etichetta di testo accanto al campo non è sufficiente.

Per alcuni componenti modulo è inoltre possibile nascondere visivamente le etichette utilizzando la casella di controllo **Nascondi titolo**. Le etichette nascoste in questo modo sono ancora disponibili per la tecnologia di assistenza, ma non vengono visualizzate sullo schermo. Anche se questo può essere un buon approccio in alcune situazioni, è meglio includere un’etichetta visiva laddove possibile. Alcuni utenti guardano una piccola sezione dello schermo (un campo alla volta) e hanno bisogno delle etichette per identificare correttamente il campo.

#### Pulsanti immagine {#image-buttons}

Se utilizzi i pulsanti immagine (ad esempio, il componente **Pulsante immagine**), il campo **Titolo** nella scheda **Titolo e testo** della finestra di dialogo di modifica fornisce effettivamente il testo alt per l’immagine, anziché l’etichetta. Nell’esempio seguente, l’immagine con il testo `Submit` presenta il testo alt `Submit`, aggiunto dal campo **Titolo** della finestra di dialogo di modifica.

![Pulsante Immagine con Testo alternativo impostato nel campo Titolo (finestra di dialogo per modifica).](assets/chlimage_1-23a.png)

#### Gruppi di campi modulo {#groups-of-form-fields}

Se è presente un gruppo di controlli correlati, ad esempio **Gruppo pulsanti di scelta**, potrebbe essere necessario assegnargli un titolo e controlli specifici. Quando si aggiunge un set di pulsanti di scelta in AEM, il campo **Titolo** fornisce il titolo del gruppo, mentre i singoli titoli vengono specificati durante la creazione dei pulsanti di scelta (**Elementi**).

![Aggiunta di elementi al gruppo radio. Il titolo del gruppo è &quot;Contattami per&quot;, definito nel campo Titolo.](assets/chlimage_1-24a.png)

Tuttavia, non esiste alcuna associazione programmatica tra il titolo del gruppo e i pulsanti di scelta. Per creare questa associazione, gli editor modelli devono racchiudere il titolo tra i tag `fieldset` e `legend` necessari. Questa operazione può essere eseguita solo modificando il codice sorgente della pagina. In alternativa, un amministratore di sistema può aggiungere il supporto di questi elementi affinché vengano visualizzati nella finestra di dialogo **Proprietà campo** (consulta [Aggiunta di supporto per elementi e attributi HTML aggiuntivi](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Considerazioni aggiuntive relative ai moduli {#additional-considerations-for-forms}

Se i dati devono essere immessi in un formato specifico, specificalo chiaramente nel testo dell’etichetta. Ad esempio, se una data deve essere inserita nel formato `DD-MM-YYYY`, indicala chiaramente come parte dell’etichetta. Ciò significa che, quando chi usa un’utilità di lettura dello schermo arriva al campo, l’etichetta viene annunciata automaticamente, insieme alle informazioni aggiuntive relative al formato.

Se l’input di un campo modulo è obbligatorio, specificalo integrando la parola “obbligatorio” nell’etichetta. AEM aggiunge un asterisco quando un campo è obbligatorio, ma sarebbe ideale includere la parola `required` nell’etichetta stessa (nel campo **Titolo** della finestra di dialogo di modifica).

![Aggiunta di informazioni aggiuntive (parola obbligatoria) per gli utenti di utilità di lettura dello schermo nel campo &#39;Titolo&#39;.](assets/chlimage_1-25a.png)

Il posizionamento delle etichette è importante anche in quanto aiuta a individuare campi appropriati. Questo è di particolare importanza quando l’utente si trova di fronte a un modulo complesso. Segui la convenzione qui di seguito:

* Caselle di controllo o pulsanti di scelta:

  Le etichette sono posizionate immediatamente a destra del campo.

* Tutti gli altri componenti del modulo (ad esempio caselle di testo, caselle combinate):

  Le etichette sono posizionate immediatamente sopra o a sinistra del campo.

Nei moduli semplici con funzionalità limitata, l&#39;etichettatura appropriata di un pulsante `Submit` può fungere da etichetta per il campo adiacente, ad esempio `Search`. Ciò è utile in situazioni in cui potrebbe risultare difficile trovare spazio per il testo dell’etichetta.

#### Ulteriori informazioni - Etichette o istruzioni (3.3.2) {#more-information-labels-or-instructions}

* [Comprendere il criterio di successo 3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [Come soddisfare il criterio di successo 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-minimize-error-cues)
