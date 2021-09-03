---
title: '[!DNL Experience Manager] Note sulla versione 6.5 del service pack'
description: Note sulla versione specifiche del service pack 10  [!DNL Adobe Experience Manager] 6.5
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: a3d52ecf9284ba22cac3739ba543e5dd5c855331
workflow-type: tm+mt
source-wordcount: '4205'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] Note sulla versione 6.5 del service pack {#aem-service-pack-release-notes}

## Informazioni sulla versione {#release-information}

| Prodotti | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.10.0 |
| Tipo | Versione Service Pack |
| Data | 26 agosto 2021 |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## Contenuto in [!DNL Adobe Experience Manager] 6.5.10.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e miglioramenti a livello di prestazioni, stabilità e sicurezza, rilasciati a partire dalla versione 6.5 di aprile 2019. Il service pack è installato su [!DNL Adobe Experience Manager] 6.5.

Le funzioni chiave e i miglioramenti introdotti in [!DNL Adobe Experience Manager] 6.5.10.0 sono:

* **Editor e  [!DNL Content Fragment] modelli migliorati**: È ora possibile creare modelli complessi e personalizzati per contenuti strutturati utilizzando  [!DNL Content Fragment] modelli nidificati. Le strutture di contenuto sono modularizzate in elementi di base modellati come sottoframmenti. I frammenti di livello superiore fanno riferimento a tali sottoframmenti. Ulteriori miglioramenti del tipo di dati, come le regole di convalida avanzate, migliorano ulteriormente la flessibilità nella modellazione dei contenuti con [!DNL Content Fragments]. L’editor [!DNL Experience Manager] [!DNL Content Fragment] supporta le strutture di frammenti nidificati in una sessione dell’editor comune, con miglioramenti quali la visualizzazione struttura ad albero e la navigazione a schede tramite gerarchie di frammenti.

* **API GraphQL per[!DNL Content Fragments]**: La nuova API GraphQL è il metodo standard per distribuire contenuti strutturati in formato JSON. Le query GraphQL consentono ai client di richiedere solo gli elementi di contenuto rilevanti per il rendering di un’esperienza. Tale selezione elimina la consegna dei contenuti in eccesso (possibilità con le API REST HTTP) che richiede l’analisi dei contenuti sul lato client. Gli schemi GraphQL sono derivati da modelli [!DNL Content Fragment] e le risposte API sono effettuate in formato JSON. In [!DNL Experience Manager] come [!DNL Cloud Service], [Le query GraphQL persistono](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) ed elaborano richieste di GET compatibili con la cache. Non è ancora possibile in [!DNL Experience Manager] 6.5.10.0.

* **Gestione della gerarchia e anteprima** futura: Gli utenti dispongono ora di un’interfaccia per accedere alle strutture di contenuto dei loro  [!DNL Experience Manager] lanci, inclusa la possibilità di aggiungere e rimuovere pagine in un lancio. Questa funzione migliora la flessibilità dei [!DNL Experience Manager] lanci per creare versioni di contenuti destinate a future pubblicazioni. [Le funzioni ](/help/sites-authoring/working-with-page-versions.md#timewarp) di deformazione in tempo libero consentono agli utenti di visualizzare in anteprima gli avvii come stati di contenuto futuri.

* **Risorse** collegate:  [!DNL Experience Manager] estende la  [!DNL Connected Assets] funzionalità all’utilizzo di  [!DNL Dynamic Media] immagini nei componenti core applicabili. Consulta [Utilizzare le risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* **Opzioni di condivisione dei collegamenti per scaricare risorse o rappresentazioni**: Quando condividi risorse e raccolte come collegamento, gli utenti possono scegliere se consentire il download delle risorse originali o delle relative rappresentazioni, oppure entrambi utilizzando il collegamento condiviso. Inoltre, gli utenti che scaricano le risorse condivise con loro tramite un collegamento possono scaricare solo le risorse originali, solo le rappresentazioni o entrambi.

* **Limita le risorse secondarie generate**: Gli amministratori possono limitare il numero di risorse secondarie  [!DNL Experience Manager] generate per risorse composte come file PDF, PowerPoint, InDesign e Keynote. Consulta [Gestire le risorse composte](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Supporto** Camera Raw: È disponibile un nuovo  [!DNL Camera Raw] pacchetto che supporta la  [!DNL Adobe Camera Raw] versione 10.4. Consulta  [elaborare le immagini utilizzando [!DNL Camera Raw]](/help/assets/camera-raw.md).

* Aggiornamento dell’archivio incorporato (Apache Jackrabbit Oak) alla versione 1.22.8.

* **Miglioramenti dell’accessibilità**:

   * [!DNL Dynamic Media] fornisce molti miglioramenti all’accessibilità per i visualizzatori. Vedere [[!DNL Dynamic Media] aggiornamenti](#dynamic-media-65100).

   * Platform fornisce alcuni miglioramenti all’accessibilità. Consulta [Aggiornamenti della piattaforma](#platform-65100).

* **Miglioramenti** dell’esperienza utente:

   * [!DNL Experience Manager] visualizza direttamente un elenco di tutti i modelli di contenuto presenti in una cartella senza che gli autori di contenuti debbano spostarsi all’interno della struttura del file. La funzione ora richiede meno clic e migliora l’efficienza di authoring.

   * Il campo percorso nell’ editor [!DNL Sites] consente agli autori di trascinare risorse da [!DNL Content Finder].

* È stato aggiunto il supporto per l’ API `GuideBridge#getGuidePath` in [!DNL AEM Forms].

* È ora possibile utilizzare il servizio Automated forms conversion per [convertire i PDF forms in francese, tedesco e spagnolo](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#language-specific-meta-model) nei moduli adattivi.

* **Messaggi di errore nel browser** Proprietà: Sono stati aggiunti messaggi di errore per ciascuna proprietà nel browser Proprietà adattive Forms. Questi messaggi consentono di comprendere i valori consentiti per un campo.

* **Supporto per utilizzare l&#39;opzione letterale per impostare il valore per una variabile** di tipo JSON: Puoi utilizzare l’opzione letterale per impostare il valore per una variabile di tipo JSON nel passaggio della variabile set di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

<!--

* [Platform Updates](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
  * [!DNL Adobe Acrobat 2020]
  * [!DNL Ubuntu 20.04]
  * [!DNL Open Office 4.1.10]
  * [!DNL Microsoft Office 2019]
  * [!DNL Microsoft Windows Server 2019]
  * [!DNL RHEL8]

  -->

Per un elenco di tutte le funzioni e i miglioramenti introdotti in [!DNL Experience Manager] 6.5.10.0, consulta [novità in [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

Di seguito è riportato l&#39;elenco delle correzioni apportate in [!DNL Experience Manager] 6.5.10.0.

### [!DNL Sites] {#sites-65100}

* Lo stato attivo passa a un altro campo quando si digita nel campo **[!UICONTROL Valore predefinito]** nella scheda **[!UICONTROL Proprietà]** dell’Editor frammento di contenuto (NPR-36992).

* Durante il filtraggio dei modelli [!DNL Content Fragment] sotto un percorso specificato, la ricerca [!DNL Experience Manager] restituisce tutti i nodi con `cq:Template` invece di restituire percorsi e nodi solo per il modello [!DNL Content Fragment] (SITES-1453).
* [!DNL Content Fragments] return  `null` come stato delle cartelle (SITES-1157).
* [!DNL Experience Manager] non consente agli utenti di disabilitare e abilitare  [!DNL Content Fragment] i modelli (SITES-1088).
* Quando un utente sposta, rinomina o elimina [!DNL Content Fragments] o risorse multimediali, i riferimenti [!DNL Content Fragments] non vengono aggiornati automaticamente (SITES-196).
* L’invio di componenti da una pagina all’altra genera errori JavaScript (NPR-37030).
* Quando le proprietà della pagina vengono visualizzate rapidamente, vengono aperte le Proprietà pagina per una pagina diversa (NPR-37025).
* Il frammento di contenuto consente al frammento di contenuto di fare riferimento a se stesso. Il selettore non supporta l’operazione (NPR-36993).
* Dopo l&#39;aggiornamento al service pack 9, alcuni utenti non possono spostare le cartelle in Experience Manager e visualizzare gli errori nei registri (SITES-1481).
* Durante la regolazione della larghezza del componente nel Contenitore di layout in modalità di modifica, si osserva uno sfarfallio (NPR-36961).
* Quando si promuove un lancio, le modifiche nel lancio promosso vengono implementate in doppio negli altri lanci. Se un utente promuove il lancio con doppio rollout, il contenuto raddoppiato viene riportato sulla pagina sorgente (NPR-36893).
* [!DNL Experience Manager] aggiunge un bordo grigio ad alcune immagini PNG con trasparenza se aggiungi le immagini a una pagina utilizzando il componente di base Immagine o se le ridimensiona utilizzando il componente Immagine di base (NPR-36879).
* [!DNL Experience Manager Sites] L’interfaccia utente amministratore con un numero elevato di modelli si traduce in una navigazione lenta (NPR-36870).
* L&#39;aggiornamento al service pack 9 impedisce l&#39;authoring di alcuni componenti. Questo problema non consente agli utenti [!DNL Sites] di creare nuove pagine (NPR-36857).
* Il metodo `ContextHubImpl` crea un elemento `ResourceResolver` non chiuso. Questo porta a messaggi di avviso sull&#39;esecuzione di `ResourceResolver` e il servizio restituisce a volte risultati imprevisti (NPR-36853).
* Quando si sincronizza una singola Live Copy dalle proprietà della pagina blueprint, vengono sincronizzate anche tutte le altre Live Copy (NPR-36829, NPR-36522).
* Quando si utilizza solo il tipo MIME XLS, la funzione di caricamento del file non funziona come previsto (NPR-36785).
* I nuovi tag con maiuscole e minuscole e tutte le parole maiuscole non vengono visualizzati nel campo tag all’interno di [!DNL Content Fragments] (NPR-36742).
* L’opzione Elemento di testo singolo quando si aggiunge un elemento [!DNL Content Fragment] causa la mancanza di testo e la creazione di una formattazione dispari relativa agli elenchi e agli elenchi nidificati (NPR-36565).
* Quando un autore annota un componente in una pagina, lo elimina ed esegue un’azione di annullamento sull’operazione di eliminazione, si verifica un errore durante il tentativo di visualizzare i dati Timeline per la pagina nella console Sites (NPR-36528).
* L&#39;opzione [!UICONTROL Salva e chiudi] delle proprietà pagina consente di salvare le modifiche ma non di chiudere l&#39;editor (NPR-36527).
* Quando un utente tenta di trascinare un nuovo componente Testo in una pagina, il componente scompare immediatamente (NPR-36442).
* Quando un utente digita in un tag on-demand che include spazio (il tag che non esiste sul sistema) e preme Invio, il tag viene visualizzato sotto il campo . Tuttavia, quando il [!DNL Content Fragment] viene salvato e riaperto, il tag on-demand non viene visualizzato (NPR-36441).
* Non è possibile eliminare il modello quando si accede all’istanza tramite il Dispatcher (NPR-36385).
* Quando una pagina viene spostata, è necessario un aggiornamento manuale del browser per eseguire il rendering delle modifiche (NPR-36381).
* Quando selezioni un componente, puoi tagliarlo o copiarlo con Ctrl+X o Ctrl+C (e Comando+X o Comando+C su Mac). Quando fai clic su un altro componente, puoi incollarlo con la barra degli strumenti, ma non con la tastiera (Ctrl+V o Comando+V) (NPR-36379).
* Quando un utente prova a tagliare i componenti utilizzando l’icona forbici per spostarli in un altro punto, si verifica un errore di console. Inoltre, quando si incolla un solo componente viene spostato (NPR-36378).
* [!DNL Experience Manager] ha una query senza indice su WCM o notifiche, rallenta le prestazioni (NPR-36303).
* Quando un autore ripristina l’ereditarietà del componente ereditato eliminato, l’opzione disponibile è quella di sincronizzare tutto il contenuto della pagina. Gli autori dei contenuti devono sincronizzare la pagina completa anche se l’ereditarietà viene ripristinata solo su un componente. Una sincronizzazione completa può causare la sincronizzazione dei contenuti indesiderati (NPR-34456, CQ-4310183).
* L’utilizzo live di un componente nell’istanza di authoring non visualizza tutte le occorrenze. Alcuni componenti vengono utilizzati in più di 1000 pagine, ma il rapporto visualizza solo circa 40 pagine (CQ-4323724).
* In presenza di una struttura del sito con molte pagine secondarie, in Experience Manager 6.5.8 il caricamento delle pagine secondarie nella vista a colonne richiede più tempo rispetto all’Experience Manager 6.4.8.2 (CQ-4322766).
* Deseleziona l’opzione &quot;All&quot; (Tutto) non funziona sull’opzione &quot;Rollout pagina&quot; (NPR-37070).
* Quando si apre una versione di un componente v3 esistente di una pagina, la finestra di dialogo Proprietà pagina non si apre e viene registrato un `NullPointerException` (SITES-1830).

### [!DNL Assets] {#assets-65100}

I seguenti problemi sono risolti in [!DNL Assets]:

* Il valore della proprietà `jcr:title` non viene aggiornato nell’istanza Pubblica dopo lo spostamento di una cartella. Se si rinomina e si ripubblica una cartella all’interno dell’istanza di authoring, il valore della proprietà `jcr:title` non viene aggiornato nell’istanza di pubblicazione (NPR-36369).

* Se sono selezionate due o più risorse e si modificano uno o più campi di metadati, l’operazione di salvataggio non riesce con il codice di errore 500 nel browser Safari (NPR-36413).

* L&#39;importazione dei metadati in blocco non riesce a causa di un formato di data non corretto (NPR-36428).

* Quando si effettua una selezione nella pagina [!UICONTROL Proprietà] per aggiornare i metadati, l&#39;interfaccia risponde lentamente quando sono presenti molte opzioni fornite dallo schema (NPR-36430).

* Il filtro di ricerca che utilizza il predicato [!UICONTROL Stato scadenza] non funziona (NPR-36436).

* Il menu a comparsa per vari campi nelle proprietà [!UICONTROL Folder Metadata] non visualizza gli ultimi valori selezionati (NPR-36937, CQ-4314429).

* Durante la ricerca di file e cartelle, se l&#39;utente applica un filtro e seleziona [!UICONTROL File e cartelle], vengono visualizzati solo i file ma non la cartella (CQ-4319543, NPR-36627).

* Le opzioni della barra degli strumenti sono diverse quando la stessa raccolta è selezionata all’interno di una cartella e quando è selezionata da un risultato di ricerca (NPR-36620).

* L&#39;opzione [!UICONTROL Pubblicazione rapida] non è disponibile nella pagina dei risultati di ricerca (NPR-36904, CQ-4317748).

* Quando gli utenti creano una Live Copy di una risorsa senza specificarne l’estensione, dopo il download il file Live Copy non è utilizzabile (NPR-36903, CQ-4326305).

* Quando un utente viene aggiunto come proprietario di una cartella figlio, l&#39;utente ottiene l&#39;autorizzazione del proprietario anche della sua cartella padre e quindi delle altre cartelle figlio del padre. Inoltre, l&#39;utente non viene rimosso come proprietario della cartella principale quando si tenta di rimuoverlo. (NPR-36801, CQ-4323737)

* [!DNL Experience Manager] genera un’eccezione di memoria esaurita quando si tenta di creare risorse secondarie per risorse composte, ad esempio una presentazione PowerPoint (NPR-36668).

* Quando gli utenti spostano una risorsa già utilizzata in una pagina dei siti pubblicata, la pagina dei siti viene pubblicata nuovamente anche se l’opzione di pubblicazione non è selezionata (NPR-36636, CQ-4323500).

* Quando utilizzi la funzione di rilevamento del tipo MIME Apache Tika, le risorse caricate utilizzando il metodo `AssetManager.createAsset` lasciano un file temporaneo denominato `apache-tika-*.tmp` nella directory temporanea. Questo file temporaneo utilizza tutto lo spazio libero su disco disponibile (NPR-36545).

* Vengono scaricate tutte le risorse protette da DRM e non viene seguita la selezione degli utenti per scaricare risorse specifiche (CQ-4327422).

* Non è possibile trascinare risorse su `pathfield` nell’interfaccia utente di (NPR-36849).

* Quando selezioni una risorsa nella vista a colonne, il pannello dei dettagli della risorsa scompare (NPR-36667).

### [!DNL Dynamic Media] {#dynamic-media-65100}

**Miglioramenti dell’accessibilità**

I seguenti miglioramenti dell’accessibilità sono disponibili in [!DNL Dynamic Media Viewers].

* Gli assistenti vocali ora leggono il testo segnaposto per cercare e aggiungere l’indirizzo e-mail come campo obbligatorio nella condivisione delle risorse come finestra di dialogo di collegamento e annunciano anche la [!UICONTROL Compila questo campo] descrizione comando (CQ-4327761).

* Gli assistenti vocali ora segnalano correttamente i nomi e le finalità di vari campi nell’ [!UICONTROL Editor predefiniti immagine] sull’accesso ai campi dell’interfaccia utente tramite tastiera (CQ-4325677).

* Lo stato attivo della tastiera ora si sposta in modo appropriato nella scheda di ricerca della finestra di dialogo [!UICONTROL Predefiniti visualizzatore] dal selettore delle risorse dell’opzione [!UICONTROL Tipo di contenuti multimediali avanzati] (CQ-4324736).

* Quando si naviga in modalità moduli utilizzando i tasti della tastiera, gli assistenti vocali leggono le etichette corrispondenti alle opzioni di incremento e decremento nella scheda [!UICONTROL Crea] di [!UICONTROL Predefiniti immagine] (CQ-4323900).

* Gli assistenti vocali ora annunciano l’opzione [!UICONTROL Cerca e aggiungi indirizzo e-mail] nella finestra di dialogo condividi risorse come collegamento (CQ-4323352).

* Lo stato attivo sulla tastiera viene mantenuto sulla barra degli strumenti quando si navigano le risorse utilizzando i tasti di scelta rapida (CQ-4322037).

* Gli assistenti vocali ora leggono le informazioni sul campo [!UICONTROL Modifica] appena aggiunte dopo aver selezionato l&#39;opzione [!UICONTROL Aggiungi ritaglio] all&#39;interno della pagina [!UICONTROL Ritaglio immagine reattivo] in [!UICONTROL Modifica profilo elaborazione immagine] (CQ-4290734).

* Nelle pagine [!UICONTROL Modifica predefinito immagine] e [!UICONTROL Crea video interattivo] , gli assistenti vocali ora annunciano in modo appropriato l’intestazione della pagina quando si navigano nelle pagine utilizzando i tasti di scelta rapida della tastiera dell’intestazione (CQ-4290730)(CQ-4290701).

* Gli assistenti vocali ora possono riconoscere le varie aree dello schermo (ad esempio l’area del pannello di destra, il pannello di sinistra, la barra delle azioni, il punto di riferimento della barra degli strumenti del visualizzatore e il punto di riferimento dell’immagine zoomabile) utilizzando punti di riferimento e tasti di scelta rapida di regione durante la navigazione nelle pagine seguenti.

   * [!UICONTROL Editor predefiniti per visualizzatori]  (CQ-4290729)

   * [!UICONTROL Editor set di immagini]  (CQ-4290710)

   * [!UICONTROL Creazione di video interattivi]  (CQ-4290702).

* Gli assistenti vocali ora annunciano il nome dell’opzione Condividi nel fotogramma video quando si naviga utilizzando il tasto freccia giù (CQ-4290728).

* Gli assistenti vocali ora segnalano i nomi delle varie opzioni nelle schede [!UICONTROL Sprite] e [!UICONTROL Sfondo] nella scheda [!UICONTROL Aspetto] in [!UICONTROL Editor predefiniti visualizzatore] (CQ-4290727).

* I campi obbligatori, come il campo da modificare [!UICONTROL Larghezza], nella scheda [!UICONTROL Base] di [!UICONTROL Modifica codifica video] dispongono ora di un simbolo asterisco (*) (CQ-4290725).

* Gli assistenti vocali ora annunciano l’etichetta per le opzioni nella pagina [!UICONTROL Profili immagine] (CQ-4290723).

* Gli utenti Windows possono ora spostarsi fuori dall’editor CSS espanso su [!UICONTROL Editor predefiniti visualizzatore] quando lo stato attivo è sull’editor CSS (CQ-4290720).

* Nella scheda [!UICONTROL Base] di [!UICONTROL Modifica predefinito immagine] durante la navigazione in modalità Modulo, gli assistenti vocali ora leggono le etichette per vari campi e opzioni di modifica (CQ-4290717).

* Gli assistenti vocali ora leggono il ruolo e lo stato (selezionato o non selezionato) delle opzioni dell’interfaccia utente nella navigazione a sinistra nella pagina dei dettagli delle risorse (CQ-4290709).

* Gli assistenti vocali ora comunicano correttamente lo stato (selezionato o non selezionato) e il collegamento per l’immagine viene attivato nella scheda [!UICONTROL Contenuto] della pagina [!UICONTROL Crea video interattivo] (CQ-4290707).

* Gli assistenti vocali ora segnalano correttamente nome, ruolo e stato di vari segmenti nella scala cronologica del video durante la navigazione tramite il tasto freccia giù nella pagina [!UICONTROL Crea video interattivo] (CQ-4290706).

* Gli assistenti vocali ora leggono nome, ruolo e stato predefinito (selezionato o non selezionato) e proprietà durante la navigazione nelle opzioni della pagina [!UICONTROL Crea video interattivo] (CQ-4290704).

* Gli assistenti vocali ora leggono il nome, il ruolo e lo stato predefinito (selezionato o non selezionato) delle opzioni in [!UICONTROL Tutte le risorse] e [!UICONTROL Tutte le raccolte] durante la navigazione nella pagina [!UICONTROL Pubblica] (CQ-4290705).

* Quando carichi un formato video non supportato (diverso da MP4) nella pagina [!UICONTROL Crea video interattivo], in Experience Manager vengono visualizzati e annunciati messaggi di errore (CQ-4290700).

* Il contrasto dei numeri (tempo in secondi) nella scala della timeline sulla pagina [!UICONTROL Crea video interattivo] ora soddisfa il rapporto di luminosità minimo richiesto, in modo che gli utenti con una percezione limitata del colore possano facilmente leggere (CQ-4290699).

* Gli assistenti vocali ora annunciano l’etichetta per il campo [!UICONTROL Nome prodotto] quando si naviga nella pagina [!UICONTROL Crea video interattivo] (CQ-4290697).

**Problemi risolti**

Le seguenti correzioni di bug sono disponibili in [!DNL Dynamic Media].

* I video caricati su [!DNL Experience Manager] visualizzano `Process failed` dopo che la modalità di esecuzione `dynamicmedia_scene7` è abilitata e la sincronizzazione è disabilitata (CQ-4327791).

### Platform {#platform-65100}

I seguenti miglioramenti sono forniti in questo service pack:

* Quando un utente seleziona un elemento nella vista Struttura, gli assistenti vocali annunciano la selezione e le opzioni della barra degli strumenti visualizzate nella parte superiore (NPR-36504).
* Alcuni nomi di testo e di controllo sono più facili da leggere per gli utenti con problemi di vista, in quanto il rapporto di luminosità soddisfa il rapporto minimo richiesto di 4,5:1 (NPR-36503).
* Quando un utente utilizza i controlli del calendario, l’assistente vocale legge le informazioni relative a data, mese e giorno della settimana. Quando un utente utilizza il tasto di scelta rapida del calendario, l’assistente vocale legge la modifica di data, mese e anno (NPR-36498).
* Supporto fornito per eseguire JavaScript personalizzato `Clientlibs` utilizzando le funzioni ECMAScript 6 senza rispettare la modalità rigorosa. Nello specifico, il flag `emitUseStrict` viene aggiunto al `GCCScriptProcessor` (NPR-36411).

Le seguenti correzioni di bug fanno parte di questo service pack:

* I controlli di integrità personalizzati vengono eseguiti più frequentemente del previsto (NPR-36985).
* Il metodo `Resourceresolver map` restituisce un risultato non corretto per le pagine di alias (NPR-36767).
* [!DNL Experience Manager] L&#39;avvio è ritardato a causa del caricamento dei flussi di lavoro (NPR-36615).

### Integrations (Integrazioni) {#integrations-65100}

* L&#39;Experience Manager non risponde quando il nodo principale MongoDB passa a un altro nodo (NPR-36566).
* [!DNL Sling content distribution] non riesce quando si esegue l&#39;operazione di eliminazione dei membri della raccolta (NPR-36521, CQ-4323578).

### Interfaccia utente {#user-interface-65100}

* Il pannello laterale **[!UICONTROL Riferimenti]** non visualizza i riferimenti a risorse e siti (GRANITE-35078, GRANITE-34892).

### Progetti di traduzione {#translation-65100}

* Le sottopagine supplementari in una copia in lingua di un progetto di traduzione multipla vengono eliminate (NPR-36622).

### Flusso di lavoro {#workflow-65100}

* Se il server riceve un messaggio fuori sede, segnala gli avvisi di memoria e smette di rispondere (NPR-36768).

### [!DNL Communities] {#communities-65100}

* Le pagine dei siti della community si aprono nello stato `LoggedIn` per gli utenti anonimi (NPR-36908).

* Quando è presente più di una pagina nella pagina **[!UICONTROL Community]** > **[!UICONTROL Idee]** > **[!UICONTROL Commenti]**, la navigazione delle pagine non funziona (NPR-36541).

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}

>[!NOTE]
>
>* Per [!DNL Experience Manager Forms] vengono rilasciati pacchetti del componente aggiuntivo una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager].


**Moduli adattivi**

<!--

* When the validations performed on the field values in an adaptive form are successful, [!DNL AEM Forms] fails to invoke the Form Data Model (CQ-4325491).

-->

* Quando aggiungi un dizionario di lingua a un progetto di traduzione e quindi apri il progetto, [!DNL AEM Forms] visualizza un messaggio di errore (CQ-4324933):

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* Problemi di prestazioni dopo l&#39;installazione di [!DNL AEM Forms] Service Pack 7 (CQ-4326828).

**Gestione della corrispondenza**

* Ritardo nella visualizzazione dei caratteri nella scheda [!UICONTROL Dati] e nell&#39;anteprima della lettera HTML (NPR-37020).

* Durante la modifica di un frammento di documento di testo, le nuove parole vengono visualizzate come tag HTML dopo il salvataggio del frammento (NPR-36837).

* Impossibile visualizzare le lettere salvate come bozze (NPR-36816).

* Quando si modifica un frammento di documento di testo e si visualizza l’anteprima della lettera, AEM Forms visualizza la lingua dell’espressione nell’anteprima della lettera HTML (CQ-4322331).

* Problemi durante il rendering dei dati con un modello di lettera self-service (NPR-37161).


**Comunicazioni interattive**

* Un carattere di tabulazione duplica tra due parole ogni volta che si stampa l’anteprima di una comunicazione interattiva dopo la modifica di un frammento di documento di testo (NPR-37021).

* [!DNL AEM Forms] visualizza un errore quando salvi un frammento di documento di testo che supera il limite di dimensione massima (NPR-36874).

* Quando aggiungi un’immagine a una comunicazione interattiva, dopo l’immagine viene visualizzato un ulteriore blocco vuoto (NPR-36659).

* Quando selezioni tutto il testo in un editor, non puoi modificare il testo del font in Arial (NPR-36646).

<!--

* When you create a URL in an editor and preview the changes, a black background displays instead of the URL text (NPR-36640).

-->

* Quando copi e incolla del testo in un editor, si verificano problemi durante la modifica del font in Arial per i punti elenco disponibili nel documento (NPR-36628).

* Problemi di rientro per i punti elenco nell’editor di testo (NPR-36513).

<!--
**Designer**

* Screen Reader fails to read floating field data placed inside text label on the Master page or on Subform pages in a dynamic PDF (CQ-4321587).

-->

**Servizi documentali**

* Quando si convertono file XDP in file PDF e si assembla il PDF risultante, le generazioni PDF non riescono e visualizza il seguente messaggio di errore (CQ-4328666):

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Flusso di lavoro per moduli**

* Impossibile inviare un modulo a un processo Workbench dopo l&#39;aggiornamento ad AEM Forms Service Pack 8 (CQ-4325846).

**Moduli HTML5**

* Quando imposti il valore della proprietà `mfAllowAttachments` come `True` nell’archivio CRX DE, il `dataXml` viene danneggiato durante l’invio del modulo HTML5 (NPR-37035).

* Quando esegui il rendering di un file XDP come HTML utilizzando `dataXml`, [!DNL AEM Forms] visualizza un errore `Page Unresponsive` (NPR-36631).

### Commerce {#commerce-65100}

* Il valore visualizzato nel campo **[!UICONTROL Pubblicato da]** non è corretto nella vista a colonne (NPR-36902).
* Quando viene introdotto un catalogo, i nuovi prodotti vengono erroneamente contrassegnati come prodotti modificati (NPR-36666).
* Quando crei nuovamente un prodotto eliminato, la pagina del prodotto non viene ricreato (NPR-36665).
* Le pagine modificate vengono aggiornate, ma i prodotti collegati corrispondenti non vengono aggiornati sul rollout del catalogo (CQ-4321409, NPR-36422).
* I flussi di lavoro **[!UICONTROL Pubblica più tardi]** e **[!UICONTROL Annulla pubblicazione più tardi]** non funzionano (CQ-4327679).

Per informazioni sugli aggiornamenti di sicurezza, vedere [[!DNL Experience Manager] pagina dei bollettini sulla sicurezza](https://helpx.adobe.com/security/products/experience-manager.html).

## Installare la versione 6.5.10.0 {#install}

**Requisiti di configurazione e ulteriori informazioni**

* Experience Manager 6.5.10.0 richiede Experience Manager 6.5. Per istruzioni dettagliate, consulta la [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) .
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* In una distribuzione con MongoDB e più istanze, installa Experience Manager 6.5.10.0 in una delle istanze Autore utilizzando Gestione pacchetti.

>[!NOTE]
>
>Adobe sconsiglia di rimuovere o disinstallare il pacchetto [!DNL Adobe Experience Manager] 6.5.10.0.

### Installare il service pack {#install-service-pack}

Per installare il service pack su un&#39;istanza [!DNL Adobe Experience Manager] 6.5, segui questi passaggi:

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia un riavvio se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di installare, scegli uno snapshot o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip).

1. Apri Gestione pacchetti e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l&#39;istanza dopo l&#39;installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l&#39;istanza. Consulta [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude durante l’installazione del service pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere questo problema si verifica nel browser [!DNL Safari] ma può verificarsi a intermittenza su qualsiasi browser.

**Installazione automatica**

Esistono due modi per installare automaticamente [!DNL Experience Manager] 6.5.10.0 in un&#39;istanza di lavoro:

A. Posiziona il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.

B. Utilizza l’ [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizza `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0 non supporta l’installazione di Bootstrap.

**Convalida l&#39;installazione**

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.10.0)` in [!UICONTROL Prodotti installati].

1. Tutti i bundle OSGi sono **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** nella console OSGi (Usa la console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.3 o successiva (Usa console Web: `/system/console/bundles`).

Per conoscere le piattaforme certificate per l’utilizzo con questa versione, consulta i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

### Installare il pacchetto aggiuntivo di Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora questa sezione se non utilizzi Experience Manager Forms. Le correzioni apportate in Experience Manager Forms vengono distribuite tramite un pacchetto aggiuntivo separato una settimana dopo il rilascio pianificato di [!DNL Experience Manager] Service Pack .

1. Assicurati di aver installato il Service Pack di Adobe Experience Manager.
1. Scarica il pacchetto corrispondente dei componenti aggiuntivi per Forms elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) per il sistema operativo in uso.
1. Installa il pacchetto aggiuntivo di Forms come descritto in [Installazione dei pacchetti aggiuntivi di AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 include una nuova versione di [Pacchetto di compatibilità AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). Se utilizzi una versione precedente del pacchetto di compatibilità di AEM Forms e aggiorni ad Experience Manager 6.5.10.0, installa la versione più recente del pacchetto dopo l’installazione del pacchetto aggiuntivo di Forms.

<!--

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

UberJar per Experience Manager 6.5.10.0 è disponibile nell’ [archivio centrale Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/).

Per utilizzare UberJar in un progetto Maven, consulta [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell’archivio centrale Maven invece dell’archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale viene rinominato in `uber-jar-<version>.jar`. Pertanto, non esiste `classifier`, con `apis` come valore, per il tag `dependency`.

## Funzioni obsolete {#removed-deprecated-features}

Di seguito è riportato un elenco di funzioni e funzionalità contrassegnate come obsolete con [!DNL Experience Manager] 6.5.7.0. Le funzioni vengono contrassegnate come obsolete inizialmente e successivamente rimosse in una versione futura. È disponibile un’opzione alternativa.

Controlla se utilizzi una funzione o una funzionalità in una distribuzione. Inoltre, pianifica di modificare l’implementazione in modo da utilizzare un’opzione alternativa.

| Area | Funzione obsoleta | Sostituzione |
|---|---|---|
| Integrations (Integrazioni) | La schermata **[!UICONTROL Opt-in di AEM Cloud Services]** è obsoleta perché l’ integrazione [!DNL Experience Manager] e [!DNL Adobe Target] viene aggiornata all’Experience Manager 6.5. L’integrazione supporta l’API di Adobe Target Standard. L’API utilizza l’autenticazione tramite Adobe IMS e [!DNL Adobe I/O] e supporta il ruolo crescente di Adobe Launch per dotare le pagine [!DNL Experience Manager] di analisi e personalizzazione, la procedura guidata di consenso è funzionalmente irrilevante. | Configura le connessioni di sistema, l’autenticazione Adobe IMS e le integrazioni [!DNL Adobe I/O] tramite i rispettivi servizi cloud [!DNL Experience Manager]. |
| Connettori | Il connettore Adobe JCR per Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 è obsoleto, ad Experience Manager 6.5. | N/D |

## Problemi noti {#known-issues}

<!--

* (For JBoss on Microsoft Windows only) To continue using the Create PDF service on [!DNL AEM Forms on JEE], download [omniORB_4.1.1_x86_win32_vc10.zip](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/omniORB_4.1.1_x86_win32_vc10.zip) from Software Distribution, extract and copy the folder available in the Zip file to the following location:
`[AEM Forms Installation]\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\CommonNatives\lib`

* As [!DNL Microsoft Windows Server 2019] does not support [!DNL MySQL 5.7] and [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] does not support turnkey installations for [!DNL AEM Forms 6.5.10.0].

-->

* Se aggiorni l’istanza [!DNL Experience Manager] dalla versione 6.5 alla versione 6.5.10.0, puoi visualizzare le eccezioni `RRD4JReporter` nel file `error.log` . Per risolvere il problema, riavvia l&#39;istanza.

* Se si installa [!DNL Experience Manager] 6.5 Service Pack 10 o un service pack precedente su [!DNL Experience Manager] 6.5, la copia in runtime del modello di flusso di lavoro personalizzato delle risorse (creato in `/var/workflow/models/dam`) viene eliminata.
Per recuperare la copia runtime, Adobe consiglia di sincronizzare la copia in fase di progettazione del modello di flusso di lavoro personalizzato con la relativa copia in fase di esecuzione utilizzando l’API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Gli utenti possono rinominare una cartella in una gerarchia in [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Durante l’installazione di Experience Manager 6.5.x.x possono essere visualizzati i seguenti errori e messaggi di avviso:
   * &quot;Quando l’integrazione di Adobe Target è configurata in Experience Manager utilizzando l’API di Target Standard (autenticazione IMS), l’esportazione di frammenti di esperienza in Target comporta la creazione di tipi di offerta errati. Invece del tipo “Frammento esperienza”/source “Adobe Experience Manager”, in Target vengono create diverse offerte con il tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * La convalida lato server del modulo adattivo non riesce quando si utilizzano funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Non è stata trovata alcuna finestra di manutenzione in granite/operations/maintenance.
   * Il punto attivo in un’immagine interattiva di Dynamic Media non è visibile quando si visualizza l’anteprima della risorsa tramite il visualizzatore di banner acquistabili.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Timeout in attesa del completamento della modifica del registro.

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.10.0:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5.10.0](assets/65100_bundles.txt)

* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.10.0](assets/65100_packages.txt)

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* Consulta [come contattare l&#39;Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Note sulla versione 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] pagina di prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

