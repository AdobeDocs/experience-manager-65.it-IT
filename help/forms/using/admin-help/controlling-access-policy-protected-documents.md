---
title: Controllo dell’accesso ai documenti protetti da criteri
description: Scopri come visualizzare, gestire e controllare l’accesso ai documenti protetti da criteri.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '2167'
ht-degree: 100%

---

# Controllo dell’accesso ai documenti protetti da criteri {#controlling-access-to-policy-protected-documents}

Puoi controllare in che modo i destinatari utilizzano i file protetti da criteri, indipendentemente da quanto è ampia la distribuzione.

Nella pagina Documenti puoi eseguire queste operazioni:

* Ricercare e visualizzare i dettagli dei documenti protetti da criteri. Puoi visualizzare informazioni relative al nome del documento, al nome dell’editore, al nome del criterio e alla data di applicazione del criterio. Se elimini il criterio che proteggeva un documento, puoi visualizzare anche l’ID del criterio eliminato sotto il nome criterio. Gli utenti possono visualizzare e gestire i propri documenti protetti da criteri. Gli amministratori possono visualizzare e gestire tutti i documenti protetti da criteri.
* Modificare i dettagli del criterio applicato a un documento. Gli utenti possono modificare i propri criteri, gli amministratori possono modificare i criteri personali e condivisi e i coordinatori dei set di criteri possono modificare i criteri condivisi nei set di criteri per i quali dispongono delle autorizzazioni. Puoi accedere al criterio associato a un documento direttamente dalla pagina Dettagli documento.
* Revocare e ripristinare l’accesso a un documento protetto da criterio. Gli amministratori possono revocare e ripristinare l’accesso a qualsiasi documento. I coordinatori dei set di criteri (che dispongono dell’autorizzazione per gestire i documenti) possono revocare e ripristinare l’accesso ai documenti protetti da criteri che utilizzano criteri condivisi dai propri set di criteri. Gli utenti possono revocare l’accesso ai propri documenti protetti da criteri se hanno creato il criterio che protegge il documento o se il criterio è condiviso e consente questa funzionalità.
* Cambiare il criterio applicato a un documento. Gli utenti che applicano criteri ai documenti possono cambiare un criterio se l’hanno creato o se si tratta di un criterio condiviso che consente questa funzionalità. I coordinatori di set di criteri possono cambiare i criteri dei propri set di criteri. Gli amministratori possono cambiare i criteri applicati a qualsiasi documento.

Quando un documento è protetto da un criterio e revochi i privilegi di accesso o cambi il criterio applicato, le modifiche diventano effettive come segue:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che il documento non sia aperto dall’utente. In questo caso, l’utente deve chiudere il documento per rendere effettive le modifiche.
* Se un destinatario utilizza il documento offline (ad esempio, su un laptop), le modifiche diventano effettive alla successiva sincronizzazione del destinatario con la protezione dei documenti tramite l’apertura di qualsiasi documento protetto da criterio.

## Visualizzare informazioni su un documento {#view-information-about-a-document}

Per ogni documento elencato nella pagina Documenti, puoi visualizzare il nome del documento, il nome dell’autore, il nome del criterio e la data di protezione del documento. Se elimini il criterio che proteggeva un documento, l’ID del criterio viene elencato in Nome criterio.

Puoi inoltre visualizzare ulteriori dettagli, descritti di seguito, su un particolare documento nella pagina Dettagli documento:

>[!NOTE]
>
>Utilizza il collegamento Nome criterio nella pagina Dettagli documento per accedere ai criteri generati automaticamente in Microsoft Outlook per i destinatari di un documento allegato a un messaggio e-mail. Questi criteri non vengono visualizzati nella pagina dei criteri.

**Nome documento:** il nome del documento selezionato.

**ID documento:** un identificatore univoco assegnato dalla protezione dei documenti quando viene applicato un criterio al documento. protezione dei documenti utilizza questo numero per il tracciamento del documento.

**Stato documento:** lo stato del documento (ad esempio, attivo o revocato).

**Autore:** il nome dell’utente che ha allegato il criterio al documento.

**Nome criterio:** il nome del criterio utilizzato per proteggere il documento. Puoi fare clic sul nome per aprire il criterio. Utilizza questo collegamento per accedere ai criteri generati da Acrobat per i destinatari di un documento allegato a un messaggio e-mail in Outlook. Tali criteri non vengono visualizzati nella pagina Criteri.

**Tipo di criterio:** il tipo di criterio applicato al documento.

**Data pubblicazione:** la data in cui il criterio è stato applicato al documento.

**Iterazioni correlate:** se il documento contiene iterazioni correlate, anche questo elemento verrà visualizzato nell’elenco. Fai clic sul collegamento per visualizzare l’elenco delle iterazioni correlate per il documento.

Gli utenti possono visualizzare le informazioni sui documenti protetti. Gli amministratori possono visualizzare le informazioni sui documenti protetti da qualsiasi utente tramite un criterio. I coordinatori dei set di criteri possono visualizzare le informazioni sui documenti protetti da criteri dai propri set di criteri.

1. Nella pagina di protezione dei documenti fai clic su Documenti.
1. Nell’elenco dei documenti, fai clic sul documento appropriato. Viene visualizzata la pagina Dettagli documento contenente informazioni dettagliate sul documento. In questa pagina sono inoltre disponibili le opzioni per la revoca dell’accesso ai documenti, il cambio dei criteri e la visualizzazione degli eventi correlati a questo documento.

## Visualizzare le iterazioni correlate di un documento {#view-related-iterations-for-a-document}

Se è abilitata la registrazione delle iterazioni correlate, è possibile tenere traccia delle versioni di un documento salvate da vari utenti. Questa funzione è supportata solo da alcune applicazioni, ad esempio PTC Pro/ENGINEER Wildfire.

Questa funzione è utile quando più utenti collaborano e salvano versioni diverse dello stesso documento. La protezione dei documenti è in grado di tenere traccia delle varie iterazioni, pertanto è possibile visualizzare facilmente le informazioni del documento per le diverse versioni.

Se questa funzione è abilitata, puoi visualizzare le iterazioni correlate di un documento dalla pagina Documenti.

1. Visualizza la pagina Dettagli documento relativa a un documento. Consulta [Visualizza informazioni su un documento](controlling-access-policy-protected-documents.md#view-information-about-a-document).
1. Fai clic su Visualizza iterazioni correlate. L’opzione è disponibile solo se la funzione è abilitata. Viene visualizzato l’elenco delle iterazioni correlate. Per ogni iterazione, puoi visualizzare le seguenti informazioni:

   * **Iterazione:** Il nome del file. Può essere diverso dal nome file originale e alla fine è aggiunto un numero di versione.
   * **Editore:** editore del documento originale.
   * **Creato da:** l’utente che ha salvato l’iterazione.
   * **Data creazione:** la data e l’ora in cui è stata salvata l’iterazione.
   * **Criterio:** il criterio che protegge l’iterazione. Diverse iterazioni possono essere protette da diversi criteri.

1. Per visualizzare la pagina Dettagli documento relativa a tale iterazione, fai clic sul nome file di un’iterazione.

## Revoca e ripristino dell’accesso ai documenti {#revoking-and-reinstating-access-to-documents}

Puoi revocare e ripristinare l’accesso ai documenti protetti tramite criterio:

**Utenti:** possono revocare o ripristinare l’accesso ai documenti protetti con i propri criteri personali o con criteri condivisi per i quali la funzionalità di revoca è abilitata per l’utente che applica i criteri. Gli utenti che non possono revocare l’accesso a un documento o cambiare un criterio devono contattare l’amministratore.

**Amministratori:** possono revocare o ripristinare i privilegi di accesso a qualsiasi documento protetto tramite criterio, inclusi quelli protetti tramite criteri personali o condivisi. Se un amministratore revoca l’accesso a un documento protetto con un criterio condiviso, solo un amministratore può ripristinare i privilegi di accesso per quel documento.

**Coordinatori set di criteri:** possono revocare o ripristinare i privilegi di accesso per i documenti protetti dai propri set di criteri.

Quando si revocano o si ripristinano i privilegi di accesso ai documenti, la modifica ha effetto nei seguenti momenti:

* Se il documento è online e chiuso, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione dei documenti tramite l’apertura di un documento protetto tramite criterio.
* Se il documento è online e aperto, la modifica ha effetto quando il destinatario chiude il documento.
* Se il documento è offline, ovvero utilizzato senza una connessione Internet, ad esempio su un laptop, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione dei documenti.

**Revocare l’accesso a un documento protetto tramite criterio**

1. Nella pagina di protezione dei documenti fai clic su Documenti.
1. Seleziona la casella di controllo accanto al documento appropriato e fai clic su Revoca. Puoi revocare l’accesso a più documenti alla volta.
1. Seleziona un messaggio da visualizzare agli utenti che tentano di aprire il documento dopo la revoca:

   * **Messaggio generale:** indica che l’autore ha revocato il documento
   * **Documento terminato:** indica che l’autore ha terminato il documento
   * **Documento rivisto**: indica che l’autore ha rivisto il documento

1. (Facoltativo) Se è disponibile una versione più recente del documento, immetti l’URL e fai clic su Test per verificare l’URL.
1. Fai clic su OK, quindi di nuovo su OK per tornare alla pagina Documenti.

**Ripristinare i privilegi di accesso ai documenti**

1. Nella pagina di protezione dei documenti fai clic su Documenti.
1. Nell’elenco dei documenti, fai clic sul documento appropriato.
1. Fai clic su Annulla revoca e quindi su OK.

## Modificare il criterio applicato a un file {#switch-a-policy-that-is-applied-to-a-document}

Gli utenti, i coordinatori di set di criteri e gli amministratori possono cambiare il criterio applicato a un documento protetto tramite criteri (puoi applicare un solo criterio per volta a un documento). Gli utenti possono cambiare i criteri applicati ai propri documenti protetti tramite criteri se hanno creato il criterio o se il criterio è condiviso e questa funzionalità è abilitata. In caso contrario, l’amministratore o il coordinatore del set di criteri deve cambiare il criterio. Gli amministratori possono cambiare i criteri dei documenti protetti da criteri di qualsiasi utente. I coordinatori di set di criteri possono cambiare i criteri dei propri set di criteri.

Quando cambi un criterio, il nuovo criterio viene applicato come segue:

* Se il documento è online e chiuso, la modifica ha effetto quando il destinatario esegue una nuova sincronizzazione con la protezione dei documenti aprendo online qualsiasi documento protetto tramite criteri.
* Se il documento è online e aperto, la modifica ha effetto quando l’utente chiude il documento.
* Se il documento è offline (in uso senza una connessione Internet o di rete attiva, ad esempio su un laptop), la modifica viene applicata quando il destinatario esegue una nuova sincronizzazione con la protezione dei documenti aprendo online un documento protetto tramite criteri.

>[!NOTE]
>
>Per consentire l’accesso anonimo a un documento protetto tramite criteri che non dispone di tale tipo di accesso, rimuovi il criterio esistente nell’applicazione client, quindi applica un criterio che consenta l’accesso anonimo. Se cambi il criterio, gli utenti devono comunque effettuare l’accesso per accedere al documento.

1. Nella pagina di protezione dei documenti fai clic su Documenti.
1. Nell’elenco dei documenti, fai clic sul documento appropriato.
1. Fai clic su Cambia criterio. Viene visualizzato un elenco contenente fino a 100 criteri.
1. Se il criterio che desideri non è visualizzato, seleziona Nome criterio o ID criterio nell’elenco Trova, digita il nome o l’ID e fai clic su Trova.
1. Fai clic su un nuovo criterio nell’elenco.
1. Fai clic su Cambia criterio e quindi su OK per tornare alla pagina Documenti.

## Cercare un documento {#search-for-a-document}

Puoi cercare i documenti nella pagina Documenti utilizzando una combinazione tra i criteri dell’intervallo di date e i criteri di ricerca disponibili nell’elenco. Questi criteri includono il nome del documento, il nome del criterio o tutti i documenti.

Alcune opzioni di ricerca aggiuntive sono disponibili solo per gli amministratori:

**ID documento:** numero ID univoco assegnato al documento dalla protezione dei documenti quando viene applicato il criterio.

**Nome documento:** il nome del documento.

**Nome editore:** nome dell’utente che ha allegato il criterio al documento. Puoi selezionare l’utente da tutti i domini o da un dominio specificato.

**ID criterio:** numero ID del criterio allegato al documento.

**Nome criterio:** nome del criterio allegato al documento.

**Tutti i documenti:** tutti i documenti protetti da amministratori e utenti. L’utilizzo dell’opzione Tutti i documenti per la ricerca può restituire un elenco di documenti molto lungo.

1. Nella pagina di protezione dei documenti fai clic su Documenti.
1. Nella finestra di dialogo Trova, seleziona i criteri di ricerca necessari.

   Puoi specificare criteri come ID documento, Nome documento, Nome editore, ID criterio, Nome criterio o Tutti i documenti.

   Se specifichi Nome editore, fai clic sull’icona Rubrica e specifica il dominio in cui eseguire la ricerca dell’utente, quindi scegli OK per tornare alla pagina di ricerca Documenti.

1. (Facoltativo) Nell’elenco Data, seleziona un’opzione per l’intervallo di date. Se selezioni Personalizza date, digita la data in formato gg/mm/aaaa nelle caselle visualizzate oppure utilizza il selettore data per specificare l’intervallo di date:

   * Fai clic sul calendario per aprire il Selettore data.
   * Usa le frecce per trovare un anno e un mese.
   * Fai clic su un giorno del mese nel calendario.
   * Fai clic su OK per chiudere il Selettore data.

1. Fai clic su Trova.

## Ordinare l’elenco dei documenti {#sort-the-document-list}

Puoi ordinare l’elenco dei documenti per intestazione di colonna. Le icone triangolari accanto all’intestazione della colonna indicano la colonna attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l’alto indica un ordine crescente, mentre un triangolo rivolto verso il basso indica un ordine decrescente.

1. Nella pagina di protezione dei documenti fai clic su Documenti.
1. Fai clic sull’intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai di nuovo clic sulla colonna.

## Aggiungere una copertina ai documenti protetti tramite criteri {#add-cover-page-to-policy-protected-documents}

Se la maggior parte degli utenti che visualizzano documenti non utilizza Adobe PDF, quandi apri un documento protetto tramite la protezione dei documenti, la prima pagina viene visualizzata come una pagina vuota o l’applicazione si interrompe senza aprire il documento.

Puoi utilizzare il supporto Pagina 0 (Wrapper) per consentire agli utenti che non usano Adobe PDF di aprire un documento protetto e di visualizzare una copertina del documento.

>[!NOTE]
>
>Quando visualizzi questi documenti (contenenti una Pagina 0) in Adobe Reader/Acrobat o Mobile Reader, il documento protetto viene aperto per impostazione predefinita.

**Per aggiungere una copertina a un documento protetto tramite criteri**

Utilizza i seguenti processi in Workbench:

**Proteggi
documento con copertina:** protegge un documento PDF con il criterio specificato e aggiunge una copertina al documento

**Estrai documento protetto:** estrae il documento PDF protetto da criterio dal documento PDF con copertina

Utilizza le seguenti API di protezione dei documenti:

**protectDocumentWithCoverPage:** protegge un determinato PDF con il criterio specificato e restituisce un documento con una copertina e il documento protetto come allegato
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** estrae il documento protetto che è un allegato nel documento con copertina. Puoi creare il documento con copertina utilizzando il metodo protectDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
