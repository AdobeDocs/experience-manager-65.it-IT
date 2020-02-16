---
title: Offerte sulla protezione dei documenti
seo-title: Offerte sulla protezione dei documenti
description: Scopri i diversi strumenti e funzionalità di AEM Document Security
seo-description: Scopri i diversi strumenti e funzionalità di AEM Document Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Offerte sulla protezione dei documenti{#document-security-offerings}

La protezione dei documenti Adobe Experience Manager Forms garantisce che i documenti vengano utilizzati solo dagli utenti autorizzati. La protezione dei documenti consente di distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. I formati di file supportati includono file Adobe PDF (Portable Document Format) e Microsoft Word, Excel e PowerPoint.

È possibile proteggere i documenti utilizzando i criteri. Le impostazioni di riservatezza specificate in un criterio determinano in che modo il destinatario può utilizzare il documento a cui si applica il criterio. Ad esempio, è possibile specificare se i destinatari possono stampare o copiare il testo, modificare il testo o aggiungere firme e commenti ai documenti protetti.

I criteri sono memorizzati in Document Security Server; i criteri vengono applicati ai documenti tramite l&#39;applicazione client. Quando applicate un criterio a un documento, le impostazioni di riservatezza specificate nel criterio proteggono le informazioni contenute nel documento. Potete distribuire il documento protetto tramite criterio ai destinatari autorizzati dal criterio.

Il diagramma seguente mostra l&#39;architettura tipica di AEM Forms Document Security:

![Document Security - Architettura consigliata](do-not-localize/document_security_architecture.png)

## Client Document Security {#document-security-clients}

Document Security offre a diversi client la possibilità di proteggere i documenti, visualizzare e modificare documenti protetti e indicizzatori per consentire la ricerca full-text sui documenti protetti. Potete scegliere un client in base alle vostre esigenze e capacità.

Document Security Server è il componente centrale tramite il quale Document Security esegue transazioni quali l&#39;autenticazione degli utenti, la gestione in tempo reale dei criteri e l&#39;applicazione della riservatezza. Il server fornisce inoltre un archivio centrale per criteri, record di controllo e altre informazioni correlate.

Il server Document Security offre un&#39;interfaccia basata sul Web (pagina Web) per creare criteri, gestire documenti protetti tramite criterio e monitorare gli eventi associati ai documenti protetti tramite criterio. Gli amministratori possono inoltre configurare opzioni globali quali l&#39;autenticazione degli utenti, il controllo e la messaggistica per gli utenti invitati e gestire gli account utente invitati.

Il server è incluso nell&#39;offerta del componente aggiuntivo AEM Forms Document Security. Potete contattare il team [di](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG) vendita di AEM Forms per acquistare il componente aggiuntivo Document Security.

### Proteggere i documenti {#protect-documents}

AEM Forms Document Security offre diversi strumenti per l&#39;applicazione dei criteri di protezione. Potete scegliere uno strumento in base alle vostre esigenze e specifiche.

![documenti-sicurezza-offerte](assets/document-security-offerings.png)

Potete utilizzare l&#39;SDK di Document Security, Adobe Acrobat, Document Security Extension for Microsoft Office o la libreria Protezione portatile per applicare e tenere traccia dei criteri di protezione:

* **** SDK di Document Security: L’SDK è un client ricco di funzioni. Document Security SDK può essere utilizzato per accedere alle funzionalità del server documenti, aprire documenti protetti tramite criterio e sviluppare estensioni, plug-in o applicazioni personalizzate. Ad esempio, puoi sviluppare estensioni per proteggere i formati di file personalizzati o integrare SDK con soluzioni DLP (Data Loss Prevention). Estensioni, applicazioni e plug-in sviluppati con Document Security SDK inviano documenti a un server AEM Forms designato e i criteri vengono applicati al server. Inoltre, l’SDK per client per la protezione dei documenti di AEM Forms (CSDK) non è in grado di rimuovere la protezione dei documenti protetti utilizzando la libreria di protezione mobile (PPL) e viceversa.

   Document Security SDK è disponibile sia per Java che per C++. L’SDK Java è incluso nell’offerta AEM Forms Document Security e viene installato nella distribuzione di moduli AEM su JEE. Puoi contattare il team [di supporto di](https://helpx.adobe.com/marketing-cloud/contact-support.html) AEM per acquisire l’SDK C++. L&#39;SDK C++ può essere compilato con Microsoft Visual Studio 2013. Potete visitare il sito della documentazione [API di](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) Document Security per apprendere e usare le funzioni dell&#39;SDK.

* **** Adobe Acrobat: È possibile utilizzare Adobe Acrobat per applicare criteri di protezione ai documenti PDF creati utilizzando le più comuni applicazioni desktop, come Microsoft Office, browser Web o qualsiasi applicazione che supporti la stampa in formato PDF.

   Potete acquistare e scaricare Adobe Acrobat dal sito Web di [Adobe](https://acrobat.adobe.com/us/en/free-trial-download.html). L&#39;articolo di Adobe Acrobat [che configura criteri di protezione per i PDF](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) fornisce informazioni dettagliate sulla creazione e l&#39;applicazione dei criteri in Adobe Acrobat.

* **Document Security Extension for Microsoft Office**: Potete utilizzare Document Security Extension for Microsoft Office per applicare criteri predefiniti ai file di Microsoft Office direttamente dalle applicazioni di Microsoft Office. L&#39;estensione assicura che solo gli utenti autorizzati possano utilizzare i file Microsoft Word, Excel e PowerPoint protetti tramite criterio. Solo gli utenti autorizzati che hanno installato il plug-in possono utilizzare i file protetti tramite criterio.

   L&#39;estensione Document Security è disponibile come plug-in di Microsoft Office. Puoi contattare il team [di supporto di](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) AEM per ottenere l’estensione. Successivamente, potrete consultare la guida di [Document Security Extension for Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/aem-document-security-extension-help.html) per informazioni sull&#39;installazione, la configurazione e l&#39;utilizzo dell&#39;estensione.

* **** Libreria di protezione portatile: La Portable Protection Library (PPL) protegge un documento localmente senza inviarlo al server AEM Forms. Solo le credenziali di sicurezza e i dettagli dei criteri viaggano sulla rete. PPL consente inoltre di limitare l&#39;accesso al recupero dei criteri solo agli utenti connessi. Potete recuperare i criteri con il contesto dell&#39;utente che ha eseguito l&#39;accesso all&#39;utente AEM.

   Oltre a quanto sopra, la Libreria protezione rettangolare offre tutte le funzioni di Document Security SDK. Document Security SDK può essere utilizzato per accedere alle funzionalità del server documenti, aprire documenti protetti tramite criterio e sviluppare estensioni, plug-in o applicazioni personalizzate. Inoltre, la libreria di protezione portatile (PPL) non è in grado di rimuovere la protezione dei documenti protetti tramite l’SDK (Document Security Client SDK) di AEM Forms e viceversa.

   La Portable Protection Library è disponibile per le lingue Java e C++ nelle versioni a 32 bit e a 64 bit. È inoltre disponibile come bundle OSGi per AEM Forms su OSGi. È possibile compilare il PPL C++ con Microsoft Visual Studio 2013. Se si dispone della licenza per il componente aggiuntivo AEM Forms Document Security, è possibile contattare il team di supporto di [AEM Forms Document Security](https://helpx.adobe.com/marketing-cloud/contact-support.html) per acquistare la libreria Protezione portatile. Successivamente, sarà possibile utilizzare la Guida della libreria Protezione portatile (fornita con la libreria) per configurare e utilizzare la libreria Protezione portatile.

### Visualizzare o modificare documenti protetti {#view-or-edit-protected-documents}

* Per i documenti **** PDF, è possibile utilizzare Adobe Acrobat DC, Acrobat Reader e Acrobat Reader Mobile per visualizzare i documenti PDF protetti. Poiché la maggior parte degli utenti dispone già di Acrobat Reader sui propri dispositivi, non è necessario procurarsi software aggiuntivo per visualizzare i documenti protetti. È inoltre possibile scaricare Acrobat Reader dal sito [Web di download di](https://get.adobe.com/reader/)Acrobat Reader.

* Per i documenti **di** Microsoft Office, è necessario Microsoft Office e AEM Forms Document Security extension per Microsoft Office. L&#39;estensione Document Security è disponibile come plug-in di Microsoft Office. Potete scaricare l’estensione dal sito Web di Adobe.

### Documenti protetti dall&#39;indice {#index-protected-documents}

I motori di ricerca full-text di Microsoft Windows (SharePoint Index Server) e Adobe Experience Manager (AEM) possono eseguire ricerche full-text nei formati di documento comunemente utilizzati, come file di testo normale, documenti di Microsoft Office e documenti PDF. Potete utilizzare gli indici di Document Security per consentire ai motori di ricerca full-text di effettuare ricerche nei documenti PDF protetti:

* **** Indicatore iFilter: È possibile utilizzare l&#39;indicizzatore iFilter per indicizzare i documenti PDF protetti e abilitare i motori di ricerca full-text di Microsoft Windows (Desktop Indexing Service e SharePoint Indexserver) per eseguire ricerche nei documenti PDF protetti. Per informazioni dettagliate, consultate [AEM SharePoint IFilter per documenti](assets/sharepoint-ifilter-doc-security.pdf)protetti.

* **** AEM Forms Document Security Indexer: È possibile utilizzare l&#39;indicizzatore AEM Forms Document Security per indicizzare i documenti PDF protetti e consentire ad Adobe Experience Manager di effettuare ricerche nei documenti PDF protetti. Gli indici fanno parte dell&#39;offerta AEM Forms Document Security. Sono inclusi nei programmi di installazione AEM Forms su JEE.

