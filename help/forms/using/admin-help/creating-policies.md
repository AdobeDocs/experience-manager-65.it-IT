---
title: Creare e gestire i criteri
description: Un criterio è un insieme di impostazioni di riservatezza e di utenti che possono accedere a un documento a cui il criterio stesso viene applicato. Puoi creare e gestire vari tipi di criteri utilizzando AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 5e57451c-1a89-442c-8404-841e95d5ceff
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '4725'
ht-degree: 100%

---

# Creare e gestire i criteri {#creating-and-managing-policies}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Un *criterio* definisce un set di impostazioni di riservatezza e gli utenti che possono accedere a un documento al quale viene applicato il criterio stesso. Un *set di criteri* viene utilizzato per raggruppare un insieme di criteri che hanno lo stesso scopo operativo. Questi set di criteri vengono quindi resi disponibili a un sottoinsieme di utenti nel sistema. Per informazioni dettagliate sui criteri, consulta [Criteri e documenti protetti tramite i criteri](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Tipi di criteri {#types-of-policies}

Per la protezione dei documenti sono disponibili i seguenti tipi di criteri.

**Criteri personali**

Gli utenti possono creare, modificare, copiare, eliminare e applicare i propri criteri con le impostazioni appropriate per una situazione specifica. Solo l’utente che ha creato un criterio e l’amministratore possono accedere al criterio personale. I criteri personali vengono visualizzati nella scheda Criteri personali della pagina Criteri.

Anche gli utenti invitati possono creare, modificare, copiare ed eliminare criteri personali, se l’amministratore abilita questa funzionalità.

**Criteri condivisi**

Gli amministratori e i coordinatori di set di criteri creano criteri condivisi in base ai requisiti di riservatezza identificati dalll’organizzazione per i diversi tipi di documenti e utenti. I criteri condivisi sono contenuti in set di criteri e sono disponibili per tutti gli utenti autorizzati di un determinato set di criteri (autori di documenti, coordinatori di set di criteri e destinatari di documenti). Gli amministratori e i coordinatori di set di criteri possono abilitare e disabilitare i criteri condivisi. I criteri condivisi vengono visualizzati nei set di criteri nella scheda Set di criteri della pagina Criteri.

Alla prima installazione, la protezione dei documenti contiene un solo criterio condiviso, denominato *Limita a tutte le entità principali*. Quando questo criterio viene applicato a un documento, qualsiasi utente che può accedere a Protezione dei documenti può accedere anche al documento. Questo criterio si trova nel set di criteri denominato *Set di criteri globale*. Per impostazione predefinita, questo criterio non è abilitato. Puoi abilitarlo se è adatto alle esigenze della tua organizzazione.

**Criteri generati automaticamente da Microsoft® Outlook**

Con Acrobat puoi applicare criteri ai documenti che invii come allegati e-mail in Microsoft® Outlook. In Outlook puoi proteggere un documento utilizzando un criterio esistente. In alternativa, puoi utilizzare un criterio che Acrobat genera automaticamente con impostazioni di riservatezza predefinite e applica al documento allegato a un messaggio e-mail. Consulta la *[Guida di Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*.

>[!NOTE]
>
>Perché un criterio sia disponibile in Outlook, devi impostarlo come preferito in Acrobat. Tutti gli altri criteri, inclusi quelli di cui sei l’editore, non vengono visualizzati in Outlook.

## Chi può creare e gestire i criteri e i set di criteri {#who-can-create-and-manage-policies-and-policy-sets}

La modalità di interazione con i criteri e i set di criteri dipende dal tuo ruolo all’interno dell’organizzazione:

**Utenti:** gli utenti possono creare, modificare ed eliminare i propri criteri personali. Anche gli utenti invitati possono creare criteri personali, se l’amministratore abilita questa funzionalità.

**Coordinatori di set di criteri:** i coordinatori di set di criteri possono creare e gestire i criteri condivisi all’interno dei set di criteri per i quali sono designati come coordinatori. Un coordinatore di set di criteri è in genere uno specialista dell’organizzazione che può creare al meglio i criteri appartenenti a un set di criteri specifico.

**Amministratori:** gli amministratori possono modificare i criteri personali di qualsiasi utente. Possono creare criteri condivisi. Possono inoltre creare, modificare ed eliminare i set di criteri e designare i coordinatori dei set di criteri.

Per informazioni dettagliate sui vari ruoli di protezione dei documenti, consulta [Informazioni sugli utenti del sistema di protezione dei documenti](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Creare e modificare criteri {#creating-and-editing-policies}

Gli utenti possono creare o modificare i criteri personali per l’utilizzo personale. Gli amministratori e i coordinatori di set di criteri possono creare o modificare i criteri condivisi per l’organizzazione.

### Considerazioni sulla modifica dei criteri {#considerations-for-editing-policies}

Quando modifichi un criterio, le modifiche hanno effetto sui documenti protetti attualmente dal criterio e su quelli che verranno protetti in seguito dal criterio stesso. Se, ad esempio, rimuovi i destinatari da un criterio applicato a un documento, i destinatari non potranno più aprire il documento.

Lo stato del documento determina quando la modifica ha effetto:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che il documento non sia aperto dall’utente. In questo caso, l’utente deve chiudere il documento per rendere effettive le modifiche.
* Se un destinatario utilizza il documento in modalità offline, ad esempio in un computer laptop, le modifiche diventeranno effettive la volta successiva in cui il destinatario caricherà il documento online. Si sincronizza quindi con la protezione dei documenti aprendo qualsiasi documento protetto tramite criteri.

>[!NOTE]
>
>I criteri generati automaticamente da Acrobat per i destinatari dei documenti allegati ai messaggi e-mail in Microsoft® Outlook non vengono visualizzati nell’elenco dei criteri. Puoi visualizzare questi criteri solo aprendo la pagina Dettagli documento relativa al documento associato.

Durante la modifica dei criteri, si applicano le seguenti restrizioni:

* Gli utenti invitati possono modificare i criteri solo se l’amministratore abilita questa funzionalità. Se non puoi modificare i criteri, l’opzione Modifica non è disponibile.
* I coordinatori dei set di criteri possono modificare i criteri all’interno dei set di criteri solo se dispongono delle autorizzazioni corrette. L’utente privilegiato o l’amministratore di un set di criteri imposta queste autorizzazioni nell’interfaccia di amministrazione della protezione dei documenti.
* Se il criterio ha una filigrana configurata che l’amministratore ha eliminato dopo la creazione del criterio, questa filigrana non verrà più applicata ai documenti se modifichi e salvi il criterio. Le filigrane eliminate rimangono attive solo per i criteri esistenti finché non modifichi il criterio. Se modifichi il criterio, devi selezionare un’altra filigrana per sostituire quella eliminata.
* Non puoi concedere l’accesso anonimo a un documento modificando il criterio applicato. Se modifichi il criterio, gli utenti devono comunque effettuare l’accesso per accedere al documento. Per applicare l’accesso anonimo a questo documento, rimuovi innanzitutto il criterio nell’applicazione client e, quindi, applica un altro criterio che consenta l’accesso anonimo.
* I criteri generati automaticamente da Acrobat per i destinatari di un documento allegato a un messaggio e-mail in Microsoft Outlook non vengono visualizzati nell’elenco dei criteri. Per accedere a questo criterio, individua il documento nella pagina Documenti, apri la pagina Dettagli documento e fai clic sul nome del criterio nell’elenco dei dettagli del documento.

**Creare o modificare un criterio**

1. Nella pagina di Protezione dei documenti, fai clic su Criteri e, quindi, su una delle seguenti schede:

   * Per creare o modificare un criterio personale, fai clic sulla scheda Criterio personale.
   * Per creare o modificare un criterio condiviso, se disponi dell’autorizzazione, fai clic sulla scheda Set di criteri, quindi sul nome del set di criteri appropriato e, infine, sulla scheda Criteri.

1. Fai clic su Nuovo o seleziona il criterio da modificare dall’elenco.
1. Nella casella Nome digita un nome che identifica in modo univoco il criterio. Nella casella Descrizione, descrivi le funzioni del criterio e quando utilizzarlo. Se il criterio si trova all’interno di un set di criteri, il nome e la descrizione vengono visualizzati nell’elenco dei criteri per tutti gli utenti specificati. I criteri personali sono disponibili solo per l’utente e gli amministratori.

   Impossibile utilizzare i seguenti caratteri nel nome o nella descrizione:

   * segno minore di (&lt;)
   * segno maggiore di (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra obliqua (/)

   Se nel nome o nella descrizione è stato utilizzato il carattere seguente, sarà convertito in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >Puoi creare il nome di un criterio che contenga caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come “e” ed “é” vengono considerati uguali. Quando un utente crea un criterio, viene eseguito un confronto per verificare se esiste un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi che sono uguali se si eccettuano i caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo criterio non sia stato aggiunto.

1. Aggiungi utenti e gruppi al criterio e imposta le autorizzazioni appropriate. (Consulta [Utenti e gruppi](creating-policies.md#users-and-groups).)
1. In Impostazioni generali, seleziona le opzioni appropriate. (Consulta [Impostazioni generali](creating-policies.md#general-settings).)
1. (Facoltativo) Se applicabile, seleziona un provider di autorizzazione esterno e specifica le sue proprietà. Se non vuoi utilizzare un provider di autorizzazione esterno, fai clic su Rimuovi provider predefinito.

   Un provider di autorizzazione esterno viene utilizzato per impostare le proprietà all’interno del criterio e, se selezionato, tal provider utilizza queste informazioni per valutare il criterio. Le proprietà disponibili vengono configurate dall’amministratore e dal responsabile dell’installazione del software.

1. In Impostazioni avanzate, seleziona le opzioni appropriate. Consulta [Impostazioni avanzate](creating-policies.md#advanced-settings).
1. In Impostazioni avanzate non modificabili seleziona le opzioni appropriate. Consulta [Impostazioni avanzate non modificabili](creating-policies.md#unchangeable-advanced-settings).
1. Fai clic su Salva. Il criterio viene visualizzato nell’elenco dei criteri. Accanto al nuovo criterio viene visualizzata un’icona con un cerchio rosso, a indicare che il criterio è ancora disattivato.

   Per rendere il criterio disponibile agli utenti, abilitalo. Consulta [Abilitare o disabilitare i criteri condivisi](creating-policies.md#enable-or-disable-shared-policies).

### Utenti e gruppi {#users-and-groups}

Nell’area Utenti e gruppi specifica gli utenti che hanno accesso ai documenti protetti con il criterio. Per ogni utente o gruppo che specifichi, puoi anche impostare i privilegi di utilizzo dei documenti.

>[!NOTE]
>
>L’editore del documento è l’utente che protegge il documento con il criterio. Questo utente viene sempre incluso per impostazione predefinita in un criterio, con diritti di accesso completi, incluse le funzionalità di revoca e cambio di criterio. Tuttavia, gli amministratori possono modificare i diritti di accesso dell’editore del documento per i criteri condivisi. Ad esempio, l’amministratore può impedire all’editore del documento di revocare l’accesso al documento o di cambiare il criterio.

**Aggiungi utente o gruppo:** per aggiungere un utente o un gruppo di utenti, fai clic su Aggiungi utente o gruppo e quindi su Ricerca avanzata per trovare gli utenti o i gruppi. Gli utenti includono gli utenti interni dell’organizzazione e gli utenti invitati che si sono registrati con la protezione dei documenti. Quando selezioni questa opzione, viene visualizzata la pagina Aggiungi utente o gruppo:

* Nella casella Trova digita il nome o l’indirizzo e-mail dell’utente o del gruppo.
* Nell’elenco Utilizzo, seleziona Nome o E-mail.
* Nell’elenco Tipo seleziona Utente o Gruppo.
* Seleziona nell’elenco il dominio in cui eseguire la ricerca e fai clic su Trova.
* Quando vengono restituiti i risultati, seleziona l’utente o il gruppo da aggiungere e fai clic su Aggiungi.

>[!NOTE]
>
>Se immetti il nome o l’indirizzo e-mail corretto di un utente invitato e non viene restituito alcun risultato, è possibile che l’utente non si sia ancora registrato o che l’account sia stato eliminato. Puoi provare ad aggiungere l’utente come tipo di utente invitato o contattare l’amministratore.

**Invita nuovo utente:** per aggiungere un utente invitato, fai clic su Invita nuovo utente, digita l’indirizzo e-mail dell’utente nella casella visualizzata e fai clic su Invita. Questa opzione è disponibile solo se è stata abilitata dall’amministratore. Quando aggiungi nuovi utenti invitati a un criterio, la protezione dei documenti invia un’e-mail di invito alla registrazione, se gli utenti non sono già stati invitati a registrarsi. Gli utenti devono utilizzare il collegamento nell’e-mail per creare un account, quindi devono attivare l’account.

Dopo la registrazione, gli utenti invitati possono utilizzare i documenti protetti tramite criteri per i quali dispongono dell’autorizzazione. A seconda delle funzionalità abilitate dall’amministratore, gli utenti esterni possono disporre dell’autorizzazione per applicare criteri ai documenti, creare, modificare ed eliminare criteri e aggiungere altri utenti esterni ai criteri.

**Aggiungi utente anonimo:** per consentire l’accesso utente anonimo, fai clic su Aggiungi utente anonimo. Questa opzione è disponibile solo se l’amministratore ha abilitato l’accesso anonimo degli utenti per la protezione dei documenti. Consulta Configurare il server di protezione dei documenti. Questa opzione consente a tutti l’accesso ai documenti protetti da questo criteri, sia che dispongano o meno di un account di protezione dei documenti. Se selezioni questa opzione, non puoi aggiungere altri tipi di utenti al criterio.

>[!NOTE]
>
>Per consentire l’accesso anonimo a un documento protetto tramite criteri che al momento non dispone di tale accesso, rimuovi il criterio esistente e quindi applica un criterio che consenta l’accesso anonimo. Se cambia o modifichi il criterio esistente, gli utenti devono comunque effettuare l’accesso per poter accedere al documento.

#### Specificare le autorizzazioni del documento per utenti e gruppi {#specify-the-document-permissions-for-users-and-groups}

Puoi specificare le autorizzazioni del documento per un utente o un gruppo alla volta, oppure selezionare più utenti e gruppi nell’elenco e modificarne le autorizzazioni utilizzando le opzioni disponibili nell’area delle intestazioni di colonna.

Per impostazione predefinita, tutti i documenti protetti tramite criteri dispongono di un’autorizzazione che consente agli utenti di aprirli mentre sono online.

La scheda Autorizzazioni e opzioni viene visualizzata in Protezione dei documenti.

Queste autorizzazioni per i documenti sono disponibili nella scheda Autorizzazioni. Puoi applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office.

**Stampa:** consente all’utente di stampare un documento protetto con questo criterio. Per i file di Office e Pro/E, puoi selezionare la casella di controllo Stampa per consentire la stampa oppure deselezionarla per impedire la stampa. Se selezioni la casella di controllo Mostra autorizzazioni personalizzate per PDF, puoi selezionare una delle opzioni seguenti:

**Non consentito:** l’utente non può stampare il PDF.

**Consentito:** l’utente è autorizzato a stampare il PDF.

**Solo risoluzione bassa:** l’utente è autorizzato a stampare il PDF a bassa risoluzione.

**Modifica:** consente all’utente di modificare un documento protetto con questo criterio. Per i file di Office e Pro/E, puoi selezionare la casella di controllo Modifica per consentire di apportare le modifiche o deselezionarla per impedirlo. Se selezioni la casella di controllo Mostra autorizzazioni personalizzate per PDF, puoi selezionare una delle opzioni seguenti:

**Non consentito:** l’utente non può modificare il PDF.

**Qualsiasi modifica consentita:** l’utente può modificare il PDF.

**Collabora:** l’utente può collaborare con altri utenti utilizzando le opzioni Collabora in Adobe Acrobat. Questa autorizzazione consente all’utente di copiare i dati del modulo anche se l’autorizzazione Copia non è specificata in modo esplicito nel criterio.

**Modifica pagine:** l’utente può aggiungere e rimuovere pagine e modificare contenuto in PDF.

**Riempi e firma:** l’utente può compilare i campi del modulo in PDF e firmarlo.

**Copia:** consente all’utente di copiare testo da un documento protetto con questo criterio.

**Lettura dello schermo:** questa autorizzazione viene visualizzata se selezioni la casella di controllo Mostra autorizzazioni personalizzate per PDF. Quando questa opzione è selezionata, Adobe Acrobat dispone dell’autorizzazione per aggiungere tag temporanei a PDF al fine di migliorarne la leggibilità con un’utilità per la lettura dello schermo.

Queste autorizzazioni per i documenti sono disponibili nella scheda Opzioni. Puoi applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office:

**Offline:** consente all’utente di visualizzare un documento non in linea protetto con questi criteri.

**Validità autorizzazioni:** imposta che le autorizzazioni sono sempre valide o seleziona un periodo di validità delle autorizzazioni del documento. Se selezioni un periodo di validità, fai clic sull’icona del calendario per selezionare una data e utilizza le frecce per specificare l’ora nel formato a 24 ore.

Per i criteri condivisi, gli amministratori possono disabilitare i seguenti privilegi per l’editore del documento (l’utente che applica i criteri a un documento):

**Revoca:** consente all’autore del documento di revocare i privilegi di accesso al documento.

**Opzione:** consente all’autore del documento di cambiare i privilegi dei criteri.

### Impostazioni generali {#general-settings}

L’area Impostazioni generali contiene le impostazioni seguenti:

**Periodo di validità:** il periodo di tempo durante il quale il documento protetto tramite criteri è accessibile ai destinatari autorizzati. Puoi scegliere tra le seguenti opzioni del periodo di validità:

**Il documento non sarà valido dopo:** il documento è accessibile per il numero di giorni specificato a partire dal momento in cui è stato protetto.

**Il documento non sarà valido dopo questa data:** il documento è valido dalla data in cui il criterio viene applicato al documento fino alla data di fine specificata.

**Valido da, a:** il documento è valido nelle date specificate. Puoi utilizzare il calendario per selezionare una data, se applicabile, facendo clic sull’icona del calendario.

**Documento sempre valido:** il periodo di validità del documento non scade.

>[!NOTE]
>
>Le date di validità dipendono dal fuso orario del sistema di protezione dei documenti e non dal fuso orario del computer locale.

**Controllo:** attiva o disattiva l’auditing degli eventi associati a un documento protetto tramite policy. La protezione dei documenti, ad esempio, può registrare eventi quali i tentativi di aprire un documento. Gli eventi controllati tramite auditing vengono visualizzati nell’elenco della pagina Eventi. Se non selezioni questa opzione, la protezione dei documenti non registra gli eventi per i documenti associati ai criteri.

>[!NOTE]
>
>Affinché l’auditing funzioni, l’amministratore deve inoltre abilitare l’auditing del server nella pagina di configurazione delle impostazioni di controllo e privacy.

**Tracciamento utilizzo esteso:** abilita o disabilita il tracciamento dell’utilizzo esteso. La protezione dei documenti supporta il tracciamento degli eventi utente associati a varie operazioni eseguite su un file PDF. Puoi accedere all’oggetto di protezione dei documenti utilizzando uno script Java. Un clic sul pulsante, un file multimediale in fase di riproduzione o il salvataggio di un file sono alcuni esempi di eventi generati da un PDF protetto tramite criteri. L’oggetto di protezione dei documenti consente inoltre di recuperare informazioni sull’utente. Il tracciamento degli eventi può essere abilitato dal server di protezione dei documenti a livello globale o a livello di criteri.

**Periodo di lease per la modalità offline automatica:** il numero massimo di giorni in cui il destinatario può utilizzare il documento protetto tramite criteri in modalità offline (senza una connessione Internet o di rete attiva). Alla scadenza del periodo di lease, il destinatario deve sincronizzare nuovamente il documento per continuare a utilizzarlo.

### Provider di autorizzazioni esterni {#external-authorization-providers}

Se ne hai già configurato uno, seleziona i provider di autenticazione esterni. Vengono elencati i provider disponibili.

### Impostazioni di autenticazione {#authentication-settings}

Puoi ignorare le impostazioni di autenticazione configurate nel server e specificare le opzioni di autenticazione pertinenti per questo criterio. Seleziona Ignora impostazioni di autenticazione globali, quindi seleziona le opzioni di autenticazione pertinenti per questo criterio. Sono disponibili le seguenti opzioni di autenticazione:

**Consenti autenticazione con password e nome utente:** seleziona questa opzione se desideri consentire alle applicazioni client di utilizzare l’autenticazione con nome utente/password durante la connessione al server.

**Consenti autenticazione Kerberos:** seleziona questa opzione se desideri consentire alle applicazioni client di utilizzare l’autenticazione Kerberos durante la connessione al server.

**Consenti autenticazione tramite certificato client:** seleziona questa opzione se desideri consentire alle applicazioni client di utilizzare l’autenticazione tramite certificato durante la connessione al server.

**Consenti autenticazione estesa:** seleziona questa opzione per abilitare l’autenticazione estesa. Se selezioni questa opzione, le applicazioni client potranno utilizzare l’autenticazione estesa. L’autenticazione estesa permette di personalizzare i processi di autenticazione e configurare diverse opzioni di autenticazione sul server di protezione dei documenti.

Se ignori le impostazioni di autenticazione globale, puoi scegliere le opzioni di autenticazione pertinenti per questo criterio. Ad esempio, se hai attivato tre opzioni di autenticazione (nome utente e password, certificato client e autenticazione estesa) sul server, puoi ignorare tale impostazione globale e selezionare solo autenticazione estesa per questo criterio. Verifica che l’opzione di autenticazione selezionata qui sia già configurata sul server. In questo esempio non puoi selezionare Kerberos come opzione di autenticazione perché non è configurata nel server.

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

### Impostazioni avanzate {#advanced-settings}

L’area Impostazioni avanzate contiene le impostazioni seguenti:

**Filigrana dinamica:** seleziona una filigrana da visualizzare in modo dinamico sulle pagine di un documento, ad esempio quando il documento viene stampato da un destinatario. Le filigrane dinamiche identificano in modo univoco un documento, contribuendo in tal modo a garantirne la riservatezza e a impedire le violazioni del copyright. Ad esempio, l’amministratore può configurare una filigrana dinamica che visualizza la data corrente, il nome utente o l’identificatore della persona che utilizza il documento. Oppure il nome del criterio utilizzato per proteggere il documento. Se configurata, una filigrana può anche visualizzare testo o elementi grafici personalizzati. Gli amministratori possono configurare le opzioni delle filigrane e gli amministratori e gli utenti possono applicarle ai criteri.

(Consulta [Configurare le filigrane dinamiche](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Se stai modificando un criterio e l’amministratore ha eliminato una filigrana configurata che hai precedentemente selezionato per questo criterio, nella pagina Modifica criterio verrà visualizzata una nota. In questo caso, se stai salvando il documento modificato, seleziona una nuova filigrana se desideri visualizzarne una nel documento.

>[!NOTE]
>
>Per i criteri che forniscono un accesso anonimo, il nome utente e l’identificatore di un utente anonimo non vengono visualizzati come filigrana anche se selezioni questo tipo di filigrana.

**Usa solo plug-in Acrobat certificati per PDF:** se selezionata per un criterio, questa opzione specifica che Acrobat 8.0 e versioni successive devono essere eseguiti in modalità certificata all’apertura dei documenti protetti con il criterio. Quando Acrobat viene eseguito in modalità certificata, non carica plug-in di terze parti.

Seleziona questa opzione se temi che un destinatario del documento possa scrivere un plug-in che potrebbe eludere le protezioni del documento in Acrobat 8.0 e versioni successive. Non selezionare questa opzione se i destinatari del documento devono utilizzare plug-in di terze parti in Acrobat per interagire con i documenti.

Questa opzione abilita solo la modalità certificata in Acrobat 8.0 o versioni successive; l’amministratore deve disabilitare l’accesso per Acrobat 7.0.

(Consulta [Configurare il server di protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server).)

Questa opzione non si applica ad Adobe Reader.

**Messaggio di errore Accesso negato:** messaggio visualizzato a chiunque tenti di aprire un documento protetto tramite criterio senza autorizzazione. Questo messaggio viene visualizzato in Acrobat. I client che non possono visualizzare questo messaggio visualizzano un messaggio predefinito per indicare che l’accesso è negato.

### Impostazioni avanzate non modificabili {#unchangeable-advanced-settings}

L’area Impostazioni avanzate non modificabili contiene le impostazioni seguenti. Non puoi modificare queste impostazioni dopo aver salvato il criterio.

**Algoritmo di crittografia e lunghezza chiave:** utilizzati per proteggere i documenti. Puoi scegliere tra le seguenti opzioni:

* AES a 128 bit
* AES a 256 bit. Solo Acrobat 9.0 e versioni successive supportano questa opzione. Per utilizzare la crittografia AES 256 per i file PDF, è necessario ottenere e installare i file Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Questi file sostituiscono i file local_policy.jar e US_export_policy.jar nella cartella [JAVE_HOME]/lib/security. Ad esempio, se utilizzi Sun JDK 1.6, copia i file scaricati nella cartella [dep root]/Java/jdk1.6.0_26/lib/security. Puoi scaricare questi file da [Download Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Nessuna crittografia. Al momento Acrobat 9.0 e versioni successive supportano questa opzione. Se selezioni questa opzione, le opzioni Restrizioni documenti vengono disattivate. Questa opzione può essere utile se desideri utilizzare la protezione dei documenti per l’auditing dei documenti o il controllo delle versioni, ma non desideri crittografare il documento.

**Restrizioni documenti:** seleziona i componenti del documento PDF da crittografare. Altre applicazioni client crittografano l’intero documento ma non i file collegati o incorporati. Puoi scegliere tra le seguenti opzioni:

* L’intero documento, inclusi gli allegati e i metadati. I *metadati* sono informazioni sul documento e sul relativo contenuto che puoi visualizzare tramite la finestra di dialogo Proprietà del documento o il menu Avanzate di Acrobat. In Acrobat puoi allegare ai documenti PDF file di diverso tipo (ad esempio, file di testo, audio e video).
* Il documento e i relativi allegati, ma non i metadati.
* Solo gli allegati del documento. Puoi crittografare gli allegati in un file PDF senza crittografare il contenuto del documento.

## Abilitare o disabilitare i criteri condivisi {#enable-or-disable-shared-policies}

Per rendere disponibile un criterio condiviso, questo deve essere attivato dall’amministratore o dal coordinatore del set di criteri. Puoi abilitare nuovi criteri o criteri precedentemente disabilitati. Un criterio condiviso che hai disabilitato viene comunque applicato ai documenti protetti con quel criterio.

Accanto a un criterio disabilitato viene visualizzata una X rossa.

>[!NOTE]
>
>Gli amministratori non possono disattivare i criteri personali e gli utenti non possono abilitare e disabilitare i propri criteri.

1. Nella pagina relativa alla protezione dei documenti fai clic su Criteri, quindi sulla scheda Set di criteri.
1. Fai clic sul nome del set di criteri appropriato, quindi sulla scheda Criteri.
1. Seleziona la casella di controllo accanto al criterio appropriato, fai clic su Attiva o Disattiva, quindi su OK.

## Visualizzare informazioni su un criterio {#view-information-about-a-policy}

Utilizzando la scheda Criteri personali, puoi effettuare ricerche nei criteri personali.

I set di criteri creati dagli amministratori sono elencati nella scheda Set di criteri della pagina Criteri. Contengono informazioni sul set di criteri, tra cui il nome, la data di creazione e di modifica e una descrizione. Fai clic sul nome di un set di criteri per visualizzarne i dettagli. I coordinatori dei set di criteri che dispongono dell’autorizzazione per gestire i criteri possono creare criteri condivisi all’interno di un determinato set di criteri.

Quando crei o modifichi un criterio, viene visualizzata una pagina in cui puoi configurare il nome del criterio, i livelli di autorizzazione, le impostazioni di riservatezza e i destinatari da includere nel criterio.

L’amministratore può configurare le seguenti impostazioni di riservatezza per un criterio:

* Opzioni generali di riservatezza dei documenti, ad esempio il periodo di validità del documento e il periodo di lease offline
* Gli utenti autorizzati e le restrizioni e i privilegi del documento per ciascuno di tali utenti
* Opzioni avanzate di riservatezza del documento, incluse filigrane dinamiche e crittografia del documento

Gli utenti possono visualizzare i criteri creati e tutti i criteri condivisi a cui hanno accesso. Gli amministratori possono visualizzare tutti i criteri condivisi e personali inclusi nella protezione dei documenti.

Puoi visualizzare informazioni più dettagliate su un criterio visualizzato nell’elenco, tra cui gli utenti o i gruppi inclusi nel criterio e le impostazioni di riservatezza specifiche per tali utenti.

>[!NOTE]
>
>I criteri generati automaticamente da Acrobat per i destinatari dei documenti allegati ai messaggi di posta elettronica in Microsoft Outlook non vengono visualizzati nell’elenco dei criteri. Puoi visualizzare questi criteri solo aprendo la pagina Dettagli documento relativa al documento associato.

1. Nella pagina Protezione dei documenti, fai clic su Criteri, quindi fai clic sulla scheda Criteri personali.
1. Completa le informazioni di ricerca per poter cercare i criteri personali.
1. Seleziona il criterio appropriato tra quelli in elenco.
1. Nella pagina Dettagli criterio puoi visualizzare i dettagli del criterio, modificarlo o visualizzare gli eventi correlati a quel criterio.

## Cercare i criteri {#search-for-policies}

Gli amministratori possono cercare i criteri condivisi e i criteri personali creati da altri utenti.

1. Per cercare un criterio condiviso, fai clic su Criteri, quindi sulla scheda Set di criteri. Fai clic su un set di criteri tra quelli in elenco, quindi sulla scheda Criteri.

   Per cercare un criterio personale, nella pagina Protezione dei documenti fai clic su Criteri, quindi fai clic sulla scheda Criteri personali.

1. Nell&#39;elenco Trova seleziona una delle opzioni seguenti:

   **ID criterio:** il numero di identificazione del criterio generato quando l’utente crea un criterio. Digita l’ID esatto del criterio.

   **Nome criterio:** il nome del criterio. Puoi cercare parte del nome del criterio o il nome intero.

1. Nella casella di testo digita il valore corrispondente. Se, ad esempio, hai selezionato Nome criterio, digita il nome del criterio che desideri cercare.
1. Nell&#39;elenco Visualizza seleziona il numero di risultati da visualizzare, quindi fai clic su Trova. Vengono visualizzati i risultati della ricerca.
1. (Facoltativo) Per visualizzare i dettagli di un criterio, fai clic sul criterio.

## Copiare un criterio {#copy-a-policy}

Puoi copiare un criterio esistente e salvarlo con un nuovo nome e una nuova descrizione. Copiare i criteri è un modo efficiente per creare i criteri utilizzando le impostazioni esistenti.

Gli utenti esterni possono copiare i criteri solo se l’amministratore abilita questa funzionalità. Se non puoi creare i criteri, l’opzione Copia non è disponibile.

1. Nella pagina Protezione dei documenti, fai clic su Criteri, quindi fai clic sulla scheda Criteri personali.
1. Seleziona il criterio appropriato tra quelli in elenco.
1. Nella pagina Dettagli criterio, fai clic su Copia.
1. Nella casella Nuovo nome criterio digita il nuovo nome del criterio. Puoi eventualmente inserire una nuova descrizione.

   Impossibile utilizzare i seguenti caratteri nel nome o nella descrizione:

   * segno minore di (&lt;)
   * segno maggiore di (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra obliqua (/)

   Se nel nome o nella descrizione è stato utilizzato il carattere seguente, sarà convertito in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >Puoi creare il nome di un criterio che contenga caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come “e” ed “é” vengono considerati uguali. Quando un utente crea un criterio, viene eseguito un confronto per verificare se esiste un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi che sono uguali se si eccettuano i caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo criterio non sia stato aggiunto.

1. Fai clic su OK.

## Eliminare un criterio {#delete-a-policy}

Puoi eliminare i criteri che hai creato. Gli amministratori possono eliminare i criteri creati da qualsiasi utente. I coordinatori dei set di criteri possono eliminare i criteri nei propri set di criteri. Se elimini un criterio, questo viene comunque applicato ai documenti protetti con tale criterio. Puoi eliminare più criteri alla volta.

Gli utenti invitati possono eliminare i criteri solo se l’amministratore abilita questa funzionalità. Se non puoi eliminare i criteri, l’opzione Elimina non è disponibile.

1. Nella pagina Protezione dei documenti, fai clic su Criteri.
1. Fai clic sulla scheda Criteri personali.
1. Per eliminare un criterio condiviso, fai clic sulla scheda Set di criteri e seleziona il nome del set di criteri appropriato.
1. Seleziona la casella di controllo accanto al criterio appropriato e fai clic su Elimina, quindi fai clic su OK.

>[!NOTE]
>
>Utilizza l’applicazione client per rimuovere i criteri dai documenti. (Consulta la Guida di Acrobat o la Guida alle estensioni di Acrobat Reader DC appropriata.)

## Ordinare l’elenco dei criteri {#sort-the-policy-list}

Per trovare i criteri in modo più facile, puoi ordinare l’elenco dei criteri in base all’intestazione della colonna. Un’icona a forma di triangolo accanto all’intestazione della colonna indica la colonna attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l’alto indica un ordine crescente, mentre un triangolo rivolto verso il basso indica un ordine decrescente.

1. Nella pagina relativa alla protezione dei documenti, fai clic su Criteri, quindi sulla scheda Set di criteri.
1. Seleziona un set di criteri, quindi fai clic sulla scheda Criteri.
1. Fai clic sull’intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai di nuovo clic sulla colonna.
