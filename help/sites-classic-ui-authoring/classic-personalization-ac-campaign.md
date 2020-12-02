---
title: Utilizzo di Adobe Campaign 6.1 e Adobe Campaign Standard
seo-title: Utilizzo di Adobe Campaign 6.1 e Adobe Campaign Standard
description: È possibile creare contenuti e-mail in AEM ed elaborarli nelle e-mail di Adobe Campaign.
seo-description: È possibile creare contenuti e-mail in AEM ed elaborarli nelle e-mail di Adobe Campaign.
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 69%

---


# Utilizzo di Adobe Campaign 6.1 e Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

È possibile creare contenuti e-mail in AEM ed elaborarli nelle e-mail di Adobe Campaign. Per fare questo, devi effettuare le seguenti operazioni:

1. Crea una nuova newsletter in AEM da un modello specifico per Adobe Campaign.
1. Seleziona [un servizio Adobe Campaign](#selectingtheadobecampaigncloudservice) prima di modificare il contenuto per accedere a tutte le funzionalità.
1. Modifica il contenuto.
1. Convalida il contenuto.

Puoi quindi sincronizzare i contenuti con una consegna in Adobe Campaign. Le istruzioni dettagliate sono descritte in questo documento.

>[!NOTE]
>
>Prima di poter utilizzare questa funzionalità, devi configurare AEM per l’integrazione con [Adobe Campaign](/help/sites-administering/campaignonpremise.md) o [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Invio di contenuti e-mail tramite Adobe Campaign {#sending-email-content-via-adobe-campaign}

Dopo aver configurato AEM e Adobe Campaign, puoi creare contenuti per l’invio di e-mail direttamente in AEM e quindi elaborarli in Adobe Campaign.

Quando create  contenuto Adobe Campaign in AEM, dovete impostare un collegamento a un servizio  Adobe Campaign prima di modificare il contenuto per accedere a tutte le funzionalità.

Esistono due casi possibili:

* Puoi sincronizzare il contenuto con una consegna da Adobe Campaign. In questo modo puoi utilizzare i contenuti AEM in una consegna.
* (Solo Adobe Campaign locale) Il contenuto può essere inviato direttamente ad Adobe Campaign, che genera in automatico una nuova e-mail di consegna. Questa modalità presenta alcune limitazioni.

Le istruzioni dettagliate sono descritte in questo documento.

### Creazione di nuovi contenuti e-mail  {#creating-new-email-content}

>[!NOTE]
>
>Quando aggiungete dei modelli e-mail, accertatevi di aggiungerli in **/content/campaign** per renderli disponibili.


1. In AEM, selezionate la cartella **Siti Web**, quindi individuate il percorso in cui vengono gestite le campagne e-mail. Nell&#39;esempio seguente, il nodo interessato è **Siti Web** > **Campagne** > **Geometrixx Outdoors** > **Campagne e-mail**.

   >[!NOTE]
   >
   >[I modelli e-mail sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md#weretail). Scaricate contenuti di Geometrixx di esempio da Package Share.

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. Selezionare **Nuovo** > **Nuova pagina** per creare nuovo contenuto e-mail.
1. Seleziona uno dei modelli disponibili specifici di Adobe Campaign, quindi inserisci le proprietà generali della pagina. Per impostazione predefinita, sono disponibili tre modelli:

   * **E-mail di Adobe Campaign (AC 6.1)**: consente di aggiungere contenuti a un pattern predefinito prima di inviarlo ad Adobe Campaign 6.1 per la consegna.
   * **E-mail di Adobe Campaign (ACS)**: consente di aggiungere contenuti a un modello predefinito prima di inviarlo ad Adobe Campaign Standard per la consegna.

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. Fate clic su **Crea** per creare il messaggio e-mail o la newsletter.

### Selezione del servizio cloud e del modello di Adobe Campaign {#selecting-the-adobe-campaign-cloud-service-and-template}

Per l’integrazione con Adobe Campaign, è necessario aggiungere alla pagina un servizio cloud Adobe Campaign. In questo modo si ha accesso alla personalizzazione e ad altre informazioni Adobe Campaign.

Inoltre, potrebbe essere necessario selezionare il modello di Adobe Campaign, modificare l’oggetto e aggiungere contenuto in testo non formattato per gli utenti che non visualizzano l’e-mail in HTML.

1. Selezionare la scheda **Pagina** nella barra laterale, quindi selezionare **Proprietà pagina.**
1. Nella scheda **Servizi cloud** della finestra a comparsa, selezionare **Aggiungi servizio** per aggiungere il servizio Adobe Campaign  e fare clic su **OK**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. Seleziona la configurazione che corrisponde all’istanza di Adobe Campaign dall’elenco a discesa, quindi fai clic su **OK**.

   >[!NOTE]
   >
   >Assicurati di toccare fare clic su **OK** o **Applica** dopo l’aggiunta dei servizi cloud. In questo modo la scheda **Adobe Campaign** funziona correttamente.

1. Se desiderate applicare un modello di consegna e-mail specifico (da  Adobe Campaign), diverso dal modello predefinito **mail**, selezionate di nuovo **Proprietà pagina**. Nella scheda **Adobe Campaign**, immettete il nome interno del modello di consegna e-mail nell&#39;istanza Adobe Campaign  correlata.

   In Adobe Campaign Standard, il modello è **Consegna con il contenuto di AEM**. In Adobe Campaign 6.1, il modello è **Consegna e-mail con il contenuto di AEM**.

   Quando selezionate il modello, AEM automaticamente abilita i componenti **Adobe Campaign Newsletter**.

### Modifica del contenuto dei messaggi e-mail {#editing-email-content}

È possibile modificare il contenuto del messaggio e-mail nell’interfaccia classica o nell’interfaccia utente ottimizzata per il tocco.

1. Immettete l&#39;oggetto e la versione del testo del messaggio e-mail selezionando **Proprietà pagina** > **E-mail** dalla casella degli strumenti.

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. Modifica il contenuto del messaggio e-mail aggiungendo elementi tra quelli disponibili nella barra laterale. Per fare questo, trascinali e rilasciali. Quindi, fai doppio clic sull’elemento da modificare.

   Ad esempio, puoi aggiungere testo contenente i campi per la personalizzazione.

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Per una descrizione dei componenti disponibili per le newsletter/campagne e-mail di Adobe Campaign, vedi [Componenti di Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-177](assets/chlimage_1-177.png)

### Inserimento di personalizzazioni {#inserting-personalization}

Quando modifichi i contenuti, puoi inserire:

* Campi di contesto di Adobe Campaign. Si tratta di campi che è possibile inserire all&#39;interno del testo e che si adattano in base ai dati del destinatario (ad esempio nome, cognome o qualsiasi dato della dimensione di destinazione).
* Blocchi di personalizzazione per Adobe Campaign. Si tratta di blocchi di contenuto predefinito che non sono correlati ai dati del destinatario, ad esempio un logo marchio, o un collegamento a una pagina mirror.

Per una descrizione dettagliata di ciascun componente, vedi [Componenti di Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

>[!NOTE]
>
>* Vengono presi in considerazione solo i campi della dimensione di destinazione dei **Profili** di Adobe Campaign.
>* Quando si visualizzano le proprietà da **Siti**, non si dispone dell&#39;accesso ai campi  contesto Adobe Campaign. È possibile accedere a tali informazioni direttamente dall’e-mail durante la modifica.

>



1. Inserite un nuovo componente **Newsletter** > **Testo e personalizzazione (Campaign)**.
1. Apri il componente facendo doppio clic su d esso. La finestra **Modifica** ha una funzionalità che permette di inserire gli elementi di personalizzazione.

   >[!NOTE]
   >
   >I campi di contesto disponibili corrispondono alla dimensione di targeting dei **Profili** in Adobe Campaign.
   >
   >Vedere [Collegamento di una pagina AEM a un&#39;e-mail  Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Selezionare **ClientContext** nella barra laterale per verificare i campi di personalizzazione utilizzando i dati nei profili personali.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Viene visualizzata una finestra che consente di selezionare la persona desiderata. I campi di personalizzazione vengono sostituiti automaticamente dai dati del profilo selezionato.

   ![chlimage_1-180](assets/chlimage_1-180.png)

### Anteprima di una newsletter {#previewing-a-newsletter}

Puoi visualizzare in anteprima l’aspetto della newsletter e la personalizzazione.

1. Apri la newsletter da visualizzare in anteprima e fai clic su Anteprima (lente d’ingrandimento) per ridurre la barra laterale.
1. Fai clic su una delle icone del client di posta per visualizzare l’aspetto della newsletter nei diversi client di posta.

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. Espandi la barra laterale per ricominciare a modificare.

### Approvazione dei contenuti in AEM  {#approving-content-in-aem}

Una volta completato il contenuto, è possibile avviare il processo di approvazione. Fare clic sulla scheda **Workflow** della casella degli strumenti e selezionare il flusso di lavoro **Approva per  Adobe Campaign**.

Questo flusso di lavoro preconfigurato si articola in due fasi: revisione e approvazione, oppure revisione e rifiuto. Tuttavia, può essere esteso e adattato a un processo più complesso.

![chlimage_1-182](assets/chlimage_1-182.png)

Per approvare il contenuto per Adobe Campaign, applica il flusso di lavoro selezionando **Flusso di lavoro** nella barra laterale e seleziona **Approva per Adobe Campaign** e fai clic su **Avvia flusso di lavoro**. Scorrete i passaggi e approvate il contenuto. È inoltre possibile rifiutare i contenuti selezionando **Rifiuta** anziché **Approva** nell’ultimo passaggio del flusso di lavoro.

![chlimage_1-183](assets/chlimage_1-183.png)

Dopo l’approvazione del contenuto, questo viene visualizzato come approvato in Adobe Campaign. L’e-mail può quindi essere inviata.

In Adobe Campaign Standard:

![chlimage_1-184](assets/chlimage_1-184.png)

In Adobe Campaign 6.1:

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>I contenuti non approvati possono essere sincronizzati con una consegna in Adobe Campaign, ma la consegna non può essere eseguita. Solo i contenuti approvati possono essere inviati tramite le consegne di Campaign.

## Collegamento di AEM con Adobe Campaign Standard e Adobe Campaign 6.1  {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Collegamento AEM con  Adobe Campaign Standard e  Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) in [Utilizzo  Adobe Campaign 6.1 e  Adobe Campaign Standard](/help/sites-authoring/campaign.md) nella documentazione standard sull&#39;authoring.

