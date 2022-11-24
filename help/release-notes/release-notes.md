---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova le informazioni sulla versione, le novità, installa le procedure guidate e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 3fff3ac4e09058a6c7f7bf4a99f85b3aab0ab1a9
workflow-type: tm+mt
source-wordcount: '3176'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | 24 novembre 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotte successivamente alla data di disponibilità iniziale di 6.5 di aprile 2019. [Installa questo service pack](#install) su [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* Se lo spostamento di una risorsa in Experience Manager non riesce, la risorsa può ancora essere rinominata. (NPR-38753)
* Quando visualizzi le risorse in un [!UICONTROL Vista a elenco], mancano alcuni titoli. (CQ-4345746)
* L’assistente vocale non annuncia il sottomenu del [!UICONTROL Relate] nella scheda Base della pagina Proprietà risorsa. (ASSETS-6938)
* L’assistente vocale rileva in modo errato le icone di cartella nella pagina di navigazione Risorse con l’elenco delle cartelle. (ASSETS-6936)
* Durante la copia di una raccolta, nell&#39;immagine manca un valore vuoto `alt` attribute or role=&quot;presentazione&quot;. Di conseguenza, l’immagine viene esposta agli utenti dell’assistente vocale. (ASSETS-6932)
* Il testo visualizzato durante l’annotazione di una risorsa non ha 4:5:1 rapporto di contrasto rispetto al colore di sfondo. (ASSETS-6931)
* Nella scheda IPTC della pagina Proprietà risorsa, quando regoli la larghezza della pagina, il contenuto della pagina non si adatta correttamente e si traduce in scorrimento orizzontale. (ASSETS-6929)
* Quando filtrate le risorse, il testo del filtro [!UICONTROL min] e [!UICONTROL max] i campi scompaiono dopo l’immissione di un valore. (ASSETS-6925)
* In Experience Manager Collections, l’assistente vocale non annuncia il [!UICONTROL email] nella schermata Download. (ASSETS-6923)
* Manca un testo alternativo durante l’annotazione degli elementi. (ASSETS-6922)
* Se il testo è scritto nel campo di selezione della data in ore e minuti, non viene visualizzato alcun messaggio di errore di testo. L&#39;errore viene identificato solo utilizzando il colore rosso. (ASSETS-6852, ASSETS-6921, ASSETS-6920, ASSETS-6907)
* Il testo alternativo in `[role='img']` nel filtro File mancante. (ASSETS-6919)
* Annuncio non corretto dell’assistente vocale per [!UICONTROL Crea] sottomenu. (ASSETS-6916)
* In Experience Manager Raccolte, il pulsante di rimozione `X` non dispone di alcun testo da annunciare per gli assistenti vocali. (ASSETS-6912)
* Quando si utilizza l’Experience Manager di Color Contrast Analyzer (Analisi di contrasto colore), non esiste alcuna distinzione tra la data corrente e la data scelta nel selettore data del widget calendario. Manca di un rapporto di contrasto di almeno 3:1 rispetto ai colori adiacenti. (ASSETS-6911)
* In File di Experience Manager, quando selezioni una delle opzioni da [!UICONTROL Pianificazione] pulsante di scelta in Gestisci pubblicazione, il nome e lo stato delle opzioni del pulsante di scelta sono annunciati dall’assistente vocale. Tuttavia, **Pianificazione** etichetta non annunciata. (ASSETS-6908, ASSETS-6906)
* Testo alternativo mancante per l’icona Ordina. (ASSETS-6904)
* Nella pagina delle proprietà della risorsa, il nome del campo `Person` in IPTC Extension le etichette della scheda non vengono annunciate dagli assistenti vocali. L’assistente vocale annuncia solo campi modificabili e attualmente vuoti, ma non il nome dell’etichetta. (ASSETS-6903, ASSETS-6848)
* Non è possibile visualizzare lo strumento di annotazione tramite tastiera. Per disegnare un&#39;immagine viene utilizzato un mouse per visualizzare lo strumento Annotazione. (ASSETS-6899)
* Ad Experience Manager, Raccolte, un campo vuoto nel campo **Avanzate** visualizza un rapporto di contrasto errato tra il bordo e uno dei colori adiacenti. (ASSETS-6895)
* Valori di attributo ARIA errati per alcuni elementi durante la modifica delle risorse. (ASSETS-6894)
* L’assistente vocale non identifica correttamente l’intestazione durante la creazione di un flusso di lavoro. (ASSETS-6892)
* Durante la copia di una raccolta, il pulsante di rimozione dell’immagine di SVG `X` con role=&quot;img&quot; manca un role=&quot;presentazione&quot;. Di conseguenza, l’immagine viene esposta agli utenti dell’assistente vocale. (ASSETS-6890)
* In **Base** scheda delle proprietà di Assets, l’assistente vocale non annuncia in modo appropriato lo stato di espansione o compressione del campo Tag. (ASSETS-6889)
* La **Base** in Proprietà risorsa la scheda contiene pagine con ID duplicato. (ASSETS-6888)
* Quando si specifica un valore nella casella di testo, l’etichetta del campo di testo che consente di definire un titolo durante la creazione di un flusso di lavoro scompare. (ASSETS-6887)
* L’elenco dei destinatari durante la condivisione di un collegamento viene visualizzato come una tabella di dati con intestazioni, ma non viene identificato semanticamente come tabella di dati per gli utenti dell’assistente vocale. (ASSETS-6886)
* Non viene visualizzato alcun messaggio di errore per rappresentare un campo vuoto in `Add Email Address` campo . L&#39;errore è rappresentato solo utilizzando un colore. (ASSETS-6885, ASSETS-6843)
* I testi segnaposto, il percorso e il testo Alt non hanno almeno un rapporto di contrasto 4,5:1 rispetto al colore di sfondo. (ASSETS-6884, ASSETS-6865)
* Valori non validi per alcuni degli attributi ARIA durante il salvataggio di una raccolta avanzata. (ASSETS-6882)
* Quando salvi una raccolta avanzata, alcune etichette non sono associate in modo appropriato all’assistente vocale. (ASSETS-6881)
* Nella scheda IPTC delle proprietà delle risorse, l’assistente vocale non annuncia l’etichetta per i campi modulo per parola chiave. (ASSETS-6879)
* In Raccolte Experienci Manager, la [!UICONTROL E-mail] Il campo non è identificato come campo obbligatorio e non viene visualizzato alcun messaggio di errore se non si specifica un valore. (ASSETS-6877)
* In File di Experience Manager, nessun messaggio di errore in **Condivisione collegamenti** la schermata viene visualizzata in `Add Email Address`. L&#39;errore viene identificato solo utilizzando un colore. (ASSETS-6876, ASSETS-6875)
* [!UICONTROL Ritaglio e mappa] le opzioni non hanno i nomi programmatici durante la modifica di una risorsa. (ASSETS-6874)
* Il testo del filtro manca della razione del contratto 4.5:1 rispetto al colore di sfondo. (ASSETS-6873)
* Il testo per il nome della cartella nella pagina di navigazione principale non ha un rapporto di contrasto 4.5:1 rispetto al colore di sfondo. (ASSETS-6872)
* Durante l&#39;esecuzione del [!UICONTROL Copia] per le raccolte, **[!UICONTROL Aggiungi utente]** il controllo modulo casella combinata non è associato correttamente all&#39;etichetta visibile. (ASSETS-6870)
* L’assistente vocale non annuncia il [!UICONTROL Crea] opzioni del sottomenu dei pulsanti. (ASSETS-6869)
* Le opzioni Ambito, Flussi di lavoro e Fuso orario non hanno un rapporto di contrasto 4,5:1 rispetto al colore di sfondo. (ASSETS-6868)
* L’assistente vocale segnala erroneamente lo stato di compressione della **Timeline** colonna. (ASSETS-6864)
* Elementi figlio mancanti per alcuni dei ruoli ARIA durante il salvataggio di una raccolta avanzata. (ASSETS-6862)
* Durante la condivisione di una risorsa, gli attributi ARIA richiesti per `Search/Add Email Address` campo non specificato. (ASSETS-6860)
* La **map** non è possibile visualizzare la finestra di dialogo utilizzando la tastiera. Per visualizzare la finestra di dialogo della mappa è invece necessario fare clic con il mouse. (ASSETS-6859)
* Elementi figlio mancanti per alcuni dei ruoli ARIA nella scheda Base della pagina Proprietà risorsa. (ASSETS-6858)
* I campi di input di testo vuoti, disponibili nella scheda IPTC delle proprietà delle risorse, non hanno un rapporto di contrasto 3:1 rispetto ai colori adiacenti. (ASSETS-6854, ASSETS-6847)
* Le icone del profilo nel **Timeline** le sezioni non vengono rilevate correttamente dagli assistenti vocali. (ASSETS-6850)
* L’assistente vocale non annuncia che la casella combinata Stato revisione, disponibile nella scheda Base delle proprietà delle risorse, è un campo di sola lettura. (ASSETS-6849)
* L’assistente vocale non annuncia in modo appropriato l’etichetta delle caselle di controllo Seleziona tutto e Annotazione . (ASSETS-6846)
* Lo stato attivo della tastiera evita `About Adobe Experience Manager` opzione disponibile in **Mostra Guida** menu. (ASSETS-6845)
* Gli assistenti vocali non annunciano correttamente le cartelle selezionate durante la navigazione nell’elenco delle cartelle utilizzando i tasti freccia della tastiera nella vista a schede. (ASSETS-6844)
* Durante il caricamento di un PDF nell’Experience Manager, l’utilizzo della memoria è in costante aumento. (ASSETS-16889)
* Quando un flusso di lavoro converte un file .ZIP in un nome di cartella in Assets, non conserva la custodia del nome del file .ZIP. (ASSETS-16712)
* Quando si passa da Brand Portal all’Experience Manager 6.5, il filtro di predicato utente non visualizza i risultati appropriati quando si applica il filtro per la prima volta. (ASSETS-15932)
* Impossibile annotare un video. (ASSETS-15217)
* **Gestisci pubblicazione** scompare per un utente senza accesso replicato e `READ` e `WRITE` accesso `ETC` e `VAR`. (ASSETS-15007)
* Il tempo di caricamento della pagina delle proprietà aumenta per una risorsa con più riferimenti. (ASSETS-14182)
* Quando un’immagine viene annullata dalla pubblicazione da Brand Portal, Experience Manager la annulla anche da Dynamic Media e di conseguenza non è visualizzata alcuna immagine sul sito web live. (ASSETS-14118)
* Problemi XSS sulle schede Smart Crop in Dynamic Media. (ASSETS-14212, ASSETS-14208, ASSETS-13704)
* Problema XSS nei predefiniti per visualizzatori in Dynamic Media. (ASSETS-13822)
* Convalida l’accesso utente durante l’anteprima delle risorse DM su AEM. (CQ-4314757)


## Commerce {#commerce-6515}

* Creazione di una pagina del negozio non riuscita, arresto del processo di rollout complessivo del catalogo. (CQ-4347181)

## [!DNL Forms] {#forms-6515}

>[!NOTE]
>
>Correzioni in [!DNL Experience Manager] Forms viene fornito tramite un pacchetto aggiuntivo separato una settimana dopo il programma [!DNL Experience Manager] Data di rilascio del Service Pack. In questo caso, i pacchetti aggiuntivi rilasceranno giovedì 1 dicembre 2022. Inoltre, a questa sezione verrà aggiunto anche un elenco di correzioni e miglioramenti di Forms.

## [!DNL Sites] {#sites-6515}

* La console Experience Manager Sites Launch risultava vuota. (NPR-39188)
* I riferimenti non venivano regolati quando era necessario attivare anche la pagina contenente il riferimento durante lo spostamento della pagina. (NPR-39061)
* Quando un contenitore Layout non è nascosto utilizzando il contenitore principale, le modifiche di layout non vengono applicate a tutti i componenti all’interno del contenitore nidificato. (NPR-39041)
* Il contenuto ora non si sovrappone più ad altri contenuti con una larghezza di 320 pixel. (SITES-8885)
* È stata aggiunta la messa a fuoco dopo la chiusura di una finestra di dialogo. (SITES-8885)

### Accessibilità {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* La **[!UICONTROL Annotazione]** manca il nome di accesso facilitato del pulsante. (SITES-2892)
* Lo stato di un componente dell’interfaccia utente ATTIVA (**[!UICONTROL Taglia]**, **[!UICONTROL Copia]**, **[!UICONTROL Incolla]**, **[!UICONTROL Inserisci componenti]**, **[!UICONTROL Gruppo]** e così via) non ha almeno un rapporto di contrasto di luminosità da tre a uno con lo sfondo adiacente interno o esterno. (SITES-8889, SITES-8756, SITES-8885)
* Il messaggio di stato non viene annunciato automaticamente. (SITES-8889, SITES-8756, SITES-8885)
* Il contenuto di testo non ha un rapporto di contrasto 4,5:1. (SITES-8756, SITES-8885)
* Il testo del collegamento o del pulsante non presenta un rapporto di contrasto di 4,5:1 al passaggio del mouse o alla messa a fuoco. (SITES-8756, SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL genera un&#39;eccezione. Ad esempio, non è possibile ottenere tag di variante da un frammento di contenuto. Non c&#39;è alcuna variazione con il nome &quot;elettrico&quot;. Questo problema è dovuto alla chiamata di `getVariationTags` per una variazione non esistente che solleva un&#39;eccezione. (SITES-8898)
* Ordinamento degli ordini dei titoli nella vista Elenco, sia ascendente che decrescente, modalità con l’ordine A, C e B. (SITES-7585)
* È stato aggiunto il supporto per l’assegnazione tag per le varianti dei frammenti di contenuto. (SITES-8168)
* Codice specifico Odin identificato e rimosso dall’Experience Manager 6.5 non necessario. (SITES-3574)
* Quando si pubblicava un frammento di copia per lingua dall’interfaccia utente dell’Editor frammento di contenuto, i riferimenti associati venivano pubblicati nella cartella Inglese. (NPR-39182)
* I campi data vengono precompilati con una data. (NPR-39124)
* La seconda volta che si seleziona l’opzione del pulsante di scelta, i tag sono scomparsi. (NPR-39071)

### Fluid XP {#sites-fluidxp-6515}

* Abilita il supporto per la compilazione ES6 per la libreria client `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* Impossibile svuotare e salvare il campo Multifield in un modello di frammento di contenuto perché la convalida viene eseguita anche se **[!UICONTROL Obbligatorio]** non è selezionato. (NPR-39063)
* In **[!UICONTROL Copia]** o **[!UICONTROL Livecopy]** i compiti `cq:targetMetadata` le informazioni non venivano duplicate correttamente. Questa funzionalità ha fatto sì che due o più frammenti esperienza in Experience Manager puntassero alla stessa offerta esportata in target. (NPR-38970)
* Dopo un’azione Ripristina albero , viene visualizzato il messaggio `Un-publication pending. #0 in the queue` viene visualizzata nell’interfaccia utente per una pagina che non è mai stata pubblicata. (NPR-38847)

### Editor pagina {#sites-pageeditor-6515}

* Annulla non ha eliminato l’ultima modifica apportata al testo aggiunto al componente. Al contrario, quando la pagina veniva aggiornata, l’intero componente veniva eliminato. (SITES-8597)
* Aggiornamento `jquery-ui` all’ultima versione, l’Editor pagina non funzionava correttamente. (NPR-38596)
* Il contenuto ora non si sovrappone più ad altri contenuti con una larghezza di 320 pixel. (SITES-8756)
* è stato aggiunto focus dopo la chiusura della finestra di dialogo (SITES-8756)

## Sling {#sling-6515}

* `Repoinit` non supportava la creazione o la gestione di gruppi con spazio vuoto nel nome principale perché il nome del gruppo era trattato come stringa e non supportava l&#39;uso di virgolette. (SLING-10952)
* I registri vengono inavvertitamente compilati con messaggi di errore ed eccezioni. (NPR-39024)

## Progetti di traduzione {#translation-6515}

* La pagina di destinazione veniva aggiunta al processo di traduzione per Copie per lingua aggiornate tramite il pannello Progetti ; pagina di origine non aggiornata. (NPR-39278)
* Errore del processo di traduzione durante la generazione di un&#39;anteprima per tutte le pagine di un progetto di traduzione. (NPR-39059)
* Se le impostazioni internazionali della lingua non esistono, vengono comunque create in una cartella locale quando le regole di riferimento sono configurate per un evento. (NPR-39054)

## Interfaccia utente {#ui-6515}

* Gli errori JavaScript si verificano all&#39;interno del file `multifield.js` per alcuni campi nel modello Frammento di contenuto nell’editor del modello Frammento di contenuto e anche nell’editor Frammento di contenuto . (NPR-39350)

## Flusso di lavoro {#workflow-6515}

* I flussi di lavoro eseguiti correttamente in Experience Manager 6.5.11 non venivano eseguiti in modo coerente alla versione 6.5.13 di Experience Manager. (NPR-39023)

## Installa [!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0 richiede [!DNL Experience Manager] 6.5. Vedi [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate. <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.15.0 su una delle istanze Autore che utilizza Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>Adobe sconsiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.15.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup del `crx-repository` nel caso sia necessario riportarlo indietro. <!-- UPDATE FOR EACH NEW RELEASE -->

### Installa il service pack su [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia un riavvio se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di installare, scegli uno snapshot o un nuovo backup del tuo [!DNL Experience Manager] istanza.

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l&#39;istanza dopo l&#39;installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l&#39;istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude durante l’installazione del service pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere, questo problema si verifica in [!DNL Safari] browser ma può verificarsi a intermittenza su qualsiasi browser.

**Installazione automatica**

Esistono due metodi diversi per l&#39;installazione automatica [!DNL Experience Manager] 6.5.15.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza la [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzo `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>Experience Manager 6.5.15.0 non supporta l’installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo con questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. La pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa di versione aggiornata `Adobe Experience Manager (6.5.15.0)` sotto [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (Usa console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.13 o successiva (Usa console Web: `/system/console/bundles`). <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installa [!DNL Experience Manager] Pacchetto aggiuntivo di Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora se non utilizzi [!DNL Experience Manager] Forms.

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

1. Assicurati di aver installato la [!DNL Experience Manager] Service Pack.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) per il sistema operativo in uso.
1. Installa il pacchetto aggiuntivo di Forms come descritto in [Installazione dei pacchetti aggiuntivi di AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Se utilizzi le lettere in Experience Manager 6.5 Forms, installa il [pacchetto di compatibilità AEM più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Installa [!DNL Experience Manager] Forms su JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Ignora questa sezione se non usi AEM Forms in JEE. Correzioni in [!DNL Experience Manager] Forms su JEE viene fornito tramite un programma di installazione separato.

Per informazioni sull&#39;installazione del programma di installazione cumulativo per [!DNL Experience Manager] Forms su JEE e configurazione post-distribuzione, vedi [note sulla versione](jee-patch-installer-65.md).

>[!NOTE]
>
>Dopo aver installato il programma di installazione cumulativo per [!DNL Experience Manager] Forms su JEE, installa il pacchetto aggiuntivo Forms più recente, elimina il pacchetto aggiuntivo Forms dal `crx-repository\install` e riavviare il server.

### UberJar {#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.15.0 è disponibile nella [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includere nel POM del progetto la seguente dipendenza: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece dell’archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Quindi, non c&#39;è `classifier`con `apis` come valore, per `dependency` tag .

## Funzioni obsolete {#removed-deprecated-features}

Di seguito è riportato un elenco di funzioni e funzionalità contrassegnate come obsolete con [!DNL Experience Manager] 6.5.7.0. Le funzioni sono inizialmente dichiarate obsolete e successivamente rimosse in una versione futura. È disponibile un’opzione alternativa.

Controlla se utilizzi una funzione o una funzionalità in una distribuzione. Inoltre, pianifica di modificare l’implementazione in modo da utilizzare un’opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrazioni | La **[!UICONTROL Opt-in di AEM Cloud Services]** la schermata è obsoleta poiché la [!DNL Experience Manager] e [!DNL Adobe Target] l&#39;integrazione viene aggiornata in [!DNL Experience Manager] 6.5. L’integrazione supporta l’API Adobe Target Standard. L’API utilizza l’autenticazione tramite Adobe IMS e [!DNL Adobe I/O Runtime]. Sostiene il ruolo crescente di Launch Adobe per lo strumento [!DNL Experience Manager] nelle pagine di analisi e personalizzazione, la procedura guidata di consenso è funzionalmente irrilevante. | Configura le connessioni di sistema, l’autenticazione Adobe IMS e [!DNL Adobe I/O Runtime] integrazioni tramite le rispettive [!DNL Experience Manager] servizi cloud. |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto per [!DNL Experience Manager] 6.5. | N/D |

## Problemi noti {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [Frammento di contenuto AEM con pacchetto indice GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Questo pacchetto è necessario per i clienti che utilizzano GraphQL; questo consente loro di aggiungere la definizione dell&#39;indice richiesta in base alle funzioni effettivamente utilizzate.

* Come [!DNL Microsoft® Windows Server 2019] non supporta [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] non supporta installazioni chiavi in mano per [!DNL AEM Forms 6.5.10.0].

* Se stai aggiornando il tuo [!DNL Experience Manager] istanza dalla versione 6.5 alla versione 6.5.10.0, puoi visualizzare `RRD4JReporter` eccezioni `error.log` file. Per risolvere il problema, riavvia l&#39;istanza.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 10 o un service pack precedente su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminato.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Gli utenti possono rinominare una cartella in una gerarchia [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando l’integrazione Adobe Target è configurata in [!DNL Experience Manager] se si utilizza l’API di Target Standard (autenticazione IMS) e poi si esportano frammenti di esperienza in Target, vengono creati tipi di offerta errati. Invece del tipo &quot;Frammento esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

* Quando si tenta di spostare/eliminare/pubblicare frammenti di contenuto o siti/pagine, si verifica un problema quando i riferimenti ai frammenti di contenuto vengono recuperati, in seguito a un errore della query in background; ovvero la funzionalità non funziona.
Per garantire il corretto funzionamento, è necessario aggiungere le seguenti proprietà al nodo di definizione dell&#39;indice `/oak:index/damAssetLucene` (non è richiesta alcuna reindicizzazione):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Elenco dei bundle OSGi inclusi nell&#39;Experience Manager 6.5.15.0](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.15.0](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina di prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

