---
title: Soluzioni per la sicurezza dei documenti
seo-title: Document security offerings
description: Scopri vari strumenti e funzionalità di AEM Document Security
seo-description: Learn about various tools and features of AEM Document Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
source-git-commit: 18c180a491af10b41393ad841f2fa74d02ec9cd9
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Soluzioni per la sicurezza dei documenti{#document-security-offerings}

La protezione dei documenti Adobe Experience Manager Forms garantisce che solo gli utenti autorizzati possano utilizzare i documenti. Utilizzando la protezione dei documenti, è possibile distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. I formati di file supportati includono i file Adobe Portable Document Format (PDF) e Microsoft Word, Excel e PowerPoint.

È possibile proteggere i documenti utilizzando i criteri. Le impostazioni di riservatezza specificate in un criterio determinano in che modo un destinatario può utilizzare un documento a cui applicare il criterio. Ad esempio, è possibile specificare se i destinatari possono stampare o copiare testo, modificare testo o aggiungere firme e commenti ai documenti protetti.

I criteri sono memorizzati sul server di sicurezza dei documenti; i criteri vengono applicati ai documenti tramite l&#39;applicazione client. Quando si applica un criterio a un documento, le impostazioni di riservatezza specificate nel criterio proteggono le informazioni contenute nel documento. Puoi distribuire il documento protetto tramite criterio ai destinatari autorizzati dal criterio.

Il diagramma seguente illustra l’architettura tipica di AEM Forms Document Security:

![Sicurezza dei documenti - Architettura consigliata](do-not-localize/document_security_architecture.png)

## Client di sicurezza dei documenti {#document-security-clients}

Document Security fornisce diversi client per proteggere i documenti, visualizzare e modificare documenti protetti e indicizzatori per abilitare la ricerca full-text su documenti protetti. Puoi scegliere un client in base alle tue esigenze e funzionalità del cliente.

Document Security Server è il componente centrale attraverso il quale Document Security esegue transazioni quali l&#39;autenticazione degli utenti, la gestione in tempo reale dei criteri e l&#39;applicazione della riservatezza. Il server fornisce inoltre un archivio centrale per i criteri, i record di controllo e altre informazioni correlate.

Il server Document Security fornisce un&#39;interfaccia basata sul Web (pagina Web) per creare criteri, gestire documenti protetti da policy e monitorare gli eventi associati a documenti protetti da policy. Gli amministratori possono inoltre configurare opzioni globali quali l’autenticazione degli utenti, il controllo e la messaggistica per gli utenti invitati e gestire gli account utente invitati.

Il server è incluso nell’offerta dei componenti aggiuntivi AEM Forms Document Security. Puoi contattare AEM Forms [sales team](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) per acquistare il componente aggiuntivo Document Security.

### Documenti Protect {#protect-documents}

AEM Forms Document Security fornisce vari strumenti per applicare i criteri di sicurezza. Potete scegliere uno strumento in base alle vostre esigenze e specifiche.

![documenti-sicurezza-offerte](assets/document-security-offerings.png)

Puoi utilizzare l’SDK per la sicurezza dei documenti, Adobe Acrobat, l’estensione per la sicurezza dei documenti per Microsoft Office o la libreria di protezione mobile per applicare e tenere traccia dei criteri di sicurezza:

* **SDK per la sicurezza dei documenti:** L’SDK è un client ricco di funzioni. Puoi utilizzare l’SDK per la sicurezza dei documenti per accedere alle funzionalità del server dei documenti, aprire documenti protetti da policy e sviluppare estensioni personalizzate, plug-in o applicazioni. Ad esempio, puoi sviluppare estensioni per proteggere i formati di file personalizzati o integrare l’SDK con le soluzioni DLP (Data Loss Prevention). Le estensioni, le applicazioni e i plug-in sviluppati utilizzando Document Security SDK inviano documenti a specifici server AEM Forms e i criteri vengono applicati al server. Inoltre, AEM Forms document security client SDK (CSDK) non è in grado di rimuovere la protezione dei documenti protetti utilizzando la libreria di protezione portatile (PPL) e viceversa.

   L’SDK per la sicurezza dei documenti è disponibile sia per Java che per C++. L’SDK Java è incluso nell’offerta AEM Forms Document Security e viene installato nella distribuzione di moduli AEM su JEE. È possibile contattare [AEM team di supporto](https://helpx.adobe.com/it/marketing-cloud/contact-support.html) per l’elaborazione dell’SDK C++. L&#39;SDK C++ può essere compilato con Microsoft Visual Studio 2013. Puoi visitare [Documentazione API per la sicurezza dei documenti](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) per scoprire e utilizzare le funzioni dell’SDK.

* **Adobe Acrobat:** È possibile utilizzare Adobe Acrobat per applicare i criteri di sicurezza ai documenti PDF creati utilizzando le applicazioni desktop più diffuse, ad esempio Microsoft Office, i browser Web o qualsiasi applicazione che supporti la stampa in formato PDF.

   Puoi acquistare e scaricare Adobe Acrobat da [Sito Web Adobe](https://acrobat.adobe.com/us/en/free-trial-download.html). Articolo Adobe Acrobat [impostazione dei criteri di sicurezza per i PDF](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) fornisce informazioni dettagliate sulla creazione e l’applicazione dei criteri in Adobe Acrobat.

* **Estensione Document Security per Microsoft Office**: È possibile utilizzare l&#39;estensione Document Security per Microsoft Office per applicare criteri predefiniti ai file Microsoft Office dall&#39;interno dei programmi Microsoft Office. L&#39;estensione assicura che solo le persone autorizzate possano utilizzare file Microsoft Word, Excel e PowerPoint protetti da criteri. Solo gli utenti autorizzati che hanno installato il plug-in possono utilizzare i file protetti da policy.

   L’estensione Document Security è disponibile come plug-in di Microsoft Office. È possibile contattare [AEM team di supporto](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) per ottenere l&#39;estensione. Successivamente, puoi visitare [Estensione Document Security per Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) Informazioni sull&#39;installazione, la configurazione e l&#39;utilizzo dell&#39;estensione.

* **Libreria di protezione portatile:** La PPL (Portable Protection Library) protegge un documento localmente senza inviare il documento al server AEM Forms. Solo le credenziali di sicurezza e i dettagli delle politiche viaggiano sulla rete. PPL consente inoltre di limitare l’accesso al recupero dei criteri solo agli utenti connessi. È possibile recuperare i criteri con il contesto dell&#39;utente connesso AEM utente.

   Oltre a quanto sopra, la Libreria di protezione rettangolare dispone di tutte le funzioni dell’SDK per la sicurezza dei documenti. Puoi utilizzare l’SDK per la sicurezza dei documenti per accedere alle funzionalità del server dei documenti, aprire documenti protetti da policy e sviluppare estensioni personalizzate, plug-in o applicazioni. Inoltre, la libreria di protezione mobile (PPL) non può rimuovere la protezione dei documenti protetti utilizzando l’SDK (CSDK) del client di protezione dei documenti di AEM Forms e viceversa.

   La Portable Protection Library è disponibile per le lingue Java e C++ nelle versioni a 32 bit e a 64 bit. È disponibile anche come bundle OSGi per AEM Forms su OSGi. È possibile compilare il PPL C++ con Microsoft Visual Studio 2013. Se si dispone della licenza del componente aggiuntivo per la sicurezza dei documenti di AEM Forms, è possibile contattare [AEM Forms Document Security](https://helpx.adobe.com/marketing-cloud/contact-support.html) team di supporto per l&#39;elaborazione della libreria di protezione portatile. Successivamente, è possibile utilizzare la Guida della libreria di protezione portatile (inclusa nella libreria) per configurare e utilizzare la Libreria di protezione portatile.

### Visualizzare o modificare documenti protetti {#view-or-edit-protected-documents}

* Per **documenti PDF**, puoi utilizzare Adobe Acrobat DC, Acrobat Reader e Acrobat Reader Mobile per visualizzare documenti PDF protetti. La maggior parte degli utenti dispone già di Acrobat Reader installato sui propri dispositivi, pertanto non è necessario ottenere o apprendere software aggiuntivo per visualizzare i documenti protetti. Puoi anche scaricare Acrobat Reader da [Sito Web per il download di Acrobat Reader](https://get.adobe.com/reader/).

* Per **Documenti di Microsoft Office**, è necessaria l’estensione Microsoft Office e AEM Forms Document Security per Microsoft Office. L’estensione Document Security è disponibile come plug-in di Microsoft Office. Puoi scaricare l’estensione dal sito web Adobe.

### Documenti protetti dall&#39;indice {#index-protected-documents}

I motori di ricerca full-text di Microsoft Windows (SharePoint Index Server) e Adobe Experience Manager (AEM) possono eseguire ricerche full-text nei formati di documento comunemente utilizzati, ad esempio file di testo normale, documenti di Microsoft Office e documenti di PDF. È possibile utilizzare gli indici di sicurezza dei documenti per abilitare i motori di ricerca full-text alla ricerca di documenti PDF protetti:

* **Indicizzatore iFilter:** È possibile utilizzare l&#39;indicizzatore iFilter per indicizzare i documenti PDF protetti e abilitare i motori di ricerca full-text di Microsoft Windows (Desktop Indexing Service e SharePoint Indexserver) per cercare documenti PDF protetti. Per informazioni dettagliate, consulta [AEM SharePoint IFilter per documenti protetti](assets/sharepoint-ifilter-doc-security.pdf).

* **Indicizzatore sicurezza dei documenti AEM Forms:** È possibile utilizzare l’indicizzatore AEM Forms Document Security per indicizzare i documenti PDF protetti e consentire ad Adobe Experience Manager di cercare documenti PDF protetti. Gli indicizzatori fanno parte dell’offerta AEM Forms Document Security. Sono inclusi nei programmi di installazione di AEM Forms su JEE.
