---
title: Creazione e gestione delle policy
seo-title: Creating and managing policies
description: Una policy è un insieme di impostazioni di riservatezza e di utenti che possono accedere a un documento a cui viene applicata. Puoi creare e gestire vari tipi di criteri utilizzando i moduli AEM.
seo-description: A policy is a set of confidentiality settings and users who can access a document to which the policy is applied. You can create and manage various types of policies using AEM forms.
uuid: 72be06f3-3e90-495e-8425-72380d95704a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fa054d30-c7dc-4b64-acf1-cbcbe8827df5
feature: Document Security
exl-id: 5e57451c-1a89-442c-8404-841e95d5ceff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4718'
ht-degree: 0%

---

# Creazione e gestione delle policy {#creating-and-managing-policies}

A *policy* definisce un set di impostazioni di riservatezza e gli utenti che possono accedere a un documento a cui viene applicata la policy. A *set di criteri* viene utilizzato per raggruppare un insieme di criteri con uno scopo aziendale comune. Questi set di criteri vengono quindi resi disponibili a un sottoinsieme di utenti nel sistema. Per informazioni dettagliate sui criteri, consulta [Criteri e documenti protetti tramite policy](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents).

## Tipi di criteri {#types-of-policies}

La protezione dei documenti offre i seguenti tipi di criteri.

**Politiche personali**

Gli utenti possono creare, modificare, copiare, eliminare e applicare i propri criteri con le impostazioni appropriate per una particolare situazione. Solo la persona che crea una policy e gli amministratori possono accedere a tale policy personale. I criteri personali vengono visualizzati nella scheda Criteri personali della pagina Criteri.

Gli utenti invitati possono anche creare, modificare, copiare ed eliminare policy personali, se l’amministratore abilita questa funzionalità.

**Criteri condivisi**

Gli amministratori e i coordinatori di set di policy creano policy condivise in base ai requisiti di riservatezza identificati dalla propria organizzazione per i diversi tipi di documenti e utenti. I criteri condivisi sono contenuti all’interno di set di criteri e sono disponibili per tutti gli utenti autorizzati (autori di documenti, coordinatori di set di criteri e destinatari di documenti) per un determinato set di criteri. Gli amministratori e i coordinatori di set di criteri possono abilitare e disabilitare i criteri condivisi. I criteri condivisi vengono visualizzati nei set di criteri nella scheda Set di criteri della pagina Criteri.

La prima volta che installi Document Security, contiene un criterio condiviso, denominato *Limita a tutte le entità*. Quando questa policy viene applicata a un documento, qualsiasi utente che può accedere a document security può accedere al documento. Questo criterio si trova nel set di criteri denominato *Set di criteri globale*. Per impostazione predefinita, questo criterio non è abilitato. Puoi abilitarlo se soddisfa le esigenze della tua organizzazione.

**Criteri generati automaticamente in Microsoft Outlook**

Con Acrobat è possibile applicare policy ai documenti inviati come allegati e-mail in Microsoft Outlook. In Outlook è possibile proteggere un documento utilizzando una policy esistente oppure una policy generata automaticamente che Acrobat genera con le impostazioni di riservatezza predefinite e applica al documento allegato a un messaggio di posta elettronica. (vedere *[Guida di Acrobat](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*.)

>[!NOTE]
>
>Affinché un criterio sia disponibile in Outlook, è necessario impostarlo come preferito in Acrobat. Tutti gli altri criteri, inclusi quelli relativi al server di pubblicazione, non vengono visualizzati in Outlook.

## Chi può creare e gestire policy e set di policy {#who-can-create-and-manage-policies-and-policy-sets}

Il modo in cui si interagisce con i criteri e i set di criteri dipende dal proprio ruolo all’interno dell’organizzazione:

**Utenti:** Gli utenti possono creare, modificare ed eliminare i propri criteri personali. Gli utenti invitati possono anche creare criteri personali, se l’amministratore abilita questa funzionalità.

**Coordinatori set di criteri:** I coordinatori dei set di criteri possono creare e gestire i criteri condivisi all&#39;interno dei set di criteri in cui sono designati come coordinatori. Un coordinatore di set di criteri è in genere uno specialista dell’organizzazione che può creare al meglio i criteri in un particolare set di criteri.

**Amministratori:** Gli amministratori possono modificare i criteri personali di qualsiasi utente. Possono creare criteri condivisi. Possono inoltre creare, modificare ed eliminare i set di criteri e designare i coordinatori dei set di criteri.

Per informazioni dettagliate sui vari ruoli di Document Security, consulta [Informazioni sugli utenti di Document Security](/help/forms/using/admin-help/document-security.md#about-document-security-users).

## Creazione e modifica di criteri {#creating-and-editing-policies}

Gli utenti possono creare o modificare i criteri personali per il proprio utilizzo. Gli amministratori e i coordinatori di set di policy possono creare o modificare i criteri condivisi per l’organizzazione.

### Considerazioni sulla modifica dei criteri {#considerations-for-editing-policies}

Quando si modifica una policy, le modifiche vengono applicate ai documenti protetti dalla policy e a quelli protetti successivamente. Ad esempio, se si rimuovono i destinatari da un criterio attualmente applicato a un documento, i destinatari non potranno più aprire il documento.

Lo stato del documento determina quando la modifica ha effetto:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che il documento non sia aperto dall&#39;utente. In questo caso, l&#39;utente deve chiudere il documento per rendere effettive le modifiche.
* Se un destinatario utilizza il documento in modalità non in linea (ad esempio, in un computer portatile), le modifiche diventano effettive la volta successiva che il destinatario porta il documento in linea e si sincronizza con la protezione dei documenti aprendo qualsiasi documento protetto tramite policy.

>[!NOTE]
>
>I criteri generati automaticamente da Acrobat per i destinatari dei documenti allegati ai messaggi di posta elettronica in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. È possibile visualizzare questi criteri solo aprendo la pagina Dettagli documento relativa al documento associato.

Quando si modificano i criteri, si applicano le seguenti restrizioni:

* Gli utenti invitati possono modificare i criteri solo se l’amministratore abilita questa funzionalità. Se non è possibile modificare i criteri, l’opzione Modifica non sarà disponibile.
* I coordinatori dei set di criteri possono modificare i criteri all’interno dei set di criteri solo se dispongono delle autorizzazioni corrette. L’amministratore di utenti con privilegi avanzati o set di criteri imposta queste autorizzazioni nell’interfaccia di amministrazione di document security.
* Se il criterio ha una filigrana configurata che l’amministratore ha eliminato dopo la creazione del criterio, questa filigrana non verrà più applicata ai documenti se si modifica e si salva il criterio. Le filigrane eliminate rimangono attive solo per i criteri esistenti, purché non vengano modificate. Se modifichi il criterio, devi selezionare un’altra filigrana per sostituire quella eliminata.
* Non è possibile concedere l&#39;accesso anonimo a un documento modificando il criterio attualmente applicato. Se modifichi la policy, gli utenti devono comunque accedere al documento. Per applicare l&#39;accesso anonimo a questo documento, rimuovere innanzitutto il criterio nell&#39;applicazione client e quindi applicare un altro criterio che consenta l&#39;accesso anonimo.
* I criteri generati automaticamente da Acrobat per i destinatari di un documento allegato a un messaggio di posta elettronica in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. Per accedere a questo criterio, individuare il documento nella pagina Documenti, aprire la pagina Dettagli documento e fare clic sul nome del criterio nell&#39;elenco dei dettagli del documento.

**Creare o modificare un criterio**

1. Nella pagina di Document Security, fai clic su Criteri e quindi su una delle seguenti schede:

   * Per creare o modificare una policy personale, fare clic sulla scheda Policy personale.
   * Per creare o modificare un criterio condiviso, se si dispone dell&#39;autorizzazione necessaria, fare clic sulla scheda Set di criteri, quindi sul nome del set di criteri appropriato e infine sulla scheda Criteri.

1. Fai clic su Nuovo o seleziona il criterio da modificare dall’elenco.
1. Nella casella Nome digitare un nome che identifichi in modo univoco il criterio. Nella casella Descrizione, descrivi le funzioni e le tempistiche del criterio. Se il criterio si trova all&#39;interno di un set di criteri, il nome e la descrizione vengono visualizzati nell&#39;elenco dei criteri per tutti gli utenti specificati. I criteri personali sono disponibili solo per l’utente e gli amministratori.

   Impossibile utilizzare i seguenti caratteri nel nome o nella descrizione:

   * segno di minore di (&lt;)
   * segno di maggiore di (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra (/)

   Se utilizzi il seguente carattere nel nome o nella descrizione, vengono convertiti in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >È possibile creare un nome di criterio che contenga caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come &quot;e&quot; ed &quot;é&quot; vengono considerati uguali. Quando un utente crea un criterio, viene eseguito un confronto per verificare se esiste già un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi uguali, ad eccezione dei caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo criterio non sia stato aggiunto.

1. Aggiungere utenti e gruppi al criterio e impostare le autorizzazioni appropriate. (vedere [Utenti e gruppi](creating-policies.md#users-and-groups).)
1. In Impostazioni generali, selezionare le opzioni appropriate. (vedere [Impostazioni generali](creating-policies.md#general-settings).)
1. (Facoltativo) Se applicabile, selezionare un provider di autorizzazione esterno e specificarne le proprietà. Se non si desidera utilizzare un provider di autorizzazione esterno, fare clic su Rimuovi provider predefinito.

   Un provider di autorizzazione esterno viene utilizzato per impostare le proprietà all&#39;interno del criterio e, se selezionato, il provider di autorizzazione esterno utilizza queste informazioni per valutare il criterio. Le proprietà disponibili vengono configurate dall&#39;amministratore e dalla persona che installa il software.

1. In Impostazioni avanzate, selezionare le opzioni appropriate. (vedere [Impostazioni avanzate](creating-policies.md#advanced-settings).)
1. In Impostazioni avanzate non modificabili selezionare le opzioni appropriate. (vedere [Impostazioni avanzate non modificabili](creating-policies.md#unchangeable-advanced-settings).)
1. Fai clic su Salva. Il criterio viene visualizzato nell&#39;elenco dei criteri. Accanto al nuovo criterio viene visualizzata un&#39;icona con un cerchio rosso a indicare che è ancora disattivato.

   Per rendere il criterio disponibile agli utenti, abilitarlo. (vedere [Abilitare o disabilitare i criteri condivisi](creating-policies.md#enable-or-disable-shared-policies).)

### Utenti e gruppi  {#users-and-groups}

Nell’area Utenti e gruppi specificare gli utenti che hanno accesso ai documenti protetti con la policy. Per ogni utente o gruppo specificato, è inoltre possibile impostare i privilegi di utilizzo del documento.

>[!NOTE]
>
>L’autore del documento è l’utente che protegge il documento con la policy. Questo utente viene sempre incluso per impostazione predefinita in una policy, con diritti di accesso completi, incluse le funzionalità di revoca e cambio di policy. Tuttavia, gli amministratori possono modificare i diritti di accesso dell’editore del documento per i criteri condivisi. Ad esempio, l’amministratore può impedire all’autore del documento di revocare l’accesso al documento o di cambiare il criterio.

**Aggiungi utente o gruppo:** Per aggiungere un utente o un gruppo di utenti, fare clic su Aggiungi utente o gruppo e quindi su Ricerca avanzata per trovare gli utenti o i gruppi. Gli utenti includono gli utenti interni all’organizzazione e gli utenti invitati che si sono registrati con document security. Quando si seleziona questa opzione, viene visualizzata la pagina Aggiungi utente o gruppo:

* Nella casella Trova digitare il nome o l&#39;indirizzo di posta elettronica dell&#39;utente o del gruppo.
* Nell’elenco Utilizzo, seleziona Nome o E-mail.
* Nell&#39;elenco Tipo selezionare Utente o Gruppo.
* Selezionare il dominio in cui si desidera eseguire la ricerca dall&#39;elenco In e fare clic su Trova.
* Quando i risultati vengono restituiti, selezionare l&#39;utente o il gruppo da aggiungere e fare clic su Aggiungi.

>[!NOTE]
>
>Se immetti un nome utente o un indirizzo e-mail invitato corretto e non viene restituito alcun risultato, è possibile che l’utente non si sia ancora registrato o che l’account venga eliminato. Puoi provare ad aggiungere l’utente come tipo di utente invitato o contattare l’amministratore.

**Invita nuovo utente:** Per aggiungere un utente invitato, fai clic su Invita nuovo utente, digita l’indirizzo e-mail dell’utente nella casella visualizzata e fai clic su Invita. Questa opzione è disponibile solo se è stata abilitata dall&#39;amministratore. Quando aggiungi nuovi utenti invitati a una policy, document security invia un’e-mail di invito alla registrazione se gli utenti non sono già invitati a registrarsi. Gli utenti devono utilizzare il collegamento nell’e-mail per creare un account, quindi devono attivare l’account.

Dopo la registrazione, gli utenti invitati possono utilizzare i documenti protetti tramite policy per i quali dispongono dell’autorizzazione. A seconda delle funzionalità abilitate dall&#39;amministratore, gli utenti esterni possono disporre dell&#39;autorizzazione per applicare criteri ai documenti, creare, modificare ed eliminare criteri e aggiungere altri utenti esterni ai criteri.

**Aggiungi utente anonimo:** Per consentire l’accesso anonimo, fai clic su Aggiungi utente anonimo. Questa opzione è disponibile solo se l’amministratore ha abilitato l’accesso anonimo degli utenti per la protezione dei documenti. Consulta Configurare il server di Document Security. Questa opzione consente a tutti di accedere ai documenti protetti da questa policy, indipendentemente dal fatto che dispongano di un account di protezione dei documenti. Se si seleziona questa opzione, non è possibile aggiungere altri tipi di utenti al criterio.

>[!NOTE]
>
>Per consentire l’accesso anonimo a un documento protetto tramite policy che al momento non lo dispone, rimuovi la policy esistente e quindi applica una policy che consenta l’accesso anonimo. Se si cambia o si modifica il criterio esistente, gli utenti devono comunque effettuare l&#39;accesso per accedere al documento.

#### Specificare le autorizzazioni del documento per utenti e gruppi {#specify-the-document-permissions-for-users-and-groups}

È possibile specificare le autorizzazioni del documento per un utente o un gruppo alla volta oppure selezionare più utenti e gruppi dall&#39;elenco e modificarne le autorizzazioni utilizzando le opzioni disponibili nell&#39;area delle intestazioni di colonna.

Per impostazione predefinita, tutti i documenti protetti tramite policy dispongono di un’autorizzazione che consente agli utenti di aprirli mentre sono online.

La scheda Autorizzazioni e opzioni viene visualizzata in Document Security.

Queste autorizzazioni per i documenti sono disponibili nella scheda Autorizzazioni. È possibile applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office.

**Stampa:** Consente all&#39;utente di stampare un documento protetto con questo criterio. Per i file di Office e Pro/E, è possibile selezionare la casella di controllo Stampa per consentire la stampa oppure deselezionarla per impedire la stampa. Se si seleziona la casella di controllo Mostra autorizzazioni personalizzate per PDF, è possibile selezionare una delle opzioni seguenti:

**Non consentito:** L&#39;utente non può stampare il PDF.

**Consentiti:** L&#39;utente può stampare il PDF.

**Risoluzione bassa. solo:** L&#39;utente può stampare il PDF a bassa risoluzione.

**Modifica:** Consente all&#39;utente di modificare un documento protetto con questo criterio. Per i file di Office e Pro/E, è possibile selezionare la casella di controllo Modifica per consentire modifiche o deselezionarla per impedire modifiche. Se si seleziona la casella di controllo Mostra autorizzazioni personalizzate per PDF, è possibile selezionare una delle opzioni seguenti:

**Non consentito:** L’utente non può modificare il PDF.

**Qualsiasi:** L’utente può modificare il PDF.

**Collaborazione:** L’utente può collaborare con altri utenti utilizzando le opzioni Collaborazione di Adobe Acrobat. Questa autorizzazione consente all’utente di copiare i dati del modulo anche se l’autorizzazione di copia non è specificata in modo esplicito nel criterio.

**Modifica pagine:** L’utente può aggiungere e rimuovere pagine e modificarne il contenuto nel PDF.

**Fill &amp; Sign:** L’utente può compilare i campi del modulo sul PDF e firmarlo.

**Copia:** Consente all&#39;utente di copiare testo da un documento protetto con questo criterio.

**Reader schermo:** Questa autorizzazione viene visualizzata se si seleziona la casella di controllo Mostra autorizzazioni personalizzate per PDF. Quando questa opzione è selezionata, Adobe Acrobat dispone dell’autorizzazione per aggiungere tag temporanei al PDF per migliorarne la leggibilità con un’utilità per la lettura dello schermo.

Queste autorizzazioni per i documenti sono disponibili nella scheda Opzioni. È possibile applicare queste autorizzazioni ai file PDF, PTC Pro/E e Microsoft Office:

**Non in linea:** Consente all&#39;utente di visualizzare un documento offline protetto con questo criterio.

**Validità autorizzazione:** Selezionare Autorizzazioni sempre valide o impostare un periodo di validità delle autorizzazioni del documento. Se selezioni un periodo di validità, fai clic sulle icone del calendario per selezionare una data e utilizza le frecce per specificare l’ora nel formato a 24 ore.

Per i criteri condivisi, gli amministratori possono disabilitare i seguenti privilegi per l’autore del documento (l’utente che applica il criterio a un documento):

**Revoca:** Consente all&#39;autore del documento di revocare i privilegi di accesso al documento.

**Switch:** Consente all&#39;autore del documento di cambiare i privilegi dei criteri.

### Impostazioni generali {#general-settings}

L&#39;area Impostazioni generali contiene le impostazioni seguenti:

**Periodo di validità:** Periodo di tempo durante il quale il documento protetto tramite policy è accessibile ai destinatari autorizzati. È possibile scegliere tra le seguenti opzioni del periodo di validità:

**Il documento non sarà valido dopo:** Il documento è accessibile per il numero di giorni specificato a partire dal momento in cui è stato protetto.

**Il documento non sarà valido dopo questa data:** Il documento è valido dalla data in cui il criterio viene applicato al documento fino alla data di fine specificata.

**Valido da, a:** Il documento è valido nelle date specificate. Puoi utilizzare il calendario per selezionare una data, se applicabile, facendo clic sull’icona del calendario.

**Il documento è sempre valido:** Il periodo di validità del documento non scade.

>[!NOTE]
>
>Le date di validità dipendono dal fuso orario del sistema di protezione dei documenti e non dal fuso orario del computer locale.

**Controllo:** Abilita o disabilita il controllo degli eventi associati a un documento protetto tramite policy. Document Security, ad esempio, può registrare eventi quali i tentativi di aprire un documento. Gli eventi controllati vengono visualizzati nell’elenco della pagina Eventi. Se non selezioni questa opzione, document security non registra gli eventi per i documenti associati alla policy.

>[!NOTE]
>
>Affinché la funzione di controllo funzioni, l’amministratore deve inoltre abilitare il controllo del server nella pagina di configurazione delle impostazioni di controllo e privacy.

**Tracciamento dell’utilizzo esteso:** Abilita o disabilita il tracciamento dell&#39;utilizzo esteso. document security supporta il tracciamento degli eventi utente associati a varie operazioni eseguite su un file PDF. È possibile accedere all’oggetto Document Security utilizzando uno script Java. Un clic sul pulsante, un file multimediale in fase di riproduzione o il salvataggio di un file sono alcuni esempi di eventi che possono essere attivati da un PDF protetto tramite policy. L’oggetto Document Security consente inoltre di recuperare informazioni sull’utente. Il tracciamento degli eventi può essere abilitato dal server di Document Security a livello globale o a livello di policy.

**Periodo di lease per attivazione automatica modalità offline:** Il numero massimo di giorni in cui il destinatario può utilizzare il documento protetto tramite policy in modalità non in linea (senza una connessione Internet o di rete attiva). Alla scadenza del periodo di lease, il destinatario deve sincronizzare nuovamente il documento per continuare a utilizzarlo.

### Provider di autorizzazioni esterni {#external-authorization-providers}

Se ne hai già configurato uno, seleziona i provider di autenticazione esterni. Vengono elencati i provider disponibili.

### Impostazioni di autenticazione {#authentication-settings}

È possibile ignorare le impostazioni di autenticazione configurate nel server e specificare le opzioni di autenticazione pertinenti per questo criterio. Selezionare Ignora impostazioni di autenticazione globali, quindi selezionare le opzioni di autenticazione relative al criterio. Sono disponibili le seguenti opzioni di autenticazione:

**Consenti autenticazione password nome utente:** Selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione nome utente/password per la connessione al server.

**Consenti autenticazione Kerberos:** Selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione Kerberos durante la connessione al server.

**Consenti autenticazione certificato client:** Selezionare questa opzione per consentire alle applicazioni client di utilizzare l&#39;autenticazione dei certificati durante la connessione al server.

**Consenti autenticazione estesa** Seleziona per abilitare l&#39;autenticazione estesa. Se si seleziona questa opzione, le applicazioni client potranno utilizzare l&#39;autenticazione estesa. L’autenticazione estesa permette di personalizzare i processi di autenticazione e configurare diverse opzioni di autenticazione sul server di Document Security

Se si ignorano le impostazioni di autenticazione globale, è possibile scegliere le opzioni di autenticazione pertinenti per questo criterio. Ad esempio, se sono state attivate tre opzioni di autenticazione (nome utente e password, certificato client e autenticazione estesa) sul server, è possibile ignorare tale impostazione globale e selezionare solo autenticazione estesa per questo criterio. È necessario assicurarsi che l&#39;opzione di autenticazione selezionata sia già configurata sul server. In questo esempio non è possibile selezionare Kerberos come opzione di autenticazione perché non è configurato nel server.

>[!NOTE]
>
>L’autenticazione estesa è supportata su Apple Mac OS X con Adobe Acrobat versione 11.0.6 e successive.

### Impostazioni avanzate {#advanced-settings}

L&#39;area Impostazioni avanzate contiene le impostazioni seguenti:

**Filigrana dinamica:** Selezionare una filigrana da visualizzare in modo dinamico sulle pagine di un documento, ad esempio quando il documento viene stampato da un destinatario. Le filigrane dinamiche identificano in modo univoco un documento, contribuendo in tal modo a garantirne la riservatezza e a prevenire le violazioni del diritto d’autore. Ad esempio, l’amministratore può configurare una filigrana dinamica che visualizzi la data corrente, il nome utente o l’identificatore della persona che utilizza il documento oppure il nome della policy utilizzata per proteggere il documento. Se configurata, una filigrana può anche visualizzare testo o elementi grafici personalizzati. Gli amministratori possono configurare le opzioni delle filigrane e gli amministratori e gli utenti possono applicarle ai criteri.

(vedere [Configurare le filigrane dinamiche](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks).)

Se si sta modificando un criterio e l&#39;amministratore ha eliminato una filigrana configurata precedentemente selezionata per il criterio, nella pagina Modifica criterio verrà visualizzata una nota. In questo caso, se si sta salvando il documento modificato, selezionare una nuova filigrana se si desidera visualizzarne una nel documento.

>[!NOTE]
>
>Per i criteri che forniscono accesso anonimo, il nome utente e l&#39;identificatore di un utente anonimo non vengono visualizzati come filigrana anche se si seleziona questo tipo di filigrana.

**Usa solo plug-in certificati di Acrobat per PDF:** Se selezionata per una policy, questa opzione specifica che Acrobat 8.0 e versioni successive devono essere eseguite in modalità certificata all’apertura dei documenti protetti con la policy. Quando Acrobat viene eseguito in modalità certificata, non carica alcun plug-in di terze parti.

Selezionare questa opzione se si teme che un destinatario del documento possa scrivere un plug-in che potrebbe eludere le protezioni del documento in Acrobat 8.0 e versioni successive. Non selezionare questa opzione se i destinatari del documento devono utilizzare plug-in di terze parti in Acrobat per interagire con i documenti.

Questa opzione abilita solo la modalità certificata in Acrobat 8.0 o versione successiva; l’amministratore deve disabilitare l’accesso per Acrobat 7.0.

(vedere [Configurare il server di Document Security](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server).)

Questa opzione non si applica ad Adobe Reader.

**Messaggio di errore Accesso negato:** Messaggio visualizzato a chiunque tenti di aprire un documento protetto tramite policy senza autorizzazione. Questo messaggio viene visualizzato in Acrobat. I client che non possono visualizzare questo messaggio visualizzano un messaggio predefinito per indicare che l&#39;accesso è negato.

### Impostazioni avanzate non modificabili {#unchangeable-advanced-settings}

L&#39;area Impostazioni avanzate non modificabili contiene le impostazioni seguenti. Non è possibile modificare queste impostazioni dopo aver salvato il criterio.

**Algoritmo di crittografia e lunghezza chiave:** Utilizzato per proteggere i documenti. Puoi scegliere tra le seguenti opzioni:

* AES a 128 bit
* AES a 256 bit. Solo Acrobat 9.0 e versioni successive supportano questa opzione. Per utilizzare la crittografia AES 256 per i file PDF, è necessario ottenere e installare i file Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Questi file sostituiscono i file local_policy.jar e US_export_policy.jar in [JAVE_HOME]/lib/cartella di protezione. Ad esempio, se si utilizza Sun JDK 1.6, copiare i file scaricati in [directory principale dep]/Java/jdk1.6.0_26/lib/cartella di protezione. Puoi scaricare questi file da [Download Java SE](https://java.sun.com/javase/downloads/index.jsp).
* Nessuna crittografia. Al momento Acrobat 9.0 e versioni successive supportano questa opzione. Se si seleziona questa opzione, le opzioni Restrizioni documenti vengono disattivate. Questa opzione può essere utile se si desidera utilizzare la protezione dei documenti per il controllo dei documenti o delle versioni, ma non si desidera crittografare il documento.

**Restrizioni documenti:** Selezionare i componenti del documento PDF da crittografare. Altre applicazioni client crittografano l&#39;intero documento ma non i file collegati o incorporati. Puoi scegliere tra le seguenti opzioni:

* L&#39;intero documento, inclusi gli allegati e i metadati. *Metadati* sono informazioni sul documento e sul relativo contenuto che è possibile visualizzare tramite la finestra di dialogo Proprietà documento o il menu Avanzate di Acrobat. In Acrobat è possibile allegare ai documenti PDF file di tipi diversi, ad esempio file di testo, audio e video.
* Il documento e i relativi allegati, ma non i metadati.
* Solo gli allegati del documento. È possibile crittografare gli allegati in un file PDF senza crittografare il contenuto del documento.

## Abilitare o disabilitare i criteri condivisi {#enable-or-disable-shared-policies}

Per rendere disponibile un criterio condiviso, l&#39;amministratore o il coordinatore del set di criteri deve attivarlo. È possibile abilitare nuovi criteri o criteri precedentemente disabilitati. Un criterio condiviso disabilitato viene comunque applicato ai documenti protetti con tale criterio.

Accanto a un criterio disabilitato viene visualizzata una X rossa.

>[!NOTE]
>
>Gli amministratori non possono disattivare i criteri personali e gli utenti non possono abilitare e disabilitare i propri criteri.

1. Nella pagina relativa alla protezione dei documenti fare clic su Criteri e quindi sulla scheda Set di criteri.
1. Fare clic sul nome del set di criteri appropriato e quindi sulla scheda Criteri.
1. Selezionare la casella di controllo accanto al criterio appropriato, fare clic su Attiva o Disattiva e quindi su OK.

## Visualizzare informazioni su un criterio {#view-information-about-a-policy}

Utilizzando la scheda I miei criteri, puoi effettuare ricerche nei criteri personali.

I set di criteri creati dagli amministratori sono elencati nella scheda Set di criteri della pagina Criteri con informazioni sul set di criteri, tra cui il nome, la data di creazione e di modifica e una descrizione. Fare clic sul nome di un set di criteri per visualizzarne i dettagli. I coordinatori di set di criteri che dispongono dell&#39;autorizzazione per gestire i criteri possono creare criteri condivisi all&#39;interno di un determinato set di criteri.

Quando si crea o si modifica una policy, viene visualizzata una pagina in cui è possibile configurare dettagli quali il nome della policy, i livelli di autorizzazione, le impostazioni di riservatezza e i destinatari da includere nella policy.

L’amministratore può configurare le seguenti impostazioni di riservatezza per un criterio:

* Opzioni generali di riservatezza dei documenti, ad esempio il periodo di validità dei documenti e il periodo di lease offline
* Gli utenti autorizzati e le restrizioni e i privilegi del documento per ciascuno di tali utenti
* Opzioni avanzate di riservatezza dei documenti, incluse filigrane dinamiche e crittografia dei documenti

Gli utenti possono visualizzare i criteri creati e tutti i criteri condivisi a cui hanno accesso. Gli amministratori possono visualizzare tutte le policy condivise e personali incluse nella protezione dei documenti.

Puoi visualizzare informazioni più dettagliate su un criterio visualizzato nell’elenco, inclusi gli utenti o i gruppi inclusi nel criterio e le impostazioni di riservatezza specificate per tali utenti.

>[!NOTE]
>
>I criteri generati automaticamente da Acrobat per i destinatari dei documenti allegati ai messaggi di posta elettronica in Microsoft Outlook non vengono visualizzati nell&#39;elenco dei criteri. È possibile visualizzare questi criteri solo aprendo la pagina Dettagli documento relativa al documento associato.

1. Nella pagina Document Security, fai clic su Criteri, quindi fai clic sulla scheda Criteri.
1. Completa le informazioni di ricerca per cercare le policy personali.
1. Selezionare il criterio appropriato dall&#39;elenco.
1. Nella pagina Dettagli criterio è possibile visualizzare i dettagli del criterio, modificarlo o visualizzare gli eventi correlati al criterio.

## Cerca criteri {#search-for-policies}

Gli amministratori possono cercare i criteri condivisi e i criteri personali creati da altri utenti.

1. Per cercare un criterio condiviso, fare clic su Criteri e quindi sulla scheda Set di criteri. Fare clic su un set di criteri nell&#39;elenco e quindi sulla scheda Criteri.

   Per cercare una policy personale, nella pagina di protezione dei documenti fai clic su Policy, quindi fai clic sulla scheda Criteri.

1. Nell&#39;elenco Trova selezionare una delle opzioni seguenti:

   **ID criterio:** Numero di identificazione del criterio generato quando l&#39;utente crea il criterio. Devi digitare l’ID esatto del criterio.

   **Nome criterio:** Nome del criterio. È possibile cercare solo una parte del nome del criterio.

1. Nella casella di testo digitare il valore corrispondente. Se ad esempio è stato selezionato Nome criterio, digitare il nome del criterio che si desidera cercare.
1. Nell&#39;elenco Visualizza selezionare il numero di risultati da visualizzare e quindi fare clic su Trova. Vengono visualizzati i risultati della ricerca.
1. (Facoltativo) Per visualizzare i dettagli dei criteri, fai clic sul criterio.

## Copiare una policy {#copy-a-policy}

È possibile copiare un criterio esistente e salvarlo con un nuovo nome e una nuova descrizione. La copia dei criteri rappresenta un modo efficiente per creare nuovi criteri utilizzando le impostazioni esistenti.

Gli utenti esterni possono copiare i criteri solo se l’amministratore abilita questa funzionalità. Se non è possibile creare i criteri, l&#39;opzione Copia non sarà disponibile.

1. Nella pagina Document Security, fai clic su Criteri, quindi fai clic sulla scheda Criteri.
1. Selezionare il criterio appropriato dall&#39;elenco.
1. Nella pagina Dettagli criterio, fai clic su Copia.
1. Nella casella Nuovo nome criterio digitare il nuovo nome del criterio. È possibile digitare una nuova descrizione.

   Impossibile utilizzare i seguenti caratteri nel nome o nella descrizione:

   * segno di minore di (&lt;)
   * segno di maggiore di (>)
   * e commerciale (&amp;)
   * virgolette singole (&#39;)
   * virgolette doppie (&quot;)
   * barra rovesciata (\)
   * barra (/)

   Se utilizzi il seguente carattere nel nome o nella descrizione, vengono convertiti in spazi:

   * ritorno a capo (carattere ASCII 13)
   * nuova riga (carattere ASCII 10).

   >[!NOTE]
   >
   >È possibile creare un nome di criterio che contenga caratteri estesi; tuttavia, quando si effettua un confronto tra due stringhe, i caratteri accentati e non accentati come &quot;e&quot; ed &quot;é&quot; vengono considerati uguali. Quando un utente crea un criterio, viene eseguito un confronto per verificare se esiste già un criterio con lo stesso nome. Il confronto non è in grado di distinguere tra nomi uguali, ad eccezione dei caratteri accentati. Si presume che il criterio sia già stato aggiunto al database e che il nuovo criterio non sia stato aggiunto.

1. Fai clic su OK.

## Eliminare un criterio {#delete-a-policy}

Puoi eliminare i criteri creati. Gli amministratori possono eliminare i criteri creati da qualsiasi utente. I coordinatori di set di criteri possono eliminare i criteri nei propri set di criteri. Una policy eliminata viene comunque applicata ai documenti protetti con tale policy. È possibile eliminare più criteri alla volta.

Gli utenti invitati possono eliminare i criteri solo se l’amministratore abilita questa funzionalità. Se non è possibile eliminare i criteri, l’opzione di eliminazione non sarà disponibile.

1. Nella pagina di Document Security, fai clic su Criteri.
1. Fare clic sulla scheda Criteri utente.
1. Per eliminare un criterio condiviso, fare clic sulla scheda Set di criteri e quindi sul nome del set di criteri appropriato.
1. Selezionare la casella di controllo accanto al criterio appropriato e fare clic su Elimina, quindi scegliere OK.

>[!NOTE]
>
>È necessario utilizzare l&#39;applicazione client per rimuovere i criteri dai documenti. Consulta la Guida di Acrobat o la Guida delle estensioni di Acrobat Reader DC appropriate.

## Ordinare l’elenco dei criteri {#sort-the-policy-list}

Per trovare i criteri in modo più semplice, è possibile ordinare l’elenco dei criteri in base all’intestazione della colonna. Un’icona a forma di triangolo accanto all’intestazione della colonna indica la colonna attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l&#39;alto indica un ordine crescente, mentre un triangolo rivolto verso il basso indica un ordine decrescente.

1. Nella pagina relativa alla protezione dei documenti, fai clic su Criteri e quindi sulla scheda Set di criteri.
1. Selezionare un set di criteri e quindi fare clic sulla scheda Criteri.
1. Fare clic sull&#39;intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai di nuovo clic sulla colonna.
