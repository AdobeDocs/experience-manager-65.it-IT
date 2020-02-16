---
title: Guida rapida a WCAG 2.0
seo-title: Guida rapida a WCAG 2.0
description: Panoramica rapida delle linee guida per l'accessibilità WCAG 2.0.
seo-description: Panoramica rapida delle linee guida per l'accessibilità WCAG 2.0.
uuid: a5cf463e-89e9-4cc0-9c91-69a1fd3d8ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-accessibility
content-type: reference
discoiquuid: 3cac0e34-7514-48ce-a93b-592bbdbcd252
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Guida rapida a WCAG 2.0{#quick-guide-to-wcag}

AEM è stato sviluppato per massimizzare la conformità alle linee guida sull’accessibilità dei contenuti Web:

Le linee guida per l&#39;accessibilità dei contenuti [Web versione 2.0 (WCAG2)](https://www.w3.org/TR/WCAG/) sono una serie di linee guida riconosciute a livello internazionale sviluppate dal [World Wide Web Consortium (W3C)](https://www.w3.org/) nell&#39;ambito della loro iniziativa per l&#39;accessibilità [Web (WAI)](https://www.w3.org/WAI/).

WCAG 2.0 è costituito da un insieme di linee guida tecnologiche indipendenti e di criteri di successo per contribuire a rendere i contenuti web accessibili e utilizzabili da persone con disabilità. Essi forniscono consulenza agli autori, ai progettisti e agli sviluppatori di contenuti web per garantire che le risorse da essi prodotte siano il più accessibili possibile a quante più persone possibile, indipendentemente da eventuali disabilità; ad esempio, disabilità visive, perdita dell&#39;udito, difficoltà di apprendimento, limiti legati all&#39;età, tra gli altri.

Ad esempio, descrivere un’immagine (o qualsiasi altro contenuto non testuale) utilizzando l’ `alt` attributo in HTML è molto vantaggioso per le persone non vedenti o ipovedenti. La descrizione testuale nell&#39; `alt` attributo può essere convertita in uscita vocale o trasmessa a display braille aggiornabili elettronici.

Inoltre, WCAG 2.0 può comportare vantaggi per altri beneficiari, comprese le persone che possono essere considerate disabili ** situazionali. Persone che, a causa di circostanze come la tecnologia di navigazione, la velocità di connessione di rete o l&#39;ambiente di navigazione, possono incontrare barriere simili a persone con disabilità.

Utilizzando Adobe Experience Manager, gli autori di contenuti e/o i proprietari di siti Web possono creare contenuti Web che soddisfano i criteri di successo WCAG 2.0 di livello A e AA.

Pertanto, comprendere gli obiettivi di WCAG 2.0 e come sono strutturate le linee guida è una parte importante della comprensione dell&#39;accessibilità Web e di come le linee guida possono essere utili per creare contenuti Web accessibili.

L&#39;intenzione di WCAG 2.0 è di fornire linee guida che:

* Non sono **tecnologici:**

   In altre parole, linee guida che possono essere applicate a una serie di formati di contenuto Web, non solo HTML. WCAG 2.0 può quindi includere contenuti generati da o forniti in PDF, Flash, JavaScript e altre tecnologie Web attuali e future. Questo obiettivo è quello di affrontare una debolezza riconosciuta di WCAG 1.0, in quanto era focalizzata su HTML a scapito di altri formati di contenuto Web.

* Sono **testabili:**

   Ogni orientamento è redatto in modo tale da poter essere testato obiettivamente per garantire che un gruppo di esperti in materia di accessibilità concordi in generale sul fatto che la linea guida è stata rispettata. Una delle sfide delle linee guida sull&#39;accessibilità è che alcuni possono essere tecnicamente testabili, altri richiedono un giudizio umano per verificare se le linee guida sono state rispettate o meno. WCAG 2.0 è stato scritto con l&#39;obiettivo di ridurre la soggettività che era presente in alcune delle linee guida WCAG 1.0 e checkpoint.

* Supporto dell&#39;implementazione contestuale e **con priorità:**

   Come per WCAG 1.0, le linee guida WCAG 2.0 hanno priorità, relative al probabile impatto di non seguire una linea guida su un particolare gruppo di utenti con disabilità. Questo consente agli autori di prendere una decisione informata sulle linee guida più importanti per la loro situazione particolare. Inoltre, viene introdotto il concetto di *accessibilità supportata* . Questo consente agli autori di decidere come utilizzare al meglio le tecnologie Web che potrebbero non disporre del supporto completo per l&#39;accessibilità, o che potrebbero richiedere agli utenti di disporre di tecnologie e/o browser di assistenza specifici per beneficiare delle funzioni di accessibilità.

Tali obiettivi hanno influenzato in modo significativo la struttura di WCAG 2.0.

>[!NOTE]
>
>Non è possibile creare un sito web che si occupi di ogni possibile disabilità o tipo di persona. Lo scopo di WCAG 2.0 è aiutare gli autori di siti Web a creare, per quanto possibile, siti accessibili in determinate condizioni e con ragione.

>[!NOTE]
>
>Se avete familiarità con WCAG 1.0, noterete alcune modifiche in WCAG 2.0. Questi riguardano la portata, l&#39;organizzazione e l&#39;obiettivo.

## Struttura {#structure}

WCAG 2.0 è strutturato in modo da introdurre concetti di creazione di contenuti Web accessibili in modo progressivamente dettagliato. Ciò può dare l&#39;impressione che WCAG 2.0 sia un insieme molto complesso di documenti interconnessi, ma l&#39;obiettivo è (progressivamente) fornire informazioni più dettagliate come e quando gli autori ne hanno bisogno - piuttosto che fornire tutto in un documento molto grande.

WCAG 2.0 è costituito da quattro principi chiave per la progettazione accessibile. Si tratta di:

1. **Percepibilità**: può un utente percepire il contenuto Web in questione?
1. **Operabile**: un utente può navigare, inserire dati o in altro modo interagire con il contenuto Web?
1. **Comprensibilità**: un utente può elaborare e comprendere il contenuto Web che gli viene presentato?
1. **Robusto**: il contenuto Web è disponibile nel modo previsto in un&#39;ampia gamma di ambienti di navigazione, inclusi ambienti di navigazione legacy ed emergenti?

Questi principi sono a volte citati dall&#39;acronimo POUR.

* Ogni **principio** è costituito da una o più **linee guida**.

   * Le linee guida sono formulate come istruzioni, che sono positive (fate questo...) o negative (non eseguite questa operazione...).
   * Le linee guida sono numerate da 1.1 a 4.1, se il primo numero corrisponde al principio primario.

* Ogni linea guida è costituita da uno o più criteri **di** successo.

   * I criteri di successo sono scritti come istruzioni, che sono `True` o `False` per una determinata pagina Web.
   * I criteri di successo possono comprendere una o più scelte, o possono includere eccezioni; situazioni in cui i criteri di successo non devono essere soddisfatti.
   * I criteri di successo sono numerati in base alla linea guida e al principio padre, da 1.1.1 a 4.1.1. Hanno anche un nome breve che riassume l’intento del criterio, per un riferimento più semplice. Ad esempio, il criterio di successo 1.1.1 è un’alternativa non testuale.
   * I criteri di successo includono un elenco delle **tecniche** correlate (descritte più dettagliatamente di seguito).

## Risorse di supporto {#supporting-resources}

Oltre alle componenti di base WCAG 2.0 di Principi, Linee guida e Criteri di successo, è disponibile una serie di documenti giustificativi. Alcuni di essi forniscono consigli specifici su come soddisfare gli aspetti delle linee guida, altri sono riferimenti più generali che aiutano gli autori, i progettisti e gli sviluppatori di tutte le capacità a comprendere e utilizzare WCAG 2.0 nel modo più efficace possibile.

Mentre WCAG 2.0 è un documento stabile e non cambierà, la maggior parte di queste risorse di supporto sono documenti dinamici; cambieranno e cresceranno nel tempo, man mano che emergeranno nuove tecnologie, e si scopriranno nuovi esempi di come l&#39;accessibilità del web può essere raggiunta.

### Risorse WCAG 2.0 {#wcag-resources}

* [un profilo di tutti i documenti](https://www.w3.org/WAI/intro/wcag.php)WCAG 2.0;
* [Spiegazione del modo in cui i diversi componenti si relazionano tra loro](https://www.w3.org/WAI/intro/wcag20);
* [Domande](https://www.w3.org/WAI/WCAG20/wcag2faq.html)frequenti su WCAG 2.0;

### Tecniche per WCAG 2.0 {#techniques-for-wcag}

Le tecniche per WCAG 2.0 sono disponibili nella pagina [Tecniche per WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/) .

**Le tecniche** costituiscono il livello seguente dei criteri di successo nella gerarchia WCAG 2.0. Sono classificati da WAI come informazioni, non normative. In altre parole, non è necessario seguire una tecnica specifica affinché una risorsa sia conforme a WCAG 2.0.

Poiché le tecniche sono molto più specifiche dei criteri di successo, in genere si riferiscono a una particolare tecnologia o tipo di contenuto (ad es. HTML, o video), o a una situazione (ad es. applicazione di e-commerce o di e-learning). È possibile considerare le tecniche come esempi comprovati di come possono essere soddisfatte specifiche linee guida e criteri di successo, per cui sono utili strumenti per autori e sviluppatori che lavorano in contesti specifici.

È possibile accedere a tecniche:

* Per raccolta (le tecniche possono essere generali, o correlate a una tecnologia o a un formato specifico, ad esempio HTML, CSS o script sul lato client), oppure
* Da criteri di successo correlati. Le tecniche possono essere applicate a più criteri di successo.

Ogni tecnica ha un numero univoco, relativo alla raccolta. Ad esempio, una delle tecniche ARIA è la *Tecnica ARIA2: Identificazione dei campi obbligatori con la proprietà*&quot;obbligatorio&quot;.

Le tecniche possono essere sufficienti, di avviso o di guasto:

* Una *Tecnica* Sufficiente è una, che, se seguita, sarà sufficiente per soddisfare un particolare criterio di successo.
* Si tratta di una tecnica ** consultiva che, se seguita, avrà un impatto positivo sull&#39;accessibilità, ma che potrebbe non essere sufficiente da sola per garantire il rispetto di un particolare criterio di successo.
* Un *fallimento* è una tecnica che descrive un esempio specifico di dove non sarebbero stati soddisfatti i criteri di successo.

I dettagli delle tecniche includono una descrizione, applicabilità, esempi, risorse per ulteriori informazioni e dettagli su come gli autori possono testare per un&#39;applicazione efficace della tecnica.

L&#39;elenco delle tecniche non è completo e WAI aggiorna costantemente l&#39;elenco con nuovi esempi, che riflettono gli sviluppi della tecnologia web, gli approcci di progettazione e i risultati della ricerca. Quindi vale la pena controllare regolarmente la lista delle tecniche per nuove aggiunte.

### Informazioni su WCAG 2.0 {#understanding-wcag}

Si tratta di una serie di documenti che forniscono consigli ai lettori per valutare lo scopo di specifiche linee guida e criteri di successo. Potete [scaricare un’introduzione e collegamenti a informazioni](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/Overview.html)più dettagliate.

Ogni orientamento e criterio di successo ha anche una propria pagina &quot;Comprensione&quot;, con informazioni su:

* L&#39;intento della linea direttrice;
* Criteri di successo specifici;
* Tecniche di consulenza, che contribuiscono a soddisfare i requisiti dell&#39;orientamento, ma che non rientrano in alcun criterio di successo specifico.

La pagina &quot;comprensione&quot; di ciascun criterio di successo fornisce informazioni su:

* l’intento del criterio di successo;
* Esempi generali di come può essere soddisfatto il criterio di successo;
* risorse correlate (non W3C) su come soddisfare il criterio di successo;
* Tecniche e guasti: esempi specifici e dettagliati di come soddisfare il criterio di successo (descritti più dettagliatamente di seguito)
* Termini chiave - un glossario di termini importanti per comprendere il criterio di successo.

Un esempio è disponibile all&#39;indirizzo: [Comprendere il criterio di successo 1.1.1 (&quot;Contenuto non testuale&quot;)](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/text-equiv-all.html).

### Come soddisfare WCAG 2.0 {#how-to-meet-wcag}

La sezione &quot;Come soddisfare il criterio&quot; è disponibile nella pagina [How To Meet WCAG 2.0](https://www.w3.org/WAI/WCAG20/quickref/) . Questa sezione fornisce una presentazione alternativa di WCAG, che consente di affinare il contenuto delle linee guida a quelli più rilevanti per gli interessi o le circostanze di un lettore. I lettori possono filtrare le tecniche relative ai criteri di successo che desiderano visualizzare specificando particolari tecnologie di contenuto Web, ad esempio Cascading Style Sheets o script, oppure specificando un particolare livello di priorità.

Senza filtro, questa risorsa fornisce tutti i criteri di successo raggruppati per linea guida. Per ciascun criterio di successo, è fornito quanto segue:

* Il testo del criterio di successo;
* un collegamento al corrispondente documento &quot;intesa&quot;;
* Un elenco delle tecniche sufficienti correlate, che si collega ai dettagli di ciascuna tecnica;
* un elenco delle tecniche di consulenza correlate, con collegamento ai dettagli di ciascuna tecnica (se presente);
* Elenco di errori correlati, collegamento ai dettagli di ogni errore.