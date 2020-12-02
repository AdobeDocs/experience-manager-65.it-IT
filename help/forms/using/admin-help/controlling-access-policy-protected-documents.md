---
title: Controllo dell'accesso ai documenti protetti tramite criterio
seo-title: Controllo dell'accesso ai documenti protetti tramite criterio
description: Scopri come visualizzare, gestire e controllare l'accesso ai documenti protetti tramite criterio.
seo-description: Scopri come visualizzare, gestire e controllare l'accesso ai documenti protetti tramite criterio.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2188'
ht-degree: 0%

---


# Controllo dell&#39;accesso ai documenti protetti tramite criterio {#controlling-access-to-policy-protected-documents}

Puoi controllare il modo in cui i destinatari utilizzano i documenti protetti tramite criterio, indipendentemente dalla loro diffusione.

Utilizzando la pagina Documenti è possibile effettuare le seguenti operazioni:

* Cercare e visualizzare i dettagli dei documenti protetti tramite criterio. Potete visualizzare informazioni sul nome del documento, il nome dell&#39;editore, il nome del criterio e la data in cui il criterio è stato applicato. Se il criterio che ha protetto un documento viene eliminato, potete anche visualizzare l&#39;ID del criterio eliminato sotto il nome del criterio. Gli utenti possono visualizzare e gestire i propri documenti protetti tramite criterio. Gli amministratori possono visualizzare e gestire tutti i documenti protetti tramite criterio.
* Modificare i dettagli del criterio applicato a un documento. Gli utenti possono modificare i propri criteri, gli amministratori possono modificare i criteri condivisi e personali, e i coordinatori dei set di criteri possono modificare i criteri condivisi nei set di criteri per i quali dispongono delle autorizzazioni. Potete accedere al criterio associato a un documento direttamente dalla pagina Dettagli documento.
* Revocare e ripristinare l&#39;accesso a un documento protetto tramite criterio. Gli amministratori possono revocare e ripristinare l&#39;accesso a qualsiasi documento. I coordinatori dei set di criteri (che dispongono dell&#39;autorizzazione per gestire i documenti) possono revocare e ripristinare l&#39;accesso ai documenti protetti tramite criterio che utilizzano i criteri condivisi dai rispettivi set di criteri. Gli utenti possono revocare l&#39;accesso ai documenti protetti tramite criterio se hanno creato il criterio che protegge il documento o se il criterio è condiviso che consente tale funzionalità.
* Cambiare il criterio applicato a un documento. Gli utenti che applicano i criteri ai documenti possono cambiare il criterio se lo hanno creato o se è un criterio condiviso che abilita questa funzionalità. I coordinatori di set di criteri possono cambiare i criteri dai rispettivi set di criteri. Gli amministratori possono cambiare criteri applicati a qualsiasi documento.

Quando un documento è protetto da un criterio e revocate i privilegi di accesso o modificate il criterio applicato, le modifiche hanno effetto come segue:

* Se il documento è online, le modifiche vengono applicate immediatamente a meno che l&#39;utente non abbia aperto il documento. In questo caso, per rendere effettive le modifiche, l&#39;utente deve chiudere il documento.
* Se un destinatario utilizza il documento offline (ad esempio, su un computer portatile), le modifiche avranno effetto alla successiva sincronizzazione del destinatario con la protezione del documento aprendo qualsiasi documento protetto tramite criterio.

## Visualizzazione delle informazioni su un documento {#view-information-about-a-document}

Per ciascun documento elencato nella pagina Documenti è possibile visualizzare il nome del documento, il nome dell&#39;editore, il nome del criterio e la data in cui il documento è stato protetto. Se il criterio che ha protetto un documento è stato eliminato, l&#39;ID del criterio è elencato in Nome criterio.

Potete anche visualizzare ulteriori dettagli, descritti di seguito, su un particolare documento nella pagina Dettagli documento:

>[!NOTE]
>
>È necessario utilizzare il collegamento Nome criterio nella pagina Dettagli documento per accedere ai criteri generati automaticamente in Microsoft Outlook per i destinatari di un documento allegato a un messaggio e-mail. Questi criteri non vengono visualizzati nella pagina dei criteri.

**Nome documento:** il nome del documento selezionato.

**ID documento:** identificatore univoco assegnato dalla protezione del documento quando viene applicato un criterio al documento. document security utilizza questo numero per tenere traccia del documento.

**Stato documento:** Stato del documento (ad esempio, attivo o revocato).

**Editore:** nome dell&#39;utente che ha allegato il criterio al documento.

**Nome criterio:** il nome del criterio utilizzato per proteggere il documento. Potete fare clic sul nome per aprire il criterio. È necessario utilizzare questo collegamento per accedere ai criteri che  Acrobat genera per i destinatari di un documento allegato a un messaggio e-mail in Outlook. Tali criteri non vengono visualizzati nella pagina Criteri.

**Tipo di criterio:** tipo di criterio applicato al documento.

**Data pubblicazione:** la data in cui il criterio è stato applicato al documento.

**Iterazioni correlate:** se il documento contiene iterazioni correlate, anche questo elemento viene visualizzato nell&#39;elenco. Fare clic sul collegamento per visualizzare l&#39;elenco delle relative iterazioni per il documento.

Gli utenti possono visualizzare informazioni sui documenti protetti. Gli amministratori possono visualizzare informazioni sui documenti protetti da qualsiasi utente tramite un criterio. I coordinatori dei set di criteri possono visualizzare informazioni sui documenti protetti dai criteri dai relativi set di criteri.

1. Nella pagina di protezione del documento, fare clic su Documenti.
1. Nell’elenco dei documenti, fare clic sul documento appropriato. Viene visualizzata la pagina Dettagli documento in cui sono visualizzate informazioni dettagliate sul documento. Questa pagina fornisce inoltre opzioni per revocare l&#39;accesso al documento, cambiare il criterio e visualizzare gli eventi relativi a questo documento.

## Visualizzare le iterazioni correlate per un documento {#view-related-iterations-for-a-document}

Se è abilitato il tracciamento delle iterazioni correlate, è possibile tenere traccia delle versioni di un documento salvate da diversi utenti. Questa funzione è supportata solo da alcune applicazioni, come PTC Pro/ENGINEER Wildfire.

Questa funzione è utile quando più utenti collaborano e salvano versioni diverse dello stesso documento. la sicurezza dei documenti può tenere traccia delle varie fasi; pertanto, è possibile visualizzare facilmente le informazioni relative ai documenti per le diverse versioni.

Se questa funzione è abilitata, è possibile visualizzare le relative iterazioni di un documento dalla pagina Documenti.

1. Visualizzare la pagina Dettagli documento per un documento. (Vedere [Visualizzare informazioni su un documento](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. Fate clic su Visualizza iterazioni correlate. L&#39;opzione è disponibile solo se la funzione è attivata. Viene visualizzato l&#39;elenco delle iterazioni correlate. Per ogni iterazione, potete visualizzare le seguenti informazioni:

   * **Iterazione:** Il nome del file. Può essere diverso dal nome del file originale e alla fine può essere aggiunto un numero di versione.
   * **Editore:** l&#39;editore del documento originale.
   * **Creato da:** l&#39;utente che ha salvato l&#39;iterazione.
   * **Data di creazione:** la data e l’ora in cui è stata salvata l’iterazione.
   * **Criteri:** il criterio che protegge l&#39;iterazione. Diverse iterazioni possono essere protette da criteri diversi.

1. Per visualizzare la pagina Dettagli documento relativa a tale iterazione, fare clic sul nome del file di un&#39;iterazione.

## Ripristino e ripristino dell&#39;accesso ai documenti {#revoking-and-reinstating-access-to-documents}

Potete revocare e ripristinare l&#39;accesso ai documenti protetti tramite criterio:

**Utenti:** può revocare o ripristinare l&#39;accesso ai documenti che proteggono con i propri criteri personali o con i criteri condivisi per i quali la funzionalità di revoca è abilitata per l&#39;utente che applica il criterio. Gli utenti che non possono revocare l&#39;accesso a un documento o cambiare criterio devono contattare l&#39;amministratore.

**Amministratori:** possono revocare o ripristinare i privilegi di accesso a qualsiasi documento protetto tramite criterio, inclusi quelli protetti tramite criteri personali o condivisi. Se un amministratore revoca l&#39;accesso a un documento protetto tramite un criterio condiviso, solo un amministratore può ripristinare i privilegi di accesso per tale documento.

**Coordinatori set di criteri:** può revocare o ripristinare i privilegi di accesso per i documenti protetti dai set di criteri.

Quando si revocano o si ripristinano i privilegi di accesso ai documenti, la modifica ha effetto al momento seguente:

* Se il documento è online e chiuso, la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione del documento aprendo un documento protetto tramite criterio.
* Se il documento è online e aperto, la modifica ha effetto alla chiusura del documento da parte del destinatario.
* Se il documento è offline (in uso senza una connessione Internet, ad esempio su un computer portatile), la modifica ha effetto alla successiva sincronizzazione del destinatario con la protezione del documento.

**Revoca dell&#39;accesso a un documento protetto tramite criterio**

1. Nella pagina di protezione del documento, fare clic su Documenti.
1. Selezionate la casella di controllo accanto al documento appropriato e fate clic su Revoca. Potete revocare l&#39;accesso a più documenti alla volta.
1. Selezionate un messaggio da visualizzare agli utenti che cercano di aprire il documento dopo la revoca:

   * **Messaggio generale:** indica che l&#39;autore ha revocato il documento
   * **Documento terminato:** Indica che l&#39;autore ha terminato il documento
   * **Documento revisionato**: Indica che l&#39;autore ha rivisto il documento

1. (Facoltativo) Se è disponibile una versione più recente del documento, immettete l’URL e fate clic su Prova per verificare l’URL.
1. Fare clic su OK, quindi di nuovo su OK per tornare alla pagina Documenti.

**Ripristino dei privilegi di accesso ai documenti**

1. Nella pagina di protezione del documento, fare clic su Documenti.
1. Nell’elenco dei documenti, fare clic sul documento appropriato.
1. Fate clic su Annulla revoca, quindi su OK.

## Cambiare un criterio applicato a un documento {#switch-a-policy-that-is-applied-to-a-document}

Utenti, coordinatori di set di criteri e amministratori possono cambiare il criterio applicato a un documento protetto tramite criterio (è possibile applicare un solo criterio alla volta a un documento). Gli utenti possono cambiare criteri applicati ai propri documenti protetti tramite criterio se hanno creato il criterio o se il criterio è condiviso con questa funzionalità abilitata. In caso contrario, l&#39;amministratore o il coordinatore del set di criteri deve cambiare criterio. Gli amministratori possono cambiare criteri per qualsiasi documento protetto tramite criterio dell&#39;utente. I coordinatori di set di criteri possono cambiare i criteri dai rispettivi set di criteri.

Quando cambiate un criterio, il nuovo criterio viene applicato come segue:

* Se il documento è online e chiuso, la modifica ha effetto alla successiva sincronizzazione del destinatario con Document Security aprendo qualsiasi documento protetto tramite criterio online.
* Se il documento è online e aperto, la modifica ha effetto alla chiusura del documento da parte dell&#39;utente.
* Se il documento è offline (in uso senza una connessione Internet o di rete attiva, ad esempio su un computer portatile), la modifica verrà applicata alla successiva sincronizzazione dell&#39;utente con la protezione dei documenti aprendo online un documento protetto tramite criterio.

>[!NOTE]
>
>Per consentire l&#39;accesso anonimo a un documento protetto tramite criterio che attualmente non dispone di tale accesso, rimuovere il criterio esistente nell&#39;applicazione client e applicare un criterio che consenta l&#39;accesso anonimo. Se cambiate il criterio, gli utenti devono comunque accedere al documento.

1. Nella pagina di protezione del documento, fare clic su Documenti.
1. Nell’elenco dei documenti, fare clic sul documento appropriato.
1. Fate clic su Cambia criterio. Viene visualizzato un elenco di fino a 100 criteri.
1. Se il criterio desiderato non è visualizzato, selezionate Nome criterio o ID criterio dall&#39;elenco Trova, digitate il nome o l&#39;ID e fate clic su Trova.
1. Fare clic su un nuovo criterio nell&#39;elenco.
1. Fare clic su Cambia criterio, quindi su OK per tornare alla pagina Documenti.

## Cercare un documento {#search-for-a-document}

È possibile cercare documenti nella pagina Documenti utilizzando una combinazione di criteri per l&#39;intervallo di date e di criteri di ricerca disponibili nell&#39;elenco. Tali criteri includono il nome del documento, il nome del criterio o tutti i documenti.

Alcune opzioni di ricerca aggiuntive sono disponibili solo per gli amministratori:

**ID documento: numero ID** univoco che la protezione del documento assegna al documento quando viene applicato il criterio.

**Nome documento:** Nome del documento.

**Nome editore:** nome dell&#39;utente che ha allegato il criterio al documento. Puoi selezionare l&#39;utente da tutti i domini o da un dominio specificato.

**ID criterio: numero** ID del criterio associato al documento.

**Nome criterio:** nome del criterio associato al documento.

**Tutti i documenti:** Tutti i documenti protetti da amministratori e utenti. L&#39;opzione Tutti i documenti da cercare può restituire un lungo elenco di documenti.

1. Nella pagina di protezione del documento, fare clic su Documenti.
1. Nell&#39;elenco Trova, selezionare i criteri di ricerca richiesti.

   Potete specificare i criteri come ID documento, nome documento, nome editore, ID criterio, nome criterio o tutti i documenti.

   Se si specifica il nome dell&#39;editore, fare clic sull&#39;icona Rubrica e specificare il dominio in cui eseguire la ricerca per l&#39;utente, quindi fare clic su OK per tornare alla pagina di ricerca Documenti.

1. (Facoltativo) Nell&#39;elenco Data, selezionare un&#39;opzione per l&#39;intervallo di date. Se si seleziona Data personalizzata, digitare la data nel formato yyyy/mm/dd nelle caselle visualizzate oppure utilizzare il Selettore data per specificare l&#39;intervallo di date:

   * Fate clic sul calendario per aprire il selettore data.
   * Usate le frecce per trovare un anno e un mese.
   * Fare clic su un giorno del mese nel calendario.
   * Fate clic su OK per chiudere il selettore data.

1. Fate clic su Trova.

## Ordinare l&#39;elenco dei documenti {#sort-the-document-list}

È possibile ordinare l’elenco di documenti per intestazione di colonna. Le icone a triangolo accanto all’intestazione della colonna indicano quale colonna è attualmente utilizzata per l’ordinamento. Un triangolo rivolto verso l’alto indica l’ordine crescente, mentre un triangolo rivolto verso il basso indica l’ordine decrescente.

1. Nella pagina di protezione del documento, fare clic su Documenti.
1. Fare clic sull&#39;intestazione di colonna appropriata.
1. Per modificare l’ordinamento, fate di nuovo clic sulla colonna.

## Aggiungere una copertina ai documenti protetti tramite criterio {#add-cover-page-to-policy-protected-documents}

Nel caso della maggior parte dei visualizzatori Adobe PDF non , se aprite un documento protetto da protezione del documento, la prima pagina viene visualizzata come pagina vuota oppure l&#39;applicazione si interrompe senza aprire il documento.

Potete utilizzare il supporto Pagina 0 (documento wrapper) per consentire ai visualizzatori Adobe PDF non  di aprire un documento protetto e visualizzare una copertina nel documento.

>[!NOTE]
>
>Quando si visualizzano tali documenti (contenenti una pagina 0) in  Adobe Reader/ Acrobat o in Reader Mobile, il documento protetto viene aperto per impostazione predefinita.

**Per aggiungere una copertina a un documento protetto tramite criterio**

Utilizzare i seguenti processi in workbench:

**Protect Document With Cover Page:** Protegge un documento PDF con il criterio specificato e aggiunge una copertina al documento

**Estrai documento protetto:** estrae il documento PDF protetto tramite criterio dal documento PDF con la copertina

Utilizzate le seguenti API per la protezione dei documenti:

**protectDocumentWithCoverPage:** protegge un PDF specificato con il criterio specificato e restituisce un documento con una copertina e il documento protetto come allegato 
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** estrae il documento protetto che è un allegato nel documento con copertina. Il documento con la copertina può essere creato utilizzando il metodo protectDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`