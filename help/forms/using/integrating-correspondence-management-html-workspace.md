---
title: Integrazione di applicazioni di terze parti nell’area di lavoro AEM Forms
seo-title: Integrazione di applicazioni di terze parti nell’area di lavoro AEM Forms
description: Integrare applicazioni di terze parti, ad esempio Gestione della corrispondenza nell'area di lavoro AEM Forms.
seo-description: Come integrare app di terze parti come Gestione della corrispondenza nell'area di lavoro AEM Forms.
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Integrazione di applicazioni di terze parti nell’area di lavoro AEM Forms{#integrating-third-party-applications-in-aem-forms-workspace}

L&#39;area di lavoro AEM Forms supporta la gestione delle attività di assegnazione e completamento per moduli e documenti. Tali moduli e documenti possono essere moduli XDP, Flex® o Guide (obsoleto) per i quali è stato eseguito il rendering in formato XDP, PDF, HTML o Flex.

Tali capacità sono ulteriormente migliorate. I AEM Forms ora supportano la collaborazione con applicazioni di terze parti che supportano funzionalità simili all&#39;area di lavoro AEM Forms. Una parte comune di questa funzionalità è rappresentata dal flusso di lavoro dell&#39;assegnazione e successiva approvazione di un&#39;attività. I AEM Forms offrono un&#39;unica esperienza unificata agli utenti enterprise di AEM Forms, in modo che tutte le assegnazioni di attività o approvazioni per le applicazioni supportate possano essere gestite tramite l&#39;area di lavoro AEM Forms.

Ad esempio, consideriamo la gestione della corrispondenza come esempio di riferimento per l’integrazione con l’area di lavoro AEM Forms. Gestione corrispondenza ha il concetto di &quot;Lettera&quot;, che può essere rappresentata e consente azioni.

## Creare le risorse Gestione corrispondenza {#create-correspondence-management-assets}

Per iniziare, create un modello di gestione della corrispondenza di esempio di cui viene eseguito il rendering nell&#39;area di lavoro AEM Forms. Per ulteriori dettagli, vedere [Creare un modello](../../forms/using/create-letter.md)di lettera.

Per verificare se il rendering del modello di gestione della corrispondenza può essere eseguito correttamente, accedete al modello di gestione della corrispondenza nel relativo URL. L&#39;URL ha un pattern simile a `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

dove `encodedLetterId` è l’ID lettera con codifica URL. Quando si definisce il processo di rendering per l&#39;attività dell&#39;area di lavoro in Workbench, specificare lo stesso ID lettera.

## Creazione di un’attività per il rendering e l’invio di una lettera in AEM Workspace {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

Prima di eseguire questi passaggi, accertatevi di essere membri dei seguenti gruppi:

* cm-agent-users
* Utenti Workspace

Per ulteriori informazioni, consultate [Aggiungere e configurare utenti](/help/forms/using/admin-help/adding-configuring-users.md).

Per creare un’attività di rendering e inviare una lettera in AEM Workspace, effettuate le seguenti operazioni:

1. Avviare Workbench. Accedete a localhost come amministratore.
1. Fate clic su File > Nuovo > Applicazione. Nel campo Nome applicazione, immettete `CMDemoSample` e fate clic su Fine.
1. Seleziona `CMDemoSample/1.0` e fai clic con il pulsante destro del mouse `NewProcess`. Nel campo del nome, immettere `CMRenderer` e fare clic su Fine.
1. Trascinate il selettore attività Punto iniziale e configuratelo:

   1. In Dati presentazione, selezionate Usa una risorsa CRX.

      ![useacrxasset](assets/useacrxasset.png)

   1. Cercate una risorsa. Nella finestra di dialogo Seleziona risorsa modulo, nella scheda Lettere sono elencate tutte le lettere presenti sul server.

      ![Scheda Lettera](assets/letter_tab_new.png)

   1. Selezionare la lettera appropriata e fare clic su **OK**.

1. Fate clic su Gestisci profili azione. Viene visualizzata la finestra di dialogo Gestisci profilo azione. Assicurarsi che le opzioni Processo di rendering e Processo di invio siano selezionate correttamente.
1. Per aprire la lettera con un file XML di dati, individuare e selezionare il file di dati appropriato nel processo Prepara dati.
1. Fai clic su OK.
1. Definire le variabili per Output punto iniziale e Allegati attività. Le variabili definite conterranno i dati Output punto iniziale e Allegati attività.
1. (Facoltativo) Per aggiungere un altro utente al flusso di lavoro, trascinate un selettore attività, configuratelo e assegnatelo a un utente. Scrivere un wrapper personalizzato (esempio riportato di seguito) oppure scaricare e installare il DSC (dato di seguito) per estrarre il modello Lettera, l&#39;Output Punto di Inizio e l&#39;Allegato Attività.

   Esempio di wrapper personalizzato:

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [Ottieni DSC](assets/dscsample.zip)download file: Un DSC di esempio è disponibile nel file DSCSample.zip allegato qui sopra. Scaricate e decomprimete il file DSCSample.zip. Prima di utilizzare il servizio DSC, è necessario configurarlo. Per informazioni, consultate [Configurare il servizio](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)DSC.

   Nella finestra di dialogo Definisci attività, selezionate l&#39;attività appropriata, ad esempio getLetterInstanceInfo, quindi fate clic su **OK**.

1. Implementare l&#39;applicazione. Se richiesto, archiviate e salvate le risorse.
1. Accedete all&#39;area di lavoro moduli di AEM all&#39;indirizzo https://&#39;[server]:[port]&#39;/lc/content/ws.
1. Aprite il compito aggiunto, CMRenderer. Viene visualizzata la lettera Gestione corrispondenza.

   ![cminworkspace](assets/cminworkspace.png)

1. Compila i dati richiesti e invia la lettera. La finestra si chiude. In questo processo, l&#39;attività viene assegnata all&#39;utente specificato nel flusso di lavoro nel passaggio 9.

   >[!NOTE]
   >
   >Il pulsante Invia non viene attivato finché non vengono compilate tutte le variabili richieste nella lettera.
