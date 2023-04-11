---
title: Note sulla versione per [!DNL Adobe Experience Manager] 6,5
description: Trova le informazioni sulla versione, le novità, installa le procedure guidate e un elenco dettagliato delle modifiche per [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: f53dbe7d51ff976f8d79702a86527f984aa00997
workflow-type: tm+mt
source-wordcount: '2983'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 Note sulla versione più recente del Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## Informazioni sulla versione {#release-information}

| Prodotto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versione | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versione Service Pack |
| Data | Giovedì 23 febbraio 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL di download | [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[..]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Cosa è incluso in [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0 include nuove funzionalità, miglioramenti chiave richiesti dai clienti, correzioni di bug e miglioramenti a livello di prestazioni, stabilità e sicurezza, introdotte successivamente alla data di disponibilità iniziale di 6.5 di aprile 2019. [Installa questo service pack](#install) su [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Un miglioramento fondamentale in Dynamic Media è il seguente:

Nuovo supporto del protocollo DASH (Dynamic Adaptive Streaming over HTTP) avviato per lo streaming a bit rate adattivo nella distribuzione video Dynamic Media (con CMAF) [Formato applicazione multimediale comune] abilitato).

* Lo streaming adattivo (DASH/HLS) garantisce una migliore esperienza di visualizzazione da parte dell’utente finale per i video.
* DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore.
* Disponibile ora in Nord America (da abilitare tramite ticket di supporto), in arrivo presto in Asia-Pacifico e in Europa-Medio Oriente-Africa.

Vedi [Abilita DASH sul tuo account](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Risorse collegate: Quando abiliti le opzioni Ritaglio avanzato per le immagini su DAM remoto, carica le immagini in una cartella e sincronizza la cartella con siti locali, la cartella non si apre nella distribuzione locale di Sites. (NPR-39912)
* Durante l&#39;ordinamento di una raccolta per nome, la visualizzazione elenco non funziona correttamente (ASSETS-19401)
* Quando un file multimediale di grandi dimensioni (JPEG) viene caricato nelle raccolte, Experience Manager smette di rispondere. (ASSETS-19387)
* Nel riquadro della struttura del contenuto, il nome della risorsa visualizzato non è corretto in quanto la posizione della risorsa non viene riprodotta in modo appropriato. (ASSETS-18870)
* Durante la condivisione di una raccolta utilizzando un collegamento, i dati nell’URL non corrispondono tra la visualizzazione a schede e la vista a elenco. (ASSETS-18758)
* Quando si esegue una ricerca omnisearch utilizzando un filtro sul tipo di cartella, i risultati della ricerca sono incoerenti. (ASSETS-18227)
* La `dam:size` La proprietà non viene aggiornata dopo XMP write-back, il che comporta la restituzione di informazioni errate dal `/platform/path/to/asset.jpg;resource=metadata` API. (ASSETS-17631)
* Risolutore risorse non chiuso su tutte le istanze di Experience Manager. (ASSETS-16904)
* Impossibile creare una versione per una risorsa anche se ti è stata assegnata la `create` e `modify` autorizzazioni. (ASSETS-15956)
* La `move` Questo pulsante viene disattivato in modo casuale durante lo spostamento di una risorsa da un punto all’altro. (ASSETS-14889)
* Gli assistenti vocali non sono in grado di identificare le intestazioni, in quanto il testo non è definito all’interno dei tag delle intestazioni ma come testo generale. (ASSETS-6924)
* Il testo alternativo sotto l’immagine non è obbligatorio, ma il testo visualizzato sotto l’immagine è ripetitivo con un `Type` attributo. (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* L’elemento modulo non contiene etichetta. Con gli assistenti vocali come NVDA e JAWS, le informazioni sull’etichetta del modulo non vengono annunciate correttamente. (CQ-4344078)
* I menu a discesa non vengono chiusi quando il `Escape` viene utilizzato su una tastiera. (CQ-4344077)
* L’icona Informazioni (la lettera &quot;i&quot;) visualizzata per il suggerimento di errore in linea dopo aver fornito un input non valido, non è accessibile tramite tastiera. (CQ-4344076)
* `getManifestURI` restituisce null a causa di una proprietà JCR letta come `toString` anziché `getString`. (ASSETS-18674)
* Il componente video SmartCrop non si comporta correttamente. Il componente esegue la riproduzione invece dello streaming e le chiamate VTT non riescono, generando un errore 404. (ASSETS-18468)
* Selezione **[!UICONTROL Proprietà]** nella pagina Visualizzatore di una risorsa causa un’eccezione Null Pointer. (ASSETS-18420)
* [!DNL Experience Manager] l’interfaccia utente cambia per lo streaming DASH che include quanto segue:
   * avere un campo CMAF (Common Media Application Format) visibile nell’editor del profilo video.
   * far sì che il processo di caricamento dei video invii un flag CMAF.
   * le opzioni **[!UICONTROL auto]**, **[!UICONTROL hls]** e **[!UICONTROL sciocco]** sono ora disponibili nell’elenco a discesa di riproduzione nell’editor predefiniti per visualizzatore **[!UICONTROL Comportamento]** scheda .
(ASSETS-17428)
* In Navigazione, quando selezioni **[!UICONTROL Risorse]** > **[!UICONTROL File]** > **[!UICONTROL Crea]** > **[!UICONTROL Set carosello]**, l’icona dell’immagine si sovrappone alla stringa di testo &quot;Diapositiva 1&quot;. (ASSETS-18578)
* Le risorse non pubblicate vengono pubblicate di nuovo. (ASSETS-16428)
* Experience Manager Author si interrompe a causa di un problema di caricamento, che richiede la creazione di un avviso sintetico. (ASSETS-15937)
* Nella pagina Impostazioni generali di Dynamic Media, messaggio di errore non tradotto `Failed to fetch data` appare. (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] Funzioni principali {#forms-features-6516}

* [Forms adattivo headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) consentono agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale.

* [Componenti core adattabili di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) sono un set di 24 componenti open-source compatibili con BEM basati sulle basi dei componenti core di Adobe Experience Manager WCM. Questi componenti sono open-source e offrono agli sviluppatori la possibilità di personalizzare ed estendere facilmente questi componenti in base alle esigenze specifiche della loro organizzazione. Chiunque abbia le competenze esistenti da personalizzare [Componenti core WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) possono personalizzare e personalizzare facilmente lo stile di questi componenti.

* Il servizio Estensione Reader su OSGi ora fornisce opzioni separate per abilitare l’importazione e l’esportazione di diritti di utilizzo su un PDF per importare o esportare dati in Adobe Acrobat Reader. (NPR-39909)

### [!DNL Forms] Correzioni {#forms-fixes-6516}

* Quando utilizzi un **Assegna attività** per inviare una notifica per un’attività assegnata, vengono inviate due e-mail invece di una alla persona assegnata. (NPR-40078)
* Quando un utente nasconde le intestazioni della tabella, la larghezza della colonna impostata in precedenza viene disattivata e tutte le colonne mantengono la stessa larghezza. (NPR-40063)
* Nel caso in cui cambi la password predefinita dell&#39;utente amministratore da `admin`, durante l&#39;esecuzione della `Prepare Adobe Experience Manager Server For DSC deployment` controlla il service pack JEE di AEM Forms che non riesce. (NPR-40062), (NPR-39387)
* Le API OutputService e AssemblerService non riescono a convertire il modulo PDF in PDF/A. (NPR-39990)
* Impossibile convertire PDF in PDF/A. Quando un utente converte PDF in PDF/A, si verifica il seguente errore: `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* Quando la convalida lato server non riesce per una chiamata API GuideSubmitServlet, gli errori non vengono restituiti nella risposta inviata al client. (NPR-39925)
* Dopo l&#39;aggiornamento a AEM Service Pack 6.5.15.0 sul server Windows, l&#39;utente riceve più messaggi di errore e il servizio e-mail non funziona.(NPR-39919)
* Quando si esegue l&#39;aggiornamento a AEM 6.5.14.0 e si utilizza il servizio importData per unire PDF con XML, si verifica il seguente errore: `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* Quando l&#39;utente installa **Document Security Office** estensione, si verificano i seguenti problemi:
   * Microsoft® Excel si blocca frequentemente.
   * Durante l&#39;apertura di un documento protetto, il **Ufficio sicurezza dei documenti** estensione non rilevata come installata in un computer. Indica all&#39;utente di scaricare e installare l&#39;estensione di sicurezza. (NPR-39768)
* Dopo l&#39;aggiornamento a AEM Service Pack 6.5.15.0 da parte di un utente, la conversione da PostScript a Pdf non funziona. (NPR-39765), (NPR-39764)
* Quando l&#39;utente tenta di aprire la schermata introduttiva dopo l&#39;apertura di un Modulo adattivo, l&#39;operazione non riesce con un&#39;eccezione NullPointer:`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:"` (NPR-39654)
* In Windows, quando l’utente abilita impostazioni di nero ad alto contrasto, il contenuto Forms di HTML5 non risulta chiaro quando viene eseguito il rendering come anteprima HTML nel browser. (NPR-39018)
* Quando l’utente tenta di aggiungere i metadati, il pulsante Salva non funziona sia per i componenti Bozza che per i componenti Inviata.(CQ-4349601)
* Dopo l&#39;aggiornamento a AEM Service Pack 6.5.15.0, il reindirizzamento degli URL relativi non funziona più in Visual Editor. (NPR-39947)
* Quando un utente esegue l&#39;aggiornamento a AEM Service Pack 6.5.15.0, il reindirizzamento smette di funzionare con Internet Explorer. (CQ-4351745)
* Dopo l’aggiornamento a AEM Service Pack 6.5.15.0 da parte di un utente, il tag di intestazione di HTML non viene riconosciuto. Il codice HTML per il tag titolo viene visualizzato come testo nel modulo HTML. (NPR-39915)
* Quando l’utente tenta di inviare un modulo adattivo, si verifica un errore di tipo: `ERROR [10.207.64.167 [1668589530607] POST /app/LS4/content/forms/af/revalidate/jcr:content/guideContainer.af.submit.jsp HTTP/1.1]`(NPR-39809)
* Quando un utente visualizza l&#39;anteprima di un documento di record utilizzando la variabile **Invia e-mail** l’azione di invio non viene visualizzata correttamente. Il modello di posta viene incorporato nell&#39;anteprima del documento di record. (CQ-4352155)
* Quando un utente visualizza l’anteprima di un modulo adattivo come HTML nel browser Microsoft Edge con modalità di compatibilità IE, questo non viene visualizzato correttamente.(CQ-4352216)
* Per abilitare la traduzione, il dizionario deve includere nuove impostazioni internazionali con caratteri speciali, ad esempio caratteri di sottolineatura o trattini. (NPR-40088)

Dopo aver installato il service pack aggiuntivo Forms 6.5.16.0 di AEM, i clienti si trovavano di fronte ai problemi elencati di seguito. Quindi, una versione aggiornata di [Service Pack aggiuntivo di Forms 6.5.16.0 - 6.0.914](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) viene rilasciato. L&#39;Adobe consiglia di utilizzare il service pack aggiornato:
* Quando un utente tenta di creare un modulo adattivo con un utente nel gruppo utenti moduli, l&#39;opzione per selezionare un modello non è presente e si verifica l&#39;errore simile al seguente: errore interno del server: java.lang.NullPointerException su com.adobe.aem.formsndocuments.servlet.ThemeClientLibraryDataSourceServlet.lambda$getThemeClientLibCategoryList$3(ThemeClientLibraryDataSourceServlet.java:76) su java.base/java.util.stream.ReferencePipeline$2$1.accept(Reference Pipeline.java:176) a java.base/java.util.Iterator.foreachRemain(Iterator.java:133) (FORMS-7629)
* Le modifiche apportate nelle regole dell&#39;editor di codice non vengono salvate.(FORMS-7532)

## Integrazioni {#integrations-6516}

* Rimuovere il codice e la dipendenza di Adobe Search&amp;Promote dall’Experience Manager 6.5. Il Search&amp;Promote di Adobe è stato raggiunto alla fine del servizio settembre 2022. Vedi [Annuncio sulla fine del servizio di Adobe Search&amp;Promote](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* Corrente `cq-wcm-core` il POM non è presente nella versione di artifactory. (SITES-10983)
* L’azione di anteprima di rollout non deve elencare la pagina da creare. (SITES-10355, CQ-4266213)
* Rollout dopo lo scollegamento di MSM ricrea la pagina staccata. (SITES-9841)
* La creazione di un lancio sta scadendo; l’utente deve attendere molti minuti su una schermata di caricamento prima che la richiesta si esaurisca. (SITES-9051)
* Nell’interfaccia utente della pagina di rollout sono visualizzati percorsi di pagina padre inesistenti. Puoi eseguire il rollout della pagina con un messaggio di successo, ma la pagina figlia non viene rollout a causa della mancata implementazione iniziale della pagina padre. (SITES-8621)

### [!DNL Sites] - Componenti core {#sites-core-components-6516}

* Centralizza l’elaborazione dei collegamenti sulle pagine e-mail in modo che le personalizzazioni dei modelli non siano più necessarie. (SITES-9002)

### [!DNL Sites] - Interfaccia utente amministratore {#sites-adminui-6516}

* Esportazione CSV non esporta tutte le pagine sotto la pagina selezionata. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* Impossibile stampare il JSON di un frammento di contenuto. Il motivo è che non è possibile generare la query GraphQL quando si apre la pagina Anteprima del frammento di contenuto. (SITES-8619)
* Quando si riapre l’Editor modello frammento di contenuto, tutte le **[!UICONTROL Data e ora]** per impostazione predefinita, i campi sono di tipo Data e ora. (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* Non è possibile spostare un frammento esperienza in un’altra cartella anche se il modello è elencato in modelli consentiti. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - Editor pagina {#sites-pageeditor-6516}

* Aggiorna le dipendenze per il miglioramento del risolutore risorse effettuato in SITES-8464 in cui il rendering della pagina in modalità Authoring ha creato un numero elevato di `TemplatedResourceImpl` oggetti. (SITES-9350)


## Sling {#sling-6516}

* Experience Manager bloccato all&#39;avvio. (NPR-39832)
* Quando nell’archivio delle versioni di Experience Manager sono presenti molti percorsi personalizzati, l’avvio dell’Experience Manager non riesce. (NPR-38955)


## Progetti di traduzione {#translation-6516}

* In `MicrosoftTranslationServiceImpl`, il parametro della stringa query `Category` non è corretto. (NPR-39828)
* La creazione di un progetto di traduzione visualizza l’errore *La risorsa della pagina master non esiste*; il progetto di traduzione non viene creato. (NPR-39762)
* Impossibile impostare una data di scadenza per un progetto di traduzione che utilizza un connettore di traduzione umano. (NPR-39593)

## Interfaccia utente {#ui-6516}

* Quando si passa a una risoluzione più piccola, DatePicker non viene visualizzato e la selezione AM/PM non viene visualizzata o modificata in modo visibile. (NPR-39948)
* Quando si utilizza minify js (minimizzazione di JavaScript), non elabora la minimizzazione a causa di un errore di analisi. (NPR-39650)
* Campo tag (`/libs/cq/gui/components/coral/common/form/tagfield`) è in conflitto con la timeline. (CQ-4350751)


## WCM {#wcm-6516}

* L’azione di anteprima di rollout non deve elencare la pagina da creare. (CQ-4266213, SITES-10355)

## Flusso di lavoro {#workflow-6516}

* Eliminazione manuale del modello di flusso di lavoro modificabile da `/conf` lascia un&#39;istanza di modello runtime persistente senza un modello modificabile. (CQ-4349365)


## Installa [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 richiede [!DNL Experience Manager] 6.5. Vedi [documentazione di aggiornamento](/help/sites-deploying/upgrade.md) per istruzioni dettagliate. <!-- UPDATE FOR EACH NEW RELEASE -->
* Il download del service pack è disponibile ad Adobe [Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html).
* In una distribuzione con MongoDB e più istanze, installare [!DNL Experience Manager] 6.5.16.0 su una delle istanze Autore che utilizza Gestione pacchetti.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe sconsiglia di rimuovere o disinstallare il [!DNL Experience Manager] pacchetto 6.5.16.0. Pertanto, prima di installare il pacchetto, è necessario creare un backup del `crx-repository` nel caso sia necessario riportarlo indietro. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


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

Esistono due metodi diversi per l&#39;installazione automatica [!DNL Experience Manager] 6.5.16.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Inserire il pacchetto in `../crx-quickstart/install` quando il server è disponibile online. Il pacchetto viene installato automaticamente.
* Utilizza la [API HTTP da Gestione pacchetti](/help/sites-administering/package-manager.md#package-share). Utilizzo `cmd=install&recursive=true` in modo che i pacchetti nidificati siano installati.

>[!NOTE]
>
>Experience Manager 6.5.16.0 non supporta l’installazione di Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Convalida l&#39;installazione**

Per informazioni sulle piattaforme certificate per l’utilizzo con questa versione, consulta [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

1. La pagina delle informazioni sul prodotto (`/system/console/productinfo`) visualizza la stringa di versione aggiornata `Adobe Experience Manager (6.5.16.0)` sotto [!UICONTROL Prodotti installati]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tutti i bundle OSGi sono **[!UICONTROL ATTIVO]** o **[!UICONTROL FRAMMENTO]** nella console OSGi (Usa console Web: `/system/console/bundles`).

1. Il bundle OSGi `org.apache.jackrabbit.oak-core` è versione 1.22.14 o successiva (Usa console Web: `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installa Service Pack per [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

Per istruzioni su come installare il service pack su AEM Forms, vedi [Istruzioni per l&#39;installazione di AEM Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installa il pacchetto indice GraphQL per frammenti di contenuto di Experience Manager {#install-aem-graphql-index-add-on-package}

I clienti che utilizzano GraphQL devono installare [Frammento di contenuto AEM con pacchetto indice GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip).

Questo consente di aggiungere la definizione dell’indice richiesta in base alle funzioni effettivamente utilizzate.

Se non si installa il pacchetto, le query GraphQL potrebbero essere lente o non essere riuscite.

>[!NOTE]
>
>Questo pacchetto deve essere installato una sola volta per istanza; non è necessario reinstallarlo con ogni Service Pack.

### UberJar {#uber-jar}

UberJar per [!DNL Experience Manager] 6.5.16.0 è disponibile nella [Archivio centrale Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>In Experience Manager 6.5.16.0, la versione UberJar (6.5.15.0) rimane la stessa della versione precedente.


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
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Aggiorna le query GraphQL che potrebbero aver utilizzato un nome API personalizzato per il modello di contenuto utilizzando invece il nome predefinito del modello di contenuto.

* Una query GraphQL può utilizzare `damAssetLucene` al posto del `fragments` indice. Questo potrebbe causare un errore delle query GraphQL o richiedere molto tempo per l’esecuzione.

   Per correggere il problema, `damAssetLucene` deve essere configurato in modo da includere le due proprietà seguenti:

   * `contentFragment`
   * `model`

   Una volta modificata la definizione dell&#39;indice, è necessaria una reindicizzazione (`reindex` = `true`).

   Dopo questi passaggi, le query GraphQL dovrebbero essere eseguite più velocemente.

* Come [!DNL Microsoft®® Windows Server 2019] non supporta [!DNL MySQL 5.7] e [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] non supporta installazioni chiavi in mano per [!DNL AEM Forms 6.5.10.0].

* Se si aggiorna il [!DNL Experience Manager] istanza da 6.5.0 a 6.5.4 all&#39;ultimo service pack su Java™ 11, vedi `RRD4JReporter` eccezioni `error.log` file. Per interrompere le eccezioni, riavvia l&#39;istanza di [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Gli utenti possono rinominare una cartella in una gerarchia [!DNL Assets] e pubblicare una cartella nidificata in [!DNL Brand Portal]. Tuttavia, il titolo della cartella non viene aggiornato in [!DNL Brand Portal] finché la cartella principale non viene ripubblicata.

* Quando un utente seleziona di configurare un campo per la prima volta in un modulo adattivo, l’opzione per salvare una configurazione non viene visualizzata in Browser proprietà. Se si seleziona per configurare altri campi del modulo adattivo nello stesso editor, il problema viene risolto.

* Durante l&#39;installazione di [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando l’integrazione Adobe Target è configurata in [!DNL Experience Manager] se si utilizza l’API di Target Standard (autenticazione IMS) e poi si esportano frammenti di esperienza in Target, vengono creati tipi di offerta errati. Invece del tipo &quot;Frammento esperienza&quot;/sorgente &quot;Adobe Experience Manager&quot;, Target crea diverse offerte con il tipo &quot;HTML&quot;/sorgente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nessuna finestra di manutenzione trovata in granite/operazioni/manutenzione.
   * La convalida lato server del modulo adattivo non riesce quando vengono utilizzate funzioni di aggregazione come SUM, MAX e MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nessuna finestra di manutenzione trovata in granite/operazioni/manutenzione.
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

* In AEM Forms, il protocollo POP3 non funziona con gli endpoint e-mail per Microsoft® Office 365.
* Sulla piattaforma JBoss® 7.1.4, quando l&#39;utente installa AEM service pack 6.5.16.0, `adobe-livecycle-jboss.ear` distribuzione non riuscita.

## Bundle OSGi e pacchetti di contenuti inclusi {#osgi-bundles-and-content-packages-included}

Nei seguenti documenti di testo sono elencati i bundle OSGi e i pacchetti di contenuti inclusi in [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Elenco dei bundle OSGi inclusi nell&#39;Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Elenco dei pacchetti di contenuti inclusi in Experience Manager 6.5.16.0](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Siti web limitati {#restricted-sites}

Questi siti web sono disponibili solo per i clienti. Se sei un cliente e hai bisogno di accedere, contatta il tuo responsabile commerciale di Adobe.

* [Download del prodotto da licensing.adobe.com](https://licensing.adobe.com/)
* [Contatta l’Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] pagina di prodotto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 documentazione](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it)
>* [Abbonati ad Adobe priority product update](https://www.adobe.com/subscription/priority-product-update.html)

