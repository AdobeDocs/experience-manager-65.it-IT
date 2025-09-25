---
title: Utilizzo delle pagine web sulla protezione dei documenti
description: Scopri come accedere, navigare e utilizzare le pagine web sulla protezione dei documenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '933'
ht-degree: 100%

---

# Utilizzo delle pagine web sulla protezione dei documenti {#using-the-document-security-webpages}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utenti e amministratori utilizzano le pagine web relative alla protezione dei documenti per creare e gestire i criteri e i documenti protetti da criteri e monitorare gli eventi associati ai documenti protetti tramite criteri. Gli amministratori utilizzano inoltre le pagine web per creare set di criteri e designare i coordinatori dei set di criteri, configurare le impostazioni predefinite sulla protezione dei documenti, gestire la registrazione e gli account degli utenti invitati e monitorare e gestire eventi relativi a server, criteri, utenti e documenti.

>[!NOTE]
>
>Puoi accedere alla protezione dei documenti anche tramite Acrobat e altre applicazioni client utilizzando il tuo account di accesso utente. Consulta [Impostazione dell’accesso alla protezione dei documenti dalle applicazioni client](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).

Per aprire le pagine web, devi disporre di un browser, dell’URL e delle informazioni di accesso per la protezione dei documenti. L’URL per gli utenti è diverso da quello per gli amministratori.

Poiché la funzione di protezione dei documenti fa riferimento alle directory esistenti dell’organizzazione per le informazioni utente, le informazioni di accesso alla funzione di protezione dei documenti potrebbero essere le stesse utilizzate per accedere alla rete e ad altre applicazioni. Per informazioni sull’account, rivolgiti all’amministratore di sistema o all’amministratore.

Per accedere come amministratore, devi disporre del ruolo di amministratore assegnato. Puoi utilizzare l’account amministratore privilegiato predefinito creato durante il processo di installazione.

## Accedi alle pagine web {#log-in-to-the-web-pages}

Per accedere alle pagine web utilizzando un browser, devi disporre dell’URL relativo alla protezione dei documenti e di un account. L’URL per gli utenti è diverso da quello per gli amministratori. Gli amministratori possono anche accedere alle pagine utente per creare i criteri.

Se hai accesso a più installazioni di protezione dei documenti, devi disporre dell’URL dell’istanza della protezione dei documenti a cui desideri accedere. Se non disponi di queste informazioni, rivolgiti al tuo amministratore. L’URL predefinito per le pagine utente è `https://[host]:[port]/edc`. In alcuni casi il numero di porta potrebbe non essere necessario. Per ulteriori informazioni, rivolgiti all’amministratore.

L’URL predefinito per gli amministratori è `https://[host]:[port]/adminui`.

Per gli amministratori, durante l’installazione viene creato un account di amministratore privilegiato predefinito. È possibile utilizzare questo account per eseguire l’accesso alla prima installazione della protezione dei documenti.

>[!NOTE]
>
>Puoi anche accedere alle pagine web da Acrobat e da altre applicazioni client. Per ulteriori informazioni, vedere la Guida di Acrobat o la Guida alle estensioni di Acrobat Reader DC appropriate.

1. Digita l’URL nel browser:

   URL alla protezione dei documenti: `https://[host]:[port]/edc`

   o URL alla Console di amministrazione: `https://[host]:[port]/adminui`

1. Nella finestra di accesso, digita il nome utente e la password e fai clic su OK.
1. Nella Console di amministrazione, fai clic su Servizi > Protezione dei documenti.

>[!NOTE]
>
>Quando utilizzi le pagine web, evita di utilizzare i pulsanti del browser, ad esempio il pulsante Indietro, il pulsante Aggiorna e le frecce Indietro e Avanti, perché questa azione può causare problemi indesiderati di acquisizione e visualizzazione dei dati.

## Navigazione nelle pagine web {#navigating-the-web-pages}

Accedendo alle pagine web degli utenti, troverai i collegamenti alle pagine utente Criteri, Documenti ed Eventi.

Quando accedi alla Console di amministrazione e apri la pagina principale relativa alla protezione dei documenti, potresti visualizzare uno o due collegamenti aggiuntivi, uno per la pagina Configurazione e uno per la pagina Utenti invitati e locali. La pagina Utenti invitati e locali viene visualizzata solo se la registrazione degli utenti invitati è abilitata.

Utilizza questi collegamenti per accedere alle varie pagine, in cui è possibile creare e gestire policy e documenti protetti tramite criteri.

**Mostra una pagina**

1. Fai clic sul nome della pagina, ad esempio Criteri.

**Torna alla pagina precedente**

1. Fai clic sul collegamento di navigazione nella parte superiore della pagina per la pagina a cui desideri tornare.

**Aggiorna l’elenco dei dati in una pagina**

1. Nella pagina principale fai clic sul collegamento alla pagina che si desidera aggiornare.

>[!NOTE]
>
>Quando utilizzi le pagine web, evita di utilizzare i pulsanti del browser, ad esempio il pulsante Indietro, il pulsante Aggiorna e le frecce Indietro e Avanti, perché questa azione può causare problemi indesiderati di acquisizione e visualizzazione dei dati.

## Impostazione dell’accesso alla protezione dei documenti dalle applicazioni client {#setting-up-access-to-document-security-from-client-applications}

Le applicazioni client devono essere configurate in modo da connettersi alla protezione dei documenti per proteggerli, aprire i documenti protetti tramite criteri e connettersi alle pagine web di sicurezza dei documenti. Per informazioni sulla configurazione della connessione nell’applicazione client, consulta la *Guida di Acrobat* o la *Guida di RightsManagementExtension* appropriata.

La protezione dei documenti è accessibile tramite Secure Sockets Layer (SSL). Installa il certificato del sito web nel tuo archivio certificati in modo da poter accedere alla protezione dei documenti tramite le applicazioni client.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Queste istruzioni sono specifiche per Internet Explorer, ma puoi installare il certificato utilizzando qualsiasi browser web supportato. Per ulteriori informazioni, consulta la Guida del browser in uso.

**Installare il certificato del server utilizzando Internet Explorer**

1. Apri il browser web e digita l’URL di base per la protezione dei documenti nella casella Indirizzo. Ad esempio, digita `https://[host]:[port]`. Verrà visualizzata una finestra di dialogo Avviso di sicurezza.
1. Fai clic su Visualizza certificato, quindi su Installa certificato e seleziona le impostazioni predefinite per l’installazione. Il certificato deve essere installato nelle Autorità di certificazione principali affidabili.
1. Chiudi la sessione del browser.
1. Apri un’altra finestra del browser e digita lo stesso URL nella casella Indirizzo. La finestra di dialogo Avviso di sicurezza non dovrebbe essere visualizzata. Il test conferma che il certificato è installato correttamente.

## Disconnettersi dalle pagine web {#log-out-of-the-web-pages}

Disconnettiti al termine dell’utilizzo delle pagine web in modo da poter utilizzare in modo sicuro il browser web per altri scopi. A seconda della configurazione della protezione dei documenti, potrebbe essere necessario chiudere il browser per disconnettersi completamente.

1. Fai clic su Disconnetti nell’angolo superiore destro della pagina.
1. Se nella pagina Disconnetti viene visualizzato un messaggio, chiudi la finestra del browser per disconnetterti completamente. In caso contrario, puoi continuare a utilizzare il browser per altri scopi.
