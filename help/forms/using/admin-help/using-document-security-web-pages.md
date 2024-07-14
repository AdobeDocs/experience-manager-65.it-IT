---
title: Utilizzo delle pagine web di Document Security
description: Scopri come accedere, navigare e utilizzare le pagine web di document security.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# Utilizzo delle pagine web di Document Security {#using-the-document-security-webpages}

Utenti e amministratori utilizzano le pagine web relative alla sicurezza dei documenti per creare e gestire le policy, gestire i documenti protetti tramite policy e monitorare gli eventi associati ai documenti protetti tramite policy. Gli amministratori utilizzano inoltre le pagine web per creare set di criteri e designare i coordinatori dei set di criteri, configurare le impostazioni predefinite di Document Security, gestire la registrazione e gli account degli utenti invitati e monitorare e gestire eventi relativi a server, criteri, utenti e documenti.

>[!NOTE]
>
>Puoi accedere a document security anche tramite Acrobat e altre applicazioni client utilizzando il tuo account di accesso utente. (Vedi [Impostazione dell&#39;accesso alla sicurezza dei documenti dalle applicazioni client](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Per aprire le pagine web, devi disporre di un browser, dell’URL e delle informazioni di accesso per Document Security. L’URL per gli utenti è diverso da quello per gli amministratori.

Poiché la funzione di protezione dei documenti fa riferimento alle directory esistenti dell’organizzazione per le informazioni utente, le informazioni di accesso alla funzione di protezione dei documenti potrebbero essere le stesse utilizzate per accedere alla rete e ad altre applicazioni. Per informazioni sull&#39;account, rivolgersi all&#39;amministratore di sistema o all&#39;amministratore di sistema.

Per accedere come amministratore, devi disporre del ruolo di amministratore assegnato. È possibile utilizzare l&#39;account amministratore privilegiato predefinito creato durante il processo di installazione.

## Accedi alle pagine web {#log-in-to-the-web-pages}

Per accedere alle pagine web utilizzando un browser, devi disporre dell’URL di document security e di un account. L’URL per gli utenti è diverso da quello per gli amministratori. Gli amministratori possono anche accedere alle pagine utente per creare i criteri.

Se hai accesso a più installazioni di document security, devi disporre dell’URL dell’istanza di document security a cui desideri accedere. Se non disponi di queste informazioni, rivolgiti al tuo amministratore. L&#39;URL predefinito per le pagine utente è `https://[host]:[port]/edc`. In alcuni casi il numero di porta potrebbe non essere necessario. Per ulteriori informazioni, rivolgersi all&#39;amministratore.

L&#39;URL predefinito per gli amministratori è `https://[host]:[port]/adminui`.

Per gli amministratori, durante l&#39;installazione viene creato un account di amministratore privilegiato predefinito. È possibile utilizzare questo account per eseguire l’accesso alla prima installazione di Document Security.

>[!NOTE]
>
>Puoi anche accedere alle pagine web da Acrobat e da altre applicazioni client. Per ulteriori informazioni, consulta la Guida di Acrobat o la Guida delle estensioni di Acrobat Reader DC appropriate.

1. Digita l’URL nel browser:

   URL di Document Security: `https://[host]:[port]/edc`

   o URL console di amministrazione: `https://[host]:[port]/adminui`

1. Nella finestra di accesso, digitare il nome utente e la password e fare clic su OK.
1. In Administration Console, fai clic su Servizi > Document Security.

>[!NOTE]
>
>Quando si lavora con le pagine Web, evitare di utilizzare i pulsanti del browser, ad esempio il pulsante Indietro, il pulsante di aggiornamento e le frecce Indietro e Avanti perché questa azione può causare problemi indesiderati di acquisizione dei dati e visualizzazione dei dati.

## Navigazione nelle pagine web {#navigating-the-web-pages}

Quando accedi alle pagine web degli utenti, trovi i collegamenti alle pagine utente Criteri, Documenti ed Eventi.

Quando accedi alla console di amministrazione e apri la pagina principale di document security, potrebbero essere visualizzati uno o due collegamenti aggiuntivi, uno per la pagina Configurazione e uno per la pagina Utenti invitati e locali. La pagina Utenti invitati e utenti locali viene visualizzata solo se la registrazione degli utenti invitati è abilitata.

Utilizzare questi collegamenti per accedere alle varie pagine, in cui è possibile creare e gestire policy e documenti protetti tramite policy.

**Visualizza una pagina**

1. Fai clic sul nome della pagina, ad esempio Criteri.

**Torna alla pagina precedente**

1. Fai clic sul collegamento di navigazione nella parte superiore della pagina per la pagina a cui desideri tornare.

**Aggiorna l&#39;elenco dei dati in una pagina**

1. Nella pagina principale fare clic sul collegamento alla pagina che si desidera aggiornare.

>[!NOTE]
>
>Quando si lavora con le pagine Web, evitare di utilizzare i pulsanti del browser, ad esempio il pulsante Indietro, il pulsante di aggiornamento e le frecce Indietro e Avanti, in quanto questa azione può causare problemi indesiderati di acquisizione dei dati e visualizzazione dei dati.

## Impostazione dell’accesso alla sicurezza dei documenti dalle applicazioni client {#setting-up-access-to-document-security-from-client-applications}

Le applicazioni client devono essere configurate in modo da connettersi alla protezione dei documenti per proteggere i documenti, aprire i documenti protetti tramite policy e connettersi alle pagine web di Document Security. Per informazioni sulla configurazione della connessione nell&#39;applicazione client, vedere *Guida di Acrobat* o la *Guida di RightsManagementExtension* appropriata.

Document Security è accessibile tramite Secure Sockets Layer (SSL). Installa il certificato del sito web nel tuo archivio certificati in modo da poter accedere alla sicurezza dei documenti tramite le applicazioni client.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Queste istruzioni sono specifiche per Internet Explorer, ma è possibile installare il certificato utilizzando qualsiasi browser Web supportato. Per ulteriori informazioni, vedere la Guida del browser in uso.

**Installare il certificato del server utilizzando Internet Explorer**

1. Apri il browser web e digita l’URL di base per la sicurezza dei documenti nella casella Indirizzo. Digitare ad esempio `https://[host]:[port]`. Verrà visualizzata una finestra di dialogo Avviso di protezione.
1. Fare clic su Visualizza certificato, quindi su Installa certificato e selezionare le impostazioni predefinite per l&#39;installazione. Il certificato deve essere installato nelle Autorità di certificazione principali attendibili.
1. Chiudi la sessione del browser.
1. Aprire un&#39;altra finestra del browser e digitare lo stesso URL nella casella Indirizzo. La finestra di dialogo Avviso di protezione non dovrebbe essere visualizzata. Il test conferma che il certificato è installato correttamente.

## Esci dalle pagine web {#log-out-of-the-web-pages}

Esci al termine dell’utilizzo delle pagine web in modo da poter utilizzare il browser web per altri scopi in modo sicuro. A seconda della configurazione di document security, potrebbe essere necessario chiudere il browser per disconnettersi completamente.

1. Nell&#39;angolo superiore destro della pagina fare clic su Disconnetti.
1. Se nella pagina Disconnetti viene visualizzato un messaggio, chiudere la finestra del browser per disconnettersi completamente. In caso contrario, puoi continuare a utilizzare il browser per altri scopi.
