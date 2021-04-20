---
title: Utilizzo delle pagine web sulla sicurezza dei documenti
seo-title: Utilizzo delle pagine web sulla sicurezza dei documenti
description: Scopri come accedere, navigare e utilizzare le pagine web sulla sicurezza dei documenti.
seo-description: Scopri come accedere, navigare e utilizzare le pagine web sulla sicurezza dei documenti.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Utilizzo delle pagine Web relative alla protezione dei documenti {#using-the-document-security-webpages}

Gli utenti e gli amministratori utilizzano le pagine web sulla sicurezza dei documenti per creare e gestire i criteri, gestire i documenti protetti da policy e monitorare gli eventi associati ai documenti protetti da policy. Gli amministratori utilizzano inoltre le pagine web per creare set di criteri e designare i coordinatori dei set di criteri, configurare le impostazioni predefinite per la protezione dei documenti, gestire la registrazione e gli account degli utenti invitati e monitorare e gestire gli eventi relativi a server, criteri, utenti e documenti.

>[!NOTE]
>
>Puoi anche accedere alla sicurezza dei documenti tramite Acrobat e altre applicazioni client utilizzando il tuo account di accesso utente. (Vedere [Impostazione dell&#39;accesso alla protezione dei documenti dalle applicazioni client](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Per aprire le pagine web, è necessario un browser e l’URL e le informazioni di accesso per la sicurezza dei documenti. L’URL per gli utenti è diverso dall’URL per gli amministratori.

Poiché la protezione dei documenti fa riferimento alle directory esistenti dell&#39;organizzazione per le informazioni utente, le informazioni di accesso alla protezione dei documenti possono essere le stesse informazioni utilizzate per accedere alla rete e ad altre applicazioni. Per informazioni sull&#39;account, rivolgiti all&#39;amministratore di sistema o all&#39;amministratore di sistema.

Per accedere come amministratore, devi assegnare il ruolo di amministratore. È possibile utilizzare l&#39;account super amministratore predefinito creato durante il processo di installazione.

## Accedi alle pagine web {#log-in-to-the-web-pages}

Per accedere alle pagine web utilizzando un browser, è necessario disporre dell’URL di protezione del documento e di un account. L’URL per gli utenti è diverso dall’URL per gli amministratori. Gli amministratori possono inoltre accedere alle pagine utente per creare i criteri.

Se si dispone dell&#39;accesso a più installazioni di sicurezza dei documenti, è necessario l&#39;URL per l&#39;istanza di protezione dei documenti a cui si desidera accedere. Se non disponi di queste informazioni, rivolgiti all’amministratore. L’URL predefinito per le pagine utente è `https://[host]:[port]/edc`. In alcuni casi il numero di porta potrebbe non essere necessario. Per ulteriori informazioni, rivolgiti all’amministratore.

L’URL predefinito per gli amministratori è `https://[host]:[port]/adminui`.

Per gli amministratori, durante l&#39;installazione viene creato un account super amministratore predefinito. È possibile utilizzare questo account per accedere quando si installa per la prima volta la sicurezza dei documenti.

>[!NOTE]
>
>Puoi anche accedere alle pagine web da Acrobat e da altre applicazioni client. Per ulteriori informazioni, consulta la Guida di Acrobat o la Guida delle estensioni Acrobat Reader DC appropriata.

1. Digita l’URL nel browser:

   URL di protezione del documento: `https://[host]:[port]/edc`

   o URL della console di amministrazione: `https://[host]:[port]/adminui`

1. Nella finestra di accesso, digitare il nome utente e la password e fare clic su OK.
1. In Console di amministrazione, fai clic su Servizi > Protezione dei documenti.

>[!NOTE]
>
>Quando lavori con le pagine web, evita di utilizzare i pulsanti del browser, ad esempio il pulsante Indietro, il pulsante di aggiornamento e le frecce indietro e avanti, perché questa azione può causare problemi indesiderati di acquisizione dei dati e visualizzazione dei dati.

## Navigazione nelle pagine web {#navigating-the-web-pages}

Quando si accede alle pagine web dell&#39;utente, vengono visualizzati i collegamenti alle pagine utente Criteri, Documenti ed Eventi.

Quando si accede alla console di amministrazione e si passa alla pagina principale di sicurezza del documento, è possibile che vengano visualizzati anche uno o due collegamenti aggiuntivi, uno per la pagina Configurazione e uno per la pagina Utenti invitati e locali. La pagina Utenti invitati e locali viene visualizzata solo se è abilitata la registrazione utente invitati.

Utilizzare questi collegamenti per accedere alle varie pagine, in cui è possibile creare e gestire criteri e documenti protetti da policy.

**Visualizzare una pagina**

1. Fare clic sul nome della pagina; ad esempio fare clic su Criteri.

**Torna alla pagina precedente**

1. Fai clic sul collegamento di navigazione nella parte superiore della pagina per la pagina a cui desideri tornare.

**Aggiornare l’elenco di dati in una pagina**

1. Nella pagina principale, fai clic sul collegamento alla pagina da aggiornare.

>[!NOTE]
>
>Quando lavori con le pagine web, evita di utilizzare i pulsanti del browser, come il pulsante Indietro, il pulsante di aggiornamento e le frecce indietro e avanti, perché questa azione può causare problemi indesiderati di acquisizione dati e visualizzazione dei dati.

## Impostazione dell&#39;accesso alla protezione dei documenti dalle applicazioni client {#setting-up-access-to-document-security-from-client-applications}

Le applicazioni client devono essere configurate per connettersi alla protezione dei documenti per proteggere i documenti, aprire documenti protetti da policy e connettersi alle pagine Web di protezione dei documenti. Per informazioni sulla configurazione della connessione all&#39;interno dell&#39;applicazione client, consulta la *Guida di Acrobat* o la *Guida di RightsManagementExtension* appropriata.

La sicurezza dei documenti è accessibile tramite Secure Sockets Layer (SSL). È necessario installare il certificato del sito Web nell’archivio certificati in modo da poter accedere alla protezione dei documenti tramite le applicazioni client.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Queste istruzioni sono specifiche di Internet Explorer, ma è possibile installare il certificato utilizzando qualsiasi browser Web supportato. Per ulteriori informazioni, consulta la Guida del browser in uso.

**Installare il certificato del server utilizzando Internet Explorer**

1. Aprire il browser Web e digitare l&#39;URL di base per la protezione del documento nella casella Indirizzo. Ad esempio, digitare `https://[host]:[port]`. Viene visualizzata una finestra di dialogo di avviso sulla sicurezza.
1. Fare clic su Visualizza certificato, quindi su Installa certificato e selezionare i valori predefiniti per l’installazione. Il certificato deve essere installato nelle Autorità di certificazione radice attendibili.
1. Chiudi la sessione del browser.
1. Aprire un&#39;altra finestra del browser e digitare lo stesso URL nella casella Indirizzo. Non dovrebbe essere visualizzata una finestra di dialogo di avviso sulla sicurezza. Questo test conferma che il certificato è installato correttamente.

## Esci dalle pagine web {#log-out-of-the-web-pages}

Disconnettiti quando hai finito di utilizzare le pagine web in modo da poter utilizzare il browser in modo sicuro per altri scopi. A seconda della configurazione della protezione dei documenti, potrebbe essere necessario chiudere il browser per disconnettersi completamente.

1. Nell’angolo in alto a destra della pagina, fai clic su Logout.
1. Se nella pagina Logout viene visualizzato un messaggio, chiudi la finestra del browser per disconnetterti completamente. In caso contrario, puoi continuare a utilizzare il browser per altri scopi.

