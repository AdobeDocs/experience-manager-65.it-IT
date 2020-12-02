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
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '4755'
ht-degree: 0%

---


# Creazione e gestione di criteri {#creating-and-managing-policies}

Un *policy* definisce un insieme di impostazioni per la salvaguardia della riservatezza e consente agli utenti di accedere a un documento a cui viene applicato il criterio. Un *set di criteri* viene utilizzato per raggruppare un insieme di criteri con uno scopo aziendale comune. Questi set di criteri vengono quindi resi disponibili a un sottoinsieme di utenti nel sistema. Per informazioni dettagliate sui criteri, vedere [Criteri e documenti protetti tramite criterio](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Tipi di criteri {#types-of-policies}

Document Security fornisce i seguenti tipi di criteri.

**Criteri personali**

Gli utenti possono creare, modificare, copiare, eliminare e applicare i propri criteri con le impostazioni appropriate per una particolare situazione. Solo la persona che crea un criterio e gli amministratori possono accedere a tale criterio personale. I criteri personali vengono visualizzati nella scheda Criteri personali della pagina Criteri.

Gli utenti invitati possono anche creare, modificare, copiare ed eliminare i criteri personali se l&#39;amministratore lo consente.

**Criteri condivisi**

Gli amministratori e i coordinatori di set di criteri creano criteri condivisi basati sui requisiti di riservatezza identificati dalla vostra organizzazione per diversi tipi di documenti e utenti. I criteri condivisi sono contenuti in set di criteri e sono disponibili per tutti gli utenti autorizzati (editori di documenti, coordinatori di set di criteri e destinatari di documenti) per un set di criteri specifico. Gli amministratori e i coordinatori di set di criteri possono attivare e disattivare i criteri condivisi. I criteri condivisi vengono visualizzati nei set di criteri nella scheda Set criteri della pagina Criteri.

La prima volta che si installa Document Security contiene un criterio condiviso denominato *Limita a tutte le entità*. Quando questo criterio viene applicato a un documento, tutti gli utenti che possono accedere a Document Security possono accedere al documento. Questo criterio si trova nel set di criteri denominato *Set di criteri globali*. Per impostazione predefinita, questo criterio non è attivato. Puoi attivarla se soddisfa le esigenze della tua organizzazione.

**Criteri generati automaticamente da Microsoft Outlook**

Utilizzando  Acrobat, è possibile applicare criteri ai documenti inviati come allegati e-mail in Microsoft Outlook. In Outlook, è possibile proteggere un documento utilizzando un criterio esistente o utilizzando un criterio generato automaticamente che  Acrobat genera con impostazioni predefinite per la salvaguardia della riservatezza e si applica al documento allegato a un messaggio e-mail. (Vedere *[Guida di Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>Affinché un criterio sia disponibile in Outlook, è necessario impostare il criterio come preferito in  Acrobat. Tutti gli altri criteri, inclusi quelli in Publisher, non vengono visualizzati in Outlook.

## Chi può creare e gestire i criteri e i set di criteri {#who-can-create-and-manage-policies-and-policy-sets}

Il modo in cui interagisci con criteri e set di criteri dipende dal tuo ruolo all&#39;interno dell&#39;organizzazione:

**Utenti:** gli utenti possono creare, modificare ed eliminare i propri criteri personali. Gli utenti invitati possono anche creare criteri personali se l’amministratore lo abilita.

**Coordinatori set di criteri:i coordinatori di set di** criteri possono creare e gestire criteri condivisi all&#39;interno dei set di criteri in cui sono designati come coordinatori. Un coordinatore del set di criteri è in genere uno specialista dell&#39;organizzazione che può creare al meglio i criteri in un particolare set di criteri.

**Amministratori:** gli amministratori possono modificare i criteri personali di qualsiasi utente. Possono creare criteri condivisi. Possono inoltre creare, modificare ed eliminare set di criteri e designare coordinatori di set di criteri.

Per informazioni dettagliate sui vari ruoli di protezione dei documenti, vedere [Informazioni sugli utenti della protezione dei documenti](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Creazione e modifica dei criteri {#creating-and-editing-policies}

Gli utenti possono creare o modificare criteri personali per il proprio uso. Gli amministratori e i coordinatori di set di criteri possono creare o modificare i criteri condivisi per l&#39;organizzazione.

### Considerazioni per la modifica dei criteri {#considerations-for-editing-policies}

Quando modificate un criterio, le modifiche interessano i documenti attualmente protetti dal criterio, nonché i documenti protetti dal criterio in seguito. Ad esempio, se rimuovi i destinatari da un criterio attualmente applicato a un documento, i destinatari non potranno più aprire il documento.

Lo stato del documento determina quando la modifica ha effetto:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che l&#39;utente non abbia aperto il documento. In questo caso, per rendere effettive le modifiche, l&#39;utente deve chiudere il documento.
* Se un destinatario utilizza il documento offline (ad esempio, su un computer portatile), le modifiche avranno effetto alla successiva esecuzione del documento online da parte del destinatario e si sincronizzeranno con la protezione dei documenti aprendo qualsiasi documento protetto tramite criterio.

>[!NOTE]
>
>I criteri che  Acrobat genera automaticamente per i destinatari dei documenti allegati ai messaggi e-mail in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. Per visualizzare questi criteri è necessario aprire la pagina Dettagli documento relativa al documento associato.

Quando modificate i criteri, si applicano le seguenti limitazioni:

* Gli utenti invitati possono modificare i criteri solo se l&#39;amministratore lo abilita. Se non è possibile modificare i criteri, l&#39;opzione Modifica non sarà disponibile.
* I coordinatori di set di criteri possono modificare i criteri all&#39;interno dei set di criteri solo se dispongono delle autorizzazioni corrette. L&#39;amministratore di super utente o set di criteri imposta queste autorizzazioni nell&#39;interfaccia dell&#39;amministratore di Document Security.
* Se nel criterio è configurata una filigrana che l&#39;amministratore ha eliminato dopo la creazione del criterio, questa filigrana non verrà più applicata ai documenti se modificate e salvate il criterio. Le filigrane eliminate restano valide solo per i criteri esistenti, purché non vengano modificate. Se modificate il criterio, dovete selezionare un&#39;altra filigrana in sostituzione di quella eliminata.
* Non è possibile concedere l&#39;accesso anonimo a un documento modificando il criterio attualmente applicato. Se modificate il criterio, gli utenti devono comunque accedere al documento. Per applicare l&#39;accesso anonimo a questo documento, rimuovere prima il criterio nell&#39;applicazione client e quindi applicare un altro criterio che consenta l&#39;accesso anonimo.
* I criteri che  Acrobat genera automaticamente per i destinatari di un documento allegato a un messaggio e-mail in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. Per accedere a questo criterio, individuare il documento nella pagina Documenti, aprire la pagina Dettagli documento e fare clic sul nome del criterio nell&#39;elenco dei dettagli del documento.

**Creare o modificare un criterio**

1. Nella pagina Protezione documento, fare clic su Criteri e quindi su una delle seguenti schede:

   * Per creare o modificare un criterio personale, fate clic sulla scheda Criterio personale.
   * Per creare o modificare un criterio condiviso, se disponete dell&#39;autorizzazione, fate clic sulla scheda Set criteri, quindi sul nome del set di criteri appropriato, quindi sulla scheda Criteri.

1. Fate clic su Nuovo oppure selezionate dall&#39;elenco il criterio da modificare.
1. Nella casella Nome, digitate un nome che identifichi in modo univoco il criterio. Nella casella Descrizione, descrivere le operazioni eseguite dal criterio e quando utilizzarlo. Se il criterio si trova all&#39;interno di un set di criteri, il nome e la descrizione vengono visualizzati nell&#39;elenco dei criteri per tutti gli utenti specificati. I criteri personali sono disponibili solo per gli utenti e gli amministratori.

   I seguenti caratteri non possono essere utilizzati nel nome o nella descrizione:

   * segno minore di (&lt;)
   * segno maggiore (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra (/)

   Se usate il seguente carattere nel nome o nella descrizione, questi vengono convertiti in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >Potete creare un nome di criterio che contenga caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come &quot;e&quot; e &quot;é&quot; sono considerati uguali. Quando un utente crea un criterio, viene effettuato un confronto per verificare se esiste già un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi identici tranne che per i caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo non sia stato aggiunto.

1. Aggiungete utenti e gruppi al criterio e impostate le autorizzazioni appropriate. (Vedere [Utenti e gruppi](creating-policies.md#users-and-groups).)
1. In Impostazioni generali, selezionate le opzioni appropriate. (Vedere [Impostazioni generali](creating-policies.md#general-settings).)
1. (Facoltativo) Se applicabile, selezionate un provider di autorizzazione esterno e specificatene le proprietà. Se non desiderate utilizzare un provider di autorizzazione esterno, fate clic su Rimuovi provider predefinito.

   Un provider di autorizzazione esterno viene utilizzato per impostare le proprietà all&#39;interno del criterio e, se selezionato, il provider di autorizzazione esterno utilizza queste informazioni per valutare il criterio. Le proprietà disponibili sono configurate dall&#39;amministratore e dalla persona che installa il software.

1. In Impostazioni avanzate, selezionate le opzioni appropriate. (Vedere [Impostazioni avanzate](creating-policies.md#advanced-settings).)
1. In Impostazioni avanzate non modificabili, selezionare le opzioni appropriate. (Vedere [Impostazioni avanzate non modificabili](creating-policies.md#unchangeable-advanced-settings).)
1. Fai clic su Salva. Il criterio viene visualizzato nell&#39;elenco dei criteri. Accanto al nuovo criterio viene visualizzata un&#39;icona con un cerchio rosso a indicare che è ancora disattivato.

   Per rendere il criterio disponibile agli utenti, attivatelo. (Vedere [Attivare o disattivare i criteri condivisi](creating-policies.md#enable-or-disable-shared-policies).)

### Utenti e gruppi {#users-and-groups}

Nell&#39;area Utenti e gruppi, specificate gli utenti che hanno accesso ai documenti protetti tramite il criterio. Per ogni utente o gruppo specificato, potete anche impostare i privilegi di utilizzo del documento.

>[!NOTE]
>
>L&#39;autore del documento è l&#39;utente che protegge il documento con il criterio. Questo utente è sempre incluso per impostazione predefinita in un criterio, con diritti di accesso completi, incluse le funzionalità di revoca e di commutazione dei criteri. Tuttavia, gli amministratori possono modificare i diritti di accesso dell&#39;editore del documento per i criteri condivisi. Ad esempio, l&#39;amministratore può impedire all&#39;autore del documento di revocare l&#39;accesso al documento o di cambiare criterio.

**Aggiungi utente o gruppo:** per aggiungere un utente o un gruppo di utenti, fai clic su Aggiungi utente o gruppo, quindi su Ricerca avanzata per trovare utenti o gruppi. Gli utenti includono gli utenti interni della tua organizzazione e gli utenti invitati che si sono registrati con Document Security. Quando selezionate questa opzione, viene visualizzata la pagina Aggiungi utente o Gruppo:

* Nella casella Trova, digitate il nome utente o del gruppo o l’indirizzo e-mail.
* Nell&#39;elenco Uso, selezionare Nome o E-mail.
* Nell&#39;elenco Tipo, selezionare Utente o Gruppo.
* Selezionare il dominio di cui si desidera eseguire la ricerca dall&#39;elenco In e fare clic su Trova.
* Quando i risultati vengono restituiti, selezionate l’utente o il gruppo da aggiungere e fate clic su Aggiungi.

>[!NOTE]
>
>Se immettete un nome utente o un indirizzo e-mail invitato corretto e non viene restituito alcun risultato, l’utente potrebbe non essersi ancora registrato oppure l’account potrebbe essere eliminato. Potete provare ad aggiungere l’utente come tipo di utente invitato o contattare l’amministratore.

**Invita nuovo utente:** per aggiungere un utente invitato, fate clic su Invita nuovo utente, digitate l’indirizzo e-mail dell’utente nella casella visualizzata e fate clic su Invita. Questa opzione è disponibile solo se è stata abilitata dall&#39;amministratore. Quando aggiungete nuovi utenti invitati a un criterio, Document Security invia un messaggio e-mail di invito per la registrazione se gli utenti non sono già invitati a registrarsi. Gli utenti devono utilizzare il collegamento presente nell&#39;e-mail per creare un account, quindi devono attivare l&#39;account.

Dopo la registrazione, gli utenti invitati possono utilizzare i documenti protetti tramite criterio per i quali dispongono dell&#39;autorizzazione. A seconda delle funzionalità abilitate dall&#39;amministratore, gli utenti esterni possono disporre dell&#39;autorizzazione per applicare criteri ai documenti, creare, modificare ed eliminare criteri e aggiungere altri utenti esterni ai criteri.

**Aggiungi utente anonimo:** per consentire l’accesso anonimo, fai clic su Aggiungi utente anonimo. Questa opzione è disponibile solo se l&#39;amministratore ha attivato l&#39;accesso anonimo per la protezione dei documenti. (vedere Configurare il server di protezione dei documenti.) Questa opzione consente a tutti di accedere ai documenti protetti da questo criterio, indipendentemente dal fatto che possiedano un account di protezione documento. Se selezionate questa opzione, non potete aggiungere altri tipi di utenti al criterio.

>[!NOTE]
>
>Per consentire l&#39;accesso anonimo a un documento protetto tramite criterio che al momento non lo contiene, rimuovere il criterio esistente e applicare un criterio che consenta l&#39;accesso anonimo. Se cambiate o modificate il criterio esistente, gli utenti dovranno comunque accedere al documento.

#### Specificare le autorizzazioni del documento per utenti e gruppi {#specify-the-document-permissions-for-users-and-groups}

Potete specificare le autorizzazioni per un utente o un gruppo alla volta oppure selezionare più utenti e gruppi dall&#39;elenco e modificarne le autorizzazioni utilizzando le opzioni nell&#39;area delle intestazioni di colonna.

Per impostazione predefinita, tutti i documenti protetti tramite criterio dispongono di un&#39;autorizzazione che consente agli utenti di aprirli mentre sono online.

La scheda Autorizzazioni e opzioni viene visualizzata nella protezione del documento.

Queste autorizzazioni del documento sono disponibili nella scheda Autorizzazioni. Potete applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office.

**Stampa:** consente all&#39;utente di stampare un documento protetto tramite questo criterio. Per i file di Office e Pro/E, potete selezionare la casella di controllo Stampa per consentire la stampa oppure deselezionare la casella per impedire la stampa. Se selezionate la casella di controllo Mostra autorizzazioni personalizzate per PDF, potete selezionare una delle seguenti opzioni:

**Non consentito:** all&#39;utente non è consentito stampare il PDF.

**Consentita: l&#39;** utente può stampare il PDF.

**A bassa risoluzione. only:** L&#39;utente può stampare il PDF a bassa risoluzione.

**Modifica:** consente all&#39;utente di modificare un documento protetto tramite questo criterio. Per i file di Office e Pro/E, potete selezionare la casella di controllo Modifica per consentire le modifiche, oppure cancellarla per impedire le modifiche. Se selezionate la casella di controllo Mostra autorizzazioni personalizzate per PDF, potete selezionare una delle seguenti opzioni:

**Non consentito:** all&#39;utente non è consentito modificare il PDF.

**Qualsiasi:** l’utente può modificare il PDF.

**Collaborazione:** l&#39;utente può collaborare con altri utenti, utilizzando le opzioni Collaborazione in  Adobe Acrobat. Questa autorizzazione consente all&#39;utente di copiare i dati del modulo anche se l&#39;autorizzazione Copia non è specificata esplicitamente nel criterio.

**Modifica pagine:** l’utente può aggiungere e rimuovere pagine e modificare contenuti nel PDF.

**Fill &amp; Sign:** L&#39;utente può compilare i campi del modulo sul PDF e firmarlo.

**Copia:** consente all&#39;utente di copiare il testo da un documento protetto tramite questo criterio.

**Reader dello schermo:** questa autorizzazione viene visualizzata se selezionate la casella di controllo Mostra autorizzazioni personalizzate per PDF. Quando questa opzione è selezionata,  Adobe Acrobat dispone dell&#39;autorizzazione per aggiungere tag temporanei al PDF per migliorarne la leggibilità con un assistente vocale.

Tali autorizzazioni del documento sono disponibili nella scheda Opzioni. Potete applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office:

**Offline:** consente all&#39;utente di visualizzare offline un documento protetto con questo criterio.

**Validità delle autorizzazioni:** selezionate Autorizzazioni sempre valide o impostate un periodo di validità delle autorizzazioni del documento. Se si seleziona un periodo di validità, fare clic sulle icone del calendario per selezionare una data e utilizzare le frecce per specificare l&#39;ora in formato 24 ore.

Per i criteri condivisi, gli amministratori possono disattivare i seguenti privilegi per l&#39;autore del documento (l&#39;utente che applica il criterio a un documento):

**Revoca:** consente all&#39;autore del documento di revocare i privilegi di accesso al documento.

**Cambia:** consente all&#39;autore del documento di cambiare i privilegi dei criteri.

### Impostazioni generali {#general-settings}

L&#39;area Impostazioni generali contiene le seguenti impostazioni:

**Periodo di validità:** il periodo di tempo durante il quale il documento protetto tramite criterio è accessibile ai destinatari autorizzati. È possibile scegliere tra le seguenti opzioni per il periodo di validità:

**Il documento non sarà valido dopo:** Il documento è accessibile per il numero specificato di giorni a partire dal momento in cui è stato protetto il documento.

**Il documento non sarà valido dopo questa data:** Il documento è valido dalla data in cui il criterio viene applicato al documento fino alla data di fine specificata.

**Valido da, a:** Il documento è valido per le date specificate. Potete utilizzare il calendario per selezionare una data, se applicabile, facendo clic sull&#39;icona del calendario.

**Il documento è sempre valido:** il periodo di validità del documento non scade.

>[!NOTE]
>
>Le date di validità si basano sul fuso orario del sistema di protezione dei documenti, non sul fuso orario del computer locale.

**Controllo:** abilitare o disabilitare il controllo degli eventi associati a un documento protetto tramite criterio. Ad esempio, Document Security può registrare eventi quali tentativi di apertura di un documento. Gli eventi controllati vengono visualizzati nell’elenco nella pagina Eventi. Se non si seleziona questa opzione, Document Security non registra eventi per i documenti associati al criterio.

>[!NOTE]
>
>Affinché la funzione di controllo funzioni correttamente, l’amministratore deve inoltre abilitare il controllo del server nella pagina di configurazione Auditing e Privacy Settings.

**Tracciamento utilizzo esteso:** attivare o disattivare il tracciamento dell’uso esteso. document security supporta il tracciamento degli eventi utente associati a varie operazioni eseguite su un file PDF. È possibile accedere all&#39;oggetto document security utilizzando uno script Java. Un clic su un pulsante, un file multimediale riprodotto o il salvataggio di un file sono alcuni esempi di eventi che possono essere attivati da un PDF protetto tramite criterio. Utilizzando l&#39;oggetto Document Security è inoltre possibile recuperare le informazioni utente. Il tracciamento degli eventi può essere abilitato dal server di protezione dei documenti a livello globale o a livello di criterio.

**Periodo di locazione automatico non in linea:** il numero massimo di giorni in cui il destinatario può utilizzare il documento protetto tramite criterio offline (senza una connessione di rete o Internet attiva). Alla scadenza del periodo consentito, il destinatario deve sincronizzare di nuovo il documento per continuare a utilizzarlo.

### Fornitori di autorizzazioni esterne {#external-authorization-providers}

Se ne avete già configurato uno, selezionate i provider di autenticazione esterni. Sono elencati i fornitori disponibili.

### Impostazioni di autenticazione {#authentication-settings}

È possibile ignorare le impostazioni di autenticazione configurate sul server e specificare le opzioni di autenticazione pertinenti per questo criterio. Selezionate Ignora impostazioni autenticazione globale, quindi selezionate le opzioni di autenticazione pertinenti per questo criterio. Sono disponibili le seguenti opzioni di autenticazione:

**Consenti autenticazione password nome utente:** selezionate questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione nome utente/password quando si connette al server.

**Consenti autenticazione Kerberos:** selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione Kerberos durante la connessione al server.

**Consenti autenticazione certificato client:** selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione basata sui certificati durante la connessione al server.

**Consenti** autenticazione estesa: consente di abilitare l&#39;autenticazione estesa. Selezionando questa opzione, le applicazioni client possono utilizzare l&#39;autenticazione estesa. L&#39;autenticazione estesa fornisce processi di autenticazione personalizzati e diverse opzioni di autenticazione configurate sul server di Document Security

Se sovrascrivete le impostazioni di autenticazione globali, potete scegliere le opzioni di autenticazione pertinenti per questo criterio. Ad esempio, se sul server erano state abilitate tre opzioni di autenticazione (nome utente e password, certificato client e autenticazione estesa), potete ignorare tale impostazione globale e selezionare solo l&#39;autenticazione estesa per questo criterio. È necessario assicurarsi che l&#39;opzione di autenticazione selezionata qui sia già configurata sul server. In questo esempio, non è possibile selezionare Kerberos come opzione di autenticazione perché non è configurato sul server.

>[!NOTE]
>
>L&#39;autenticazione estesa è supportata su Apple Mac OS X con  versione 11.0.6 e successiva di Adobe Acrobat.

### Impostazioni avanzate {#advanced-settings}

L’area Impostazioni avanzate contiene le seguenti impostazioni:

**Filigrana dinamica:** selezionare una filigrana da visualizzare dinamicamente sulle pagine di un documento (ad esempio, quando il destinatario stampa il documento). Le filigrane dinamiche identificano in modo univoco un documento, contribuendo in tal modo a garantire la riservatezza del documento e a prevenire la violazione del copyright. Ad esempio, l&#39;amministratore può configurare una filigrana dinamica che visualizzi la data corrente, il nome utente o l&#39;identificatore della persona che utilizza il documento o il nome del criterio utilizzato per proteggere il documento. Una filigrana può anche visualizzare testo o elementi grafici personalizzati, se configurati. Gli amministratori configurano le opzioni relative alle filigrane e gli amministratori e gli utenti possono applicarle ai criteri.

(Vedere [Configurare le filigrane dinamiche](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Se modificate un criterio e l&#39;amministratore ha eliminato una filigrana configurata precedentemente selezionata per il criterio, nella pagina Modifica criterio viene visualizzata una nota. In questo caso, se state salvando il documento modificato, selezionate una nuova filigrana se desiderate che venga visualizzata sul documento.

>[!NOTE]
>
>Per i criteri che forniscono l&#39;accesso anonimo agli utenti, il nome utente e l&#39;identificatore di un utente anonimo non vengono visualizzati come filigrane anche se si seleziona questo tipo di filigrana.

**Usa solo plug-in Acrobat certificati  per PDF:** se è selezionata per un criterio, questa opzione specifica che  Acrobat 8.0 e versioni successive deve essere eseguito in modalità certificata all&#39;apertura di documenti protetti tramite criterio. Se  Acrobat viene eseguito in modalità certificata, non verrà caricato alcun plug-in di terze parti.

Selezionare questa opzione se si desidera che un destinatario del documento scriva un plug-in che possa aggirare le protezioni del documento in  Acrobat 8.0 e versioni successive. Non selezionate questa opzione se i destinatari del documento devono utilizzare plug-in di terze parti in  Acrobat per interagire con i documenti.

Questa opzione attiva solo la modalità certificata in  Acrobat 8.0 o versioni successive; l&#39;amministratore deve disattivare l&#39;accesso per  Acrobat 7.0.

(Vedere [Configurare il server di protezione dei documenti](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server).)

Questa opzione non si applica a  Adobe Reader.

**Messaggio di errore di accesso negato:** messaggio che viene visualizzato a chiunque tenti di aprire un documento protetto tramite criterio senza autorizzazione. Questo messaggio viene visualizzato in  Acrobat. I client che non possono visualizzare questo messaggio visualizzano un messaggio predefinito per indicare che l&#39;accesso è negato.

### Impostazioni avanzate immutabili {#unchangeable-advanced-settings}

L&#39;area Impostazioni avanzate non modificabili contiene le seguenti impostazioni. Non potete modificare queste impostazioni dopo aver salvato il criterio.

**Algoritmo di cifratura e lunghezza chiave:** utilizzato per proteggere i documenti. Potete scegliere tra le seguenti opzioni:

* AES a 128 bit
* AES a 256 bit. Questa opzione è supportata solo  Acrobat 9.0 e versioni successive. Per utilizzare la cifratura AES 256 per i file PDF, è necessario ottenere e installare i file JCE (Java Cryptography Extension) Unlimited Strense Jurisdizione Policy. Questi file sostituiscono i file local_policy.jar e US_export_policy.jar nella cartella [JAVE_HOME]/lib/security. Ad esempio, se utilizzate Sun JDK 1.6, copiate i file scaricati nella cartella [dep root]/Java/jdk1.6.0_26/lib/security. Potete scaricare questi file da [Download Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Nessuna crittografia.  Acrobat 9.0 e versioni successive supportano attualmente questa opzione. Se si seleziona questa opzione, le opzioni Limitazioni documento sono disattivate. Questa opzione può essere utile se si desidera utilizzare la protezione dei documenti per il controllo dei documenti o per il controllo delle versioni, ma non per cifrare il documento.

**Limitazioni del documento:** selezionare i componenti del documento PDF da cifrare. Altre applicazioni client crittografano l&#39;intero documento ma non i file collegati o incorporati. Potete scegliere tra le seguenti opzioni:

* L’intero documento, inclusi gli allegati e i metadati. *I* metadati contengono informazioni sul documento e sul relativo contenuto che è possibile visualizzare tramite la finestra di dialogo Proprietà documento o il menu  Acrobat Advanced. In  Acrobat, è possibile allegare file di tipi diversi (ad esempio, file di testo, audio e video) ai documenti PDF.
* Il documento e i relativi allegati, ma non i metadati.
* Solo allegati del documento. È possibile cifrare gli allegati a un file PDF senza cifrare il contenuto del documento.

## Abilitare o disabilitare i criteri condivisi {#enable-or-disable-shared-policies}

Per rendere disponibile un criterio condiviso, l&#39;amministratore o il coordinatore del set di criteri deve attivarlo. È possibile abilitare nuovi criteri o criteri precedentemente disabilitati. Un criterio condiviso disattivato viene comunque applicato ai documenti protetti tramite tale criterio.

Accanto a un criterio disabilitato viene visualizzata una X rossa.

>[!NOTE]
>
>Gli amministratori non possono disattivare i criteri personali e gli utenti non possono attivare e disattivare i propri criteri.

1. Nella pagina Protezione documento, fare clic su Criteri, quindi fare clic sulla scheda Set di criteri.
1. Fate clic sul nome del set di criteri appropriato e fate clic sulla scheda Criteri.
1. Selezionate la casella di controllo accanto al criterio appropriato, fate clic su Attiva o Disattiva, quindi su OK.

## Visualizzazione delle informazioni su un criterio {#view-information-about-a-policy}

La scheda Criteri personali consente di effettuare ricerche nei criteri personali.

I set di criteri creati dagli amministratori sono elencati nella scheda Set di criteri della pagina Criteri con informazioni sul set di criteri, incluso il nome, la data di creazione e modifica e una descrizione. Fate clic sul nome di un set di criteri per visualizzarne i dettagli. I coordinatori di set di criteri che dispongono dell&#39;autorizzazione per gestire i criteri possono creare criteri condivisi all&#39;interno di un set di criteri specifico.

Quando create o modificate un criterio, viene visualizzata una pagina in cui potete configurare dettagli quali il nome del criterio, i livelli di autorizzazione, le impostazioni per la salvaguardia della riservatezza e i destinatari da includere nel criterio.

L&#39;amministratore può configurare le seguenti impostazioni di riservatezza per un criterio:

* Opzioni generali per la riservatezza dei documenti, ad esempio il periodo di validità del documento e il periodo di tempo consentito per la pubblicazione offline
* Gli utenti autorizzati, nonché le restrizioni e i privilegi del documento per ciascuno di questi utenti
* Opzioni avanzate per la salvaguardia della riservatezza dei documenti, comprese filigrane dinamiche e cifratura dei documenti

Gli utenti possono visualizzare i criteri creati e tutti i criteri condivisi a cui hanno accesso. Gli amministratori possono visualizzare tutti i criteri personali e condivisi presenti nella protezione dei documenti.

Potete visualizzare informazioni più dettagliate su un criterio visualizzato nell&#39;elenco, compresi gli utenti o i gruppi inclusi nel criterio e le impostazioni di riservatezza specificate per tali utenti.

>[!NOTE]
>
>I criteri che  Acrobat genera automaticamente per i destinatari dei documenti allegati ai messaggi e-mail in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. Per visualizzare questi criteri è necessario aprire la pagina Dettagli documento relativa al documento associato.

1. Nella pagina Protezione documento, fare clic su Criteri e quindi sulla scheda Criteri personali.
1. Compila le informazioni di ricerca per cercare le politiche personali.
1. Selezionare il criterio appropriato dall&#39;elenco.
1. Nella pagina Dettagli criterio potete visualizzare i dettagli relativi al criterio, modificare il criterio o visualizzare gli eventi relativi al criterio.

## Cerca criteri {#search-for-policies}

Gli amministratori possono cercare criteri condivisi e criteri personali creati da altri utenti.

1. Per cercare un criterio condiviso, fate clic su Criteri e quindi sulla scheda Set criteri. Fare clic su un set di criteri nell&#39;elenco, quindi fare clic sulla scheda Criteri.

   Per cercare un criterio personale, nella pagina Protezione documento fare clic su Criteri e quindi sulla scheda Criteri personali.

1. Nell&#39;elenco Trova, selezionare una delle seguenti opzioni:

   **ID criterio:** il numero di identificazione del criterio generato al momento della creazione del criterio da parte dell&#39;utente. È necessario digitare l&#39;ID esatto del criterio.

   **Nome criterio:** il nome del criterio. Potete cercare parte o tutto il nome del criterio.

1. Nella casella di testo, digitare il valore corrispondente. Ad esempio, se hai selezionato Nome criterio, digita il nome del criterio che stai cercando.
1. Nell&#39;elenco Visualizza, selezionare il numero di risultati da visualizzare, quindi fare clic su Trova. Vengono visualizzati i risultati della ricerca.
1. (Facoltativo) Per visualizzare i dettagli del criterio, fate clic su di esso.

## Copiare un criterio {#copy-a-policy}

Potete copiare un criterio esistente e salvarlo con un nuovo nome e una nuova descrizione. Copiare i criteri è un modo efficiente per creare nuovi criteri utilizzando le impostazioni esistenti.

Gli utenti esterni possono copiare i criteri solo se l&#39;amministratore ne abilita la funzionalità. Se non potete creare criteri, l&#39;opzione Copia non sarà disponibile.

1. Nella pagina Protezione documento, fare clic su Criteri e quindi sulla scheda Criteri personali.
1. Selezionare il criterio appropriato dall&#39;elenco.
1. Nella pagina Dettagli criterio, fate clic su Copia.
1. Nella casella Nuovo nome criterio, digitate il nuovo nome del criterio. Facoltativamente, digitare una nuova Descrizione.

   I seguenti caratteri non possono essere utilizzati nel nome o nella descrizione:

   * segno minore di (&lt;)
   * segno maggiore (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra (/)

   Se usate il seguente carattere nel nome o nella descrizione, questi vengono convertiti in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >Potete creare un nome di criterio che contenga caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come &quot;e&quot; e &quot;é&quot; sono considerati uguali. Quando un utente crea un criterio, viene effettuato un confronto per verificare se esiste già un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi identici tranne che per i caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo non sia stato aggiunto.

1. Fai clic su OK.

## Eliminare un criterio {#delete-a-policy}

È possibile eliminare i criteri creati. Gli amministratori possono eliminare i criteri creati da qualsiasi utente. I coordinatori di set di criteri possono eliminare i criteri nei relativi set di criteri. Un criterio eliminato viene comunque applicato ai documenti protetti tramite tale criterio. Potete eliminare più criteri alla volta.

Gli utenti invitati possono eliminare i criteri solo se l&#39;amministratore lo abilita. Se non è possibile eliminare i criteri, l&#39;opzione di eliminazione non sarà disponibile.

1. Nella pagina di protezione del documento, fare clic su Criteri.
1. Fate clic sulla scheda Criterio personale.
1. Per eliminare un criterio condiviso, fate clic sulla scheda Set criteri e fate clic sul nome del set di criteri appropriato.
1. Selezionate la casella di controllo accanto al criterio appropriato e fate clic su Elimina, quindi su OK.

>[!NOTE]
>
>È necessario utilizzare l&#39;applicazione client per rimuovere i criteri dai documenti. (vedere  Guida di Acrobat o la Guida delle estensioni Acrobat Reader DC appropriata).

## Ordinare l&#39;elenco dei criteri {#sort-the-policy-list}

Potete ordinare l&#39;elenco dei criteri per intestazione di colonna per individuare più facilmente i criteri. Un&#39;icona a forma di triangolo accanto all&#39;intestazione della colonna indica quale colonna è attualmente utilizzata per ordinare. Un triangolo rivolto verso l’alto indica l’ordine crescente, mentre un triangolo rivolto verso il basso indica l’ordine decrescente.

1. Nella pagina Protezione documento, fare clic su Criteri e fare clic sulla scheda Set criteri.
1. Selezionate un set di criteri, quindi fate clic sulla scheda Criteri.
1. Fare clic sull&#39;intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fate di nuovo clic sulla colonna.

