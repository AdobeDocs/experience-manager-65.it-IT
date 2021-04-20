---
title: Creazione e gestione dei criteri
seo-title: Creazione e gestione dei criteri
description: Un criterio è un insieme di impostazioni di riservatezza e di utenti che possono accedere a un documento a cui viene applicato il criterio. È possibile creare e gestire diversi tipi di criteri utilizzando AEM moduli.
seo-description: Un criterio è un insieme di impostazioni di riservatezza e di utenti che possono accedere a un documento a cui viene applicato il criterio. È possibile creare e gestire diversi tipi di criteri utilizzando AEM moduli.
uuid: 72be06f3-3e90-495e-8425-72380d95704a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fa054d30-c7dc-4b64-acf1-cbcbe8827df5
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4757'
ht-degree: 0%

---


# Creazione e gestione dei criteri {#creating-and-managing-policies}

Un *criterio* definisce un set di impostazioni di riservatezza e di utenti che possono accedere a un documento a cui viene applicato il criterio. Un *set di criteri* viene utilizzato per raggruppare un set di criteri con uno scopo aziendale comune. Questi set di criteri vengono quindi resi disponibili a un sottoinsieme di utenti nel sistema. Per informazioni dettagliate sui criteri, vedere [Criteri e documenti protetti da policy](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Tipi di criteri {#types-of-policies}

La protezione dei documenti fornisce i seguenti tipi di criteri.

**Politiche personali**

Gli utenti possono creare, modificare, copiare, eliminare e applicare i propri criteri con le impostazioni appropriate per una particolare situazione. Solo la persona che crea un criterio e gli amministratori possono accedere a tale criterio personale. I criteri personali vengono visualizzati nella scheda Criteri personali della pagina Criteri.

Gli utenti invitati possono inoltre creare, modificare, copiare ed eliminare i criteri personali se l’amministratore abilita questa funzionalità.

**Criteri condivisi**

Gli amministratori e i coordinatori dei set di criteri creano criteri condivisi in base ai requisiti di riservatezza identificati dalla tua organizzazione per diversi tipi di documenti e utenti. I criteri condivisi sono contenuti in set di criteri e sono disponibili per tutti gli utenti autorizzati (editori di documenti, coordinatori di set di criteri e destinatari di documenti) per un determinato set di criteri. Gli amministratori e i coordinatori dei set di criteri possono abilitare e disabilitare i criteri condivisi. I criteri condivisi vengono visualizzati nei set di criteri nella scheda Set di criteri della pagina Criteri.

Quando si installa per la prima volta la sicurezza dei documenti, questa contiene un criterio condiviso denominato *Limita a tutti i principali*. Quando questo criterio viene applicato a un documento, tutti gli utenti che possono effettuare l&#39;accesso a tale documento possono accedere al documento. Questo criterio si trova nel set di criteri denominato *Set di criteri globali*. Per impostazione predefinita, questo criterio non è attivato. Puoi abilitarlo se soddisfa le esigenze della tua organizzazione.

**Criteri generati automaticamente da Microsoft Outlook**

Utilizzando Acrobat, è possibile applicare criteri ai documenti inviati come allegati e-mail in Microsoft Outlook. In Outlook è possibile proteggere un documento utilizzando un criterio esistente o un criterio generato automaticamente generato da Acrobat con impostazioni di riservatezza predefinite e applicato al documento allegato a un messaggio e-mail. (Consulta la *[Guida di Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>Affinché un criterio sia disponibile in Outlook, è necessario impostare il criterio come preferito in Acrobat. In Outlook non vengono visualizzati tutti gli altri criteri, compresi quelli in Publisher.

## Chi può creare e gestire policy e set di criteri {#who-can-create-and-manage-policies-and-policy-sets}

Il modo in cui interagisci con i criteri e i set di criteri dipende dal tuo ruolo all’interno dell’organizzazione:

**Utenti:** gli utenti possono creare, modificare ed eliminare i propri criteri personali. Gli utenti invitati possono inoltre creare criteri personali se l’amministratore abilita questa funzionalità.

**Coordinatori set di criteri:** i coordinatori set di criteri possono creare e gestire politiche condivise all&#39;interno dei set di criteri in cui sono designati come coordinatori. Un coordinatore del set di criteri è in genere uno specialista dell’organizzazione che può creare al meglio i criteri in un determinato set di criteri.

**Amministratori:** gli amministratori possono modificare i criteri personali di qualsiasi utente. Possono creare criteri condivisi. Possono inoltre creare, modificare ed eliminare i set di criteri e designare i coordinatori dei set di criteri.

Per informazioni dettagliate sui vari ruoli di protezione dei documenti, vedere [Informazioni sugli utenti della protezione dei documenti](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Creazione e modifica di criteri {#creating-and-editing-policies}

Gli utenti possono creare o modificare i criteri personali per il proprio utilizzo. Gli amministratori e i coordinatori dei set di criteri possono creare o modificare i criteri condivisi per la tua organizzazione.

### Considerazioni sulla modifica dei criteri {#considerations-for-editing-policies}

Quando si modifica un criterio, le modifiche interessano i documenti attualmente protetti dal criterio, nonché i documenti protetti dal criterio in seguito. Ad esempio, se si rimuovono i destinatari da un criterio attualmente applicato a un documento, i destinatari non potranno più aprire il documento.

Lo stato del documento determina quando la modifica ha effetto:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che l&#39;utente non abbia aperto il documento. In questo caso, l&#39;utente deve chiudere il documento per rendere effettive le modifiche.
* Se un destinatario utilizza il documento offline (ad esempio, su un computer portatile), le modifiche avranno effetto alla successiva attivazione del documento online e si sincronizzeranno con la protezione del documento aprendo qualsiasi documento protetto da policy.

>[!NOTE]
>
>I criteri generati automaticamente da Acrobat per i destinatari dei documenti allegati ai messaggi di posta elettronica in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. È possibile visualizzare questi criteri solo aprendo la pagina Dettagli documento del documento associato.

Quando modifichi i criteri, si applicano le seguenti limitazioni:

* Gli utenti invitati possono modificare i criteri solo se l’amministratore abilita questa funzionalità. Se non è possibile modificare i criteri, l’opzione Modifica non sarà disponibile.
* I coordinatori dei set di criteri possono modificare i criteri all&#39;interno dei set di criteri solo se dispongono delle autorizzazioni corrette. L&#39;amministratore del superutente o del set di criteri imposta queste autorizzazioni nell&#39;interfaccia dell&#39;amministratore della protezione dei documenti.
* Se il criterio dispone di una filigrana configurata dall&#39;amministratore e eliminata dopo la creazione del criterio, questa filigrana non verrà più applicata ai documenti se si modifica e si salva il criterio. Le filigrane eliminate rimangono valide solo per i criteri esistenti, purché non vengano modificate. Se si modifica il criterio, è necessario selezionare un&#39;altra filigrana per sostituire quella eliminata.
* Non è possibile concedere l&#39;accesso anonimo a un documento modificando il criterio attualmente applicato. Se si modifica il criterio, gli utenti devono comunque accedere al documento. Per applicare l&#39;accesso anonimo a questo documento, rimuovere prima il criterio nell&#39;applicazione client e quindi applicare un altro criterio che consenta l&#39;accesso anonimo.
* I criteri generati automaticamente da Acrobat per i destinatari di un documento allegato a un messaggio di posta elettronica in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. Per accedere a questo criterio, individuare il documento nella pagina Documenti, aprire la pagina Dettagli documento e fare clic sul nome del criterio nell&#39;elenco dei dettagli del documento.

**Creare o modificare un criterio**

1. Nella pagina Protezione documento fare clic su Criteri e fare clic su una delle seguenti schede:

   * Per creare o modificare un criterio personale, fare clic sulla scheda Criterio personale .
   * Per creare o modificare un criterio condiviso, se disponi dell&#39;autorizzazione, fai clic sulla scheda Set di criteri e fai clic sul nome del set di criteri appropriato, quindi fai clic sulla scheda Criteri .

1. Fare clic su Nuovo oppure selezionare il criterio da modificare dall’elenco.
1. Nella casella Nome digitare un nome che identifichi in modo univoco il criterio. Nella casella Descrizione, descrivere l’attività del criterio e il momento in cui utilizzarlo. Se il criterio si trova all&#39;interno di un set di criteri, il nome e la descrizione vengono visualizzati nell&#39;elenco dei criteri per tutti gli utenti specificati. I criteri personali sono disponibili solo per l’utente e gli amministratori.

   I seguenti caratteri non possono essere utilizzati nel nome o nella descrizione:

   * segno di minore (&lt;)
   * segno maggiore (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra (/)

   Se utilizzi il seguente carattere nel nome o nella descrizione, questi vengono convertiti in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >È possibile creare un nome di criterio contenente caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accenti come &quot;e&quot; e &quot;é&quot; sono considerati uguali. Quando un utente crea un criterio, viene effettuato un confronto per verificare se esiste già un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi uguali, ad eccezione dei caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo non sia stato aggiunto.

1. Aggiungi utenti e gruppi al criterio e imposta le autorizzazioni appropriate. (Consultare [Utenti e gruppi](creating-policies.md#users-and-groups).)
1. In Impostazioni generali, selezionare le opzioni appropriate. (Vedere [Impostazioni generali](creating-policies.md#general-settings).)
1. (Facoltativo) Se applicabile, selezionare un provider di autorizzazioni esterno e specificarne le proprietà. Se non si desidera utilizzare un provider di autorizzazione esterno, fare clic su Rimuovi provider predefinito.

   Un provider di autorizzazioni esterno viene utilizzato per impostare le proprietà all&#39;interno del criterio e, se selezionato, il provider di autorizzazioni esterno utilizza queste informazioni per valutare il criterio. Le proprietà disponibili sono configurate dall&#39;amministratore e dalla persona che installa il software.

1. In Impostazioni avanzate, seleziona le opzioni appropriate. (Vedere [Impostazioni avanzate](creating-policies.md#advanced-settings).)
1. In Impostazioni avanzate non modificabili, selezionare le opzioni appropriate. (Vedere [Impostazioni avanzate non modificabili](creating-policies.md#unchangeable-advanced-settings).)
1. Fai clic su Salva. Il criterio viene visualizzato nell&#39;elenco dei criteri. Accanto al nuovo criterio viene visualizzata un’icona con un cerchio rosso, a indicare che è ancora disattivato.

   Per rendere il criterio disponibile agli utenti, attivalo. (Consultare [Abilitare o disabilitare i criteri condivisi](creating-policies.md#enable-or-disable-shared-policies).)

### Utenti e gruppi {#users-and-groups}

Nell’area Utenti e gruppi è possibile specificare gli utenti che hanno accesso ai documenti protetti dal criterio. Per ogni utente o gruppo specificato, è inoltre possibile impostare i privilegi di utilizzo del documento.

>[!NOTE]
>
>L&#39;autore del documento è l&#39;utente che protegge il documento con il criterio. Questo utente è sempre incluso per impostazione predefinita in un criterio, con diritti di accesso completi, incluse le funzionalità di revoca e di cambio di policy. Tuttavia, gli amministratori possono modificare i diritti di accesso dell’editore del documento per i criteri condivisi. Ad esempio, l’amministratore può impedire all’autore del documento di revocare l’accesso al documento o di cambiare il criterio.

**Aggiungi utente o gruppo:** per aggiungere un utente o un gruppo di utenti, fai clic su Aggiungi utente o gruppo, quindi su Ricerca avanzata per trovare utenti o gruppi. Gli utenti includono gli utenti interni della tua organizzazione e gli utenti invitati che si sono registrati con la sicurezza dei documenti. Quando si seleziona questa opzione, viene visualizzata la pagina Aggiungi utente o gruppo:

* Nella casella Trova digitare il nome utente o il nome del gruppo o l&#39;indirizzo e-mail.
* Nell’elenco Utilizzo, selezionare Nome o E-mail.
* Dall’elenco Tipo, selezionare Utente o Gruppo.
* Selezionare il dominio da cercare dall&#39;elenco In e fare clic su Trova.
* Quando vengono restituiti i risultati, selezionare l&#39;utente o il gruppo da aggiungere e fare clic su Aggiungi.

>[!NOTE]
>
>Se immetti un nome utente o un indirizzo e-mail invitato corretto e non viene restituito alcun risultato, l’utente potrebbe non essersi ancora registrato oppure l’account potrebbe essere eliminato. Puoi provare ad aggiungere l’utente come tipo di utente invitato o contattare l’amministratore.

**Invita nuovo utente:** per aggiungere un utente invitato, fai clic su Invita nuovo utente, digita l’indirizzo e-mail dell’utente nella casella visualizzata e fai clic su Invita. Questa opzione è disponibile solo se l’amministratore l’ha abilitata. Quando aggiungi nuovi utenti invitati a un criterio, la sicurezza del documento invia un messaggio e-mail di invito per la registrazione se gli utenti non sono già invitati a registrarsi. Gli utenti devono utilizzare il collegamento nell’e-mail per creare un account, quindi devono attivare l’account.

Dopo la registrazione, gli utenti invitati possono utilizzare documenti protetti da policy per i quali dispongono dell&#39;autorizzazione. A seconda delle funzionalità abilitate dall&#39;amministratore, gli utenti esterni possono disporre delle autorizzazioni necessarie per applicare i criteri ai documenti, creare, modificare ed eliminare i criteri e aggiungere altri utenti esterni ai criteri.

**Aggiungi utente anonimo:** per consentire l’accesso anonimo, fai clic su Aggiungi utente anonimo. Questa opzione è disponibile solo se l’amministratore ha attivato l’accesso anonimo dell’utente per la sicurezza dei documenti. (Consultare Configurare il server di protezione dei documenti.) Questa opzione consente a tutti l&#39;accesso ai documenti protetti da questo criterio, indipendentemente dal fatto che dispongano o meno di un account di protezione dei documenti. Se selezioni questa opzione, non puoi aggiungere altri tipi di utenti al criterio.

>[!NOTE]
>
>Per consentire l&#39;accesso anonimo a un documento protetto da policy che attualmente non lo possiede, rimuovere la policy esistente e quindi applicare una policy che consenta l&#39;accesso anonimo. Se si cambia o si cambia il criterio esistente, gli utenti devono comunque accedere al documento.

#### Specifica le autorizzazioni del documento per utenti e gruppi {#specify-the-document-permissions-for-users-and-groups}

È possibile specificare le autorizzazioni del documento per un utente o un gruppo alla volta oppure selezionare più utenti e gruppi dall’elenco e modificarne le autorizzazioni utilizzando le opzioni nell’area delle intestazioni di colonna.

Per impostazione predefinita, tutti i documenti protetti da policy dispongono di un&#39;autorizzazione che consente agli utenti di aprirli online.

Nella protezione dei documenti viene visualizzata la scheda Autorizzazioni e opzioni .

Queste autorizzazioni del documento sono disponibili nella scheda Autorizzazioni . È possibile applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office.

**Stampa:** consente all&#39;utente di stampare un documento protetto da questo criterio. Per i file di Office e Pro/E, è possibile selezionare la casella di controllo Stampa per consentire la stampa o cancellarla per impedire la stampa. Se si seleziona la casella di controllo Mostra autorizzazioni personalizzate per PDF, è possibile selezionare una delle seguenti opzioni:

**Non consentito:** l’utente non può stampare il PDF.

**Consentito:** l’utente può stampare il PDF.

**a bassa risoluzione Solo:** L&#39;utente può stampare il PDF a bassa risoluzione.

**Modifica:** consente all&#39;utente di modificare un documento protetto con questo criterio. Per i file di Office e Pro/E, è possibile selezionare la casella di controllo Modifica per consentire le modifiche o cancellarla per impedire le modifiche. Se si seleziona la casella di controllo Mostra autorizzazioni personalizzate per PDF, è possibile selezionare una delle seguenti opzioni:

**Non consentito:** l’utente non può modificare il PDF.

**Qualsiasi:** l’utente può modificare il PDF.

**Collaborazione:** l’utente può collaborare con altri utenti utilizzando le opzioni Collaborazione di Adobe Acrobat. Questa autorizzazione consente all’utente di copiare i dati del modulo anche se l’autorizzazione Copia non è esplicitamente specificata nel criterio.

**Modifica pagine:** l’utente può aggiungere e rimuovere pagine e modificare contenuti nel PDF.

**Fill &amp; Sign:** l’utente può compilare i campi del modulo sul PDF e firmarlo.

**Copia:** consente all’utente di copiare il testo da un documento protetto con questo criterio.

**Reader schermata:** questa autorizzazione viene visualizzata se si seleziona la casella di controllo Mostra autorizzazioni personalizzate per PDF . Quando questa opzione è selezionata, Adobe Acrobat dispone dell’autorizzazione per aggiungere tag temporanei al PDF per migliorarne la leggibilità con un assistente vocale.

Queste autorizzazioni del documento sono disponibili nella scheda Opzioni . È possibile applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office:

**Offline:** consente all&#39;utente di visualizzare un documento offline protetto da questo criterio.

**Validità delle autorizzazioni:** seleziona Autorizzazioni sempre valide o imposta un periodo di validità delle autorizzazioni del documento. Se selezioni un periodo di validità, fai clic sulle icone del calendario per selezionare una data e utilizza le frecce per specificare l’ora in formato 24 ore.

Per i criteri condivisi, gli amministratori possono disattivare i seguenti privilegi per l&#39;autore del documento (l&#39;utente che applica il criterio a un documento):

**Revoca:** consente all’autore del documento di revocare i privilegi di accesso ai documenti.

**Cambia:** consente all&#39;editore del documento di cambiare i privilegi dei criteri.

### Impostazioni generali {#general-settings}

L&#39;area Impostazioni generali contiene le seguenti impostazioni:

**Periodo di validità:** il periodo di tempo durante il quale il documento protetto tramite criterio è accessibile ai destinatari autorizzati. Puoi scegliere tra le seguenti opzioni relative al periodo di validità:

**Il documento non sarà valido dopo:** Il documento è accessibile per il numero specificato di giorni a partire dal momento in cui il documento è stato protetto.

**Il documento non sarà valido dopo questa data:** il documento è valido dalla data in cui il criterio viene applicato al documento fino alla data di fine specificata.

**Valido da, a:** il documento è valido durante le date specificate. Puoi utilizzare il calendario per selezionare una data, se applicabile, facendo clic sull’icona del calendario.

**Il documento è sempre valido:** il periodo di validità del documento non scade.

>[!NOTE]
>
>Le date di validità si basano sul fuso orario del sistema di protezione dei documenti e non sul fuso orario del computer locale.

**Controllo:** abilitare o disabilitare il controllo degli eventi associati a un documento protetto da policy. Ad esempio, la protezione dei documenti può registrare eventi quali tentativi di apertura di un documento. Gli eventi controllati vengono visualizzati nell’elenco della pagina Eventi. Se non si seleziona questa opzione, la protezione dei documenti non registra gli eventi per i documenti associati al criterio.

>[!NOTE]
>
>Affinché la funzione di controllo funzioni correttamente, l’amministratore deve inoltre abilitare il controllo del server nella pagina di configurazione Auditing e Impostazioni privacy .

**Tracciamento esteso dell&#39;utilizzo:** abilitare o disabilitare il tracciamento esteso dell&#39;utilizzo. document security supporta il tracciamento degli eventi utente associati a varie operazioni eseguite su un file PDF. È possibile accedere all’oggetto protezione del documento utilizzando uno script Java. Un clic su un pulsante, un file multimediale in fase di riproduzione o il salvataggio di un file sono alcuni esempi di eventi che possono essere generati da un PDF protetto da policy. È inoltre possibile recuperare le informazioni utente utilizzando l&#39;oggetto di protezione del documento. Il tracciamento degli eventi può essere abilitato dal server di sicurezza dei documenti a livello globale o a livello di policy.

**Periodo di rilascio offline automatica:** il numero massimo di giorni in cui il destinatario può utilizzare il documento protetto dai criteri offline (senza una connessione Internet o di rete attiva). Quando il periodo di leasing scade, il destinatario deve sincronizzare di nuovo il documento per continuare a utilizzarlo.

### Provider di autorizzazioni esterni {#external-authorization-providers}

Se ne hai già configurati alcuni, seleziona i provider di autenticazione esterni. Sono elencati i provider disponibili.

### Impostazioni di autenticazione {#authentication-settings}

È possibile ignorare le impostazioni di autenticazione configurate sul server e specificare le opzioni di autenticazione pertinenti per questo criterio. Selezionare Ignora impostazioni autenticazione globale, quindi selezionare le opzioni di autenticazione pertinenti per questo criterio. Sono disponibili le seguenti opzioni di autenticazione:

**Consenti autenticazione password nome utente:** seleziona questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione nome utente/password quando si connettono al server.

**Consenti autenticazione Kerberos:** selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione Kerberos durante la connessione al server.

**Consenti autenticazione certificato client:** seleziona questa opzione per consentire alle applicazioni client di utilizzare l’autenticazione dei certificati durante la connessione al server.

**Consenti** autenticazione estesaSelezionare per abilitare l&#39;autenticazione estesa. Selezionando questa opzione le applicazioni client possono utilizzare l’autenticazione estesa. L&#39;autenticazione estesa fornisce processi di autenticazione personalizzati e diverse opzioni di autenticazione configurate sul server Document Security

Se sovrascrivi le impostazioni di autenticazione globale, puoi scegliere le opzioni di autenticazione rilevanti per questo criterio. Ad esempio, se sul server erano state abilitate tre opzioni di autenticazione (nome utente e password, certificato client e autenticazione estesa), puoi ignorare tale impostazione globale e selezionare solo l’autenticazione estesa per questo criterio. Assicurati che l’opzione di autenticazione selezionata qui sia già configurata sul server. In questo esempio non è possibile selezionare Kerberos come opzione di autenticazione perché non è configurato sul server.

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

### Impostazioni avanzate {#advanced-settings}

L&#39;area Impostazioni avanzate contiene le seguenti impostazioni:

**Filigrana dinamica:** seleziona una filigrana da visualizzare dinamicamente sulle pagine di un documento (ad esempio, quando un destinatario stampa il documento). Le filigrane dinamiche identificano in modo univoco un documento, contribuendo quindi a garantire la riservatezza del documento e a prevenire le violazioni del diritto d&#39;autore. Ad esempio, l&#39;amministratore può configurare una filigrana dinamica che visualizza la data corrente, il nome utente o l&#39;identificatore della persona che utilizza il documento o il nome del criterio utilizzato per proteggere il documento. Una filigrana può anche visualizzare elementi grafici o di testo personalizzati, se configurati. Gli amministratori configurano le opzioni relative alle filigrane e gli amministratori e gli utenti possono applicarle ai criteri.

(Consultare [Configurare filigrane dinamiche](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Se si sta modificando un criterio e l&#39;amministratore ha eliminato una filigrana configurata selezionata in precedenza per questo criterio, nella pagina Modifica criterio viene visualizzata una nota. In questo caso, se si salva il documento modificato, selezionare una nuova filigrana se si desidera che venga visualizzata sul documento.

>[!NOTE]
>
>Per i criteri che forniscono accesso anonimo agli utenti, il nome utente e l&#39;identificatore di un utente anonimo non vengono visualizzati come filigrana, anche se si seleziona questo tipo di filigrana.

**Usa solo plug-in Acrobat certificati per PDF:** se selezionata per un criterio, questa opzione specifica che Acrobat 8.0 e versioni successive devono essere eseguite in modalità certificata all’apertura di documenti protetti con il criterio. Quando Acrobat viene eseguito in modalità certificata, non carica alcun plug-in di terze parti.

Selezionare questa opzione se si desidera che un destinatario del documento scriva un plug-in in grado di aggirare qualsiasi protezione del documento in Acrobat 8.0 e versioni successive. Non selezionare questa opzione se i destinatari del documento devono utilizzare plug-in di terze parti in Acrobat per interagire con i documenti.

Questa opzione abilita solo la modalità certificata in Acrobat 8.0 o versione successiva; l’amministratore deve disattivare l’accesso per Acrobat 7.0.

(Consultare [Configurare il server di protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server).)

Questa opzione non si applica ad Adobe Reader.

**Messaggio di errore accesso negato:** messaggio visualizzato a chiunque tenti di aprire un documento protetto da policy senza autorizzazione. Questo messaggio viene visualizzato in Acrobat. I client che non possono visualizzare questo messaggio visualizzano un messaggio predefinito per indicare che l’accesso è negato.

### Impostazioni avanzate non modificabili {#unchangeable-advanced-settings}

L&#39;area Impostazioni avanzate non modificabili contiene le seguenti impostazioni. Non è possibile modificare queste impostazioni dopo aver salvato il criterio.

**Algoritmo di cifratura e lunghezza della chiave:**  utilizzato per proteggere i documenti. Puoi scegliere tra le seguenti opzioni:

* AES a 128 bit
* AES a 256 bit. Questa opzione è supportata solo da Acrobat 9.0 e versioni successive. Per utilizzare la crittografia AES 256 per i file PDF, ottieni e installa i file dei criteri di valutazione della forza illimitata dell’estensione Java Cryptography Extension (JCE). Questi file sostituiscono i file local_policy.jar e US_export_policy.jar nella cartella [JAVE_HOME]/lib/security . Ad esempio, se utilizzi Sun JDK 1.6, copia i file scaricati nella cartella [root]/Java/jdk1.6.0_26/lib/security . Puoi scaricare questi file da [Download Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Nessuna crittografia. Questa opzione è attualmente supportata da Acrobat 9.0 e versioni successive. Se si seleziona questa opzione, le opzioni Restrizioni documenti sono disabilitate. Questa opzione può essere utile se si desidera utilizzare la protezione dei documenti per il controllo dei documenti o per il controllo delle versioni, ma non si desidera crittografare il documento.

**Restrizioni documenti:** selezionare i componenti del documento PDF da crittografare. Altre applicazioni client crittografano l’intero documento ma non i file collegati o incorporati. Puoi scegliere tra le seguenti opzioni:

* L&#39;intero documento, compresi i relativi allegati e metadati. ** I metadati forniscono informazioni sul documento e sul relativo contenuto visualizzabili tramite la finestra di dialogo Proprietà documento o il menu Avanzate di Acrobat. In Acrobat è possibile allegare file di tipi diversi (ad esempio file di testo, audio e video) ai documenti PDF.
* Il documento e i relativi allegati, ma non i metadati.
* Solo allegati al documento. È possibile crittografare gli allegati in un file PDF senza crittografare il contenuto del documento.

## Abilita o disabilita i criteri condivisi {#enable-or-disable-shared-policies}

Per rendere disponibile un criterio condiviso, l&#39;amministratore o il coordinatore del set di criteri deve abilitarlo. È possibile abilitare nuovi criteri o criteri precedentemente disabilitati. I criteri condivisi disabilitati vengono comunque applicati per i documenti protetti da tali criteri.

Accanto a un criterio disabilitato viene visualizzata una X rossa.

>[!NOTE]
>
>Gli amministratori non possono disabilitare i criteri personali e gli utenti non possono abilitare e disabilitare i propri criteri.

1. Nella pagina Protezione documento fare clic su Criteri e quindi sulla scheda Set di criteri.
1. Fare clic sul nome del set di criteri appropriato e quindi sulla scheda Criteri.
1. Selezionare la casella di controllo accanto al criterio appropriato, fare clic su Attiva o Disattiva, quindi fare clic su OK.

## Visualizza informazioni su un criterio {#view-information-about-a-policy}

La scheda Criteri personali consente di cercare i criteri personali.

I set di criteri creati dagli amministratori sono elencati nella scheda Set di criteri della pagina Criteri con informazioni sul set di criteri, compreso il nome, la data di creazione e modifica e una descrizione. Fai clic sul nome di un set di criteri per visualizzarne i dettagli. I coordinatori di set di criteri che dispongono dell&#39;autorizzazione per gestire i criteri possono creare criteri condivisi all&#39;interno di un determinato set di criteri.

Quando crei o modifichi un criterio, viene visualizzata una pagina in cui puoi configurare dettagli quali il nome del criterio, i livelli di autorizzazione, le impostazioni di riservatezza e i destinatari da includere nel criterio.

L’amministratore può configurare le seguenti impostazioni di riservatezza per un criterio:

* Opzioni generali sulla riservatezza dei documenti, ad esempio il periodo di validità del documento e il periodo di leasing offline
* Gli utenti autorizzati, nonché le restrizioni e i privilegi del documento per ciascuno di questi utenti
* Opzioni avanzate di riservatezza dei documenti, tra cui filigrane dinamiche e crittografia dei documenti

Gli utenti possono visualizzare i criteri creati e tutti i criteri condivisi a cui hanno accesso. Gli amministratori possono visualizzare tutti i criteri personali e condivisi presenti nella protezione dei documenti.

Puoi visualizzare informazioni più dettagliate su un criterio visualizzato nell’elenco, inclusi gli utenti o i gruppi inclusi nel criterio e le impostazioni di riservatezza specificate per tali utenti.

>[!NOTE]
>
>I criteri generati automaticamente da Acrobat per i destinatari dei documenti allegati ai messaggi di posta elettronica in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. È possibile visualizzare questi criteri solo aprendo la pagina Dettagli documento del documento associato.

1. Nella pagina Protezione documento fare clic su Criteri e quindi sulla scheda Criteri personali.
1. Completa le informazioni di ricerca per cercare le politiche personali.
1. Seleziona il criterio appropriato dall’elenco.
1. Nella pagina Dettagli criterio è possibile visualizzare i dettagli del criterio, modificare il criterio o visualizzare gli eventi relativi al criterio.

## Cerca criteri {#search-for-policies}

Gli amministratori possono cercare i criteri condivisi e quelli personali creati da altri utenti.

1. Per cercare un criterio condiviso, fare clic su Criteri e quindi sulla scheda Set di criteri. Fare clic su un set di criteri nell’elenco, quindi fare clic sulla scheda Criteri.

   Per cercare un criterio personale, nella pagina Protezione documento fare clic su Criteri e quindi sulla scheda Criteri personali.

1. Nell’elenco Trova, selezionare una delle seguenti opzioni:

   **ID criterio:** il numero di identificazione del criterio generato quando l’utente crea il criterio. Devi digitare l&#39;ID criterio esatto.

   **Nome criterio:** il nome del criterio. È possibile cercare parte o tutto il nome del criterio.

1. Nella casella di testo digitare il valore corrispondente. Ad esempio, se hai selezionato Nome criterio, digitare il nome del criterio che stai cercando.
1. Nell&#39;elenco Visualizzazione selezionare il numero di risultati da visualizzare, quindi fare clic su Trova. Vengono visualizzati i risultati della ricerca.
1. (Facoltativo) Per visualizzare i dettagli dei criteri, fare clic sul criterio.

## Copia un criterio {#copy-a-policy}

Puoi copiare un criterio esistente e salvarlo con un nuovo nome e una nuova descrizione. Copiare i criteri è un modo efficiente per creare nuovi criteri utilizzando le impostazioni esistenti.

Gli utenti esterni possono copiare i criteri solo se l’amministratore abilita questa funzionalità. Se non è possibile creare criteri, l&#39;opzione Copia non sarà disponibile.

1. Nella pagina Protezione documento fare clic su Criteri e quindi sulla scheda Criteri personali.
1. Seleziona il criterio appropriato dall’elenco.
1. Nella pagina Dettagli criterio fare clic su Copia.
1. Nella casella Nuovo nome criterio digitare il nuovo nome del criterio. Facoltativamente, digitare una nuova Descrizione.

   I seguenti caratteri non possono essere utilizzati nel nome o nella descrizione:

   * segno di minore (&lt;)
   * segno maggiore (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra (/)

   Se utilizzi il seguente carattere nel nome o nella descrizione, questi vengono convertiti in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >È possibile creare un nome di criterio contenente caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accenti come &quot;e&quot; e &quot;é&quot; sono considerati uguali. Quando un utente crea un criterio, viene effettuato un confronto per verificare se esiste già un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi uguali, ad eccezione dei caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo non sia stato aggiunto.

1. Fai clic su OK.

## Eliminare un criterio {#delete-a-policy}

È possibile eliminare i criteri creati. Gli amministratori possono eliminare i criteri creati da qualsiasi utente. I coordinatori di set di criteri possono eliminare i criteri nei rispettivi set di criteri. I criteri eliminati vengono comunque applicati per i documenti protetti da tali criteri. È possibile eliminare più criteri alla volta.

Gli utenti invitati possono eliminare i criteri solo se l’amministratore abilita questa funzionalità. Se non è possibile eliminare i criteri, l’opzione Elimina non sarà disponibile.

1. Nella pagina Protezione documento fare clic su Criteri.
1. Fare clic sulla scheda Criterio personale.
1. Per eliminare un criterio condiviso, fai clic sulla scheda Set di criteri e fai clic sul nome del set di criteri appropriato.
1. Selezionare la casella di controllo accanto al criterio appropriato e fare clic su Elimina, quindi fare clic su OK.

>[!NOTE]
>
>È necessario utilizzare l&#39;applicazione client per rimuovere i criteri dai documenti. (Consulta la Guida di Acrobat o la Guida delle estensioni Acrobat Reader DC appropriate.)

## Ordina l&#39;elenco dei criteri {#sort-the-policy-list}

È possibile ordinare l’elenco dei criteri in base all’intestazione di colonna per trovare più facilmente i criteri. Un’icona a forma di triangolo accanto all’intestazione della colonna indica quale colonna è attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l&#39;alto indica l&#39;ordine crescente, mentre un triangolo rivolto verso il basso indica l&#39;ordine decrescente.

1. Nella pagina Protezione documento fare clic su Criteri e quindi sulla scheda Set di criteri.
1. Seleziona un set di criteri e fai clic sulla scheda Criteri .
1. Fai clic sull’intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai nuovamente clic sulla colonna .

