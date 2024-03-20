---
title: Che cos’è la protezione dei documenti?
description: Scopri come creare, archiviare e applicare impostazioni di riservatezza predefinite e distribuire le informazioni in modo sicuro utilizzando la protezione dei documenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: 0cdc9ee3-0172-43be-9b62-ed768534c074
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3219'
ht-degree: 0%

---

# Informazioni sulla protezione dei documenti {#about-document-security}

La protezione dei documenti garantisce che solo gli utenti autorizzati possano utilizzare i documenti. Grazie alla protezione dei documenti è possibile distribuire in modo sicuro le informazioni salvate in un formato supportato. I formati di file supportati includono:

* File Adobe PDF
* File Microsoft® Word, Excel e PowerPoint

Per ulteriori informazioni su come le policy proteggono i tipi di file supportati, vedi [ulteriori informazioni sulla protezione dei documenti](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-security/document-security-offerings.html?lang=en).

La protezione dei documenti consente di creare, archiviare e applicare facilmente impostazioni di riservatezza predefinite ai documenti. Per evitare che le informazioni si diffondano oltre la portata dell&#39;utente, è inoltre possibile monitorare e controllare il modo in cui i destinatari utilizzano i documenti dopo averli distribuiti.

È possibile proteggere i documenti utilizzando le policy. Una *policy* è una raccolta di informazioni che comprendono impostazioni di riservatezza e un elenco di utenti autorizzati. Le impostazioni di riservatezza specificate in una policy determinano il modo in cui un destinatario può utilizzare un documento al quale si applica la policy. È ad esempio possibile specificare se i destinatari possono stampare o copiare testo, modificare testo o aggiungere firme e commenti ai documenti protetti.

Gli utenti di Document Security possono creare policy tramite le pagine web degli utenti finali. Gli amministratori utilizzano le pagine web di Document Security per creare set di criteri contenenti criteri condivisi, disponibili per tutti gli utenti autorizzati.

Sebbene le policy siano memorizzate nella protezione dei documenti, è possibile applicarle ai documenti tramite l’applicazione client. La procedura per applicare le policy ai documenti di PDF è descritta in dettaglio in *Guida di Acrobat*. L’applicazione delle policy utilizzando altre applicazioni, come Microsoft® Office, è documentata nella sezione *Guida delle estensioni di Acrobat Reader DC* per l&#39;applicazione.

Quando si applica una policy a un documento, le impostazioni di riservatezza specificate nella policy proteggono le informazioni contenute nel documento. Le impostazioni di riservatezza proteggono anche tutti i file (testo, audio o video) all’interno di un documento PDF. Puoi distribuire il documento protetto tramite policy ai destinatari autorizzati dalla policy.

**Controllo e verifica dell’accesso ai documenti**

L&#39;utilizzo di una policy per proteggere un documento offre un controllo costante su quel documento, anche dopo averlo distribuito. È possibile monitorare il documento, modificare la policy, impedire agli utenti di continuare ad accedere al documento e cambiare la policy applicata al documento.

Tramite la protezione dei documenti è possibile monitorare i documenti protetti tramite policy e tenere traccia degli eventi, ad esempio quando un utente autorizzato o non autorizzato tenta di aprire il documento.

**Componenti**

Document Security è costituito da un server e da un’interfaccia utente:

**Server:** Componente centrale attraverso il quale la protezione dei documenti esegue transazioni quali l’autenticazione degli utenti, la gestione in tempo reale delle policy e l’applicazione della riservatezza. Il server fornisce inoltre un repository centrale per le regole, i record di controllo e altre informazioni correlate.

**Pagine Web:** Interfaccia in cui è possibile creare policy, gestire i documenti protetti tramite policy e monitorare gli eventi associati ai documenti protetti tramite policy. Gli amministratori possono anche configurare opzioni globali quali l’autenticazione degli utenti, il controllo e la messaggistica per gli utenti invitati e gestire gli account utente invitati.

![rm_psworkflow](assets/rm_psworkflow.png)

I passaggi nell’illustrazione sono i seguenti:

1. Il proprietario del documento crea i criteri utilizzando le pagine Web. I proprietari dei documenti possono creare policy personali accessibili solo a loro. Gli amministratori e i coordinatori di set di policy possono creare policy condivise all’interno di set accessibili agli utenti autorizzati.
1. Il proprietario del documento applica la policy, quindi salva e distribuisce il documento. Il documento può essere distribuito via e-mail, tramite una cartella di rete o su un sito Web.
1. Il destinatario apre il documento nell’applicazione client appropriata. Il destinatario può utilizzare il documento in base ai propri criteri.
1. Il proprietario del documento, il coordinatore di set di policy o l’amministratore possono tenere traccia dei documenti e modificarne l’accesso utilizzando le pagine web.

## Informazioni sugli utenti di Document Security {#about-document-security-users}

Diversi tipi di utenti utilizzano la protezione dei documenti per eseguire attività diverse:

* L’amministratore di sistema o la persona che si occupa di altri sistemi informativi installa e configura la protezione dei documenti. Questa persona può anche essere responsabile della configurazione delle impostazioni globali per il server, le pagine web, le policy e i documenti.

  Queste impostazioni possono includere, ad esempio, un URL di sicurezza del documento di base, notifiche di controllo e privacy, avvisi di registrazione per gli utenti invitati e periodi di lease offline predefiniti.

* Gli amministratori della sicurezza dei documenti creano policy e set di policy e gestiscono i documenti protetti tramite policy per gli utenti in base alle esigenze. Inoltre, creano gli account utente invitati e monitorano il sistema, il documento, l’utente, i criteri, il set di criteri e gli eventi personalizzati. Possono anche essere responsabili della configurazione del server globale e delle impostazioni della pagina web e dei criteri con un amministratore di sistema.

  Gli amministratori possono assegnare agli utenti i seguenti ruoli nell’area User Management della console di amministrazione. Gli utenti a cui sono assegnati questi ruoli eseguono le proprie attività nell’area dell’interfaccia utente di document security della console di amministrazione.

  **Amministratore privilegiato di Document Security**

  Gli utenti con questo ruolo possono accedere a tutte le impostazioni di protezione dei documenti nella console di amministrazione. Queste autorizzazioni sono associate al ruolo:

   * Gestisci configurazione
   * Gestire i criteri
   * Gestire i set di criteri
   * Gestione documenti
   * Gestisci autori documenti
   * Gestire gli utenti invitati e locali
   * Visualizza eventi
   * Delega
   * Invita utenti esterni

  **Amministratore di Document Security**

  Gli utenti con questo ruolo possono configurare il server di Document Security utilizzando la pagina Configurazione nella sezione Document Security della console di amministrazione. Questa autorizzazione è associata al ruolo Gestisci configurazione.

  >[!NOTE]
  >
  >Gli utenti con questo ruolo devono inoltre disporre del ruolo User della console di amministrazione per poter accedere alla console di amministrazione e modificare le impostazioni relative alla configurazione.

  **Amministratore set di criteri di sicurezza dei documenti**

  Gli utenti con questo ruolo possono utilizzare la sezione document security della console di amministrazione per modificare le policy di altri utenti e per creare, modificare ed eliminare set di policy. Quando un amministratore crea un set di criteri, può assegnargli un coordinatore. Queste autorizzazioni sono associate al ruolo:

   * Gestire i criteri
   * Gestire i set di criteri
   * Gestione documenti
   * Gestisci autori documenti
   * Visualizza eventi
   * Delega

  >[!NOTE]
  >
  >Gli utenti con questo ruolo devono inoltre disporre del ruolo User della console di amministrazione per poter accedere alla console di amministrazione e modificare le impostazioni relative alla configurazione.

  **Document Security gestisce gli utenti invitati e locali**

  Gli utenti con questo ruolo possono eseguire le attività necessarie per gestire tutti gli utenti invitati e locali sulle pagine web di Document Security pertinenti. Queste autorizzazioni sono associate al ruolo:

   * Gestire gli utenti invitati e locali
   * Invita utenti esterni
   * Accedere alle pagine web degli utenti finali

  >[!NOTE]
  >
  >Gli utenti con questo ruolo devono inoltre disporre del ruolo User della console di amministrazione per poter accedere alla console di amministrazione e modificare le impostazioni relative alla configurazione.

  **Utente invito Document Security**

  Gli utenti con questo ruolo possono invitare gli utenti. Queste autorizzazioni sono associate al ruolo:

   * Invita utenti esterni
   * Accedere alle pagine web degli utenti finali

  **Utente finale di Document Security**

  Gli utenti con questo ruolo possono accedere alle pagine web degli utenti finali di Document Security. Questo ruolo può anche essere assegnato agli amministratori per consentire loro di creare criteri utilizzando le pagine degli utenti finali. Questa autorizzazione è associata al ruolo Accedere alle pagine Web degli utenti finali.

* Gli utenti dell’organizzazione che dispongono di account di Document Security validi creano policy proprie, utilizzano policy per proteggere i documenti, tenere traccia e gestire i documenti protetti tramite policy e monitorare gli eventi correlati ai propri documenti.
* I coordinatori di set di policy gestiscono documenti, visualizzano eventi e gestiscono altri coordinatori di set di policy (in base alle loro autorizzazioni). Gli amministratori designano gli utenti come coordinatori di set di criteri per set di criteri specifici.
* Gli utenti esterni all’organizzazione (ad esempio, un partner commerciale) possono utilizzare documenti protetti tramite policy se si trovano nella directory document security, se l’amministratore crea un account per loro o se si registrano con document security tramite un processo di invito e-mail automatico. A seconda del modo in cui l’amministratore abilita le impostazioni di accesso, gli utenti invitati possono anche disporre dell’autorizzazione per applicare policy ai documenti, creare, modificare ed eliminare le proprie policy e invitare altri utenti esterni a utilizzare i propri documenti protetti tramite policy.
* Gli sviluppatori utilizzano l’SDK di AEM Forms per integrare applicazioni personalizzate con la sicurezza dei documenti.

Gli amministratori di Document Security possono creare ruoli personalizzati utilizzando le seguenti autorizzazioni in Gestione utente:

* Gestione configurazione Document Security
* Gestione della sicurezza dei documenti per utenti invitati e locali
* Gestione set di criteri per la protezione dei documenti
* Gestione set di criteri per la protezione dei documenti
* Document Security View Server Events
* Proprietario modifica criterio di protezione documento

## Criteri e documenti protetti tramite policy {#policies-and-policy-protected-documents}

A *policy* definisce un set di impostazioni di riservatezza e gli utenti che possono accedere a un documento a cui viene applicata la policy. Una policy consente inoltre di modificare dinamicamente le autorizzazioni di un documento. Alla persona che protegge il documento viene concessa l’autorizzazione a modificare le impostazioni di riservatezza per revocare l’accesso al documento o cambiare la policy.

È possibile applicare la protezione tramite policy a un documento PDF utilizzando Adobe Acrobat® Pro e Acrobat Standard. È possibile applicare la protezione tramite policy ad altri tipi di file, ad esempio i file Microsoft® Word, Excel e PowerPoint, utilizzando l&#39;applicazione client con le estensioni di Acrobat Reader DC appropriate installate.

### Funzionamento dei criteri {#how-policies-work}

Le policy contengono informazioni sugli utenti autorizzati e le impostazioni di riservatezza da applicare ai documenti. Gli utenti possono essere tutti nell’organizzazione e le persone esterne all’organizzazione che dispongono di un account. Se l’amministratore abilita la funzione di invito dell’utente, è anche possibile aggiungere nuovi utenti ai criteri, avviando quindi un processo e-mail di invito alla registrazione.

Le impostazioni di riservatezza di una policy determinano il modo in cui i destinatari possono utilizzare il documento. È ad esempio possibile specificare se i destinatari possono stampare o copiare testo, apportare modifiche o aggiungere firme e commenti ai documenti protetti. Lo stesso criterio può inoltre specificare impostazioni di riservatezza diverse per utenti specifici.

>[!NOTE]
>
>Le impostazioni di riservatezza applicate tramite una policy sostituiscono eventuali impostazioni applicate a un documento PDF in Acrobat utilizzando le opzioni di sicurezza relative alla password o al certificato. Per ulteriori informazioni, consulta la Guida di Acrobat.

Gli utenti e gli amministratori possono creare policy tramite le pagine web di document security. A un documento è possibile applicare un solo criterio alla volta. È possibile applicare una policy utilizzando uno dei seguenti metodi:

* Apri il documento in Acrobat o in un’altra applicazione client e seleziona una policy per proteggere il documento.
* Inviare un documento come allegato e-mail in Microsoft® Outlook. In questo caso, è possibile selezionare un criterio da un elenco di criteri. In alternativa, puoi selezionare una policy generata automaticamente che Acrobat crea con un set predefinito di impostazioni di riservatezza per proteggere il documento solo per i destinatari del messaggio e-mail.

È possibile rimuovere una policy da un documento utilizzando l’applicazione client.

![rm_psonline_policy](assets/rm_psonline_policy.png)

I passaggi nel diagramma sono i seguenti:

1. Il proprietario del documento protegge il documento da un&#39;applicazione client supportata con un criterio che consente l&#39;utilizzo online.
1. Document Security crea una licenza per documenti e le relative chiavi, quindi crittografa la policy. La licenza del documento, la policy crittografata e la chiave del documento vengono restituite all&#39;applicazione client.
1. Il documento viene crittografato con la chiave del documento, che viene quindi eliminata. Il documento ora incorpora la licenza e il criterio. Queste attività vengono eseguite nell’applicazione client supportata.

Quando applichi una policy a un documento, le informazioni in esso contenute, inclusi eventuali file contenuti (testo, audio o video) nei documenti PDF, sono protette dalle impostazioni di riservatezza specificate nella policy. Document Security genera una licenza e informazioni di crittografia che vengono poi incorporate nel documento. Quando si distribuisce il documento, Document Security può autenticare i destinatari che tentano di aprirlo e autorizzare l’accesso in base ai privilegi specificati nella policy.

Se l&#39;utilizzo offline è abilitato, i destinatari possono anche utilizzare documenti protetti tramite policy in modalità offline (senza una connessione Internet o di rete attiva) per il periodo di tempo specificato nella policy.

### Funzionamento dei documenti protetti tramite policy {#how-policy-protected-documents-work}

Per aprire e utilizzare documenti protetti tramite policy, è necessario includere il proprio nome come destinatario e disporre di un account di protezione dei documenti valido. Per i documenti PDF, è necessario Acrobat o Adobe Reader®. Per altri tipi di file, è necessaria l’applicazione appropriata per il file con le estensioni di Acrobat Reader DC installate.

Quando apri un documento protetto tramite policy, Acrobat, Adobe Reader o le estensioni Acrobat Reader DC si connettono alla protezione dei documenti per autenticarti. Quindi, è possibile accedere. Se l&#39;utilizzo del documento è sottoposto a controllo, viene visualizzato un messaggio di notifica. Una volta che la protezione dei documenti determina le autorizzazioni da concedere, gestisce la decrittografia del documento. È quindi possibile utilizzare il documento in base alle impostazioni di riservatezza delle policy.

![rm_psopen_online](assets/rm_psopen_online.png)

I passaggi nel diagramma sono i seguenti:

1. L&#39;utente apre il documento in un&#39;applicazione client supportata e si autentica con il server. L’identificatore del documento viene inviato al server di Document Security.
1. Document Security autentica gli utenti, controlla la policy per l’autorizzazione e crea un voucher. Il voucher (che contiene la chiave del documento e le autorizzazioni) viene restituito all&#39;applicazione client.
1. Il documento viene decrittografato con la chiave del documento e la chiave del documento viene eliminata. Il documento può quindi essere utilizzato in base alle impostazioni di riservatezza della policy. Queste attività vengono eseguite nell’applicazione client supportata.

È possibile continuare a utilizzare un documento nelle seguenti condizioni:

* A tempo indeterminato o per il periodo di validità specificato nella polizza
* Fino a quando l’amministratore o la persona che ha applicato la policy non revoca l’accesso al documento o non modifica la policy

È inoltre possibile utilizzare documenti protetti tramite policy in modalità non in linea (senza una connessione Internet o di rete) se la policy consente l’accesso non in linea. Accedi innanzitutto a document security per sincronizzare il documento. È quindi possibile utilizzare il documento durante il periodo di lease offline specificato nel criterio.

Al termine del periodo di lease offline, sincronizza nuovamente il documento con document security, accedendo online e aprendo un documento protetto tramite policy o utilizzando un comando nell’applicazione client. Consulta *Guida di Acrobat* o il *Guida delle estensioni di Acrobat Reader DC* per i dettagli.

Se si salva una copia di un documento protetto tramite policy utilizzando il comando di menu Salva o Salva con nome, la policy viene automaticamente applicata e applicata al nuovo documento. Eventi come i tentativi di aprire il nuovo documento vengono controllati e registrati anche per il documento originale.

## Set di criteri {#policy-sets}

*Set di criteri* vengono utilizzati per raggruppare un insieme di criteri con uno scopo aziendale comune. Questi set di criteri vengono quindi resi disponibili a un sottoinsieme di utenti nel sistema.

A ogni set di criteri possono essere associati uno o più coordinatori di set di criteri. Il coordinatore del set di criteri è un amministratore o un utente che dispone di più autorizzazioni. Il *coordinatore set di criteri* in genere è uno specialista dell’organizzazione che può creare al meglio i criteri in un particolare set di criteri.

I coordinatori dei set di criteri possono eseguire le seguenti attività:

* Creare criteri
* Modificare ed eliminare qualsiasi criterio nel set di criteri
* Modifica impostazioni set di criteri
* Aggiungere e rimuovere i coordinatori di set di criteri
* Visualizzare eventi relativi a criteri e documenti per qualsiasi criterio o documento all&#39;interno del set di criteri
* Revoca dell&#39;accesso ai documenti
* Cambia criteri per il documento.

>[!NOTE]
>
>È possibile recuperare un massimo di 1000 nomi di set di criteri dal database utilizzando `getAllPolicysetnames()` API.

I set di criteri vengono creati ed eliminati nelle pagine web dell’amministrazione di Document Security dagli amministratori e dai coordinatori dei set di criteri che dispongono delle autorizzazioni necessarie.

I set di criteri vengono resi disponibili a un numero limitato di utenti specificando quali utenti o gruppi all&#39;interno di un dominio possono utilizzare i criteri del set di criteri per proteggere i documenti.

Quando è installata la protezione dei documenti, viene creato un set di criteri predefinito denominato *Set di criteri globale*. L&#39;amministratore che ha installato il software gestisce questo set di criteri.

## Best practice {#best-practices}

I criteri sono set riutilizzabili di autorizzazioni e gruppi di utenti che possono essere applicati a vari documenti. Per i documenti protetti. Queste policy garantiscono che solo gli utenti autorizzati possano utilizzare le funzioni consentite. Il numero di criteri e set di criteri dovrebbe aumentare con l&#39;aumento dei diversi ruoli utente e documenti all&#39;interno di un reparto. Per creare e gestire le policy, ecco alcune considerazioni e best practice:

* **Creare criteri riutilizzabili:** L’Adobe consiglia di riutilizzare le policy in vari documenti. Consente di ridurre al minimo il numero di criteri, fornire prestazioni ottimali e semplificare la gestione. Per creare un criterio riutilizzabile:

1. Identificare e definire i requisiti di controllo dell&#39;accesso a livello di reparto e organizzazione.

1. Creare gruppi di utenti e aggiungere utenti a tali gruppi.

1. Crea un set di criteri.

1. Apri il set di criteri e crea un criterio. Aggiungere gruppi di utenti e impostare le impostazioni di riservatezza (controllo di accesso) per il criterio.

Aggiungere gruppi di utenti ai criteri anziché singoli utenti. Semplifica la gestione e l’applicazione delle policy a molti utenti.

* **Creare set di criteri personalizzati:** Un set di criteri combina più criteri in un’entità gestibile. Creare set di criteri personalizzati per l&#39;organizzazione o il reparto, utilizzarli per raggruppare i criteri correlati e renderli disponibili per un sottoinsieme di utenti nel sistema.

  L&#39;utilizzo dei set di criteri semplifica l&#39;assegnazione e la gestione dei criteri correlati a utenti specifici di un&#39;organizzazione o di un reparto. Ad esempio, set di politiche separati per il reparto finanze e risorse umane possono facilitare la gestione e l&#39;applicazione delle politiche correlate ai documenti designati per i reparti corrispondenti.

* **Utilizza un autorizzatore esterno per applicare le autorizzazioni in modo dinamico:** È possibile utilizzare [autorizzatore esterno](https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html) per valutare e applicare in modo dinamico le autorizzazioni in base alla condizione esterna. Quando le autorizzazioni vengono valutate dinamicamente, in base alla condizione esterna, è possibile:

   * Controllo centralizzato dell&#39;accesso ai documenti dell&#39;organizzazione.

   * Controllare l’accesso ai documenti protetti tramite policy determinando in modo dinamico se un utente può accedere a un documento protetto tramite policy. Ad esempio, decide in modo dinamico se un utente può stampare un documento protetto tramite policy.

   * Oltre al processo standard di valutazione dei criteri, utilizza un meccanismo di controllo degli accessi utilizzato dal sistema di gestione dei contenuti. Ad esempio, quando il servizio determina se un utente può stampare un documento protetto tramite policy, può utilizzare il processo standard di valutazione della policy. Può inoltre utilizzare il meccanismo di controllo degli accessi utilizzato dal sistema di gestione dei contenuti.

  Sebbene sia possibile sostituire completamente il processo di valutazione dei criteri di Document Security con un gestore di autorizzazioni esterno, si consiglia di utilizzare un gestore di autorizzazioni esterno con il processo di valutazione dei criteri. Di conseguenza, l&#39;accesso ai documenti può essere controllato mediante lo stesso meccanismo di controllo utilizzato dal sistema di gestione dei contenuti. Ad esempio, quando il servizio Document Security determina se un utente può stampare un documento protetto tramite policy, utilizza il processo standard di valutazione delle policy. Utilizza anche il meccanismo di controllo degli accessi utilizzato dal sistema di gestione dei contenuti. Per ulteriori informazioni, consulta [Creazione di gestori di autorizzazioni esterni](https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-6f26.2.html).

* **Mantieni i set di criteri a un numero limitato:** Diversi fattori determinano una crescita costante delle politiche e delle serie di politiche. Alcuni fattori comuni sono:

   * Incremento di ruoli utente, reparti e documenti all&#39;interno di un&#39;organizzazione in un periodo.
   * I dipartimenti di un&#39;organizzazione lavorano in isolamento e mantengono uno stretto controllo sulle politiche specifiche del dipartimento. Questo porta a politiche identiche all’interno di un’organizzazione.

  L&#39;Adobe raccomanda di mantenere al minimo il numero di politiche e set di politiche. Consente di gestire facilmente le regole e i set di regole e di fornire prestazioni migliori. Per ridurre al minimo il numero:

   * Creare criteri riutilizzabili. Questi criteri possono essere condivisi tra più reparti.
   * Prendere in considerazione la creazione di set di criteri a livello di organizzazione, se alcuni criteri vengono applicati a più reparti anziché a un singolo set di criteri per ogni reparto.
   * Criteri correlati al gruppo in un set di criteri. Non creare un set di criteri separato per ciascun criterio.
   * Utilizza un autorizzatore esterno per controllare dinamicamente le autorizzazioni utente.

  >[!NOTE]
  >
  >È possibile utilizzare [getAllPolicysetnames()](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/PolicyManager.html) API per recuperare un massimo di 1000 nomi di set di criteri. Internamente, l’API recupera un massimo di 1000 criteri per i quali l’invocatore API dispone dell’autorizzazione di pubblicazione del documento, quindi crea e restituisce all’utente un elenco di nomi univoci di set di criteri associati ai criteri recuperati. Ad esempio, quando l’API recupera 1000 criteri e i criteri recuperati sono associati a 200 set di criteri in totale, l’API restituisce solo 200 nomi di set di criteri.
