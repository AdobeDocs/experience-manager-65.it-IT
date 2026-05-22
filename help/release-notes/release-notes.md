---
title: Note sulla versione per  [!DNL Adobe Experience Manager] 6.5
description: Trova informazioni sulla versione, novità, procedure di installazione e un elenco dettagliato delle modifiche per  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: d60ff7278e62833c732c55d328882a2976bfd964
workflow-type: tm+mt
source-wordcount: '7116'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione del Service Pack |
| Data | 21 maggio 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

<!--
OLD DOWNLOAD URL
(https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)
-->

## Cosa è incluso in [!DNL Experience Manager] 6.5.25.0 {#what-is-included-in-aem-6525}

[!DNL Experience Manager] 6.5.25.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la data di disponibilità iniziale di 6.5 di aprile 2019. [Installa il Service Pack &#x200B;](#install) in [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- ## Key features and enhancements -->


## Problemi risolti in Service Pack 25 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### Accessibilità {#sites-accessibility-6525}

* I controlli di trascinamento della riga della tabella nella vista a elenco Sites ora funzionano con la navigazione da tastiera. Gli utenti che usano un’utilità di lettura dello schermo e una tastiera possono riordinare le righe e ricevere feedback durante l’azione. (SITES-24946)

* La barra degli strumenti Modifica layout presenta ora le etichette per schermi e tablet più piccoli in una sequenza significativa di utilità per la lettura dello schermo. Gli utenti sentono le etichette con le misurazioni del righello correlate invece di sentirle fuori ordine. (SITES-25291)
* La finestra modale a comparsa Campioni ora gestisce correttamente lo stato attivo quando si apre dalla finestra modale Annotazione. Lo stato attivo inizia dall’intestazione modale invece di spostarsi direttamente sul pulsante campione selezionato. (SITES-25275)
* Il modale Teaser ora fornisce un modo accessibile per spostare la finestra di dialogo con una tastiera. Gli utenti non hanno più bisogno di un mouse per riposizionare il modale sulla pagina. (SITES-25226)
* La vista a schede migliora l’accessibilità rimuovendo il comportamento superfluo della griglia ARIA. Gli utenti di utilità di lettura dello schermo ricevono informazioni più chiare sulle schede senza controlli di navigazione della griglia che non corrispondono al layout visivo. (SITES-24933)
* Le descrizioni comandi nella finestra modale Elimina ora vengono visualizzate in modo coerente dopo ripetute azioni al passaggio del mouse. Gli utenti possono spostare il puntatore e tornare all&#39;icona per leggere nuovamente la descrizione. (SITES-24778)
* La barra a sinistra ora viene attivata nell’ordine previsto dopo che gli utenti la aprono dalla home page di Sites. Gli utenti che utilizzano la tastiera e l’assistente vocale possono passare dal pulsante di configurazione al contenuto della barra senza saltare l’area espansa. (SITES-24754)
* La gestione del focus ora funziona in modo coerente nella finestra di dialogo modale Carosello. Gli utenti che utilizzano la tastiera o un assistente vocale possono iniziare dall&#39;intestazione modale e tornare al controllo originale dopo aver chiuso la finestra di dialogo. (SITES-24716)
* La finestra di dialogo Selezione collegamento consente ora di spostare lo stato attivo sul controllo che lo ha aperto dopo che gli utenti hanno chiuso la finestra di dialogo. Gli utenti che utilizzano la tastiera o l’assistente vocale non perdono più il posto che occupano dopo aver chiuso la finestra di dialogo. (SITES-24707)
* La finestra modale Immagine non sposta più lo stato attivo sulla prima scheda o sul punto di riferimento della pagina principale quando gli autori aprono o chiudono la finestra di dialogo. Lo stato attivo si sposta prima sull&#39;intestazione della finestra di dialogo, quindi ritorna al controllo che ha aperto la finestra di dialogo. (SITES-24693)
* La barra dei riferimenti ora gestisce correttamente lo stato attivo quando si apre una finestra di dialogo modale. Gli utenti che utilizzano la tastiera e l&#39;utilità di lettura dello schermo rimangono all&#39;interno della finestra di dialogo fino a quando non la chiudono, quindi proseguono la navigazione senza perdere contesto. (SITES-24683)
* La finestra modale di selezione del percorso del collegamento ipertestuale non sposta più lo stato attivo sul campo o sul controllo errato quando gli autori lo aprono o lo chiudono. Lo stato attivo inizia dall’intestazione modale e torna al pulsante che ha aperto il modale. (SITES-24672)
* La finestra modale Teaser non sposta più lo stato attivo sulla prima scheda o sulla parte superiore della pagina quando gli autori la aprono o la chiudono. Lo stato di attivazione segue ora il flusso previsto della finestra di dialogo e riduce gli annunci non necessari degli assistenti vocali. (SITES-24522)

* Il pulsante di blocco Editor pagina ora fornisce un feedback più preciso sull’utilità di lettura dello schermo. Gli assistenti vocali utilizzano l’attributo title quando disponibile, il che riduce gli annunci dettagliati per gli autori che utilizzano tecnologie per l’accessibilità. (SITES-41431)
* La navigazione tramite tastiera ora ignora il contenuto nascosto. Gli utenti possono spostarsi tra gli elementi visibili dell’interfaccia senza spostare lo stato attivo su contenuti che non possono visualizzare. (SITES-41430)
* Lo stato attivo su tastiera ora ritorna all’elemento attivatore dopo che gli utenti hanno chiuso una sovrapposizione. L’Editor pagina non riporta più lo stato attivo sulla sovrapposizione, migliorando la navigazione per gli utenti che utilizzano la tastiera. (SITES-40819)
* La barra degli strumenti Editor pagina ora visualizza etichette, come le descrizioni comandi, quando gli utenti navigano tra gli elementi della barra degli strumenti utilizzando una tastiera. Gli utenti possono comprendere ogni azione della barra degli strumenti quando lo stato attivo si sposta da un elemento all’altro. (SITES-40751)
* Il passaggio del mouse sugli elementi del browser Componenti non rimuove più lo stato attivo da un componente Testo attivo. Gli autori possono modificare il testo senza interruzioni e lo stato attivo sulla tastiera rimane prevedibile. (SITES-35370)
* Gli assistenti vocali ora annunciano più chiaramente il pulsante Search Modal sort direction (Ricerca modale). L’etichetta del pulsante non ripete più la stessa direzione e descrive meglio il comportamento di attivazione/disattivazione. (SITES-25534)
* Nella casella di riepilogo Cambia file o cartella viene ora visualizzato un indicatore visivo per l&#39;opzione selezionata. Gli utenti possono identificare l’opzione breadcrumb corrente senza affidarsi esclusivamente allo stato attivo. (SITES-25532)
* La finestra modale Ricerca ora aumenta il contrasto per l’etichetta Ordina per. Il testo soddisfa i requisiti di accessibilità e migliora la leggibilità per gli utenti ipovedenti. (SITES-25531)
* I pulsanti di selezione dei dispositivi ora mostrano le informazioni corrette sullo stato corrente nella barra degli strumenti Modifica layout. Gli utenti di utilità di lettura dello schermo possono identificare il dispositivo attivo senza sentire uno stato di attivazione fuorviante. (SITES-25524)
* La navigazione tramite tastiera e utilità di lettura dello schermo ora chiude il menu Posta in arrivo quando lo stato attivo non è più disponibile. Gli utenti evitano lo stato confusionale in cui il menu rimane aperto mentre lo stato attivo si sposta altrove. (SITES-25518)
* La navigazione tramite tastiera e utilità di lettura dello schermo ora chiude il menu della Guida quando lo stato attivo non è più disponibile. Lo stato di attivazione non si sposta più sul contenuto all&#39;esterno del menu mentre quest&#39;ultimo rimane aperto. (SITES-25517)
* La home page Frammenti di contenuto fornisce ora un’etichetta accessibile coerente per le schede della barra laterale. NVDA annuncia correttamente l&#39;etichetta della scheda quando gli utenti passano ai controlli della scheda. (SITES-25509)
* Le opzioni attivate nel menu Informazioni pagina ora soddisfano i requisiti di contrasto minimo. Il contrasto migliorato aiuta gli utenti ipovedenti a identificare la voce di menu attiva. (SITES-25321)
* La navigazione tramite tastiera ora ignora i controlli nascosti nella barra degli strumenti Demografica compressa. Lo stato attivo resta sugli elementi interattivi visibili, che migliorano l’ordine di navigazione nell’anteprima di layout. (SITES-25304)
* Il pulsante Ruota dispositivo ora fornisce un feedback più chiaro sull’utilità di lettura dello schermo nella barra degli strumenti Modifica layout. Gli assistenti vocali annunciano l’orientamento corrente e l’azione che lo modifica. (SITES-25292)
* Sulla barra degli strumenti Modifica layout viene ora visualizzato uno stato deselezionato per il pulsante Desktop. L&#39;opzione Desktop corrisponde agli altri pulsanti del dispositivo e facilita l&#39;identificazione della visualizzazione attiva. (SITES-25290)
* La barra degli strumenti Modifica layout ora etichetta l’area del righello per le tecnologie per l’accessibilità. Gli utenti di utilità di lettura dello schermo non rilevano più valori di misurazione senza etichetta durante la modifica del layout. (SITES-25287)
* Sulla barra degli strumenti Modifica layout l&#39;etichetta completa del pulsante iPhone 8 Plus è ora deselezionata. L’etichetta non viene più troncata quando intorno al pulsante è presente spazio sufficiente. (SITES-25284)
* Il problema segnalato descriveva un indicatore dello stato attivo nella barra degli strumenti Modifica layout che sembrava coprire più controlli dispositivo. Questo problema riguardava gli utenti che utilizzavano la tastiera e che potevano perdere traccia del controllo attivo quando il profilo dello stato attivo includeva pulsanti adiacenti. Il problema funzionava come previsto. (SITES-25283)
* Il problema segnalato descriveva i pulsanti modali per l’annotazione che annunciavano l’annotazione prima di ogni etichetta di pulsante. Il problema si concentrava sull’output non chiaro dell’utilità di lettura dello schermo per azioni quali Annota, Campioni ed Elimina. (SITES-25277)
* Il testo del pulsante Annotazione ora utilizza un contrasto sufficiente nel modale Annotazione. Questo aggiornamento migliora la leggibilità per gli utenti ipovedenti e supporta i requisiti di contrasto WCAG. (SITES-25267)
* Gli assistenti vocali ricevono ora gli aggiornamenti di stato quando gli utenti filtrano l’elenco Inserisci nuovo componente. Il modale annuncia le modifiche dei risultati in modo che gli utenti possano capire che l’elenco è cambiato mentre digitavano. (SITES-25251)
* Il problema registrato descriveva la semantica di intestazione mancante per il titolo modale dell’annotazione. La preoccupazione si è concentrata sulla navigazione degli assistenti vocali e sulla capacità di comprendere la struttura modale. (SITES-25248)
* I livelli di intestazione nella barra laterale dell’Editor pagina ora seguono una gerarchia di contenuti più chiara. La sezione Barra a sinistra non viene più visualizzata come intestazione della pagina principale per le tecnologie per l’accessibilità. (SITES-25222)
* Il pulsante Modifica nella barra a sinistra di Assets ora ha un target touch più grande. Gli utenti con esigenze di mobilità possono attivare il pulsante più facilmente ed evitare i controlli nelle vicinanze. (SITES-25221)
* La barra a sinistra di Assets ora identifica quando il pulsante Modifica apre una nuova scheda del browser. Gli utenti possono anticipare il cambiamento di navigazione invece di perdere il contesto in modo imprevisto. (SITES-25220)
* I titoli dei componenti ora vengono visualizzati correttamente quando gli utenti applicano una maggiore spaziatura del testo. La barra laterale mantiene le etichette leggibili e supporta i requisiti di spaziatura del testo WCAG. (SITES-25219)
* Il campo del filtro in Componenti della barra laterale ora espone un nome accessibile corretto. Questo aggiornamento consente agli utenti di utilità di lettura dello schermo di identificare il campo senza affidarsi al testo segnaposto. (SITES-25212)
* Il problema segnalato descriveva una sequenza di attivazione illogica in modalità Annotation. È stato segnalato che gli utenti che utilizzano la tastiera non hanno visualizzato la barra degli strumenti delle annotazioni, a meno che non utilizzino Maiusc+Tab dopo l’attivazione della modalità. (SITES-24996)
* L’area di lavoro dell’editor espone il titolo della barra superiore come intestazione. Gli assistenti vocali possono annunciare il titolo con la struttura corretta, migliorando la navigazione e la comprensione della pagina. (SITES-24993)
* Nel rapporto sull’accessibilità è stato rilevato un contrasto insufficiente per il messaggio di stato di caricamento visualizzato quando gli utenti passano da una visualizzazione all’altra. La preoccupazione si è concentrata sulla leggibilità per gli utenti ipovedenti o con daltonismo. (SITES-24991)
* Nel rapporto sull’accessibilità si osservava che i collegamenti delle schede includevano testo non descrittivo. Questa preoccupazione si concentra sull’aiutare gli utenti di utilità di lettura dello schermo a comprendere ogni destinazione di collegamento senza ulteriore contesto. (SITES-24975)
* Nella vista a elenco Sites ora viene visualizzato il testo Live Copy con un contrasto maggiore. L’aggiornamento migliora la leggibilità per gli autori ipovedenti e per gli utenti che lavorano in condizioni di luminosità dello schermo. (SITES-24956)
* La navigazione da tastiera ora sposta lo stato attivo nel menu dell’emulatore dopo che gli utenti lo hanno espanso. Questo comportamento consente agli utenti di utilità per la lettura dello schermo e della tastiera di accedere alle opzioni di menu nell’ordine previsto. (SITES-24954)
* La vista a elenco Sites ora migliora la visibilità dei pulsanti di trascinamento nelle righe della tabella. Gli autori possono identificare il controllo più facilmente quando riordinano il contenuto. (SITES-24951)
* Una scheda non espone più sia il collegamento immagine che il collegamento intestazione come collegamenti separati quando condividono la stessa destinazione. L’aggiornamento riduce la complessità dell’utilità di lettura dello schermo e migliora l’efficienza della navigazione. (SITES-24947)
* I pulsanti del menu intestazione ora utilizzano attributi di accessibilità più precisi. Gli assistenti vocali annunciano che i pulsanti sono controlli espandibili anziché controlli che consentono l&#39;apertura di finestre di dialogo. (SITES-24742)
* La casella in entrata ora contrassegna i collegamenti correlati con il markup dell’elenco semantico. Gli utenti che usano un’utilità di lettura dello schermo possono comprendere più facilmente il numero e il raggruppamento dei collegamenti nella casella in entrata. (SITES-24730)
* Le etichette dei pulsanti di intestazione ora evitano nomi accessibili in modalità dettagliata. Gli utenti che usano un’utilità di lettura dello schermo ricevono annunci più chiari senza duplicare le informazioni sul ruolo dal testo dell’icona. (SITES-24715)
* Il pulsante Rapporto CSV fornisce ora un feedback più chiaro sul comportamento delle nuove schede. Gli utenti possono comprendere che selezionando il pulsante si apre una nuova scheda del browser prima di attivarlo. (SITES-24704)
* Le finestre di dialogo modali ora utilizzano markup di accessibilità più precisi per i controlli intestazione. I pulsanti Guida in linea e Attiva/Disattiva schermo intero rimangono controlli interattivi e non vengono più visualizzati come intestazioni per gli assistenti vocali. (SITES-24696)
* Il punto di riferimento della barra dei filtri ora utilizza un’etichetta distinta che ne identifica lo scopo. Gli utenti che usano un’utilità di lettura dello schermo possono navigare tra le pagine con più punti di riferimento simili in modo più affidabile. (SITES-24686)
* I messaggi della barra dei riferimenti ora forniscono una migliore leggibilità per gli utenti che si basano su un contrasto di testo sufficiente. Il problema segnalato riguardava la selezione e i messaggi di selezione multipla che apparivano troppo chiari sullo sfondo. (SITES-24666)
* Il modale di ricerca ora fornisce destinazioni di contatto più grandi per i pulsanti Rimuovi posizione e Chiudi. Questa modifica aiuta gli utenti con tremori alle mani, spasmi o ipovisione ad attivare il controllo desiderato. (SITES-24530)
* È stato segnalato che il collegamento dell’intestazione Adobe Experience Manager utilizzava un attributo ARIA errato. I test hanno confermato che il collegamento controlla il contenuto espandibile, pertanto lo stato accessibile esistente rimane appropriato. (SITES-24528)
* L&#39;indicatore di stato attivo per il pulsante Byline non viene più visualizzato tagliato nell&#39;elenco Componenti. La struttura visibile consente agli utenti che utilizzano la tastiera di tenere traccia della loro posizione nell’editor. (SITES-24503)
* Un problema segnalato descriveva un’alternativa testuale mancante per l’icona della descrizione comando delle informazioni nel pannello Componenti. Il problema non si riproduce, ma il riesame ha confermato che le icone informative devono esporre un nome chiaramente accessibile. (SITES-24500)
* L’Editor pagina non espone più più punti di riferimento per più aree geografiche con la stessa etichetta. Ogni punto di riferimento ora ha un nome accessibile univoco, in modo che gli utenti di utilità di lettura dello schermo possano identificare la regione corrente. (SITES-24497)
* Il controllo Cambia file o cartella ora separa l&#39;etichetta del controllo dalle informazioni sullo stato. Gli utenti che usano un’utilità di lettura dello schermo sentono un nome più breve e chiaro quando navigano nel controllo dell’intestazione. (SITES-24496)
* I controlli interattivi nella tabella Amministratore frammenti di contenuto ora supportano la navigazione da tastiera standard. Gli utenti che utilizzano la tastiera possono passare a pulsanti e collegamenti invece di individuarli solo tramite la navigazione con tasti di direzione. (SITES-24285)
* L’interfaccia utente di amministrazione di Sites ora tratta correttamente le icone decorative di Globe per gli assistenti vocali. Le icone utilizzano testo alternativo vuoto, in modo che gli utenti possano ascoltare solo contenuti significativi dell’interfaccia. (SITES-3057)

#### Interfaccia utente amministratore{#sites-adminui-6525}

Nella console Sites sono ora visualizzate correttamente le impostazioni di colonna **Vista elenco** salvate. Le colonne selezionate rimangono selezionate quando gli autori riaprono la finestra di dialogo delle impostazioni e il numero di colonne attive rimane accurato. (SITES-38576)

#### Interfaccia classica{#sites-classicui-6525}

Le finestre di dialogo del componente Testo dell’interfaccia classica ora visualizzano il contenuto dell’Editor Rich Text (RTE) come testo formattato invece che come HTML non elaborato. Gli autori possono modificare il testo esistente senza passare alla modalità Source o rimuovere manualmente il markup. (SITES-38709)

#### Console dei componenti{#sites-component-console-6525}

* Ora gli utenti possono cercare nella console Componenti con caratteri localizzati o multibyte. Nella console viene inoltre visualizzata un&#39;etichetta **Rimuovi** localizzata al posto della stringa inglese non tradotta. (SITES-39747)
* La pagina Proprietà componente ora localizza le stringhe in Strumenti > Componenti > Proprietà componente. Gli utenti non vedono più le etichette inglesi non tradotte nelle interfacce di authoring localizzate. (SITES-39745)

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

Assets Search ora risponde correttamente quando gli utenti selezionano o modificano i filtri. Il set di risultati filtrato viene aggiornato come previsto, ripristinando un perfezionamento affidabile della ricerca nella console Assets. (SITES-38686)

#### [!DNL Content Fragments] - Amministratore{#sites-admin-6525}

* Nella vista a elenco di Assets è ora disponibile una descrizione comando Localizzato Estratto da per per i frammenti di contenuto bloccati. Questa correzione migliora la coerenza della localizzazione quando gli autori esaminano le righe del flusso di lavoro. (SITES-42531)

* AEM ora localizza l’etichetta Principale nella finestra di dialogo di download del frammento di contenuto. La correzione mantiene la coerenza del flusso di lavoro di download tra le lingue diverse dall’inglese. (SITES-42534)
* AEM ora traduce l’etichetta di stato `Later` quando gli autori pianificano la pubblicazione del frammento di contenuto da Assets. Questa correzione mantiene la coerenza della colonna Pubblicato tra le interfacce localizzate. (SITES-42532)
* Durante la creazione di frammenti di contenuto ora viene visualizzato un messaggio di convalida localizzato quando gli autori immettono caratteri non validi nel campo Titolo. La finestra di dialogo non mostra più la stringa non localizzata &quot;Nome non valido fornito&quot;. (SITES-19796)
* La pagina Modifica frammento di contenuto ora utilizza etichette localizzate per tag e raccolte. Gli autori visualizzano i nomi dei campi tradotti invece delle stringhe inglesi non localizzate. (SITES-977)

#### [!DNL Content Fragments] - Editor frammenti{#sites-fragments-editor-6525}

* Contenuto associato nell’Editor frammento di contenuto ora mostra la stringa localizzata corretta quando gli autori rimuovono contenuto da una raccolta. La finestra di dialogo non sostituisce più il nome del contenuto con non definito. (SITES-33675)
* L’Editor frammento di contenuto ora visualizza un’etichetta Generale tradotta per le schede senza un segnaposto configurato. Le interfacce localizzate non mostrano più la stringa inglese non tradotta in quell’area dell’editor. (SITES-30715)
* Il selettore Riferimento contenuto nell’Editor frammento di contenuto ora mostra le etichette localizzate per i tipi di risorse consentiti. Le interfacce localizzate non visualizzano più nomi di tipo inglese per le categorie di risorse supportate. (SITES-29699)

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6525}

* Le risposte JSON GraphQL ora includono riferimenti a immagini incorporate da campi Rich Text di frammenti di contenuto quando i nomi di file DAM contengono spazi o caratteri non ASCII. Questa correzione consente alle applicazioni di eseguire il rendering delle immagini di riferimento senza richiedere agli autori di rinominare le risorse. (SITES-42191)
* Le risposte di GraphQL per i frammenti di contenuto ora gestiscono in modo più affidabile le query persistenti. Gli aggiornamenti correggono le intestazioni della cache duplicate, migliorano la gestione delle variabili codificate e restituiscono risposte più chiare in caso di contenuto mancante o query non riuscite. (SITES-40159)
* Le query persistenti GraphQL ora vengono eseguite senza messaggi di ERRORE e AVVISO non necessari nei registri. AEM gestisce correttamente le variabili codificate, pertanto le query riuscite non creano più `PersistedQueryServlet` voci fuorvianti. (SITES-39354)

* La finestra di dialogo Modifica endpoint GraphQL ora localizza le relative stringhe di interfaccia. Gli utenti non vedono più che lo schema di GraphQL non tradotto viene preso dal messaggio di configurazione nelle interfacce localizzate. (SITES-34018)

#### [!DNL Content Fragments] - Editor di query GraphQL{#sites-graphql-query-editor-6525}

Ora gli utenti possono aprire GraphQL Query Editor quando il nome del browser di configurazione selezionato contiene caratteri CJK o cirillici. L’editor visualizza le query persistenti per l’endpoint invece di mostrare un errore. (SITES-31616)

#### [!DNL Content Fragments] - Modelli e Editor modelli{#sites-models-model-editor-6525}

* Ora gli utenti visualizzano un messaggio di convalida localizzato nell’Editor modello per frammenti di contenuto quando un valore selezionato richiede un tipo di modello valido. L’editor non visualizza più il messaggio in inglese non tradotto nelle interfacce localizzate. (SITES-41117)
* Il pannello dei filtri Modello per frammenti di contenuto ora ne localizza lo stato e le stringhe di titolo. Gli utenti non visualizzano più etichette non tradotte come Titolo modello, Stato, Bozza, Abilitato e Disabilitato. (SITES-30863)

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

ContextHub ora viene caricato senza un errore JavaScript che ha interrotto la personalizzazione. I teaser e altre esperienze personalizzate possono essere visualizzati correttamente sulle pagine interessate. (SITES-38430)

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### Componenti core{#sites-core-components-6525}

* AEM non genera più errori ThumbnailServlet ripetuti quando una richiesta viene indirizzata a una risorsa DAM mancante. Il servlet interrompe l’elaborazione dopo il reindirizzamento, impedendo alle voci NullPointerException di inondare il registro degli errori. (SITES-41238)
* AEM non contrassegna più i campi delle finestre di dialogo facoltative come obbligatori quando gli autori riaprono le finestre di dialogo dei componenti. La finestra di dialogo mantiene la convalida incentrata sui campi che richiedono effettivamente l’input, impedendo in tal modo errori fuorvianti a livello di scheda. (SITES-40449)

* AEM include diverse correzioni di sicurezza supportate che rafforzano Sites e i relativi componenti di Cloud Services. Queste correzioni riducono il rischio di scripting tra siti e migliorano la gestione delle richieste tra i percorsi di authoring interessati. (SITES-38314)
* La finestra di dialogo Image v3 Component configuration (Configurazione del componente Immagine v3) ora localizza le stringhe nell’Editor pagina. Gli autori non visualizzano più le etichette non tradotte quando configurano i componenti Immagine nelle interfacce localizzate. (SITES-38726)

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### Crosswalk {#sites-crosswalk-6525}

* Dopo l&#39;installazione, il percorso incrociato non richiede più l&#39;installazione separata del pacchetto e della configurazione. AEM include i bundle richiesti, i pacchetti di contenuti, gli utenti del sistema, le mappature degli utenti del servizio e gli interruttori delle funzioni nel pacchetto preconfigurato. (SITES-41417)
* I flussi di lavoro cross-walk ora funzionano con il supporto cq-wcm-core richiesto in AEM 6.5. Gli autori possono utilizzare le azioni Crea modello e Apri editor universale senza aggiornamenti separati dei bundle di base. (SITES-37666)

#### Frammenti di esperienza{#sites-experiencefragments-6525}

AEM ora carica i modelli corretti quando gli autori creano varianti di Frammento esperienza e scorrono oltre i primi 40 risultati. Il selettore modelli mantiene il percorso del frammento esperienza selezionato durante l’impaginazione. (SITES-41531)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### Lanci{#sites-launches-6525}

* La Timeline Sites ora localizza il messaggio visualizzato quando AEM crea una versione prima di promuovere un lancio. Gli utenti non visualizzano più la stringa inglese non tradotta nelle interfacce localizzate. (SITES-39157)
* L’elenco Lanci ora visualizza la descrizione corretta per i lanci creati senza l’ereditarietà di modelli o Live Copy. Gli utenti non visualizzano più l’etichetta ingannevole del modello sostituito. (SITES-34229)

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### Localizzazione{#sites-localization-6525}

* Le proprietà dei componenti di testo nei Frammenti esperienza ora utilizzano etichette localizzate. Il menu Formato non mostra più stringhe non localizzate per le scelte di paragrafo, intestazione, virgolette o testo preformattato. (SITES-15091)

* Il testo dello stato del modello ora è allineato correttamente in **Strumenti** > **Generale** > **Modelli**. Le etichette di stato aggiornate, attivate e pubblicate vengono visualizzate su una linea orizzontale. (SITES-36797)
* Nella finestra di dialogo Sposta pagina viene ora visualizzata l&#39;etichetta Seleziona data e ora completa. L’etichetta non troncerà più nelle interfacce localizzate come il francese. (SITES-36795)
* La sezione Assets nell’Editor modelli ora mostra un’etichetta di Tag tradotti. Le interfacce di authoring localizzate presentano etichette coerenti durante la configurazione del modello. (SITES-33770)
* Le descrizioni dei criteri di pagina ora vengono visualizzate correttamente nell’Editor modelli. Gli utenti possono leggere la guida completa sulle classi CSS predefinite senza troncare il testo nella scheda Stili. (SITES-29724)
* Ora quando un autore tenta di trascinare un componente su un modello eliminato, nell’Editor modelli viene visualizzato un errore localizzato. Il messaggio non viene più visualizzato come stringa non tradotta &quot;durante l’elaborazione&quot;. (SITES-19313)
* Ora viene visualizzata l’etichetta &quot;Target&quot; nella finestra Configurazione teaser con testo localizzato. La sezione Collegamento ipertestuale non mostra più la stringa inglese in lingue diverse dall&#39;inglese. (SITES-18622)
* La finestra di dialogo Avvia flusso di lavoro nell’Editor pagina ora visualizza le etichette delle azioni per il flusso di lavoro localizzato. Gli autori non visualizzano più le stringhe in inglese per le opzioni del flusso di lavoro come le azioni di approvazione, pubblicazione, richiesta e annullamento della pubblicazione. (SITES-18103)
* Il menu a discesa Padre nel pannello di modifica Separatore ora visualizza le stringhe localizzate senza troncamento. Gli autori possono rivedere l’etichetta completa quando configurano il componente. (SITES-17480)
* L’Editor pagina ora visualizza le etichette localizzate per &quot;Larghezza intera&quot; e &quot;Larghezza fissa&quot; nel menu Stili del componente Contenitore. Gli autori che utilizzano le lingue supportate non visualizzano più tali stringhe in inglese. (SITES-17478)
* Ora gli autori possono leggere la descrizione completa nell’area Proprietà di navigazione della console Modelli. L’interfaccia utente mantiene la descrizione allineata e impedisce il troncamento del testo durante la modifica del modello. (SITES-15480)
* Gli autori ora possono leggere l’etichetta completa &quot;Forms e documenti con modello&quot; nel pannello laterale Riferimenti. La console Modelli non taglia più la stringa per le lingue supportate. (SITES-13167)
* Nella vista Riferimenti viene ora utilizzato il testo localizzato per il messaggio di errore di aggiornamento. Gli autori visualizzano i messaggi tradotti quando AEM non può aggiornare l’elenco dei riferimenti. (SITES-13102)
* La convalida del modulo ora identifica il campo che contiene un valore di ora non valido. La finestra modale Alterazione ora visualizza un messaggio di errore più chiaro, in modo che gli autori possano correggere il campo Ore o Minuti interessato. (SITES-10980)
* Nella console Modelli ora viene visualizzata un’etichetta Assets localizzata nella finestra di dialogo Seleziona immagine. L’etichetta viene visualizzata correttamente quando gli autori sfogliano le risorse dalle proprietà del modello. (SITES-8113)

#### MSM - Live Copy{#sites-msm-live-copies-6525}

* La Panoramica Live Copy ora localizza i formati delle date nella vista Stato relazione. I campi L **Live Copy Source Last Modified**, **Live Copy Last Modified** e **Last rollout** mostrano date che corrispondono alle impostazioni locali dell&#39;utente. (SITES-40756)
* MSM ora registra ulteriori dettagli per gli eventi push-on-modify. Le informazioni sull’evento aggiunte consentono ai team di tracciare l’attività di rollout e identificare l’origine di modifiche di pagina impreviste. (SITES-38029)

#### Editor di pagine{#sites-pageeditor-6525}

* Gli autori possono ora creare tag che includono lettere maiuscole o spazi e applicarli durante il primo salvataggio delle Proprietà pagina. Durante la stessa operazione, AEM crea il tag e scrive il valore corretto nei metadati della pagina. (SITES-42550)

* Gli autori ora possono creare frammenti di contenuto nelle cartelle DAM i cui nomi contengono un apostrofo. AEM gestisce correttamente il percorso della cartella codificata e non attiva più un’eccezione NullPointerException durante la creazione. (SITES-38653)

* AEM ora supporta le azioni di copia e incolla per i componenti Frammento di contenuto configurati nell’Editor pagina. Il componente conserva il riferimento Frammento di contenuto, in modo che gli autori possano duplicare il contenuto senza dover eseguire nuovamente l’authoring manuale. (SITES-41586)
* L’Editor pagina ora visualizza correttamente le descrizioni del primo campo nelle finestre di dialogo dei componenti. Le descrizioni lunghe rimangono visibili, pertanto gli autori possono rivedere le istruzioni dei campi senza perdere testo nella parte superiore della descrizione comando. (SITES-39937)
* Gli autori possono ora aprire la finestra di dialogo Collegamento editor Rich Text quando utilizzano AEM su HTTP. La correzione ripristina la modifica dei collegamenti per gli ambienti locali che non utilizzano HTTPS. (SITES-39467)

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### Editor universale {#sites-universal-editor-6525}

* Per impostazione predefinita, Universal Editor non si apre più in modalità Anteprima. AEM invia gli utenti all’ambiente di produzione Universal Editor, a meno che non richiedano esplicitamente il comportamento di anteprima. (SITES-37193)
* Universal Editor ora si apre in modalità Anteprima per gli ambienti di sviluppo, sviluppo rapido e stage di AEM. Il comando Apri utilizza il comportamento di anteprima corretto per le istanze non di produzione. (SITES-33839)

### [!DNL Assets] {#assets-6525}

* La libreria client Le mie condivisioni ora gestisce in modo sicuro i dati del titolo della risorsa condivisa prima di aggiungerla al markup della pagina. Le pagine di condivisione generate non espongono più gli utenti all’inserimento di script tramite metadati di risorse manipolati. (ASSETS-60898)

* Le licenze di Adobe Stock ora funzionano correttamente nell’interfaccia utente di Assets. Il pulsante License (Licenza) non rimane più disattivato dopo il caricamento da parte di AEM del profilo della risorsa Stock e dei dati di adesione. (ASSETS-62610)
* La notifica di scadenza preconfigurata delle risorse ora gestisce correttamente le date di scadenza. Le e-mail di promemoria vengono eseguite quando il tempo rimanente raggiunge la soglia configurata invece di saltare le risorse con una scadenza di otto giorni. (ASSETS-57857)

* AEM Assets ora ripristina la navigazione da tastiera dopo che gli utenti hanno scelto una ricerca salvata. L’interfaccia consente agli utenti di allontanarsi dal menu a discesa senza aggiornare o riavviare la vista Assets. (ASSETS-52061)

* Il flusso di lavoro di download della visualizzazione amministratore ora mantiene correttamente i nomi dei file ZIP. Il download di una risorsa ZIP non produce più un nome file con estensione .zip doppia. (ASSETS-62207)
* Il flusso di lavoro di riferimento Assets ora gestisce correttamente gli spazi nei nomi dei file. Gli aggiornamenti delle risorse correlate non hanno più esito negativo se il nome di un file selezionato include uno o più spazi. (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-6525}

Il menu a discesa Sottotitoli e tracce audio mostra ora l’arabo come lingua supportata in Dynamic Media. Questo aggiornamento consente agli utenti di aggiungere tracce di sottotitoli in arabo senza soluzioni alternative personalizzate. (ASSETS-61771)

### [!DNL Forms]{#forms-6525}

>[!NOTE]
>
>Le correzioni in [!DNL Experience Manager] Forms vengono distribuite tramite un pacchetto aggiuntivo separato una settimana dopo la data di rilascio pianificata per il Service Pack [!DNL Experience Manager]. In questo caso, il pacchetto del componente aggiuntivo sarà rilasciato giovedì 28 maggio 2026. Inoltre, a questa sezione viene aggiunto un elenco di correzioni e miglioramenti di Forms.



<!-- ALL THE FORMS BUG FIXES LISTED BELOW GO WITH AEM 6.5.25 FORMS MAY 28 2026 RELEASE!! UNHIDE THEM!! -->




<!-- #### Forms Designer {#forms-designer-6525} -->

<!-- 
* The Output API now handles dynamic form content consistently when PDF generation uses client rendering. Generated PDFs retain scripted description text across affected sections instead of leaving some fields blank. (LC-3928858)
* Document of Record generation now handles repeated panel pagination correctly when parent and child panels use the same "Place Top of Next Page" configuration. Authors no longer lose child panel data during the first repeated panel instance in generated output documents. (LC-3923274)
* Long multiline text fields in PDF preview now flow correctly across pages. The generated PDF no longer duplicates page content or drops hidden text during printing. (LC-3924324)
* Fillable PDFs now reset accessibility data when users clear form fields. Screen readers announce the cleared state correctly instead of reading old field values that no longer appear in the form. (LC-3923872)
* The Accessibility Checker now handles Nepali text correctly during PDF validation. Users can check Nepali-language documents without false accessibility errors tied to character encoding. (LC-3922988) 
-->

<!-- #### XMLFM {#forms-xmlfm-6525} -->

<!-- 
* Generated PDFs now include proper tags for supported form fields that use borders in the template. Screen readers can identify numeric fields, date fields, text fields, and checkboxes more reliably. (LC-3923534)
* Document of Record output now applies the correct tag structure to supported fields that include borders in the template. Numeric, date, text, and checkbox fields remain accessible in the generated PDF. (LC-3923265)
-->

<!-- #### XTG {#forms-xtg-6525} -->

<!-- 
* Forms output now merges XML data correctly when generatePDFOutputBatch generates PDFs in batch mode. The batch process no longer creates documents with blank or missing merged fields. (LC-3924192) 
* Document of Record output now includes nested child panels in the first occurrence of a repeatable panel. Forms that use Top of Next Page pagination no longer drop child panel data from the generated output. (LC-3923923)
* Custom bullet characters in XDP templates now map correctly for accessible PDF output. PAC validation no longer reports that text object characters cannot map to Unicode. (LC-3923079) 
-->


### Foundation {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

Il servizio CredentialsSupport per l&#39;autenticazione basata su Felix viene ora eseguito correttamente all&#39;avvio. In questo modo si evitano errori di dipendenza che possono influire sull’autenticazione dei token durante l’avvio di AEM. (GRANITE-63186)

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

La modifica dei file JSP ora funziona come previsto in CRXDE Lite dopo gli aggiornamenti di AEM 6.5. L’editor CodeMirror carica il contenuto del file invece di lasciare vuota la scheda JSP. (GRANITE-64333)

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### Localizzazione{#foundation-localization-6525}

* La finestra di dialogo Caricamento certificato in Sicurezza > Archivio attendibile ora mostra le etichette per il formato dei dati localizzati. Gli utenti non visualizzano più le etichette inglesi non localizzate quando aggiungono un certificato. (NPR-43412)

* La finestra di dialogo Crea registro chiavi allinea il pulsante Annulla agli altri pulsanti della finestra di dialogo. Il layout del pulsante rimane coerente e non si sposta più fuori allineamento. (NPR-43291)
* Nella finestra di dialogo Verifica in **Sicurezza** > A **Configurazioni DOBE IMS** viene ora visualizzato il testo di conferma localizzato. I messaggi di controllo ed eliminazione non vengono più visualizzati come stringhe inglesi non localizzate. (NPR-43289)
* Le etichette dell’interfaccia utente localizzate ora vengono visualizzate correttamente nelle finestre di dialogo interessate e nella scheda Registro chiavi. I valori Aria-label utilizzano stringhe tradotte e le etichette dei campi della password vengono visualizzate senza troncamento. (NPR-43285)
* Il flusso di lavoro Crea nuovo utente ora mostra gli errori di convalida localizzati per i caratteri non validi. Gli utenti ricevono un messaggio chiaro e tradotto invece di una stringa IllegalArgumentException non localizzata. (GRANITE-52920)

<!-- #### Oak {#foundation-oak-6525} -->

#### Platform{#foundation-platform-6525}

* Il pulsante Mostra riferimenti tag ora visualizza il numero di riferimenti per il tag selezionato. Questo aggiornamento consente agli utenti di comprendere l’utilizzo dei tag senza navigazione aggiuntiva. (CQ-4355509)
* La finestra di dialogo Sposta in Assegnazione tag consente ora di posizionare correttamente i messaggi di convalida. Il testo dell’errore non copre più l’icona del percorso di ricerca quando gli utenti inviano la finestra di dialogo con un campo obbligatorio vuoto. (CQ-4353009)

#### Sicurezza{#foundation-security-6525}

AEM ora inserisce nell&#39;elenco Consentiti ulteriori parole chiave che contengono segreto client. La creazione della configurazione non ha più esito negativo quando le integrazioni supportate utilizzano tali pattern di denominazione client-segreto. (GRANITE-66495)

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### Traduzione{#foundation-translation-6525}

I conteggi dello stato del progetto di traduzione ora vengono aggiornati correttamente dopo l’aggiornamento. Gli autori possono rivedere i valori bozza, bozza in corso e valori completi senza affidarsi a metadati obsoleti derivati dal comportamento precedente dei service pack. (NPR-43418)

#### Interfaccia utente{#foundation-ui-6525}

* Gli URL immessi manualmente nella console Sites ora vengono risolti nel percorso della pagina o della cartella desiderato. La gerarchia dei contenuti rimane coerente dopo l’aggiornamento e non viene più utilizzata come fallback dell’URL di base. (NPR-43688)
* La suite di test di CRX Package Manager non ha più esito negativo dopo l&#39;aggiornamento di un&#39;istanza AEM 6.5 LTS SP1 a LTS SP2. Il test del servlet elenco miniature ora viene completato come previsto. (NPR-43534)

* La struttura del contenuto della console Sites ora viene caricata in modo coerente dopo ogni aggiornamento del browser. Gli autori non visualizzano più una barra a sinistra vuota o un messaggio &quot;Non esiste alcun elemento&quot; quando il contenuto esiste. (NPR-43442)

<!-- #### WCM{#foundation-wcm-6525} -->

#### Flusso di lavoro{#foundation-workflow-6525}

* L’editor modelli di flusso di lavoro ora convalida correttamente i percorsi dei modelli di flusso di lavoro specifici del tenant. I clienti che memorizzano i modelli di flusso di lavoro nei percorsi /conf a livello di tenant possono modificare tali modelli senza spostarli nei percorsi di configurazione globali. (GRANITE-65376)

* L’editor modelli di flusso di lavoro ora normalizza i percorsi dei file di Windows durante la convalida del percorso. Gli autori possono modificare i modelli di flusso di lavoro sui server Windows senza errori di accesso che bloccano gli aggiornamenti dei modelli. (GRANITE-63692)
* La creazione delle attività ora include la convalida lato server per le date di scadenza. Gli utenti non possono creare attività con una data di scadenza che si verifica prima della data di inizio, che mantiene coerenti i dati delle attività della casella in entrata. (CQ-4362253)
* La creazione dello spazio dei nomi ora gestisce correttamente il testo localizzato. Gli utenti possono immettere caratteri non latini nel campo Titolo e creare lo spazio dei nomi senza un errore di convalida. (CQ-4355587)

## Installa [!DNL Experience Manager] 6.5.25.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0 richiede [!DNL Experience Manager] 6.5. Per istruzioni dettagliate, consulta la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md). <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del Service Pack è disponibile in Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.25.0 in una delle istanze di authoring utilizzando Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe consiglia di non rimuovere o disinstallare il pacchetto [!DNL Experience Manager] 6.5.25.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup di `crx-repository` nel caso sia necessario eseguirne il rollback. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installare il Service Pack in [!DNL Experience Manager] 6.5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). Adobe consiglia di riavviare il sistema se il tempo di attività corrente di un’istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il Service Pack da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Selezionare il pacchetto, quindi selezionare **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta la finestra di dialogo nell’interfaccia utente di Gestione pacchetti si chiude durante l’installazione del Service Pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di avere la certezza che l’installazione sia andata a buon fine. Questo problema si verifica in genere nel browser [!DNL Safari], ma può verificarsi in modo intermittente in qualsiasi browser.

**Installazione automatica**

Per installare [!DNL Experience Manager] 6.5.25.0 è possibile utilizzare due metodi diversi.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza l&#39;API HTTP [da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` per installare i pacchetti nidificati.

>[!NOTE]
>
>Experience Manager 6.5.25.0 non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l&#39;utilizzo di questa versione, vedere i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.25.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

UberJar per [!DNL Experience Manager] 6.5.25.0 è disponibile nel [archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell&#39;archivio centrale di Maven anziché nell&#39;archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale è stato rinominato in `uber-jar-<version>.jar`. Non esiste alcun `classifier`, con `apis` come valore, per il tag `dependency`.



## Funzioni obsolete e rimosse{#removed-deprecated-features}

Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md) per un elenco dettagliato di tutte le funzioni obsolete o rimosse per AEM 6.5.

### Supporto ai frammenti di contenuto nell’API REST di AEM Assets {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 fornisce OpenAPI moderne per la gestione dei modelli e frammenti di contenuto, pertanto gli endpoint precedenti per il supporto dei frammenti di contenuto nell’API REST di AEM Assets sono ora obsoleti.

Adobe intende mantenere questi endpoint meno recenti disponibili fino a un annuncio sulla fine del ciclo di vita. Adobe non pianifica ulteriori miglioramenti per gli endpoint obsoleti.

### Editor di SPA {#spa-editor}

[L&#39;editor SPA](/help/sites-developing/spa-overview.md) è stato dichiarato obsoleto per i nuovi progetti a partire dalla versione 6.5.25 di AEM 6.5. L’editor SPA rimane supportato per i progetti esistenti, ma non deve essere utilizzato per i nuovi progetti.

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

* Quando si tenta di spostare, eliminare o pubblicare frammenti di contenuto, siti o pagine, si verifica un problema durante il recupero dei riferimenti ai frammenti di contenuto. La query in background non riesce; la funzionalità non funziona.
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

### Problema noto per AEM Sites {#known-issues-aem-sites-6525}

Frammenti di contenuto-Anteprima non riuscita a causa della protezione DoS per una grande struttura ad albero di frammenti. Vedi l&#39;articolo [KB sulle opzioni di configurazione predefinite di GraphQL Query Executor](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemi noti per AEM Forms {#known-issues-aem-forms-6525}

* **FORMS-14521** Se un utente tenta di visualizzare in anteprima una bozza di lettera con dati XML salvati, si blocca nello stato `Loading` per alcune lettere specifiche.
* **FORMS-16603** Nell&#39;anteprima di stampa dell&#39;interfaccia utente di Interactive Communications Agent alcuni valori calcolati non vengono visualizzati correttamente.
* **FORMS-15681** Quando la lettera viene visualizzata in Anteprima di stampa, il contenuto viene modificato. Alcuni spazi vengono eliminati e alcune lettere vengono sostituite con `x`.
* **FORMS-15428** Dopo l&#39;aggiornamento ad AEM Forms Service Pack 20 (6.5.20.0) con il componente aggiuntivo Forms, le configurazioni basate sul servizio Adobe Analytics Cloud legacy che utilizzano l&#39;autenticazione basata sulle credenziali cessano di funzionare. Questo problema impediva la corretta esecuzione delle regole di analisi.
* **FORMS-16557** Nell&#39;anteprima di stampa dell&#39;interfaccia utente di Interactive Communications Agent, il simbolo di valuta (ad esempio il simbolo del dollaro $) viene visualizzato in modo incoerente per tutti i valori di campo. Viene visualizzato per valori fino a 999 ma non per valori di 1000 e superiori.
* **FORMS-16575** Eventuali modifiche all&#39;XDP dei frammenti di layout nidificati in una comunicazione interattiva non vengono riportate nell&#39;editor IC.
* **FORMS-21378** Quando la convalida lato server (SSV) è abilitata, l&#39;invio del modulo potrebbe non riuscire. Se riscontri questo problema, contatta il supporto Adobe per assistenza.
* **FORMS-23722** Quando un modulo contenente un campo **File allegato** che utilizza `bindref` viene inviato a un flusso di lavoro di AEM con un passaggio **Assegna attività**, gli allegati non vengono visualizzati. Di conseguenza, non vengono visualizzate quando l&#39;attività viene aperta dalla cartella Posta in arrivo. I file vengono salvati correttamente nell’archivio, ma l’interfaccia utente del passaggio Assegna attività non riesce a visualizzare gli allegati.
* **Le funzioni personalizzate di FORMS-23802** non vengono caricate in anteprima o pubblicate quando un modulo adattivo è incorporato in una pagina Sites. Questo problema si verifica quando la versione della libreria **aem-forms-core-component** è precedente al 1.1.76. Nei registri potrebbe essere visualizzato un errore come `InvalidFormContainerException: No form container found`. Per risolvere il problema, [scarica e installa l&#39;aggiornamento rapido](/help/release-notes/aem-forms-hotfix.md) per AEM Forms SP24 (AddOn 6.0.1454).

#### Problemi noti con gli hotfix disponibili {#aem-forms-issues-with-hotfixes}

<!--
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.25.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.25.0 only after the required hotfixes are released.
-->

Nei seguenti problemi è disponibile un hotfix per il download e l’installazione. Puoi [scaricare e installare l&#39;Hotfix](/help/release-notes/aem-forms-hotfix.md) per risolvere questi problemi:

* **FORMS-23881** Nelle implementazioni di AEM Forms JEE configurate utilizzando il programma di installazione completo di 6.5.23.0, il servizio di output non è in grado di elaborare le richieste quando nella chiamata viene fornito un file XCI personalizzato. Per risolvere il problema, installare il Service Pack di AEM 6.5.25.0 Forms più recente dal portale [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).
* **FORMS-23789** (solo AEM Forms su JEE): gli utenti hanno riscontrato problemi con Log4j in AEM Forms su JEE SP24, che hanno causato interruzioni nella registrazione e nel monitoraggio per i clienti aziendali. Per risolvere il problema, [scarica e installa l&#39;hotfix](/help/release-notes/aem-forms-hotfix.md) per AEM Forms su JEE Service Pack 6.5.25.0.
* **Le funzioni personalizzate di FORMS-23802** non vengono caricate in anteprima o pubblicate quando il modulo si trova in una pagina Sites con una versione precedente di aem-forms-core-component (&lt;1.1.76). Per risolvere il problema, installare l&#39;aggiornamento rapido [AEM Forms AddOn 6.0.1454](/help/release-notes/aem-forms-hotfix.md) per SP24.
* **FORMS-23789** (solo AEM Forms su JEE): gli utenti hanno riscontrato problemi con Log4j in AEM Forms su JEE SP24, che hanno causato interruzioni nella registrazione e nel monitoraggio per i clienti aziendali. Per risolvere il problema, [scarica e installa l&#39;hotfix](/help/release-notes/aem-forms-hotfix.md) per AEM Forms su JEE Service Pack 6.5.25.0.
* **Le funzioni personalizzate di FORMS-23802** non vengono caricate in anteprima o pubblicate quando il modulo si trova in una pagina Sites con una versione precedente di aem-forms-core-component (&lt;1.1.76). Per risolvere il problema, installare l&#39;aggiornamento rapido [AEM Forms AddOn 6.0.1454](/help/release-notes/aem-forms-hotfix.md) per SP24.
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

* **FORMS-23703** Quando la regola `contains` è configurata senza un valore predefinito, la convalida lato server per un modulo adattivo non riesce. È possibile installare la versione più recente di [AEM Forms 6.5.25.0 Service Pack](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases) per risolvere il problema.
* **GRANITE-63681** I connettori del modello dati modulo potrebbero non riuscire ad eseguire l&#39;autenticazione perché le parole chiave e il pattern regex richiesti non sono consentiti per impostazione predefinita. Per risolvere il problema, scarica e installa l&#39;aggiornamento rapido da [link](/help/release-notes/aem-forms-hotfix.md).
* **FORMS-23979** la conversione da HTML a PDF (PDFG) potrebbe verificarsi timeout intermittenti. Successivamente è stata rilasciata una versione più recente del componente aggiuntivo Forms per SP24 che include la correzione. Se si verifica questo problema, aggiornare l&#39;ambiente al componente aggiuntivo di Forms [più recente rilasciato per 6.5.25.0](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases).
* **FORMS-23717** Dopo l&#39;aggiornamento a **AEM Forms6.5.25.0**, `server.log` e `error.log` possono essere inondati da messaggi di avvertenza ripetuti, ad esempio *Creazione della factory del parser protetto non riuscita* o *L&#39;attributo di sicurezza ... non è supportato*. I registri possono crescere di circa **5-10 righe al secondo** (centinaia di MB all&#39;ora), che possono riempire il disco e bloccare il rollout di produzione.

Per ridurre il volume del log, impostare il livello di log per `com.adobe.util.XMLSecurityUtil` su `ERROR` nella configurazione del server applicazioni o tramite l&#39;argomento JVM `-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`. Questa funzionalità nasconde solo i messaggi e non corregge la causa sottostante.

* **FORMS-23875** Nella ricerca del modello dati modulo, un tag HTML viene visualizzato nell&#39;interfaccia utente anche quando non è presente un&#39;entità rilevante. Per risolvere il problema, scaricare e installare l&#39;aggiornamento rapido da [il collegamento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip).

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

I seguenti file zip contengono i documenti di testo che elencano i bundle OSGi e i pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 Service Pack:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5.25.0](/help/release-notes/assets/65250-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.25.0](/help/release-notes/assets/65250-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se fai parte della clientela e necessiti dell’accesso, contatta il responsabile dell’account Adobe.

* [Scarica il prodotto all’indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* Contatta l’[Assistenza Clienti di Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/it/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/it/docs/experience-manager-65)
>* [Iscriviti agli aggiornamenti dei prodotti con priorità Adobe](https://www.adobe.com/subscription/priority-product-update.html)



