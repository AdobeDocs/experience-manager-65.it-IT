---
title: Flusso di lavoro Forms basato su OSGi - Riferimento passo
seo-title: Flusso di lavoro Forms basato su OSGi - Riferimento passo
description: Flusso di lavoro Forms incentrato sui passaggi OSGi per creare rapidamente flussi di lavoro basati su moduli adattivi.
seo-description: Flusso di lavoro Forms incentrato sui passaggi OSGi per creare rapidamente flussi di lavoro basati su moduli adattivi.
uuid: 6f791c45-0e35-4c55-9106-5340caab94b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: f0a5588d-f210-4f04-bc35-b62834f90ab1
docset: aem65
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '7109'
ht-degree: 0%

---


# Flusso di lavoro Forms incentrato su OSGi - Riferimento passo{#forms-centric-workflow-on-osgi-step-reference}

## Passaggi Forms Workflow {#forms-workflow-steps}

I passaggi del flusso di lavoro Forms eseguono  operazioni specifiche di AEM Forms in un flusso di lavoro AEM. Questi passaggi consentono di creare rapidamente in OSGi un flusso di lavoro basato su Forms basato su moduli adattivi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di revisione e approvazione di base, processi aziendali interni e attraverso il firewall. È inoltre possibile utilizzare i passaggi di Forms Workflow per avviare Document Services, integrarsi con  flusso di lavoro di firma Adobe Sign ed eseguire altre operazioni  AEM Forms. È necessario [ componente aggiuntivo AEM Forms](https://www.adobe.com/go/learn_aemforms_documentation_63) per utilizzare questi passaggi in un flusso di lavoro.

## Assegna passaggio attività {#assign-task-step}

Il passaggio dell&#39;attività di assegnazione crea un&#39;attività e la assegna a un utente o gruppo. Oltre ad assegnare l’attività, il componente specifica anche il modulo adattivo o il PDF non interattivo per l’attività. Il modulo adattivo è richiesto per accettare l&#39;input degli utenti e i PDF non interattivi oppure un modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di sola revisione.

È inoltre possibile utilizzare il componente per controllare il comportamento dell&#39;attività. Ad esempio, creazione di un documento di record automatico, assegnazione dell&#39;attività a un utente o gruppo specifico, specifica il percorso dei dati inviati, specifica il percorso dei dati da precompilare e specifica delle azioni predefinite. Il passaggio Assegna attività ha le seguenti proprietà:

* **Titolo:** Titolo dell’attività. Il titolo viene visualizzato in AEM Posta in arrivo.
* **Descrizione:** Spiegazione delle operazioni eseguite nell&#39;attività. Queste informazioni sono utili per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **Percorso miniatura:** percorso della miniatura dell’attività. Se non viene specificato alcun percorso, per la miniatura predefinita di un modulo adattivo e per il documento di registrazione viene visualizzata un&#39;icona predefinita.
* **Fase flusso di lavoro:** Un flusso di lavoro può avere più fasi. Questi passaggi vengono visualizzati nella AEM Posta in arrivo. È possibile definire questi passaggi nelle proprietà del modello (barra laterale > Pagina > Proprietà pagina > Stadi).
* **Priorità: la priorità** selezionata viene visualizzata nella casella in entrata AEM. Le opzioni disponibili sono Alta, Media e Bassa. Il valore predefinito è Medium.
* **Data scadenza:** specificare il numero di giorni o ore dopo i quali l&#39;attività è contrassegnata come scaduta. Se si seleziona **Off**, l&#39;attività non viene mai contrassegnata come scaduta. È inoltre possibile specificare un gestore di timeout per eseguire attività specifiche dopo la scadenza dell&#39;attività.

* **Giorni:** il numero di giorni prima dei quali deve essere completata l&#39;attività. Numero di giorni contati dopo che l’attività è stata assegnata a un utente. Se un&#39;attività non è completa e supera il numero di giorni specificato nel campo Giorni, se selezionata, viene attivato un gestore di timeout dopo la data di scadenza.
* **Ore:** il numero di ore prima delle quali l&#39;attività deve essere completata. Numero di ore contate dopo che l’attività è stata assegnata a un utente. Se un&#39;attività non è completa e supera il numero di ore specificato nel campo Ore, se selezionata, viene attivato un gestore di timeout dopo le ore di scadenza.
* **Timeout dopo la data di scadenza:** selezionate questa opzione per abilitare il campo di selezione Gestore timeout.
* **Gestore di timeout:** selezionare lo script da eseguire quando il passaggio dell&#39;attività di assegnazione supera la data di scadenza. Gli script inseriti nell&#39;archivio CRX in [apps]/fd/dashboard/scripts/timeoutHandler sono disponibili per la selezione. Il percorso specificato non esiste nell&#39;archivio crx. Un amministratore crea il percorso prima di utilizzarlo.
* **Evidenziare l&#39;azione e il commento dall&#39;ultima attività in Dettagli attività:** selezionare questa opzione per visualizzare l&#39;ultima azione eseguita e il commento ricevuto sulla sezione dei dettagli dell&#39;attività di un&#39;attività.
* **Tipo:** scegliete il tipo di documento da compilare all’avvio del flusso di lavoro. È possibile scegliere un modulo adattivo, un modulo adattivo di sola lettura, un documento PDF non interattivo, l&#39;interfaccia utente dell&#39;agente di comunicazione interattiva o un documento canale Web di comunicazione interattiva.
* **Usa modulo adattivo:** specifica il metodo per individuare il modulo adattivo di input. Questa opzione è disponibile se si seleziona Modulo adattivo o Modulo adattivo di sola lettura dall&#39;elenco a discesa Tipo. È possibile utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto, oppure disponibile nel percorso di una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso.\
   È possibile associare più moduli adattivi a un flusso di lavoro. Di conseguenza, è possibile specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

* **Usa comunicazione interattiva:** specifica il metodo per individuare la comunicazione interattiva di input. È possibile utilizzare la comunicazione interattiva inviata al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso. Questa opzione è disponibile se si seleziona Interattivo comunicazione agente interfaccia utente o Documento canale Web comunicazione interattiva dall&#39;elenco a discesa Tipo.

>[!NOTE]
>
>Per accedere all&#39;interfaccia utente di Interactive Communications Agent nella casella in AEM in entrata è necessario disporre di assegnazioni di gruppi di agenti e utenti del flusso di lavoro.

* **Modulo adattivo o percorso** di comunicazione interattiva: Specificate il percorso del modulo adattivo o della comunicazione interattiva. È possibile utilizzare il modulo adattivo o la comunicazione interattiva inviata al flusso di lavoro, disponibile in un percorso assoluto, oppure recuperare il modulo adattivo da un percorso memorizzato in una variabile di tipo dati stringa.
* **Selezionare l&#39;input PDF utilizzando:** specificare il percorso di un documento PDF non interattivo. Il campo è disponibile quando si sceglie un documento PDF non interattivo nel campo Tipo. È possibile selezionare il PDF di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio, [Payload_Directory]/Workflow/PDF/credit-card.pdf. Il percorso non esiste nell&#39;archivio crx. Un amministratore crea il percorso prima di utilizzarlo. Per utilizzare l&#39;opzione Percorso PDF è necessario abilitare l&#39;opzione Documento di registrazione o utilizzare moduli adattivi basati su modelli di modulo.
* **Per l&#39;attività completata, eseguite il rendering del modulo adattivo come** segue: Quando un&#39;attività è contrassegnata come completa, è possibile eseguire il rendering del modulo adattivo come modulo adattivo di sola lettura o come documento PDF. Per eseguire il rendering del modulo adattivo come documento di registrazione, è necessario abilitare l&#39;opzione Documento di registrazione o i moduli adattivi basati su modelli di modulo.
* **Precompilati:** I seguenti campi elencati di seguito fungono da input per l&#39;attività:

   * **Selezionare il file di dati di input utilizzando:** Percorso del file di dati di input (.json,. xml, .doc o modello dati modulo). È possibile recuperare il file di dati di input utilizzando un percorso relativo al payload o recuperare il file memorizzato in una variabile del tipo di dati Document, XML o JSON. Ad esempio, il file contiene i dati inviati per il modulo tramite un&#39;applicazione Casella in entrata AEM. Un percorso di esempio è [Payload_Directory]/workflow/data.
   * **Selezionare gli allegati di input utilizzando:** gli allegati disponibili nella posizione sono allegati al modulo associato all&#39;attività. Il percorso è sempre relativo al payload. Un percorso di esempio è [Payload_Directory]/attachments/
   * **Scegli JSON di input:** seleziona un file JSON di input utilizzando un percorso relativo al payload o memorizzato in una variabile del tipo di dati Document, JSON o Form Data Model. Questa opzione è disponibile se si seleziona Interattivo comunicazione agente interfaccia utente o Documento canale Web comunicazione interattiva dall&#39;elenco a discesa Tipo.
   * **Scegliete un servizio di precompilazione personalizzato:** selezionate il servizio di precompilazione per recuperare i dati e precompilare il documento del canale Web di comunicazione interattiva o l&#39;interfaccia utente dell&#39;agente.

   * **Utilizzate il servizio di precompilazione della comunicazione interattiva selezionata sopra:** Utilizzate questa opzione per utilizzare il servizio di precompilazione della comunicazione interattiva definita nell&#39;elenco a discesa Usa comunicazione interattiva.
   * **Mapping attributi richiesta:** utilizzate la sezione Mappatura attributi richiesta per definire il  [nome e il valore dell&#39;attributo](../../forms/using/work-with-form-data-model.md#bindargument) richiesta. Recuperare i dettagli dall&#39;origine dati in base al nome e al valore dell&#39;attributo specificati nella richiesta. È possibile definire un valore attributo di richiesta utilizzando un valore letterale o una variabile del tipo di dati String.\
      Le opzioni di mappatura del servizio di precompilazione e degli attributi di richiesta sono disponibili solo se si seleziona Interattivo comunicazione agente interfaccia utente o Documento canale Web comunicazione interattiva dall&#39;elenco a discesa Tipo.

* **Informazioni inviate:** I seguenti campi elencati di seguito fungono da posizioni di output per l’attività:

   * **Salva il file di dati di output utilizzando:** Salva il file di dati (.json,. xml, .doc o modello dati modulo). Il file di dati contiene informazioni inviate tramite il modulo associato. È possibile salvare il file di dati di output utilizzando un percorso relativo al payload o memorizzarlo in una variabile del tipo di dati Document, XML o JSON. Ad esempio, [Payload_Directory]/Workflow/data, dove i dati sono un file.
   * **Salvare gli allegati utilizzando:** Salvare gli allegati del modulo forniti in un&#39;attività. È possibile salvare gli allegati utilizzando un percorso relativo al payload o memorizzarlo in una variabile di array di tipi di dati Document.
   * **Salva documento di record utilizzando:** Percorso per salvare un file del documento di registrazione. Ad esempio, [Payload_Directory]/DocumentofRecord/credit-card.pdf. È possibile salvare il documento di record utilizzando un percorso relativo al payload o memorizzarlo in una variabile del tipo di dati Documento. Se si seleziona l&#39;opzione **Relative a Payload**, il documento di registrazione non viene generato se il campo del percorso viene lasciato vuoto. Questa opzione è disponibile solo se si seleziona Modulo adattivo dall&#39;elenco a discesa Tipo.

   * **Salva i dati del canale Web utilizzando:** Salva il file di dati del canale Web utilizzando un percorso relativo al payload o archivialo in una variabile del tipo di dati Documento, JSON o Modello dati modulo. Questa opzione è disponibile solo se si seleziona Interattivo agente di comunicazione dall&#39;elenco a discesa Tipo.
   * **Salvare il documento PDF utilizzando:** Salvare il documento PDF utilizzando un percorso relativo al payload o memorizzarlo in una variabile del tipo di dati Documento. Questa opzione è disponibile solo se si seleziona Interattivo agente di comunicazione dall&#39;elenco a discesa Tipo.
   * **Salvate il modello di layout utilizzando:** salvate il modello di layout utilizzando un percorso relativo al payload o archiviatelo in una variabile del tipo di dati Documento. Il [modello di layout](../../forms/using/layout-design-details.md) fa riferimento a un file XDP creato con Forms Designer. Questa opzione è disponibile solo se si seleziona Interattivo agente di comunicazione dall&#39;elenco a discesa Tipo.

* **Assegnatario > Opzioni di assegnazione:** specificare il metodo per assegnare l’attività a un utente. Potete assegnare dinamicamente l’attività a un utente o a un gruppo utilizzando lo script Selezione partecipanti o assegnando l’attività a un utente o gruppo AEM specifico.
* **Selettore partecipanti:** l&#39;opzione è disponibile quando l&#39;opzione  **Dynamically to a user or** groupoption (Destinazione dinamica a un utente o gruppo) è selezionata nel campo Assign options (Opzioni assegnabili). È possibile utilizzare uno script ECMAS o un servizio per selezionare in modo dinamico un utente o un gruppo. Per ulteriori informazioni, vedere [Assegnare dinamicamente un flusso di lavoro agli utenti](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Creazione di un passaggio personalizzato per i partecipanti dinamici di Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/dynamic-steps.html)

* **Partecipanti:** Il campo è disponibile quando l&#39;opzione  **[!UICONTROL com.adobe.granite.workflow.core.process.]** RandomParticipantChooseroption è selezionata nel campo  **Partecipanti** selezionati. Il campo consente di selezionare utenti o gruppi per l&#39;opzione RandomParticipantChooser.

* **Assegnatario:** Il campo è disponibile quando  **[!UICONTROL com.adobe.fd.workspace.step.service.]** VariableParticipantChooseris è selezionato nel campo  **Selezione** partecipanti. Il campo consente di selezionare una variabile del tipo di dati String per definire l&#39;assegnatario.

* **Argomenti:** Il campo è disponibile quando nel campo Selezione partecipanti è selezionato uno script diverso da RandomParticipantChoose. Il campo consente di fornire un elenco di argomenti separati da virgola per lo script selezionato nel campo Selezione partecipanti.

* **Utente o gruppo:** l&#39;attività è assegnata all&#39;utente o al gruppo selezionato. L&#39;opzione è disponibile quando l&#39;opzione **Per un utente o un gruppo specifico** è selezionata nel campo **Assegna opzioni**. Il campo elenca tutti gli utenti e i gruppi del gruppo Workflow-utenti.\
   Il menu a discesa **Utente o Gruppo** elenca gli utenti e i gruppi a cui l&#39;utente ha accesso. La visualizzazione del nome utente dipende dal fatto che si disponga delle autorizzazioni di accesso sul nodo **users** nell&#39;archivio crx di quel particolare utente.

* **Notifica all&#39;assegnatario tramite e-mail:** selezionate questa opzione per inviare le notifiche e-mail all&#39;assegnatario. Queste notifiche vengono inviate quando un&#39;attività viene assegnata a un utente. Prima di utilizzare l&#39;opzione, abilita le notifiche dalla console AEM Web. Per istruzioni dettagliate, vedere [configurare le notifiche e-mail per l&#39;assegnazione delle attività](../../forms/using/aem-forms-workflow.md)

* **Modello** e-mail HTML: Selezionate il modello e-mail per il messaggio e-mail di notifica. Per modificare un modello, modificate il file che si trova in /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt in crx-repository.
* **Consenti delega a:** AEM Posta in arrivo fornisce all&#39;utente che ha effettuato l&#39;accesso un&#39;opzione per delegare il flusso di lavoro assegnato a un altro utente. Potete delegare lo stesso gruppo o l’utente del flusso di lavoro di un altro gruppo. Se l&#39;attività è assegnata a un singolo utente e l&#39;opzione **consenti delega ai membri del gruppo assegnatario** è selezionata, non è possibile delegare l&#39;attività a un altro utente o gruppo.
* **Impostazioni condivisione:** AEM Posta in arrivo offre opzioni per condividere con altri utenti una o tutte le attività della inbox:
   * Quando è selezionata l&#39;opzione **Consenti all&#39;assegnatario di condividere in modo esplicito in inbox**, l&#39;utente può fare clic sull&#39;attività e condividerla con un altro utente AEM.
   * Quando è selezionata l&#39;opzione **Consenti al cessionario di condividere tramite la condivisione in inbox** e un utente condivide i propri elementi in entrata o consente ad altri utenti di accedere ai propri elementi in entrata, solo le attività con l&#39;opzione sopra riportata vengono condivise con altri utenti.

* **Azioni > Azioni predefinite:** sono disponibili azioni Invia, Salva e Ripristina. Per impostazione predefinita sono attivate tutte le azioni predefinite.
* **Variabile route:** nome della variabile route. La variabile route acquisisce le azioni personalizzate selezionate da un utente AEM Posta in arrivo.
* **Cicli:** Un&#39;attività può essere indirizzata a percorsi diversi. Se selezionato in AEM Posta in arrivo, la route restituisce un valore e i rami del flusso di lavoro in base alla route selezionata. È possibile memorizzare i percorsi in una variabile di array di tipo dati String oppure selezionare **Letterale** per aggiungere manualmente i percorsi.

* **Titolo**: Specificare il titolo della route. Viene visualizzato in AEM Posta in arrivo.
* **Icona** Corallo: Specificate l&#39;attributo HTML di un&#39;icona corallo.  libreria CorelUI Adobe offre un vasto set di icone per i primi tocco. È possibile scegliere e utilizzare un&#39;icona per la route. Viene visualizzato insieme al titolo in AEM Posta in arrivo. Se si memorizzano le route in una variabile, le route utilizzano l&#39;icona corale &#39;Tags&#39; predefinita.
* **Consenti all&#39;assegnatario di aggiungere un commento**: Selezionare questa opzione per abilitare i commenti per l&#39;attività. Un assegnatario può aggiungere i commenti dall&#39;interno AEM Posta in arrivo al momento dell&#39;invio dell&#39;attività.
* **Salva commento in variabile:** salva il commento in una variabile del tipo di dati String. Questa opzione viene visualizzata solo se si seleziona la casella di controllo **Consenti all&#39;assegnatario di aggiungere commenti**.

* **Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività**: Selezionare questa opzione per abilitare gli allegati per l&#39;attività. Un assegnatario può aggiungere gli allegati dall&#39;interno AEM Posta in arrivo al momento dell&#39;invio dell&#39;attività.
* **Salva gli allegati delle attività di output utilizzando**: Specificate il percorso della cartella dell&#39;allegato. È possibile salvare gli allegati delle attività di output utilizzando un percorso relativo al payload o in una variabile di array di tipi di dati del documento. Questa opzione viene visualizzata solo se si seleziona la casella di controllo **Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività** e si seleziona **Modulo adattivo**, **Modulo adattivo di sola lettura** o **Documento PDF non interattivo** dall&#39;elenco a discesa **Tipo** Scheda **Modulo/Documento**.

>[!NOTE]
>
>Utilizzare la scheda Allegati nell&#39;interfaccia utente dell&#39;agente durante il runtime per associare gli allegati a una comunicazione interattiva. Gli allegati associati vengono visualizzati come allegati attività nella barra laterale dopo l’apertura dell’elemento di lavoro in stato Completato.

* **Usa metadati personalizzati:** selezionate questa opzione per abilitare il campo di metadati personalizzato. I metadati personalizzati vengono utilizzati nei modelli e-mail.
* **Metadati personalizzati:** selezionate i metadati personalizzati per i modelli e-mail. I metadati personalizzati sono disponibili nell&#39;archivio crx in apps/fd/dashboard/scripts/metadataScripts. Il percorso specificato non esiste nell&#39;archivio crx. Un amministratore crea il percorso prima di utilizzarlo. Potete anche utilizzare un servizio per i metadati personalizzati. È inoltre possibile estendere l&#39;interfaccia WorkitemUserMetadataService per fornire metadati personalizzati.
* **Mostra dati dai passaggi** precedenti: Selezionare questa opzione per consentire agli assegnatari di visualizzare gli assegnatari precedenti, le azioni già eseguite sull&#39;attività, i commenti aggiunti all&#39;attività e il documento di registrazione dell&#39;attività completata, se disponibile.
* **Mostra dati dai passaggi successivi:** selezionare questa opzione per consentire all&#39;assegnatario corrente di visualizzare l&#39;azione eseguita e i commenti aggiunti all&#39;attività dagli assegnatari successivi. Consente inoltre all&#39;assegnatario corrente di visualizzare un documento di registrazione dell&#39;attività completata, se disponibile.
* **Visibilità del tipo di dati:** per impostazione predefinita, un assegnatario può visualizzare un documento di registrazione, assegnatari, azioni eseguite e commenti aggiunti da assegnatari precedenti e successivi. Utilizzare l&#39;opzione di visibilità del tipo di dati per limitare il tipo di dati visibili agli assegnatari.

## Invia passaggio e-mail {#send-email-step}

Utilizzare il passaggio e-mail per inviare un messaggio e-mail, ad esempio un messaggio e-mail contenente un documento record, un collegamento a un modulo adattivo, un collegamento a una comunicazione interattiva o un documento PDF allegato. Invia e-mail supporta [HTML email](https://en.wikipedia.org/wiki/HTML_email). Le e-mail HTML sono reattive e si adattano al client e-mail e alle dimensioni dello schermo dei destinatari. Potete utilizzare un modello e-mail HTML per definire l’aspetto, lo schema colore e il comportamento del messaggio e-mail.

Il passaggio e-mail utilizza Day CQ Mail Service per inviare e-mail. Prima di utilizzare il passaggio e-mail, assicurarsi che il [servizio e-mail](../../forms/using/aem-forms-workflow.md) sia configurato. Il passaggio e-mail ha le seguenti proprietà:

**Titolo:** Il titolo del passaggio consente di identificare il passaggio nell’editor del flusso di lavoro.

**Descrizione:** Spiegazione è utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

**Oggetto e-mail:** l’oggetto può essere recuperato dai metadati di un flusso di lavoro, specificato manualmente o recuperato dal valore memorizzato in una variabile. Selezionate una delle seguenti opzioni:

* **Letterale: specificare** manualmente un oggetto.
* **Recuperare dai metadati**  del flusso di lavoro - Recuperare l’oggetto da una proprietà di metadati.
* **Variabile** : recupera l&#39;oggetto dal valore memorizzato in una variabile del tipo di dati stringa.

**Modello** e-mail HTML: Modello HTML per l’e-mail. Potete specificare le variabili in un modello e-mail. Il Passaggio e-mail estrae e visualizza per gli input tutte le variabili incluse in un modello.

**Metadati modello e-mail:** il valore delle variabili del modello e-mail può essere un valore specificato dall’utente, il percorso di una risorsa sull’autore o sul server di pubblicazione, l’immagine o la proprietà dei metadati di un flusso di lavoro.

* **Letterale:** utilizzare l&#39;opzione quando si conosce il valore esatto da specificare. Ad esempio, [example@example.com](mailto:example@example.com).

* **Metadati flusso di lavoro:** utilizzate questa opzione quando il valore da utilizzare viene salvato in una proprietà di metadati del flusso di lavoro. Dopo aver selezionato l’opzione, immettete il nome della proprietà dei metadati nella casella di testo vuota sotto l’opzione Metadati flusso di lavoro. Ad esempio, emailAddress.
* **URL risorsa:** utilizzate l’opzione per incorporare un collegamento Web di una comunicazione interattiva all’e-mail. Dopo aver selezionato l&#39;opzione, individuate e scegliete la comunicazione interattiva da incorporare. La risorsa può risiedere sull’autore o sul server di pubblicazione.
* **Immagine:** utilizzate l&#39;opzione per incorporare un&#39;immagine nell&#39;e-mail. Dopo aver selezionato l’opzione, sfogliate e scegliete l’immagine. L&#39;opzione immagine è disponibile solo per i tag immagine (&lt;img src=&quot;*&quot;/>) disponibili nel modello e-mail.

**Indirizzo e-mail del mittente/destinatario:** selezionare l&#39;opzione  **** Lettera per specificare manualmente un indirizzo e-mail oppure selezionare l&#39;opzione  **Recupera dai** metadati del flusso di lavoro per recuperare l&#39;indirizzo e-mail da una proprietà di metadati. Potete anche specificare un elenco di array di proprietà di metadati per l&#39;opzione **Recupera dai metadati del flusso di lavoro**. Selezionare l&#39;opzione **Variabile** per recuperare l&#39;indirizzo e-mail dal valore memorizzato in una variabile del tipo di dati stringa.

**Allegato file:** la risorsa disponibile nel percorso specificato viene associata all’e-mail. Il percorso della risorsa può essere relativo al payload o al percorso assoluto. Un percorso di esempio è [Payload_Directory]/attachments/.

Selezionare l&#39;opzione **Variabile** per recuperare l&#39;allegato del file memorizzato in una variabile del tipo di dati Document, XML o JSON.

**Nome file:** nome del file allegato e-mail. Il Passaggio e-mail modifica il nome file originale dell&#39;allegato in base al nome file specificato. Il nome può essere specificato manualmente o recuperato da una proprietà di metadati di un flusso di lavoro o da una variabile. Utilizzare l&#39;opzione **Letterale** quando si conosce il valore esatto da specificare. Utilizzare l&#39;opzione **Variabile** per recuperare il nome del file dal valore memorizzato in una variabile del tipo di dati stringa. Utilizzate l&#39;opzione **Recupera da un metadati del flusso di lavoro** quando il valore da utilizzare viene salvato in una proprietà di metadati del flusso di lavoro.

## Passaggio Genera documento record {#generate-document-of-record-step}

Quando un modulo viene compilato o inviato, è possibile tenere un record del modulo, in formato cartaceo o in formato documento. Questo viene definito documento di registrazione (DoR). È possibile utilizzare il passaggio Genera documento di record per creare una versione PDF in sola lettura o interattiva di un modulo adattivo. La versione PDF contiene informazioni inserite nel modulo insieme al layout del modulo adattivo.

Il passaggio Documento di registrazione ha le proprietà seguenti:

**Usa modulo** adattivo: Specificare il metodo per individuare il modulo adattivo di input. È possibile utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto, oppure disponibile nel percorso di una variabile. È possibile utilizzare una variabile del tipo di dati String per specificare il percorso nel campo **Seleziona variabile da risolvere**.\
È possibile associare più moduli adattivi a un flusso di lavoro. Di conseguenza, è possibile specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

**Percorso** modulo adattivo: Specificare il percorso del modulo adattivo. Il campo è disponibile quando si seleziona l&#39;opzione **Disponibile in un percorso assoluto** nel campo **Usa modulo adattivo**.

**Selezionare Input data using:** Percorso dei dati di input per il modulo adattivo. È possibile mantenere i dati in una posizione relativa al payload, specificare un percorso assoluto dei dati o recuperare i dati memorizzati in una variabile di tipo Document, JSON o XML. I dati di input vengono uniti al modulo adattivo per creare un documento di record.

**Selezionare Percorso allegato di input utilizzando:** Percorso degli allegati. Questi allegati sono inclusi nel documento di registrazione. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di array di tipo dati Document.

Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella vengono allegati al documento di registrazione. Se qualsiasi file è disponibile nelle cartelle direttamente disponibili nel percorso allegato specificato, i file sono inclusi nel documento di registrazione come allegati. Se sono presenti cartelle in cartelle direttamente disponibili, queste vengono ignorate.

**Salva documento di registrazione generato utilizzando le opzioni riportate di seguito:** specificare la posizione in cui conservare un documento di record. È possibile scegliere di sovrascrivere la cartella payload, inserire il documento di record in una posizione all&#39;interno della directory di payload o memorizzare il documento di record in una variabile del tipo di dati Documento.

**Impostazioni internazionali**: Specificare la lingua del documento di record. Selezionare **Letterale** per selezionare le impostazioni internazionali da un elenco a discesa oppure selezionare **Variabile** per recuperare le impostazioni internazionali dal valore memorizzato in una variabile del tipo di dati stringa. È necessario definire il codice delle impostazioni internazionali durante la memorizzazione del valore delle impostazioni internazionali in una variabile. Ad esempio, specificare **en_US** per l&#39;inglese e **fr_FR** per il francese.

## Richiama il passaggio del servizio del modello dati modulo {#invoke-form-data-model-service-step}

È possibile utilizzare [ AEM Forms Data Integration](../../forms/using/data-integration.md) per configurare e connettersi a origini dati diverse. Queste origini dati possono essere un database, un servizio Web, un servizio REST, un servizio OData e una soluzione CRM.  AEM Forms Data Integration consente di creare un modello dati modulo che include vari servizi per eseguire operazioni di recupero, aggiunta e aggiornamento dei dati nel database configurato. È possibile utilizzare il passaggio **Richiama servizio modello dati** per selezionare un modello dati del modulo (FDM) e utilizzare i servizi di FDM per recuperare, aggiornare o aggiungere dati a origini dati diverse.

Per spiegare gli input per i campi del passaggio, la seguente tabella di database e il file JSON sono utilizzati come esempio:

**Esempio di tabella CustomerDetails**

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

**Esempio di file JSON**

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

Il passaggio Richiama servizio modello dati modulo include i campi elencati di seguito per facilitare le operazioni del modello dati del modulo:

* **Titolo:** Titolo del passaggio. Consente di identificare il passaggio nell’editor del flusso di lavoro.
* **Descrizione:** Spiegazione utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **Percorso** modello dati modulo: Individuare e selezionare un modello dati modulo presente sul server.

* **Servizio**: Elenco dei servizi forniti dal modello dati modulo selezionato.
* **Input per services > Fornisci dati di input utilizzando metadati letterali, variabili o flussi di lavoro e un file** JSON: Un servizio può avere più argomenti. Selezionate l&#39;opzione per ottenere il valore degli argomenti del servizio da una proprietà di metadati di un flusso di lavoro, un oggetto JSON, una variabile o immettete direttamente il valore nella casella di testo fornita:

   * **Letterale:** utilizzare l&#39;opzione quando si conosce il valore esatto da specificare. Ad esempio, srose@we.info.
   * **Variabile:** utilizzare l&#39;opzione per recuperare il valore memorizzato in una variabile.
   * **Recupera da metadati flusso di lavoro:** utilizzate l&#39;opzione quando il valore da utilizzare viene salvato in una proprietà di metadati del flusso di lavoro. Ad esempio, emailAddress.
   * **Notazione punto JSON:** utilizzate l&#39;opzione quando il valore da utilizzare si trova in un file JSON. Ad esempio, Insurance.customerDetails.emailAddress. L&#39;opzione Notazione punto JSON è disponibile solo se è selezionata l&#39;opzione Mappa campi di input dall&#39;opzione JSON di input.
   * **Mappare i campi di input dal JSON di input:** specificate il percorso di un file JSON per ottenere il valore di input di alcuni argomenti del servizio dal file JSON. Il percorso del file JSON può essere relativo al payload, a un percorso assoluto, oppure potete selezionare un documento JSON di input utilizzando una variabile di tipo JSON o Form Data Model.

* **Input per services > Fornisce i dati di input utilizzando una variabile o un file JSON:** Selezionare l&#39;opzione per ottenere i valori per tutti gli argomenti da un file JSON salvato in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **Selezionate il documento JSON di input utilizzando**: Il file JSON contiene i valori per tutti gli argomenti del servizio. Il percorso del file JSON può essere **relativo al payload** o un percorso assoluto **.** È inoltre possibile recuperare il documento JSON di input utilizzando una variabile del tipo di dati JSON o del modello dati modulo.

* **Notazione punto JSON:** lasciate vuoto il campo per utilizzare tutti gli oggetti del file JSON specificato come input per gli argomenti del servizio. Per leggere un oggetto JSON specifico dal file JSON specificato come input per gli argomenti del servizio, specificate la notazione del punto per l&#39;oggetto JSON, ad esempio, se disponete di un JSON simile a quello elencato all&#39;inizio della sezione, specificate Insurance.customerDetails per fornire tutti i dettagli di un cliente come input al servizio.
* **Output di service > Mappa e scrittura dei valori di output su variabili o metadati:** Selezionare l&#39;opzione per salvare i valori di output come proprietà del nodo di metadati dell&#39;istanza del flusso di lavoro in crx-repository. Specificate il nome della proprietà dei metadati e selezionate l&#39;attributo di output del servizio corrispondente da mappare con la proprietà dei metadati, ad esempio, mappate il numero_telefono restituito dal servizio di output con la proprietà phone_number dei metadati del flusso di lavoro. Analogamente, è possibile memorizzare l&#39;output in una variabile di tipo dati Long. Quando si seleziona una proprietà per l&#39;opzione **[!UICONTROL Service output attribute to mapping]**, solo le variabili in grado di memorizzare i dati della proprietà selezionata vengono popolate per l&#39;opzione **[!UICONTROL Salva l&#39;output in]**.

* **Output di service > Salva output in una variabile o un file JSON:** selezionare l&#39;opzione per salvare i valori di output in un file JSON in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **Salva il documento Output JSON utilizzando le seguenti opzioni:** Salva il file JSON di output. Il percorso del file JSON di output può essere relativo al payload o a un percorso assoluto. È inoltre possibile salvare il file JSON di output utilizzando una variabile del tipo di dati JSON o del modello dati modulo.

## Sign Document step {#sign-document-step}

Il passaggio Firma documento consente di utilizzare  Adobe Sign per firmare i documenti. Il passaggio Firma documento presenta le proprietà seguenti:

* **Nome accordo:** specifica il titolo del contratto. Il nome del contratto fa parte dell’oggetto e del corpo del messaggio e-mail inviato ai firmatari. È possibile memorizzare il nome in una variabile del tipo di dati String oppure selezionare **Letterale** per aggiungere il nome manualmente.

* **Lingua:** specifica la lingua per le opzioni di e-mail e verifica. È possibile memorizzare le impostazioni internazionali in una variabile del tipo di dati String oppure selezionare **Letterale** per scegliere le impostazioni internazionali dall&#39;elenco delle opzioni disponibili. È necessario definire il codice delle impostazioni internazionali durante la memorizzazione del valore delle impostazioni internazionali in una variabile. Ad esempio, specificare **en_US** per l&#39;inglese e **fr_FR** per il francese.

* **Configurazione** Adobe Sign Cloud : Scegliete una configurazione  Adobe Sign Cloud. Se non avete configurato  Adobe Sign per  AEM Forms, consultate [Integrare  Adobe Sign con  AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

* **Selezionare Documento da firmare:** È possibile scegliere un documento da una posizione relativa al payload, utilizzare payload come documento, specificare un percorso assoluto del documento o recuperare il documento memorizzato in una variabile del tipo di dati Documento.
* **Giorni fino alla scadenza:** Un documento è contrassegnato come scadenza (scadenza trascorsa) dopo l&#39;assenza di attività sull&#39;attività per il numero di giorni specificato nel campo  **Giorni fino alla** scadenza. Il numero di giorni contati dopo che il documento è stato assegnato a un utente per la firma.
* **Frequenza e-mail promemoria:** puoi inviare un promemoria a intervalli giornalieri o settimanali. La settimana viene conteggiata a partire dal giorno in cui il documento viene assegnato a un utente per la firma.
* **Procedura di firma:** è possibile scegliere di firmare un documento in ordine sequenziale o parallelo. In ordine sequenziale, un firmatario riceve il documento alla volta per la firma. Dopo che il primo firmatario ha completato la firma del documento, quest&#39;ultimo viene inviato al secondo firmatario e così via. In ordine parallelo, più firmatari possono firmare un documento alla volta.
* **URL di reindirizzamento:** specificate un URL di reindirizzamento. Dopo aver firmato il documento, è possibile reindirizzare l&#39;assegnatario a un URL. In genere, questo URL contiene un messaggio di ringraziamento o ulteriori istruzioni.
* **Fase flusso di lavoro:** Un flusso di lavoro può avere più fasi. Questi passaggi vengono visualizzati nella AEM Posta in arrivo. È possibile definire questi passaggi nelle proprietà del modello (barra laterale > Pagina > Proprietà pagina > Stadi).
* **Seleziona Firmatari:** specifica il metodo per scegliere i firmatari per il documento. Puoi assegnare il flusso di lavoro in modo dinamico a un utente o a un gruppo oppure puoi aggiungere manualmente i dettagli di un firmatario.
* **Script o servizio per selezionare i firmatari:** L&#39;opzione è disponibile solo se l&#39;opzione Dinamicamente è selezionata nel campo Seleziona firmatari. È possibile specificare uno script ECMAS o un servizio per scegliere i firmatari e le opzioni di verifica per un documento.
* **Dettagli firmatario:** l’opzione è disponibile solo se l’opzione Manualmente è selezionata nel campo Seleziona firmatari. Specificate l&#39;indirizzo e-mail e scegliete un meccanismo di verifica opzionale. Prima di selezionare un meccanismo di verifica in due fasi, accertatevi che l&#39;opzione di verifica corrispondente sia abilitata per l&#39;account Adobe Sign  configurato. È possibile utilizzare una variabile del tipo di dati String per definire i valori dei campi **[!UICONTROL Email]**, **[!UICONTROL Country Code]** e **[!UICONTROL Phone Number]**. I campi **[!UICONTROL Codice paese]** e **[!UICONTROL Numero di telefono]** vengono visualizzati solo se si seleziona **[!UICONTROL Verifica telefono]** dall&#39;elenco a discesa **[!UICONTROL Verifica in 2 fasi]**.
* **Variabile di stato:** un documento abilitato per  Adobe Sign memorizza lo stato di firma del documento in una variabile del tipo di dati String. Specificare il nome della variabile di stato (adobeSignStatus). Una variabile di stato di un&#39;istanza è disponibile in CRXDE in /etc/workflow/instance/&lt;server>/&lt;data-ora>/&lt;istanza del modello di flusso di lavoro>/workItems/&lt;nodo>/metaData contiene lo stato di una variabile.
* **Salvare il documento firmato utilizzando le opzioni riportate di seguito:** specificare il percorso in cui conservare i documenti firmati. È possibile scegliere di sovrascrivere il file di payload, posizionare il documento firmato in una posizione all&#39;interno della directory di payload o archiviare il documento firmato in una variabile di tipo Document.

## Passaggi di Document Services {#document-services-steps}

AEM Document Services è un insieme di servizi per la creazione, l&#39;assemblaggio e la protezione di documenti PDF.  AEM Forms fornisce un passaggio AEM Workflow separato per ogni servizio documenti.

Come per altri passaggi  flusso di lavoro AEM Forms, quali Assegna attività, Invia e-mail e Firma documento, è possibile utilizzare le variabili in tutti AEM passaggi di Document Services. Per ulteriori informazioni sulla creazione e gestione di variabili, vedere [Variabili nei flussi di lavoro AEM](../../forms/using/variable-in-aem-workflows.md).

### Applica timestamp documento passaggio {#apply-document-time-stamp-step}

Aggiunta di marca temporale a un documento. Vengono forniti i dettagli del documento, ad esempio il percorso del documento di input, il nome del documento di input, la posizione in cui memorizzare i dati esportati. Potete scegliere di sovrascrivere il file di payload esistente, scegliere un nome file diverso per memorizzare i dati in un file diverso in una cartella payload, fornire un percorso assoluto ai dati o archiviare i dati in una variabile del tipo di dati Documento.

### Converti in passaggio immagine {#convert-to-image-step}

Converte un documento PDF in un elenco di immagini. I formati immagine supportati sono JPEG, JPEG2000, PNG e TIFF. Le seguenti informazioni si applicano alle conversioni a immagini TIFF:

* Viene generato un file TIFF con più pagine.
* Alcune annotazioni non sono incluse nelle immagini TIFF. Le annotazioni che richiedono  Acrobat per generare il relativo aspetto non sono incluse.

### Converti in PDF/A passaggio {#convert-to-pdf-a-step}

Converte un documento PDF in formato PDF/A utilizzando le opzioni disponibili. La versione PDF/A del formato PDF (Portable Document Format) è specializzata nell&#39;archiviazione e nella conservazione a lungo termine dei documenti.

### Converti in fase PS {#convert-to-ps-step}

Convertire i documenti PDF in PostScript. Durante la conversione in PostScript, è possibile utilizzare l&#39;operazione di conversione per specificare il documento di origine e se convertire in PostScript livello 2 o 3. Il documento PDF convertito in file PostScript deve essere non interattivo.

### Crea PDF dal passaggio del tipo specificato {#create-pdf-from-specified-type-step}

Generare un documento PDF da un file di input. Il documento di input può essere relativo al payload, avere un percorso assoluto, può essere payload stesso o memorizzato in una variabile del tipo di dati Documento.

### Crea PDF da URL/HTML/passaggio ZIP {#create-pdf-from-url-html-zip-step}

Genera un documento PDF a partire da URL, HTML e file ZIP forniti.

### Passaggio dati di esportazione {#export-data-step}

Esporta i dati da un file PDF forms o XDP. È necessario immettere il percorso del file Documento di input e Formato dati di esportazione. Le opzioni di Esporta formato dati sono Auto, XDP e XmlData.

###  Export PDF al passaggio di tipo specificato {#export-pdf-to-specified-type-step}

Converte un documento PDF in un formato selezionato.

### Genera passaggio PDF non interattivo {#generatenoninteractive}

Generare un PDF non interattivo. Offre diverse opzioni di personalizzazione.

>[!NOTE]
>
>Potete utilizzare le variabili per specificare il file modello per i documenti di input. Memorizzare il percorso del file modello in una variabile di tipo dati String.

### Passaggio dati di importazione {#import-data-step}

Unisce i dati del modulo in un modulo PDF. È possibile importare i dati del modulo in un modulo PDF.

### Richiama il passaggio DDX {#invokeddx}

Esegue il file DDX sulla mappa specificata dei documenti di input e restituisce i documenti PDF modificati.

>[!NOTE]
>
>È possibile utilizzare le variabili per specificare il file DDX per i documenti di input. Memorizzare il file DDX in una variabile del tipo di dati Document o XML.

###  passo Optimize PDF {#optimize-pdf-step}

Ottimizza i file PDF riducendone le dimensioni. Il risultato di questa conversione è rappresentato da file PDF di dimensioni inferiori rispetto alle versioni originali. Questa operazione converte anche i documenti PDF nella versione PDF specificata nei parametri di ottimizzazione.

Le impostazioni di ottimizzazione specificano la modalità di ottimizzazione dei file. Di seguito sono riportati alcuni esempi di impostazioni:

* Versione PDF di destinazione
* Eliminazione di oggetti quali azioni JavaScript e miniature di pagina incorporate
* Eliminazione di dati utente quali commenti e allegati di file
* Eliminazione delle impostazioni non valide o non utilizzate
* Compressione di dati non compressi o utilizzo di algoritmi di compressione più efficienti
* Rimozione dei font incorporati
* Impostazione dei valori di trasparenza

### Rendering del modulo PDF passaggio {#renderpdf}

Consente di eseguire il rendering di un modulo creato in Form Designer (XDP) in un modulo PDF.

>[!NOTE]
>
>Potete utilizzare le variabili per specificare il file modello per i documenti di input. Memorizzare il percorso del file modello in una variabile di tipo dati String.

### Passaggio del documento protetto {#secure-document-step}

Cifra, firma e certifica un documento.  AEM Forms supporta sia la crittografia basata su password che la crittografia basata su certificato. È inoltre possibile scegliere tra vari algoritmi per la firma dei documenti. Ad esempio, SHA-256 e SH-512. È inoltre possibile utilizzare il passaggio del flusso di lavoro per leggere ed estendere i documenti PDF. Il passaggio del flusso di lavoro fornisce l&#39;opzione per abilitare la decodifica dei codici a barre, le firme digitali, l&#39;importazione e l&#39;esportazione di dati PDF e altre opzioni.

### Passaggio di invio alla stampante {#send-to-printer-step}

Inviare un documento direttamente a una stampante. Supporta i seguenti meccanismi di accesso alla stampa:

* **Stampante** con accesso diretto: Una stampante installata sullo stesso computer è denominata stampante con accesso diretto e il computer è denominato host della stampante. Questo tipo di stampante può essere una stampante locale collegata direttamente al computer.
* **Stampante** con accesso diretto: La stampante installata in un server di stampa è accessibile da altri computer. Per la connessione a una stampante di rete sono disponibili tecnologie quali il sistema di stampa comune UNIX® (CUPS) e il protocollo Line Printer Daemon (LPD). Per accedere a una stampante con accesso indiretto, specificare il nome IP o host del server di stampa. Utilizzando questo meccanismo, è possibile inviare un documento a un URI LPD quando la rete ha un LPD in esecuzione. Il meccanismo consente di indirizzare il documento a qualsiasi stampante collegata alla rete con un LPD in esecuzione.

### Genera passo di output stampato {#generatePrintedOutput}

Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL in base a una struttura del modulo e a un file di dati. Il file di dati viene unito alla struttura del modulo e formattato per la stampa. L&#39;output generato da questo passaggio può essere inviato direttamente a una stampante o salvato come file. È consigliabile utilizzare questo passaggio quando si desidera utilizzare le strutture del modulo o i dati provenienti da un&#39;applicazione. Se le strutture del modulo o le strutture del modulo si trovano in rete, nel file system locale o in una posizione HTTP, utilizzare l&#39;operazione generatePrintedOutput.

Ad esempio, l&#39;applicazione richiede l&#39;unione di una struttura del modulo con un file di dati. I dati contengono centinaia di record. Inoltre, richiede l&#39;invio dell&#39;output a una stampante che supporti ZPL. La struttura del modulo e i dati di input dell&#39;utente si trovano in un&#39;applicazione. Utilizzare l&#39;operazione generatePrintedOutput per unire ogni record a una struttura del modulo e inviare l&#39;output a una stampante che supporta ZPL.

Il passaggio Genera output stampato ha le seguenti proprietà:

**Proprietà di input**

* **[!UICONTROL Selezionate il file modello utilizzando]**: Specificate il percorso del file modello. È possibile selezionare il file modello utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio, [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste nell&#39;archivio crx, un amministratore può creare il percorso prima di utilizzarlo. È inoltre possibile accettare payload come file di dati di input.

* **[!UICONTROL Selezionare il documento dati utilizzando]**: Specificare il percorso di un file di dati di input. È possibile selezionare il file di dati di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio, [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste nell&#39;archivio crx, un amministratore può creare il percorso prima di utilizzarlo.

* **[!UICONTROL Formato]** stampante: Un valore Formato di stampa che specifica il linguaggio di descrizione della pagina da utilizzare, quando non viene fornito un file XDC, per generare il flusso di output. Se si fornisce un valore letterale, selezionare uno dei seguenti valori:

   * **[!UICONTROL PCL]** personalizzato: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per PCL.
   * **[!UICONTROL PostScript]** personalizzato: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per PostScript.
   * **[!UICONTROL ZPL]** personalizzato: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per ZPL.
   * **[!UICONTROL PCL a colori generico (5c)]**: Utilizzare un PCL a colori generico (5c).
   * **[!UICONTROL PostScript generico di livello3]**: Utilizzare PostScript generico di livello 3.
   * **[!UICONTROL ZPL 300 DPI]**: Utilizzate ZPL 300 DPI. Viene utilizzato zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: Utilizzate ZPL 600 DPI. Viene utilizzato il file zpl600.xdc.
   * **[!UICONTROL IPL]** personalizzato: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per IPL.
   * **[!UICONTROL IPL 300 DPI]**: Utilizzate IPL 300 DPI. Viene utilizzato ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: Utilizzate IPL 400 DPI. Viene utilizzato il file ipl400.xdc.
   * **[!UICONTROL TPCL]** personalizzato: Utilizzare l&#39;opzione per specificare un file XDC personalizzato per TPCL.
   * **[!UICONTROL TPCL 305 DPI]**: Utilizzate TPCL 300 DPI. Viene utilizzato il file tpcl305.xdc.
   * **[!UICONTROL PCL 600 DPI]**: Utilizzate TPCL 600 DPI. Viene utilizzato il file tpcl600.xdc.
   * **[!UICONTROL DPL]** personalizzato: Utilizzare l&#39;opzione per specificare un file DPL XDC personalizzato.
   * **[!UICONTROL DPL300DPI]**: Utilizzate DPL 300 DPI. Viene utilizzato il file dpl300.xdc.
   * **[!UICONTROL DPL406DPI]**: Utilizzate DPL 400 DPI. Viene utilizzato dpl406.xdc.
   * **[!UICONTROL DPL600DPI]**: Utilizzate DPL 600 DPI. Viene utilizzato dpl600.xdc.

**Proprietà output**

* **[!UICONTROL Salva documento di output utilizzando]**: Specificare il percorso in cui salvare il file di output. È possibile salvare il file di output in una posizione relativa al payload, in una variabile, oppure specificare una posizione assoluta in cui salvare il file di output. Se il percorso non esiste nell&#39;archivio crx, un amministratore può creare il percorso prima di utilizzarlo.

**Proprietà avanzate**

* **[!UICONTROL Selezionate Posizione directory principale contenuto utilizzando]**: La radice del contenuto è un valore di stringa che specifica l&#39;URI, il riferimento assoluto o la posizione nell&#39;archivio per recuperare le risorse relative utilizzate dalla struttura del modulo. Ad esempio, se la struttura del modulo fa riferimento a un&#39;immagine relativa, ad esempio ../myImage.gif, myImage.gif deve essere ubicata in repository://. Il valore predefinito è repository://, che indica il livello principale della directory archivio.

   Quando scegliete una risorsa dall’applicazione, il percorso URI radice contenuto deve avere la struttura corretta. Ad esempio, se un modulo viene prelevato da un&#39;applicazione denominata SampleApp e viene posizionato in SampleApp/1.0/forms/Test.xdp, l&#39;URI della directory principale contenuto deve essere specificato come repository://administrator@password/Applications/SampleApp/1.0/forms/ oppure repository:/Applications/SampleApp/1.0/forms/ (quando l&#39;autorità è null). Quando l&#39;URI della directory principale contenuto viene specificato in questo modo, i percorsi di tutte le risorse di riferimento nel modulo verranno risolti rispetto a questo URI.

* **[!UICONTROL Selezionare il file XCI utilizzando]**: I file XCI vengono utilizzati per descrivere i font e altre proprietà utilizzati per gli elementi della struttura del modulo. È possibile mantenere un file XCI relativo al payload, a un percorso assoluto o utilizzando una variabile del tipo di dati Documento.

* **[!UICONTROL Impostazioni internazionali]**: Specifica la lingua utilizzata per generare il documento PDF. Se si specifica un valore letterale, selezionare una lingua dall&#39;elenco o selezionare uno dei seguenti valori:
   * **Per utilizzare il server predefinito**: (Impostazione predefinita) Utilizzate le impostazioni internazionali configurate sul server AEM Forms . L’impostazione internazionale è configurata tramite la console di amministrazione. (Vedere [Guida di Designer](http://www.adobe.com/go/learn_aemforms_designer_65).)

   * **Per utilizzare un valore** personalizzato: Digitare il codice delle impostazioni internazionali nella casella letterale o selezionare una variabile di stringa contenente il codice delle impostazioni internazionali. Per un elenco completo dei codici lingua supportati, consultate http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copie]**: Un valore intero che specifica il numero di copie da generare per l&#39;output. Il valore predefinito è 1.

* **[!UICONTROL Stampa]** fronte retro: Valore di impaginazione che specifica se utilizzare la stampa fronte/retro o solo fronte. Le stampanti che supportano PostScript e PCL utilizzano questo valore. Se si fornisce un valore letterale, selezionare uno dei seguenti valori:
   * **[!UICONTROL Bordo]** lungo fronte retro: Utilizzare la stampa e la stampa fronte/retro utilizzando l&#39;impaginazione sul lato lungo.
   * **[!UICONTROL Bordo]** corto fronte retro: Utilizzare la stampa e la stampa fronte/retro utilizzando l&#39;impaginazione sul lato corto.
   * **[!UICONTROL Semplicex]**: Utilizzare la stampa su un solo lato.