---
title: Offerte sulla sicurezza dei documenti
description: Scopri i vari strumenti e le funzioni di AEM Document Security.
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# Offerte sulla sicurezza dei documenti{#document-security-offerings}

La funzione di protezione dei documenti di Adobe Experience Manager Forms garantisce che solo gli utenti autorizzati possano utilizzare i documenti. Grazie alla protezione dei documenti è possibile distribuire in modo sicuro le informazioni salvate in un formato supportato. I formati di file supportati sono Adobe Portable Document Format (PDF) e i file Microsoft® Word, Excel e PowerPoint.

È possibile proteggere i documenti utilizzando le policy. Le impostazioni di riservatezza specificate in una policy determinano il modo in cui un destinatario può utilizzare un documento al quale si applica la policy. È ad esempio possibile specificare se i destinatari possono stampare o copiare testo, modificare testo o aggiungere firme e commenti ai documenti protetti.

Le policy vengono memorizzate nel server di Document Security e applicate ai documenti tramite l’applicazione client. Quando si applica una policy a un documento, le impostazioni di riservatezza specificate nella policy proteggono le informazioni contenute nel documento. Puoi distribuire il documento protetto tramite policy ai destinatari autorizzati dalla policy.

Il diagramma seguente mostra l’architettura tipica di AEM Forms Document Security:

![Sicurezza dei documenti - Architettura consigliata](do-not-localize/document_security_architecture.png)

## Client Document Security {#document-security-clients}

Document Security offre a diversi client la protezione dei documenti, la visualizzazione e la modifica di documenti protetti e indicizzatori per consentire la ricerca full-text nei documenti protetti. Puoi scegliere un cliente in base ai tuoi requisiti e alle funzionalità del cliente.

Document Security Server è il componente centrale tramite il quale Document Security esegue transazioni quali l’autenticazione degli utenti, la gestione in tempo reale di policy e l’applicazione di criteri di riservatezza. Il server fornisce inoltre un repository centrale per le regole, i record di controllo e altre informazioni correlate.

Il server di Document Security fornisce un’interfaccia basata su web (pagina web) per creare policy, gestire documenti protetti tramite policy e monitorare gli eventi associati ai documenti protetti tramite policy. Gli amministratori possono anche configurare opzioni globali quali l’autenticazione degli utenti, il controllo e la messaggistica per gli utenti invitati e gestire gli account utente invitati.

Il server è incluso nell’offerta del componente aggiuntivo AEM Forms Document Security. Per acquistare il componente aggiuntivo Document Security, contatta il [team di vendita](https://business.adobe.com/request-consultation/experience-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) di AEM Forms.

### Documenti Protect {#protect-documents}

AEM Forms Document Security fornisce diversi strumenti per applicare i criteri di sicurezza. Puoi scegliere uno strumento in base alle tue esigenze e specifiche.

![offerte di protezione dei documenti](assets/document-security-offerings.png)

È possibile utilizzare Document Security SDK, Adobe Acrobat, Document Security Extension for Microsoft® Office o Portable Protection Library per applicare e tenere traccia delle policy di sicurezza:

* **Document Security SDK:** l&#39;SDK è un client ricco di funzionalità. Document Security SDK consente di accedere alle funzionalità del server documenti, aprire documenti protetti tramite policy e sviluppare estensioni, plug-in o applicazioni personalizzate. Ad esempio, puoi sviluppare estensioni per proteggere i formati di file personalizzati o integrare l’SDK con le soluzioni DLP (Data Loss Prevention). Estensioni, applicazioni e plug-in sviluppati utilizzando Document Security SDK per inviare documenti al server AEM Forms designato e le policy vengono applicate al server. Il CSDK (Document Security Client SDK) di AEM Forms non è in grado di rimuovere la protezione dei documenti protetti utilizzando la Portable Protection Library (PPL) e viceversa.

  Document Security SDK è disponibile sia per Java™ che per C++. Java™ SDK è incluso nell’offerta AEM Forms Document Security e viene installato nella distribuzione di moduli AEM su JEE. Contatta l&#39;[Assistenza clienti AEM](https://experienceleague.adobe.com/it?support-solution=General&amp;support-tab=homehome?lang=it#support) per ottenere l&#39;SDK C++. L&#39;SDK C++ può essere compilato con Microsoft® Visual Studio 2013. Visita il sito [Documentazione API di Document Security](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) dove puoi imparare e utilizzare le funzioni dell’SDK.

* **Adobe Acrobat:** è possibile utilizzare Adobe Acrobat per applicare i criteri di sicurezza ai documenti PDF creati utilizzando le applicazioni desktop più diffuse, ad esempio Microsoft® Office, browser Web o qualsiasi applicazione che supporti la stampa in formato PDF.

  Puoi acquistare e scaricare Adobe Acrobat dal [sito Web Adobe](https://www.adobe.com/acrobat/free-trial-download.html). L&#39;articolo di Adobe Acrobat [impostazione dei criteri di sicurezza per PDF](https://helpx.adobe.com/it/acrobat/using/setting-security-policies-pdfs.html) fornisce informazioni dettagliate sulla creazione e l&#39;applicazione dei criteri in Adobe Acrobat.

* **Document Security Extension for Microsoft® Office**: è possibile utilizzare Document Security Extension for Microsoft® Office per applicare policy predefinite ai file di Microsoft® Office direttamente dalle applicazioni di Microsoft® Office. L’estensione garantisce che solo gli utenti autorizzati possano utilizzare file Microsoft® Word, Excel e PowerPoint protetti tramite policy. Solo gli utenti autorizzati che dispongono del plug-in possono utilizzare i file protetti tramite policy.

  L’estensione Document Security è disponibile come plug-in di Microsoft® Office. Contatta l&#39;Assistenza clienti [AEM](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) per ottenere l&#39;estensione. In seguito, puoi visitare la guida di [Document Security Extension for Microsoft® Office](https://experienceleague.adobe.com/docs/experience-manager-document-security/using/download-installer.html?lang=it) per informazioni sull’installazione, la configurazione e l’utilizzo dell’estensione.

* **Libreria di protezione portatile:** PPL protegge un documento localmente, senza inviarlo al server AEM Forms. Solo le credenziali di protezione e i dettagli dei criteri possono essere utilizzati in rete. PPL consente inoltre di limitare l’accesso al recupero dei criteri solo agli utenti connessi. Puoi recuperare i criteri con il contesto dell’utente connesso all’utente AEM.

  Oltre a quanto sopra, il PPL offre tutte le funzioni dell’SDK di Document Security. Document Security SDK consente di accedere alle funzionalità del server documenti, aprire documenti protetti tramite policy e sviluppare estensioni, plug-in o applicazioni personalizzate. Il PPL non può rimuovere la protezione dei documenti protetti utilizzando AEM Forms document security client SDK (CSDK) e viceversa.

  Il PPL è disponibile per i linguaggi Java™ e C++ nelle versioni a 32 bit e a 64 bit. È disponibile anche come bundle OSGi per AEM Forms su OSGi. Il file PPL C++ può essere compilato con Microsoft® Visual Studio 2013. Se hai concesso in licenza il componente aggiuntivo AEM Forms Document Security, puoi contattare il team di supporto di [AEM Forms Document Security](https://experienceleague.adobe.com/it?support-solution=General&amp;support-tab=homehome?lang=it#support) per ottenere il PPL. In seguito, è possibile utilizzare la Guida PPL (fornita in dotazione con la libreria) per impostare e utilizzare la PPL.

### Visualizzare o modificare documenti protetti {#view-or-edit-protected-documents}

* Per **documenti PDF**, è possibile utilizzare Adobe Acrobat DC, Acrobat Reader e Acrobat Reader Mobile per visualizzare documenti PDF protetti. La maggior parte degli utenti dispone già di Acrobat Reader installato sui propri dispositivi, pertanto non è necessario ottenere o apprendere software aggiuntivo per visualizzare i documenti protetti. È inoltre possibile scaricare Acrobat Reader dal [sito Web di download di Acrobat Reader](https://get.adobe.com/reader/).

* Per i **documenti di Microsoft® Office**, è necessario Microsoft® Office e AEM Forms Document Security Extension for Microsoft® Office. L’estensione Document Security è disponibile come plug-in di Microsoft® Office. Puoi scaricare l’estensione dal sito web dell’Adobe.

### Indice documenti protetti {#index-protected-documents}

I motori di ricerca full-text di Microsoft® Windows (server indice di SharePoint) e Adobe Experience Manager (AEM) possono eseguire ricerche full-text su formati di documenti di uso comune, come file di testo normale, documenti di Microsoft® Office e PDF. È possibile utilizzare gli indicizzatori di Document Security per abilitare i motori di ricerca full-text nella ricerca di documenti PDF protetti:

* **Indicizzatore iFilter:** È possibile utilizzare l&#39;indicizzatore iFilter per indicizzare i documenti protetti di PDF e abilitare i motori di ricerca full-text di Microsoft® Windows (servizio di indicizzazione desktop e server indice SharePoint) per eseguire ricerche nei documenti protetti di PDF. Per informazioni dettagliate, vedere [AEM SharePoint IFilter per documenti protetti](assets/sharepoint-ifilter-doc-security.pdf).

* **Indicizzatore di AEM Forms Document Security:** È possibile utilizzare l&#39;indicizzatore di AEM Forms Document Security per indicizzare i documenti protetti di PDF e consentire a Adobe Experience Manager di effettuare ricerche nei documenti protetti di PDF. Gli indicizzatori fanno parte dell’offerta AEM Forms Document Security. Sono inclusi nei programmi di installazione di AEM Forms su JEE.
