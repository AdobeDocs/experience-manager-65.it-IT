---
title: Note sulla versione per  [!DNL Adobe Experience Manager] 6.5
description: Trova informazioni sulla versione, novità, procedure di installazione e un elenco dettagliato delle modifiche per  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 7fdfcc9964bccfea03304e6cae3b5569421720ed
workflow-type: tm+mt
source-wordcount: '9628'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.24.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione del Service Pack |
| Data | 26 novembre 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!-- OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) -->

## Cosa è incluso in [!DNL Experience Manager] 6.5.24.0 {#what-is-included-in-aem-6524}

[!DNL Experience Manager] 6.5.24.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la data di disponibilità iniziale di 6.5 di aprile 2019. [Installa il Service Pack ](#install) in [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->


## Nuove funzioni e miglioramenti

### Forms

* **Supporto per il passaggio di XCI personalizzati:** Aggiunta del supporto per il passaggio di XCI personalizzati nei parametri dell&#39;applicazione cmdlet xmlformcmd. Questo consente agli utenti di specificare file XCI personalizzati per il test, migliorando la flessibilità e il controllo sul processo di test. (LC-3923248)


## Problemi risolti in Service Pack 24 {#fixed-issues}

<!-- 6.5.24.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Assets] {#assets-sp24}

* Dopo l&#39;aggiornamento alla versione 6.5.23.0, l&#39;ordinamento delle cartelle in base alla data di modifica in Vista a schede ha causato difficoltà nell&#39;individuare le risorse modificate di recente per le distribuzioni on-premise. (ASSETS-56946)
* Le voci ripetute del registro di avviso vengono generate durante le esecuzioni del modulo di pianificazione. (ASSETS-52554)
* L’ordinamento dei titoli non funziona nella vista a elenco. (ASSETS-50716)
* La finestra Proprietà raccolta non si chiude neanche dopo aver fatto clic sul pulsante Annulla. (ASSETS-48504)

* Errore *URL non valido* durante il tentativo di annotare risorse in AEM 6.5.22. (NPR-42684)
* Il modulo Editor metadati di Assets non viene reinizializzato dopo l’esecuzione di azioni di correlazione o di annullamento della correlazione. (ASSETS-52207)
* Quando le risorse da DAM remoto vengono risincronizzate con Sites local, lo stato di pubblicazione delle risorse viene erroneamente aggiornato a `Not published`. (ASSETS-48958)
* Problemi riscontrati durante l’aggiornamento da SP23 alla versione 6.5 LTS. (ASSETS-50541)

### [!DNL Sites]{#sites-6524}

#### Accessibilità {#sites-accessibility-6524}

* La finestra di dialogo **Cambia formato di visualizzazione** ora supporta l&#39;utilizzo della tastiera. Lo stato attivo non ignora più il pulsante **Visualizza impostazioni** e le chiavi standard (`Tab`, `Enter`, `Space`) funzionano in modo coerente. (SITES-24306)
* Gli utenti che utilizzano la tastiera possono rimuovere i tag di stato pubblicati senza il mouse. Lo stato attivo termina su ciascun tag e l&#39;attivazione funziona con `Enter`/`Space` e Backspace/Delete. Il controllo tag ora si comporta come un pulsante, che migliora il feedback dell’assistente vocale e soddisfa la tastiera WCAG 2.1.1. (SITES-24491)
* La barra dei filtri viene ridisposta in modo dinamico in riquadri di visualizzazione stretti. I controlli di selezione e i risultati rimangono all&#39;interno del riquadro di visualizzazione con uno zoom del 400%, eliminando lo scorrimento orizzontale e il cut-off dei contenuti. (SITES-24708)
* AEM ripristina l’accesso completo da tastiera ai pulsanti Reimpostazione ContextHub, Persona e Dispositivo. I tasti TAB e freccia raggiungono ogni controllo, visualizzano un indicatore di stato attivo visibile e attivano azioni con `Enter` o `Space`. Le utilità per la lettura dello schermo annunciano etichette chiare. (SITES-24939)
* L’input della data e il selettore rimangono completamente visibili a 320 px. La finestra modale Timewarp utilizza il dimensionamento dinamico, in modo che il controllo non venga più ritagliato o scomparso sulla finestra di visualizzazione più piccola. (SITES-24962)
* La barra dei riferimenti ora supporta lo zoom del browser al 400% senza perdere l’accesso al relativo contenuto. La barra utilizza un ridimensionamento dinamico invece di una larghezza fissa, in modo che gli elementi rimangano visibili e selezionabili a 1280×1024. (SITES-24972)
* La barra dei filtri ora funziona con uno zoom del 400%. La barra si ridimensiona con le unità relative e non blocca né nasconde più i controlli filtro. Gli utenti possono visualizzare e selezionare ogni opzione di filtro senza scorrimento orizzontale o destinazioni di hit troncate. (SITES-24981)
* Gli utenti che utilizzano la tastiera possono utilizzare i menu di formattazione nella finestra modale Teaser. Premendo `Enter` o `Space` su **Elenco** o **Formato paragrafo** si apre la finestra popup, le opzioni di spostamento dei tasti freccia e `Enter` si applica la selezione. `Escape` chiude il menu e ripristina lo stato attivo sul controllo di attivazione, generando un flusso di lavoro della barra degli strumenti coerente. (SITES-25235)
* La finestra a comparsa del selettore colore Campione ora rimane nella finestra della vista a 320 px. Il popover mostra tutte le righe di colore e supporta lo scorrimento, in modo che gli autori possano selezionare qualsiasi campione su schermi di piccole dimensioni. (SITES-25274)
* I menu a discesa della barra degli strumenti demografica ora funzionano completamente con la tastiera. Quando si apre un menu, lo stato attivo viene spostato sulla prima opzione, i tasti di direzione consentono di spostarsi nell&#39;elenco e le opzioni Esc/Tab chiudono o avanzano senza spostare lo stato attivo sulla barra degli strumenti. Gli elementi interattivi utilizzano la semantica corretta in modo che NVDA e altri lettori comunichino correttamente le opzioni. (SITES-25310)
* L’aggiunta di un componente nella struttura Contenuto funziona come previsto in AEM 6.5 SP24. L’errore iniziale deriva da autorizzazioni di authoring mancanti in una configurazione locale, non da AEM. Gli autori con i diritti di modifica possono attivare il pulsante e aggiungere componenti tramite tastiera o mouse. (SITES-25312)
* L’accesso tramite tastiera e utilità di lettura dello schermo nella barra degli strumenti Demografica ora funziona in modo affidabile. Gli autori che utilizzano NVDA possono attraversare **Commerce**, **Persona** e 88 con frecce, osservare il feedback chiaro dell&#39;elemento attivo e capire quale scheda è attiva. (SITES-25326)

* Il collegamento **Passa al contenuto** ora sposta lo stato attivo della tastiera sull&#39;intestazione del contenuto principale. Lo stato di attivazione rimane visibile su un target identificato in modo univoco, pertanto gli assistenti vocali annunciano la sezione corretta. La modifica soddisfa le linee guida WCAG 2.4.1 e 2.4.3. (SITES-24061)
* La navigazione tramite tastiera nella struttura della home page di Sites segue una sequenza logica dopo l&#39;utilizzo di **Seleziona tutto**. Lo stato attivo si sposta da **Seleziona tutto** al controllo successivo (barra a sinistra aperta) invece di tornare all&#39;inizio della pagina. (SITES-24307)
* I titoli delle sezioni e i controlli di modifica nell’editor Sites rispondono all’attivazione e allo stato attivo della tastiera. Gli utenti di tastiera mostrano lo stesso titolo e le stesse azioni che apparivano in precedenza solo al passaggio del mouse. (SITES-24479)
* I pulsanti nell’editor Sites espongono nomi descrittivi invece di etichette generiche o mancanti. Le tecnologie per l’accessibilità annunciano l’azione corretta, che migliora la chiarezza e riduce i clic errati. (SITES-24480)
* Gli assistenti vocali ricevono un messaggio vocale di &quot;Caricamento&quot; durante l’aggiornamento della visualizzazione Sites. L’aggiornamento aggiunge un’area live di stato dedicata e scrive il messaggio in essa a livello di programmazione, che conferma l’avanzamento senza spostare lo stato attivo. (SITES-24481)
* La barra laterale di Assets ora include un controllo **Chiudi** deselezionato e riporta lo stato attivo sul pulsante di attivazione/disattivazione. Gli utenti che utilizzano la tastiera o gli assistenti vocali ignorano immediatamente il pannello invece di passare da un controllo all’altro. La modifica riduce la pressione dei tasti e corrisponde al comportamento previsto per il pannello. (SITES-24489)
* L’elenco delle schede ARIA nell’Editor pagina Sites include un nome descrittivo. Gli assistenti vocali ora identificano il controllo come un elenco di schede e leggono l’etichetta corretta, consentendo agli utenti di trovare il set giusto di schede e spostarsi tra di esse in modo affidabile. (SITES-24492)
* La ricerca nella barra laterale dell’editor ora annuncia i risultati agli assistenti vocali. Quando gli utenti digitano, un messaggio di stato live segnala il numero di corrispondenze e aggiornamenti senza spostare lo stato attivo. Gli utenti di tastiera scoprono immediatamente i risultati. (SITES-24506)
* La selezione delle righe nella Vista a elenco è più efficace per gli utenti di tecnologie per l’accessibilità. La casella di controllo espone un nome significativo derivato dalla riga Titolo, pertanto gli annunci rimangono brevi e descrivono correttamente l’azione. (SITES-24514)
* Nomi di accessibilità della Vista a elenco corretti. La tabella rimuove `aria-label` da elementi non interattivi e assegna l&#39;etichetta al collegamento o al pulsante actionable. Gli utenti che utilizzano un’utilità di lettura dello schermo ora sentono etichette precise e non duplicate in tutta la colonna. (SITES-24515)
* L’intestazione fissa ha smesso di oscurare la finestra di dialogo modale del teaser durante l’uso di zoom elevato. Il contenuto rimane leggibile e utilizzabile con uno zoom del 200% e del 400%, con flusso verticale e senza sezioni ritagliate. (SITES-24523)
* La digitazione nel campo di ricerca non attiva più un annuncio prematuro del primo risultato o un’attivazione accidentale. L’esperienza ora annuncia un messaggio di stato conciso con il conteggio dei risultati, mentre lo stato attivo rimane nel campo fino a quando l’utente non passa all’elenco. (SITES-24658)
* Il campo Testo alternativo nella finestra di dialogo Collegamento ipertestuale dell’editor di testo ora espone un’etichetta programmatica. Gli assistenti vocali annunciano &quot;Testo alternativo&quot; per il campo e lo stato attivo si focalizza sul controllo con nome corretto. Questa correzione migliora la navigazione per gli utenti che utilizzano tastiera e riconoscimento vocale. (SITES-24675)
* È stato aggiunto un messaggio di stato in tempo reale alla barra Riferimenti in modo che le tecnologie per l’accessibilità possano annunciare immediatamente le modifiche. Selezionando più elementi si attiva un messaggio chiaro sulla disponibilità del riferimento, che impedisce le modifiche dello stato invisibile all&#39;utente e riduce le azioni ripetute. (SITES-24678)
* Ora la finestra di dialogo Immagine annuncia il suo stato di caricamento attraverso un’area ARIA live. Gli assistenti vocali sentono un messaggio di tipo &quot;Caricamento in corso, attendi&quot; mentre viene visualizzato il pulsante di selezione. Inoltre, è un aggiornamento pronto al termine del contenuto, per consentire agli utenti di sapere quando possono interagire. (SITES-24697)
* La finestra di dialogo Selezione collegamento ora espone un’area attiva che annuncia i risultati della ricerca. Gli assistenti vocali sentono lo stato &quot;risultati aggiornati&quot; dopo ogni ricerca senza spostare lo stato attivo, quindi gli utenti ricevono una chiara conferma del completamento della ricerca. (SITES-24700)
* La finestra di dialogo Selezione link ora viene riavviata a 320 px. Tutti i campi e le azioni rimangono visibili e utilizzabili e la barra di scorrimento orizzontale non viene più visualizzata. (SITES-24709)
* La finestra di dialogo Selezione link ora utilizza la stessa etichetta sia per il testo sullo schermo che per il nome accessibile su ogni elemento della struttura. Gli assistenti vocali annunciano ogni elemento mentre si spostano con i tasti freccia, incluso l’ultimo livello, eliminando i nodi silenziosi e i nomi non corrispondenti. (SITES-24710)
* Modifica I filtri ora segnalano il loro stato come espanso o compresso. Il pulsante attiva `aria-expanded` in sincronia con il pannello dei filtri ed espone un singolo nome non crittografato (&quot;Cambia filtri&quot;), rimuovendo la confusione &quot;filtro?&quot; annuncio. Gli utenti che usano un’utilità di lettura dello schermo possono prevedere il risultato dell’attivazione del controllo. (SITES-24713)
* Le intestazioni modali non coprono più il contenuto con una larghezza di 320 px. L’intestazione viene rilasciata dal suo stato permanente e il corpo della finestra di dialogo scorre, in modo che tutti i campi e i pulsanti di azione rimangano visibili e utilizzabili. Gli utenti che utilizzano la tastiera possono raggiungere tutti i controlli senza perdere la messa a fuoco. (SITES-24718)
* I collegamenti di navigazione nelle app ora espongono la semantica dei collegamenti corretta. Gli assistenti vocali annunciano ogni elemento come collegamento anziché come voce di elenco, migliorando la navigazione da tastiera e il controllo vocale. Il contenitore elenco mantiene la semantica degli elenchi, mentre i collegamenti rimangono le destinazioni attivabili. (SITES-24719)
* Lo stato dei risultati ora viene comunicato agli assistenti vocali quando i filtri cambiano. NVDA legge sia il conteggio &quot;X di Y risultati&quot; che il messaggio &quot;nessun risultato&quot;. Lo stato di paging utilizza un’area live che viene aggiornata nella stessa posizione, in modo che gli utenti ricevano la conferma senza spostare lo stato attivo. (SITES-24720)
* Il pulsante di selezione nella finestra di dialogo Carosello ora annuncia un nome singolo e conciso agli assistenti vocali. Il controllo non ripete più sia l’etichetta del gruppo che l’etichetta di input, riducendo la complessità e la confusione per gli utenti NVDA. (SITES-24725)
* L&#39;elenco di ricerca del menu? mostra la semantica corretta. Il contenitore presenta un elenco e ogni risultato rimane un collegamento senza un ruolo in conflitto. NVDA e JAWS annunciano accuratamente i collegamenti e la navigazione rimane coerente. (SITES-24729)
* Adobe ha corretto la finestra a comparsa dei campioni colore in Preferenze utente in modo che NVDA annunciasse il campione in questione, non quello selezionato in precedenza. Gli utenti che utilizzano la tastiera possono ascoltare i nomi accurati dei colori mentre si spostano nell&#39;elenco e confermare la selezione corretta. (SITES-24739)
* NVDA legge ora la descrizione completa nella directory Tree (Struttura). Il pannello dei dettagli espone il testo su più righe come un unico valore e lo collega all’etichetta del campo. Gli utenti che utilizzano la tastiera visualizzano il testo completo quando si passa da un campo di sola lettura all&#39;altro. (SITES-24780)
* La directory della struttura ora annuncia la data Modificata. NVDA legge la data in cui lo stato attivo si sposta nella colonna Modificato. La griglia collega ogni data al nome dell’elemento in modo che gli utenti possano sentire sia il file che il suo ultimo aggiornamento. (SITES-24782)
* La modalità Anteprima ora rispetta le preferenze di spaziatura del testo dell’utente. L’area di lavoro riflette le modifiche apportate a lettere, parole e altezza di riga in tutto il contenuto visualizzato in anteprima. Il testo non rimane fisso o le clip mentre la spaziatura aumenta. Gli utenti che utilizzano la tastiera o ipovedenti leggono i contenuti senza interruzioni di layout. (SITES-24936)
* AEM corregge l’ordine di tabulazione nelle pagine dell’editor di Assets. La tabulazione ora si sposta dai controlli dell&#39;intestazione ai pulsanti dell&#39;hub di contatto e infine negli strumenti dell&#39;area di lavoro in una sequenza chiara. Le utilità per la lettura dello schermo seguono lo stesso ordine, eliminando confusione e velocizzando la navigazione da tastiera. (SITES-24937)
* AEM aggiunge un nome programmatico alla barra dei menu Azioni scheda. Gli assistenti vocali annunciano correttamente il controllo e gli utenti che utilizzano il riconoscimento vocale possono impostarlo come destinazione per nome. La navigazione da tastiera e lo stato attivo rimangono invariati. (SITES-24938)
* I menu Vista a schede rispettano la spaziatura del testo aumentata. L&#39;elemento Altre azioni cresce e non tronca più le etichette, inclusa la Pubblicazione rapida. Gli utenti che sollevano lettere, parole o interlinea mantengono le etichette complete e l&#39;accesso da tastiera. (SITES-24941)
* È stato rimosso il ruolo &quot;presentazione&quot; che nascondeva la tabella della home page di Sites dalla struttura Accesso facilitato. La tabella viene di nuovo letta correttamente. NVDA e JAWS rilevano la tabella, riconoscono le intestazioni e annunciano le relazioni tra le intestazioni durante la navigazione tra righe e colonne. (SITES-24942)
* L’ordinamento del feedback nella Vista a elenco è esplicito e coerente. Dopo un ordinamento, l&#39;intestazione espone l&#39;ordine tramite `aria-sort`. La modifica viene annunciata, mentre le intestazioni non ordinate non rivendicano più uno stato, consentendo agli utenti di utilità di lettura dello schermo di tenere traccia della colonna che controlla l’ordinamento. (SITES-24943)
* L&#39;intestazione Modifica layout non espone più un pulsante **Modifica** non funzionante. Il controllo ora funziona come un&#39;etichetta di stato statica e rimane fuori dall&#39;ordine di tabulazione, pertanto gli utenti che utilizzano la tastiera non sprecano una sequenza di tasti. Utilizza **Seleziona un&#39;altra modalità** per modificare le modalità, con un feedback chiaro dell&#39;assistente vocale. (SITES-24950)
* La barra degli strumenti dell’emulatore mostra i nomi completi dei dispositivi per impostazione predefinita. L&#39;etichetta non troncerà più al caricamento, consentendo agli utenti di leggere e selezionare i dispositivi senza indovinare. Il testo viene ridimensionato in base ai livelli di zoom e alle larghezze ridotte. (SITES-24952)
* La barra degli strumenti dell’emulatore è adatta ai riquadri di visualizzazione di piccole dimensioni. Con 320 pixel, l’elenco dei dispositivi e controlla lo schermo senza clipping, consentendo agli utenti di selezionare Galaxy S7 e i modelli più recenti. Il layout si adatta e si avvolge per evitare lo scorrimento orizzontale anche con uno zoom del 400%. (SITES-24953)
* Gli assistenti vocali annunciano il dispositivo selezionato e le relative misurazioni nell’emulatore. NVDA interrompe la lettura del flusso del righello; il pulsante dispositivo utilizza una descrizione allegata per il testo della descrizione comando, che riduce il rumore e guida la navigazione. (SITES-24955)
* La barra dei filtri ora tratta ogni tag selezionato come un pulsante di azione. Cancellare i nomi accessibili e la gestione dello stato attivo migliorano gli annunci e il controllo da tastiera. (SITES-24980)
* Gli aggiornamenti di stato nella vista filtro Amministrazione siti annunciano agli assistenti vocali. Quando gli utenti cambiano scheda/elenco durante il caricamento degli elementi, NVDA visualizza ora il messaggio &quot;Attendi&quot; attraverso un’area live. Questa guida impedisce clic aggiuntivi e confusione. (SITES-24992)
* Lo stato attivo della tastiera ora si sposta in ordine logico quando gli utenti espandono la barra a sinistra. Lo stato di attivazione si sposta direttamente dal pulsante della barra a sinistra al contenuto espanso, eliminando la necessità di tornare indietro o saltare elementi. Questa modifica migliora l’accessibilità per gli utenti che usano utilità di lettura dello schermo e tastiera. (SITES-24998)
* Il feedback dell&#39;assistente vocale per il pulsante **Modifica** ora corrisponde al controllo. L&#39;attivazione del pulsante annuncia l&#39;azione Modifica anziché un messaggio di anteprima, migliorando la chiarezza e riducendo gli errori di input per gli utenti che non utilizzano il mouse. (SITES-25208)
* L’azione di conferma nella finestra di dialogo Teaser viene visualizzata correttamente per gli assistenti vocali. Il controllo riporta il messaggio &quot;Confirm&quot;, non la descrizione dell&#39;icona, fornendo agli utenti di tastiera e utilità di lettura dello schermo indicazioni chiare. (SITES-25223)
* Il pulsante Aiuto ora mostra un nome chiaro e accessibile. Gli assistenti vocali annunciano &quot;Aiuto&quot; invece di una descrizione dettagliata dell’icona. Gli utenti conoscono l’azione e possono trovare assistenza più rapidamente. (SITES-25224)
* La finestra modale Timewarp visualizza un anello di attivazione chiaro sui collegamenti **`Set Date`** e **Esci da Timewarp**. Gli utenti che utilizzano la scheda visualizzano esattamente dove si trova l’elemento attivo ed evitano azioni non intenzionali. L&#39;anello mantiene almeno 3:1 contrasto rispetto allo sfondo. (SITES-25232)
* Gli assistenti vocali ora annunciano con precisione i controlli Annota e Chiudi annotazione nella barra degli strumenti Annotazione. NVDA non dice più &quot;Anteprima pulsante premuto&quot;, che fuorviava gli autori e suggeriva l&#39;azione sbagliata. L’annuncio corrisponde al pulsante premuto e mantiene il flusso di lavoro pulito. (SITES-25234)
* La navigazione tramite tastiera nella barra degli strumenti delle annotazioni si comporta in modo coerente. Lo stato attivo non passa più a Esci all’apertura della modalità, ma si sposta sul controllo iniziale per l’aggiunta di annotazioni. Gli utenti possono spostarsi tra i controlli in sequenza senza passare da una scheda all&#39;altra. (SITES-25241)
* La visualizzazione su piccolo schermo funziona come previsto nella finestra modale Teaser. La finestra di dialogo non crea più una barra di scorrimento orizzontale a 320 px e la barra degli strumenti rimane accessibile senza eseguire la panoramica lateralmente. Questo aggiornamento consente agli utenti ipovedenti di ingrandire la pagina. (SITES-25242)
* La visualizzazione su piccolo schermo funziona come previsto nella finestra modale Immagine. La finestra di dialogo non crea più una barra di scorrimento orizzontale a 320 px e gli strumenti immagine rimangono accessibili senza effettuare lo scorrimento laterale. Questo aggiornamento migliora la navigazione per gli utenti ipovedenti che ingrandiscono la pagina. (SITES-25244)
* La finestra modale di ricerca rispetta le impostazioni di spaziatura del testo dell’utente. L&#39;aumento dell&#39;altezza delle righe, della spaziatura tra paragrafi, della spaziatura tra lettere o della spaziatura tra parole non taglia più il testo o si sovrappone all&#39;albero. Il contenuto viene ridistribuito ai valori WCAG 1.4.12 e rimane completamente leggibile. (SITES-25245)
* Il modale di ricerca ora si adatta a schermate piccole senza sovrapporsi alla directory della struttura a 320 px. Il contenuto rifluisce all&#39;interno della finestra di dialogo, mantiene solo lo scorrimento verticale e mantiene visibili i controlli. Questa correzione migliora la leggibilità e la navigazione da tastiera, allineandosi al riflusso WCAG. (SITES-25246)
* L’overflow modale del carosello non forza più lo scorrimento orizzontale a larghezze telefoniche. Il componente si adatta a 320 px, mantiene il flusso verticale e mantiene visibili i controlli. La modifica migliora la leggibilità e l’accesso da tastiera durante l’authoring. (SITES-25254)
* I flussi di lavoro per le annotazioni non perdono più lo stato attivo. La finestra modale pone lo stato attivo iniziale su un’intestazione significativa, impedisce che lo stato attivo salti al di fuori della finestra di dialogo e ripristina lo stato attivo sul trigger dopo la rimozione. L&#39;output dell&#39;utilità di lettura dello schermo rimane conciso e rilevante. (SITES-25257)
* La finestra di dialogo **Elimina annotazione** ora gestisce correttamente lo stato attivo sulla tastiera. Quando si apre la finestra di dialogo, lo stato attivo viene spostato sul relativo titolo per il contesto dell&#39;utilità di lettura dello schermo e lo stato attivo viene nuovamente attivato sul pulsante **Elimina annotazione** che l&#39;ha avviata. Gli utenti non passano più a controlli non correlati o dietro il modale. (SITES-25258)
* Il Selettore data di Timewarp ora gestisce lo stato attivo correttamente. Premendo `Esc` si torna al pulsante **Selezione data** e scegliendo una data si sposta lo stato attivo sul campo di input collegato. Gli utenti che utilizzano la tastiera e gli assistenti vocali mantengono il contesto e non si spostano dietro il modale. (SITES-25264)
* Gli assistenti vocali annunciano le azioni corrette per i pulsanti **Annota** e **Chiudi annotazione**. NVDA non indica più &quot;Pulsante Anteprima premuto&quot;; annuncia il nome del pulsante in modo che gli utenti sappiano quando la modalità di annotazione inizia o termina. (SITES-25268)
* La finestra modale Annotazione ora mostra un&#39;azione **Invia** deselezionata. Gli autori possono aggiungere un commento e inviarlo con il pulsante di icona a forma di penna o ignorare il modale con `Esc`, senza indovinare il flusso. (SITES-25269)
* La voce Annotation include pulsanti di azione espliciti. La finestra di dialogo espone **Invia** per salvare la nota e **Annulla** per chiuderla, accessibile da tastiera e annunciata dalla tecnologia per l&#39;accessibilità. Gli autori non dovranno più fare affidamento su un clic all&#39;esterno della finestra di dialogo o premendo solo `Esc` per terminare. (SITES-25281)
* La modalità Annotazione ora mantiene lo stato attivo sulla tastiera per la sovrapposizione e la relativa barra degli strumenti. La pagina dietro la sovrapposizione non viene più attivata quando gli autori premono TAB, in modo che gli utenti rimangano orientati e possano navigare nelle annotazioni senza passare al contenuto sottostante. (SITES-25282)
* Il selettore dei dispositivi in Modifica layout funziona come previsto. Quando due opzioni del dispositivo hanno larghezze simili (ad esempio, iPhone 8 Plus accanto a Galaxy 7), il pulsante selezionato mostra una descrizione comando per mostrare l’etichetta completa, mentre entrambi i pulsanti rimangono visibili e accessibili. (SITES-25285)
* Con uno zoom del 200%, Modifica layout non sovrascrive più la pagina. La barra degli strumenti è completamente riprodotta ed espone lo scorrimento orizzontale quando necessario, ripristinando l’accesso ai controlli precedentemente nascosti per gli utenti ipovedenti. (SITES-25288)
* L’ordine delle schede nell’anteprima di layout ora si sposta dalla barra degli strumenti principale direttamente alla barra degli strumenti Demografia. Gli utenti che utilizzano la tastiera o l’assistente vocale possono attraversare i controlli in una sequenza prevedibile invece di passare alla barra degli strumenti secondaria. La modifica è conforme all’ordine del focus WCAG 2.4.3. (SITES-25305)
* Quando si ingrandisce la pagina al 200%, non viene più nascosta parte della barra degli strumenti Demografia. La sezione della barra degli strumenti gestisce l&#39;overflow e fornisce lo scorrimento nella propria area, mantenendo ogni controllo visibile e utilizzabile con un ingrandimento elevato. (SITES-25309)
* Gli input di testo nella barra degli strumenti Demografia ora espongono i nomi accessibili appropriati. Ogni campo include un ID univoco con un’etichetta programmatica, in modo che gli assistenti vocali possano annunciare lo scopo del campo e gli utenti possano navigare in base all’etichetta. L’etichetta visibile è posizionata vicino al controllo per migliorare la leggibilità in condizioni di ipovisione. (SITES-25316)
* Il pulsante Modifica ora annuncia l’azione corretta agli assistenti vocali nella barra degli strumenti secondaria. Quando si attiva questa opzione, viene visualizzato il messaggio &quot;Edit&quot; (Modifica) invece del pulsante &quot;Preview button pressed&quot; (Anteprima) non correlato, eliminando così confusione durante la navigazione da tastiera. (SITES-25320)
* Il cursore del carrello della barra degli strumenti Demografia ora mostra un nome accessibile corretto. Gli assistenti vocali annunciano che il &quot;totale del carrello&quot; e gli strumenti di input vocale possono eseguire il targeting del controllo in base al nome, migliorando la conformità a WCAG 4.1.2 (nome, ruolo, valore). (SITES-25322)
* Il cursore della barra degli strumenti Demografia ora mantiene lo stato attivo quando gli autori modificano il valore con i tasti freccia. Lo stato di attivazione non passa più al pulsante Carrello, pertanto gli utenti che utilizzano la tastiera regolano continuamente il valore e gli assistenti vocali annunciano ogni modifica. (SITES-25324)
* Cerca in Assets ora Ridisponi in modo pulito a 320 px (zoom di circa 400%). La finestra modale mantiene intestazioni, campi e azioni leggibili e non sovrapposti, consentendo agli autori di eseguire ricerche senza scorrimento orizzontale. (SITES-25330)
* Il pannello Assets nell’editor segue una sequenza logica di attivazione. Gli utenti che utilizzano la tastiera possono scorrere le miniature e accedere ai controlli di uscita dal pannello. La modifica rimuove i salti e migliora la conformità a WCAG 2.4.3. (SITES-25360)
* AEM aggiorna i pulsanti **Elenchi** e **Paragrafi** nell&#39;editor Rich Text del modale Teaser per esporne lo stato espanso e compresso. I pulsanti ora attivano `aria-expanded` e annunciano la modifica dello stato agli assistenti vocali. Gli autori ricevono un feedback chiaro ed evitano supposizioni prima di aprire o chiudere i menu di formattazione. (SITES-25365)
* AEM annuncia lo stato di caricamento nel modale Teaser. Il modale ora espone un messaggio di stato live durante il caricamento del contenuto, quindi NVDA e JAWS dicono &quot;Caricamento, attendi&quot;. Gli autori devono ricevere un feedback chiaro ed evitare di interagire con la finestra di dialogo prima che sia pronta. (SITES-25366)
* Migliora la messaggistica di stato nella scheda Risorsa della finestra di dialogo Selezione collegamento. Quando si verifica un errore, il componente inserisce un aggiornamento dello stato leggibile e mantiene stabile lo stato attivo sulla tastiera, consentendo a NVDA/JAWS di informare immediatamente gli utenti. (SITES-25368)
* È stato corretto il comportamento dell’interfaccia utente nel pannello Nota per i riquadri di visualizzazione molto stretti. A 320 px, il controllo title e Add si erano scontrati in precedenza; la barra degli strumenti ora si ridisfa e mantiene una chiara separazione tra gli elementi. Gli autori possono utilizzare i controlli senza perdere informazioni o funzioni. (SITES-25376)
* È stato corretto uno stato di errore residuo nella scheda **Collegamenti e azioni** della finestra di dialogo **Teaser**. Dopo che gli autori hanno abilitato **Call to action** e corretto campi vuoti o non validi, la scheda cancella lo stile e l&#39;icona dell&#39;errore e rimuove `aria-invalid`. Una volta convalidati i campi, gli assistenti vocali non visualizzano più l’errore. (SITES-25527)
* La gestione degli errori nei moduli di amministrazione di Sites ora soddisfa le aspettative di accessibilità. Quando la convalida non riesce, la pagina mostra immediatamente l’errore, sposta lo stato attivo su un target di messaggio utilizzabile ed espone il testo agli assistenti vocali come JAWS. (SITES-27138)
* Ora quando si crea una cartella in Sites viene visualizzato un avviso popup di conferma. JAWS annuncia il messaggio attraverso l&#39;area geografica live, in modo che gli autori ricevano un feedback immediato e accessibile dopo l&#39;azione. (SITES-27141)
* È stato corretto uno spazio vuoto di accessibilità a causa del quale veniva eseguito il rendering delle immagini nelle finestre di dialogo di creazione senza testo alternativo. La finestra di dialogo ora fornisce testo alternativo descrittivo dove necessario e alt vuoto per gli elementi puramente visivi, ripristinando il comportamento conforme per JAWS e altri assistenti vocali. (SITES-27153)
* È stata migliorata la gestione degli errori nelle finestre di dialogo di creazione. Quando si verifica un errore di configurazione, l’interfaccia utente mostra un testo esplicito e attiva un annuncio screen reader tramite un’area di avviso. Gli autori ricevono un feedback immediato e possono correggere il problema senza perdere contesto. (SITES-27155)
* È stato corretto un difetto di accessibilità del riversamento in Amministrazione siti. Con uno zoom del browser del 400%, i controlli della barra degli strumenti e della griglia si sovrapponevano e spingevano le azioni dei tasti fuori dallo schermo, bloccando la navigazione da tastiera e l&#39;uso di utilità per la lettura dello schermo. Il layout ora si riavvia correttamente in modo che i pulsanti di ricerca, filtro e azione rimangano visibili e utilizzabili con uno zoom del 400%. (SITES-27238)
* È stato corretto un contrasto basso nel messaggio di stato del blocco visualizzato nel flusso di lavoro Blocca/Sblocca pagina. Il messaggio ora soddisfa una proporzione di 4,5:1, migliorando la leggibilità e la conformità ADA per gli autori. (SITES-27270)
* Sono stati aggiunti nomi accessibili alle icone dei segni di spunta nella finestra di dialogo **Autorizzazioni effettive**. JAWS ora annuncia le icone e il loro significato, migliorando la navigazione da tastiera e la conformità ADA. (SITES-27272)
* La navigazione nascosta nelle intestazioni accettava lo stato attivo e confondeva sia gli utenti vedenti che quelli che leggevano gli schermi. L&#39;aggiornamento disattiva lo stato attivo sui controlli compressi ed espone solo gli elementi visibili. La navigazione rimane prevedibile e soddisfa le linee guida WCAG 2.4.3. (SITES-35224)

* Sono state corrette le icone delle miniature delle cartelle in Sites Admin in modo che si comportassero come immagini decorative. L’aggiornamento rimuove il ruolo immagine e applica il testo alternativo vuoto, pertanto la tecnologia per l’accessibilità ignora le icone e legge solo etichette significative. (SITES-2852)
* Adobe ha aumentato il contrasto cromatico per il testo Riferimenti nella home page di Sites. Il testo ora soddisfa le linee guida WCAG 2.1 AA con un rapporto di almeno 4,5:1 e legge chiaramente i temi luminosi e gli schermi luminosi. (SITES-24755)
* Il punto di riferimento della barra laterale Riferimenti ora annuncia il suo nome agli assistenti vocali. La regione espone un `aria-label` univoco (&quot;Barra dei riferimenti&quot;), che migliora la navigazione dei punti di riferimento e la distingue da altre regioni. (SITES-24973)
* L’Editor Rich Text descrizione bloccava la navigazione in avanti nella scheda e interrompeva il flusso della finestra di dialogo. La correzione ripristina lo spostamento standard della tastiera. Gli autori continuano oltre il campo con una singola scheda e mantengono l’ordine di selezione prevedibile. (SITES-35228)
* Ai controlli di authoring mancavano nomi accessibili e testo dell&#39;icona non elaborato esposto, il che confondeva JAWS. La correzione aggiunge etichette ARIA esplicite e ruoli standard. Gli annunci sembrano corretti e in linea con le aspettative di accessibilità. (SITES-35227)
* L&#39;elenco a discesa Categorie mancava di un&#39;etichetta specifica, quindi JAWS ha pronunciato un generico &quot;menu del pulsante immagini&quot;. L&#39;aggiornamento assegna al controllo il nome &quot;Categories&quot; e ne definisce il ruolo. Gli utenti che usano un’utilità di lettura dello schermo sentono un’etichetta accurata e comprendono le scelte disponibili. (SITES-35226)
* Nella finestra di dialogo Proprietà è visualizzata una griglia dati che consente di trattare i lettori di schermo come testo normale. JAWS e NVDA non sono state attivate e non sono state annunciate righe e colonne. La correzione aggiunge semantiche di tabella reali e ruoli ARIA. Gli assistenti vocali ora riconoscono correttamente la tabella e tengono traccia dello stato attivo. (SITES-35225)
* L’editor di testo per frammenti di contenuto è caricato con una barra delle azioni troncata. Le icone sono state ritagliate e il menu di overflow è diventato irraggiungibile. L’aggiornamento corregge il layout in modo che la barra degli strumenti completa rimanga visibile e accessibile. (SITES-33005)
* I campi modulo scheda Base non hanno mostrato un testo di errore utile. Il modulo ora visualizza messaggi chiari e in linea e li collega al campo per gli assistenti vocali. Gli utenti che utilizzano la tastiera o la tecnologia per l’accessibilità ricevono indicazioni immediate per correggere l’input. (SITES-32480)
* Il campo multiplo utilizzato in un componente personalizzato mostrava pulsanti di icona senza etichetta e un ordine di tabulazione incoerente. JAWS/NVDA ha annunciato solo il &quot;pulsante&quot; o saltato i controlli, che hanno bloccato il funzionamento della tastiera. L&#39;aggiornamento fornisce nomi descrittivi per Aggiungi, Rimuovi e Sposta, normalizza le tabulazioni e annuncia aggiornamenti dell&#39;elenco per soddisfare le aspettative ADA. (SITES-30660)
* La pubblicazione rapida ora restituisce una notifica di successo chiara. La finestra di dialogo si chiude, un avviso popup conferma l’azione e gli assistenti vocali annunciano il messaggio in modo che gli autori non perdano il risultato. (SITES-26912)
* Nessuna modifica richiesta. Adobe ha rivisto l’affermazione secondo cui l’icona di ricerca si sovrappone al testo adiacente. L’intestazione includeva un’etichetta aggiunta dal cliente; vanilla AEM esegue il rendering solo dell’icona. Un’istanza pulita mostra il layout corretto con uno zoom del 100%, pertanto il bug è stato chiuso perché non rientrato nell’ambito. (SITES-26910)
* I temi Crea pagina non nascondono più lo stato attivo. Gli stili Acquatico e Deserto evidenziano in modo coerente la scheda **Base** e le schede adiacenti durante la navigazione da tastiera. Questa modifica ripristina un feedback del focus prevedibile e percepibile per gli utenti ipovedenti. (SITES-26907)



#### Interfaccia utente amministratore{#sites-adminui-6524}

Gli utenti di utilità di lettura dello schermo non hanno ricevuto alcun aiuto di navigazione nella griglia **Blueprint del catalogo**. JAWS ha solo annunciato la posizione della cellula e poi è rimasto in silenzio. Il rilascio aggiunge indicazioni e ruoli accessibili, consentendo a JAWS di leggere il contesto dell’elenco, l’elemento selezionato e i controlli freccia/spazio richiesti. (SITES-30661)

#### Interfaccia classica{#sites-classicui-6524}

Le caselle di controllo dell’interfaccia classica hanno perso le etichette e hanno mostrato opzioni vuote. Nelle finestre di dialogo sono inoltre visualizzati HTML codificati come `<br>`. L&#39;aggiornamento ripristina le etichette delle caselle di controllo e decodifica il markup, in modo che le finestre di dialogo vengano lette correttamente. (SITES-31822)

<!--
#### [!DNL Content Fragments]{#sites-contentfragments-6524}
-->

#### [!DNL Content Fragments] - Amministratore{#sites-admin-6524}

A causa delle parentesi in un nome di frammento di contenuto, il pannello Riferimenti non riportava correttamente l’utilizzo. Gli autori hanno visualizzato 0 anche quando altri frammenti vi facevano riferimento. La correzione corregge l&#39;analisi del percorso per &quot;(&quot; e &quot;)&quot; e fa emergere il conteggio e le voci corretti diversi da zero. (SITES-35078)


#### [!DNL Content Fragments] - Editor frammenti{#sites-fragments-editor-6524}

* Annullamento della pubblicazione non riuscito per i frammenti di contenuto il cui percorso DAM conteneva parentesi. La procedura guidata Gestisci pubblicazione ha riscritto &quot;(&quot; e &quot;)&quot; ed ha interrotto il percorso della risorsa. La correzione mantiene i caratteri e risolve l’elemento corretto, pertanto l’azione di annullamento della pubblicazione viene completata. (SITES-35077)
* Quando si modifica un frammento di contenuto e si torna all’elenco Assets, il frammento o l’intera cartella sono nascosti. Impossibile aggiornare l’elenco dopo la chiusura dell’editor. La correzione ora aggiorna l’elenco in modo affidabile e mantiene visibile il frammento modificato senza un ricaricamento rigido. (SITES-35374)

* L’editor dei frammenti di contenuto non è riuscito ad aprire il selettore di risorse Polaris perché gli ambiti IMS richiesti sono stati rimossi. La correzione ripristina gli ambiti minimi e ristabilisce la connessione Delivery. La navigazione e la selezione delle risorse funzionano di nuovo, senza errori HTTP 500. (SITES-35837)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6524}

Dopo ogni distribuzione, le query GraphQL valide hanno iniziato a restituire `GraphQL_QueryValidationError`. L’endpoint ha mantenuto uno schema non aggiornato fino al riavvio o allo svuotamento delle cache da parte dei team. La correzione aggiorna lo schema GraphQL e il registro delle query persistenti durante la distribuzione, ripristinando immediatamente le risposte normali. (SITES-34301)

<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6524}


#### [!DNL Content Fragments] - REST API{#sites-restapi-6524}


#### Component Console{#sites-component-console-6524}


#### Core Backend{#sites-core-backend-6524}


#### Core Components{#sites-core-components-6524}


#### Campaign integration{#sites-campaign-integration-6524}
-->


#### ContentHub {#sites-contenthub-6524}

ContextHub non inserisce più una seconda copia jQuery nelle pagine pubblicate. La libreria client del motore di segmenti rilascia la dipendenza cq.shared che ha estratto jQuery 1.12.4, quindi i siti caricano un jQuery coerente e il codice front-end funziona in modo affidabile. (SITES-30404)

#### Frammenti di esperienza{#sites-experiencefragments-6524}

* Frammenti esperienza ora localizza l’avviso visualizzato quando non esiste alcuna configurazione di Adobe Target. Il messaggio viene visualizzato nella lingua dell’autore invece che in inglese, pertanto i passaggi di esportazione e attivazione vengono letti correttamente per i team globali. (SITES-11868)
* Quando si pubblica una variante del frammento di esperienza, ora viene visualizzato un messaggio di errore localizzato quando nessun servizio cloud si collega alla variante. Il messaggio viene visualizzato nell’interfaccia utente nella lingua dell’utente anziché in una stringa in sola inglese. (SITES-20293)
* Si è verificato un arresto anomalo durante l&#39;esportazione di un frammento di esperienza in Target con `Attempt to modify attribute at illegal index: -1`. La strumentazione Web Vitals è in conflitto con l&#39;utilità di esportazione e la gestione degli attributi è danneggiata. La correzione rafforza l’elaborazione degli attributi e rimuove tale conflitto. Le esportazioni hanno esito positivo e il frammento viene riprodotto in Target. (SITES-31891)

* Le proprietà dei frammenti esperienza ora localizzano la scheda **Riferimenti**. Etichette e intestazioni di colonna come &quot;Pagina&quot;, &quot;Percorso pagina&quot; e &quot;Titolo variante&quot; vengono visualizzate nella lingua dell’autore. Questa modifica rimuove le stringhe solo in inglese e mantiene la visualizzazione delle proprietà coerente per i team globali. (SITES-11203)
* Il **Varianti** > **Crea flusso di lavoro** mostra ora il testo di traduzione completo. La finestra di dialogo gestisce le stringhe internazionali lunghe racchiudendo e ridimensionando correttamente il contenuto, eliminando le etichette ritagliate o tagliate. (SITES-19304)
* Le proprietà dei frammenti esperienza ora localizzano le etichette di stato dei social media. Gli autori visualizzano i valori di stato, ad esempio Pubblicato e Non pubblicato, nella lingua selezionata in tutte le lingue. Questa modifica rimuove le stringhe solo in inglese che hanno causato confusione durante la revisione. (SITES-20014)

<!--
#### Foundation Components (Legacy){#sites-foundation-components-legacy-6524}
-->

#### Lanci{#sites-launches-6524}

* L’eliminazione di un lancio di grandi dimensioni ha bloccato l’archivio. Il processo ha messo in coda troppe rimozioni e ha ridotto alla fame altre richieste. La correzione ora batch l’eliminazione e restituisce tra i blocchi, quindi la pulizia viene completata mentre il sistema resta reattivo. (SITES-32004)

* Launch Configuration (Configurazione avvio) > Properties (Proprietà) mostra i menu a discesa Company (Società) e Property (Proprietà) funzionanti. **Salva** e **Chiudi** rispetta i campi completati e la convalida del titolo non attiva più errori nella società o nella proprietà. (CQ-4359853)
* Controlli richiesti nella configurazione IMS eseguiti all’aggiornamento, non solo alla creazione. I valori vuoti in campi come ID client o Segreto client mostrano un errore e interrompono il salvataggio fino a quando non viene immesso un valore valido, impedendo il riutilizzo del valore precedente. (CQ-4359938)
* La creazione di un lancio mostra le stringhe di errore e di convalida tradotte. I messaggi in lingua inglese per gli errori di creazione e le pagine sorgente mancanti non vengono più visualizzati. Gli autori visualizzano un feedback chiaro e corretto per le impostazioni internazionali durante la configurazione di Launch. (SITES-13085)
* La promozione di Launch aggiorna le proprietà di pagina `jcr:title`, `jcr:description` e `cq:redirectTarget` nella pagina sorgente. La modifica rimuove le esclusioni di proprietà nella configurazione e nella logica del flusso di lavoro di rollout MSM. Campagne, traduzioni e SEO mantengono titoli, descrizioni e reindirizzamenti coerenti. (SITES-34509)
* L’azione Launch ha ignorato l’ambito e ha incluso pagine che condividevano lo stesso elemento principale della sezione di destinazione. L’aggiornamento applica i limiti della sottostruttura e promuove solo la pagina scelta e i suoi discendenti. Le pagine non correlate mantengono il contenuto esistente. (SITES-34344)
* È stato corretto l’innalzamento automatico nidificato di Launch che si interrompeva in corrispondenza dell’istanza di authoring e saltava il livello di pubblicazione. La promozione automatica di un lancio figlio pubblica le pagine aggiornate agli editori configurati e completa il lancio completo come pianificato. (SITES-30420)

<!--
#### Link Checker{#sites-link-checker-6524}
-->

#### MSM - Live Copy{#sites-msm-live-copies-6524}

* Un rollout a livello di cartella non è riuscito a creare Live Copy per i frammenti di esperienza in tale cartella. I singoli rollout hanno funzionato, interrompendo i flussi di lavoro in blocco. La modifica allinea il rollout della cartella al comportamento della pagina e propaga le relazioni e i riferimenti nella sottostruttura. (SITES-35161)
* Dopo aver eliminato un componente in una Live Copy, **Abilita ereditarietà** si è interrotto con un errore JavaScript e il componente è rimasto mancante fino a un secondo tentativo. L’aggiornamento corregge il ricaricamento post-eliminato in modo da mantenere i parametri corretti e sostituisce la chiamata di avviso obsoleta. La finestra di dialogo si apre correttamente e l’ereditarietà viene ripristinata al primo tentativo. (SITES-31387)
* Rollout guidato ha accettato **Più tardi** senza data. Gli autori hanno avanzato e creato un rollout senza una pianificazione. L’aggiornamento applica la selezione della data e visualizza un prompt di cancellazione. L&#39;azione **Continua** rimane disabilitata fino a quando non esiste una data. (SITES-31374)


#### Editor pagina{#sites-pageeditor-6524}

* L’apertura della struttura del contenuto in una pagina con un contenitore Personalization ha restituito un pannello vuoto e un errore di riferimento null della console. Gli autori non potevano scegliere o configurare i componenti. L’aggiornamento rimuove l’errore e riabilita le interazioni struttura e componente. (SITES-34336)
* AEM 6.5 SP23: cambio di modalità non riuscito nell’Editor pagina. Facendo clic su **Layout**, **Sviluppatore** o **Targeting**, l&#39;editor si è bloccato in modalità **Modifica** ed è stata generata una console `TypeError`. L’aggiornamento ripristina le modifiche alla modalità della barra degli strumenti e cancella l’errore. (SITES-34536)
* L’Editor pagina si allontanava dal punto di inserimento quando gli autori aggiungevano componenti in contenitori lunghi. L&#39;aggiornamento regola i tempi di sovrapposizione e la gestione dello scorrimento. La vista mantiene il suo posto e il nuovo componente rimane in vista e pronto per la configurazione. (SITES-32621)
* Etichette tag personalizzate non riuscite nell’Editor pagina e nell’interfaccia utente veniva sempre visualizzato &quot;Tag&quot;. Il predicato ora valuta `fieldLabel` prima e `labelText` secondo, quindi applica il valore predefinito. Gli autori visualizzano l’etichetta che hanno impostato. (SITES-32278)
* Annullamento del filtro Posizione in Sites: l’icona OmniSearch non è allineata correttamente e si sovrappone al testo segnaposto. L&#39;icona diventò incliccabile. La correzione riallinea l’icona e ripristina l’area hit, pertanto sia il mouse che la tastiera attivano la ricerca. (SITES-30946)
* La scelta di Sviluppatore ha lasciato la pagina in uno stato errato e ha bloccato l’authoring su tale pagina. Il pannello scomparve e l’interfaccia utente non rispondeva più. L’aggiornamento ripristina la logica di attivazione/disattivazione della modalità e la gestione della cache, mantenendo la pagina modificabile e mostrando immediatamente i dati per sviluppatori. (SITES-30922)
* Facendo clic su **Cancella** in **Inserisci nuovo componente** non è stata rimossa la query di ricerca e l&#39;elenco è stato filtrato su un singolo elemento (Pannello a soffietto). La correzione reimposta la query e aggiorna l’elenco. Tutti i componenti consentiti vengono visualizzati di nuovo. (SITES-30921)

<!--
#### Replication{#sites-replication-6524}
-->

#### Editor Rich Text{#sites-rte-6524}

* A schermo intero, l’editor Rich Text nascondeva il risultato del controllo ortografico dietro la finestra di dialogo quando non esistevano errori. L’aggiornamento porta in primo piano il pannello dei risultati e mantiene visibili messaggi e suggerimenti. Gli autori possono rivedere e accettare le correzioni senza uscire dalla modalità a schermo intero. (SITES-32366)
* Le immagini dell’editor Rich Text ora rispettano l’allineamento selezionato. Gli autori impostano a sinistra, al centro o a destra nella finestra di dialogo dell’immagine e l’editor applica tale scelta in modo coerente nell’output. La modifica stabilizza anche la finestra di dialogo Testo alt, in modo che il testo alt e l’allineamento vengano salvati e mantenuti in tutte le modifiche successive. (SITES-30634)

#### Editor universale {#sites-universal-editor-6524}

La configurazione del gestore di autenticazione del token di query ha confuso gli utenti perché le etichette non corrispondevano ai campi. L’interfaccia utente ha estratto del testo dal percorso e ha visualizzato nomi errati. La correzione ripristina etichette chiare e precise per le opzioni di classificazione del servizio e token di query. (SITES-31305)


### [!DNL Assets]{#assets-6524}


#### [!DNL Dynamic Media]{#assets-dm-6524}

* L&#39;opzione **Seleziona miniatura** per i video ora si comporta correttamente in AEM Assets - Dynamic Media. Il clic apre la finestra di dialogo e consente di selezionare una miniatura da Assets, eliminando il precedente comportamento di clic inattivo e rimuovendo il limite all’estrazione dei soli fotogrammi video. (ASSETS-58926)


### [!DNL Forms]{#forms-6524}

<!--
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, December 4, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

#### Forms Designer

* Gli utenti hanno riscontrato problemi a causa dei quali non era possibile fare clic sui collegamenti ipertestuali in casi di test specifici, compromettendo la possibilità di spostarsi e verificare i collegamenti all’interno dell’applicazione. (LC-3923505)
* Gli utenti hanno riscontrato problemi di accessibilità con i PDF generati con AEM Forms Designer 6.5.23 per lingue non latine. I tag percorso non venivano inseriti all’interno di un contenitore Artefatto, causando errori nei controlli di PAC e utilità per la lettura dello schermo. (LC-3923295)
* Dopo l’applicazione della patch dalla versione 6.5.21 al 6.5.23 con il servizio di output, nelle caselle di testo Portable Document Format (PDF) sono stati rilevati collegamenti ipertestuali interrotti. (LC-3923290)
* Si sono verificati problemi di accessibilità con i moduli DoR (Document of Record). Quando i campi di input erano vuoti, gli assistenti vocali leggevano solo i sottotitoli dei campi e non i valori, rendendo difficile agli utenti con disabilità navigare nei moduli in modo efficace. (LC-3923234)
* Gli utenti hanno riscontrato problemi di accessibilità in DoR PDF forms, dove NVDA non legge correttamente &quot;non disponibile&quot; per caselle di controllo, pulsanti di scelta e campi di testo, spesso ripetendo il messaggio e creando confusione per gli utenti di utilità per la lettura dello schermo. (LC-3923201)
* Durante l’aggiunta di nuovi campi, gli utenti hanno riscontrato una discrepanza nell’ordine di tabulazione nell’XDP. L&#39;ordine di tabulazione esistente è stato modificato in modo imprevisto, influendo sulla navigazione del modulo. (LC-3923183, LC-3922630)
* Gli utenti hanno riscontrato problemi con il rendering di HTML. L&#39;evento `docReady` non è stato attivato correttamente in HTML, causando la mancata esecuzione degli script come previsto. (LC-3923118)
* Gli utenti hanno riscontrato problemi con gli script di rendering di PDF che non funzionano nell’ambiente di produzione AEM Forms Cloud. (LC-3923082 )
* Gli utenti hanno riscontrato problemi con i campi mobili nei moduli. Quando si utilizzano file di dati diversi, i campi mobili vengono riprodotti correttamente con un file ma non con l’altro, nonostante differenze minori non correlate ai campi. (LC-3923056)
* Gli utenti visualizzavano una pagina master spagnola vuota quando in un pacchetto di dati XML (XDP) con più pagine master era selezionato solo il contenuto inglese. (LC-3923009)
* Gli utenti hanno osservato informazioni obsolete sull’anno del copyright in AEM Designer. Ciò si verificava nella casella pop-up all’avvio, nella sezione &quot;Informazioni su&quot; e nella sezione &quot;Note legali&quot;, visualizzando &quot;2003-2024&quot; invece di &quot;2003-2025&quot;. (LC-3923005)
* Gli utenti hanno rilevato una pagina PDF vuota durante l’utilizzo dell’impaginazione in AEM Forms Designer. Il problema si verificava selezionando &quot;Top of the Next Page/Top of Page&quot; (Inizio pagina/inizio pagina successiva) per WireAdviceHeader, interrompendo il layout delle iterazioni di dati. (LC-3922997, LC-3922830)
* Gli utenti hanno riscontrato un problema che impediva la persistenza del valore filedigest per la definizione dello schema XSD (Extensible Markup Language) nella versione a 64 bit di AEM Forms Designer. (LC-3922924)
* In AEM Designer 6.5.19, gli utenti hanno sperimentato una formattazione instabile dei collegamenti ipertestuali, in cui i collegamenti ipertestuali all’interno di una casella di testo adottavano erroneamente gli stili del testo circostante, ad esempio la formattazione del primo carattere. (LC-3922376)
* Con AEM Forms OSGI v6.5.22, gli utenti hanno riscontrato dei problemi durante il rendering dei moduli HTML tramite il rendering Mobile su MAC. (LC-3923058)
* Gli utenti hanno riscontrato errori di &quot;oggetto percorso senza tag&quot; nei file PDF (Portable Document Format) quando si utilizzano campi con bordi o in background in modelli XDP creati con Designer 6.5.23 e analizzati con PAC 2024. (LC-3923013)
* Si è verificato un errore nel colore di sfondo dell&#39;intestazione &quot;Dati Richiedente&quot; nel componente applicazione portatile (PAC), durante la ricezione del messaggio &quot;oggetto percorso non taggato&quot;. (LC-3922912)
* Gli utenti hanno riscontrato un problema in cui modelli specifici sostituiscono il font desiderato con un font compatto. (LC-3922330)

#### Moduli adattivi

* Opzioni mancanti nell’editor di regole per gli utenti. Quando gli autori scrivevano regole sugli input numerici, le opzioni Query, UTM e Browser non erano disponibili. (FORMS-21660)
* Si sono verificati arresti anomali dell&#39;applicazione durante l&#39;interazione con OdataResponse a causa di un&#39;eccezione Null Pointer. (FORMS-20344)
* Gli utenti hanno riscontrato dei problemi durante la creazione delle regole per mostrare un pannello e impostare lo stato attivo su un elemento al suo interno. La regola setFocus viene eseguita prima dell’aggiornamento della visibilità, causando un errore nell’azione di attivazione. (FORMS-19563)
* In AEM Forms Author gli utenti hanno riscontrato problemi nella selezione dei componenti. Durante la navigazione tra le schede in modalità di modifica, alcuni contenitori sono diventati non selezionabili, impedendo una facile identificazione e interazione. (FORMS-18525)
* Si è verificato un errore &quot;URL non valido&quot; durante il tentativo di annotare risorse in AEM 6.5.22. (NPR-42684)

### Foundation {#foundation-6524}


#### Apache Felix {#foundation-apachefelix-6524}

Il bundle Felix Web Console è stato aggiornato per includere FELIX-6747. Questa patch corregge la gestione delle risposte che in precedenza compromettevano il rendering e l’autenticazione delle pagine nella console web OSGi. La console viene caricata in modo coerente e non genera più voci IllegalStateException nei registri. (NPR-42730)

<!--
#### Campaign{#foundation-campaign-6524}

#### Cloud Services{#foundation-cloudservices-6524}

#### Communities {#foundation-communities-6524}

#### Content distribution{#foundation-content-distribution-6524}

#### CRX {#foundation-crx-6524}
-->

#### Granite{#foundation-granite-6524}

* Le stringhe non elaborate o solo in lingua inglese non vengono più visualizzate nella finestra di dialogo **Rimuovi controllo di accesso**. La finestra di dialogo presenta contenuti completamente localizzati in più lingue supportate per garantire un&#39;accessibilità coerente. (GRANITE-48479)
* L’icona Aiuto ora espone un’etichetta concisa alle tecnologie per l’accessibilità. JAWS legge &quot;Pulsante Aiuto&quot; e non aggiunge più la dicitura &quot;menu&quot; estranea. Questo aggiornamento rende il controllo conforme a WCAG 4.1.2 e semplifica l’utilizzo della tastiera e degli assistenti vocali. (GRANITE-55360)
* Ripristina la factory del motore di script HTL dopo l’eliminazione di un loop di dipendenza nei servizi OSGi. Gli ambienti vengono avviati correttamente, il rendering HTL funziona tra i pod di authoring e gli amministratori non rilevano più errori di avvio o servizi di script mancanti. (GRANITE-58276)

* La casella di ricerca dell&#39;intestazione non sovrappone più l&#39;icona della lente di ingrandimento sul testo segnaposto. Il segnaposto viene visualizzato con una spaziatura corretta e rimane completamente leggibile nei vari browser. (GRANITE-54391)
* Gli autori visualizzano le etichette leggibili nei campi di completamento automatico anziché i valori non elaborati nella finestra di dialogo. L’implementazione mantiene il valore persistente in JCR e migliora la chiarezza per le configurazioni a selezione singola e multipla che originano le opzioni in modo dinamico. (GRANITE-57615)
* La modalità di modifica rimane funzionante quando htmlLibraryManager.debug è impostato su true. La modifica ripristina la risoluzione e il caricamento clientlib corretti, consentendo agli sviluppatori di utilizzare gli strumenti di debug di HTML Library Manager durante l’authoring. (GRANITE-58002)
* La pagina di modifica dell’agente di replica non genera più un errore JavaScript nell’interfaccia classica. La pagina si apre, visualizza tutte le schede e salva le impostazioni dell’agente senza errori della console. (GRANITE-58302)
* È stata corretta l’aggregazione stato-integrità in Panoramica del sistema. La visualizzazione ora si aggiorna dopo l’esecuzione dei singoli controlli e visualizza i conteggi corretti. Gli operatori visualizzano &quot;OK&quot; quando i controlli di sicurezza e manutenzione vengono superati, invece di un banner &quot;2 errori&quot; errato. (GRANITE-61482)
* Interruzione dell&#39;esecuzione di `CodeUpgradeTasks` durante gli aggiornamenti AEM 6.5 LTS (Long Term Support). L’aggiornamento ora procede senza che vengano apportate modifiche o riconfigurazioni all’archivio attivate da attività. Questa correzione riduce il rischio di aggiornamento e impedisce i tempi di inattività evitabili. (GRANITE-61486)
* Nelle finestre di dialogo di creazione, i campi obbligatori ora mostrano un singolo errore di convalida accurato. Il messaggio utilizza l’etichetta propria del campo, se presente, e torna a un prompt generico se non esiste alcuna etichetta. I messaggi duplicati e non corrispondenti nei vari campi non vengono più visualizzati. (GRANITE-59531)
* La finestra di dialogo della procedura guidata di creazione pagina ora riconvalida i campi obbligatori su ogni interazione, incluse le modifiche alle schede e ai campi multipli. Il pulsante **Crea** rimane disattivato fino a quando gli autori non completano tutti gli input richiesti e la procedura guidata visualizza errori in linea per i valori mancanti. (GRANITE-58826)

#### Integrazioni{#foundation-integrations-6524}

La pubblicazione delle attività di AEM Target non ha più esito negativo quando gli autori impostano le date di inizio e di fine. L’integrazione invia marche temporali conformi agli standard che includono il fuso orario, pertanto Target elabora il payload dell’attività e completa la sincronizzazione come previsto. (CQ-4360733)

<!--
#### Jetty{#foundation-jetty-6524}
-->

#### Localizzazione{#foundation-localization-6524}

* La localizzazione in zh-CN rimuove una frase ambigua nello stato di raccolta dei riferimenti visualizzato durante le operazioni delle risorse, ad esempio Sposta. L&#39;interfaccia utente visualizza ora `正在获取对 [[0]] 项的引用`, fornendo un significato preciso e una terminologia coerente. (CQ-4354648)
* La creazione di una raccolta avanzata non traduce più le parole chiave di ricerca salvate all&#39;aggiornamento. Gli autori che immettono termini in inglese noteranno che tali termini vengono mantenuti e la raccolta continuerà a restituire risultati coerenti. (NPR-43158)
* È stato corretto il testo troncato nella descrizione nel pannello Immagine. La descrizione &quot;Visualizza didascalia come nota a comparsa&quot; viene riprodotta completamente in tutte le lingue supportate, migliorando le indicazioni per gli autori non inglesi. (SITES-10490)
* Nella vista a colonne dell’amministrazione dei siti, le etichette localizzate troncate sono in francese e spagnolo. &quot;Ora di fine&quot; e &quot;Ora di disattivazione&quot; sono apparse troncate e non hanno mostrato alcun suggerimento. Adobe ha corretto le traduzioni e ripristinato la descrizione comando al passaggio del mouse, in modo che le etichette vengano lette completamente. (SITES-31318)
* Nella finestra di dialogo **Sposta** in Sites sono presenti chiavi i18n non elaborate anziché etichette leggibili. Elementi come &quot;Pagine di riferimento&quot;, &quot;Creato il&quot;, &quot;Creato da&quot; e &quot;Percorso&quot; sembravano illeggibili. La correzione aggancia la finestra di dialogo ai dizionari corretti e fornisce traduzioni, con un fallback in inglese. (SITES-30881)

<!--
#### Oak {#foundation-oak-6524}
-->

#### Platform{#foundation-platform-6524}

* Gli errori di convalida ora mostrano un testo chiaro e descrittivo invece di una sola icona. Gli assistenti vocali annunciano il messaggio automaticamente quando viene visualizzato, pertanto gli utenti non devono passare a un’icona per scoprire qual è stato il problema. (CQ-4359152)


* Le etichette posizionate al passaggio del mouse nella barra di spostamento non rimangono più sullo schermo dopo che il cursore si sposta fuori dal controllo. L’interfaccia utente nasconde queste descrizioni comandi immediatamente in caso di sfocatura o allontanamento del mouse, impedendo disagi visivi e clic errati. (CQ-4360030)
* In Sites, le azioni della barra degli strumenti interrompono la creazione di un secondo pop-up quando si fanno clic ripetutamente. Il secondo clic chiude il pop-up esistente e lascia visibile una sola istanza, eliminando sovrapposizioni e distrazioni. (CQ-4360038)
* Il testo obsoleto del copyright del 2024 non viene più visualizzato. La pagina di accesso e la **Guida** > **Informazioni sulla finestra a comparsa di AEM** mostrano il 2025 e AEM legge l&#39;anno a livello di programmazione per evitare modifiche manuali. (CQ-4360042)
* Facendo clic su una descrizione comando nella barra dell’intestazione di AEM, l’azione sottostante non viene più attivata. I popup vengono aperti solo quando gli utenti fanno clic sul pulsante effettivo, evitando finestre di dialogo accidentali durante l&#39;interazione con il testo della descrizione. (CQ-4360105)
* Il rollover dell&#39;anno non lascia più il testo del copyright obsoleto. La schermata Login e la finestra di dialogo **Guida** > **Informazioni su AEM** derivano l&#39;anno dall&#39;orologio di sistema ed eseguono il rendering del valore aggiornato ogni volta che l&#39;interfaccia utente viene caricata. (CQ-4360173)
* I pop-up della barra dell’intestazione ora vengono attivati correttamente. Se si fa clic sulla stessa azione, ad esempio **Cerca** o **Filtro**, il popup aperto viene chiuso invece di aprire un&#39;altra sovrapposizione. La modifica impedisce la sovrapposizione dei popup e restituisce lo stato attivo al controllo intestazione. (NPR-42891)
* Viene eseguito correttamente il rendering della vista Progetti e Calendario casella in entrata. Il passaggio da una visualizzazione all’altra non spegne più la pagina; il calendario carica e mostra gli elementi pianificati. (NPR-42968)

<!--
#### Security{#foundation-security-6524}
-->

#### Sling{#foundation-sling-6524}

* È stato corretto un errore di compilazione JSP imprevisto con il bundle `org.apache.sling.scripting.jsp:2.6.0`. (SLING-12442)
* La piattaforma aggiorna il motore Sling di base da 2.16.2 a 2.16.6. Il nuovo motore rafforza la convalida dell’input e stabilizza l’elaborazione delle richieste sotto carico. (NPR-43105)

#### Editor SPA {#foundation-spa-editor-6524}

L&#39;attivazione del servlet principale Sling **Controlla le sostituzioni Content-Type** ha interrotto `.model.json` esportazioni in AEM 6.5 SP21/22. Le richieste hanno restituito HTML o errori perché l’esportatore ha capovolto il tipo mid-chain. La correzione emette JSON con il tipo corretto dall&#39;inizio, quindi `.model.json` funziona negli ambienti di authoring e pubblicazione. (SITES-32634)


#### Traduzione{#foundation-translation-6524}

* È stata aggiunta un’operazione di reindicizzazione per lo stato del progetto di traduzione. Gli amministratori possono ricreare l’indice di backup quando la visualizzazione dello stato non è sincronizzata, ripristinando i risultati ed eliminando gli avvisi di attraversamento di Oak. La pagina viene caricata più velocemente e mostra gli stati del processo correnti. (NPR-42699)
* È stata corretta una regressione a causa della quale le importazioni XLIFF riportavano il successo ma lasciavano invariati i file del dizionario JSON. Le importazioni ora eseguono il targeting del percorso i18n corretto e mantengono le traduzioni in modo che i viaggi di andata e ritorno per la localizzazione siano completati senza modifiche manuali. (NPR-42989)


* L’XML delle regole di traduzione ora funziona come configurato. Il framework di traduzione rispetta le regole di eccezione e si applica correttamente ai modelli `include` e `exclude` durante la creazione di processi. Le richieste di traduzione non inviano più contenuti esclusi. (NPR-42761)



#### Interfaccia utente{#foundation-ui-6524}

* È stata corretta una regressione dell’interfaccia utente che disabilitava gli input nella finestra di dialogo Licenza Adobe Stock. La finestra di dialogo ora funziona normalmente, accetta il testo nei campi obbligatori e completa il flusso di licenze Stock asset dalla vista Dettagli asset. (NPR-42748)

* È stata corretta la visibilità dei gruppi nell’ambiente di authoring. La console Gruppi non si ferma più a circa 41 risultati e restituisce l’intero set di appartenenze per ogni utente. Questa correzione ripristina un comportamento coerente dopo le correzioni cumulative e mantiene l’attuale protezione avanzata. (NPR-42749)


<!--
#### WCM{#foundation-wcm-6524}



#### Workflow{#foundation-workflow-6524}
-->




## Installa [!DNL Experience Manager] 6.5.24.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.24.0 richiede [!DNL Experience Manager] 6.5. Per istruzioni dettagliate, consulta la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md). <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del Service Pack è disponibile in Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.24.0 in una delle istanze di authoring utilizzando Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe consiglia di non rimuovere o disinstallare il pacchetto [!DNL Experience Manager] 6.5.24.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup di `crx-repository` nel caso sia necessario eseguirne il rollback. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installare il Service Pack in [!DNL Experience Manager] 6.5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). Adobe consiglia di riavviare il sistema se il tempo di attività corrente di un’istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il Service Sack da [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.24.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Selezionare il pacchetto, quindi selezionare **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta la finestra di dialogo nell’interfaccia utente di Gestione pacchetti si chiude durante l’installazione del Service Pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di avere la certezza che l’installazione sia andata a buon fine. Questo problema si verifica in genere nel browser [!DNL Safari], ma può verificarsi in modo intermittente in qualsiasi browser.

**Installazione automatica**

Per installare [!DNL Experience Manager] 6.5.24.0 è possibile utilizzare due metodi diversi.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza l&#39;API HTTP [da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` per installare i pacchetti nidificati.

>[!NOTE]
>
>Experience Manager 6.5.24.0 non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l&#39;utilizzo di questa versione, vedere i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.24.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (usa la console Web: `/system/console/bundles`).

1. La versione del bundle OSGi `org.apache.jackrabbit.oak-core` è 1.22.20 o successiva (utilizzare la console Web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installa Service Pack per [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Per istruzioni sull&#39;installazione del Service Pack in Experience Manager Forms, vedere [Istruzioni di installazione del Service Pack di Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funzione Forms adattivo, disponibile in [QuickStart per AEM 6.5](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), è progettata esclusivamente a scopo di esplorazione e valutazione. Per l’utilizzo in produzione, è essenziale ottenere una licenza valida per AEM Forms, in quanto la funzionalità Adaptive Forms richiede una licenza appropriata.

### Installare il pacchetto di indice GraphQL per i frammenti di contenuto Experience Manager{#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare il [Frammento di contenuto Experience Manager con pacchetto indice GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

In questo modo puoi aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate.

Se non si installa questo pacchetto, è possibile che le query GraphQL risultino lente o non riuscite.

>[!NOTE]
>
>Installare il pacchetto una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar{#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.24.0 è disponibile nel [archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.24/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.24</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell&#39;archivio centrale di Maven anziché nell&#39;archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale è stato rinominato in `uber-jar-<version>.jar`. Non esiste alcun `classifier`, con `apis` come valore, per il tag `dependency`.



## Funzioni obsolete e rimosse{#removed-deprecated-features}

Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) per un elenco dettagliato di tutte le funzioni obsolete o rimosse per AEM 6.5.

### Supporto dei frammenti di contenuto nell’API REST di AEM Assets {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 fornisce API OpenAPI moderne per la gestione di modelli e frammenti di contenuto; pertanto, gli endpoint precedenti per il supporto dei frammenti di contenuto nell’API REST di AEM Assets sono ora obsoleti.

Adobe intende mantenere questi endpoint meno recenti disponibili fino a un annuncio sulla fine del ciclo di vita. Adobe non prevede ulteriori miglioramenti per gli endpoint obsoleti.

### Editor di SPA {#spa-editor}

[L&#39;editor SPA](/help/sites-developing/spa-overview.md) è stato dichiarato obsoleto per i nuovi progetti a partire dalla versione 6.5.24 di AEM 6.5. L’editor SPA rimane supportato per i progetti esistenti, ma non deve essere utilizzato per i nuovi progetti.

Gli editor preferiti per la gestione dei contenuti headless in AEM sono ora:

* [Editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.
* [Editor frammenti di contenuto](/help/sites-developing/universal-editor/introduction.md) per la modifica basata su modulo.

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Correlato ad Oak**
Da Service Pack 13 e versioni successive è stato avviato il seguente log degli errori che influisce sulla cache di persistenza:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Oppure

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Per risolvere l&#39;eccezione, eseguire le operazioni seguenti:

   1. Elimina le due cartelle seguenti da `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Installa il Service Pack o riavvia Experience Manager as a Cloud Service.
Le nuove cartelle di `cache` e `diff-cache` vengono create automaticamente e non si verifica più un&#39;eccezione relativa a `mvstore` in `error.log`.

* Aggiorna le query GraphQL che potrebbero aver utilizzato un nome API personalizzato per il modello di contenuto in modo da utilizzare il nome predefinito del modello di contenuto.

* Una query GraphQL può utilizzare l&#39;indice `damAssetLucene` anziché l&#39;indice `fragments`. Questa azione potrebbe causare l’errore o richiedere molto tempo per l’esecuzione delle query GraphQL.

  Per risolvere il problema, è necessario configurare `damAssetLucene` in modo da includere le due proprietà seguenti in `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Dopo aver modificato la definizione dell&#39;indice, è necessario reindicizzare (`reindex` = `true`).

  Dopo questi passaggi, le query GraphQL dovrebbero funzionare più rapidamente.

* Quando si tenta di spostare, eliminare o pubblicare frammenti di contenuto, siti o pagine, si verifica un problema durante il recupero dei riferimenti ai frammenti di contenuto. La query in background non riesce. In altre parole, la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell&#39;indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Se si aggiorna l&#39;istanza di [!DNL Experience Manager] dalla versione 6.5.0 alla versione 6.5.4 al Service Pack più recente in Java™ 11, vengono visualizzate `RRD4JReporter` eccezioni nel file `error.log`. Per interrompere le eccezioni, riavviare l&#39;istanza di [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Gli utenti possono rinominare una cartella in una gerarchia in [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x potrebbero essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l&#39;integrazione Adobe Target è configurata in [!DNL Experience Manager] utilizzando l&#39;API Target Standard (autenticazione IMS), l&#39;esportazione di frammenti di esperienza in Target genera la creazione di tipi di offerta errati. Invece del tipo &quot;Frammento di esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in `granite/operations/maintenance`.
   * La convalida lato server di Moduli adattivi non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nessuna finestra di manutenzione trovata in `granite/operations/maintenance`.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro per l&#39;annullamento della registrazione.

* A partire da AEM 6.5.15, il motore JavaScript Rhino fornito dal bundle ```org.apache.servicemix.bundles.rhino``` ha un nuovo comportamento di posizionamento. Gli script che utilizzano la modalità rigorosa (```use strict;```) devono dichiarare le variabili corrette. In caso contrario, non vengono eseguiti e finiscono per generare un errore di runtime.

* Se si installa il contenuto predefinito correlato ai tag tramite un pacchetto di aggiornamento ufficiale, la proprietà Languages del nodo `/content/cq:tags` viene ripristinata sul valore predefinito. Questa azione è valida per Service Pack, Service Pack di sicurezza, Feature Pack estesi, Feature Pack cumulativi, patch e così via. Pertanto, è necessario aggiungerlo dalle proprietà prima dell’installazione.

### Problema noto per AEM Sites {#known-issues-aem-sites-6524}

Frammenti di contenuto-Anteprima non riuscita a causa della protezione DoS per una grande struttura ad albero di frammenti. Vedi l&#39;articolo [KB sulle opzioni di configurazione predefinite di GraphQL Query Executor](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemi noti per AEM Forms {#known-issues-aem-forms-6524}

* **FORMS-14521** Se un utente tenta di visualizzare in anteprima una bozza di lettera con dati XML salvati, si blocca nello stato `Loading` per alcune lettere specifiche.
* **FORMS-16603** Nell&#39;anteprima di stampa dell&#39;interfaccia utente di Interactive Communications Agent alcuni valori calcolati non vengono visualizzati correttamente.
* **FORMS-15681** Quando la lettera viene visualizzata nell&#39;anteprima di stampa, il contenuto cambia. In altre parole, alcuni spazi scompaiono e alcune lettere vengono sostituite con `x`.
* **FORMS-15428**: dopo l&#39;aggiornamento ad AEM Forms Service Pack 20 (6.5.20.0) con il componente aggiuntivo Forms, le configurazioni basate sul servizio Adobe Analytics Cloud legacy che utilizzano l&#39;autenticazione basata sulle credenziali cessano di funzionare. Questo problema impediva la corretta esecuzione delle regole di analisi.
* **FORMS-16557** Nell&#39;anteprima di stampa dell&#39;interfaccia utente di Interactive Communications Agent, il simbolo di valuta (ad esempio il simbolo del dollaro $) viene visualizzato in modo incoerente per tutti i valori di campo. Viene visualizzato per valori fino a 999 ma non per valori di 1000 e superiori.
* **FORMS-16575** Eventuali modifiche all&#39;XDP dei frammenti di layout nidificati in una comunicazione interattiva non vengono riportate nell&#39;editor IC.
* **FORMS-21378** Quando la convalida lato server (SSV) è abilitata, l&#39;invio del modulo potrebbe non riuscire. Se riscontri questo problema, contatta il supporto Adobe per assistenza.
* **FORMS-23722** (file allegati mancanti in Assegna attività): quando un modulo con un campo **File allegato** che utilizza bindref viene inviato a un flusso di lavoro di AEM che utilizza un passaggio **Assegna attività**, gli allegati non vengono visualizzati quando l&#39;attività viene aperta dalla Posta in arrivo. I file vengono salvati correttamente nell’archivio, ma l’interfaccia utente del passaggio Assegna attività non riesce a visualizzare gli allegati.

#### Problemi relativi agli hotfix disponibili {#aem-forms-issues-with-hotfixes}

<!-- 
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.24.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.24.0 only after the required hotfixes are released. -->

Nei seguenti problemi è disponibile un hotfix per il download e l’installazione. Puoi [scaricare e installare l&#39;Hotfix](/help/release-notes/aem-forms-hotfix.md) per risolvere questi problemi:

<!--* **FORMS-23881** On AEM Forms JEE deployments set up using the 6.5.23.0 full installer, Output Service fails to process requests when a custom XCI file is supplied in the invocation. To resolve this issue, install the latest AEM 6.5.24.0 Forms Service Pack from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) portal.-->

* AEM Forms ora include un aggiornamento della versione Struts da 2.5.33 a 6.x per il componente Forms. Questo aggiornamento consente di apportare le modifiche di avvio precedentemente mancate non incluse in SP24. Il supporto è stato aggiunto tramite un [Hotfix](/help/release-notes/aem-forms-hotfix.md) che puoi scaricare e installare per aggiungere il supporto per la versione più recente di Struts.

* **FORMS-14926** Dopo aver installato AEM Forms JEE Service Pack 21 (6.5.21.0), se trovi voci duplicate dei file JAR Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` nella cartella `<AEM_Forms_Installation>/lib/caching/lib`, effettua le seguenti operazioni per risolvere il problema:

   1. Fermate i localizzatori, se sono in esecuzione.
   2. Arresta il server AEM.
   3. Passare a `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Rimuovere tutti i file patch Geode ad eccezione di `geode-*-1.15.1.2.jar`. Verificare che siano presenti solo i file jar Geode con `version 1.15.1.2`.
   5. Apri il prompt dei comandi in modalità amministratore.
   6. Installare la patch Geode utilizzando il file `geode-*-1.15.1.2.jar`.

* **FORMS-15256** Quando gli utenti sono stati aggiornati da AEM 6.5 Forms Service Pack 18 o 19 al Service Pack 20 o 21, si è verificato un errore di compilazione JSP. Questo errore impediva loro di aprire o creare moduli adattivi. Inoltre, ha causato problemi con altre interfacce AEM. Tali interfacce includevano l’Editor pagina, l’interfaccia utente di AEM Forms, l’Editor flusso di lavoro e l’interfaccia utente Panoramica sistema.

  In caso di problemi di questo tipo, effettua le seguenti operazioni per risolverli:
   1. Passare alla directory `/libs/fd/aemforms/install/` in CRXDE.
   2. Eliminare il bundle con il nome `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Riavvia il server AEM.

* **FORMS-23703** Se la regola `contains` è configurata senza un valore predefinito, la convalida lato server per un modulo adattivo non riesce. È possibile installare la versione più recente di [AEM Forms 6.5.24.0 Service Pack](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases) per risolvere il problema.

* **GRANITE-63681** I connettori del modello dati modulo potrebbero non riuscire ad eseguire l&#39;autenticazione perché le parole chiave e il pattern regex richiesti non sono consentiti per impostazione predefinita. Per risolvere il problema, scarica e installa l&#39;aggiornamento rapido da [link](/help/release-notes/aem-forms-hotfix.md).

  <!--To resolve the issue, add the following via the Configuration Manager (`/system/console/configmgr`):

  * **Keywords:** `fdm-client-secret`, `oauth-client-secret`
  * **Regex:** `^\[/conf/[^/]+(/[^/]+)?/settings/dam/cfm/models/[^,\]]+(?:,/conf/[^/]+(/[^/]+)?/settings/dam/cfm/models/[^,\]]+)*\]$`

    >[!VIDEO](https://video.tv.adobe.com/v/3479697)-->

* **FORMS-23979** la conversione da HTML a PDF (PDFG) potrebbe verificarsi timeout intermittenti. Successivamente è stata rilasciata una versione più recente del componente aggiuntivo Forms per SP24 che include la correzione. Se si verifica questo problema, aggiornare l&#39;ambiente al componente aggiuntivo di Forms [più recente rilasciato per 6.5.24.0](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases).

* **FORMS-23717** Dopo l&#39;aggiornamento a **AEM Forms6.5.24.0**, `server.log` e `error.log` possono essere inondati da messaggi di avvertenza ripetuti, ad esempio *Creazione della factory del parser protetto non riuscita* o *L&#39;attributo di sicurezza ... non è supportato*. I registri possono crescere di circa **5-10 righe al secondo** (centinaia di MB all&#39;ora), che possono riempire il disco e bloccare il rollout di produzione. **Correzione:** inclusa in AEM Forms **6.5.25.0**. **Fino ad allora:**

  Per ridurre il volume del log, impostare il livello di log per `com.adobe.util.XMLSecurityUtil` su `ERROR` nella configurazione del server applicazioni o tramite l&#39;argomento JVM `-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`. Questo nasconde solo i messaggi e non corregge la causa sottostante.

* **FORMS-23875** Nella ricerca del modello dati modulo, un tag HTML viene visualizzato nell&#39;interfaccia utente anche quando non è presente un&#39;entità rilevante. Per risolvere il problema, scaricare e installare l&#39;aggiornamento rapido da [il collegamento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip).

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 Service Pack:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5.24.0](/help/release-notes/assets/65240-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.24.0](/help/release-notes/assets/65240-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/it/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/it/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/it/docs/experience-manager-65)
>* [Iscriviti agli aggiornamenti dei prodotti con priorità Adobe](https://www.adobe.com/subscription/priority-product-update.html)

