---
title: Flusso di lavoro incentrato su Forms su OSGi - Riferimento dettagliato
seo-title: Forms-centric workflow on OSGi - Step Reference
description: I passaggi OSGi di Forms-centric consentono di creare rapidamente flussi di lavoro basati su moduli adattivi.
seo-description: Forms-centric workflow on OSGi steps allow you rapidly build adaptive forms based workflows.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
exl-id: 470fcfda-dfde-437c-b539-d5af1e13a7d6
source-git-commit: de7b1d2d0f3863f9554b346204c18cc57d4bf814
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# Flusso di lavoro incentrato su Forms su OSGi - Riferimento dettagliato {#forms-centric-workflow-on-osgi-step-reference}

I modelli di flusso di lavoro consentono di convertire una logica di business in un processo ripetitivo automatizzato. Un modello consente di definire ed eseguire una serie di passaggi. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o se utilizza più risorse. È possibile [includere vari passaggi del flusso di lavoro AEM in un modello per raggiungere la logica di business](/help/sites-developing/workflows-models.md#extending-aem).

## Passaggi Forms Workflow {#forms-workflow-steps}

I passaggi del flusso di lavoro Forms eseguono operazioni specifiche per AEM Forms in un flusso di lavoro AEM. Questi passaggi ti consentono di creare rapidamente flussi di lavoro incentrati su Forms basati su moduli adattivi su OSGi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di revisione e approvazione di base, processi aziendali interni e tra firewall. È inoltre possibile utilizzare i passaggi di Forms Workflow per avviare document services, integrarsi con il flusso di lavoro della firma Adobe Sign ed eseguire altre operazioni AEM Forms. Richiedi [Componente aggiuntivo AEM Forms](https://www.adobe.com/go/learn_aemforms_documentation_63) per utilizzare questi passaggi in un flusso di lavoro.

I passaggi del flusso di lavoro incentrati su Forms eseguono operazioni specifiche di AEM Forms in un flusso di lavoro AEM. Questi passaggi ti consentono di creare rapidamente un flusso di lavoro basato su Forms adattivo basato su Forms su OSGi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di base per la revisione e l’approvazione, processi aziendali interni e attraverso il firewall.

>[!NOTE]
>
>Se il modello di flusso di lavoro è contrassegnato per uno storage esterno, per tutti i passaggi del flusso di lavoro Forms è possibile selezionare solo l&#39;opzione variabile per archiviare o recuperare file di dati e allegati.

## Assegna passaggio attività {#assign-task-step}

Il passaggio dell&#39;attività di assegnazione crea un&#39;attività e la assegna a un utente o a un gruppo. Oltre ad assegnare l’attività, il componente specifica anche il modulo adattivo o PDF non interattivo per l’attività. Il modulo adattivo è necessario per accettare l’input degli utenti e PDF non interattivo o un modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di sola revisione.

È inoltre possibile utilizzare il componente per controllare il comportamento dell’attività. Ad esempio, creazione di un documento di record automatico, assegnazione dell&#39;attività a un utente o a un gruppo specifico, specifica il percorso dei dati inviati, specifica il percorso dei dati da precompilare e specifica le azioni predefinite. Il passaggio Assegna attività ha le seguenti proprietà:

* **Titolo:** Titolo dell’attività. Il titolo viene visualizzato in AEM casella in entrata.
* **Descrizione:** Spiegazione delle operazioni eseguite nell&#39;attività. Queste informazioni sono utili per altri sviluppatori di processi quando lavori in un ambiente di sviluppo condiviso.

* **Percorso miniature:** Percorso della miniatura dell&#39;attività. Se non viene specificato alcun percorso, per una miniatura predefinita di un modulo adattivo e per Documento di record viene visualizzata un’icona predefinita.
* **Fase del flusso di lavoro:** Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata AEM. Puoi definire questi stadi nelle proprietà del modello (Barra laterale > Pagina > Proprietà pagina > Stadi).
* **Priorità:** La priorità selezionata viene visualizzata nella casella in entrata AEM. Le opzioni disponibili sono Alta, Media e Bassa. Il valore predefinito è Medio.
* **Data di scadenza:** Specificare il numero di giorni o ore dopo le quali l&#39;attività è contrassegnata come scaduta. Se si seleziona **Disattivato**, quindi l&#39;attività non viene mai contrassegnata come scaduta. È inoltre possibile specificare un gestore di timeout per eseguire attività specifiche dopo la scadenza dell&#39;attività.

* **Giorni:** Numero di giorni precedenti al completamento dell&#39;attività. Il numero di giorni conteggiati dopo l’assegnazione dell’attività a un utente. Se un&#39;attività non è completa e supera il numero di giorni specificato nel campo Giorni, se selezionato, viene attivato un gestore di timeout dopo la data di scadenza.
* **Ore:** Numero di ore prima del completamento dell&#39;attività. Il numero di ore viene conteggiato dopo che l’attività è stata assegnata a un utente. Se un&#39;attività non è completa e supera il numero di ore specificato nel campo Ore, se selezionato, viene attivato un gestore di timeout dopo le ore di scadenza.
* **Timeout dopo la data di scadenza:** Selezionare questa opzione per abilitare il campo di selezione Gestore timeout.
* **Gestore di timeout:** Selezionare lo script da eseguire quando la fase dell&#39;attività di assegnazione supera la data di scadenza. Script inseriti nell’archivio CRX in [app]/fd/dashboard/scripts/timeoutHandler sono disponibili per la selezione. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo.
* **Evidenziare l&#39;azione e il commento dell&#39;ultima attività in Dettagli attività:** Selezionare questa opzione per visualizzare l’ultima azione eseguita e il commento ricevuto sulla sezione dei dettagli dell’attività di un’attività.
* **Tipo:** Scegliere il tipo di documento da compilare all&#39;avvio del flusso di lavoro. È possibile scegliere un modulo adattivo, un modulo adattivo di sola lettura, un documento PDF non interattivo, l’interfaccia utente di Interactive Communication Agent o il documento del canale Web di comunicazione interattiva.
* **Usa modulo adattivo:** Specifica il metodo per individuare il modulo adattivo di input. Questa opzione è disponibile se si seleziona Modulo adattivo o Modulo adattivo di sola lettura dall’elenco a discesa Tipo . Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso.\
   È possibile associare più moduli adattivi a un flusso di lavoro. Di conseguenza, è possibile specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

* **Usa comunicazione interattiva:** Specificare il metodo per individuare la comunicazione interattiva di input. Puoi utilizzare la comunicazione interattiva inviata al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso. Questa opzione è disponibile se si seleziona Interfaccia utente di Interactive Communication Agent o Documento canale Web di comunicazione interattiva dall’elenco a discesa Tipo.

>[!NOTE]
>
>Per accedere all’interfaccia utente di Interactive Communications Agent nella casella in entrata è necessario disporre di assegnazioni di gruppi di utenti e utenti di un agente cm-agent e di un gruppo di utenti del flusso di lavoro.

* **Percorso di comunicazione o modulo adattivo**: Specifica il percorso del modulo adattivo o della comunicazione interattiva. Puoi utilizzare il modulo adattivo o la comunicazione interattiva inviata al flusso di lavoro, disponibile in un percorso assoluto, oppure recuperare il modulo adattivo da un percorso memorizzato in una variabile di tipo dati stringa.
* **Seleziona PDF di input utilizzando:** Specifica il percorso di un documento PDF non interattivo. Il campo è disponibile quando si sceglie un documento PDF non interattivo nel campo Tipo. È possibile selezionare il PDF di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio: [Payload_Directory]/Workflow/PDF/credit-card.pdf. Il percorso non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Per utilizzare l’opzione Percorso di PDF è necessario abilitare l’opzione Documento di record o i moduli adattivi basati su modelli di modulo.
* **Per l’attività completata, esegui il rendering del modulo adattivo come**: Quando un’attività è contrassegnata come completa, è possibile eseguire il rendering del modulo adattivo come modulo adattivo di sola lettura o come documento PDF. Per eseguire il rendering del modulo adattivo come documento di record, è necessario abilitare l’opzione Documento di record o i moduli adattivi basati su modelli di modulo.
* **Prepopolato:** I campi seguenti elencati fungono da input per l’attività:

   * **[!UICONTROL Seleziona il file di dati di input utilizzando]**: Percorso del file di dati di input (.json, .xml, .doc o modello di dati del modulo). È possibile recuperare il file di dati di input utilizzando un percorso relativo al payload o recuperare il file memorizzato in una variabile di tipo di dati Document, XML o JSON. Ad esempio, il file contiene i dati inviati per il modulo tramite un’applicazione Casella in entrata AEM. Un esempio di percorso è [Payload_Directory]/workflow/data.

   * **Selezionare gli allegati di input utilizzando:** Gli allegati disponibili nella posizione vengono allegati al modulo associato all&#39;attività. Il percorso può essere relativo al payload o recuperare gli allegati memorizzati in una variabile del tipo ArrayList of Document. Un esempio di percorso è [Payload_Directory]/attachment/. È possibile specificare gli allegati posizionati in relazione al payload o utilizzare una variabile di tipo documento (Elenco array > Documento) per specificare un allegato di input per il modulo adattivo.

      * **Scegli JSON di input:** Seleziona un file JSON di input utilizzando un percorso relativo al payload o memorizzato in una variabile del tipo di dati Document, JSON o Form Data Model. Questa opzione è disponibile se si seleziona Interfaccia utente di Interactive Communication Agent o Documento canale Web di comunicazione interattiva dall’elenco a discesa Tipo.
      * **Scegli un servizio di precompilazione personalizzato:** Selezionare il servizio di precompilazione per recuperare i dati e precompilare il documento del canale Web di comunicazione interattiva o l&#39;interfaccia utente dell&#39;agente.
      * **Utilizza il servizio di precompilazione della comunicazione interattiva selezionata sopra:** Utilizzare questa opzione per utilizzare il servizio di precompilazione della comunicazione interattiva definita nell’elenco a discesa Usa comunicazione interattiva .
      * **Mappatura attributo richiesta:** Utilizza la sezione Mappatura attributi di richiesta per definire la [nome e valore dell’attributo della richiesta](../../forms/using/work-with-form-data-model.md#bindargument). Recupera i dettagli dall’origine dati in base al nome e al valore dell’attributo specificati nella richiesta. È possibile definire un valore dell&#39;attributo della richiesta utilizzando un valore letterale o una variabile di tipo dati String.\
         Le opzioni di mappatura del servizio di precompilazione e dell’attributo della richiesta sono disponibili solo se si seleziona Interfaccia utente di Interactive Communication Agent o Documento del canale Web di comunicazione interattiva dall’elenco a discesa Tipo.

* **Informazioni trasmesse:** I campi seguenti elencati fungono da percorsi di output per l’attività:

   * **Salva il file di dati di output utilizzando:** Salva il file di dati (.json,. modello dati xml, doc o form). Il file di dati contiene informazioni inviate tramite il modulo associato. È possibile salvare il file di dati di output utilizzando un percorso relativo al payload o archiviarlo in una variabile di tipo di dati Document, XML o JSON. Ad esempio: [Payload_Directory]/Workflow/data, dove i dati sono un file.
   * **Salva gli allegati utilizzando:** Salvare gli allegati del modulo forniti in un’attività. È possibile salvare gli allegati utilizzando un percorso relativo al payload o archiviarlo in una variabile di tipo di dati Document.
   * **Salva documento di record utilizzando:** Percorso per il salvataggio di un file del documento di record. Ad esempio: [Payload_Directory]/DocumentofRecord/credit-card.pdf. È possibile salvare il documento di record utilizzando un percorso relativo al payload o archiviarlo in una variabile del tipo di dati Documento. Se si seleziona **Relativo al payload** Se il campo percorso viene lasciato vuoto, il documento di record non viene generato. Questa opzione è disponibile solo se si seleziona Modulo adattivo dall’elenco a discesa Tipo .

   * **Salva i dati del canale web utilizzando:** Salvare il file di dati Canale Web utilizzando un percorso relativo al payload o archiviarlo in una variabile del tipo di dati Document, JSON o Form Data Model. Questa opzione è disponibile solo se si seleziona Interfaccia utente di Interactive Communication Agent dall’elenco a discesa Tipo.
   * **Salvare il documento PDF utilizzando:** Salvare il documento PDF utilizzando un percorso relativo al payload o archiviarlo in una variabile di tipo Dati documento. Questa opzione è disponibile solo se si seleziona Interfaccia utente di Interactive Communication Agent dall’elenco a discesa Tipo.
   * **Salva il modello di layout utilizzando:** Salvare il modello layout utilizzando un percorso relativo al payload o archiviarlo in una variabile di tipo Dati documento. La [modello di layout](../../forms/using/layout-design-details.md) fa riferimento a un file XDP creato con Forms Designer. Questa opzione è disponibile solo se si seleziona Interfaccia utente di Interactive Communication Agent dall’elenco a discesa Tipo.

* **Assegnatario > Assegna opzioni:** Specificare il metodo per assegnare l&#39;attività a un utente. È possibile assegnare dinamicamente l&#39;attività a un utente o a un gruppo utilizzando lo script Selezione partecipanti o assegnarla a un utente o gruppo AEM specifico.
* **Selettore partecipante:** L’opzione è disponibile quando **In modo dinamico per un utente o un gruppo** l’opzione è selezionata nel campo Assegna opzioni . È possibile utilizzare uno script ECMAScript o un servizio per selezionare in modo dinamico un utente o un gruppo. Per ulteriori informazioni, consulta [Assegnazione dinamica di un flusso di lavoro agli utenti](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Creazione di un passaggio personalizzato Adobe Experience Manager Dynamic Participant .](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **Partecipanti:** Il campo è disponibile quando la **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** è selezionata nella **Selettore partecipante** campo . Il campo consente di selezionare utenti o gruppi per l’opzione RandomParticipantChooser.

* **Assegnatario:** Il campo è disponibile quando la **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** è selezionato in **Selettore partecipante** campo . Il campo ti consente di selezionare una variabile del tipo di dati String per definire l’assegnatario.

* **Argomenti:** Il campo è disponibile quando nel campo Selettore partecipante è selezionato uno script diverso da quello RandomParticipantChoose . Il campo consente di fornire un elenco di argomenti separati da virgola per lo script selezionato nel campo Selettore partecipante.

* **Utente o gruppo:** L&#39;attività viene assegnata all&#39;utente o al gruppo selezionato. L’opzione è disponibile quando **Per un utente o un gruppo specifico** è selezionato in **Opzioni di assegnazione** campo . Il campo elenca tutti gli utenti e i gruppi del gruppo utenti del flusso di lavoro.\
   La **Utente o gruppo** nel menu a discesa sono elencati gli utenti e i gruppi a cui l&#39;utente connesso ha accesso. La visualizzazione del nome utente dipende dal se si dispone delle autorizzazioni di accesso per **utenti** nodo in crx-repository per quel particolare utente.

* **[!UICONTROL Invia e-mail di notifica]**: Seleziona questa opzione per inviare notifiche e-mail all’assegnatario. Queste notifiche vengono inviate quando un’attività viene assegnata a un utente o a un gruppo. È possibile utilizzare **[!UICONTROL Indirizzo e-mail destinatario]** per specificare il meccanismo per recuperare l’indirizzo e-mail.

* **[!UICONTROL Indirizzo e-mail destinatario]**: È possibile memorizzare l’indirizzo e-mail in una variabile, utilizzare un valore letterale per specificare un indirizzo e-mail permanente o utilizzare l’indirizzo e-mail predefinito dell’assegnatario specificato nel profilo dell’assegnatario. Puoi utilizzare il valore letterale o una variabile per specificare l’indirizzo e-mail di un gruppo. L’opzione della variabile è utile per recuperare e utilizzare in modo dinamico un indirizzo e-mail. La **[!UICONTROL Usa indirizzo e-mail predefinito dell’assegnatario]** l&#39;opzione è disponibile solo per un singolo assegnatario. In questo caso, viene utilizzato l’indirizzo e-mail memorizzato nel profilo utente assegnatari.

* **Modello e-mail HTML**: Seleziona il modello e-mail per l’e-mail di notifica. Per modificare un modello, modifica il file che si trova in /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt in crx-repository.
* **Consenti Delega A:** AEM casella in entrata fornisce all’utente connesso un’opzione per delegare il flusso di lavoro assegnato a un altro utente. Puoi delegare all’interno dello stesso gruppo o all’utente del flusso di lavoro di un altro gruppo. Se l’attività viene assegnata a un singolo utente e la **consentire la delega ai membri del gruppo assegnatario** l’opzione è selezionata, quindi non è possibile delegare l’attività a un altro utente o gruppo.
* **Impostazioni condivisione:** AEM casella in entrata fornisce opzioni per condividere con un altro utente una singola o tutte le attività presenti nella casella in entrata:
   * Quando il **Consentire agli assegnatari di condividere esplicitamente nella casella in entrata** è selezionata, l&#39;utente può fare clic sull&#39;attività e condividerla con un altro utente AEM.
   * Quando il **Consentire agli assegnatari di condividere tramite condivisione in entrata** l’opzione viene selezionata e un utente condivide gli elementi della casella in entrata o consente ad altri utenti di accedere agli elementi della casella in entrata, solo le attività con l’opzione sopra indicata abilitata vengono condivise con altri utenti.

* **Azioni > Azioni predefinite:** Sono disponibili le azioni Invia, Salva e Ripristina predefinite. Per impostazione predefinita sono abilitate tutte le azioni predefinite.
* **Variabile di percorso:** Nome della variabile di route. La variabile di route acquisisce le azioni personalizzate selezionate da un utente nella casella in entrata AEM.
* **Percorsi:** Un&#39;attività può essere suddivisa in percorsi diversi. Se selezionata in AEM casella in entrata, la route restituisce un valore e i rami del flusso di lavoro in base alla route selezionata. È possibile memorizzare i percorsi in una variabile della matrice del tipo di dati String oppure selezionare **Letterale** per aggiungere manualmente i percorsi.

* **Titolo**: Specifica il titolo della route. Viene visualizzato in AEM casella in entrata.
* **Icona Corallo**: Specifica l&#39;attributo HTML di un&#39;icona corallo. La libreria CorelUI di Adobe fornisce un ampio set di icone touch-first. È possibile scegliere e utilizzare un&#39;icona per il percorso. Viene visualizzato insieme al titolo nella casella in entrata AEM. Se si memorizzano i percorsi in una variabile, i percorsi utilizzano un&#39;icona corallina &#39;Tags&#39; predefinita.
* **Consenti all&#39;assegnatario di aggiungere un commento**: Selezionare questa opzione per abilitare i commenti per l&#39;attività. Al momento dell’invio dell’attività, un assegnatario può aggiungere i commenti all’interno AEM casella in entrata.
* **Salva il commento nella variabile :** Salvare il commento in una variabile di tipo dati String. Questa opzione viene visualizzata solo se si seleziona la **Consenti all&#39;assegnatario di aggiungere un commento** casella di controllo.

* **Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività**: Selezionare questa opzione per abilitare gli allegati per l&#39;attività. Al momento dell’invio dell’attività, un assegnatario può aggiungere gli allegati dall’interno AEM casella in entrata.
* **Salva gli allegati delle attività di output utilizzando**: Specificare il percorso della cartella dell&#39;allegato. È possibile salvare gli allegati dell&#39;attività di output utilizzando un percorso relativo al payload o in una variabile di matrice del tipo di dati del documento. Questa opzione viene visualizzata solo se si seleziona la **Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività** seleziona e seleziona **Modulo adattivo**, **Modulo adattivo di sola lettura** oppure **Documento PDF non interattivo** dal **Tipo** elenco a discesa nella **Modulo/Documento** scheda .

>[!NOTE]
>
>Utilizzare la scheda Allegati nell&#39;interfaccia utente dell&#39;agente durante il runtime per associare gli allegati a una comunicazione interattiva. Gli allegati associati vengono visualizzati come allegati dell&#39;attività nella barra laterale dopo l&#39;apertura dell&#39;elemento di lavoro in uno stato Completo.

* **Utilizza metadati personalizzati:** Seleziona questa opzione per abilitare il campo metadati personalizzato. I metadati personalizzati vengono utilizzati nei modelli e-mail.
* **Metadati personalizzati:** Seleziona un metadati personalizzato per i modelli e-mail. I metadati personalizzati sono disponibili in crx-repository su apps/fd/dashboard/scripts/metadataScripts. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Puoi anche utilizzare un servizio per i metadati personalizzati. È inoltre possibile estendere l&#39;interfaccia WorkitemUserMetadataService per fornire metadati personalizzati.
* **Mostra dati dai passaggi precedenti**: Selezionare questa opzione per consentire agli assegnatari di visualizzare gli assegnatari precedenti, le azioni già eseguite sull&#39;attività, i commenti aggiunti all&#39;attività e il documento di registrazione dell&#39;attività completata, se disponibile.
* **Mostra dati dai passaggi successivi:** Selezionare questa opzione per consentire all&#39;assegnatario corrente di visualizzare l&#39;azione intrapresa e i commenti aggiunti all&#39;attività dagli assegnatari successivi. Consente inoltre all&#39;assegnatario corrente di visualizzare un documento di registrazione dell&#39;attività completata, se disponibile.
* **Visibilità del tipo di dati:** Per impostazione predefinita, un assegnatario può visualizzare un documento di registrazione, gli assegnatari, le azioni intraprese e i commenti aggiunti dagli assegnatari precedenti e successivi. Utilizza l’opzione di visibilità del tipo di dati per limitare il tipo di dati visibili agli assegnatari.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e recuperare la cronologia del passaggio Assegna attività sono disabilitate quando si configura un [!DNL Adobe Experience Manager] modello di flusso di lavoro per l’archiviazione dei dati esterni. Inoltre, in Posta in arrivo, l’opzione per il salvataggio è disabilitata.

## Invia passaggio e-mail {#send-email-step}

Utilizza il passaggio e-mail per inviare un’e-mail, ad esempio un messaggio e-mail con un documento di registrazione, un collegamento di un modulo adattivo, un collegamento di una comunicazione interattiva o un documento PDF allegato. Supporto dei passaggi di invio e-mail [E-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Le e-mail di HTML sono reattive e si adattano al client e-mail e alle dimensioni dello schermo dei destinatari. Puoi utilizzare un modello e-mail di HTML per definire l’aspetto, lo schema di colori e il comportamento dell’e-mail.

Il passaggio e-mail utilizza Day CQ Mail Service per inviare e-mail. Prima di utilizzare il passaggio e-mail, assicurati che [servizio e-mail](../../forms/using/aem-forms-workflow.md) è configurato. Il passaggio e-mail ha le seguenti proprietà:

**Titolo:** Il titolo del passaggio ti aiuta a identificare il passaggio nell’editor del flusso di lavoro.

**Descrizione:** La spiegazione è utile per altri sviluppatori di processi quando lavori in un ambiente di sviluppo condiviso.

**Oggetto e-mail** L’oggetto può essere recuperato dai metadati di un flusso di lavoro, specificati manualmente o recuperati dal valore memorizzato in una variabile. Seleziona tra le seguenti opzioni:

* **Letterale -** Specifica manualmente un oggetto.
* **Recupera dai metadati del flusso di lavoro** - Recupera l&#39;oggetto da una proprietà di metadati.
* **Variabile** - Recupera l&#39;oggetto dal valore memorizzato in una variabile del tipo di dati stringa.

**Modello e-mail HTML**: Modello HTML per l’e-mail. Puoi specificare le variabili in un modello e-mail. Il Passaggio e-mail estrae e visualizza tutte le variabili incluse in un modello per gli input.

**Metadati modello e-mail:** Il valore delle variabili del modello e-mail può essere un valore specificato dall’utente, il percorso di una risorsa sull’autore o sul server di pubblicazione, sull’immagine o su una proprietà di metadati del flusso di lavoro.

* **Letterale:** Utilizza l’opzione quando conosci il valore esatto da specificare. Ad esempio: [example@example.com](mailto:example@example.com).

* **Metadati flusso di lavoro:** Utilizza l’opzione quando il valore da utilizzare viene salvato in una proprietà di metadati di un flusso di lavoro. Dopo aver selezionato l’opzione , immetti il nome della proprietà metadati nella casella di testo vuota sotto l’opzione Metadati flusso di lavoro . Ad esempio, emailAddress.
* **URL risorsa:** Utilizza l’opzione per incorporare un collegamento web di una comunicazione interattiva all’e-mail. Dopo aver selezionato l&#39;opzione , sfoglia e scegli la comunicazione interattiva da incorporare. La risorsa può risiedere sull’autore o sul server di pubblicazione.
* **Immagine:** Utilizza l’opzione per incorporare un’immagine nell’e-mail. Dopo aver selezionato l&#39;opzione , sfoglia e scegli l&#39;immagine. L’opzione immagine è disponibile solo per i tag immagine (&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>) disponibili nel modello e-mail.&#42;

**Indirizzo e-mail del mittente/destinatario:** Seleziona la **Letterale** opzione per specificare manualmente un indirizzo e-mail o selezionare **Recupera dai metadati del flusso di lavoro** per recuperare l’indirizzo e-mail da una proprietà metadati. È inoltre possibile specificare un elenco di array di proprietà di metadati per **Recupera dai metadati del flusso di lavoro** opzione . Seleziona la **Variabile** per recuperare l’indirizzo e-mail dal valore memorizzato in una variabile di tipo dati stringa.

**File allegato:** La risorsa disponibile nel percorso specificato viene allegata all’e-mail. Il percorso della risorsa può essere relativo al payload o al percorso assoluto. Un esempio di percorso è [Payload_Directory]/attachment/.

Seleziona la **Variabile** per recuperare l’allegato del file memorizzato in una variabile del tipo di dati Document, XML o JSON.

**Nome file:** Nome del file allegato e-mail. Il Passaggio e-mail modifica il nome file originale dell’allegato al nome file specificato. Il nome può essere specificato manualmente o recuperato da una proprietà di metadati di un flusso di lavoro o da una variabile. Utilizza la **Letterale** quando si conosce il valore esatto da specificare. Utilizza la **Variabile** per recuperare il nome del file dal valore memorizzato in una variabile di tipo dati stringa. Utilizza la **Recupera da un metadati del flusso di lavoro** quando il valore da utilizzare viene salvato in una proprietà di metadati del flusso di lavoro.

## Passaggio Genera documento di record {#generate-document-of-record-step}

Quando un modulo viene compilato o inviato, è possibile conservare un record del modulo, in formato cartaceo o documento. Questo viene definito documento di registrazione (DoR). È possibile utilizzare il passaggio Genera documento di record per creare una versione PDF interattiva o di sola lettura di un modulo adattivo. La versione PDF contiene informazioni inserite nel modulo insieme al layout del modulo adattivo.

Il passaggio Documento di record ha le seguenti proprietà:

**Usa modulo adattivo**: Specifica il metodo per individuare il modulo adattivo di input. Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile del tipo di dati String per specificare il percorso nel **Selezionare la variabile da risolvere** campo .\
È possibile associare più moduli adattivi a un flusso di lavoro. Di conseguenza, è possibile specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

**Percorso modulo adattivo**: Specifica il percorso del modulo adattivo. Il campo è disponibile quando selezioni la **Disponibile in un percorso assoluto** dall&#39;opzione **Usa modulo adattivo** campo .

**Seleziona i dati di input utilizzando:** Percorso dei dati di input per il modulo adattivo. È possibile mantenere i dati in una posizione relativa al payload, specificare un percorso assoluto dei dati o recuperare i dati memorizzati in una variabile di tipo Document, JSON o XML. I dati di input vengono uniti al modulo adattivo per creare un documento di record.

**Selezionare il percorso dell&#39;allegato di input utilizzando:** Percorso degli allegati. Questi allegati sono inclusi nel documento di registrazione. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di tipo di dati Documento.

Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella vengono allegati al documento di record. Se sono disponibili file nelle cartelle direttamente disponibili nel percorso allegato specificato, i file sono inclusi nel documento di registrazione come allegati. Se sono presenti cartelle in cartelle direttamente disponibili, queste vengono ignorate.

**Salva documento di record generato utilizzando le opzioni seguenti:** Specificare il percorso in cui conservare un documento del file di record. È possibile scegliere di sovrascrivere la cartella payload, inserire il documento di record in una posizione all’interno della directory di payload o archiviare il documento di record in una variabile di tipo di dati Documento.

**Impostazioni internazionali**: Specificare la lingua del documento di registrazione. Seleziona **Letterale** per selezionare le impostazioni internazionali da un elenco a discesa o selezionare **Variabile** per recuperare le impostazioni internazionali dal valore memorizzato in una variabile di tipo dati stringa. È necessario definire il codice delle impostazioni internazionali quando si memorizza il valore delle impostazioni internazionali in una variabile. Ad esempio, specifica **en_US** per inglese e **fr_FR** per il francese.

## Passaggio Invoca il servizio del modello dati del modulo {#invoke-form-data-model-service-step}

È possibile utilizzare [Integrazione dei dati di AEM Forms](../../forms/using/data-integration.md) per configurare e connettersi a origini dati diverse. Queste origini dati possono essere un database, un servizio Web, un servizio REST, un servizio OData e una soluzione CRM. L’integrazione dei dati di AEM Forms consente di creare un modello di dati del modulo che include vari servizi per eseguire operazioni di recupero, aggiunta e aggiornamento dei dati sul database configurato. È possibile utilizzare **Richiama del passaggio Servizio del modello dati** per selezionare un modello dati modulo (FDM) e utilizzare i servizi di FDM per recuperare, aggiornare o aggiungere dati a origini dati diverse.

Per spiegare gli input per i campi del passaggio , come esempio vengono utilizzati la seguente tabella di database e il file JSON :

**Tabella CustomerDetails di esempio**

<table>
 <tbody> 
  <tr> 
   <td>Proprietà</td> 
   <td>Valore<br /> </td> 
  </tr> 
  <tr> 
   <td>Nome<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>Cognome</td> 
   <td>Rosa</td> 
  </tr> 
  <tr> 
   <td>ID cliente</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Indirizzo e-mail<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**File JSON di esempio**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

Il passaggio Invoke Form Data Model Service presenta i campi elencati di seguito per facilitare le operazioni del modello dati del modulo:

* **Titolo:** Titolo del passaggio. Consente di identificare il passaggio nell’editor del flusso di lavoro.
* **Descrizione:** Spiegazione utile per altri sviluppatori di processi quando lavori in un ambiente di sviluppo condiviso.

* **Percorso modello dati modulo**: Sfogliare e selezionare un modello di dati modulo presente sul server.

* **Servizio**: Elenco dei servizi forniti dal modello dati modulo selezionato.
* **Input for services > Fornisci dati di input utilizzando metadati letterali, variabili o flussi di lavoro e un file JSON**: Un servizio può avere più argomenti. Seleziona l’opzione per ottenere il valore degli argomenti del servizio da una proprietà dei metadati di un flusso di lavoro, un oggetto JSON, una variabile o immetti direttamente il valore nella casella di testo fornita:

   * **Letterale:** Utilizza l’opzione quando conosci il valore esatto da specificare. Ad esempio, srose@we.info.
   * **Variabile:** Utilizza l’opzione per recuperare il valore memorizzato in una variabile.
   * **Recupera dai metadati del flusso di lavoro:** Utilizza l’opzione quando il valore da utilizzare viene salvato in una proprietà di metadati di un flusso di lavoro. Ad esempio, emailAddress.
   * **[!UICONTROL Relativo al payload]**: Utilizzare l&#39;opzione per recuperare l&#39;allegato salvato in un percorso relativo al payload. Selezionare l&#39;opzione e specificare il nome della cartella che include l&#39;allegato o specificare il nome dell&#39;allegato del file nella casella di testo.

      Ad esempio, se la cartella Relativo a Payload nell&#39;archivio CRX include un allegato al `attachment\attachment-folder` posizione, specificare `attachment\attachment-folder` nella casella di testo dopo aver selezionato il **[!UICONTROL Relativo al payload]** opzione .
   * **Notazione punto JSON:** Utilizza l’opzione quando il valore da utilizzare si trova in un file JSON. Ad esempio, Insurance.customerDetails.emailAddress. L’opzione Notazione punto JSON è disponibile solo se è selezionata l’opzione Mappa campi di input dall’input JSON di input.
   * **Mappare i campi di input da JSON di input:** Specifica il percorso di un file JSON per ottenere il valore di input di alcuni argomenti di servizio dal file JSON. Il percorso del file JSON può essere relativo al payload, a un percorso assoluto, oppure è possibile selezionare un documento JSON di input utilizzando una variabile di tipo JSON o Form Data Model.

* **Input for services > Fornisci i dati di input utilizzando una variabile o un file JSON:** Seleziona l’opzione per ottenere i valori per tutti gli argomenti da un file JSON salvato in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **Seleziona il documento JSON di input utilizzando**: Il file JSON contenente i valori per tutti gli argomenti del servizio. Il percorso del file JSON può essere **relativo al payload** o **percorso assoluto.** È inoltre possibile recuperare il documento JSON di input utilizzando una variabile di tipo JSON o Form Data Model.

* **Notazione punto JSON:** Lascia vuoto il campo per utilizzare tutti gli oggetti del file JSON specificato come input per gli argomenti del servizio. Per leggere un oggetto JSON specifico dal file JSON specificato come input per gli argomenti del servizio, specifica la notazione del punto per l’oggetto JSON, ad esempio, se disponi di un JSON simile a quello elencato all’inizio della sezione, specifica Insurance.customerDetails per fornire tutti i dettagli di un cliente come input al servizio.
* **Output di service > Mappa e scrittura dei valori di output su variabili o metadati:** Seleziona l&#39;opzione per salvare i valori di output come proprietà del nodo di metadati dell&#39;istanza del flusso di lavoro in crx-repository. Specifica il nome della proprietà metadati e seleziona l&#39;attributo di output del servizio corrispondente da mappare con la proprietà metadati, ad esempio, mappa il numero_telefono restituito dal servizio di output con la proprietà numero_telefono dei metadati del flusso di lavoro. Allo stesso modo, è possibile memorizzare l&#39;output in una variabile di tipo dati Long.Quando si seleziona una proprietà per **[!UICONTROL Attributo di output del servizio da mappare]** solo le variabili in grado di memorizzare i dati della proprietà selezionata vengono compilate per **[!UICONTROL Salva l’output in]** opzione .

* **Output di service > Save output to variable o a JSON file:** Seleziona l’opzione per salvare i valori di output in un file JSON in un percorso assoluto, in un percorso relativo al payload o in una variabile .
* **Salva il documento JSON di output utilizzando le seguenti opzioni:** Salva il file JSON di output. Il percorso del file JSON di output può essere relativo al payload o a un percorso assoluto. Puoi anche salvare il file JSON di output utilizzando una variabile di tipo JSON o Form Data Model.

## Passaggio Firma documento {#sign-document-step}

Il passaggio Firma documento consente di utilizzare Adobe Sign per firmare i documenti. Il passaggio Firma documento ha le seguenti proprietà:

* **Nome accordo:** Specifica il titolo del contratto. Il nome del contratto fa parte dell’oggetto e del corpo del messaggio e-mail inviato ai firmatari. È possibile memorizzare il nome in una variabile di tipo dati String oppure selezionare **Letterale** per aggiungere manualmente il nome.

* **Impostazioni internazionali:** Specifica la lingua per le opzioni di e-mail e verifica. È possibile memorizzare le impostazioni internazionali in una variabile di tipo dati String oppure selezionare **Letterale** per scegliere le impostazioni internazionali dall’elenco delle opzioni disponibili. È necessario definire il codice delle impostazioni internazionali quando si memorizza il valore delle impostazioni internazionali in una variabile. Ad esempio, specifica **en_US** per inglese e **fr_FR** per il francese.

* **Configurazione di Adobe Sign Cloud**: Scegli una configurazione cloud di Adobe Sign. Se non hai configurato Adobe Sign per AEM Forms, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Selezionare il documento da firmare utilizzando:** È possibile scegliere un documento da una posizione relativa al payload, utilizzare il payload come documento, specificare un percorso assoluto del documento o recuperare il documento memorizzato in una variabile di tipo Dati documento.


* **Selezionare Percorso allegato di input utilizzando:** Percorso degli allegati. Questi allegati sono inclusi nel documento di firma. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di tipo di dati Documento.


   Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella vengono allegati al documento di firma. Se sono disponibili file nelle cartelle direttamente disponibili nel percorso allegato specificato, i file sono inclusi nel documento di firma come allegati. Se sono presenti cartelle in cartelle direttamente disponibili, queste vengono ignorate.

* **Giorni fino alla scadenza:** Un documento viene contrassegnato come scaduto (superato il termine) dopo che non vi è alcuna attività sull&#39;attività per il numero di giorni specificato nel **Giorni fino alla scadenza** campo . Il numero di giorni viene conteggiato dopo che il documento è stato assegnato a un utente per la firma.
* **Frequenza e-mail promemoria:** Puoi inviare un messaggio e-mail di promemoria a intervalli giornalieri o settimanali. La settimana viene conteggiata dal giorno in cui il documento viene assegnato a un utente per la firma.
* **Processo firma:** È possibile scegliere di firmare un documento in ordine sequenziale o parallelo. In ordine sequenziale, un firmatario riceve il documento alla volta per la firma. Al termine della firma del documento da parte del primo firmatario, il documento viene inviato al secondo firmatario e così via. In ordine parallelo, più firmatari possono firmare un documento alla volta.
* **URL di reindirizzamento:** Specifica un URL di reindirizzamento. Dopo aver firmato il documento, è possibile reindirizzare l’assegnatario a un URL. Di solito, questo URL contiene un messaggio di ringraziamento o ulteriori istruzioni.
* **Fase del flusso di lavoro:** Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata AEM. Puoi definire questi stadi nelle proprietà del modello (Barra laterale > Pagina > Proprietà pagina > Stadi).
* **Selezionare i firmatari:** Specificare il metodo per scegliere i firmatari per il documento. Puoi assegnare dinamicamente il flusso di lavoro a un utente o a un gruppo oppure aggiungere manualmente i dettagli di un firmatario.
* **Script o servizio per selezionare i firmatari:** L’opzione è disponibile solo se nel campo Seleziona firmatari è selezionata l’opzione Dinamicamente . È possibile specificare uno script ECMAScript o un servizio per scegliere i firmatari e le opzioni di verifica di un documento.
* **Dettagli del firmatario:** L’opzione è disponibile solo se l’opzione Manualmente è selezionata nel campo Seleziona firmatari . Specifica l’indirizzo e-mail e scegli un meccanismo di verifica facoltativo. Prima di selezionare un meccanismo di verifica in due fasi, assicurati che l’opzione di verifica corrispondente sia abilitata per l’account Adobe Sign configurato. È possibile utilizzare una variabile del tipo di dati String per definire i valori per **[!UICONTROL E-mail]**, **[!UICONTROL Codice paese]** e **[!UICONTROL Numero di telefono]** campi. La **[!UICONTROL Codice paese]** e **[!UICONTROL Numero di telefono]** i campi vengono visualizzati solo se si seleziona **[!UICONTROL Verifica telefonica]** dal **[!UICONTROL Verifica in due fasi]** elenco a discesa.
* **Variabile di stato:** Un documento abilitato per Adobe Sign memorizza lo stato di firma del documento in una variabile di tipo dati String. Specifica il nome della variabile di stato (adobeSignStatus). Una variabile di stato di un&#39;istanza è disponibile in CRXDE in /etc/workflow/instances/&lt;server>/&lt;date-time>/&lt;instance of=&quot;&quot; workflow=&quot;&quot; model=&quot;&quot;>/workItems/&lt;node>/metaData contiene lo stato di una variabile.
* **Salva documento firmato utilizzando le opzioni seguenti:** Specificare il percorso in cui conservare i documenti firmati. È possibile scegliere di sovrascrivere il file di payload, posizionare il documento firmato in una posizione all’interno della directory di payload o archiviare il documento firmato in una variabile di tipo Documento.

## Passaggi di Document Services {#document-services-steps}

AEM Document Services è un insieme di servizi per la creazione, l’assemblaggio e la protezione di documenti PDF. AEM Forms fornisce un passaggio AEM flusso di lavoro separato per ogni servizio di documentazione.

Analogamente ad altri passaggi del flusso di lavoro di AEM Forms, ad esempio Assegna attività, Invia e-mail e Firma documento, è possibile utilizzare le variabili in tutti i passaggi AEM servizi documenti. Per ulteriori informazioni sulla creazione e la gestione delle variabili, consulta [Variabili nei flussi di lavoro AEM](../../forms/using/variable-in-aem-workflows.md).

### Passaggio del timestamp del documento {#apply-document-time-stamp-step}

Aggiungi una marca temporale a un documento. Fornisci dettagli del documento quali il percorso del documento di input, il nome del documento di input, la posizione in cui memorizzare i dati esportati. È possibile scegliere di sovrascrivere il file di payload esistente, scegliere un nome file diverso per memorizzare i dati in un file diverso in una cartella di payload, fornire un percorso assoluto ai dati o archiviare i dati in una variabile di tipo di dati Documento.

### Passaggio Converti in immagine {#convert-to-image-step}

Converte un documento PDF in un elenco di immagini. I formati immagine supportati sono JPEG, JPEG2000, PNG e TIFF. Le seguenti informazioni si applicano alle conversioni nelle immagini di TIFF:

* Viene generato un file TIFF multipagina.
* Alcune annotazioni non sono incluse nelle immagini di TIFF. Le annotazioni per le quali Acrobat deve generare l’aspetto non sono incluse.

### Passaggio Converti in PDF/A {#convert-to-pdf-a-step}

Converte un documento PDF in formato PDF/A utilizzando le opzioni disponibili. La versione PDF/A di Portable Document Format (PDF) è specializzata nell&#39;archiviazione e nella conservazione a lungo termine dei documenti.

### Passaggio Converti in PS {#convert-to-ps-step}

Convertire documenti PDF in PostScript. Durante la conversione in PostScript, è possibile utilizzare l&#39;operazione di conversione per specificare il documento di origine e se convertire in PostScript di livello 2 o 3. Il documento PDF convertito in un file PostScript deve essere non interattivo.

### Crea PDF dal passaggio del tipo specificato {#create-pdf-from-specified-type-step}

Generare un documento PDF da un file di input. Il documento di input può essere relativo al payload, avere un percorso assoluto, può essere payload stesso o memorizzato in una variabile di tipo di dati Documento.

### Crea PDF da un passaggio URL/HTML/ZIP {#create-pdf-from-url-html-zip-step}

Genera un documento PDF dal file URL, HTML e ZIP fornito.

### Passaggio Esporta dati {#export-data-step}

Esporta dati da un file PDF forms o XDP. Richiede di inserire il percorso file del documento di input e del formato di esportazione dei dati. Le opzioni per Formato dati esportazione sono Auto, XDP e XmlData.

### Export PDF al passaggio del tipo specificato {#export-pdf-to-specified-type-step}

Converte un documento PDF in un formato selezionato.

### Passaggio Genera PDF non interattivo {#generatenoninteractive}

Generare un PDF non interattivo. Offre diverse opzioni di personalizzazione.

>[!NOTE]
>
>È possibile utilizzare le variabili per specificare il file modello per i documenti di input. Memorizza il percorso del file modello in una variabile di tipo dati String.

### Passaggio Importa dati {#import-data-step}

Unisce i dati del modulo in un modulo PDF. È possibile importare i dati del modulo in un modulo PDF.

### Richiama passaggio DDX {#invokeddx}

Esegue il file DDX sulla mappa specificata dei documenti di input e restituisce i documenti PDF manipolati.

>[!NOTE]
>
>È possibile utilizzare le variabili per specificare il file DDX per i documenti di input. Memorizzare il file DDX in una variabile di tipo di dati Document o XML.

### Passaggio Optimize PDF {#optimize-pdf-step}

Ottimizza i file PDF riducendone le dimensioni. Il risultato di questa conversione sono i file PDF che possono essere più piccoli delle versioni originali. Questa operazione converte anche i documenti PDF nella versione di PDF specificata nei parametri di ottimizzazione.

Le impostazioni di ottimizzazione specificano la modalità di ottimizzazione dei file. Di seguito sono riportati alcuni esempi di impostazioni:

* Versione di Target PDF
* Eliminazione di oggetti come azioni JavaScript e miniature di pagina incorporate
* Eliminazione dei dati utente, ad esempio commenti e allegati di file
* Eliminazione delle impostazioni non valide o non utilizzate
* Compressione dei dati non compressi o utilizzo di algoritmi di compressione più efficienti
* Rimozione dei font incorporati
* Impostazione dei valori di trasparenza

### Passaggio Rendering del modulo PDF {#renderpdf}

Esegue il rendering di un modulo creato in Form Designer (XDP) in un modulo PDF.

>[!NOTE]
>
>È possibile utilizzare le variabili per specificare il file modello per i documenti di input. Memorizza il percorso del file modello in una variabile di tipo dati String.

### Passaggio Secure Document {#secure-document-step}

Cifrare, firmare e certificare un documento. AEM Forms supporta sia la crittografia basata su password che la crittografia basata su certificato. È inoltre possibile scegliere tra vari algoritmi per la firma dei documenti. Ad esempio, SHA-256 e SH-512. È inoltre possibile utilizzare il passaggio del flusso di lavoro per estendere i documenti PDF tramite il lettore. Il passaggio del flusso di lavoro fornisce l’opzione per abilitare la decodifica del codice a barre, le firme digitali, l’importazione e l’esportazione di dati di PDF e altre opzioni.

### Passaggio Invia a stampante {#send-to-printer-step}

Invia un documento direttamente a una stampante. Supporta i seguenti meccanismi di accesso alla stampa:

* **Stampante con accesso diretto**: Una stampante installata sullo stesso computer è denominata stampante diretta accessibile e il computer è denominato host della stampante. Questo tipo di stampante può essere una stampante locale collegata direttamente al computer.
* **Stampante con accesso indiretto**: La stampante installata in un server di stampa è accessibile da altri computer. Per la connessione a una stampante di rete sono disponibili tecnologie come il sistema di stampa UNIX® (CUPS) comune e il protocollo Line Printer Daemon (LPD). Per accedere a una stampante con accesso indiretto, specificare il nome IP o host del server di stampa. Utilizzando questo meccanismo, è possibile inviare un documento a un URI LPD quando la rete ha un LPD in esecuzione. Il meccanismo consente di indirizzare il documento a qualsiasi stampante collegata alla rete che dispone di un LPD in esecuzione.

### Genera passaggio di output stampato {#generatePrintedOutput}

Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL in base a una struttura del modulo e a un file di dati. Il file di dati viene unito alla struttura del modulo e formattato per la stampa. L&#39;output generato da questo passaggio può essere inviato direttamente a una stampante o salvato come file. Si consiglia di utilizzare questo passaggio quando si desidera utilizzare le strutture del modulo o i dati provenienti da un&#39;applicazione. Se le strutture del modulo o le strutture del modulo si trovano in una posizione di rete, in un file system locale o in una posizione HTTP, utilizzare l&#39;operazione generaStampaOutput.

Ad esempio, l’applicazione richiede l’unione di una struttura del modulo con un file di dati. I dati contengono centinaia di record. Inoltre, richiede l&#39;invio dell&#39;output a una stampante che supporti ZPL. La struttura del modulo e i dati di input si trovano in un’applicazione. Utilizzare l&#39;operazione generatePraintOutput per unire ogni record con una struttura del modulo e inviare l&#39;output a una stampante che supporti ZPL.

Il passaggio Genera output stampato ha le seguenti proprietà:

**Proprietà di input**

* **[!UICONTROL Seleziona il file modello utilizzando]**: Specifica il percorso del file modello. È possibile selezionare il file modello utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio: [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può creare il percorso prima di utilizzarlo. Inoltre, puoi anche accettare payload come file di dati di input.

* **[!UICONTROL Seleziona il documento dati utilizzando]**: Specifica il percorso di un file di dati di input. È possibile selezionare il file di dati di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio: [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può creare il percorso prima di utilizzarlo.

* **[!UICONTROL Formato stampante]**: Valore di formato di stampa che specifica il linguaggio di descrizione della pagina da utilizzare, quando non viene fornito un file XDC, per generare il flusso di output. Se si specifica un valore letterale, selezionare uno dei seguenti valori:

   * **[!UICONTROL PCL personalizzato]**: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per PCL.
   * **[!UICONTROL PostScript personalizzato]**: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per PostScript.
   * **[!UICONTROL ZPL personalizzato]**: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per ZPL.
   * **[!UICONTROL Colore generico PCL (5c)]**: Utilizzare un colore generico PCL (5c).
   * **[!UICONTROL Livello 3 generico PostScript]**: Utilizzare un PostScript generico di livello 3.
   * **[!UICONTROL ZPL 300 DPI]**: Utilizzare ZPL 300 DPI. Viene utilizzato zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: Utilizzare ZPL 600 DPI. Viene utilizzato il file zpl600.xdc.
   * **[!UICONTROL IPL personalizzato]**: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per IPL.
   * **[!UICONTROL IPL 300 DPI]**: Utilizzare IPL 300 DPI. Viene utilizzato ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: Utilizzare IPL 400 DPI. Viene utilizzato il file ipl400.xdc.
   * **[!UICONTROL TPCL personalizzato]**: Utilizzare l’opzione per specificare un file XDC personalizzato per TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: Utilizzare TPCL 300 DPI. Viene utilizzato il file tpcl305.xdc.
   * **[!UICONTROL PCL 600 DPI]**: Utilizzare TPCL 600 DPI. Viene utilizzato il file tpcl600.xdc.
   * **[!UICONTROL DPL personalizzato]**: Utilizza l’opzione per specificare un file XDC personalizzato DPL.
   * **[!UICONTROL DPL300DPI]**: Utilizzare DPL 300 DPI. Viene utilizzato il file dpl300.xdc.
   * **[!UICONTROL DPL406DPI]**: Utilizzare DPL 400 DPI. Viene utilizzato dpl406.xdc.
   * **[!UICONTROL DPL600DPI]**: Utilizzare DPL 600 DPI. Viene utilizzato dpl600.xdc.

**Proprietà di output**

* **[!UICONTROL Salva documento di output utilizzando]**: Specificare il percorso in cui salvare il file di output. È possibile salvare il file di output in una posizione relativa al payload, in una variabile, oppure specificare una posizione assoluta per salvare il file di output. Se il percorso non esiste in crx-repository, un amministratore può creare il percorso prima di utilizzarlo.

**Proprietà avanzate**

* **[!UICONTROL Selezionare la posizione principale del contenuto utilizzando]**: La directory principale del contenuto è un valore stringa che specifica l’URI, il riferimento assoluto o la posizione nell’archivio per recuperare le risorse relative utilizzate dalla struttura del modulo. Ad esempio, se la struttura del modulo fa riferimento a un’immagine relativamente, ad esempio ../myImage.gif, myImage.gif deve trovarsi all’indirizzo repository://. Il valore predefinito è repository://, che punta al livello principale dell&#39;archivio.

   Quando selezioni una risorsa dall&#39;applicazione, il percorso URI della directory principale contenuto deve avere la struttura corretta. Ad esempio, se un modulo viene prelevato da un&#39;applicazione denominata SampleApp e viene posizionato in SampleApp/1.0/forms/Test.xdp, l&#39;URI della directory principale del contenuto deve essere specificato come repository://administrator@password/Applications/SampleApp/1.0/forms/ o repository:/Applications/SampleApp/1.0/forms/ (quando l&#39;autorità è null). Quando l’URI della directory principale contenuto viene specificato in questo modo, i percorsi di tutte le risorse di riferimento nel modulo verranno risolti rispetto a questo URI.

* **[!UICONTROL Seleziona il file XCI utilizzando]**: I file XCI vengono utilizzati per descrivere i font e altre proprietà utilizzati per gli elementi della struttura del modulo. È possibile mantenere un file XCI relativo al payload, in un percorso assoluto o utilizzando una variabile del tipo di dati Documento.

* **[!UICONTROL Impostazioni internazionali]**: Specifica la lingua utilizzata per generare il documento PDF. Se si specifica un valore letterale, selezionare una lingua dall’elenco o selezionare uno dei seguenti valori:
   * **Per utilizzare le impostazioni predefinite del server**: (Impostazione predefinita) Utilizza le impostazioni internazionali configurate sul server AEM Forms. Le impostazioni internazionali sono configurate mediante la console di amministrazione. (Vedi [Guida di Designer](http://www.adobe.com/go/learn_aemforms_designer_65).)

   * **Per utilizzare un valore personalizzato**: Digitare il codice di impostazione internazionale nella casella letterale oppure selezionare una variabile di stringa contenente il codice di impostazione internazionale. Per un elenco completo dei codici locali supportati, consulta http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copie]**: Un valore intero che specifica il numero di copie da generare per l&#39;output. Il valore predefinito è 1.

* **[!UICONTROL Stampa fronte retro]**: Valore di impaginazione che specifica se utilizzare la stampa fronte/retro o fronte/retro. Le stampanti che supportano PostScript e PCL utilizzano questo valore.Se si fornisce un valore letterale, selezionare uno dei seguenti valori:
   * **[!UICONTROL Doppio lato lungo]**: Utilizzare la stampa e la stampa fronte/retro utilizzando l&#39;impaginazione a lungo termine.
   * **[!UICONTROL Bordo corto duplex]**: Utilizzare la stampa e la stampa fronte/retro utilizzando l’impaginazione a bordi brevi.
   * **[!UICONTROL Simplex]**: Utilizzare la stampa su un solo lato.
