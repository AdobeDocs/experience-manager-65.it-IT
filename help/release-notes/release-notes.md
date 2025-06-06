---
title: Note sulla versione per  [!DNL Adobe Experience Manager] 6.5
description: Trova informazioni sulla versione, novità, procedure di installazione e un elenco dettagliato delle modifiche per  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 8cbf7188baf8cc997e0747be366f13c3b6c2c632
workflow-type: tm+mt
source-wordcount: '4590'
ht-degree: 2%

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
| Versione | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | Giovedì 22 maggio 2025 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.23.0 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti e correzioni di bug. Include inoltre miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotti dopo la data di disponibilità iniziale di 6.5 di aprile 2019. [Installa il Service Pack ](#install) in [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funzioni principali e miglioramenti

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Moduli {#forms-sp23}

Le funzionalità e i miglioramenti principali di questa versione includono:

* [Collegamenti ipertestuali accessibili con stili di testo misti nei PDF statici](https://helpx.adobe.com/content/dam/help/it/experience-manager/6-5/forms/pdf/using-designer.pdf): i collegamenti ipertestuali contenenti stili di testo misti nei PDF statici sono ora contrassegnati come un singolo elemento accessibile. Questo miglioramento semplifica la struttura ad albero dei tag, migliora la navigazione degli assistenti vocali e supporta una migliore conformità in materia di accessibilità.

* [Matrice di piattaforma supportata aggiornata](/help/forms/using/aem-forms-jee-supported-platforms.md)

  La versione più recente introduce aggiornamenti alla matrice di piattaforma supportata, garantendo la compatibilità con le tecnologie più recenti.

   * Client IBM Content Manager 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Driver JDBC Microsoft® SQL Server 12.8

   * Microsoft® Office 2021

   * Red Hat® Enterprise Linux® 9 (kernel 4.x, 64 bit) 



* [Componente allegato file protetto](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): come misura di sicurezza, il componente ora impedisce l&#39;invio di file con estensioni modificate che tentano di ignorare i controlli dei tipi di file consentiti. Tali file vengono bloccati durante l’invio per garantire che siano accettati solo i tipi di file validi.

<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## Problemi risolti in Service Pack 23 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### Accessibilità {#sites-accessibility-6523}

* Le sezioni Canvas nelle pagine dell’Editor di AEM ora supportano l’accessibilità completa da tastiera. Gli utenti possono attivare i titoli delle sezioni e i pulsanti di modifica utilizzando solo la tastiera, senza dover passare con il mouse. Questo aggiornamento garantisce la conformità a WCAG 2.1.1 e migliora l’usabilità tra i componenti quali i moduli Teaser, Immagine, Carosello, Layout, Alterazione tempo e Annotazione. (SITES-25256) <!-- 6.5 LTS SP1 -->
* È stato risolto un problema di accessibilità nell’Editor pagina di AEM a causa del quale lo stato attivo sulla tastiera si ripristina all’inizio della barra degli strumenti Demografica dopo l’attivazione di pulsanti come Persona, Carrello o Abbandonato. Ora è attivo il pulsante attivato per supportare flussi di lavoro coerenti per la navigazione da tastiera e l’utilità di lettura dello schermo. (SITES-25306)
* È stato risolto un problema critico di accessibilità nell’Editor pagina di AEM a causa del quale gli elementi dell’area di lavoro in più finestre di dialogo e modalità (ad esempio, barra delle risorse o anteprima del layout) non potevano essere utilizzati utilizzando solo una tastiera. Tutti gli elementi dell’area di lavoro interattiva ora supportano la navigazione solo da tastiera, garantendo la conformità al criterio di successo WCAG 2.1.1 (SITE-25256)
* È stato risolto un problema di accessibilità nell’interfaccia utente di amministrazione di Sites a causa del quale le voci di elenco interattive nel pop-up Crea utilizzavano ruoli ARIA errati. Agli elementi che si comportavano come collegamenti veniva assegnato `role="listitem"` invece di `role="menuitem"`, violando i pattern di progettazione ARIA e confondendo gli assistenti vocali. Gli aggiornamenti garantiscono che tutti i componenti dell’elenco seguano i ruoli semantici appropriati per migliorare il supporto della tastiera e della tecnologia per l’accessibilità. (SITES-24493)
* È stato risolto il problema di associazione delle etichette di accessibilità per i campi titolo pagina e tag. L’interfaccia di AEM ora associa correttamente le etichette di accessibilità ai campi &quot;Titolo&quot; e &quot;Titolo pagina&quot; quando si utilizzano utilità per la lettura dello schermo come JAWS. La correzione assicura la corretta lettura delle etichette e migliora la conformità ADA nei flussi di lavoro di creazione, proprietà e spostamento delle pagine. (SITES-27149)
* È stato risolto un problema di accessibilità relativo all’identificazione delle tabelle nella finestra di dialogo delle autorizzazioni. La tabella delle autorizzazioni in AEM ora utilizza i ruoli e gli attributi ARIA corretti per garantire che gli assistenti vocali come JAWS la identifichino correttamente come tabella. La correzione migliora la conformità in materia di accessibilità e garantisce che gli utenti ricevano annunci accurati relativi alla navigazione e ai contenuti. (SITES-27140)
* È stata corretta l’etichetta visiva mancante per i campi di input dei commenti nella timeline. Sono state corrette le etichette visive mancanti per i campi di input &quot;commento&quot; nella sezione timeline per migliorarne l’accessibilità. L’aggiornamento garantisce che gli assistenti vocali possano annunciare con precisione le etichette dei campi. Questa esperienza migliora la navigazione e l’invio dei moduli per tutti gli utenti, in particolare gli utenti che si basano su tecnologie per l’accessibilità. (SITES-26903)
* È stata corretta l’accessibilità da tastiera per il pulsante con puntini di sospensione nei commenti della timeline. Attivazione della navigazione tramite tastiera per il pulsante con puntini di sospensione (tre punti) accanto ai commenti nella sezione timeline. Gli utenti possono ora accedere al pulsante e interagire con esso utilizzando il tasto TAB, migliorando l’accessibilità per gli utenti che si affidano alla navigazione tramite sola tastiera. (SITES-26891)
* Sono stati migliorati gli annunci NVDA/Assistente vocale per i risultati di ricerca nelle finestre di dialogo di selezione. È stata aggiornata la finestra di dialogo Apri selezione per indicare se i risultati della ricerca vengono trovati o meno quando si utilizzano utilità per la lettura dello schermo, come NVDA o Assistente vocale. Questo miglioramento consente agli utenti che si affidano alle tecnologie per l’accessibilità di comprendere il risultato delle azioni di ricerca senza bisogno di conferma visiva. (SITES-26883)
* È stato corretto il ruolo ARIA per l’icona con i puntini di sospensione accanto al campo di input del commento. È stata aggiornata l’icona con i puntini di sospensione (tre punti) accanto al campo di immissione del commento per utilizzare il ruolo ARIA corretto, in modo che gli assistenti vocali possano identificare con precisione l’elemento. Questo miglioramento migliora la conformità in materia di accessibilità e l’esperienza degli utenti che si affidano alle tecnologie per l’accessibilità. (SITES-26881)
* Sono stati corretti gli attributi ARIA non validi nei componenti dell’interfaccia utente Coral. Sono stati aggiornati i componenti dell’interfaccia utente Coral per garantire che tutti gli attributi ARIA utilizzino valori validi, migliorando l’accessibilità e la conformità. In particolare, sono stati risolti casi in cui valori non validi come `aria-modal="dialog"` non venivano assegnati correttamente. Questo miglioramento consente agli assistenti vocali di interpretare correttamente gli elementi delle finestre di dialogo, migliorando l’accessibilità per gli utenti che si affidano a tecnologie per l’accessibilità. (SITES-26873)
* Sono state migliorate la visibilità e le descrizioni per le icone negli scenari di riversamento. È stato migliorato il comportamento di riversamento per garantire la corretta visualizzazione delle descrizioni per le icone **Scarica**, **Rielabora risorse** e **Estrai**. Focalizzato su un problema di accessibilità in cui le icone e le relative etichette diventavano invisibili quando il riquadro di visualizzazione veniva ridimensionato o le impostazioni di zoom del browser cambiavano. Questa correzione consente agli utenti ipovedenti di mantenere la visibilità e fornire descrizioni delle icone durante il reflow. (SITES-26871)

#### Interfaccia utente amministratore{#sites-adminui-6523}

È stata corretta l&#39;eccezione Servizio URL di Universal Editor con endpoint Externalizer mancanti. Il servizio URL di Universal Editor ora gestisce gli endpoint mancanti relativi all’authoring, alla pubblicazione o all’esternalizzazione locale senza generare eccezioni. Gli utenti amministratori possono aprire l’Editor pagina correttamente anche quando alcune configurazioni di Externalizer sono incomplete. (SITES-28877) <!-- LTS -->

#### Interfaccia classica{#sites-classicui-6523}

* Nelle finestre di dialogo dell’interfaccia classica, si verificava un problema che impediva di visualizzare nuovamente un’area di testo quando si faceva clic su un pulsante. La correzione assicura che l&#39;area di testo riappaia correttamente quando viene attivata, ripristinando il comportamento previsto ed evitando interruzioni nei flussi di lavoro delle finestre di dialogo dinamiche. (SITES-30230)
* È stata corretta la funzionalità di ricerca di risorse immagine dell’interfaccia classica interrotta dopo l’aggiornamento di Service Pack 22. Il mirino delle risorse dell’immagine dell’interfaccia classica ora gestisce correttamente i nomi delle risorse contenenti spazi o caratteri speciali. Questo aggiornamento assicura che il Finder risorse codifica correttamente i nomi dei file, evitando errori di ricerca e consentendo agli autori di individuare e selezionare le risorse immagine senza errori. (SITES-29151)

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* È stato corretto un errore di test di convalida per `DeleteVariationIT.testUpdateBasic`. Il test `DeleteVariationIT.testUpdateBasic` non ha più esito negativo durante l&#39;esecuzione della convalida del Service Pack. La correzione corregge un problema di mappatura del testo mancante nella logica di gestione JSON, garantendo la stabilità del test ed evitando inutili interruzioni del test. (SITES-28022)
* AEM ora evita il deterioramento delle prestazioni causato da metadati XMP non validi nelle risorse immagine. Assets che contiene nomi di proprietà XMP non validi o non conformi, ad esempio quelli con segmenti numerici o strutture non qualificate, non attiva più i registri di avviso ripetuti durante l’elaborazione. Il sistema filtra i metadati problematici per garantire che l’inserimento e la convalida delle risorse siano completati senza errori. (SITES-30683) <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - Editor frammenti{#sites-fragments-editor-6523}

Altri autori possono comunque pubblicare frammenti di contenuto anche quando un altro autore li estrae, il che è contrario al comportamento previsto della funzione di estrazione. Questa correzione impedisce ad altri utenti di visualizzare o utilizzare i pulsanti di pubblicazione nell’interfaccia di authoring quando viene estratto un frammento di contenuto. (SITES-30578) <!-- LTS -->

#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6523}

È stato corretto GraphQL QueryValidationError con schemi di frammenti di contenuto. L&#39;aggiornamento del bundle `cq-dam-cfm-graphql` corregge gli errori di convalida dello schema quando si utilizzano riferimenti a frammenti di contenuto. La correzione assicura il corretto funzionamento delle query GraphQL senza richiedere il riallineamento manuale dello schema o la ripubblicazione dopo le distribuzioni dei pacchetti. (SITES-27001) <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### Console Componenti{#sites-component-console-6523}

Sono stati apportati miglioramenti al caricamento della pagina &quot;Utilizzo live dei componenti&quot;. Ottimizza la pagina &quot;Utilizzo live dei componenti&quot; in AEM per impedire la visualizzazione di righe vuote durante lo scorrimento tra set di dati di grandi dimensioni. Gli utenti che caricano componenti con riferimenti di utilizzo estesi possono ora eseguire il caricamento continuo dei dati senza spazi vuoti o voci vuote. Questa esperienza migliora la navigazione nelle pagine, la precisione del tracciamento e l’efficienza di gestione nei rapporti sull’utilizzo dei componenti. (SITES-26454)

#### Back-end core{#sites-core-backend-6523}

* È stato corretto un errore nell’elenco delle risorse di Content Finder causato da nomi di risorse non validi. Content Finder ora gestisce correttamente i nomi delle risorse con caratteri non codificabili. L’elenco delle risorse nell’Editor pagina non ha più esito negativo o genera eccezioni quando si incontrano risorse con nomi problematici. (SITES-28722)
* Si è verificato un problema a causa del quale il componente `SearchPathLimiter` ha generato voci di registro eccessive stampando messaggi a livello ERROR per ogni chiamata. Questo comportamento è iniziato dopo Service Pack 17 e ha causato problemi di prestazioni a causa di volumi di registro estremamente elevati. La correzione riduce il livello di registro a DEBUG, riducendo in modo significativo il disturbo del registro e migliorando il monitoraggio del sistema e l&#39;efficienza diagnostica. (SITES-29835)
* I metadati di XMP formattati in modo non corretto hanno generato un errore durante l&#39;elaborazione delle risorse immagine in `ValidationDataServlet`. La correzione assicura la gestione dei metadati conforme ed evita l’analisi ridondante di proprietà non valide. (30683 DEL SITO) <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### Lanci{#sites-launches-6523}

* È stata corretta la visualizzazione della data di lancio tra il 25 dicembre e il 31 dicembre. L’interfaccia utente Lanci ora visualizza le date tra il 25 dicembre e il 31 dicembre con l’anno corretto. La correzione assicura che le date non vengano più visualizzate in modo errato nell’anno successivo, evitando confusione durante la pianificazione e la pianificazione delle campagne. (SITES-28706)
* Sono stati corretti i modelli AEM Launch non funzionanti dopo l’aggiornamento a Service Pack 22. I modelli di AEM Launch ora vengono caricati correttamente dopo un aggiornamento a Service Pack 22. La correzione corregge i dati non validi nelle configurazioni di avvio interne, consentendo agli utenti di visualizzare, modificare e creare lanci senza errori o campi mancanti. (SITES-28504)


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### Editor pagina{#sites-pageeditor-6523}

* È stato risolto un problema di caricamento di AssetPicker con risoluzioni dello schermo inferiori. AssetPicker ora carica correttamente le risorse quando gli utenti scorrono con risoluzioni dello schermo inferiori (1728×1117 o inferiori). Gli utenti non rilevano più le risorse mancanti durante lo scorrimento, migliorando la gestione delle risorse tra i diversi punti di interruzione del dispositivo. (SITES-28065)
* È stato corretto l’annuncio dell’utilità di lettura dello schermo mancante per le azioni di blocco e sblocco della pagina. L’Editor pagina ora annuncia correttamente il messaggio &quot;Info: La pagina è stata bloccata/sbloccata&quot; quando gli utenti attivano il pulsante di blocco/sblocco. La correzione migliora la conformità in materia di accessibilità e garantisce che gli utenti di utilità di lettura dello schermo ricevano aggiornamenti dinamici durante la modifica delle pagine. (SITES-27143)
* È stato migliorato il comportamento di attivazione della tastiera per le azioni dei componenti in AEM Authoring. È stata migliorata la navigazione da tastiera nello strumento AEM Author per garantire che lo stato attivo rimanga sul componente appena creato o selezionato dopo azioni quali Configura, Elimina o Converti. In precedenza, lo stato attivo veniva spostato nella parte superiore della pagina, causando problemi di conformità per l’accessibilità. Questo aggiornamento migliora l’esperienza utente degli utenti che utilizzano la tastiera e la tecnologia per l’accessibilità. In questo modo, si mantiene la progressione logica dello stato attivo all&#39;interno del flusso di lavoro di editing. (SITES-26549)
* È stata migliorata la navigazione tra schede nelle finestre di dialogo di creazione. Migliora la navigazione da tastiera nelle finestre di dialogo di AEM Author consentendo agli utenti di continuare a spostarsi in avanti dopo aver raggiunto la casella di modifica Descrizione. In precedenza, la funzione di focus trapping sul campo Description (Descrizione) bloccava l’ulteriore navigazione senza utilizzare combinazioni di tasti speciali. L’aggiornamento garantisce che gli utenti possano spostarsi facilmente tra i campi utilizzando solo il tasto TAB, migliorando la conformità in materia di accessibilità e l’esperienza utente. (SITES-26524)
* In AEM 6.5 Service Pack 22 è stata introdotta una regressione che impediva agli utenti di includere spazi nei titoli di Launch. La correzione ripristina la possibilità di utilizzare gli spazi, consentendo ai team di definire e organizzare i nomi di Launch in modo più flessibile, in linea con il comportamento previsto. (SITES-29414)
* È stato risolto un problema di ridimensionamento per i componenti all’interno dei Contenitori di layout dopo le azioni Nascondi/Mostra. L’Editor pagina ora calcola correttamente i valori delle colonne dopo aver nascosto e reso visibile un Contenitore di layout. Gli utenti possono ridimensionare i componenti senza errori e le colonne vengono visualizzate correttamente durante le azioni di ridimensionamento. (SITES-28463)
* Posizionamento errato del pulsante Struttura contenuto fisso nell’Editor pagina. L’Editor pagina ora posiziona correttamente il pulsante di configurazione della struttura del contenuto nella finestra di dialogo prevista &quot;Teaser intestazione&quot; invece della sezione errata. La correzione aggiorna il CSS per la finestra di dialogo Struttura contenuto in modo che utilizzi `top:0` invece di `bottom:0`, garantendo il corretto posizionamento dei pulsanti. (SITES-28448)


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### Editor Rich Text{#sites-rte-6523}

Correggi i tag `<br>` imprevisti nell&#39;Editor Rich Text con la modalità Incolla testo normale. L&#39;Editor Rich Text ora gestisce correttamente le operazioni di taglia e incolla quando si utilizza il testo normale `defaultPasteMode`. La correzione impedisce l&#39;inserimento di tag `<br>` imprevisti quando gli utenti tagliano e incollano testo all&#39;interno di campi Editor Rich Text, garantendo una formattazione pulita durante la modifica del contenuto. (SITES-27780)

#### Editor universale {#sites-universal-editor-6523}

* Quando si inviano ad AEM più richieste contenenti il parametro query, il cookie token di accesso potrebbe non essere restituito in tempo, il che potrebbe causare un accesso non riuscito. (SITES-30659) <!-- LTS -->
* Per garantire la compatibilità e il supporto con i gestori SAML, è necessario configurare la proprietà `service.ranking` in modo che il gestore `Query Token Auth` esegua *prima* del gestore `SAML Auth`. (SITES-29684)

### [!DNL Assets]{#assets-6523}

* I seguenti problemi si verificano nella pagina di navigazione on-premise [!DNL AEM] (6.5.22.0) dopo aver selezionato ![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL Assets &#x200B;]**, aver selezionato la cartella&#x200B;**[!UICONTROL &#x200B; Search Adobe Stock &#x200B;]**&#x200B;e aver selezionato un&#39;immagine di archivio:
   * L&#39;immagine stock selezionata non può essere concessa in licenza e salvata perché facendo clic su **[!UICONTROL Licenza e salvataggio]** viene visualizzato un elenco a discesa vuoto.
   * Selezionando l&#39;immagine Stock o immettendo nuovamente l&#39;URL della pagina Stock, si reindirizza alla home page di [!DNL AEM], impedendo l&#39;accesso all&#39;immagine Adobe Stock. (ASSETS-48687)
* Problemi durante la gestione delle cartelle se il nome della cartella include `/` nel nome nella pagina di navigazione locale [!DNL AEM] (6.5.22.0). (ASSETS-46740)
* In [!DNL AEM] 6.5, la pagina dei dettagli della risorsa non viene caricata dalla visualizzazione ![Raccolta](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL Raccolte &#x200B;]**&#x200B;a causa di un elevato utilizzo di memoria. (ASSETS-46738)
* Problemi di integrazione con [!DNL InDesign] come servizio `Day CQ DAM Mime Type OSGI` che identifica erroneamente [!DNL InDesign] file come `x-adobe-indesign` invece di `x-indesign`. (ASSETS-45953)
* [!DNL AEM 6.5.21] perdita di dati della sessione rilevata nel passaggio del flusso di lavoro predefinito **[!UICONTROL Pubblicazione pianificata in Brand Portal]**. (ASSETS-44104)
* **[!UICONTROL Memoria insufficiente]** errori visualizzati in [!DNL AEM] durante l&#39;elaborazione e la pubblicazione delle immagini. Questo problema era dovuto a metodi obsoleti nei flussi di lavoro, ad esempio **[!DNL Dam Asset update]** e **[!DNL Dynamic Media: Reprocess assets]**. (ASSETS-43343)
* Dopo aver apportato una modifica minore, ad esempio l&#39;aggiornamento del titolo, riaprire e salvare di nuovo **[!DNL Connected Assets configuration]** nell&#39;istanza Sites locale. L’istanza remota perde quindi la connessione all’istanza locale. Di conseguenza, non è in grado di stabilire una comunicazione con l’istanza Sites locale. (ASSETS-44484)
* In [!DNL AEM 6.5.21], quando il caricamento di una risorsa nella vista a elenco viene annullato e viene eseguito un secondo caricamento, [!DNL AEM] visualizza un errore **[!UICONTROL 0 di risorse NaN caricate]**. (ASSETS-44124)

#### [!DNL Dynamic Media]{#assets-dm-6523}

È stata aggiunta una proprietà di metadati (`jcr:content/metadata/dam:scene7SmartCropStatus`) alle risorse per identificare le generazioni di ritaglio avanzato non riuscite. Consente di cercare, filtrare e rielaborare in modo efficiente le risorse in caso di problemi di ritaglio avanzato tramite flussi di lavoro manuali o automatizzati. (ASSETS-46237)

#### [!DNL Dynamic Media] - Modalità ibrida {#assets-dm-hybrid-6523}

##### Dynamic Media - Pacchetto del componente aggiuntivo ibrido (AEM 6.5.23 e versioni successive)

A partire da AEM 6.5 Service Pack 23, è disponibile un nuovo pacchetto aggiuntivo per Dynamic Media - Modalità ibrida. Questo pacchetto include il bundle `cq-scene7-imaging` compatibile in modo specifico con Dynamic Media - Modalità di esecuzione ibrida.

**Correzione chiave inclusa**

È stato risolto un problema nelle distribuzioni Dynamic Media - Hybrid a causa del quale gli aggiornamenti al parametro `catalog.expiration` in `/conf/global/settings/dam/dm/imageserver` non venivano rispecchiati negli URL del server o dell&#39;autore, nonostante la replica fosse riuscita senza errori. L’aggiornamento garantisce valori di scadenza coerenti tra CRX/DE, la risposta del server e gli URL di consegna pubblici. A sua volta, migliora il comportamento della cache e l&#39;affidabilità delle trasformazioni delle immagini. (ASSETS-44837)

**Considerazioni importanti**

* Il bundle `cq-scene7-imaging` nell&#39;installazione base di AEM 6.5.23 (e versioni successive) è *non compatibile* con Dynamic Media - Modalità di esecuzione ibrida.
* Installando solo Service Pack 23 (e versioni successive), *non aggiorna automaticamente* il bundle `cq-scene7-imaging` esistente nelle istanze di AEM configurate per Dynamic Media - Ibrido (`-r dynamicmedia` modalità di esecuzione).

**Quando installare il pacchetto aggiuntivo ibrido**

* Durante l’aggiornamento diretto ad AEM 6.5.23 (e versioni successive) da AEM 6.5.19 o versioni precedenti.
* Quando sono necessarie correzioni specifiche per la funzionalità Dynamic Media - Ibrido.
* Durante l’implementazione di una nuova istanza Dynamic Media - Hybrid direttamente da AEM 6.5 GA (General Availability) a Service Pack 23 (e versioni successive).

**Scarica pacchetto del componente aggiuntivo ibrido**

Il pacchetto del componente aggiuntivo Ibrido è disponibile pubblicamente su Adobe Software Distribution a partire da giovedì 22 maggio 2025, con la versione ufficiale di AEM 6.5.23. Gli utenti possono trovarlo cercando **Pacchetto del componente aggiuntivo ibrido per AEM 6.5** in Distribuzione software.


<!--### [!DNL Forms]{#forms-6523}


#### Forms Designer 

* When a user exports the data for an XFA-based PDF using the exportDataAPI, the resulting XML shows discrepancies when compared with the XML data exported manually using Acrobat Reader. Values of some fields were missing in the output compared to the output generated from Acrobat Reader. (LC-3922791).  

* On AEM Forms 6.5.22.0, when a user attempts to generate a tagged PDF using the Output Service in Workbench, the resulting PDF contains an extra label tag under the reference tag in the table of content item. (LC-3922756) 

* When a user places field captions with bottom or right alignment in AEM Forms Designer, the tag tree includes only the caption without the corresponding value, leading to incomplete accessibility tagging. (LC-3922619). 

* On upgrading from AEM Forms 6.5 Service Pack 6 to AEM Forms Service Pack 20, the QR codes in generated PDFs become unreadable. The alternative text for the QR codes also fails accessibility testing, affecting screen reader compatibility. (LC-3922551). 

* When a user renders a letter in Agent UI on AEM Forms Service Pack 18, the content fails to display correctly due to the FormService.render() API. (LC-3922461). 

 

#### Forms

* When a user enables "Allow Rich Text for Title" on the root panel in an AEM Forms Adaptive Form, the "Exclude Title from Document of Record" setting on a nested panel incorrectly hides the root panel's title in the auto-generated Document of Record. (FORMS-19696). 

* When a user attempts to assign a custom sling:resourceType to a core component using the aem:afProperties in a JSON schema on an on-premise AEM 6.5 instance, the custom resource type is not applied. (FORMS-19691). 

* When a user submits an Adaptive Form with prefilled attachments using URIs, the form submission fails with a NullPointerException due to missing binary data. (FORMS-19371) (FORMS-19486). 

* When a user uploads a PDF under the 'Forms and Documents' section in AEM 6.5 Forms, the timeline feature stops functioning. (FORMS-19407)(FORMS-19234). 

* When a user uploads files using the out-of-the-box (OOTB) file attachment component in AEM Forms, security vulnerabilities are identified. This leads to potential interception of the submission process by unauthorized entities. (FORMS-19271). 

* When a user configures an out-of-the-box Adaptive Form in AEM Forms to automatically generate a Document of Record (DoR), the "Title" field in Acrobat Reader's Document Properties does not display the captured DoR title, and the form title does not appear by default in place of the filename. (FORMS-19263). 

* When a user opens an Interactive Communication in Agent UI, the prefilled data cannot be completely erased; upon removal, it automatically refills with the same data. (FORMS-19151). 

* When a user previews a date field in the Agent UI, the date unexpectedly changes due to time zone discrepancies between the VM's UTC setting and the system's interpretation of the date. (FORMS-19115). 

* When a user submits a form, file attachments may duplicate leading to multiple uploads of the same file. (FORMS-19045)(FORMS-19051). 

* Adding coordinators to policy sets in AEM 6.5 Document Security fails across both production and lower environments. (FORMS-18603, FORMS-18212, FORMS-19697). 

* When a user clicks the "datepicker-calendar-icon" in desktop mode with an empty field in AEM Forms Service Pack 22, an error occurs due to the undefined _$focusedDate variable, disrupting associated custom scripts. (FORMS-18483)(FORMS-18268). 

* On AEM Forms Service Pack 19 (6.5.19.0), when a customer previews a letter, the 'Amount in words' field fails to display or update number values incorrectly, leading to misalignment and missing spaces in the content. (FORMS-18437, FORMS-17330, FORMS-18209, FORMS-18557, CTG-4150848,FORMS-19614, LC-3922004) 

* When a customer previews a saved letter in AEM Forms 6.5 SP19 on RHEL, the content misaligns, spaces are missing, and unexpected characters like 'x' appear. (FORMS-18422)(FORMS-17641). 

* When a user navigates between tabs in AEM Forms, selecting components on the first tab becomes unresponsive. (FORMS-18345). 

* In AEM Forms 6.5.21.0, when a user converts an HTML file to PDF using the WebToPDF option, the output PDF is missing the header section, including metadata and title tags. (FORMS-18223, FORMS-17835, FORMS-19642, FORMS-18224). 

* In the AEM JEE Process Manager SDK, when a user invokes the retryAction(long actionOid) method, the system incorrectly retries the first action found in the tb_action_instance table. This occurs even when a specific action ID is provided or when the ID is null, resulting in unintended behavior. (FORMS-18187). 

* After updating to SP22, a user encounters issues where the save draft and submission functionalities fail without displaying any error message. (FORMS-18069). 

* In AEM 6.5.21.0, transitioning from XSD-based foundation components to core components prevents the implementation of cross-file references in JSON schemas, impacting Adaptive Forms migration. (FORMS-18065). 

* When a user previews a letter in the Agent UI, the date field shows an incorrect value due to IC time conversion issues. These discrepancies arise from time zone differences between the VM environment and the system's interpretation of time (UTC vs. local time). (FORMS-17988) (FORMS-17248). 

* When a user previews letters using Notice IC templates in AEM Forms, PDF generation times vary significantly, from 1.5 seconds to more than 10 seconds, even on the same server. This inconsistency affects business critical workflows. (FORMS-17951). 

* When a user binds a Scribble Signature object in an Adaptive Form to an XDP using the 'Data Sources' option, changes cannot be saved due to persistent aspect ratio validation errors, even when using valid values. (FORMS-17587). 

* When a user uses a specific XDP with many hidden fields for document fragments, AEM creates CRX nodes with the cm:optional property set to false, which causes the Interactive Communication (IC) submission to fail. (FORMS-17538). 

* On AEM Forms 6.5.19.0, when a customer previews a letter, the numeric box field fails to handle negative values correctly when digit limits for Lead and Frac are defined. This issue occurs due to the use of parseFloat, which treats the minus sign as part of the number. (FORMS-17451). 

* On AEM Forms 6.5, when a letter is previewed, the use of the "*" wildcard in the Adobe.json file is noticed, raising a concern about its purpose and potential modification (FORMS-17317). 

* When a user uses a screen reader on the "Apply for a Fixed Rate Saver joint account", the headings are incorrectly announced as 'clickable', causing accessibility issues. (FORMS-17038). 

* When a form is embedded, the generated iframe is missing a title attribute, leading to an accessibility compliance issue. (FORMS-17010). 

* It is not possible to download a form using the Forms Manager UI without including associated dependencies such as themes and fragments. (FORMS-15811). 

* When a user accesses the form on mobile devices (iOS and Android), the 'next' and 'previous' buttons on the first page are disabled, but the screen reader does not identify them as disabled. (FORMS-15773). 

* When a user saves a large form with fragments and lazy loading enabled, it fails to retrieve drafts, disrupting the workflow. (FORMS-19890, FORMS-19808). 

 

#### Forms JEE 

* When a user reconfigures the database in AEM Forms, the connection fails due to hardcoded parameters. (FORMS-19568, FORMS-17621) 

* When a user sets up AEM 6.5 with MySQL 8.4 using the partial turnkey method, the LiveCycle Configuration Manager (LCM) fails to recognize the required MySQL connector driver during the database connection test, causing the setup to fail. (FORMS-19442). 

* When a user runs LCM with JDBC 12.8.1 on JRE 11 in a JEE environment, the setup fails due to incompatibility issues.(FORMS-19276). 

* When a user opens a task in AEM On-Premise, the system executes the Workspace Start Action Profile instead of the AssignedUserProfile. (FORMS-19065). 

* When a user uses the retryAction(long actionOid) method in the AEM JEE Process Manager, unexpected behavior occurs. (FORMS-18357)(FORMS-18187). 

* On AEM Forms 6.5.21.0, the PDFG conversion fails with the error below: (FORMS-16851)(FORMS-14613).   
 
#### Forms Captcha {#forms-captcha-6523} 

* Improved reCAPTCHA alerting in Adaptive Forms by updating submit error codes to 400. Also, refined log alerts to distinguish between timeouts, expirations, and bot detection failures, enhancing troubleshooting accuracy and system observability. (FORMS-19240) 
* Closed an unclosed `ResourceResolver` instance in `ReCaptchaConfigurationServiceImpl` to prevent potential resource leaks and improve system stability when using reCAPTCHA integrations in AEM Forms. (FORMS-19242) 
* Improved CAPTCHA configuration handling for AEM Forms by ensuring the correct configuration binds to each form when multiple entries exist in the `/conf/global` folder. Prevents unintended use of incorrect CAPTCHA settings when the configuration container is not explicitly selected. (FORMS-19239)-->


<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### Foundation {#foundation-6523}

* È stato risolto un problema in Coral Alert Banners a causa del quale il colore del testo veniva visualizzato in bianco invece che in nero dopo l&#39;aggiornamento a Service Pack 21. Assicura che venga applicato lo stile corretto per mantenere il contrasto e la leggibilità corretti dei messaggi di avviso nell’interfaccia. (NPR-42359)
* È stato aggiunto il supporto per l’integrazione di OAuth nella configurazione di tag avanzati per allinearla con il deprecato JWT (JSON Web Token). Garantisce la continuità delle funzionalità dei tag avanzati utilizzando metodi di autenticazione aggiornati. (NPR-42296)

#### Apache Felix {#foundation-apachefelix-6523}

È stata corretta un’eccezione NullPointerException che si verificava durante il caricamento di file di chiave privata in un campo di proprietà di tipo binario in CRX, ripristinando la compatibilità presente tramite Service Pack 16. Abilita i flussi di lavoro sicuri per il caricamento di file chiave in AEM Managed Services senza errori del server o interruzioni dei processi di rinnovo dei certificati. (CQ-4359178)


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* Sono stati risolti i cicli di dipendenza OSGi tra i servizi di script Apache Sling che causavano ritardi o errori durante il caricamento delle pagine HTML dopo l’aggiornamento a Service Pack 21. Sono stati aggiornati i riferimenti ai servizi interni per eliminare le dipendenze cicliche che coinvolgono `SightlyScriptingEngineFactory` e i componenti correlati, migliorando l&#39;affidabilità e il comportamento di avvio del motore di script. (GRANITE-56808)
* È stato aggiornato l’utilizzo degli script JS in Apache Sling per caricare solo on-demand anziché con impazienza all’avvio, eliminando i conflitti di thread e riducendo il rischio che i server di pubblicazione non rispondano durante il caricamento. Questa modifica migliora la stabilità del server e i tempi di risposta in caso di traffico elevato impedendo il blocco delle risorse causato dalla risoluzione anticipata degli script. (GRANITE-56611)
* È stato risolto un problema in AEM Omnisearch a causa del quale i segnaposto per i campi di input venivano visualizzati in modo errato come etichette, creando confusione visiva. Assicura il rendering corretto dei segnaposto tra i campi filtro, mantenendo un comportamento coerente e accessibile dei moduli. (GRANITE-51791)
* È stato risolto un errore del server attivato durante la selezione di più di 30 CFM (Content Fragment Models) con riferimenti a più campi nell’editor di modelli per frammenti di contenuto. È stato migliorato il componente di suggerimento del filtro per supportare le operazioni POST. Questa funzionalità consente di gestire in modo corretto set di riferimento di grandi dimensioni durante la creazione di frammenti di contenuto e di migliorare la stabilità per configurazioni di modelli con volumi elevati. (GRANITE-57164)
* È stato risolto un problema nei CFM a causa del quale, se si faceva clic su Chiudi per selezionare una casella di controllo, lo stato veniva attivato non intenzionalmente. Sono stati aggiornati gli stili per limitare l’attivazione dei clic rigorosamente all’elemento casella di controllo, evitando interazioni accidentali da parte dell’utente e migliorando l’usabilità e l’accessibilità dei moduli. (GRANITE-52384)


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

È stato risolto un problema a causa del quale la convalida SNI bloccava le chiamate API tramite HTTPS per i clienti AEM che utilizzano configurazioni SSL Dispatcher con intestazioni host personalizzate. Introduce un&#39;opzione per disabilitare la convalida SNI come parte della configurazione Jetty, abilitando la compatibilità con specifiche impostazioni reverse proxy dove `mod_proxy` non è fattibile. (NPR-42614)


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### Platform{#foundation-platform-6523}

* È stato corretto un comportamento di unione dei tag incoerente, garantendo che il valore dei tag uniti venisse sempre visualizzato correttamente tra le risorse, indipendentemente dal fatto che i tag venissero creati in linea o tramite il metodo standard di creazione dei tag. Impedisce che i valori residui dei campi `EN:title` sovrascrivano la visualizzazione dei tag uniti. (CQ-4358812)
* È stata corretta la codifica ripetuta dei caratteri della e commerciale nei valori dei tag nella finestra di dialogo di modifica dei tag. Impedisce che a ogni salvataggio vengano aggiunte ulteriori entità &quot;&amp;&quot;, garantendo che i valori dei tag rimangano puliti e coerenti tra le varie modifiche ed evitando errori di visualizzazione nei contenuti creati. (CQ-4359048)
* È stato risolto un errore `ClassCastException` che impediva la consegna di e-mail all&#39;invio di moduli adattivi in AEM 6.5 in esecuzione su WebSphere®. La correzione consente la corretta trasmissione dei messaggi di posta elettronica assicurando la compatibilità tra `com.sun.mail.handlers.text_plain` e `java.activation.DataContentHandler`, in linea con la configurazione del gestore di posta prevista dagli ambienti WebSphere®. (NPR-42500)
* È stata migliorata la gestione degli errori in Gestione pacchetti, garantendo che AEM trasmetta un messaggio chiaro quando l’installazione non riesce e la risposta di errore sia vuota. Questa correzione evita errori automatici e favorisce un debug più rapido durante la distribuzione del pacchetto. (NPR-42375)

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### Traduzione{#foundation-translation-6523}

È stato risolto un problema NPE (NullPointerException) attivato durante l&#39;aggiornamento dei frammenti di contenuto nei flussi di lavoro tramite **Aggiorna copia lingua**. Questa correzione assicura che i flussi di lavoro non entrino in uno stato di errore o rimangano bloccati in uno stato di esecuzione durante la modifica del contenuto associato ai riferimenti di traduzione. (NPR-42115)

#### Interfaccia utente{#foundation-ui-6523}

Aggiunge attributi `title` mancanti ai pulsanti della finestra di dialogo dell&#39;interfaccia utente di Coral, ad esempio **Fine** e **Annulla** nelle finestre di dialogo di modifica dei componenti per migliorare l&#39;accessibilità e abilitare la convalida automatica. Assicura che i pulsanti mantengano gli attributi previsti nel rendering del markup, evitando errori nei test dell’interfaccia utente basati su Selenium. (NPR-42412)

#### WCM{#foundation-wcm-6523}

È stato risolto un problema che impediva l&#39;aggiunta di pagine ai processi di traduzione quando si utilizzava **Aggiorna copia lingua** in ambienti con Service Pack 19 o successivo. Assicura che i flussi di lavoro di traduzione procedano come previsto, abilitando il corretto trasferimento di pagina tra le copie per lingua senza intervento manuale. (CQ-4357929)

#### Flusso di lavoro{#foundation-workflow-6523}

È stato risolto un problema in `EmailNotificationServiceProcessor` a causa del quale il metodo `getSegmentId` restituiva `null` dopo la distribuzione dell&#39;hotfix, causando un errore dei trigger e-mail durante l&#39;elaborazione del flusso di lavoro. Ripristina la logica corretta di risoluzione degli ID segmento assicurandosi che il processore recuperi i valori `SegmentInfo` richiesti per supportare i flussi di lavoro delle notifiche e-mail tra le istanze di AEM. (CQ-4359755)


## Installa [!DNL Experience Manager] 6.5.23.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 richiede [!DNL Experience Manager] 6.5. Per istruzioni dettagliate, consulta la [documentazione sull&#39;aggiornamento](/help/sites-deploying/upgrade.md). <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del Service Pack è disponibile in Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.23.0 in una delle istanze di authoring utilizzando Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe consiglia di non rimuovere o disinstallare il pacchetto [!DNL Experience Manager] 6.5.23.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup di `crx-repository` nel caso sia necessario eseguirne il rollback. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installare il Service Pack in [!DNL Experience Manager] 6.5{#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). Adobe consiglia di riavviare il sistema se il tempo di attività corrente di un’istanza è elevato.

1. Prima di eseguire l&#39;installazione, creare una copia istantanea o un nuovo backup dell&#39;istanza [!DNL Experience Manager].

1. Scarica il Service Sack da [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, vedere [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Selezionare il pacchetto, quindi selezionare **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l’istanza dopo l’installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l’istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Talvolta la finestra di dialogo nell’interfaccia utente di Gestione pacchetti si chiude durante l’installazione del Service Pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di avere la certezza che l’installazione sia andata a buon fine. Questo problema si verifica in genere nel browser [!DNL Safari], ma può verificarsi in modo intermittente in qualsiasi browser.

**Installazione automatica**

Per installare [!DNL Experience Manager] 6.5.23.0 è possibile utilizzare due metodi diversi.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto nella cartella `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza l&#39;API HTTP [da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzare `cmd=install&recursive=true` per installare i pacchetti nidificati.

>[!NOTE]
>
>Experience Manager 6.5.23.0 non supporta l&#39;installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l&#39;utilizzo di questa versione, vedere i [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. Nella pagina delle informazioni sul prodotto (`/system/console/productinfo`) viene visualizzata la stringa di versione aggiornata `Adobe Experience Manager (6.5.23.0)` in [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

UberJar per [!DNL Experience Manager] 6.5.23.0 è disponibile nel [archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includi nel POM del progetto la seguente dipendenza: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar e gli altri artefatti correlati sono disponibili nell&#39;archivio centrale di Maven anziché nell&#39;archivio pubblico Maven di Adobe (`repo.adobe.com`). Il file UberJar principale è stato rinominato in `uber-jar-<version>.jar`. Non esiste alcun `classifier`, con `apis` come valore, per il tag `dependency`.



## Funzioni obsolete e rimosse{#removed-deprecated-features}

Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md/) per un elenco dettagliato di tutte le funzioni obsolete o rimosse per AEM 6.5.

### Editor di SPA {#spa-editor}

[L&#39;editor SPA](/help/sites-developing/spa-overview.md) è stato dichiarato obsoleto per i nuovi progetti a partire dalla versione 6.5.23 di AEM 6.5. L’editor SPA rimane supportato per i progetti esistenti, ma non deve essere utilizzato per i nuovi progetti.

Gli editor preferiti per la gestione dei contenuti headless in AEM sono ora:

* [Editor universale](/help/sites-developing/universal-editor/introduction.md) per la modifica visiva.
* [Editor frammenti di contenuto](/help/sites-developing/universal-editor/introduction.md) per la modifica basata su modulo.

## Problemi noti{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Problema con il bundle di script JSP in AEM 6.5.21-6.5.23 e AEM 6.5 LTS GA**
AEM 6.5.21, 6.5.22, 6.5.23 e AEM 6.5 LTS GA vengono forniti con il bundle `org.apache.sling.scripting.jsp:2.6.0`, che contiene un problema noto. Il problema si verifica in genere con un carico elevato quando l’istanza AEM gestisce molte richieste simultanee.

  Quando si verifica questo problema, è possibile che nei registri errori venga visualizzata una delle eccezioni seguenti insieme ai riferimenti a `org.apache.sling.scripting.jsp:2.6.0`:

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  Quando si verifica questo errore, l&#39;unico metodo di ripristino consiste nel riavviare l&#39;istanza di AEM.

  Contatta l’Assistenza clienti Adobe e fai riferimento a questa nota sulla versione per una risoluzione.

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

### Problema noto per AEM Sites {#known-issues-aem-sites-6523}

Frammenti di contenuto-Anteprima non riuscita a causa della protezione DoS per una grande struttura ad albero di frammenti. Vedi l&#39;articolo [KB sulle opzioni di configurazione predefinite di GraphQL Query Executor](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

<!--### Known issues for AEM Forms {#known-issues-aem-forms-6523}

* When a customer upgrades from Struts 2.x to 6.x, stricter type checking can cause silent failures—especially when checkbox components return false and are bound to a List *Integer*. This value mismatch must be handled explicitly to avoid deserialization errors.

* If the HTML to PDF conversion fails on a SUSE&reg; Linux&reg; (SLES 15 SP6 onwards) server with the following error:
  
  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
  then set the following environment variable and restart the server:
    `OPENSSL_CONF=/etc/ssl`

* After installing AEM Forms JEE Service Pack 21 (6.5.21.0), if you find duplicate entries of Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` under the `<AEM_Forms_Installation>/lib/caching/lib` folder (FORMS-14926), perform the following steps to resolve the issue:

  1. Stop the locators, if they are running.
  1. Stop the AEM Server. 
  1. Go to the `<AEM_Forms_Installation>/lib/caching/lib`. 
  1. Remove all the Geode patch files except `geode-*-1.15.1.2.jar`. Confirm that only the Geode jars with `version 1.15.1.2` are present.
  1. Open the command prompt in administrator mode.  
  1. Install the Geode patch using the `geode-*-1.15.1.2.jar` file. 

* If a user tries to preview a draft letter with saved XML data, it gets stuck in `Loading` state for some specific letters. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-14521)
  
* After upgrading to AEM Forms Service Pack 6.5.21.0, the `PaperCapture` service fails to perform OCR (Optical Character Recognition) operations on PDFs. The service does not generate output in the form of a PDF or a log file. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (CQDOC-21680)

* When users upgraded from AEM 6.5 Forms Service Pack 18 or 19 to Service Pack 20 or 21, they encountered a JSP compilation error. This error prevented them from opening or creating adaptive forms. It also caused issues with other AEM interfaces. Those interfaces included the Page Editor, AEM Forms UI, Workflow editor, and System Overview UI. (FORMS-15256)

  If you face such an issue, perform the following steps to resolve it:
    1. Navigate to the directory `/libs/fd/aemforms/install/` in CRXDE.
    1. Delete the bundle with the name `com.adobe.granite.ui.commons-5.10.26.jar`.
    1. Restart your AEM Server.

* After updating to AEM Forms Service Pack 20 (6.5.20.0) with the Forms Add-On, configurations relying on the legacy Adobe Analytics Cloud Service using credential-based authentication stop working. This issue prevented analytics rules from executing correctly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-15428)

* When a user updates to AEM Forms Service Pack 20 (6.5.20.0) on the JEE server and generates PDFs using output services, the PDFs render with accessibility issues. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922112)
* When a user generates Tagged PDFs using the output service on JEE, it shows "Inappropriate structure warning." To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922038)
* When a form is submitted on AEM Forms JEE, the instances of a repeating XML element are removed from the data. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922017)
* When a user in a Linux&reg; environment renders an Adaptive Form (on JEE) in HTML, it fails to render properly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921957)
* When a user converts an XTG file to PostScript format using the Output Service on AEM Forms JEE, it fails with the error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921720)
* After upgrading to AEM Forms Service Pack 18 (6.5.18.0) on JEE server, when a user submits a form, it fails to render HTML5 or PDF Forms and XMLFM crashes. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921718)
* In the Print Preview of the Interactive Communications Agent UI, the currency symbol (such as the dollar sign $) is inconsistently displayed for all field values. It appears for values up to 999 but is missing for values of 1000 and above. (FORMS-16557)
* Any modifications to nested layout fragments' XDP in an Interactive Communication are not reflected in the IC editor. (FORMS-16575)
* In the Print Preview of the Interactive Communications Agent UI, some calculated values are not displayed correctly. (FORMS-16603)
* When the letter is viewed in Print Preview, the content is changed. That is, some spaces disappear, and certain letters are replaced with `x`. (FORMS-15681)
* When a user configures a WebLogic 14c instance, the PDFG service in AEM Forms Service Pack 21 (6.5.21.0) on JEE running on JBoss&reg; fails due to classloader conflicts involving the SLF4J library. The error is displayed as follows (CQDOC-22178):
  
    ```java
    Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
    the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
    @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
    (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
    have different Class objects for the type org/slf4j/ILoggerFactory used in the signature-->

## Bundle OSGi e pacchetti di contenuti inclusi{#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in questa versione di [!DNL Experience Manager] 6.5 Service Pack:

* [Elenco dei bundle OSGi inclusi in Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti Web con restrizioni{#restricted-sites}

Questi siti Web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedervi, contatta il tuo account manager Adobe.

* [Download del prodotto all&#39;indirizzo licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta L&#39;Assistenza Clienti Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina prodotto](https://business.adobe.com/it/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Iscriviti agli aggiornamenti dei prodotti con priorità Adobe](https://www.adobe.com/subscription/priority-product-update.html)
