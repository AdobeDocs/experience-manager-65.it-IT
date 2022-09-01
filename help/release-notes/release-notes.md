---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova le informazioni sulla versione, le novità, installa le procedure guidate e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 0bd7c444bf0424b60c11b7171b7ea7ae9d7f3926
workflow-type: tm+mt
source-wordcount: '2624'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | 25 agosto 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.14.0 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotte successivamente alla data di disponibilità iniziale di 6.5 di aprile 2019. [Installa questo service pack](#install) su [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* Impossibile aggiungere o visualizzare tag per i file PDF. (NPR-38452)
* Quando configuri Risorse collegate, salva la configurazione, riapri la pagina di configurazione e verifica la configurazione già salvata, la connessione di prova non riesce. (NPR-38507)
* Impossibile aggiungere utenti con ID utente numerico alle raccolte. (NPR-38538)
* L&#39;Experience Manager non riesce a elaborare il FFmpeg installato nell&#39;istanza di authoring. (NPR-38568)
* L’elaborazione di PDF non riesce con un errore `NoClassDefFoundError` messaggio di errore. (NPR-38741)
* Il pulsante Aggiungi in Colonne personalizzate non viene visualizzato correttamente durante la creazione di un rapporto sulle risorse per `de_DE` locale. (ASSETS-10641)
* Quando carichi una risorsa duplicata nell’archivio Digital Asset Management e Experience Manager rileva e fornisce un’opzione per eliminare la risorsa duplicata, anche la risorsa originale viene eliminata dall’archivio. (ASSETS-10826)
* Experience Manager non salva correttamente i metadati della cartella quando si specificano caratteri speciali in più campi. (ASSETS-10721)
* Impossibile salvare le proprietà della risorsa finché non fai clic su **[!UICONTROL Salva e chiudi]** due volte. (ASSETS-12040)
* L’assistente vocale annuncia solo l’ `Relate` pulsante . Tuttavia, `Relate` contiene anche un sottomenu e può essere espanso e compresso. (ASSETS-6938)
* Attributi ARIA richiesti (applicazioni Rich Internet accessibili) `aria-expanded` per `role="combo box"` è mancante. (ASSETS-6928)
* Nella vista a schede, nell’area di navigazione dei file principale, il contenuto del testo **[!UICONTROL Ordina per]** non ha almeno un rapporto di contrasto 4,5:1 rispetto al colore di sfondo. (ASSETS-6926)
* L&#39;Experience Manager non identifica **[!UICONTROL Selezionare un modello di flusso di lavoro]** elenco a discesa come campo obbligatorio durante la creazione di un modello di flusso di lavoro. (ASSETS-6871)

>[!NOTE]
>
>I servizi di contenuti avanzati non saranno disponibili per i nuovi clienti Experience Manager Assets On-Premise a partire dal 1° settembre 2022. Nessun impatto sui clienti esistenti On-Premise e Adobe Managed Services che dispongono già di questa funzionalità abilitata.

### [!DNL Dynamic Media] {#dynamic-media-6514}

* Aggiungi il supporto per la reimpostazione della password per l&#39;utente Dynamic Media Classic in Experience Manager. (ASSETS-10298)
* Le Smart Crop generate per le immagini con sfondo trasparente hanno sfondo bianco. (ASSETS-13148)
* Dynamic Media non genera miniature per i file EPS. (ASSETS-10959)
* Le risorse non vengono caricate nell’account Dynamic Media a causa di un parametro di caricamento mancante. (ASSETS-13165)
* Consenti il caricamento in Dynamic Media di risorse con nomi superiori a 127 caratteri. (ATTIVO-9991)
* Abilitazione di JavaScript ES6 (ECMAScript 6) per visualizzatori Dynamic Media in Experience Manager 6.5.14.0. (NPR-38393)
* Configurazione delle opzioni in Dynamic Media **[!UICONTROL Impostazioni generali]** e **[!UICONTROL Pubblica installazione]** non devono essere accessibili da utenti non amministratori. (ASSETS-8628)
* Dynamic Media **[!UICONTROL Impostazioni generali]** La pagina non mostra correttamente i parametri di caricamento già configurati. (ASSETS-10245)
* L’interfaccia utente di Experience Manager non mostra alcun messaggio di errore nel caso in cui la creazione/aggiornamento del set non riesca. (ASSETS-10264)
* Impossibile applicare un criterio salvato a uno dei contenitori di un modello modificabile per consentire l&#39;aggiunta di componenti Dynamic Media. (ASSETS-11044)
* Le risorse che non vengono caricate nell’account Dynamic Media dopo l’esecuzione del flusso di lavoro Dynamic Media Reprocess Assets su risorse con handle di lavoro non corretti. (ASSETS-12084, ASSETS-9877)
* Gli utenti degli assistenti vocali sono interessati `title` attributo non fornito `<frame>` e `<iframe>` in **[!UICONTROL Digitare per cercare]** finestra di dialogo. (ASSETS-5483)
* Lettori di schermo, correlati e significativi `alt=` deve essere fornito per più immagini presenti in **[!UICONTROL Risorse]** nel riquadro a sinistra. (ASSETS-5644)
* L’assistente vocale non legge **[!UICONTROL Disattiva]** e **[!UICONTROL Disattiva]** su video utilizzando il componente Dynamic Media. (ASSETS-10169)

## Commerce {#commerce-6514}

* I prodotti Commerce non vengono ordinati utilizzando l’intestazione di colonna e vengono utilizzati _remoto_ modalità di ordinamento; i prodotti Commerce devono essere ordinati utilizzando intestazioni di colonna con _locale_ modalità di ordinamento. (CQ-4343750, NPR-38498)

## [!DNL Forms] {#forms-6514}

>[!NOTE]
>
>* I pacchetti del componente aggiuntivo [!DNL Experience Manager Forms] vengono rilasciati una settimana dopo la data di rilascio pianificata per il Service Pack di [!DNL Experience Manager]. In questo caso, i pacchetti aggiuntivi verranno rilasciati giovedì 1 settembre 2022. Inoltre, a questa sezione verrà aggiunto anche un elenco di correzioni e miglioramenti di Forms.


## Integrazioni {#integrations-6514}

* Abilita supporto per la compilazione JavaScript ES6 (modalità ECMAScript6 o superiore) per la minimizzazione del `/libs/cq/analytics/widgets.js` libreria. (NPR-38433)
* Abilita supporto per la compilazione JavaScript ES6 (modalità ESMAScript6 o superiore) per la minimizzazione del `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` libreria. (NPR-38435)
* Maggiore è il contenuto presente in `/content/campaigns`, più lunga è la chiamata a `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`) viene utilizzata all’apertura dell’Editor pagina. (NPR-38663)

## Platform {#platform-6514}

* Impossibile accedere a Gestione pacchetti per distribuire gli aggiornamenti. (NPR-38646)
* Nell’interfaccia utente del selettore dei tag delle risorse, i tag vengono visualizzati nell’ordine in cui sono stati creati. Tuttavia, in presenza di molti tag, è difficile visualizzarli e gestirli perché non è possibile ordinarli. (CQ-4344279)
* Crea una notifica nell’interfaccia utente quando un utente viene rappresentato da un amministratore o da un altro utente che utilizza il **[!UICONTROL Impersona come]** campo . (CQ-4345288)
* In una raccolta avanzata, tutte le risorse venivano visualizzate quando si filtrava utilizzando una ricerca salvata. (CQ-4345326)
* Viene visualizzato un numero errato di risorse selezionate per **[!UICONTROL Aggiungi alla raccolta]** quando **[!UICONTROL Seleziona tutto]** è selezionato. (CQ-4345424)
* Si è verificato un messaggio di eccezione durante l&#39;utilizzo del **[!UICONTROL Impersona come]** con un gruppo o un utente inesistente. (CQ-4346098)

## [!DNL Sites] {#sites-6514}

* Eliminazioni impreviste dei percorsi durante l&#39;aggiornamento di Experience Manager da 6.5.12.0 a 6.5.13.0. (NPR-38532)

### Accessibilità {#access-6514}

* In Experience Manager Sites, quando espandi la **[!UICONTROL Cambiare il formato di visualizzazione e regolare le impostazioni di visualizzazione]** quindi seleziona **[!UICONTROL Vista a elenco]**, **[!UICONTROL Trascina e rilascia]** manca un nome accessibile al pulsante. (SITES-2863, NPR-38760)
* L’assistente vocale deve annunciare il nome accessibile, ad esempio `Show description for Archive` o `Show description for mini shopping cart`. Tuttavia, il nome accessibile corrente viene annunciato come `Info Circle button show description` per _tutto_ i pulsanti delle informazioni sulla descrizione comando. (SITES-3104)
* Migliorare l’annullamento per i componenti che non dispongono della funzione di modifica in linea o di destinazione nel `cq:editConfig`. (NPR-38361) <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* Il menu a discesa Sistema di stili potrebbe essere stato posizionato nella parte superiore della pagina anziché nel contesto del componente, per i componenti che utilizzano `cq:editConfig` &quot;post-modifica: REFRESH_PAGE&quot;. (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* Il componente testo non è allineato quando viene aggiunto ai contenitori di layout nidificati. (NPR-38193)
* Una scheda stile vuota era visualizzata quando non vi era alcuna configurazione del sistema di stili per un componente. La scheda ora è nascosta quando non è presente alcuna configurazione. (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* La proprietà `useLegacyResponsiveBehaviour` funziona solo se autenticato. (NPR-37996)
* L’aggiornamento di jquery-ui all’ultima versione causava l’interruzione dell’editor. (SITES-5647)

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* Al primo caricamento del frammento di contenuto si verifica un problema di convalida del campo di enumerazione dei frammenti di contenuto. (SITES-7140)
* Aggiunta di campi di personalizzazione per Campaign nell’editor Rich Text dell’editor Frammenti di contenuto . (NPR-38526)
* Durante la creazione o la modifica di un nuovo frammento di contenuto nell’editor frammento di contenuto, tramite Dispatcher, il modello di frammento di contenuto non viene salvato. Inoltre, l’editor dei frammenti di contenuto non viene chiuso e viene visualizzato un errore nel registro del browser. (NPR-38691)
* Errore di convalida della query persistente. (NPR-38523)
* Nella finestra di dialogo Frammento di contenuto, in **[!UICONTROL Proprietà]**, **[!UICONTROL Frammento di contenuto]** il campo non mantiene il percorso salvato nel pop-up di selezione. (NPR-38632)
* Quando si crea un modello per frammenti di contenuto e si aggiunge un campo di enumerazione del tipo a discesa, la convalida corretta per _`is required`_fallisce. (NPR-38237)

### Componenti core  {#sites-corecomponents-6514}

* Il nuovo componente E-mail pagina non deve forzarti ad accedere all’interfaccia utente classica durante la modifica `/etc`. (NPR-38648)

### Editor pagina {#sites-pageeditor-6514}

* L’utente non è in grado di ridimensionare il componente in base al numero di colonne desiderato. (NPR-38688)

### Editor modelli {#sites-templateeditor-6514}

* Mancante **[!UICONTROL Elimina]** e **[!UICONTROL Taglia]** i pulsanti sulla barra dei menu in un modello modificabile dopo un `cq:actions` proprietà personalizzata. (NPR-38521)
* Se un componente include un altro componente, non è possibile eliminare il componente all’interno della struttura del modello perché il **[!UICONTROL Elimina]** nella barra Menu manca il pulsante. (NPR-38585)

## Sling {#sling-6514}

* Un aumento del numero di file aperti in produzione è stato riscontrato a causa di una perdita di memoria nel modulo `DiscoveryLiteDescriptor` in `org.apache.sling.discovery.commons`, versione 1.0.20. (NPR-38288)
* Ad Experience Manager, da **[!UICONTROL Operazioni]** > **[!UICONTROL Diagnosi]**, si verifica un errore quando si seleziona **[!UICONTROL Scarica ZIP di stato]** > **[!UICONTROL Scarica]**. (NPR-38514)

## Progetti di traduzione {#translation-6514}

* Launch per le pagine secondarie aggiunte come riferimento in una pagina padre non veniva promosso quando `isDeep` è stato impostato su `false`. (NPR-38531)

## Interfaccia utente {#ui-6514}

* Quando utilizzi **[!UICONTROL Seleziona tutto]** > **[!UICONTROL Pubblicazione rapida]**, ad Experience Manager non venivano pubblicate tutte le risorse o mostrate quante risorse sarebbero state pubblicate in **[!UICONTROL Scheda]** visualizzare o **[!UICONTROL Elenco]** visualizza. (NPR-38546)
* Viene visualizzato un conteggio delle risorse selezionate errato per **[!UICONTROL Aggiungi alla raccolta]** in **[!UICONTROL Seleziona tutto]** caso. (NPR-38633)
* Gli utenti disabilitati possono ancora essere aggiunti a raccolte e progetti. (NPR-38651)
* Se si elimina un filtro senza salvare il modulo di ricerca, viene generato un errore. (NPR-38698)
* La sessione di un utente non può ottenere un `ModifiableValueMap` istanza per i gruppi al fine di stabilire l&#39;appartenenza diretta al gruppo. (NPR-38710)

## Flusso di lavoro {#workflow-6514}

* Abilita supporto per la compilazione JavaScript ES6 (modalità ESMAScript6 o superiore) per la minimizzazione del `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` libreria. (NPR-38304)
* Una volta eseguito il flusso di lavoro e completati i passaggi del processo, lo stesso commento viene ripetuto più volte. (NPR-38364)

## Installa [!DNL Experience Manager] 6.5.14.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0 richiede [!DNL Experience Manager] 6.5. Vedi [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate. <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.14.0 su una delle istanze Autore che utilizza Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobe sconsiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.14.0. <!-- UPDATE FOR EACH NEW RELEASE -->

### Installa il service pack su [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Riavvia l’istanza prima dell’installazione se l’istanza è in modalità di aggiornamento (quando l’istanza è stata aggiornata da una versione precedente). L&#39;Adobe consiglia un riavvio se il tempo di attività corrente per un&#39;istanza è elevato.

1. Prima di installare, scegli uno snapshot o un nuovo backup del tuo [!DNL Experience Manager] istanza.

1. Scarica il service pack da [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Apri Gestione pacchetti, quindi seleziona **[!UICONTROL Carica pacchetto]** per caricare il pacchetto. Per ulteriori informazioni, consulta [Gestione pacchetti](/help/sites-administering/package-manager.md).

1. Seleziona il pacchetto, quindi seleziona **[!UICONTROL Installa]**.

1. Per aggiornare il connettore S3, arresta l&#39;istanza dopo l&#39;installazione del Service Pack, sostituisci il connettore esistente con un nuovo file binario fornito nella cartella di installazione e riavvia l&#39;istanza. Vedi [Archivio dati Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La finestra di dialogo nell’interfaccia utente di Gestione pacchetti talvolta si chiude durante l’installazione del service pack. Adobe consiglia di attendere la stabilizzazione dei registri di errore prima di accedere alla distribuzione. Attendi i registri specifici relativi alla disinstallazione del bundle dell’aggiornamento prima di essere certi che le installazioni abbiano esito positivo. In genere, questo problema si verifica in [!DNL Safari] browser ma può verificarsi a intermittenza su qualsiasi browser.

**Installazione automatica**

Esistono due metodi diversi per l&#39;installazione automatica [!DNL Experience Manager] 6.5.14.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza la [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzo `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>Experience Manager 6.5.14.0 non supporta l’installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo con questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. La pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa di versione aggiornata `Adobe Experience Manager (6.5.14.0)` sotto [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (Usa console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.12 o successiva (Usa console Web: `/system/console/bundles`). <!-- NPR-38747 -->


### Installa [!DNL Experience Manager] Pacchetto aggiuntivo di Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignora se non utilizzi [!DNL Experience Manager] Forms. Correzioni in [!DNL Experience Manager] Forms viene fornito tramite un pacchetto aggiuntivo separato una settimana dopo il programma [!DNL Experience Manager] Versione Service Pack.

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

UberJar per [!DNL Experience Manager] 6.5.13.0 è disponibile nella [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>In Experience Manager 6.5.14.0, tieni presente che la versione UberJar (6.5.13.0) rimane la stessa della versione precedente.

Per utilizzare UberJar in un progetto Maven, vedi [come utilizzare UberJar](/help/sites-developing/ht-projects-maven.md) e includere nel POM del progetto la seguente dipendenza: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
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

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [Frammento di contenuto AEM con pacchetto indice GraphQL 1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

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

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Elenco dei bundle OSGi inclusi nell&#39;Experience Manager 6.5.14.0](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.14.0](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il manager del tuo account Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina di prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

