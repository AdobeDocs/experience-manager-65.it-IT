---
title: Controllo dell'accesso ai documenti protetti da policy
seo-title: Controllo dell'accesso ai documenti protetti da policy
description: Scopri come visualizzare, gestire e controllare l’accesso ai documenti protetti da policy.
seo-description: Scopri come visualizzare, gestire e controllare l’accesso ai documenti protetti da policy.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 0%

---


# Controllo dell&#39;accesso ai documenti protetti da policy {#controlling-access-to-policy-protected-documents}

Puoi controllare il modo in cui i destinatari utilizzano i documenti protetti da policy indipendentemente dalla loro diffusione.

Utilizzando la pagina Documenti è possibile eseguire le operazioni seguenti:

* Cercare e visualizzare i dettagli dei documenti protetti da policy. È possibile visualizzare informazioni sul nome del documento, il nome dell’editore, il nome del criterio e la data in cui il criterio è stato applicato. Se il criterio che ha protetto un documento viene eliminato, è anche possibile visualizzare l&#39;ID del criterio eliminato sotto il nome del criterio. Gli utenti possono visualizzare e gestire i propri documenti protetti da policy. Gli amministratori possono visualizzare e gestire tutti i documenti protetti da policy.
* Modificare i dettagli del criterio applicato a un documento. Gli utenti possono modificare i propri criteri, gli amministratori possono modificare i criteri condivisi e personali e i coordinatori dei set di criteri possono modificare i criteri condivisi nei set di criteri per i quali dispongono delle autorizzazioni. È possibile accedere al criterio associato a un documento direttamente dalla pagina Dettagli documento.
* Revoca e ripristina l&#39;accesso a un documento protetto da policy. Gli amministratori possono revocare e ripristinare l’accesso a qualsiasi documento. I coordinatori dei set di criteri (che dispongono dell&#39;autorizzazione per gestire i documenti) possono revocare e ripristinare l&#39;accesso ai documenti protetti da policy che utilizzano i criteri condivisi dai rispettivi set di criteri. Gli utenti possono revocare l&#39;accesso ai propri documenti protetti da policy se hanno creato il criterio che protegge il documento o se il criterio è condiviso che consente questa funzionalità.
* Cambiare il criterio applicato a un documento. Gli utenti che applicano i criteri ai documenti possono cambiare un criterio se lo hanno creato o se si tratta di un criterio condiviso che abilita questa funzionalità. I coordinatori dei set di criteri possono cambiare i criteri dai rispettivi set di criteri. Gli amministratori possono cambiare i criteri applicati a qualsiasi documento.

Quando un documento è protetto da un criterio e si revocano i privilegi di accesso o si cambia il criterio applicato, le modifiche hanno effetto come segue:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che l&#39;utente non abbia aperto il documento. In questo caso, l&#39;utente deve chiudere il documento per rendere effettive le modifiche.
* Se un destinatario utilizza il documento offline (ad esempio, su un computer portatile), le modifiche avranno effetto alla successiva sincronizzazione del destinatario con la protezione dei documenti aprendo qualsiasi documento protetto da policy.

## Visualizza informazioni su un documento {#view-information-about-a-document}

Per ogni documento elencato nella pagina Documenti, è possibile visualizzare il nome del documento, il nome dell&#39;autore, il nome del criterio e la data in cui il documento è stato protetto. Se il criterio che ha protetto un documento è stato eliminato, l&#39;ID del criterio è elencato in Nome criterio.

È inoltre possibile visualizzare ulteriori dettagli, descritti di seguito, su un particolare documento nella pagina Dettagli documento:

>[!NOTE]
>
>È necessario utilizzare il collegamento Nome criterio nella pagina Dettagli documento per accedere ai criteri generati automaticamente in Microsoft Outlook per i destinatari di un documento allegato a un messaggio e-mail. Questi criteri non vengono visualizzati nella pagina dei criteri.

**Nome documento:** il nome del documento selezionato.

**ID documento:** identificatore univoco assegnato dalla sicurezza del documento quando un criterio viene applicato al documento. document security utilizza questo numero per tenere traccia del documento.

**Stato documento:** stato del documento (ad esempio, attivo o revocato).

**Editore:** nome dell&#39;utente che ha allegato il criterio al documento.

**Nome criterio:** il nome del criterio utilizzato per proteggere il documento. Puoi fare clic sul nome per aprire il criterio. È necessario utilizzare questo collegamento per accedere ai criteri generati da Acrobat per i destinatari di un documento allegato a un messaggio di posta elettronica in Outlook. Tali criteri non vengono visualizzati nella pagina Criteri.

**Tipo di criterio:** il tipo di criterio applicato al documento.

**Data di pubblicazione:** la data in cui il criterio è stato applicato al documento.

**Iterazioni correlate:** se il documento contiene iterazioni correlate, anche questo elemento viene visualizzato nell’elenco. Fare clic sul collegamento per visualizzare l&#39;elenco delle iterazioni correlate al documento.

Gli utenti possono visualizzare informazioni sui documenti protetti. Gli amministratori possono visualizzare informazioni sui documenti protetti da un criterio da qualsiasi utente. I coordinatori dei set di criteri possono visualizzare le informazioni sui documenti protetti dai criteri dai rispettivi set di criteri.

1. Nella pagina Protezione documento fare clic su Documenti.
1. Nell&#39;elenco dei documenti fare clic sul documento appropriato. Viene visualizzata la pagina Dettagli documento contenente informazioni dettagliate sul documento. Questa pagina fornisce inoltre opzioni per revocare l’accesso ai documenti, cambiare il criterio e visualizzare gli eventi correlati a questo documento.

## Visualizzare le iterazioni correlate per un documento {#view-related-iterations-for-a-document}

Se è abilitato il tracciamento delle iterazioni correlate, puoi tenere traccia delle versioni di un documento salvate da diversi utenti. Questa funzione è supportata solo da alcune applicazioni, come PTC Pro/ENGINEER Wildfire.

Questa funzione è utile quando più utenti collaborano e salvano versioni diverse dello stesso documento. la sicurezza dei documenti può tenere traccia delle varie iterazioni; è quindi possibile visualizzare facilmente le informazioni relative ai documenti per le diverse versioni.

Se questa funzione è abilitata, è possibile visualizzare le iterazioni correlate di un documento dalla pagina Documenti.

1. Visualizzare la pagina Dettagli documento per un documento. (Vedere [Visualizzare informazioni su un documento](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. Fare clic su Visualizza iterazioni correlate. L’opzione è disponibile solo se la funzione è abilitata. Viene visualizzato l’elenco delle iterazioni correlate. Per ogni iterazione, puoi visualizzare le seguenti informazioni:

   * **Iterazione:** il nome del file. Può essere diverso dal nome del file originale e ha un numero di versione aggiunto alla fine di esso.
   * **Editore:** l&#39;editore del documento originale.
   * **Creato da:** l’utente che ha salvato l’iterazione.
   * **Data di creazione:** la data e l’ora in cui l’iterazione è stata salvata.
   * **Criterio:** il criterio che protegge l’iterazione. Le diverse iterazioni possono essere protette da politiche diverse.

1. Per visualizzare la pagina Dettagli documento relativa a tale iterazione, fare clic sul nome del file di un&#39;iterazione.

## Revoca e ripristino dell&#39;accesso ai documenti {#revoking-and-reinstating-access-to-documents}

È possibile revocare e ripristinare l&#39;accesso ai documenti protetti da policy:

**Utenti:** possono revocare o ripristinare l’accesso ai documenti che proteggono con i propri criteri personali o con quelli condivisi per i quali la funzionalità di revoca è abilitata per l’utente che applica il criterio. Gli utenti che non possono revocare l&#39;accesso a un documento o cambiare un criterio devono contattare l&#39;amministratore.

**Amministratori:** possono revocare o ripristinare i privilegi di accesso a qualsiasi documento protetto da policy, inclusi quelli protetti da policy personali o condivise. Se un amministratore revoca l&#39;accesso a un documento protetto da un criterio condiviso, solo un amministratore può ripristinare i privilegi di accesso per quel documento.

**Coordinatori set di criteri:** può revocare o ripristinare i privilegi di accesso per i documenti protetti dai set di criteri.

Quando si revocano o si ripristinano i privilegi di accesso ai documenti, la modifica ha effetto nei seguenti momenti:

* Se il documento è online e chiuso, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione del documento aprendo un documento protetto da policy.
* Se il documento è online e aperto, la modifica ha effetto quando il destinatario chiude il documento.
* Se il documento è offline (in uso senza una connessione Internet, ad esempio su un computer portatile), la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione dei documenti.

**Revoca dell&#39;accesso a un documento protetto da policy**

1. Nella pagina Protezione documento fare clic su Documenti.
1. Selezionare la casella di controllo accanto al documento appropriato e fare clic su Revoca. È possibile revocare l’accesso a più documenti alla volta.
1. Selezionare un messaggio da visualizzare agli utenti che tentano di aprire il documento dopo la revoca:

   * **Messaggio generale:** indica che l’autore ha revocato il documento
   * **Documento terminato:** indica che l&#39;autore ha terminato il documento
   * **Documento revisionato**: Indica che l&#39;autore ha rivisto il documento

1. (Facoltativo) Se è disponibile una versione più recente del documento, immetti l’URL e fai clic su Prova per verificare l’URL.
1. Fare clic su OK, quindi di nuovo su OK per tornare alla pagina Documenti.

**Ripristino dei privilegi di accesso ai documenti**

1. Nella pagina Protezione documento fare clic su Documenti.
1. Nell&#39;elenco dei documenti fare clic sul documento appropriato.
1. Fare clic su Annulla revoca e quindi su OK.

## Cambiare un criterio applicato a un documento {#switch-a-policy-that-is-applied-to-a-document}

Gli utenti, i coordinatori dei set di criteri e gli amministratori possono cambiare il criterio applicato a un documento protetto da policy (è possibile applicare un solo criterio alla volta a un documento). Gli utenti possono cambiare i criteri applicati ai propri documenti protetti da policy se hanno creato il criterio o se il criterio è condiviso con questa funzionalità abilitata. In caso contrario, l&#39;amministratore o il coordinatore del set di criteri devono cambiare il criterio. Gli amministratori possono cambiare criteri per qualsiasi documento protetto da policy dell’utente. I coordinatori dei set di criteri possono cambiare i criteri dai rispettivi set di criteri.

Quando si cambia un criterio, il nuovo criterio viene applicato come segue:

* Se il documento è online e chiuso, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione del documento aprendo qualsiasi documento protetto da policy online.
* Se il documento è online e aperto, la modifica ha effetto quando l&#39;utente chiude il documento.
* Se il documento è offline (in uso senza una connessione Internet o di rete attiva, ad esempio su un computer portatile), la modifica viene applicata alla successiva sincronizzazione dell&#39;utente con la protezione dei documenti aprendo un documento protetto da policy online.

>[!NOTE]
>
>Per consentire l&#39;accesso anonimo a un documento protetto da policy che attualmente non dispone di questo accesso, rimuovere il criterio esistente nell&#39;applicazione client e quindi applicare un criterio che consenta l&#39;accesso anonimo. Se si cambia il criterio, gli utenti devono comunque accedere al documento.

1. Nella pagina Protezione documento fare clic su Documenti.
1. Nell&#39;elenco dei documenti fare clic sul documento appropriato.
1. Fare clic su Cambia criterio. Viene visualizzato un elenco di fino a 100 criteri.
1. Se il criterio desiderato non è visualizzato, selezionare Nome criterio o ID criterio dall&#39;elenco Trova, digitare il nome o l&#39;ID e fare clic su Trova.
1. Fare clic su un nuovo criterio nell&#39;elenco.
1. Fare clic su Cambia criterio e quindi su OK per tornare alla pagina Documenti.

## Cerca un documento {#search-for-a-document}

È possibile cercare documenti nella pagina Documenti utilizzando una combinazione di criteri di intervallo di date e di criteri di ricerca disponibili nell’elenco. Questi criteri includono il nome del documento, il nome del criterio o tutti i documenti.

Alcune opzioni di ricerca aggiuntive sono disponibili solo per gli amministratori:

**ID documento:** numero ID univoco assegnato alla sicurezza del documento quando viene applicato il criterio.

**Nome del documento:** nome del documento.

**Nome editore:** nome dell&#39;utente che ha allegato il criterio al documento. Puoi selezionare l’utente da tutti i domini o da un dominio specificato.

**ID criterio:** numero ID del criterio allegato al documento.

**Nome criterio:** nome del criterio associato al documento.

**Tutti i documenti:** tutti i documenti protetti da amministratori e utenti. L&#39;utilizzo dell&#39;opzione Tutti i documenti per la ricerca potrebbe restituire un lungo elenco di documenti.

1. Nella pagina Protezione documento fare clic su Documenti.
1. Nell’elenco Trova, selezionare i criteri di ricerca richiesti.

   È possibile specificare i criteri come ID documento, nome documento, nome editore, ID criterio, nome criterio o tutti i documenti.

   Se si specifica il nome dell&#39;editore, fare clic sull&#39;icona Rubrica e specificare il dominio in cui si desidera cercare l&#39;utente, quindi fare clic su OK per tornare alla pagina di ricerca Documenti.

1. (Facoltativo) Nell’elenco Data, selezionare un’opzione relativa all’intervallo di date. Se si seleziona Date personalizzate, digitare la data nel formato aaaa/mm/gg nelle caselle visualizzate o utilizzare il Selettore data per specificare l&#39;intervallo di date:

   * Fare clic sul calendario per aprire il selettore data.
   * Usa le frecce per trovare un anno e un mese.
   * Fai clic su un giorno del mese nel calendario.
   * Fare clic su OK per chiudere il selettore data.

1. Fare clic su Trova.

## Ordinare l&#39;elenco dei documenti {#sort-the-document-list}

È possibile ordinare l’elenco dei documenti in base all’intestazione della colonna. Le icone a triangolo accanto all’intestazione della colonna indicano quale colonna è attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l&#39;alto indica l&#39;ordine crescente, mentre un triangolo rivolto verso il basso indica l&#39;ordine decrescente.

1. Nella pagina Protezione documento fare clic su Documenti.
1. Fai clic sull’intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fai nuovamente clic sulla colonna .

## Aggiungi la copertina ai documenti protetti da policy {#add-cover-page-to-policy-protected-documents}

Nel caso della maggior parte dei visualizzatori non Adobe PDF, se si apre un documento protetto dalla sicurezza dei documenti, la prima pagina viene visualizzata come pagina vuota oppure l&#39;applicazione si interrompe senza aprire il documento.

È possibile utilizzare il supporto Pagina 0 (documento wrapper) per consentire ai visualizzatori non Adobe PDF di aprire un documento protetto e visualizzare una copertina nel documento.

>[!NOTE]
>
>Quando si visualizzano tali documenti (contenenti una pagina 0) in Adobe Reader/Acrobat o nel Reader Mobile, il documento protetto viene aperto per impostazione predefinita.

**Per aggiungere una copertina a un documento protetto da criteri**

Utilizzare i seguenti processi in workbench:

**Documento Protect con copertina:** protegge un documento PDF con il criterio specificato e aggiunge una copertina al documento

**Estrai documento protetto:** estrae il documento PDF protetto da policy dal documento PDF con copertina

Utilizza le seguenti API di protezione dei documenti:

**protectDocumentWithCoverPage:** protegge un dato PDF con il criterio specificato e restituisce un documento con una copertina e il documento protetto come un 
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **estratto allegatoProtectedDocument:** Estrae il documento protetto che è un allegato nel documento con copertina. È possibile creare il documento con la copertina utilizzando il metodo protectDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`