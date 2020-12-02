---
title: Utilizzo delle pagine Web sulla protezione dei documenti
seo-title: Utilizzo delle pagine Web sulla protezione dei documenti
description: Scoprite come accedere, navigare e utilizzare le pagine Web sulla protezione dei documenti.
seo-description: Scoprite come accedere, navigare e utilizzare le pagine Web sulla protezione dei documenti.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---


# Utilizzo delle pagine Web di protezione del documento {#using-the-document-security-webpages}

Utenti e amministratori utilizzano le pagine Web sulla protezione dei documenti per creare e gestire i criteri, gestire i documenti protetti tramite criterio e monitorare gli eventi associati ai documenti protetti tramite criterio. Gli amministratori possono inoltre utilizzare le pagine Web per creare set di criteri e designare coordinatori di set di criteri, configurare le impostazioni predefinite per la protezione dei documenti, gestire la registrazione e gli account degli utenti invitati e monitorare e gestire eventi relativi a server, criteri, utenti e documenti.

>[!NOTE]
>
>È inoltre possibile accedere alla protezione dei documenti tramite  Acrobat e altre applicazioni client utilizzando l&#39;account di accesso utente. (Vedere [Impostazione dell&#39;accesso alla protezione dei documenti dalle applicazioni client](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Per aprire le pagine Web, è necessario un browser e l&#39;URL e le informazioni di login per la protezione del documento. L’URL per gli utenti è diverso dall’URL per gli amministratori.

Poiché Document Security fa riferimento alle directory esistenti dell&#39;azienda per ottenere informazioni sugli utenti, le informazioni di accesso a Document Security possono essere le stesse informazioni utilizzate per accedere alla rete e ad altre applicazioni. Consultate l’amministratore di sistema o l’amministratore per informazioni sull’account.

Per effettuare l’accesso come amministratore, dovete avere il ruolo di amministratore assegnato a voi. Potete utilizzare l&#39;account super amministratore predefinito creato durante il processo di installazione.

## Accedere alle pagine Web {#log-in-to-the-web-pages}

Per accedere alle pagine Web utilizzando un browser, è necessario disporre dell&#39;URL di protezione del documento e di un account. L’URL per gli utenti è diverso dall’URL per gli amministratori. Gli amministratori possono inoltre accedere alle pagine utente per creare i criteri.

Se si dispone dell&#39;accesso a più installazioni di Document Security, è necessario l&#39;URL per l&#39;istanza di Document Security a cui si desidera accedere. Se non disponete di tali informazioni, rivolgetevi all’amministratore. L&#39;URL predefinito per le pagine utente è `https://[host]:[port]/edc`. In alcuni casi il numero di porta potrebbe non essere richiesto. Per ulteriori informazioni, rivolgetevi all’amministratore.

L&#39;URL predefinito per gli amministratori è `https://[host]:[port]/adminui`.

Per gli amministratori, durante l&#39;installazione viene creato un account super amministratore predefinito. È possibile utilizzare questo account per accedere al momento della prima installazione di Document Security.

>[!NOTE]
>
>Potete inoltre accedere alle pagine Web da  Acrobat e da altre applicazioni client. Per ulteriori informazioni, consultate  Guida di Acrobat o la relativa Guida alle estensioni Acrobat Reader DC.

1. Digitate l’URL nel browser:

   URL protezione documento: `https://[host]:[port]/edc`

   o URL console di amministrazione: `https://[host]:[port]/adminui`

1. Nella finestra di accesso, digitate il nome utente e la password e fate clic su OK.
1. In Admin Console, fai clic su Servizi > Protezione documento.

>[!NOTE]
>
>Quando lavorate con le pagine Web, evitate di utilizzare i pulsanti del browser, come il pulsante Indietro, il pulsante Aggiorna e le frecce indietro e avanti, perché questa azione può causare problemi indesiderati di acquisizione dei dati e visualizzazione dei dati.

## Navigazione nelle pagine Web {#navigating-the-web-pages}

Quando si accede alle pagine Web dell&#39;utente, vengono visualizzati i collegamenti alle pagine utente Criteri, Documenti ed Eventi.

Quando si accede alla console di amministrazione e si passa alla pagina principale di protezione del documento, è possibile che vengano visualizzati anche uno o due collegamenti aggiuntivi, uno per la pagina Configurazione e uno per la pagina Utenti invitati e locali. La pagina Utenti invitati e Utenti locali viene visualizzata solo se è abilitata la registrazione degli utenti invitati.

Utilizzate questi collegamenti per accedere alle varie pagine, in cui potete creare e gestire criteri e documenti protetti tramite criterio.

**Visualizzare una pagina**

1. Fate clic sul nome della pagina; ad esempio fare clic su Criteri.

**Torna alla pagina precedente**

1. Fate clic sul collegamento di navigazione nella parte superiore della pagina per la quale desiderate tornare.

**Aggiornare l’elenco dei dati in una pagina**

1. Nella pagina principale, fare clic sul collegamento alla pagina da aggiornare.

>[!NOTE]
>
>Quando lavorate con le pagine Web, evitate di utilizzare i pulsanti del browser, come il pulsante Indietro, il pulsante Aggiorna e le frecce indietro e avanti, perché questa azione può causare problemi indesiderati di acquisizione dei dati e visualizzazione dei dati.

## Impostazione dell&#39;accesso alla protezione dei documenti dalle applicazioni client {#setting-up-access-to-document-security-from-client-applications}

Le applicazioni client devono essere configurate per connettersi alla protezione dei documenti al fine di proteggere i documenti, aprire documenti protetti tramite criterio e connettersi alle pagine Web della protezione dei documenti. Per informazioni sulla configurazione della connessione all&#39;interno dell&#39;applicazione client, vedere *Guida di Acrobat* o la *Guida di RightsManagementExtension* appropriata.

La protezione del documento è accessibile tramite SSL (Secure Sockets Layer). È necessario installare il certificato del sito Web nell&#39;archivio certificati per poter accedere alla protezione dei documenti tramite le applicazioni client.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Queste istruzioni sono specifiche per Internet Explorer, ma è possibile installare il certificato utilizzando qualsiasi browser Web supportato. Per ulteriori informazioni, consultate la guida del browser in uso.

**Installare il certificato del server utilizzando Internet Explorer**

1. Aprite il browser Web e digitate l&#39;URL di base per la protezione del documento nella casella Indirizzo. Ad esempio, digitare `https://[host]:[port]`. Viene visualizzata una finestra di dialogo di avviso sulla protezione.
1. Fate clic su Visualizza certificato, quindi su Installa certificato e selezionate i valori predefiniti per l&#39;installazione. Il certificato deve essere installato nelle Autorità di certificazione radice attendibili.
1. Chiudete la sessione del browser.
1. Aprite un&#39;altra finestra del browser e digitate lo stesso URL nella casella Indirizzo. Non dovrebbe essere visualizzata una finestra di avviso sulla protezione. Questo test conferma che il certificato è installato correttamente.

## Disconnettersi dalle pagine Web {#log-out-of-the-web-pages}

Disconnettetevi al termine dell’utilizzo delle pagine Web per poter utilizzare in modo sicuro il browser Web per altri scopi. A seconda della configurazione della protezione del documento, potrebbe essere necessario chiudere il browser per disconnettersi completamente.

1. Nell’angolo superiore destro della pagina, fate clic su Logout.
1. Se nella pagina Logout viene visualizzato un messaggio, chiudete la finestra del browser per disconnettersi completamente. In caso contrario, potete utilizzare il browser per altri scopi.

