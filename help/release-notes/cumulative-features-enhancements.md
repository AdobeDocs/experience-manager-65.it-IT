---
title: Funzioni chiave e miglioramenti cumulativi nella versione 6.5 di Adobe Experience Manager.
description: Elenco cumulativo delle funzioni chiave e dei miglioramenti apportati in Adobe Experience Manager 6.5 dalle otto versioni precedenti dei service pack.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: a49af471c5fc2f799687173bff6cdcb21505740a
workflow-type: tm+mt
source-wordcount: '2335'
ht-degree: 19%

---

# Funzioni principali e miglioramenti cumulativi

Elenco cumulativo delle funzioni chiave e dei miglioramenti introdotti in Adobe Experience Manager 6.5 per le otto versioni precedenti dei service pack.

Consulta anche [Note sulla versione più recente del Service Pack di Adobe Experience Manager 6.5](/help/release-notes/release-notes.md).

## AEM 6.5, Service Pack 18 - 7 dicembre 2023

* Abilitazione dell’utente del componente Editor pagina/immagine di Sites per fare riferimento alle risorse dal Cloud Service Assets remoto. (SITES-13448, SITES-13433)
* AEM ora supporta l’ordinamento lato server per una navigazione più rapida dei progetti nella vista a elenco. I nodi del progetto vengono ordinati in base alla colonna selezionata dall’utente prima di essere visualizzati nell’interfaccia.

### [!DNL Forms]

* **Nuovi componenti core modulo adattivo**: sono state aggiunte schede verticali, termini e condizioni e casella di controllo per migliorare la scalabilità dei moduli.
   * **[Componente casella di controllo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: Forms adattivo basato su componenti core ora può includere un componente casella di controllo. Consente agli utenti di effettuare scelte binarie, selezionando o deselezionando una particolare opzione. In genere viene visualizzata come una piccola casella su cui è possibile fare clic o toccare per alternare due stati: selezionato e deselezionato. La casella di controllo è un elemento modulo comune utilizzato per presentare una scelta sì/no o vero/falso.

   * **[Componente termini e condizioni](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: Forms adattivo basato su componenti core può ora includere un componente termini e condizioni. Consente agli autori di Forms di introdurre una sezione specifica nel modulo in cui agli utenti vengono presentati i termini, le condizioni o gli accordi legali associati all’utilizzo di un servizio, un prodotto o una piattaforma. Questo componente è progettato per informare gli utenti sulle regole, le normative e gli obblighi che si impegnano a rispettare inviando il modulo.

     ![Schede verticali, termini e condizioni e componenti casella di controllo](/help/forms/using/assets/forms-components.png)

   * **[Componente schede verticali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: Forms adattivo basato su componenti core ora può organizzare il contenuto del modulo in un elenco verticale di schede, fornendo un layout strutturato e navigabile. L’utilizzo di schede verticali in un modulo può migliorare l’esperienza utente complessiva semplificando la navigazione e migliorando l’organizzazione del contenuto del modulo, soprattutto nelle situazioni in cui un modulo contiene più sezioni o informazioni complesse.

* **[Versione a 64 bit di AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: la versione a 64 bit di AEM Forms Designer offre prestazioni, scalabilità e gestione della memoria migliorate per migliorare l&#39;esperienza di creazione dei moduli. Grazie all&#39;architettura a 64 bit, è possibile gestire con facilità progetti ancora più grandi e complessi, garantendo flussi di lavoro di progettazione ottimizzati ed efficienza. Migliora le funzionalità di progettazione dei moduli e abbraccia il futuro di AEM Forms Designer con questa versione all’avanguardia.

* **[Collegare un Forms adattivo all&#39;elenco Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms fornisce un&#39;integrazione preconfigurata per inviare i dati dei moduli direttamente all&#39;elenco SharePoint, consentendo di utilizzare le funzionalità degli elenchi SharePoint. È possibile configurare Microsoft® SharePoint List come origine dati per un modello dati modulo e utilizzare l’azione Invia utilizzando il modello dati modulo per inviare un modulo adattivo a SharePoint List.

* **[Supporto per la configurazione delle proprietà del documento di record per i frammenti di moduli adattivi](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: è ora possibile personalizzare facilmente i frammenti di moduli adattivi e i relativi campi nell&#39;editor di moduli adattivi.

* **XMLFM a 64 bit**: l&#39;iterazione a 64 bit di XMLFM offre prestazioni, scalabilità e gestione della memoria migliorate. È il primo servizio nativo a 64 bit implementato sul lato server. Sfruttando la capacità intrinseca di accedere a risorse di memoria più grandi rispetto alla sua controparte a 32 bit, XMLFM a 64 bit consente la gestione senza problemi di carichi di lavoro di rendering più grandi. Questa tappa rappresenta non solo un salto nelle prestazioni, ma introduce anche miglioramenti fondamentali al framework di servizio nativo all’interno del server AEM Forms. Questo aggiornamento consente ad AEM Forms Server di supportare senza problemi qualsiasi servizio nativo a 64 bit.

## AEM 6.5, Service Pack 18 - 24 agosto 2023

* Assets, Dynamic Medie - [Supporto di più sottotitoli e tracce audio per i video in Dynamic Medie](/help/assets/video.md#about-msma) - È ora possibile aggiungere facilmente più sottotitoli e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. È possibile personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono anche gestire i sottotitoli e le tracce audio da una singola scheda nell’interfaccia utente.
* Assets - Dai risultati della ricerca, ora puoi passare alla posizione della cartella che contiene una risorsa per eseguire varie attività di gestione delle risorse.
* Il selettore Polaris di Sites nei frammenti di contenuto ha migliorato le prestazioni.
* Abilitazione dell’utente del componente Editor pagina/immagine di Sites per fare riferimento alle risorse dal Cloud Service Assets remoto.
* Per trovare rapidamente un progetto nella vista a elenco, in cui è possibile che siano presenti molti progetti, Adobe ora supporta l’ordinamento lato server. I nodi del progetto sono ordinati sul backend in base alla colonna selezionata dall’utente prima di eseguirne il rendering nell’interfaccia utente.
* L’AEM 6.5.18.0 supporta MongoDB da 5.0 a 6.0.

### [!DNL Forms]

* **[Gestione avanzata degli errori con gestori di errori personalizzati nell&#39;editor di regole](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)** - È ora possibile richiamare una funzione personalizzata (utilizzando la libreria client) in risposta a un errore restituito da un servizio esterno. Inoltre, è possibile fornire una risposta personalizzata agli utenti finali. In alternativa, è possibile eseguire azioni specifiche per gli errori restituiti da un servizio. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel backend per codici di errore specifici o informare il cliente che il servizio non è disponibile

* **[Passaggio del flusso di lavoro Adobe Sign migliorato](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** - Il passaggio del flusso di lavoro Adobe Sign nei flussi di lavoro AEM è disponibile con i seguenti miglioramenti.

   * **Sicurezza avanzata con autenticazione basata su ID governativi per Adobe Sign** - L&#39;autenticazione basata su ID governativi di Adobe Acrobat Sign offre un ulteriore livello di verifica. Consente agli utenti di autenticare la propria identità utilizzando gli ID governativi (patente di guida, carta d&#39;identità, passaporto). Utilizzando documenti di identificazione attendibili, questo miglioramento aggiunge un ulteriore livello di affidabilità al processo di firma, rendendolo ideale per scenari che richiedono maggiore sicurezza, conformità e convalida degli utenti.

   * **Trasparenza avanzata con Audit Trail per documenti Adobe Sign**. Utilizza la funzione Audit Trail per ottenere informazioni dettagliate sul ciclo di vita dei documenti Adobe Sign. Con l’Audit Trail è ora possibile mantenere un record completo di tutte le azioni e interazioni relative ai documenti. Tali azioni e interazioni includono dettagli quali visualizzazioni, modifiche o firme del documento, nonché le marche temporali di ciascun evento. Questo miglioramento è fondamentale per mantenere la conformità, risolvere le controversie e garantire l’integrità degli accordi digitali.


   * **I ruoli per i destinatari del contratto sono stati estesi oltre al solo firmatario** - Adobe Acrobat Sign consente di espandere i ruoli per i destinatari del contratto oltre al solo firmatario per soddisfare meglio i requisiti del flusso di lavoro. Quando questa opzione è abilitata, ogni destinatario di un contratto ha il proprio ruolo configurabile singolarmente, con Firmatario come impostazione predefinita.


* **[Programma di installazione completo per AEM Forms su JEE](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)** - Il service pack include un programma di installazione completo per AEM Forms su JEE che supporta più nuove combinazioni di software, tra cui:
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C su Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Connettore JDBC MySQL 8

Se stai installando o pianificando di utilizzare il software più recente per il tuo Forms AEM 6.5 in ambiente JEE, Adobe consiglia di utilizzare il programma di installazione completo di AEM 6.5.18.0 Forms su JEE. Per esplorare l’elenco completo dei nuovi software aggiunti e obsoleti, consulta la documentazione di AEM Forms su JEE o AEM Forms su OSGi.

## AEM 6.5, Service Pack 17 - 25 maggio 2023

* **Miglioramenti all’esperienza di ricerca**: è ora possibile eseguire rapidamente le seguenti operazioni sulle risorse visualizzate nei risultati di ricerca:
   * Crea un flusso di lavoro
   * Crea una versione
   * Correla o non correla risorse

  Per eseguire queste operazioni, non è necessario passare alla posizione della risorsa e visualizzarne le proprietà.
* **Dynamic Medie _Snapshot_**: prova le immagini di prova o gli URL di Dynamic Medie per visualizzare l&#39;output di diversi modificatori di immagini e le ottimizzazioni di Smart Imaging per le dimensioni del file (con distribuzione WebP e AVIF), la larghezza di banda di rete e le proporzioni pixel del dispositivo. Consulta [Dynamic Media Snapshot](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=it).
* **Streaming DASH con Dynamic Medie** - È stato avviato il supporto del nuovo protocollo (DASH - Dynamic Adaptive Streaming over HTTP) per lo streaming adattivo nella distribuzione di video Dynamic Medie (con CMAF abilitato). Disponibile ora per tutte le aree geografiche, [abilitato tramite un ticket di supporto](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Integrazione di Experience Manager Sites e frammenti di contenuto con Assets Dynamic Medie di nuova generazione** - Gli utenti di Experience Manager Assets as a Cloud Service Dynamic Medie di nuova generazione possono ora utilizzare tali risorse ospitate nel cloud per l&#39;authoring e la distribuzione con istanze locali o Managed Services di Experience Manager Sites 6.5.

### [!DNL Forms]

* **[Moduli adattivi nell’Editor pagina di AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: ora è possibile utilizzare l’Editor pagina di AEM per creare e aggiungere rapidamente più moduli alle pagine del sito. Questa funzionalità consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno delle pagine di Sites utilizzando la potenza dei componenti per moduli adattivi, tra cui il comportamento dinamico, le convalide, l’integrazione dei dati, la generazione di documenti di record e l’automazione dei processi aziendali. Operazioni disponibili:
   * Creare un modulo adattivo trascinando i componenti del modulo nel componente Contenitore di moduli adattivi nell’editor di AEM Sites o nei Frammenti di esperienza.
   * Utilizzare la procedura guidata per moduli adattivi nell’editor di AEM Sites per creare moduli indipendenti da qualsiasi pagina di Sites e poter riutilizzare tali moduli su più pagine.
   * Aggiungere più moduli a una pagina di Sites per semplificare l’esperienza utente e fornire maggiore flessibilità.
* **[Supporto di reCAPTCHA Enterprise in Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)**: è stato aggiunto il supporto per reCAPTCHA Enterprise in Experience Manager Forms, che fornisce una protezione avanzata contro attività fraudolente e spam, oltre al supporto di Google reCAPTCHA v2 esistente.
* **[Supporto per Adobe Acrobat Sign for Government con Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: AEM Forms è ora integrato con Adobe Acrobat Sign for Government (compatibile con FedRAMP). Questa integrazione fornisce un livello avanzato di conformità e sicurezza per le firme elettroniche con l’invio di moduli adattivi per gli account governativi associati (dipartimenti e agenzie governative). L’integrazione con Adobe Acrobat Sign per la Pubblica amministrazione consente ai partner e ai clienti del settore pubblico di Adobe di utilizzare le firme elettroniche in moduli adattivi per alcune delle linee di business più critiche e sensibili. Questo ulteriore livello di sicurezza garantisce che tutte le firme elettroniche siano pienamente conformi alla conformità FedRAMP Moderate, garantendo ai clienti del settore pubblico di Adobe la massima tranquillità.
* **Abilitare l&#39;integrazione di Salesforce con Experience Manager Forms per lo scambio di dati**: configurare l&#39;integrazione tra Experience Manager Forms e l&#39;applicazione Salesforce utilizzando il flusso di credenziali client OAuth 2.0. Questa funzionalità consente l&#39;autenticazione e l&#39;autorizzazione sicure e dirette dell&#39;applicazione e permette una comunicazione fluida senza il coinvolgimento dell&#39;utente.
* **Ottimizzazione e funzionalità migliorate del motore del flusso di lavoro**: aumenta le prestazioni dei motori del flusso di lavoro riducendo al minimo il numero di istanze del flusso di lavoro. Oltre ai valori di stato `COMPLETED` e `RUNNING`, il flusso di lavoro supporta anche tre nuovi valori di stato: `ABORTED`, `SUSPENDED` e `FAILED`.

## AEM 6.5, Service Pack 16 - 23 febbraio 2023

Il nuovo protocollo DASH (Dynamic Adaptive Streaming over HTTP) supporta lo streaming con bitrate adattivo avviato nella distribuzione di video Dynamic Medie (con CMAF [Common Media Application Format] abilitato).

* Lo streaming adattivo (DASH/HLS) garantisce una migliore esperienza di visualizzazione per i video per l’utente finale.
* DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore.
* Disponibile ora in Asia-Pacifico e Nord America (da attivare tramite un ticket di supporto); disponibile a breve in Europa-Medio Oriente-Africa.

Vedi [Abilita DASH sul tuo account](/help/assets/video.md#enable-dash).

### [!DNL Forms]

* [Forms adattivo headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it) consente agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui interagire tramite API, anziché tramite un&#39;interfaccia utente grafica tradizionale.

* [I componenti core adattivi di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) sono un set di 24 componenti open source conformi a BEM e basati sui componenti core di Adobe Experience Manager WCM. Questi componenti sono open source e consentono agli sviluppatori di personalizzarli ed estenderli facilmente in base alle esigenze specifiche dell’organizzazione. Chiunque disponga delle competenze necessarie per personalizzare [Componenti core WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html) può personalizzare e assegnare uno stile a tali componenti.

* Il servizio Reader Extension su OSGi ora fornisce opzioni separate per abilitare i diritti di utilizzo di importazione ed esportazione su un PDF per importare o esportare dati in Adobe Acrobat Reader.

## AEM 6.5, Service Pack 15 - 24 novembre 2022

### [!DNL Forms]

* AEM Forms Designer è ora disponibile nelle [impostazioni locali spagnole](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
* È ora possibile utilizzare [OAuth2 per l&#39;autenticazione con i protocolli del server di posta di Microsoft® Office 365 (SMTP e IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* È possibile impostare la proprietà [Riconvalida sul server](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=it#enabling-server-side-validation-br) su true per identificare i campi nascosti per l&#39;esclusione da un documento di record sul lato server.
* AEM Forms Designer richiede una versione a 32 bit di Visual C++ 2019 Redistributable (x86).

## AEM 6.5, Service Pack 14 - 25 agosto 2022

Solo correzioni di bug.

## AEM 6.5, Service Pack 13 - 26 maggio 2022

* Utilizzare il CAPTCHA invisibile in un modulo adattivo: ora puoi utilizzare un CAPTCHA invisibile per mostrare la richiesta CAPTCHA solo se viene rilevata un’attività sospetta. Se non viene trovata alcuna attività sospetta, la richiesta CAPTCHA non viene visualizzata. Consente di valutare il completamento manuale dei moduli senza bisogno di caselle di controllo, ridurre le operazioni di personalizzazione e migliorare l’esperienza dell’utente finale.

* È stato aggiunto il supporto per recuperare le intestazioni di risposta nel postprocessore del modello dati modulo per gli endpoint REST.

* Ora, quando si genera un file di traduzione di un modulo adattivo, la stessa sequenza di testi del file XLIFF generato è identica alla sequenza di componenti nel modulo adattivo corrispondente.

* Quando localizzi un modulo adattivo e apporti anche una piccola modifica al testo della lingua di base, la traduzione completa risulta mancante per tutte le altre lingue. Il problema è risolto in [!DNL Experience Manager] 6.5.13.0.

* Miglioramenti all’accessibilità per Forms:

   * È stato aggiunto il supporto per gli assistenti vocali per riconoscere l’intestazione e il corpo di una tabella come entità continue e connesse. Consente agli assistenti vocali di navigare correttamente nelle tabelle. (NPR-37139)
   * È stato aggiunto il supporto per gli assistenti vocali per interrompere la navigazione nell’area di lavoro di HTML fino all’apertura di una finestra di dialogo.

## AEM 6.5, Service Pack 12 - 24 febbraio 2022

* Dopo aver configurato una connessione tra le implementazioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell’implementazione di Sites. È ora possibile aggiornare, eliminare, ridenominare e spostare le risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites.
* È ora possibile eseguire il rollout push di un’origine Live Copy a più Live Copy per impostazione predefinita, senza richiedere una configurazione blueprint.
* Ora nell’interfaccia utente è visualizzato lo stato delle operazioni asincrone in corso per evitare che gli utenti attivino accidentalmente più operazioni asincrone sullo stesso percorso.
* Per le API di Analytics 2.0 è disponibile il supporto per l’autenticazione basata su IMS.
* Supporto API per frammento di esperienza di tipo offerta JSON.
* Ora viene fornita la richiesta di offerta per Elimina offerta (API Frammento di esperienza) in IMS.
* L’archivio incorporato (Apache Jackrabbit Oak) rimane ancora alla versione 1.22.9.
