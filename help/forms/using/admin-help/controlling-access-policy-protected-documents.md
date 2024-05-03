---
title: Controllo dell’accesso ai documenti protetti tramite policy
description: Scopri come visualizzare, gestire e controllare l’accesso ai documenti protetti tramite policy.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 0%

---

# Controllo dell’accesso ai documenti protetti tramite policy {#controlling-access-to-policy-protected-documents}

È possibile controllare il modo in cui i destinatari utilizzano i documenti protetti tramite policy, indipendentemente dal numero di persone distribuite.

Nella pagina Documenti è possibile eseguire le operazioni seguenti:

* Cerca e visualizza i dettagli dei documenti protetti tramite policy. È possibile visualizzare informazioni relative al nome del documento, al nome dell&#39;editore, al nome del criterio e alla data di applicazione del criterio. Se il criterio che ha protetto un documento viene eliminato, è possibile visualizzare anche l’ID del criterio eliminato sotto il nome del criterio. Gli utenti possono visualizzare e gestire i propri documenti protetti tramite policy. Gli amministratori possono visualizzare e gestire tutti i documenti protetti tramite policy.
* Modificare i dettagli della policy applicata a un documento. Gli utenti possono modificare i propri criteri, gli amministratori possono modificare i criteri personali e condivisi e i coordinatori dei set di criteri possono modificare i criteri condivisi nei set di criteri per i quali dispongono delle autorizzazioni. È possibile accedere al criterio associato a un documento direttamente dalla pagina Dettagli documento.
* Revoca e ripristino dell&#39;accesso a un documento protetto tramite policy. Gli amministratori possono revocare e ripristinare l’accesso a qualsiasi documento. I coordinatori dei set di policy (che dispongono dell’autorizzazione per gestire i documenti) possono revocare e ripristinare l’accesso ai documenti protetti tramite policy che utilizzano policy condivise dai propri set di policy. Gli utenti possono revocare l’accesso ai propri documenti protetti tramite policy se hanno creato la policy che protegge il documento o se la policy è condivisa e consente questa funzionalità.
* Cambia il criterio applicato a un documento. Gli utenti che applicano policy ai documenti possono cambiare una policy se l’hanno creata o se si tratta di una policy condivisa che abilita questa funzionalità. I coordinatori di set di criteri possono cambiare i criteri dai propri set di criteri. Gli amministratori possono cambiare i criteri applicati a qualsiasi documento.

Quando un documento è protetto da una policy e si revocano i privilegi di accesso o si cambia la policy applicata, le modifiche hanno effetto come segue:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che il documento non sia aperto dall&#39;utente. In questo caso, l&#39;utente deve chiudere il documento per rendere effettive le modifiche.
* Se un destinatario utilizza il documento in modalità non in linea (ad esempio, su un laptop), le modifiche diventano effettive alla successiva sincronizzazione del destinatario con la protezione dei documenti tramite l’apertura di qualsiasi documento protetto tramite policy.

## Visualizzare informazioni su un documento {#view-information-about-a-document}

Per ogni documento elencato nella pagina Documenti, è possibile visualizzare il nome del documento, il nome dell&#39;autore, il nome della policy e la data di protezione del documento. Se il criterio che ha protetto un documento è stato eliminato, l’ID del criterio è elencato in Nome criterio.

È inoltre possibile visualizzare ulteriori dettagli, descritti di seguito, su un particolare documento nella pagina Dettagli documento:

>[!NOTE]
>
>Utilizzare il collegamento Nome criterio nella pagina Dettagli documento per accedere ai criteri generati automaticamente in Microsoft Outlook per i destinatari di un documento allegato a un messaggio di posta elettronica. Questi criteri non vengono visualizzati nella pagina dei criteri.

**Nome documento:** Nome del documento selezionato.

**ID documento:** Identificatore univoco assegnato da Document Security quando viene applicata una policy al documento. document security utilizza questo numero per tenere traccia del documento.

**Stato documento:** Stato del documento, ad esempio attivo o revocato.

**Editore:** Nome dell’utente che ha allegato il criterio al documento.

**Nome criterio:** Nome del criterio utilizzato per proteggere il documento. Puoi fare clic sul nome per aprire il criterio. Utilizzare questo collegamento per accedere ai criteri generati da Acrobat per i destinatari di un documento allegato a un messaggio di posta elettronica in Outlook. Tali criteri non vengono visualizzati nella pagina Criteri.

**Tipo di criterio:** Tipo di criterio applicato al documento.

**Data di pubblicazione:** Data in cui il criterio è stato applicato al documento.

**Iterazioni correlate:** Se nel documento sono presenti iterazioni correlate, anche questo elemento viene visualizzato nell&#39;elenco. Fare clic sul collegamento per visualizzare l&#39;elenco delle iterazioni correlate per il documento.

Gli utenti possono visualizzare informazioni sui documenti protetti. Gli amministratori possono visualizzare informazioni sui documenti protetti da qualsiasi utente tramite una policy. I coordinatori dei set di policy possono visualizzare informazioni sui documenti protetti da policy dai propri set di policy.

1. Nella pagina di protezione dei documenti fare clic su Documenti.
1. Nell&#39;elenco dei documenti fare clic sul documento appropriato. Viene visualizzata la pagina Dettagli documento contenente informazioni dettagliate sul documento. In questa pagina sono inoltre disponibili le opzioni per la revoca dell&#39;accesso ai documenti, il cambiamento della policy e la visualizzazione degli eventi correlati al documento.

## Visualizzare le iterazioni correlate di un documento {#view-related-iterations-for-a-document}

Se è abilitata la registrazione delle iterazioni correlate, è possibile tenere traccia delle versioni di un documento salvate da vari utenti. Questa funzione è supportata solo da alcune applicazioni, ad esempio PTC Pro/ENGINEER Wildfire.

Questa funzione è utile quando più utenti collaborano e salvano versioni diverse dello stesso documento. document security è in grado di tenere traccia delle varie iterazioni, pertanto è possibile visualizzare facilmente le informazioni del documento per le diverse versioni.

Se questa funzione è abilitata, è possibile visualizzare le iterazioni correlate di un documento dalla pagina Documenti.

1. Visualizzare la pagina Dettagli documento relativa a un documento. (vedere [Visualizzare informazioni su un documento](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. Fare clic su Visualizza iterazioni correlate. L’opzione è disponibile solo se la funzione è abilitata. Viene visualizzato l&#39;elenco delle iterazioni correlate. Per ogni iterazione, potete visualizzare le seguenti informazioni:

   * **Iterazione:** Il nome del file. Può essere diverso dal nome file originale e alla fine è aggiunto un numero di versione.
   * **Editore:** Autore del documento originale.
   * **Creato da:** Utente che ha salvato l&#39;iterazione.
   * **Data di creazione:** Data e ora in cui è stata salvata l&#39;iterazione.
   * **Criteri:** Criterio che protegge l&#39;iterazione. Diverse iterazioni possono essere protette da diversi criteri.

1. Per visualizzare la pagina Dettagli documento relativa a tale iterazione, fare clic sul nome file di un&#39;iterazione.

## Revoca e ripristino dell&#39;accesso ai documenti {#revoking-and-reinstating-access-to-documents}

È possibile revocare e ripristinare l’accesso ai documenti protetti tramite policy:

**Utenti:** Possono revocare o ripristinare l’accesso ai documenti protetti con le proprie policy personali o con le policy condivise per le quali è abilitata la funzionalità di revoca per l’utente che applica la policy. Gli utenti che non possono revocare l’accesso a un documento o cambiare una policy devono contattare l’amministratore.

**Amministratori:** Possono revocare o ripristinare i privilegi di accesso a qualsiasi documento protetto tramite policy, inclusi quelli protetti tramite policy personali o condivise. Se un amministratore revoca l’accesso a un documento protetto con una policy condivisa, solo un amministratore può ripristinare i privilegi di accesso per quel documento.

**Coordinatori set di criteri:** È possibile revocare o ripristinare i privilegi di accesso per i documenti protetti dai propri set di criteri.

Quando si revocano o si ripristinano i privilegi di accesso ai documenti, la modifica ha effetto nei seguenti momenti:

* Se il documento è online e chiuso, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione dei documenti tramite l’apertura di un documento protetto tramite policy.
* Se il documento è online e aperto, la modifica ha effetto quando il destinatario chiude il documento.
* Se il documento è offline, ovvero utilizzato senza una connessione Internet, ad esempio su un laptop, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione dei documenti.

**Revoca dell’accesso a un documento protetto tramite policy**

1. Nella pagina di protezione dei documenti fare clic su Documenti.
1. Selezionare la casella di controllo accanto al documento appropriato e fare clic su Revoca. È possibile revocare l&#39;accesso a più documenti alla volta.
1. Selezionare un messaggio da visualizzare agli utenti che tentano di aprire il documento dopo la revoca:

   * **Messaggio generale:** Indica che l&#39;autore ha revocato il documento
   * **Documento terminato:** Indica che l&#39;autore ha terminato il documento
   * **Documento revisionato**: indica che l’autore ha rivisto il documento

1. (Facoltativo) Se è disponibile una versione più recente del documento, immettere l&#39;URL e fare clic su Test per verificare l&#39;URL.
1. Fare clic su OK, quindi di nuovo su OK per tornare alla pagina Documenti.

**Ripristinare i privilegi di accesso ai documenti**

1. Nella pagina di protezione dei documenti fare clic su Documenti.
1. Nell&#39;elenco dei documenti fare clic sul documento appropriato.
1. Fare clic su Annulla revoca e quindi su OK.

## Cambiare un criterio applicato a un documento {#switch-a-policy-that-is-applied-to-a-document}

Gli utenti, i coordinatori di set di policy e gli amministratori possono cambiare la policy applicata a un documento protetto tramite policy (è possibile applicare una sola policy alla volta a un documento). Gli utenti possono cambiare i criteri applicati ai propri documenti protetti tramite policy se hanno creato la policy o se la policy è condivisa e questa funzionalità è abilitata. In caso contrario, l’amministratore o il coordinatore del set di criteri deve cambiare il criterio. Gli amministratori possono cambiare le policy per i documenti protetti tramite policy di qualsiasi utente. I coordinatori di set di criteri possono cambiare i criteri dai propri set di criteri.

Quando si cambia un criterio, il nuovo criterio viene applicato come segue:

* Se il documento è online e chiuso, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione dei documenti, tramite l’apertura online di qualsiasi documento protetto tramite policy.
* Se il documento è online e aperto, la modifica ha effetto quando l&#39;utente chiude il documento.
* Se il documento è offline (in uso senza una connessione Internet o di rete attiva, ad esempio su un laptop), la modifica viene applicata alla successiva sincronizzazione dell’utente con document security aprendo online un documento protetto tramite policy.

>[!NOTE]
>
>Per consentire l’accesso anonimo a un documento protetto tramite policy a cui attualmente non si accede, rimuovi la policy esistente nell’applicazione client e quindi applica una policy che consenta l’accesso anonimo. Se si cambia la policy, gli utenti devono comunque effettuare l’accesso per accedere al documento.

1. Nella pagina di protezione dei documenti fare clic su Documenti.
1. Nell&#39;elenco dei documenti fare clic sul documento appropriato.
1. Fare clic su Cambia criterio. Viene visualizzato un elenco contenente fino a 100 criteri.
1. Se il criterio desiderato non è visualizzato, selezionare Nome criterio o ID criterio dall&#39;elenco Trova, digitare il nome o l&#39;ID e fare clic su Trova.
1. Fai clic su un nuovo criterio nell’elenco.
1. Fare clic su Cambia criterio e quindi su OK per tornare alla pagina Documenti.

## Cercare un documento {#search-for-a-document}

È possibile cercare i documenti nella pagina Documenti utilizzando una combinazione di criteri di intervallo di date e di criteri di ricerca disponibili nell&#39;elenco. Questi criteri includono il nome del documento, il nome del criterio o tutti i documenti.

Alcune opzioni di ricerca aggiuntive sono disponibili solo per gli amministratori:

**ID documento:** Numero ID univoco assegnato da Document Security al documento quando viene applicata la policy.

**Nome documento:** Nome del documento.

**Nome editore:** Nome dell’utente che ha allegato il criterio al documento. Puoi selezionare l’utente da tutti i domini o da un dominio specificato.

**ID criterio:** Numero ID del criterio allegato al documento.

**Nome criterio:** Nome del criterio allegato al documento.

**Tutti i documenti:** Tutti i documenti protetti da amministratori e utenti. L&#39;utilizzo dell&#39;opzione Tutti i documenti per la ricerca può restituire un lungo elenco di documenti.

1. Nella pagina di protezione dei documenti fare clic su Documenti.
1. Nell&#39;elenco Trova selezionare i criteri di ricerca richiesti.

   È possibile specificare i criteri come ID documento, nome documento, nome autore, ID criterio, nome criterio o tutti i documenti.

   Se si specifica il nome dell&#39;autore, fare clic sull&#39;icona Rubrica e specificare il dominio in cui si desidera eseguire la ricerca nell&#39;utente, quindi scegliere OK per tornare alla pagina di ricerca Documenti.

1. (Facoltativo) Nell’elenco Data, seleziona un’opzione per l’intervallo di date. Se selezioni Date personalizzate, digita la data in formato aaaa/mm/gg nelle caselle visualizzate oppure utilizza il Selettore data per specificare l’intervallo di date:

   * Fai clic sul calendario per aprire il Selettore data.
   * Utilizzare le frecce per trovare un anno e un mese.
   * Fare clic su un giorno del mese nel calendario.
   * Fare clic su OK per chiudere il selettore data.

1. Fai clic su Trova.

## Ordinare l&#39;elenco dei documenti {#sort-the-document-list}

È possibile ordinare l&#39;elenco dei documenti in base all&#39;intestazione di colonna. Le icone triangolari accanto all’intestazione della colonna indicano la colonna attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l&#39;alto indica un ordine crescente, mentre un triangolo rivolto verso il basso indica un ordine decrescente.

1. Nella pagina di protezione dei documenti fare clic su Documenti.
1. Fare clic sull&#39;intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai di nuovo clic sulla colonna.

## Aggiungi copertina a documenti protetti tramite policy {#add-cover-page-to-policy-protected-documents}

Se la maggior parte dei visualizzatori non è Adobe PDF, se apri un documento protetto tramite Document Security la prima pagina viene visualizzata come pagina vuota o l’applicazione viene interrotta senza aprire il documento.

È possibile utilizzare il supporto Page 0 (Wrapper Document) per consentire ai visualizzatori non Adobe PDF di aprire un documento protetto e di visualizzare una pagina di copertina nel documento.

>[!NOTE]
>
>Quando si visualizzano tali documenti (contenenti una pagina 0) in Adobe Reader/Acrobat o in un Reader mobile, il documento protetto viene aperto per impostazione predefinita.

**Per aggiungere una pagina di copertina a un documento protetto tramite policy**

Utilizza i seguenti processi in Workbench:

**Documento Protect con copertina:** Protegge un documento PDF con la policy specificata e aggiunge una pagina di copertina al documento

**Estrai documento protetto:** Estrae il documento PDF protetto tramite policy dal documento PDF con la pagina di copertina

Utilizza le seguenti API di Document Security:

**protectDocumentWithCoverPage:** Protegge un determinato PDF con la policy specificata e restituisce un documento con una pagina di copertina e il documento protetto come allegato
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** Estrae il documento protetto che è un allegato del documento con la pagina di copertina. È possibile creare il documento con la pagina di copertina utilizzando il metodo protectDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
