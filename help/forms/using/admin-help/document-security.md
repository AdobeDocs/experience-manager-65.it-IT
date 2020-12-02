---
title: 'Informazioni sulla protezione dei documenti '
seo-title: 'Informazioni sulla protezione dei documenti '
description: Scoprite come creare, archiviare e applicare impostazioni predefinite per la salvaguardia della riservatezza e distribuire le informazioni in modo sicuro utilizzando la protezione dei documenti.
seo-description: Scoprite come creare, archiviare e applicare impostazioni predefinite per la salvaguardia della riservatezza e distribuire le informazioni in modo sicuro utilizzando la protezione dei documenti.
uuid: e4fba2a4-f3c1-4b20-8e05-8e241b40ebd0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1820cb38-ba70-4cce-8895-290524bdd9bf
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '2546'
ht-degree: 0%

---


# Informazioni sulla protezione dei documenti {#about-document-security}

La protezione dei documenti garantisce che solo gli utenti autorizzati possano utilizzare i documenti. La protezione dei documenti consente di distribuire in modo sicuro tutte le informazioni salvate in un formato supportato. I formati di file supportati includono:

*  file Adobe PDF
* File di Microsoft® Word, Excel e PowerPoint

Per ulteriori informazioni sulla protezione dei tipi di file supportati tramite i criteri, vedere [Informazioni aggiuntive sulla protezione dei documenti](https://www.adobe.com/go/learn_aemforms_doc_security_63).

La protezione dei documenti consente di creare, memorizzare e applicare facilmente ai documenti impostazioni predefinite per la salvaguardia della riservatezza. Per evitare che le informazioni si diffondano oltre la portata dell&#39;utente, è inoltre possibile monitorare e controllare in che modo i destinatari utilizzano i documenti dopo averli distribuiti.

È possibile proteggere i documenti utilizzando i criteri. Una *policy* è una raccolta di informazioni che include impostazioni per la salvaguardia della riservatezza e un elenco di utenti autorizzati. Le impostazioni di riservatezza specificate in un criterio determinano in che modo il destinatario può utilizzare il documento a cui si applica il criterio. Ad esempio, è possibile specificare se i destinatari possono stampare o copiare il testo, modificare il testo o aggiungere firme e commenti ai documenti protetti.

Gli utenti di Document Security creano i criteri tramite le pagine Web dell&#39;utente finale. Gli amministratori utilizzano le pagine Web relative alla protezione dei documenti per creare set di criteri che contengono criteri condivisi disponibili per tutti gli utenti autorizzati.

Sebbene i criteri siano memorizzati nella protezione dei documenti, tali criteri vengono applicati ai documenti tramite l&#39;applicazione client. Come applicare i criteri ai documenti PDF è descritto dettagliatamente in *Guida di Acrobat*. L&#39;applicazione dei criteri tramite l&#39;uso di altre applicazioni, come Microsoft Office, è documentata nella Guida delle *estensioni Acrobat Reader DC* per l&#39;applicazione.

Quando applicate un criterio a un documento, le impostazioni di riservatezza specificate nel criterio proteggono le informazioni contenute nel documento. Le impostazioni per la salvaguardia della riservatezza proteggono inoltre tutti i file (testo, audio o video) presenti in un documento PDF. Potete distribuire il documento protetto tramite criterio ai destinatari autorizzati dal criterio.

**Controllo e controllo dell&#39;accesso ai documenti**

L&#39;utilizzo di un criterio per proteggere un documento consente di controllare in modo continuativo il documento, anche dopo averlo distribuito. È possibile monitorare il documento, apportare modifiche al criterio, impedire agli utenti di continuare ad accedere al documento e cambiare il criterio applicato al documento.

Tramite la protezione dei documenti è possibile monitorare i documenti protetti tramite criterio e tenere traccia degli eventi, ad esempio quando un utente autorizzato o non autorizzato tenta di aprire il documento.

**Componenti**

Document Security è costituito da un&#39;interfaccia server e utente:

**Server:** Il componente centrale tramite il quale la protezione dei documenti esegue transazioni quali l&#39;autenticazione degli utenti, la gestione in tempo reale dei criteri e l&#39;applicazione della riservatezza. Il server fornisce inoltre un archivio centrale per criteri, record di controllo e altre informazioni correlate.

**Pagine Web:** Interfaccia in cui vengono creati criteri, gestiti i documenti protetti tramite criterio e monitorati gli eventi associati ai documenti protetti tramite criterio. Gli amministratori possono inoltre configurare opzioni globali quali l&#39;autenticazione degli utenti, il controllo e la messaggistica per gli utenti invitati e gestire gli account utente invitati.

![rm_psworkflow](assets/rm_psworkflow.png)

I passaggi nell&#39;illustrazione sono i seguenti:

1. Il proprietario del documento crea i criteri utilizzando le pagine Web. I proprietari dei documenti possono creare criteri personali accessibili solo a tali utenti. Gli amministratori e i coordinatori di set di criteri possono creare criteri condivisi all&#39;interno di set di criteri accessibili agli utenti autorizzati.
1. Il proprietario del documento applica il criterio, quindi salva e distribuisce il documento. Il documento può essere distribuito via e-mail, tramite una cartella di rete o su un sito Web.
1. Il destinatario apre il documento nell&#39;applicazione client appropriata. Il destinatario può utilizzare il documento in base ai propri criteri.
1. Il proprietario del documento, il coordinatore del set di criteri o l&#39;amministratore possono tenere traccia dei documenti e modificarne l&#39;accesso tramite le pagine Web.

## Informazioni sugli utenti della protezione dei documenti {#about-document-security-users}

Diversi tipi di utenti utilizzano la protezione dei documenti per eseguire diverse attività:

* L&#39;amministratore di sistema o altri sistemi informativi (IS) persona installa e configura la protezione dei documenti. Questa persona può anche essere responsabile della configurazione delle impostazioni globali per il server, le pagine Web, i criteri e i documenti.

   Queste impostazioni possono includere, ad esempio, un URL di protezione del documento di base, notifiche di controllo e privacy, avvisi di registrazione degli utenti invitati e periodi di tempo di tempo consentito per l&#39;utilizzo offline predefinito.

* Gli amministratori di Document Security creano criteri e set di criteri e gestiscono i documenti protetti tramite criterio per gli utenti, a seconda delle necessità. Possono inoltre creare account utente invitati e monitorare il sistema, il documento, l&#39;utente, il criterio, il set di criteri e gli eventi personalizzati. Possono inoltre essere responsabili della configurazione del server globale, delle pagine Web e delle impostazioni dei criteri insieme a un amministratore di sistema.

   Gli amministratori possono assegnare agli utenti i seguenti ruoli nell’area Gestione utente della console di amministrazione. Gli utenti ai quali sono stati assegnati questi ruoli eseguono le proprie attività nell&#39;area dell&#39;interfaccia utente di Document Security della console di amministrazione.

   **Amministratore di Document Security**

   Gli utenti con questo ruolo possono accedere a tutte le impostazioni di protezione dei documenti nella console di amministrazione. Tali autorizzazioni sono associate al ruolo:

   * Gestisci configurazione
   * Gestisci criterio
   * Gestire i set di criteri
   * Gestire i documenti
   * Gestire gli editori di documenti
   * Gestione degli utenti invitati e locali
   * Visualizzare gli eventi
   * Delega
   * Invita utenti esterni

   **Amministratore di Document Security**

   Gli utenti con questo ruolo possono configurare il server di protezione del documento, utilizzando la pagina Configurazione nella sezione Protezione documento della console di amministrazione. Questa autorizzazione è associata al ruolo Gestisci configurazione.

   >[!NOTE]
   >
   >Gli utenti con questo ruolo devono anche avere il ruolo utente della console di amministrazione per poter accedere alla console di amministrazione e modificare le impostazioni relative alla configurazione.

   **Amministratore set di criteri di protezione documenti**

   Gli utenti con questo ruolo possono utilizzare la sezione relativa alla protezione dei documenti della console di amministrazione per modificare i criteri degli altri utenti e per creare, modificare ed eliminare i set di criteri. Quando un amministratore di set di criteri crea un set di criteri, può assegnare a tale set di criteri un coordinatore di set di criteri. Tali autorizzazioni sono associate al ruolo:

   * Gestisci criterio
   * Gestire i set di criteri
   * Gestire i documenti
   * Gestire gli editori di documenti
   * Visualizzare gli eventi
   * Delega

   >[!NOTE]
   >
   >Gli utenti con questo ruolo devono anche avere il ruolo utente della console di amministrazione per poter accedere alla console di amministrazione e modificare le impostazioni relative alla configurazione.

   **Document Security gestisce gli utenti invitati e locali**

   Gli utenti con questo ruolo possono eseguire le attività necessarie per gestire tutti gli utenti invitati e locali nelle relative pagine Web sulla protezione dei documenti. Tali autorizzazioni sono associate al ruolo:

   * Gestione degli utenti invitati e locali
   * Invita utenti esterni
   * Accesso alle pagine Web dell&#39;utente finale

   >[!NOTE]
   >
   >Gli utenti con questo ruolo devono anche avere il ruolo utente della console di amministrazione per poter accedere alla console di amministrazione e modificare le impostazioni relative alla configurazione.

   **Utente invitato alla protezione dei documenti**

   Gli utenti con questo ruolo possono invitare gli utenti. Tali autorizzazioni sono associate al ruolo:

   * Invita utenti esterni
   * Accesso alle pagine Web dell&#39;utente finale

   **Utente finale di Document Security**

   Gli utenti con questo ruolo possono accedere alle pagine Web dell&#39;utente finale relative alla protezione dei documenti. Questo ruolo può anche essere assegnato agli amministratori per consentire agli amministratori di creare criteri utilizzando le pagine dell&#39;utente finale. Questa autorizzazione è associata al ruolo Accesso alle pagine Web dell&#39;utente finale.

* Gli utenti all&#39;interno dell&#39;organizzazione che dispongono di account di protezione documenti validi creano criteri propri, utilizzano criteri per proteggere i documenti, tenere traccia e gestire i documenti protetti tramite criterio e monitorare gli eventi correlati ai documenti.
* I coordinatori di set di criteri gestiscono documenti, visualizzano eventi e gestiscono altri coordinatori di set di criteri (in base alle loro autorizzazioni). Gli amministratori designano gli utenti come coordinatori di set di criteri per specifici set di criteri.
* Gli utenti esterni all&#39;organizzazione (ad esempio, un partner commerciale) possono utilizzare documenti protetti tramite criterio se si trovano nella directory di protezione del documento di protezione, se l&#39;amministratore crea un account per tali documenti o se si registrano con la protezione del documento tramite un processo di invito e-mail automatico. A seconda di come l&#39;amministratore abilita le impostazioni di accesso, gli utenti invitati possono anche disporre dell&#39;autorizzazione per applicare i criteri ai documenti, per creare, modificare ed eliminare i propri criteri e per invitare altri utenti esterni a utilizzare i documenti protetti tramite criterio.
* Gli sviluppatori utilizzano l&#39;SDK per moduli AEM per integrare applicazioni personalizzate con la protezione dei documenti.

Gli amministratori di Document Security possono creare ruoli personalizzati utilizzando le seguenti autorizzazioni in Gestione utente:

* Configurazione di Document Security Manage
* Document security Gestisci utenti invitati e locali
* Set di criteri di gestione per la protezione dei documenti
* Set di criteri di gestione per la protezione dei documenti
* Eventi del server di visualizzazione della protezione dei documenti
* Proprietario criterio modifica protezione documento

## Criteri e documenti protetti tramite criterio {#policies-and-policy-protected-documents}

Un *policy* definisce un insieme di impostazioni per la salvaguardia della riservatezza e consente agli utenti di accedere a un documento a cui viene applicato il criterio. Un criterio consente inoltre di modificare dinamicamente le autorizzazioni per un documento. Consente alla persona che garantisce il documento di modificare le impostazioni di riservatezza per revocare l&#39;accesso al documento o cambiare il criterio.

La protezione tramite criterio può essere applicata a un documento PDF utilizzando  Adobe Acrobat® Pro e  Acrobat Standard. La protezione tramite criterio può essere applicata ad altri tipi di file, come file Microsoft Word, Excel e PowerPoint, utilizzando l&#39;applicazione client con le estensioni Acrobat Reader DC appropriate installate.

### Funzionamento dei criteri {#how-policies-work}

I criteri contengono informazioni sugli utenti autorizzati e le impostazioni per la salvaguardia della riservatezza da applicare ai documenti. Gli utenti possono essere qualsiasi nell&#39;organizzazione, nonché persone esterne all&#39;organizzazione che dispongono di un account. Se l&#39;amministratore abilita la funzione di invito dell&#39;utente, è anche possibile aggiungere nuovi utenti ai criteri, avviando quindi una procedura e-mail di invito alla registrazione.

Le impostazioni relative alla riservatezza specificate in un criterio determinano in che modo i destinatari possono utilizzare il documento. Ad esempio, è possibile specificare se i destinatari possono stampare o copiare il testo, apportare modifiche o aggiungere firme e commenti ai documenti protetti. Lo stesso criterio può anche specificare impostazioni di riservatezza diverse per utenti specifici.

>[!NOTE]
>
>Le impostazioni di riservatezza applicate tramite un criterio prevalgono su tutte le impostazioni che possono essere state applicate a un documento PDF in  Acrobat utilizzando le opzioni di protezione della password o del certificato. Per ulteriori informazioni, consultate  Guida di Acrobat.

Utenti e amministratori creano i criteri tramite le pagine Web di protezione dei documenti. A un documento è possibile applicare un solo criterio alla volta. È possibile applicare un criterio utilizzando uno dei seguenti metodi:

* Aprire il documento in  Acrobat o in un&#39;altra applicazione client e selezionare un criterio per proteggere il documento.
* Inviare un documento come allegato e-mail in Microsoft Outlook. In questo caso, è possibile selezionare un criterio da un elenco di criteri o selezionare un criterio generato automaticamente che  Acrobat crea con un set predefinito di impostazioni di riservatezza per proteggere il documento solo per i destinatari del messaggio e-mail.

Un criterio può essere rimosso da un documento utilizzando l&#39;applicazione client.

![rm_psonline_policy](assets/rm_psonline_policy.png)

I passaggi nel diagramma sono i seguenti:

1. Il proprietario del documento protegge il documento da un&#39;applicazione client supportata con un criterio che consente l&#39;uso online.
1. Document Security crea una licenza del documento e le chiavi del documento e cifra il criterio. La licenza del documento, i criteri crittografati e la chiave del documento vengono restituiti all&#39;applicazione client.
1. Il documento è crittografato con la chiave del documento e la chiave del documento viene scartata. Il documento ora incorpora la licenza e il criterio. Tali attività vengono eseguite nell&#39;applicazione client supportata.

Quando applicate un criterio a un documento, le informazioni contenute nel documento, compresi eventuali file contenuti (testo, audio o video) nei documenti PDF, sono protette dalle impostazioni per la salvaguardia della riservatezza specificate nel criterio. Document Security genera una licenza e informazioni di cifratura che vengono quindi incorporate nel documento. Quando si distribuisce il documento, Document Security può autenticare i destinatari che cercano di aprire il documento e autorizzare l&#39;accesso in base ai privilegi specificati nel criterio.

Se l&#39;utilizzo offline è abilitato, i destinatari possono anche utilizzare i documenti protetti tramite criterio offline (senza una connessione Internet o di rete attiva) per il periodo di tempo specificato nel criterio.

### Funzionamento dei documenti protetti tramite criterio {#how-policy-protected-documents-work}

Per aprire e utilizzare i documenti protetti tramite criterio, il criterio deve includere il vostro nome come destinatario e dovete disporre di un account valido per la protezione dei documenti. Per i documenti PDF, è necessario  Acrobat o  Adobe Reader®. Per altri tipi di file, è necessaria l&#39;applicazione appropriata per il file con le estensioni Acrobat Reader DC installate.

Quando si tenta di aprire un documento protetto tramite criterio,  Acrobat,  Adobe Reader o le estensioni Acrobat Reader DC si connettono alla protezione del documento per l&#39;autenticazione. Quindi, potete procedere all&#39;accesso. Se l&#39;uso del documento è sottoposto a controllo, viene visualizzato un messaggio di notifica. Dopo che Document Security determina le autorizzazioni del documento da concedere, gestisce la decrittazione del documento. Potete quindi utilizzare il documento in base alle impostazioni di riservatezza dei criteri.

![rm_psopen_online](assets/rm_psopen_online.png)

I passaggi nel diagramma sono i seguenti:

1. L&#39;utente del documento apre il documento in un&#39;applicazione client supportata e si autentica con il server. L&#39;identificatore del documento viene inviato al server di protezione del documento.
1. Document Security autentica gli utenti, verifica il criterio di autorizzazione e crea un voucher. Il voucher (che contiene la chiave del documento e le autorizzazioni) viene restituito all&#39;applicazione client.
1. Il documento viene decrittografato con la chiave del documento e la chiave del documento viene eliminata. Il documento può quindi essere utilizzato in base alle impostazioni di riservatezza del criterio. Tali attività vengono eseguite nell&#39;applicazione client supportata.

È possibile continuare a utilizzare un documento alle seguenti condizioni:

* Indefinitamente o per il periodo di validità specificato nel criterio
* Fino a quando l&#39;amministratore o la persona che ha applicato il criterio revoca l&#39;accesso al documento o cambia il criterio

Potete inoltre utilizzare i documenti protetti tramite criterio offline (senza una connessione Internet o di rete) se il criterio consente l&#39;accesso offline. Per sincronizzare il documento è innanzitutto necessario eseguire il login per proteggere il documento. Potete quindi utilizzare il documento per la durata del periodo di tempo consentito per l&#39;utilizzo non in linea specificato nel criterio.

Al termine del periodo consentito per l&#39;utilizzo non in linea, è necessario sincronizzare nuovamente il documento con la protezione del documento, accedendo online e aprendo un documento protetto tramite criterio oppure utilizzando un comando nell&#39;applicazione client. (Per ulteriori informazioni, vedere *Acrobat Help* o la *Guida delle estensioni Acrobat Reader DC*.)

Se si salva una copia di un documento protetto tramite criterio utilizzando il comando Salva o Salva con nome, il criterio viene applicato e imposto automaticamente per il nuovo documento. Eventi come i tentativi di aprire il nuovo documento vengono anche sottoposti a controllo e registrati per il documento originale.

## Set di criteri {#policy-sets}

*I* set di criteri vengono utilizzati per raggruppare un insieme di criteri che hanno uno scopo commerciale comune. Questi set di criteri vengono quindi resi disponibili a un sottoinsieme di utenti nel sistema.

A ciascun set di criteri possono essere associati uno o più coordinatori di set di criteri. Il coordinatore del set di criteri è un amministratore o un utente che dispone di autorizzazioni aggiuntive. Il *coordinatore del set di criteri* è in genere uno specialista dell&#39;organizzazione che può creare al meglio i criteri in un particolare set di criteri.

I coordinatori dei set di criteri possono eseguire le seguenti attività:

* Creare nuovi criteri
* Modificare ed eliminare qualsiasi criterio nel set di criteri
* Modificare le impostazioni del set di criteri
* Aggiunta e rimozione di coordinatori di set di criteri
* Visualizzare gli eventi dei criteri e dei documenti per qualsiasi criterio o documento all&#39;interno del set di criteri
* Revoca dell&#39;accesso ai documenti
* Cambiare i criteri per il documento.

I set di criteri vengono creati ed eliminati nelle pagine Web dell&#39;amministrazione della protezione dei documenti dagli amministratori e dai coordinatori dei set di criteri che dispongono dell&#39;autorizzazione necessaria.

I set di criteri sono generalmente resi disponibili a un numero limitato di utenti specificando quali utenti o gruppi all&#39;interno di un dominio possono utilizzare i criteri del set di criteri per proteggere i documenti.

Quando è installata la protezione del documento, viene creato un set di criteri predefinito denominato *Set di criteri globali*. L&#39;amministratore che ha installato il software gestisce questo set di criteri.
