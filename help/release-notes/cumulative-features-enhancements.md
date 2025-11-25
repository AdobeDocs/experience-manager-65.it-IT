---
title: Funzioni chiave e miglioramenti cumulativi nella versione 6.5 di Adobe Experience Manager.
description: Elenco cumulativo delle funzioni chiave e dei miglioramenti apportati in Adobe Experience Manager 6.5 dalle otto versioni precedenti dei service pack.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '3109'
ht-degree: 9%

---

# Funzioni principali e miglioramenti cumulativi

Elenco cumulativo delle funzioni chiave e dei miglioramenti introdotti in Adobe Experience Manager 6.5 per le otto versioni precedenti dei service pack.

Consulta anche [Note sulla versione più recente del Service Pack di Adobe Experience Manager 6.5](/help/release-notes/release-notes.md).


## AEM 6.5, Service Pack 23 - 22 maggio 2025

### Forms {#forms-sp23}

* [Collegamenti ipertestuali accessibili con stili di testo misti nei PDF statici](https://helpx.adobe.com/content/dam/help/it/experience-manager/6-5/forms/pdf/using-designer.pdf): i collegamenti ipertestuali contenenti stili di testo misti nei PDF statici sono ora contrassegnati come un singolo elemento accessibile. Questo miglioramento semplifica la struttura ad albero dei tag, migliora la navigazione degli assistenti vocali e supporta una migliore conformità in materia di accessibilità.

* [Matrice di piattaforma supportata aggiornata](/help/forms/using/aem-forms-jee-supported-platforms.md)

  La versione più recente introduce aggiornamenti alla matrice di piattaforma supportata, garantendo la compatibilità con le tecnologie più recenti.

   * Client IBM® Content Manager 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Driver JDBC Microsoft® SQL Server 12.8

   * Red Hat® Enterprise Linux® 9 (kernel 4.x, 64 bit)

* [Componente allegato file protetto](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): come misura di sicurezza, il componente ora impedisce l&#39;invio di file con estensioni modificate che tentano di ignorare i controlli dei tipi di file consentiti. Tali file vengono bloccati durante l’invio per garantire che siano accettati solo i tipi di file validi.

## AEM 6.5, Service Pack 22 - 21 novembre 2024

### Sites {#sites}

[L&#39;editor universale](/help/sites-developing/universal-editor/introduction.md) è ora disponibile in AEM 6.5 per i casi d&#39;uso headless con l&#39;applicazione di un feature pack.

### [!DNL Assets]

La scheda IPTC ora supporta [!UICONTROL Alt Text] e [!UICONTROL Extended Description] campi di testo. (Assets-34918)

### Forms {#forms-sp22}

#### Nuove funzioni GA in AEM Forms {#ga-aem-forms-sp22}

* È stato aggiunto il supporto per abilitare l&#39;incorporamento dei font nelle [API Batch di comunicazioni interattive](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel). Le comunicazioni interattive ora includono il supporto per l&#39;incorporamento dei font Adobe Ming e Adobe Myungjo nei PDF generati tramite l&#39;API Batch. Questo miglioramento garantisce un rendering accurato del testo nei documenti generati, anche quando si utilizzano sottoinsiemi di font, fornendo un migliore supporto per contenuti multilingue negli output di PDF.

* [API per l&#39;accesso facilitato di PDF](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - AEM Forms su OSGi ora supporta la nuova API per tag TOC per migliorare PDF per gli standard di accesso facilitato. Rende i PDF più accessibili agli utenti con tecnologia assistiva.

* [Risoluzione XDP del frammento](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository): AEM Forms su OSGi ora risolve gli XDP del frammento a cui si fa riferimento negli XDP primari e memorizzati nell&#39;archivio AEM CRX.

* [Miglioramenti alla conformità di PDF/A](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) - Ora gli utenti possono convertire i PDF in formati PDF/A (1a, 2a, 3a) a scopo di archiviazione, garantendo al contempo l&#39;accessibilità e verificando la conformità a questi standard.

* **Supporto per il ridimensionamento automatico dei caratteri per i documenti PDF statici** - AEM Forms Designer, OutputService e FormsService ora supportano il ridimensionamento automatico dei caratteri per i PDF statici. Se l&#39;utente imposta la dimensione del carattere 0 per i campi di tipo testo, numerico, password o datetime, la dimensione del carattere viene regolata automaticamente all&#39;interno di questi campi senza modificare la dimensione complessiva del campo. Per utilizzare la funzione, gli utenti passano un flag nell&#39;XCI personalizzato: `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

#### Nuove funzioni di Beta in AEM Forms {#beta-aem-forms-sp22}

La funzione beta offre un’opportunità unica per ottenere accesso esclusivo alle innovazioni all’avanguardia e aiutarti a modellarne lo sviluppo. Ti interessa abilitare una funzione beta per i tuoi ambienti? Invia un’e-mail dal tuo indirizzo ufficiale a aem-forms-ea@adobe.com con l’elenco delle funzionalità che ti interessano.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) e [Servizi CAPTCHA di Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md): AEM Forms supporta i seguenti servizi Captcha:
   * Captcha protegge i moduli da bot, spam e abusi automatizzati sfidando gli utenti con un widget di casella di controllo. Garantisce che solo gli utenti umani procedano, migliorando la sicurezza per le transazioni online.
   * Cloudflare Turnstile offre una misura di sicurezza che mira a proteggere i moduli da bot automatizzati, attacchi dannosi, spam e traffico automatizzato indesiderato. Presenta una casella di controllo all’invio del modulo per verificare che sia umana, prima di consentire loro di inviare il modulo.

* Controllo delle versioni dei moduli adattivi:
   * [Creare più versioni di un modulo adattivo](/help/forms/using/add-versioning-reviews-comments.md) - Ora gli utenti possono gestire facilmente le varianti dei moduli esistenti. Questo processo semplifica il controllo delle versioni e facilita il confronto per l’ottimizzazione dei moduli, il tutto all’interno di un unico flusso di lavoro semplificato.
   * [Confronta Forms adattivo](/help/forms/using/compare-forms-core-components.md): ora gli utenti possono confrontare facilmente due moduli per identificare le differenze. Questo semplifica la collaborazione consentendo ai membri del gruppo di confrontare le revisioni e discutere le modifiche in modo efficiente.

## AEM 6.5, Service Pack 21 - 6 giugno 2024

### [!DNL Assets]

#### Miglioramenti

La scheda IPTC ora supporta [!UICONTROL Alt Text] e [!UICONTROL Extended Description] campi di testo. (Assets-34918)

#### Accessibilità

* Se lo stato di elaborazione di una risorsa è Non riuscito o Metadati non riusciti, l’interfaccia utente delle didascalie e delle tracce audio ora funziona in modo appropriato. (Assets-37281)
* Quando salvi i metadati di una risorsa e provi a modificarli, ora viene visualizzato il nome della lingua. (Assets-37281)

### [!DNL Forms]

* **Supporto per le credenziali Oauth**: credenziali nuove e più facili da utilizzare per l&#39;autenticazione server-to-server, che sostituiscono le credenziali dell&#39;account di servizio (JWT) esistenti. (NPR-41994)
* [Miglioramenti all&#39;editor di regole in AEM Forms](/help/forms/using/rule-editor-core-components.md):
   * Supporto per l&#39;implementazione di condizioni nidificate con funzionalità `When-then-else`.
   * Convalidare o reimpostare pannelli e moduli, inclusi i campi.
   * Supporto delle funzioni JavaScript moderne, ad esempio le funzioni let e arrow (supporto ES10) all’interno delle funzioni personalizzate.
* [API di assegnazione tag automatici per l&#39;accessibilità di PDF](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services): AEM Forms su OSGi ora supporta la nuova API di assegnazione tag automatici per migliorare PDF per gli standard di accessibilità aggiungendo tag: paragrafi ed elenchi. Rende i PDF più accessibili agli utenti con tecnologia assistiva.
* **Supporto PNG a 16 bit**: il servizio ImageToPdf di PDF Generator ora supporta la conversione di PNG con profondità colore a 16 bit.
* **Applicare artefatti a singoli blocchi di testo in XDP**: Forms Designer ora consente agli utenti di configurare le impostazioni per singoli blocchi di testo nei file XDP. Questa funzionalità consente di controllare gli elementi trattati come artefatti nei PDF risultanti. Questi elementi, come intestazioni e piè di pagina, sono resi accessibili per le tecnologie per l’accessibilità. Le funzioni chiave includono contrassegnare i blocchi di testo come artefatti e incorporare queste impostazioni nei metadati XDP. Il servizio Output di Forms applica queste impostazioni durante la generazione di PDF, garantendo la corretta assegnazione di tag PDF/UA.
* **AEM Forms Designer è certificato con `GB18030:2022` standard**: con la certificazione `GB18030:2022`, ora Forms Designer supporta il set di caratteri Unicode cinese che consente di inserire caratteri cinesi in tutti i campi e le finestre di dialogo modificabili.
* [Supporto per la route WebToPDF nel server JEE](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) tramite il servizio PDF Generator ora supporta la route WebToPDF per la conversione di file HTML in documenti PDF in JEE. Questo supporto si aggiunge alle route Webkit e WebCapture esistenti (solo Windows). Mentre la route WebToPDF è già disponibile su OSGi ed estesa a JEE. Ora, su entrambe le piattaforme JEE e OSGi, il servizio PDF Generator supporta le seguenti route tra diversi sistemi operativi:
   * **Windows**: WebKit, WebCapture, WebToPDF
   * **Linux®**: Webkit, WebToPDF


## AEM 6.5, Service Pack 20 - 22 febbraio 2024

### [!DNL Assets]

* Dynamic Media ora supporta il formato immagine HEIC senza perdita di dati per Apple iOS/iPadOS. Consulta [fmt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt) nell&#39;API di server e rendering immagini Dynamic Media.
* Multisite Manager (MSM) ora supporta le strutture dei frammenti di esperienza, incluse cartelle e sottocartelle, per un rollout in blocco efficiente dei frammenti di esperienza in Live Copy.

### [!DNL Forms]

* **Generazione rapporti sulle transazioni in AEM Forms su JEE**: è stata introdotta la funzionalità di generazione rapporti sulle transazioni per AEM Forms su JEE. Consente la registrazione completa delle transazioni dei documenti, ad esempio Conversioni, Rappresentazioni e Invii. Questo miglioramento aumenta l’efficienza e facilita una migliore conservazione dei documenti. La funzione è disabilitata per impostazione predefinita. Puoi abilitarlo dall’interfaccia utente di amministrazione.
* **Sicurezza avanzata con supporto ECDSA**: AEM Forms offre ora un supporto affidabile per l&#39;algoritmo ECDSA (Elliptic Curve Digital Signature Algorithm) in entrambi gli stack JEE e OSGi. Gli utenti possono ora firmare, certificare e verificare i documenti di PDF con maggiore sicurezza. Gli algoritmi di curva EC supportati includono:
   * Curva ellittica ECDSA P256 con algoritmo di digest SHA256
   * Curva ellittica ECDSA P384 con algoritmo di digest SHA384
   * Curva ellittica ECDSA P512 con algoritmo di digest SHA512
* **Compatibilità perfetta con Windows 11 per Forms Designer**: AEM Forms Designer ora supporta Windows 11, garantendo una corretta installazione e funzionamento. Gli utenti possono effettuare l&#39;aggiornamento a Windows 11 senza dover reinstallare Forms Designer o preoccuparsi di problemi di compatibilità, garantendo così un flusso di lavoro ininterrotto.
* **Accesso facilitato con ruolo personalizzato &quot;Didascalia&quot; in AEM Forms Designer**: AEM Forms Designer ora include un ruolo di accesso facilitato personalizzato denominato &quot;Didascalia&quot;, che consente agli utenti di creare XDP con elementi di didascalia personalizzati. Questa funzione migliora l’accessibilità consentendo agli utenti di integrare didascalie personalizzate nelle progettazioni dei documenti in modo da migliorare l’inclusività e l’esperienza utente.

## AEM 6.5, Service Pack 19 - 7 dicembre 2023

* Abilitazione dell’utente del componente Editor pagina/Immagine di Sites per fare riferimento alle risorse dal Cloud Service Assets remoto. (SITES-13448, SITES-13433)
* AEM ora supporta l’ordinamento lato server per velocizzare la navigazione dei progetti nella vista a elenco. I nodi del progetto vengono ordinati in base alla colonna selezionata dall’utente prima di essere visualizzati nell’interfaccia.

### [!DNL Forms]

* **Nuovi componenti core modulo adattivo**: sono state aggiunte schede verticali, termini e condizioni e casella di controllo per migliorare la scalabilità dei moduli.
   * **[Componente casella di controllo](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**: Forms adattivo basato su componenti core ora può includere un componente casella di controllo. Consente agli utenti di effettuare scelte binarie, selezionando o deselezionando una particolare opzione. In genere viene visualizzata come una piccola casella su cui è possibile fare clic o toccare per alternare due stati: selezionato e deselezionato. La casella di controllo è un elemento modulo comune utilizzato per presentare una scelta sì/no o vero/falso.

   * **[Componente termini e condizioni](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**: il Forms adattivo basato su componenti core ora include un componente termini e condizioni. Gli autori dei moduli aggiungono questa sezione per mostrare agli utenti i termini, le condizioni o gli accordi legali per il servizio, il prodotto o la piattaforma. Questo componente è progettato per informare gli utenti sulle regole, le normative e gli obblighi che si impegnano a rispettare inviando il modulo.

     ![Schede verticali, termini e condizioni e componenti casella di controllo](/help/forms/using/assets/forms-components.png)

   * **[Componente schede verticali](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**: Forms adattivo basato su componenti core ora può organizzare il contenuto del modulo in un elenco verticale di schede, fornendo un layout strutturato e navigabile. Le schede verticali in un modulo migliorano l’esperienza utente semplificando la navigazione e organizzando il contenuto. Sono particolarmente utili quando il modulo contiene più sezioni o informazioni complesse.

* **[Versione a 64 bit di AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: la versione a 64 bit di AEM Forms Designer offre prestazioni, scalabilità e gestione della memoria migliorate per migliorare l&#39;esperienza di creazione dei moduli. Grazie all&#39;architettura a 64 bit, è possibile gestire con facilità progetti ancora più grandi e complessi, garantendo flussi di lavoro di progettazione ottimizzati ed efficienza. Migliora le funzionalità di progettazione dei moduli e abbraccia il futuro di AEM Forms Designer con questa versione all’avanguardia.

* **[Collegare un Forms adattivo all&#39;elenco Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms fornisce un&#39;integrazione preconfigurata per inviare i dati dei moduli direttamente all&#39;elenco SharePoint, consentendo di utilizzare le funzionalità degli elenchi SharePoint. È possibile configurare Microsoft® SharePoint List come origine dati per un modello dati modulo e utilizzare l’azione Invia utilizzando il modello dati modulo per inviare un modulo adattivo a SharePoint List.

* **[Supporto per la configurazione delle proprietà del documento di record per i frammenti di moduli adattivi](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: è ora possibile personalizzare facilmente i frammenti di moduli adattivi e i relativi campi nell&#39;editor di moduli adattivi.

* **XMLFM a 64 bit**: l&#39;iterazione a 64 bit di XMLFM offre prestazioni, scalabilità e gestione della memoria migliorate. È il primo servizio nativo a 64 bit implementato sul lato server. Sfruttando la capacità intrinseca di accedere a risorse di memoria più grandi rispetto alla sua controparte a 32 bit, XMLFM a 64 bit consente la gestione senza problemi di carichi di lavoro di rendering più grandi. Questa tappa rappresenta non solo un salto nelle prestazioni, ma introduce anche miglioramenti fondamentali al framework di servizio nativo all’interno del server AEM Forms. Questo aggiornamento consente ad AEM Forms Server di supportare senza problemi qualsiasi servizio nativo a 64 bit.

## AEM 6.5, Service Pack 18 - 24 agosto 2023

* Assets, Dynamic Media - [Supporto di più sottotitoli e tracce audio per video in Dynamic Media](/help/assets/video.md#about-msma). È ora possibile aggiungere facilmente più sottotitoli e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. È possibile personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono anche gestire i sottotitoli e le tracce audio da una singola scheda nell’interfaccia utente.
* Assets - Dai risultati della ricerca, ora puoi passare alla posizione della cartella che contiene una risorsa per eseguire varie attività di gestione delle risorse.
* Il selettore Polaris di Sites nei frammenti di contenuto ha migliorato le prestazioni.
* Abilitazione dell’utente del componente Editor pagina/Immagine di Sites per fare riferimento alle risorse dal Cloud Service Assets remoto.
* Per trovare rapidamente un progetto nella vista a elenco, in cui è possibile che siano presenti molti progetti, Adobe ora supporta l’ordinamento lato server. I nodi del progetto sono ordinati sul backend in base alla colonna selezionata dall’utente prima di eseguirne il rendering nell’interfaccia utente.
* AEM 6.5.18.0 supporta MongoDB da 5.0 a 6.0.

### [!DNL Forms]

* **[Gestione avanzata degli errori con gestori di errori personalizzati nell&#39;editor di regole](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** - È ora possibile richiamare una funzione personalizzata (utilizzando la libreria client) in risposta a un errore restituito da un servizio esterno. Inoltre, è possibile fornire una risposta personalizzata agli utenti finali. In alternativa, è possibile eseguire azioni specifiche per gli errori restituiti da un servizio. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel backend per codici di errore specifici o informare il cliente che il servizio non è disponibile

* **[Passaggio del flusso di lavoro Adobe Sign migliorato](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** - Il passaggio del flusso di lavoro Adobe Sign nei flussi di lavoro di AEM è disponibile con i seguenti miglioramenti.

   * **Sicurezza migliorata con l&#39;autenticazione basata su ID governativi per Adobe Sign** - L&#39;autenticazione basata su ID governativi di Adobe Acrobat Sign offre un ulteriore livello di verifica. Consente agli utenti di autenticare la propria identità utilizzando gli ID governativi (patente di guida, carta d&#39;identità, passaporto). Utilizzando documenti di identificazione attendibili, questo miglioramento aggiunge un ulteriore livello di affidabilità al processo di firma, rendendolo ideale per scenari che richiedono maggiore sicurezza, conformità e convalida degli utenti.

   * **Trasparenza migliorata tramite Audit Trail per i documenti Adobe Sign**. Utilizza la funzione Audit Trail per ottenere informazioni dettagliate sul ciclo di vita dei documenti Adobe Sign. Con Audit Trail è ora possibile mantenere un registro completo di tutte le azioni e interazioni relative ai documenti. Queste azioni e interazioni includono l’utente che ha visualizzato, modificato o firmato il documento, oltre ai timestamp di ogni evento. Questo miglioramento è fondamentale per mantenere la conformità, risolvere le controversie e garantire l’integrità degli accordi digitali.


   * **I ruoli per i destinatari del contratto sono stati estesi oltre al solo firmatario** - Adobe Acrobat Sign consente di espandere i ruoli per i destinatari del contratto oltre al solo firmatario per soddisfare meglio i requisiti del flusso di lavoro. Quando questa opzione è abilitata, ogni destinatario di un contratto ha il proprio ruolo configurabile singolarmente, con Firmatario come impostazione predefinita.


* **[Programma di installazione completo per AEM Forms su JEE](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** - Il service pack include un programma di installazione completo per AEM Forms su JEE che supporta più nuove combinazioni di software, tra cui:
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C su Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Connettore JDBC MySQL 8

Se stai installando o pianificando di utilizzare il software più recente per il tuo ambiente AEM 6.5 Forms su JEE, Adobe consiglia di utilizzare il programma di installazione completo di AEM 6.5.18.0 Forms su JEE. Per esplorare l’elenco completo dei nuovi software aggiunti e obsoleti, consulta la documentazione di AEM Forms su JEE o AEM Forms su OSGi.

## AEM 6.5, Service Pack 17 - 25 maggio 2023

* **Miglioramenti all’esperienza di ricerca**: è ora possibile eseguire rapidamente le seguenti operazioni sulle risorse visualizzate nei risultati di ricerca:
   * Crea un flusso di lavoro
   * Crea una versione
   * Correla o non correla risorse

  Per eseguire queste operazioni, non è necessario passare alla posizione della risorsa e visualizzarne le proprietà.

* **Dynamic Media _Snapshot_**consente di visualizzare in anteprima i modificatori di immagini e le ottimizzazioni di Smart Imaging, ad esempio l&#39;output WebP o AVIF, la compressione in base alla larghezza di banda e il ridimensionamento delle proporzioni pixel del dispositivo, utilizzando immagini di test o URL di Dynamic Media. Puoi quindi confrontare immediatamente il modo in cui ogni impostazione influisce sulla qualità e sulla dimensione del file.
Consulta [Dynamic Media Snapshot](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot).
* **Streaming DASH con Dynamic Media** - Nuovo protocollo (DASH - Dynamic Adaptive Streaming over HTTP) avviato per lo streaming adattivo nella distribuzione video Dynamic Media (con CMAF abilitato). Disponibile ora per tutte le aree geografiche.
* **Integrazione di Experience Manager Sites e frammenti di contenuto con Assets Dynamic Media di nuova generazione** - Gli utenti possono ora utilizzare le risorse ospitate nel cloud in Experience Manager Sites 6.5. Possono creare e distribuire tali risorse on-premise o sulle istanze Managed Services.

### [!DNL Forms]

* **[Forms adattivo nell&#39;Editor pagine di AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** - È ora possibile utilizzare l&#39;Editor pagine di AEM per creare e aggiungere rapidamente più moduli alle pagine dei siti. Questa funzionalità consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno delle pagine di Sites utilizzando la potenza dei componenti per moduli adattivi, tra cui il comportamento dinamico, le convalide, l’integrazione dei dati, la generazione di documenti di record e l’automazione dei processi aziendali. Operazioni disponibili:
   * Crea un modulo adattivo trascinando i componenti del modulo sul componente Contenitore Forms adattivo nell’editor AEM Sites o nei Frammenti esperienza.
   * Utilizza l’Adaptive Forms Wizard (Impostazione rapida adattivo) nell’editor di AEM Sites per creare moduli indipendentemente da qualsiasi pagina Sites, e puoi riutilizzarli su più pagine.
   * Aggiungere più moduli a una pagina di Sites per semplificare l’esperienza utente e fornire maggiore flessibilità.
* **[Supporto di reCAPTCHA Enterprise in Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)** - Aggiunto supporto per reCAPTCHA Enterprise in Experience Manager Forms. Questa funzionalità offre una protezione avanzata contro attività fraudolente e spam, oltre al supporto Google reCAPTCHA v2 esistente.
* **[È stato aggiunto il supporto per Adobe Acrobat Sign for Government con Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**. AEM Forms ora si integra con Adobe Acrobat Sign for Government (compatibile con FedRAMP). Questa integrazione fornisce un livello avanzato di conformità e sicurezza per le firme elettroniche con l’invio di moduli adattivi per gli account governativi associati (dipartimenti e agenzie governative). Le integrazioni con Adobe Acrobat Sign for Government consentono ai partner Adobe e ai clienti governativi di utilizzare le firme elettroniche in Adaptive Forms per alcune delle linee di business più critiche e sensibili. Questo ulteriore livello di sicurezza garantisce che tutte le firme elettroniche siano pienamente conformi alla conformità FedRAMP Moderate, garantendo ai clienti del settore pubblico di Adobe la massima tranquillità.
* **Abilitare l&#39;integrazione di Salesforce con Experience Manager Forms per lo scambio di dati** - Configurare l&#39;integrazione tra Experience Manager Forms e l&#39;applicazione Salesforce utilizzando il flusso di credenziali client OAuth 2.0. Questa funzionalità consente l&#39;autenticazione e l&#39;autorizzazione sicure e dirette dell&#39;applicazione e permette una comunicazione fluida senza il coinvolgimento dell&#39;utente.
* **Ottimizzazione e funzionalità migliorate del motore del flusso di lavoro**: aumenta le prestazioni dei motori del flusso di lavoro riducendo al minimo il numero di istanze del flusso di lavoro. Oltre ai valori di stato `COMPLETED` e `RUNNING`, il flusso di lavoro supporta anche tre nuovi valori di stato: `ABORTED`, `SUSPENDED` e `FAILED`.

## AEM 6.5, Service Pack 16 - 23 febbraio 2023

È stato avviato il nuovo DASH (Dynamic Adaptive Streaming over HTTP) del protocollo per lo streaming con bitrate adattivo nella distribuzione di video Dynamic Media (con CMAF [Common Media Application Format] abilitato).

* Lo streaming adattivo (DASH/HLS) garantisce una migliore esperienza di visualizzazione per i video per l’utente finale.
* DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore.
* Disponibile ora in Asia-Pacifico e Nord America; disponibile a breve in Europa-Medio Oriente-Africa.

### [!DNL Forms]

* [Forms adattivo headless](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview) consente agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui interagire tramite API, anziché tramite un&#39;interfaccia utente grafica tradizionale.

* [I componenti core adattivi di Forms](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#features) sono un set di 24 componenti open source conformi a BEM e basati sui componenti core di Adobe Experience Manager WCM. Questi componenti sono open source e consentono agli sviluppatori di personalizzarli ed estenderli facilmente in base alle esigenze specifiche dell’organizzazione. Chiunque disponga delle competenze necessarie per personalizzare [Componenti core WCM](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/get-started/authoring) può personalizzare e assegnare uno stile a tali componenti.

* Il servizio Reader Extension su OSGi ora fornisce opzioni separate per abilitare i diritti di utilizzo di importazione ed esportazione su un PDF per importare o esportare dati in Adobe Acrobat Reader.
