---
title: Utilizzo di Adobe Campaign Classic e Adobe Campaign Standard
description: Puoi creare contenuti e-mail in AEM ed elaborarli in e-mail Adobe Campaign
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d7e4d424-0ca7-449f-95fb-c4fe19dd195d
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '2769'
ht-degree: 2%

---

# Utilizzo di Adobe Campaign Classic e Adobe Campaign Standard{#working-with-adobe-campaign-classic-and-adobe-campaign-standard}

Puoi creare contenuti e-mail in AEM ed elaborarli in e-mail Adobe Campaign. Per farlo, devi:

1. Crea una newsletter in AEM da un modello specifico di Adobe Campaign.
1. Seleziona [un servizio Adobe Campaign](#selecting-the-adobe-campaign-cloud-service-and-template) prima di modificare il contenuto per accedere a tutte le funzionalità.
1. Modifica il contenuto.
1. Convalida il contenuto.

Il contenuto può quindi essere sincronizzato con una consegna in Adobe Campaign. Istruzioni dettagliate sono descritte in questo documento.

Vedi anche [Creazione di Adobe Campaign Forms in AEM](/help/sites-authoring/adobe-campaign-forms.md).

>[!NOTE]
>
>Prima di poter utilizzare questa funzionalità, devi configurare AEM per l&#39;integrazione con [Adobe Campaign](/help/sites-administering/campaignonpremise.md) o [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Invio di contenuti e-mail tramite Adobe Campaign {#sending-email-content-via-adobe-campaign}

Dopo aver configurato AEM e Adobe Campaign, puoi creare i contenuti di consegna e-mail direttamente in AEM, quindi elaborarli in Adobe Campaign.

Quando crei contenuti Adobe Campaign in AEM, devi collegare un servizio Adobe Campaign prima di modificarli per accedere a tutte le funzionalità.

Esistono due casi possibili:

* Il contenuto può essere sincronizzato con una consegna da Adobe Campaign. Questo consente di utilizzare il contenuto di AEM in una consegna.
* (Solo per Adobe Campaign Classic) Il contenuto può essere inviato direttamente ad Adobe Campaign, che genera automaticamente una nuova consegna e-mail. Questa modalità presenta limitazioni.

Istruzioni dettagliate sono descritte in questo documento.

### Creazione di nuovi contenuti e-mail {#creating-new-email-content}

>[!NOTE]
>
>Quando aggiungi modelli e-mail, assicurati di aggiungerli in **/content/campaigns** per renderli disponibili.

#### Creazione di nuovi contenuti e-mail {#creating-new-email-content-1}

1. In AEM, seleziona **Sites**, quindi **Campagne**, quindi individua il punto in cui vengono gestite le campagne e-mail. Nell&#39;esempio seguente, il percorso è **Siti** > **Campagne** > **Geometrixx Outdoors** > **Campagne e-mail**.

   >[!NOTE]
   >
   >[Gli esempi di e-mail sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md). Scarica contenuti Geometrixx di esempio da Package Share.

   ![chlimage_1-15](assets/chlimage_1-15a.png)

1. Seleziona **Crea** e quindi **Crea pagina**.
1. Seleziona uno dei modelli disponibili specifici per l&#39;Adobe Campaign a cui ti stai connettendo, quindi fai clic su **Avanti**. Per impostazione predefinita sono disponibili tre modelli:

   * **E-mail Adobe Campaign Classic**: ti consente di aggiungere contenuto a un modello predefinito (due colonne) prima di inviarlo a Adobe Campaign Classic per la consegna.
   * **E-mail Adobe Campaign Standard**: ti consente di aggiungere contenuto a un modello predefinito (due colonne) prima di inviarlo ad Adobe Campaign Standard per la consegna.

1. Compila il **Titolo** e facoltativamente la **Descrizione** e fai clic su **Crea**. Il titolo viene utilizzato come oggetto della newsletter/e-mail a meno che non venga sovrascritto durante la modifica dell’e-mail.

### Selezione del servizio cloud Adobe Campaign e del modello {#selecting-the-adobe-campaign-cloud-service-and-template}

Per l’integrazione con Adobe Campaign, devi aggiungere alla pagina un servizio cloud Adobe Campaign. In questo modo puoi accedere alla personalizzazione e ad altre informazioni su Adobe Campaign.

Inoltre, potrebbe essere necessario selezionare il modello Adobe Campaign, modificare l’oggetto e aggiungere contenuto di testo normale per gli utenti che non visualizzeranno l’e-mail in HTML.

Puoi selezionare il servizio cloud dalla scheda **Sites** o dall&#39;interno dell&#39;e-mail/newsletter dopo averlo creato.

Si consiglia di selezionare il servizio cloud dalla scheda **Sites**. La selezione del servizio cloud dall’e-mail/newsletter richiede una soluzione alternativa.

Dalla pagina **Sites**:

1. In AEM, seleziona la pagina e-mail e fai clic su **Visualizza proprietà**.

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. Seleziona **Modifica** e quindi la scheda **Servizi cloud**, scorri verso il basso e fai clic sul segno + per aggiungere una configurazione, quindi seleziona **Adobe Campaign**.

   ![chlimage_1-17](assets/chlimage_1-17a.png)

1. Seleziona la configurazione che corrisponde alla tua istanza di Adobe Campaign dall&#39;elenco a discesa, quindi conferma facendo clic su **Salva**.
1. Puoi visualizzare il modello applicato dall&#39;e-mail facendo clic sulla scheda **Adobe Campaign**. Se desideri selezionare un altro modello, puoi accedervi dall’interno dell’e-mail durante la modifica.

   Se desideri applicare un modello di consegna e-mail specifico (da Adobe Campaign), diverso dal modello di posta predefinito, in **Proprietà**, seleziona la scheda **Adobe Campaign**. Immetti il nome interno del modello di consegna e-mail nell’istanza di Adobe Campaign correlata.

   Il modello selezionato determina i campi di personalizzazione disponibili da Adobe Campaign.

   ![chlimage_1-18](assets/chlimage_1-18a.png)

Nella newsletter/e-mail in fase di authoring, potresti non essere in grado di selezionare la configurazione del servizio cloud Adobe Campaign in **Proprietà pagina** a causa di un problema di layout. È possibile utilizzare la soluzione alternativa descritta di seguito:

1. In AEM, seleziona la pagina e-mail e fai clic su **Modifica**. Fare clic su **Apri proprietà**.

   ![chlimage_1-19](assets/chlimage_1-19a.png)

1. Seleziona **Servizi cloud** e fai clic su **+** per aggiungere una configurazione. Seleziona una configurazione visibile (non importa quale). Fai clic sul segno **+** per aggiungere un&#39;altra configurazione, quindi seleziona **Adobe Campaign**.

   >[!NOTE]
   >
   >In alternativa, è possibile selezionare i servizi cloud selezionando **Visualizza proprietà** nella scheda **Sites**.

1. Seleziona dall’elenco a discesa la configurazione che corrisponde all’istanza di Adobe Campaign in uso, elimina la prima configurazione creata che non era per Adobe Campaign, quindi conferma facendo clic sul segno di spunta.
1. Procedi con il passaggio 4 della procedura precedente per selezionare i modelli e aggiungere testo normale.

### Modifica del contenuto delle e-mail {#editing-email-content}

Per modificare il contenuto delle e-mail:

1. Apri l’e-mail e, per impostazione predefinita, entra in modalità Modifica.

   ![chlimage_1-20](assets/chlimage_1-20a.png)

1. Se desideri modificare l&#39;oggetto dell&#39;e-mail o aggiungere testo normale per gli utenti che non visualizzeranno l&#39;e-mail in HTML, seleziona **E-mail** e aggiungi un oggetto e un testo. Seleziona l’icona della pagina per generare automaticamente una versione in testo normale da HTML. Al termine, fai clic sul segno di spunta.

   Puoi personalizzare la newsletter utilizzando i campi di personalizzazione di Adobe Campaign. Per aggiungere un campo di personalizzazione, apri il selettore dei campi di personalizzazione facendo clic sul pulsante con il logo Adobe Campaign. Potrai quindi scegliere tra tutti i campi disponibili per questa newsletter.

   >[!NOTE]
   >
   >Se i campi di personalizzazione nelle proprietà dall’interno dell’editor sono disattivati, riesamina la configurazione.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Apri il pannello dei componenti sul lato sinistro dello schermo e seleziona **Adobe Campaign Newsletter** dal menu a discesa per trovare tali componenti.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. Trascina i componenti direttamente nella pagina e modificali di conseguenza. Ad esempio, puoi trascinare un componente **Text &amp; Personalization (Campaign)** e aggiungere testo personalizzato.

   ![chlimage_1-23](assets/chlimage_1-23a.png)

   Per una descrizione dettagliata di ciascun componente, vedi [Componenti Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).

   ![chlimage_1-24](assets/chlimage_1-24a.png)

### Inserimento della personalizzazione {#inserting-personalization}

Durante la modifica del contenuto, puoi inserire:

* Campi contestuali di Adobe Campaign. Si tratta di campi che puoi inserire all’interno del testo e che si adattano in base ai dati del destinatario (ad esempio, nome, cognome o qualsiasi dato della dimensione di destinazione).
* Blocchi di personalizzazione di Adobe Campaign. Si tratta di blocchi di contenuto predefinito non correlati ai dati del destinatario, ad esempio il logo di un brand o il collegamento a una pagina speculare.

Consulta [Componenti Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) per una descrizione completa dei componenti di Campaign.

>[!NOTE]
>
>* Vengono presi in considerazione solo i campi della dimensione di targeting **Profili** di Adobe Campaign.
>* Quando si visualizzano le proprietà da **Sites**, non si dispone dell&#39;accesso ai campi contestuali di Adobe Campaign. Puoi accedervi direttamente dall’e-mail durante la modifica.

Per inserire la personalizzazione:

1. Inserisci un nuovo componente **Newsletter** > **Testo e Personalization (Campaign)** trascinandolo sulla pagina.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Apri il componente facendo clic sull’icona della matita. Viene aperto l’editor locale.

   ![chlimage_1-26](assets/chlimage_1-26a.png)

   >[!NOTE]
   >
   >**Per Adobe Campaign Standard:**
   >
   >* I campi di contesto disponibili corrispondono alla dimensione di targeting **Profili** in Adobe Campaign.
   >* Vedi [Collegamento di una pagina di AEM a un&#39;e-mail di Adobe Campaign](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard).
   >
   >**Per Adobe Campaign Classic:**
   >
   >* I campi di contesto disponibili vengono recuperati in modo dinamico dallo schema Adobe Campaign **nms:seedMember**. I dati dell’estensione di Target vengono recuperati in modo dinamico dal flusso di lavoro che contiene la consegna sincronizzata con il contenuto. (Vedi la sezione [Sincronizzazione del contenuto creato in AEM con una consegna da Adobe Campaign](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)).
   >
   >* Per aggiungere o nascondere elementi di personalizzazione, vedere [Gestione di campi e blocchi di personalizzazione](/help/sites-administering/campaignonpremise.md#managing-personalization-fields-and-blocks).
   >* **Importante**: tutti i campi della tabella di seeding devono essere presenti anche nella tabella dei destinatari o nella tabella dei contatti corrispondente.

1. Inserire il testo digitandolo. Per inserire campi di contesto o blocchi di personalizzazione, fai clic sui componenti di Adobe Campaign e selezionali. Al termine, seleziona il segno di spunta.

   ![chlimage_1-27](assets/chlimage_1-27a.png)

   Dopo aver inserito campi di contesto o blocchi di personalizzazione, puoi visualizzare in anteprima la newsletter e verificare i campi. Vedi [Anteprima di una newsletter](#previewing-a-newsletter).

### Anteprima di una newsletter {#previewing-a-newsletter}

Puoi visualizzare in anteprima come si presenterà la newsletter e la personalizzazione.

1. Con la newsletter aperta, fai clic su **Anteprima** nell&#39;angolo superiore destro di AEM. AEM mostra l’aspetto della newsletter quando gli utenti la ricevono.

   ![chlimage_1-28](assets/chlimage_1-28a.png)

   >[!NOTE]
   >
   >Se utilizzi Adobe Campaign Standard e utilizzi il modello di esempio, due blocchi di personalizzazione che visualizzano il contenuto iniziale - **&quot;&lt;%@ include view=&quot;MirrorPage&quot; %>&quot;** e **&quot;&lt;%@ include view=&quot;UnsubscriptionLink&quot; %>&quot;** - genereranno errori durante l’importazione del contenuto durante la consegna. Puoi regolarli selezionando i blocchi corrispondenti utilizzando il selettore dei blocchi di personalizzazione.

1. Per visualizzare in anteprima la personalizzazione, apri ContextHub facendo clic o toccando l’icona corrispondente nella barra degli strumenti. I tag dei campi di personalizzazione vengono ora sostituiti dai dati di seed dell’utente tipo selezionato. Scopri come le variabili si adattano quando si passa da un utente tipo a un altro in ContextHub.

   ![chlimage_1-29](assets/chlimage_1-29a.png)

1. Puoi visualizzare i dati di seed provenienti da Adobe Campaign e associati all’utente tipo attualmente selezionato. A questo scopo, fai clic sul modulo Adobe Campaign nella barra di ContextHub. Viene visualizzata una finestra di dialogo in cui vengono visualizzati tutti i dati di inizializzazione del profilo corrente. Anche in questo caso, i dati si adattano quando si passa a un utente tipo diverso.

   ![chlimage_1-30](assets/chlimage_1-30a.png)

### Approvazione di contenuti in AEM {#approving-content-in-aem}

Al termine del contenuto, puoi avviare il processo di approvazione. Vai alla scheda **Flusso di lavoro** della casella degli strumenti e seleziona il flusso di lavoro **Approva per Adobe Campaign**.

Questo flusso di lavoro preconfigurato prevede due passaggi: revisione e quindi approvazione oppure revisione e infine rifiuto. Tuttavia, questo flusso di lavoro può essere esteso e adattato a un processo più complesso.

![chlimage_1-31](assets/chlimage_1-31a.png)

Per approvare il contenuto per Adobe Campaign, applica il flusso di lavoro selezionando **Flusso di lavoro**, selezionando **Approva per Adobe Campaign** e facendo clic su **Avvia flusso di lavoro**. Segui i passaggi e approva il contenuto. Puoi anche rifiutare il contenuto selezionando **Rifiuta** invece di **Approva** nell&#39;ultimo passaggio del flusso di lavoro.

![chlimage_1-32](assets/chlimage_1-32a.png)

Dopo l’approvazione, il contenuto viene visualizzato come approvato in Adobe Campaign. L’e-mail può quindi essere inviata.

In Adobe Campaign Standard:

![chlimage_1-33](assets/chlimage_1-33a.png)

In Adobe Campaign Classic:

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>Il contenuto non approvato può essere sincronizzato con una consegna in Adobe Campaign, ma la consegna non può essere eseguita. Solo i contenuti approvati possono essere inviati tramite le consegne di Campaign.

## Collegamento di AEM con Adobe Campaign Standard e Adobe Campaign Classic {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic}

Il modo in cui si collega o sincronizza AEM con Adobe Campaign dipende dal fatto che si utilizzi un Adobe Campaign Standard basato su abbonamento o un Adobe Campaign Classic basato su on-premise.

Per istruzioni basate sulla soluzione Adobe Campaign in uso, consulta le sezioni seguenti:

* [Collegamento di una pagina di AEM a un’e-mail di Adobe Campaign (Adobe Campaign Standard)](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)
* [Sincronizzazione dei contenuti creati in AEM con una consegna da Adobe Campaign Classic](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)

### Collegamento di una pagina di AEM a un’e-mail di Adobe Campaign (Adobe Campaign Standard) {#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard}

Adobe Campaign Standard consente di recuperare e collegare i contenuti creati in AEM con:

* Un messaggio e-mail.
* Un modello e-mail.

In questo modo puoi distribuire i contenuti. Puoi vedere se una newsletter è collegata a una singola consegna dal codice visualizzato nella pagina.

![chlimage_1-35](assets/chlimage_1-35a.png)

>[!NOTE]
>
>Se una newsletter è collegata a più consegne, indica il numero di consegne collegate (ma non ogni ID).

Per collegare una pagina creata in AEM con un messaggio e-mail di Adobe Campaign:

1. Crea un messaggio e-mail basato su un modello e-mail specifico di AEM. Per ulteriori informazioni, consulta [Creazione di e-mail in Adobe Campaign Standard](https://helpx.adobe.com/it/campaign/standard/channels/using/creating-an-email.html).

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. Apri il blocco **Content** dal dashboard di consegna.

   ![chlimage_1-37](assets/chlimage_1-37a.png)

1. Selezionare **Collegamento con contenuto Adobe Experience Manager** nella barra degli strumenti per accedere all&#39;elenco dei contenuti disponibili in AEM.

   >[!NOTE]
   >
   >Se l&#39;opzione **Collegamento con Adobe Experience Manager** non viene visualizzata nella barra delle azioni, verificare che la **modalità di modifica del contenuto** sia configurata correttamente impostata su **Adobe Experience Manager** nelle proprietà e-mail.

   ![chlimage_1-38](assets/chlimage_1-38a.png)

1. Seleziona il contenuto da utilizzare nell’e-mail.

   Questo elenco specifica:

   * Etichetta del contenuto in AEM.
   * Lo stato di approvazione del contenuto in AEM. Se il contenuto non è approvato, puoi sincronizzarlo ma dovrà essere approvato prima dell’invio della consegna. Tuttavia, puoi eseguire alcune operazioni, ad esempio l’invio di una bozza o il test di anteprima.
   * Data dell’ultima modifica del contenuto.
   * Eventuali contenuti già collegati a una consegna.

   >[!NOTE]
   >
   >Per impostazione predefinita, il contenuto già sincronizzato con una consegna è nascosto. Tuttavia, puoi visualizzarlo e utilizzarlo. Ad esempio, se desideri utilizzare il contenuto come modello per diverse consegne.

   Quando l’e-mail è collegata a un contenuto AEM, non è possibile modificarne il contenuto in Adobe Campaign.

1. Specifica gli altri parametri del messaggio e-mail dal dashboard (pubblico, pianificazione dell’esecuzione).
1. Esegui la consegna e-mail. Durante l’analisi della consegna, viene recuperata la versione più aggiornata del contenuto AEM.

   >[!NOTE]
   >
   >Se il contenuto viene aggiornato in AEM mentre è collegato a un’e-mail, viene automaticamente aggiornato in Adobe Campaign durante l’analisi. È inoltre possibile eseguire manualmente la sincronizzazione utilizzando **Aggiorna contenuto Adobe Experience Manager** dalla barra delle azioni del contenuto.
   >
   >Puoi annullare il collegamento tra un&#39;e-mail e il contenuto di AEM utilizzando **Elimina il collegamento con il contenuto di Adobe Experience Manager** dalla barra delle azioni del contenuto. Questo pulsante è disponibile solo se un contenuto è già collegato alla consegna. Per collegare un contenuto diverso a una consegna, è necessario eliminare il collegamento del contenuto corrente prima di poter stabilire un nuovo collegamento.
   >
   >Quando il collegamento viene eliminato, il contenuto locale viene mantenuto e diventa modificabile in Adobe Campaign. Se colleghi nuovamente il contenuto dopo averlo modificato, tutte le modifiche andranno perse.

### Sincronizzazione dei contenuti creati in AEM con una consegna da Adobe Campaign Classic {#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic}

Adobe Campaign consente di recuperare e sincronizzare i contenuti creati in AEM con:

* Una consegna di campagna
* Un’attività di consegna in un flusso di lavoro della campagna
* Una consegna ricorrente
* Una consegna continua
* Una consegna del Centro messaggi
* Un modello di consegna

In AEM, se una newsletter è collegata a una singola consegna, il codice di consegna viene visualizzato nella pagina.

![chlimage_1-39](assets/chlimage_1-39a.png)

>[!NOTE]
>
>Se la newsletter è collegata a più consegne, indica il numero di consegne collegate (ma non tutti gli ID).
>
>[!NOTE]
>
>Il passaggio del flusso di lavoro **Pubblica in Adobe Campaign** è obsoleto in AEM 6.1. Questo passaggio faceva parte dell’integrazione di AEM 6.0 con Adobe Campaign e non è più necessario.

Per sincronizzare il contenuto creato in AEM con una consegna da Adobe Campaign:

1. Creare una consegna o aggiungere un&#39;attività di consegna a un flusso di lavoro della campagna selezionando il modello di consegna **Email delivery with AEM content (mailAEMContent)**.

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. Seleziona **Sincronizza** nella barra degli strumenti per accedere all&#39;elenco dei contenuti disponibili in AEM.

   >[!NOTE]
   >
   >Se l&#39;opzione **Sincronizza** non viene visualizzata nella barra degli strumenti della consegna, verificare che il campo **Modalità di modifica del contenuto** sia configurato correttamente in **AEM** selezionando **Proprietà** > **Avanzate**.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Seleziona il contenuto da sincronizzare con la consegna.

   Questo elenco specifica:

   * Etichetta del contenuto in AEM.
   * Lo stato di approvazione del contenuto in AEM. Se il contenuto non è approvato, puoi sincronizzarlo ma dovrà essere approvato prima dell’invio della consegna. Tuttavia, puoi eseguire alcune operazioni, ad esempio l’invio di un BAT o il test di anteprima.
   * La data dell’ultima modifica apportata al contenuto.
   * Eventuali contenuti già collegati a una consegna.

   >[!NOTE]
   >
   >Per impostazione predefinita, il contenuto già sincronizzato con una consegna è nascosto. Tuttavia, puoi visualizzarlo e utilizzarlo. Ad esempio, se desideri utilizzare il contenuto come modello per diverse consegne.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Specifica gli altri parametri della consegna (target e così via)
1. Se necessario, avvia il processo di approvazione della consegna in Adobe Campaign. Oltre alle approvazioni configurate in Adobe Campaign (budget, target e così via), è necessaria l’approvazione dei contenuti in AEM. L’approvazione dei contenuti in Adobe Campaign è possibile solo se il contenuto è già approvato in AEM.
1. Esegui la consegna. Durante l’analisi della consegna, viene recuperata la versione più aggiornata del contenuto AEM.

   >[!NOTE]
   >
   >* Dopo la sincronizzazione della consegna e del contenuto, il contenuto della consegna in Adobe Campaign diventa di sola lettura. L’oggetto e il contenuto dell’e-mail non possono più essere modificati.
   >* Se il contenuto viene aggiornato in AEM mentre è collegato a una consegna in Adobe Campaign, viene automaticamente aggiornato nella consegna durante l’analisi della consegna. La sincronizzazione può anche essere eseguita manualmente utilizzando il pulsante **Aggiorna contenuto ora**.
   >* Puoi annullare la sincronizzazione tra una consegna e il contenuto di AEM utilizzando il pulsante **Desincronizza**. Questa opzione è disponibile solo se un contenuto è già sincronizzato con la consegna. Per sincronizzare un contenuto diverso con una consegna, è necessario annullare la sincronizzazione del contenuto corrente prima di poter stabilire un nuovo collegamento.
   >* Se desincronizzato, il contenuto locale viene mantenuto e diventa modificabile in Adobe Campaign. Se sincronizzi nuovamente il contenuto dopo averlo modificato, tutte le modifiche andranno perse.
   >* Per le consegne ricorrenti e continue, la sincronizzazione con il contenuto di AEM viene interrotta ogni volta che viene eseguita la consegna.
