---
title: Flusso di lavoro incentrato su Forms su OSGi - Riferimento passaggio
description: I flussi di lavoro basati su Forms e sui passaggi OSGi consentono di creare rapidamente flussi di lavoro basati su moduli adattivi.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 470fcfda-dfde-437c-b539-d5af1e13a7d6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '7640'
ht-degree: 0%

---

# Flusso di lavoro incentrato su Forms su OSGi - Riferimento passaggio {#forms-centric-workflow-on-osgi-step-reference}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=it) |
| AEM 6.5 | Questo articolo |

I modelli di workflow consentono di convertire una regola business in un processo ripetitivo automatizzato. Un modello consente di definire ed eseguire una serie di passaggi. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o utilizza più risorse. Puoi [includere vari passaggi del flusso di lavoro AEM in un modello per ottenere la logica di business](/help/sites-developing/workflows-models.md#extending-aem).

## Passaggi Forms Workflow {#forms-workflow-steps}

I passaggi di Forms Workflow eseguono operazioni specifiche per AEM Forms in un flusso di lavoro AEM. Questi passaggi consentono di creare rapidamente un flusso di lavoro adattivo basato su Forms su OSGi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di revisione e approvazione di base, processi aziendali interni e attraverso il firewall. Puoi anche utilizzare i passaggi di Forms Workflow per avviare i servizi documentali, integrarli con il flusso di lavoro della firma di Adobe Sign ed eseguire altre operazioni AEM Forms. È necessario [il componente aggiuntivo AEM Forms](https://www.adobe.com/go/learn_aemforms_documentation_63) per utilizzare questi passaggi in un flusso di lavoro.

I passaggi del flusso di lavoro incentrati su Forms eseguono operazioni specifiche per AEM Forms in un flusso di lavoro AEM. Questi passaggi ti consentono di creare rapidamente un flusso di lavoro basato su Forms e adattivo per Forms su OSGi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di revisione e approvazione di base, interni e attraverso il firewall.

>[!NOTE]
>
>Se il modello di flusso di lavoro è contrassegnato per un archivio esterno, per tutti i passaggi del Forms Workflow è possibile selezionare solo l&#39;opzione della variabile per memorizzare o recuperare file di dati e allegati.

## Assegna passaggio attività {#assign-task-step}

Il passaggio Assegna attività crea un&#39;attività e la assegna a un utente o a un gruppo. Oltre all’assegnazione dell’attività, il componente specifica anche il modulo adattivo o il PDF non interattivo per l’attività. Il modulo adattivo è necessario per accettare l’input degli utenti e dei PDF non interattivi, oppure un modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di sola revisione.

È inoltre possibile utilizzare il componente per controllare il comportamento dell&#39;attività. Ad esempio, la creazione di un documento di record automatico, l’assegnazione dell’attività a un utente o gruppo specifico, la specifica del percorso dei dati inviati, il percorso dei dati da precompilare e le azioni predefinite. Il passaggio Assegna attività presenta le seguenti proprietà:

* **Titolo:** Titolo dell&#39;attività. Il titolo viene visualizzato nella casella in entrata AEM.
* **Descrizione:** Spiegazione delle operazioni eseguite nell&#39;attività. Queste informazioni sono utili per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **Percorso miniatura:** Percorso della miniatura dell&#39;attività. Se non viene specificato alcun percorso, viene visualizzata la miniatura predefinita di un modulo adattivo e per il documento di record viene visualizzata un’icona predefinita.
* **Fase flusso di lavoro:** Un flusso di lavoro può avere più fasi. Questi stadi vengono visualizzati nella casella in entrata AEM. Potete definire questi stadi nelle proprietà del modello (Sidekick > Pagina > Proprietà pagina > Stadi).
* **Priorità:** La priorità selezionata viene visualizzata nella casella in entrata AEM. Le opzioni disponibili sono Alta, Medium e Bassa. Il valore predefinito è Medium.
* **Data di scadenza:** Specificare il numero di giorni o di ore dopo le quali l&#39;attività viene contrassegnata come scaduta. Se selezioni **Disattivato**, l&#39;attività non verrà mai contrassegnata come scaduta. È inoltre possibile specificare un gestore di timeout per eseguire attività specifiche dopo la scadenza dell&#39;attività.

* **Giorni:** il numero di giorni prima dei quali l&#39;attività deve essere completata. Il numero di giorni viene conteggiato dopo l&#39;assegnazione dell&#39;attività a un utente. Se un’attività non è completa e supera il numero di giorni specificato nel campo Giorni, se selezionata, viene attivato un gestore di timeout dopo la data di scadenza.
* **Ore:** il numero di ore prima delle quali l&#39;attività deve essere completata. Il numero di ore che vengono conteggiate dopo l&#39;assegnazione dell&#39;attività a un utente. Se un’attività non è completa e supera il numero di ore specificato nel campo Ore, se selezionato viene attivato un gestore di timeout dopo le ore dovute.
* **Timeout dopo la data di scadenza:** Selezionare questa opzione per abilitare il campo di selezione Gestore di timeout.
* **Gestore timeout:** Selezionare lo script da eseguire quando il passaggio dell&#39;attività di assegnazione supera la data di scadenza. Gli script inseriti nell&#39;archivio CRX in [apps]/fd/dashboard/scripts/timeoutHandler sono disponibili per la selezione. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo.
* **Evidenzia l&#39;azione e il commento dall&#39;ultima attività in Dettagli attività:** Selezionare questa opzione per visualizzare l&#39;ultima azione eseguita e il commento ricevuto nella sezione dei dettagli dell&#39;attività di un&#39;attività.
* **Tipo:** Scegliere il tipo di documento da compilare all&#39;avvio del workflow. Puoi scegliere un modulo adattivo, un modulo adattivo di sola lettura, un documento PDF non interattivo, un’interfaccia utente di Interactive Communication Agent o un documento canale web di comunicazione interattiva.
* **Usa modulo adattivo:** Specifica il metodo per individuare il modulo adattivo di input. Questa opzione è disponibile se si seleziona Modulo adattivo o Modulo adattivo di sola lettura dall’elenco a discesa Tipo. Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso.\
  È possibile associare più moduli adattivi a un flusso di lavoro. Di conseguenza, puoi specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

* **Usa comunicazione interattiva:** Specificare il metodo per individuare la comunicazione interattiva di input. Puoi utilizzare la comunicazione interattiva inviata al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso. Questa opzione è disponibile se si seleziona Interfaccia utente agente comunicazione interattiva o Documento canale web comunicazione interattiva dall’elenco a discesa Tipo.

>[!NOTE]
>
>Per accedere all’interfaccia utente di Interactive Communications Agent nella casella in entrata dell’AEM, è necessario disporre delle assegnazioni di gruppi cm-agent-users e workflow-users.

* **Modulo adattivo o percorso di comunicazione interattiva**: specifica il percorso del modulo adattivo o della comunicazione interattiva. Puoi utilizzare il modulo adattivo o la comunicazione interattiva inviati al flusso di lavoro, disponibili in un percorso assoluto, oppure recuperare il modulo adattivo da un percorso memorizzato in una variabile di tipo dati stringa.
* **Selezionare PDF di input utilizzando:** Specificare il percorso di un documento di PDF non interattivo. Il campo è disponibile quando si sceglie un documento PDF non interattivo nel campo Tipo. È possibile selezionare il PDF di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio, [Directory_Payload]/Workflow/PDF/credit-card.pdf. Il percorso non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Per utilizzare l’opzione Percorso PDF è necessario abilitare l’opzione Documento di record o moduli adattivi basati su modelli di modulo.
* **Per l&#39;attività completata, esegui il rendering del modulo adattivo come**: quando un&#39;attività è contrassegnata come completata, puoi eseguire il rendering del modulo adattivo come modulo adattivo di sola lettura o documento PDF. Per poter eseguire il rendering del modulo adattivo come documento record, è necessario abilitare l’opzione Documento di record o i moduli adattivi basati su modello di modulo.
* **Precompilati:** I campi elencati di seguito fungono da input per l&#39;attività:

   * **[!UICONTROL Selezionare il file di dati di input utilizzando]**: percorso del file di dati di input (.json, .xml, .doc o modello dati modulo). Puoi recuperare il file di dati di input utilizzando un percorso relativo al payload o recuperare il file memorizzato in una variabile di tipo Documento, XML o JSON. Ad esempio, il file contiene i dati inviati per il modulo tramite un&#39;applicazione Casella in entrata AEM. Il percorso di esempio è [Payload_Directory]/workflow/data.

   * **Selezionare gli allegati di input utilizzando:** Gli allegati disponibili nel percorso sono allegati al modulo associato all&#39;attività. Il percorso può essere relativo al payload o recuperare gli allegati memorizzati in una variabile di tipo ArrayList of Document. Il percorso di esempio è [Payload_Directory]/allegati/. È possibile specificare gli allegati posizionati rispetto al payload o utilizzare una variabile di tipo documento (Elenco array > Documento) per specificare un allegato di input per il modulo adattivo.

      * **Scegli JSON di input:** Seleziona un file JSON di input utilizzando un percorso relativo al payload o memorizzato in una variabile di tipo di dati Document, JSON o Form Data Model. Questa opzione è disponibile se si seleziona Interfaccia utente agente comunicazione interattiva o Documento canale web comunicazione interattiva dall’elenco a discesa Tipo.
      * **Scegli un servizio di precompilazione personalizzato:** Seleziona il servizio di precompilazione per recuperare i dati e precompilare il documento del canale web di comunicazione interattiva o l&#39;interfaccia utente dell&#39;agente.
      * **Utilizza il servizio di precompilazione della comunicazione interattiva selezionata in precedenza:** Utilizza questa opzione per utilizzare il servizio di precompilazione della comunicazione interattiva definito nell&#39;elenco a discesa Usa comunicazione interattiva.
      * **Mappatura attributo richiesta:** Utilizzare la sezione Mappatura attributo richiesta per definire il [nome e il valore dell&#39;attributo richiesta](../../forms/using/work-with-form-data-model.md#bindargument). Recupera i dettagli dall’origine dati in base al nome e al valore dell’attributo specificati nella richiesta. È possibile definire un valore di attributo della richiesta utilizzando un valore letterale o una variabile di tipo di dati String.\
        Il servizio di precompilazione e le opzioni di mappatura degli attributi della richiesta sono disponibili solo se dall’elenco a discesa Tipo si seleziona Interfaccia utente agente di comunicazione interattiva o Documento canale web di comunicazione interattiva.

* **Informazioni inviate:** I campi elencati di seguito fungono da percorsi di output per l&#39;attività:

   * **Salva file di dati di output tramite:** Salva il file di dati (.json,. xml, .doc o modello dati modulo). Il file di dati contiene informazioni inviate tramite il modulo associato. Puoi salvare il file di dati di output utilizzando un percorso relativo al payload o memorizzarlo in una variabile di tipo Documento, XML o JSON. Ad esempio, [Payload_Directory]/Workflow/data, dove i dati sono un file.
   * **Salva allegati tramite:** Salva gli allegati del modulo forniti in un&#39;attività. È possibile salvare gli allegati utilizzando un percorso relativo al payload o memorizzarlo in una variabile di matrice del tipo di dati Document.
   * **Salva documento di record utilizzando:** Percorso per salvare un file del documento di record. Ad esempio, [Directory_Payload]/DocumentofRecord/credit-card.pdf. Puoi salvare il documento record utilizzando un percorso relativo al payload o memorizzarlo in una variabile di tipo Dati documento. Se si seleziona l&#39;opzione **Relativo al payload**, il documento di record non viene generato se il campo percorso viene lasciato vuoto. Questa opzione è disponibile solo se si seleziona Modulo adattivo dall’elenco a discesa Tipo.

   * **Salvare i dati del canale Web utilizzando:** Salvare il file di dati del canale Web utilizzando un percorso relativo al payload o memorizzarlo in una variabile di tipo Documento, JSON o Modello dati modulo. Questa opzione è disponibile solo se dall’elenco a discesa Tipo selezioni Interfaccia utente agente di comunicazione interattiva.
   * **Salva documento PDF tramite:** Salva il documento PDF utilizzando un percorso relativo al payload o archivialo in una variabile di tipo dati Documento. Questa opzione è disponibile solo se dall’elenco a discesa Tipo selezioni Interfaccia utente agente di comunicazione interattiva.
   * **Salva modello di layout utilizzando:** Salva il modello di layout utilizzando un percorso relativo al payload o memorizzalo in una variabile di tipo dati Documento. Il [modello di layout](../../forms/using/layout-design-details.md) fa riferimento a un file XDP creato con Forms Designer. Questa opzione è disponibile solo se dall’elenco a discesa Tipo selezioni Interfaccia utente agente di comunicazione interattiva.

* **Assegnatario > Assegna opzioni:** Specificare il metodo per assegnare l&#39;attività a un utente. È possibile assegnare dinamicamente l&#39;attività a un utente o a un gruppo utilizzando lo script Selettore partecipanti oppure assegnare l&#39;attività a un utente o a un gruppo AEM specifico.
* **Selettore partecipanti:** L&#39;opzione è disponibile quando l&#39;opzione **Assegna dinamicamente a un utente o a un gruppo** è selezionata nel campo Assegna opzioni. È possibile utilizzare un codice ECMAScript o un servizio per selezionare dinamicamente un utente o un gruppo. Per ulteriori informazioni, vedere [Assegnazione dinamica di un flusso di lavoro agli utenti](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Creazione di un passaggio personalizzato Partecipante dinamico Adobe Experience Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it&amp;CID=RedirectAEMCommunityKautuk)

* **Partecipanti:** Il campo è disponibile quando l&#39;opzione **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** è selezionata nel campo **Selettore partecipanti**. Il campo consente di selezionare utenti o gruppi per l&#39;opzione RandomParticipantChooser.

* **Assegnatario:** Il campo è disponibile quando **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** è selezionato nel campo **Selettore partecipanti**. Il campo consente di selezionare una variabile di tipo String per definire l’assegnatario.

* **Argomenti:** Il campo è disponibile quando nel campo Selettore partecipanti è selezionato uno script diverso da RandomParticipantChoose. Il campo consente di fornire un elenco di argomenti separati da virgole per lo script selezionato nel campo Selettore partecipanti.

* **Utente o gruppo:** l&#39;attività è assegnata all&#39;utente o al gruppo selezionato. L&#39;opzione è disponibile quando l&#39;opzione **A un utente o gruppo specifico** è selezionata nel campo **Assegna opzioni**. Il campo elenca tutti gli utenti e i gruppi del gruppo flusso di lavoro-utenti.\
  Il menu a discesa **Utente o Gruppo** elenca gli utenti e i gruppi a cui l&#39;utente connesso ha accesso. La visualizzazione del nome utente dipende dalla disponibilità delle autorizzazioni di accesso per il nodo **users** in crx-repository per quel particolare utente.

* **[!UICONTROL Invia e-mail di notifica]**: selezionare questa opzione per inviare notifiche e-mail all&#39;assegnatario. Queste notifiche vengono inviate quando un’attività viene assegnata a un utente o a un gruppo. È possibile utilizzare l&#39;opzione **[!UICONTROL Indirizzo e-mail destinatario]** per specificare il meccanismo di recupero dell&#39;indirizzo e-mail.

* **[!UICONTROL Indirizzo e-mail destinatario]**: è possibile memorizzare l&#39;indirizzo e-mail in una variabile, utilizzare un valore letterale per specificare un indirizzo e-mail permanente o utilizzare l&#39;indirizzo e-mail predefinito dell&#39;assegnatario specificato nel profilo dell&#39;assegnatario. Puoi utilizzare il letterale o una variabile per specificare l’indirizzo e-mail di un gruppo. L’opzione della variabile è utile per recuperare e utilizzare in modo dinamico un indirizzo e-mail. L&#39;opzione **[!UICONTROL Usa indirizzo e-mail predefinito dell&#39;assegnatario]** è riservata a un solo assegnatario. In questo caso, viene utilizzato l’indirizzo e-mail memorizzato nel profilo utente degli assegnatari.

* **Modello e-mail HTML**: seleziona il modello e-mail per l&#39;e-mail di notifica. Per modificare un modello, modifica il file che si trova in /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt in crx-repository.
* **Consenti delega a:** La Posta in arrivo AEM fornisce un&#39;opzione all&#39;utente connesso per delegare il flusso di lavoro assegnato a un altro utente. Puoi delegare all’interno dello stesso gruppo o all’utente del flusso di lavoro di un altro gruppo. Se l&#39;attività è assegnata a un singolo utente e l&#39;opzione **consenti delega ai membri del gruppo assegnatario** è selezionata, non è possibile delegare l&#39;attività a un altro utente o gruppo.
* **Impostazioni condivisione:** La casella in entrata AEM fornisce le opzioni per condividere una o tutte le attività della casella in entrata con altri utenti:
   * Quando l&#39;opzione **Consenti all&#39;assegnatario di condividere in modo esplicito la cartella Posta in arrivo** è selezionata, l&#39;utente può fare clic sull&#39;attività e condividerla con un altro utente AEM.
   * Quando l&#39;opzione **Consenti all&#39;assegnatario di condividere tramite la condivisione della casella in entrata** è selezionata e un utente condivide i propri elementi della casella in entrata o consente ad altri utenti di accedere ai propri elementi della casella in entrata, solo le attività con l&#39;opzione sopra indicata abilitata vengono condivise con altri utenti.

* **Azioni > Azioni predefinite:** Sono disponibili le azioni Invia, Salva e Reimposta. Per impostazione predefinita, sono attivate tutte le azioni predefinite.
* **Variabile di route:** Nome della variabile di route. La variabile di route acquisisce le azioni personalizzate selezionate da un utente nella casella in entrata AEM.
* **Route:** un&#39;attività può diramarsi in route diverse. Se selezionata nella casella in entrata AEM, la route restituisce un valore e i rami del flusso di lavoro si basano sulla route selezionata. È possibile archiviare le route in una variabile di tipo di dati String oppure selezionare **Letterale** per aggiungere le route manualmente.

* **Titolo**: specificare il titolo della route. Viene visualizzato nella casella in entrata AEM.
* **Icona rosso corallo**: specificare l&#39;attributo HTML di un&#39;icona rosso corallo. La libreria CorelUI di Adobe fornisce un ampio set di icone touch-first. È possibile scegliere e utilizzare un&#39;icona per il ciclo di lavorazione. Viene visualizzato insieme al titolo nella casella in entrata AEM. Se memorizzi le route in una variabile, le route utilizzano un&#39;icona di corallo &quot;Tag&quot; predefinita.
* **Consenti all&#39;assegnatario di aggiungere commenti**: selezionare questa opzione per abilitare i commenti per l&#39;attività. L’assegnatario può aggiungere i commenti dalla casella in entrata AEM al momento dell’invio dell’attività.
* **Salva commento nella variabile:** Salva il commento in una variabile di tipo dati String. Questa opzione viene visualizzata solo se si seleziona la casella di controllo **Consenti all&#39;assegnatario di aggiungere commenti**.

* **Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività**: selezionare questa opzione per abilitare gli allegati per l&#39;attività. L’assegnatario può aggiungere gli allegati dalla casella in entrata AEM al momento dell’invio dell’attività.
* **Salva allegati attività di output tramite**: specifica il percorso della cartella degli allegati. È possibile salvare gli allegati delle attività di output utilizzando un percorso relativo al payload o in una variabile di matrice del tipo di dati del documento. Questa opzione viene visualizzata solo se si seleziona la casella di controllo **Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività** e si seleziona **Modulo adattivo**, **Modulo adattivo di sola lettura** o **Documento PDF non interattivo** dall&#39;elenco a discesa **Tipo** nella scheda **Modulo/Documento**.

>[!NOTE]
>
>Utilizzare la scheda Allegati nell&#39;interfaccia utente dell&#39;agente durante il runtime per associare gli allegati a una comunicazione interattiva. Gli allegati associati vengono visualizzati come allegati delle attività nella barra laterale dopo l&#39;apertura dell&#39;elemento di lavoro in stato Completato.

* **Usa metadati personalizzati:** Selezionare questa opzione per abilitare il campo metadati personalizzato. I metadati personalizzati vengono utilizzati nei modelli e-mail.
* **Metadati personalizzati:** Selezionare metadati personalizzati per i modelli di posta elettronica. I metadati personalizzati sono disponibili nel crx-repository in apps/fd/dashboard/scripts/metadataScripts. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Puoi anche utilizzare un servizio per i metadati personalizzati. È inoltre possibile estendere l&#39;interfaccia WorkitemUserMetadataService per fornire metadati personalizzati.
* **Mostra dati da passaggi precedenti**: selezionare questa opzione per consentire agli assegnatari di visualizzare gli assegnatari precedenti, le azioni già eseguite sull&#39;attività, i commenti aggiunti all&#39;attività e il documento di record dell&#39;attività completata, se disponibile.
* **Mostra dati da passaggi successivi:** Selezionare questa opzione per consentire all&#39;assegnatario corrente di visualizzare l&#39;azione eseguita e i commenti aggiunti all&#39;attività dagli assegnatari successivi. Consente inoltre all’assegnatario corrente di visualizzare un documento di record dell’attività completata, se disponibile.
* **Visibilità del tipo di dati:** Per impostazione predefinita, un assegnatario può visualizzare un documento di record, assegnatari, azioni intraprese e commenti aggiunti dagli assegnatari precedenti e successivi. Utilizza l’opzione visibilità del tipo di dati per limitare il tipo di dati visibile agli assegnatari.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e per recuperare la cronologia del passaggio Assegna attività sono disabilitate quando si configura un modello di flusso di lavoro [!DNL Adobe Experience Manager] per l&#39;archiviazione dati esterna. Inoltre, nella casella in entrata, l’opzione di salvataggio è disabilitata.

## Passaggio Invia e-mail {#send-email-step}

Utilizza la fase e-mail per inviare un’e-mail, ad esempio un messaggio e-mail con un documento record, un collegamento di un modulo adattivo, un collegamento di una comunicazione interattiva o un documento PDF allegato. Il passaggio Invia e-mail supporta [e-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Le e-mail di HTML sono dinamiche e si adattano alle dimensioni del client e-mail e dello schermo dei destinatari. Puoi utilizzare un modello di e-mail HTML per definire l’aspetto, la combinazione di colori e il comportamento dell’e-mail.

Il passaggio e-mail utilizza Day CQ Mail Service per inviare le e-mail. Prima di utilizzare il passaggio e-mail, assicurati che il servizio e-mail [&#128279;](../../forms/using/aem-forms-workflow.md) sia configurato. Il passaggio e-mail presenta le seguenti proprietà:

**Titolo:** Il titolo del passaggio consente di identificare il passaggio nell&#39;editor del flusso di lavoro.

**Descrizione:** La spiegazione è utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

**Oggetto e-mail:** L&#39;oggetto può essere recuperato da metadati di un flusso di lavoro, specificato manualmente o recuperato dal valore archiviato in una variabile. Selezionare una delle opzioni seguenti:

* **Valore letterale -** Specificare manualmente un oggetto.
* **Recupera dai metadati del flusso di lavoro** - Recupera l&#39;oggetto da una proprietà dei metadati.
* **Variabile** - Recupera l&#39;oggetto dal valore memorizzato in una variabile di tipo dati stringa.

**Modello e-mail HTML**: modello HTML per l&#39;e-mail. Puoi specificare le variabili in un modello e-mail. Il passaggio E-mail estrae e visualizza tutte le variabili incluse in un modello per gli input.

**Metadati modello e-mail:** Il valore delle variabili del modello e-mail può essere un valore specificato dall&#39;utente, il percorso di una risorsa nell&#39;autore o nel server di pubblicazione, un&#39;immagine o una proprietà dei metadati del flusso di lavoro.

* **Valore letterale:** Utilizzare l&#39;opzione quando si conosce il valore esatto da specificare. Ad esempio, [example@example.com](mailto:example@example.com).

* **Metadati flusso di lavoro:** Utilizzare l&#39;opzione quando il valore da utilizzare viene salvato in una proprietà dei metadati del flusso di lavoro. Dopo aver selezionato l’opzione, immetti il nome della proprietà dei metadati nella casella di testo vuota sotto l’opzione Metadati del flusso di lavoro. Ad esempio, emailAddress.
* **URL risorsa:** Utilizza l&#39;opzione per incorporare un collegamento web di una comunicazione interattiva nell&#39;e-mail. Dopo aver selezionato l’opzione, sfoglia e scegli la comunicazione interattiva da incorporare. La risorsa può trovarsi nel server di authoring o di pubblicazione.
* **Immagine:** Utilizza l&#39;opzione per incorporare un&#39;immagine nell&#39;e-mail. Dopo aver selezionato l’opzione, sfoglia e scegli l’immagine. L&#39;opzione immagine è disponibile solo per i tag immagine (&lt;img src=&quot;&#42;&quot;/>) disponibili nel modello e-mail.

**Indirizzo e-mail del mittente/destinatario:** Seleziona l&#39;opzione **Letterale** per specificare manualmente un indirizzo e-mail o seleziona l&#39;opzione **Recupera dai metadati del flusso di lavoro** per recuperare l&#39;indirizzo e-mail da una proprietà dei metadati. È inoltre possibile specificare un elenco di matrici di proprietà dei metadati per l&#39;opzione **Recupera dai metadati del flusso di lavoro**. Selezionare l&#39;opzione **Variabile** per recuperare l&#39;indirizzo di posta elettronica dal valore memorizzato in una variabile di tipo di dati stringa.

**File allegato:** La risorsa disponibile nel percorso specificato è allegata all&#39;e-mail. Il percorso della risorsa può essere relativo al payload o al percorso assoluto. Il percorso di esempio è [Payload_Directory]/allegati/.

Selezionare l&#39;opzione **Variabile** per recuperare l&#39;allegato archiviato in una variabile di tipo Documento, XML o JSON.

**Nome file:** Nome del file allegato e-mail. Il passaggio E-mail modifica il nome file originale dell’allegato con il nome file specificato. Il nome può essere specificato manualmente o recuperato da una proprietà o variabile di metadati del flusso di lavoro. Utilizza l&#39;opzione **Letterale** quando conosci il valore esatto da specificare. Utilizzare l&#39;opzione **Variabile** per recuperare il nome del file dal valore memorizzato in una variabile di tipo di dati stringa. Utilizzare l&#39;opzione **Recupera da un flusso di lavoro metadati** quando il valore da utilizzare viene salvato in una proprietà dei metadati del flusso di lavoro.

## Passaggio Genera documento di record {#generate-document-of-record-step}

Quando un modulo viene compilato o inviato, è possibile conservarne una registrazione, in formato cartaceo o in formato documento. Questo documento è denominato documento di record (DoR). È possibile utilizzare il passaggio Genera documento di record per creare una versione PDF interattiva o di sola lettura di un modulo adattivo. La versione per PDF contiene informazioni inserite nel modulo insieme al layout del modulo adattivo.

Il passaggio Documento record presenta le seguenti proprietà:

**Usa modulo adattivo**: specifica il metodo per individuare il modulo adattivo di input. Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso nel campo **Seleziona variabile per risolvere**.\
È possibile associare più moduli adattivi a un flusso di lavoro. Di conseguenza, puoi specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

**Percorso modulo adattivo**: specifica il percorso del modulo adattivo. Il campo è disponibile quando si seleziona l&#39;opzione **Disponibile in un percorso assoluto** dal campo **Usa modulo adattivo**.

**Selezionare i dati di input utilizzando:** Percorso dei dati di input per il modulo adattivo. È possibile mantenere i dati in una posizione relativa al payload, specificare un percorso assoluto dei dati o recuperare i dati memorizzati in una variabile di tipo Documento, JSON o XML. I dati di input vengono uniti al modulo adattivo per creare un documento di record.

**Selezionare il percorso dell&#39;allegato di input utilizzando:** Percorso degli allegati. Questi allegati sono inclusi nel documento di record. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di matrice di tipo dati Documento.

Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella vengono allegati al documento di record. Se nelle cartelle sono disponibili file direttamente disponibili nel percorso di allegato specificato, tali file vengono inclusi nel documento di record come allegati. Le eventuali cartelle presenti nelle cartelle direttamente disponibili vengono ignorate.

**Salva documento di record generato utilizzando le opzioni seguenti:** Specificare il percorso in cui conservare il file del documento di record. Puoi scegliere di sovrascrivere la cartella del payload, inserire il documento di record in una posizione all’interno della directory del payload o archiviare il documento di record in una variabile di tipo dati Documento.

**Impostazioni locali**: specificare la lingua del documento record. Selezionare **Letterale** per selezionare le impostazioni locali da un elenco a discesa oppure selezionare **Variabile** per recuperare le impostazioni locali dal valore memorizzato in una variabile di tipo di dati stringa. Definisci il codice locale durante la memorizzazione del valore della lingua in una variabile. Ad esempio, specifica **en_US** per l&#39;inglese e **fr_FR** per il francese.

## Passaggio del servizio Richiama modello dati modulo {#invoke-form-data-model-service-step}

È possibile utilizzare [Integrazione dati di AEM Forms](../../forms/using/data-integration.md) per configurare e connettersi a diverse origini dati. Queste origini dati possono essere un database, un servizio Web, un servizio REST, un servizio OData e una soluzione CRM. L’integrazione dei dati di AEM Forms consente di creare un modello di dati modulo che include vari servizi per eseguire operazioni di recupero, aggiunta e aggiornamento dei dati sul database configurato. È possibile utilizzare il passaggio **Richiama servizio modello dati** per selezionare un modello dati modulo (FDM) e utilizzare i servizi di FDM per recuperare, aggiornare o aggiungere dati a origini dati diverse.

Per spiegare gli input per i campi del passaggio, vengono utilizzati, ad esempio, la seguente tabella di database e il seguente file JSON:

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

Il passaggio Richiama servizio modello dati modulo include i campi elencati di seguito per facilitare le operazioni del modello dati modulo:

* **Titolo:** Titolo del passaggio. Consente di identificare il passaggio nell’editor del flusso di lavoro.
* **Descrizione:** Spiegazione utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **Percorso modello dati modulo**: sfogliare e selezionare un modello dati modulo presente nel server.

* **Servizio**: elenco dei servizi forniti dal modello dati del modulo selezionato.
* **Input per servizi > Fornisci dati di input utilizzando metadati letterali, variabili o del flusso di lavoro e un file JSON**: un servizio può avere più argomenti. Seleziona l’opzione per ottenere il valore degli argomenti del servizio da una proprietà di metadati del flusso di lavoro, da un oggetto JSON, da una variabile o inserisci direttamente il valore nella casella di testo fornita:

   * **Valore letterale:** Utilizzare l&#39;opzione quando si conosce il valore esatto da specificare. Ad esempio, srose@we.info.
   * **Variabile:** Utilizzare l&#39;opzione per recuperare il valore archiviato in una variabile.
   * **Recupera dai metadati del flusso di lavoro:** Utilizzare l&#39;opzione quando il valore da utilizzare viene salvato in una proprietà dei metadati del flusso di lavoro. Ad esempio, emailAddress.
   * **[!UICONTROL Relativo al payload]**: utilizzare l&#39;opzione per recuperare l&#39;allegato salvato in un percorso relativo al payload. Selezionare l&#39;opzione e specificare il nome della cartella che include il file allegato oppure specificare il nome del file allegato nella casella di testo.

     Se ad esempio la cartella Relativa al payload nel repository di CRX include un file allegato nel percorso `attachment\attachment-folder`, specificare `attachment\attachment-folder` nella casella di testo dopo aver selezionato l&#39;opzione **[!UICONTROL Relativa al payload]**.
   * **JSON Dot Notation:** Utilizzare l&#39;opzione quando il valore da utilizzare si trova in un file JSON. Ad esempio, insurance.customerDetails.emailAddress. L’opzione JSON Dot Notation è disponibile solo se è selezionata l’opzione Mappa campi di input da JSON di input.
   * **Eseguire il mapping dei campi di input dal JSON di input:** Specificare il percorso di un file JSON per ottenere il valore di input di alcuni argomenti del servizio dal file JSON. Il percorso del file JSON può essere relativo al payload, un percorso assoluto oppure puoi selezionare un documento JSON di input utilizzando una variabile di tipo JSON o Modello dati modulo.

* **Input per servizi > Fornisci dati di input utilizzando una variabile o un file JSON:** Seleziona l&#39;opzione per ottenere valori per tutti gli argomenti da un file JSON salvato in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **Selezionare il documento JSON di input utilizzando**: il file JSON contenente i valori per tutti gli argomenti del servizio. Il percorso del file JSON può essere **relativo al payload** o **percorso assoluto.** È inoltre possibile recuperare il documento JSON di input utilizzando una variabile di tipo di dati JSON o Form Data Model.

* **Notazione punti JSON:** Lasciare vuoto il campo per utilizzare tutti gli oggetti del file JSON specificato come input per gli argomenti del servizio. Per leggere un oggetto JSON specifico dal file JSON specificato come input per gli argomenti del servizio, specifica la notazione del punto per l’oggetto JSON. Ad esempio, se disponi di un JSON simile a quello elencato all’inizio della sezione, specifica insurance.customerDetails per fornire tutti i dettagli di un cliente come input per il servizio.
* **Output del servizio > Mappa e scrivi i valori di output in una variabile o nei metadati:** Selezionare l&#39;opzione per salvare i valori di output come proprietà del nodo dei metadati dell&#39;istanza del flusso di lavoro in crx-repository. Specifica il nome della proprietà dei metadati e seleziona l’attributo di output del servizio corrispondente da mappare con la proprietà dei metadati. Ad esempio, mappa phone_number restituito dal servizio di output con la proprietà phone_number dei metadati del flusso di lavoro. Allo stesso modo, puoi memorizzare l’output in una variabile di tipo dati Long. Quando si seleziona una proprietà per l&#39;opzione **[!UICONTROL Attributo di output del servizio da mappare]**, vengono compilate solo le variabili in grado di memorizzare i dati della proprietà selezionata per l&#39;opzione **[!UICONTROL Salva output in]**.

* **Output del servizio > Salva output in una variabile o in un file JSON:** Selezionare l&#39;opzione per salvare i valori di output in un file JSON in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **Salva documento JSON di output utilizzando le opzioni seguenti:** Salva il file JSON di output. Il percorso del file JSON di output può essere relativo al payload o a un percorso assoluto. Puoi anche salvare il file JSON di output utilizzando una variabile di tipo di dati JSON o Modello dati modulo.

## Passaggio Firma documento {#sign-document-step}

Il passaggio Firma documento consente di utilizzare Adobe Sign per firmare i documenti. Il passaggio Firma documento presenta le seguenti proprietà:

* **Nome contratto:** Specificare il titolo del contratto. Il nome del contratto diventa parte dell’oggetto e del corpo del testo dell’e-mail inviata ai destinatari. È possibile archiviare il nome in una variabile di tipo di dati String oppure selezionare **Letterale** per aggiungere il nome manualmente.

* **Impostazioni internazionali:** Specificare la lingua per le opzioni di posta elettronica e verifica. È possibile archiviare le impostazioni locali in una variabile di tipo di dati String oppure selezionare **Letterale** per scegliere le impostazioni locali dall&#39;elenco delle opzioni disponibili. Definisci il codice locale durante la memorizzazione del valore della lingua in una variabile. Ad esempio, specifica **en_US** per l&#39;inglese e **fr_FR** per il francese.

* **Configurazione cloud Adobe Sign**: scegli una configurazione cloud Adobe Sign. Se non hai configurato Adobe Sign per AEM Forms, consulta [Integrare Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Selezionare il documento da firmare utilizzando:** È possibile scegliere un documento da una posizione relativa al payload, utilizzare il payload come documento, specificare un percorso assoluto del documento o recuperare il documento memorizzato in una variabile di tipo dati Documento.


* **Selezionare il percorso allegato di input utilizzando:** Percorso degli allegati. Questi allegati sono inclusi nel documento di firma. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di matrice di tipo dati Documento.


  Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella verranno allegati al documento di firma. Se nelle cartelle sono disponibili file direttamente disponibili nel percorso di allegato specificato, tali file vengono inclusi nel documento di firma come allegati. Le eventuali cartelle presenti nelle cartelle direttamente disponibili vengono ignorate.

* **Giorni fino alla scadenza:** Un documento è contrassegnato come scadenza (scadenza passata) dopo che non è presente alcuna attività per il numero di giorni specificato nel campo **Giorni fino alla scadenza**. Il numero di giorni viene conteggiato dopo che il documento è stato assegnato a un utente per la firma.
* **Frequenza e-mail promemoria:** Puoi inviare un messaggio e-mail di promemoria ogni giorno o ogni settimana. La settimana viene conteggiata dal giorno in cui il documento viene assegnato a un utente per la firma.
* **Processo di firma:** È possibile scegliere di firmare un documento in ordine sequenziale o parallelo. In ordine sequenziale, un destinatario riceve il documento alla volta per la firma. Dopo che il primo destinatario ha completato la firma del documento, il documento viene inviato al secondo destinatario e così via. In parallelo, più destinatari possono firmare un documento alla volta.
* **URL di reindirizzamento:** Specificare un URL di reindirizzamento. Dopo aver firmato il documento, puoi reindirizzare l’assegnatario a un URL. Di solito, questo URL contiene un messaggio di ringraziamento o ulteriori istruzioni.
* **Fase flusso di lavoro:** Un flusso di lavoro può avere più fasi. Questi stadi vengono visualizzati nella casella in entrata AEM. Potete definire questi stadi nelle proprietà del modello (Sidekick > Pagina > Proprietà pagina > Stadi).
* **Selezionare i destinatari:** Specificare il metodo per scegliere il destinatario del documento. Puoi assegnare dinamicamente il flusso di lavoro a un utente o a un gruppo oppure aggiungere manualmente i dettagli di un destinatario. Quando selezioni Manualmente nel menu a discesa, aggiungi i dettagli del destinatario come E-mail, Ruolo e Metodo di autenticazione.

  >[!NOTE]
  >
  >* Nella sezione Ruolo è possibile specificare il ruolo del destinatario come Firmatario, Approvatore, Accettatore, Destinatario certificato, Form Filler e Delegatore.
  >* Se si seleziona Delegante nell&#39;opzione Ruolo, il Delegante può assegnare l&#39;attività di firma a un altro destinatario.
  >* Se è stato configurato un metodo di autenticazione per [!DNL Adobe Sign], in base alla configurazione selezionata verrà selezionato un metodo di autenticazione, ad esempio l&#39;autenticazione basata su telefono, l&#39;autenticazione basata su identità social, l&#39;autenticazione basata su Knowledge, l&#39;autenticazione basata su identità pubblica.


* **Script o servizio per selezionare i destinatari:** L&#39;opzione è disponibile solo se si seleziona Dinamicamente nel campo Seleziona destinatari. È possibile specificare un ECMAScript o un servizio per scegliere i destinatari e le opzioni di verifica per un documento.
* **Dettagli destinatario:** L&#39;opzione è disponibile solo se l&#39;opzione Manualmente è selezionata nel campo Seleziona destinatari. Specifica l’indirizzo e-mail e scegli un meccanismo di verifica opzionale. Prima di selezionare un meccanismo di verifica in due fasi, accertati che l’opzione di verifica corrispondente sia abilitata per l’account Adobe Sign configurato. È possibile utilizzare una variabile di tipo String per definire i valori per i campi **[!UICONTROL Email]**, **[!UICONTROL Codice paese]** e **[!UICONTROL Numero telefono]**. I campi **[!UICONTROL Codice paese]** e **[!UICONTROL Numero di telefono]** vengono visualizzati solo se si seleziona **[!UICONTROL Verifica telefono]** dall&#39;elenco a discesa **in** 2 passaggi di verifica.
* **Variabile di stato:** un documento abilitato per Adobe Sign memorizza lo stato di firma del documento in una variabile di tipo dati String. Specifica il nome della variabile di stato (adobeSignStatus). Una variabile di stato di un’istanza è disponibile in CRXDE in /etc/workflow/instances/&lt;server>/&lt;data-ora>/&lt;istanza del modello di flusso di lavoro>/workItems/&lt;nodo>/metaData contiene lo stato di una variabile.
* **[!UICONTROL Documento firmato]**: è possibile salvare lo stato del documento firmato in Variabile. Per aggiungere un audit trail della firma elettronica per una maggiore sicurezza e legalità al documento firmato, è possibile includere un rapporto di audit. È possibile salvare il documento firmato utilizzando la cartella Variabile o Payload.
  >[!NOTE]
  >
  > Il rapporto di audit viene aggiunto all&#39;ultima pagina del documento firmato.
<!--
* **Save signed document using below options:** Specify the location to keep signed documents. You can choose to overwrite the payload file, place the signed document at a location within the payload directory, or store the signed document in a variable of Document type.
-->

## Passaggi di Document Services {#document-services-steps}

I servizi di documentazione AEM sono un insieme di servizi per la creazione, l’assemblaggio e la protezione di documenti PDF. AEM Forms fornisce un passaggio del flusso di lavoro AEM separato per ogni servizio documentale.

Analogamente ad altri passaggi del flusso di lavoro di AEM Forms, come Assegna attività, Invia e-mail e Firma documento, puoi utilizzare le variabili in tutti i passaggi dei servizi documentali AEM. Per ulteriori informazioni sulla creazione e la gestione delle variabili, vedere [Variabili nei flussi di lavoro AEM](../../forms/using/variable-in-aem-workflows.md).

### Passaggio Applica marca temporale documento {#apply-document-time-stamp-step}

Aggiungere la marca temporale a un documento. È possibile specificare dettagli del documento quali il percorso del documento di input, il nome del documento di input e il percorso in cui memorizzare i dati esportati. Puoi scegliere di sovrascrivere il file di payload esistente, scegliere un nome di file diverso per memorizzare i dati in un file diverso nella cartella di payload, fornire un percorso assoluto ai dati o archiviare i dati in una variabile di tipo Documento.

### Passaggio Converti in immagine {#convert-to-image-step}

Converte un documento PDF in un elenco di immagini. I formati immagine supportati sono JPEG, JPEG2000, PNG e TIFF. Le informazioni seguenti si applicano alle conversioni nelle immagini TIFF:

* Viene generato un file TIFF con più pagine.
* Alcune annotazioni non sono incluse nelle immagini TIFF. Le annotazioni che richiedono Acrobat per generare il loro aspetto non sono incluse.

### Passaggio Converti in PDF/A {#convert-to-pdf-a-step}

Converte un documento PDF in formato PDF/A utilizzando le opzioni fornite. La versione PDF/A di Portable Document Format (PDF) è specializzata nell&#39;archiviazione e nella conservazione a lungo termine dei documenti.

### Passaggio Converti in PS {#convert-to-ps-step}

Convertire documenti PDF in PostScript. Durante la conversione in PostScript, è possibile utilizzare l&#39;operazione di conversione per specificare il documento di origine e se eseguire la conversione in PostScript livello 2 o 3. Il documento PDF da convertire in un file PostScript deve essere non interattivo.

### Crea PDF dal passaggio del tipo specificato {#create-pdf-from-specified-type-step}

Genera un documento PDF da un file di input. Il documento di input può essere relativo al payload, avere un percorso assoluto, può essere il payload stesso o memorizzato in una variabile di tipo dati Documento.

### Crea PDF dal passaggio URL/HTML/ZIP {#create-pdf-from-url-html-zip-step}

Genera un documento PDF dall&#39;URL, dal HTML e dal file ZIP forniti.

### Passaggio Esporta dati {#export-data-step}

Esporta dati da un file PDF forms o XDP. È necessario immettere il percorso del file del documento di input e il formato dei dati di esportazione. Le opzioni per Export Data Format sono Auto, XDP e XmlData.

### Export PDF al passaggio del tipo specificato {#export-pdf-to-specified-type-step}

Converte un documento PDF in un formato selezionato.

### Genera passaggio di PDF non interattivo {#generatenoninteractive}

Genera un PDF non interattivo. Offre diverse opzioni di personalizzazione.

>[!NOTE]
>
>È possibile utilizzare le variabili per specificare il file modello per i documenti di input. Memorizza il percorso del file modello in una variabile di tipo dati String.

### Passaggio Importa dati {#import-data-step}

Unisce i dati del modulo in un modulo PDF. È possibile importare i dati del modulo in un modulo PDF.

### Richiama passaggio DDX {#invokeddx}

Esegue il file DDX sulla mappa specificata dei documenti di input e restituisce i documenti PDF manipolati.

>[!NOTE]
>
>È possibile utilizzare le variabili per specificare il file DDX per i documenti di input. Memorizzare il file DDX in una variabile di tipo Documento o Dati XML.

### Passaggio di Optimize PDF {#optimize-pdf-step}

Ottimizza i file PDF riducendone le dimensioni. Il risultato di questa conversione è costituito da file PDF che potrebbero essere più piccoli delle versioni originali. Questa operazione converte anche i documenti PDF nella versione PDF specificata nei parametri di ottimizzazione.

Le impostazioni di ottimizzazione specificano la modalità di ottimizzazione dei file. Di seguito sono riportati alcuni esempi di impostazioni:

* Versione di Target PDF
* Eliminazione di oggetti quali azioni JavaScript e miniature di pagina incorporate
* Eliminazione dei dati utente come commenti e file allegati
* Eliminazione delle impostazioni non valide o inutilizzate
* Compressione di dati non compressi o utilizzo di algoritmi di compressione più efficienti
* Rimozione di font incorporati
* Impostazione dei valori di trasparenza

### Passaggio Rendering modulo PDF {#renderpdf}

Esegue il rendering di un modulo creato in Form Designer (XDP) in un modulo PDF.

>[!NOTE]
>
>È possibile utilizzare le variabili per specificare il file modello per i documenti di input. Memorizza il percorso del file modello in una variabile di tipo dati String.

### Passaggio Proteggi documento {#secure-document-step}

Crittografare, firmare e certificare un documento. AEM Forms supporta sia la crittografia basata su password che quella basata su certificato. È inoltre possibile scegliere tra diversi algoritmi per la firma dei documenti. Ad esempio, SHA-256 e SH-512. È inoltre possibile utilizzare il passaggio del flusso di lavoro per estendere i documenti di PDF. Il passaggio del flusso di lavoro fornisce opzioni per abilitare la decodifica del codice a barre, le firme digitali, l’importazione e l’esportazione di dati PDF e altre opzioni.

### Passaggio Invia a stampante {#send-to-printer-step}

Invia un documento direttamente a una stampante. Supporta i seguenti meccanismi di accesso alla stampa:

* **Stampante con accesso diretto**: una stampante installata nello stesso computer è denominata stampante con accesso diretto e il computer è denominato host stampante. Questo tipo di stampante può essere una stampante locale collegata direttamente al computer.
* **Stampante con accesso indiretto**: la stampante installata in un server di stampa è accessibile da altri computer. Per la connessione a una stampante di rete sono disponibili tecnologie quali il CUPS (Common UNIX® Printer System) e il protocollo LPD (Line Printer Daemon). Per accedere a una stampante con accesso indiretto, specificare il nome host o l&#39;indirizzo IP del server di stampa. Utilizzando questo meccanismo, è possibile inviare un documento a un URI LPD quando la rete dispone di un LPD in esecuzione. Il meccanismo consente di indirizzare il documento a qualsiasi stampante connessa alla rete che dispone di un LPD in esecuzione.

### Genera passaggio di output stampato {#generatePrintedOutput}

Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL in base a un progetto di modulo e a un file di dati. Il file di dati viene unito alla struttura del modulo e formattato per la stampa. L&#39;output generato da questo passaggio può essere inviato direttamente a una stampante o salvato come file. È consigliabile utilizzare questo passaggio quando si desidera utilizzare le progettazioni dei moduli o i dati di un&#39;applicazione. Se le progettazioni di moduli o moduli si trovano in rete, nel file system locale o in una posizione HTTP, utilizzare l&#39;operazione generatePrintedOutput.

Ad esempio, l&#39;applicazione richiede l&#39;unione di una struttura di modulo con un file di dati. I dati contengono centinaia di record. Inoltre, richiede che l&#39;output venga inviato a una stampante che supporta ZPL. La struttura del modulo e i dati di input sono inclusi in un&#39;applicazione. Utilizzare l&#39;operazione generatePrintedOutput per unire ogni record con una struttura di modulo e inviare l&#39;output a una stampante che supporta ZPL.

Il passaggio Genera output stampato ha le seguenti proprietà:

**Proprietà input**

* **[!UICONTROL Selezionare il file modello utilizzando]**: specificare il percorso del file modello. Puoi selezionare il file modello utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio, [Directory_Payload]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo. Inoltre, puoi anche accettare il payload come file di dati di input.

* **[!UICONTROL Seleziona documento dati tramite]**: specifica il percorso di un file di dati di input. Puoi selezionare il file di dati di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio, [Directory_Payload]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo.

* **[!UICONTROL Formato stampante]**: valore Formato di stampa che specifica il linguaggio di descrizione della pagina da utilizzare quando non viene fornito un file XDC per generare il flusso di output. Se fornisci un valore letterale, seleziona uno dei seguenti valori:

   * **[!UICONTROL PCL personalizzato]**: utilizzare l&#39;opzione per specificare un file XDC personalizzato per PCL.
   * **[!UICONTROL PostScript personalizzato]**: utilizzare l&#39;opzione per specificare un file XDC personalizzato per PostScript.
   * **[!UICONTROL ZPL]** personalizzato: utilizzare l&#39;opzione per specificare un file XDC personalizzato per ZPL.
   * **[!UICONTROL PCL colore generico (5c)]**: utilizzare un PCL colore generico (5c).
   * **[!UICONTROL PostScript generico livello3]**: utilizzare PostScript generico livello 3.
   * **[!UICONTROL ZPL 300 DPI]**: utilizzare ZPL 300 DPI. Viene utilizzato zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: utilizzare ZPL 600 DPI. Viene utilizzato il file zpl600.xdc.
   * **[!UICONTROL IPL personalizzato]**: utilizzare l&#39;opzione per specificare un file XDC personalizzato per IPL.
   * **[!UICONTROL IPL 300 DPI]**: utilizzare IPL 300 DPI. Viene utilizzato ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: utilizzare IPL 400 DPI. Viene utilizzato il file ipl400.xdc.
   * **[!UICONTROL TPCL personalizzato]**: utilizzare l&#39;opzione per specificare un file XDC personalizzato per TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: utilizzare TPCL 300 DPI. Viene utilizzato il file tpcl305.xdc.
   * **[!UICONTROL PCL 600 DPI]**: utilizzare TPCL 600 DPI. Viene utilizzato il file tpcl600.xdc.
   * **[!UICONTROL DPL personalizzato]**: utilizzare l&#39;opzione per specificare un DPL per file XDC personalizzato.
   * **[!UICONTROL DPL300DPI]**: utilizzare DPL 300 DPI. Viene utilizzato il file dpl300.xdc.
   * **[!UICONTROL DPL406DPI]**: utilizzare DPL 400 DPI. Viene utilizzato dpl406.xdc.
   * **[!UICONTROL DPL600DPI]**: utilizzare DPL 600 DPI. Viene utilizzato dpl600.xdc.

**Proprietà output**

* **[!UICONTROL Salva documento di output tramite]**: specificare il percorso in cui salvare il file di output. Puoi salvare il file di output in una posizione relativa al payload, in una variabile, oppure specificare una posizione assoluta per salvare il file di output. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo.

**Proprietà avanzate**

* **[!UICONTROL Selezionare il percorso della directory principale del contenuto utilizzando]**: la directory principale del contenuto è un valore stringa che specifica l&#39;URI, il riferimento assoluto o il percorso nel repository per recuperare le risorse relative utilizzate dalla progettazione del modulo. Ad esempio, se la progettazione del modulo fa riferimento a un’immagine relativamente, come ../myImage.gif, myImage.gif deve trovarsi in repository://. Il valore predefinito è repository://, che punta al livello principale dell’archivio.

  Quando scegli una risorsa dall’applicazione, il percorso URI della directory principale del contenuto deve avere la struttura corretta. Ad esempio, se un modulo viene scelto da un’applicazione denominata SampleApp e si trova in SampleApp/1.0/forms/Test.xdp, l’URI della directory principale dei contenuti deve essere specificato come repository://administrator@password/Applications/SampleApp/1.0/forms/ o repository:/Applications/SampleApp/1.0/forms/ (quando l’autorità è null). Quando l’URI della directory principale del contenuto viene specificato in questo modo, i percorsi di tutte le risorse a cui si fa riferimento nel modulo verranno risolti in base a questo URI.

* **[!UICONTROL Seleziona file XCI tramite]**: i file XCI vengono utilizzati per descrivere i font e altre proprietà utilizzati per gli elementi di progettazione dei moduli. È possibile mantenere un file XCI relativo al payload, in un percorso assoluto o utilizzando una variabile di tipo dati Documento.

* **[!UICONTROL Impostazioni locali]**: specifica la lingua utilizzata per generare il documento PDF. Se fornisci un valore letterale, seleziona una lingua dall’elenco o scegli uno dei seguenti valori:
   * **Per utilizzare il server predefinito**:
Impostazione predefinita. Utilizza l&#39;impostazione Locale configurata sul server AEM Forms. L&#39;impostazione Locale viene configurata utilizzando la console di amministrazione. (Vedi [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_65_it).)

   * **Per utilizzare un valore personalizzato**:
Digita il codice locale nella casella letterale o seleziona una variabile stringa contenente il codice locale. Per un elenco completo dei codici delle impostazioni internazionali supportati, vedere https://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copie]**: valore intero che specifica il numero di copie da generare per l&#39;output. Il valore predefinito è 1.

* **[!UICONTROL Stampa fronte retro]**: valore di paginazione che specifica se utilizzare la stampa fronte/retro o fronte/retro. Le stampanti che supportano PostScript e PCL utilizzano questo valore. Se fornisci un valore letterale, seleziona uno dei seguenti valori:
   * **[!UICONTROL Edge lungo fronte-retro]**: utilizzare la stampa fronte-retro e la stampa utilizzando la paginazione a lato lungo.
   * **[!UICONTROL Edge corto fronte-retro]**: utilizzare la stampa fronte-retro e la stampa utilizzando la paginazione lato-corto.
   * **[!UICONTROL Simplex]**: utilizzare la stampa fronte/retro.