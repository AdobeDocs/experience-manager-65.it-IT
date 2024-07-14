---
title: Configurazione della campagna
description: Per impostare una nuova campagna devi creare un marchio che contenga le campagne, creare una campagna che contenga le esperienze e infine definire le proprietà per la nuova campagna.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 1b607a52-f065-4e35-8215-d54df7c8403d
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2194'
ht-degree: 1%

---

# Configurazione della campagna{#setting-up-your-campaign}

La configurazione di una nuova campagna include i seguenti passaggi (generici):

1. [Crea un marchio](#creating-a-new-brand) per le tue campagne.
1. Se necessario, puoi [definire le proprietà per il nuovo brand](#defining-the-properties-for-your-new-brand).
1. [Crea una campagna](#creating-a-new-campaign) per raccogliere esperienze, ad esempio pagine teaser o newsletter.
1. Se necessario, puoi [definire le proprietà per la nuova campagna](#defining-the-properties-for-your-new-campaign).

Quindi, a seconda del tipo di esperienze create, devi [creare un&#39;esperienza](#creating-a-new-experience). I dettagli dell’esperienza e le azioni che seguono la sua creazione dipendono dal tipo di esperienza che desideri creare:

* Se crei un teaser:

   1. [Crea un&#39;esperienza teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience).
   1. [Aggiungi contenuto al teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser).
   1. [Crea un punto di contatto per il teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (aggiungi il teaser a una pagina di contenuto).

* Durante la creazione di una newsletter:

   1. [Crea un&#39;esperienza newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience).
   1. [Aggiungi contenuto alla newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   1. [Personalizza la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   1. [Crea una pagina di destinazione interessante per le newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).
   1. [Invia la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) agli abbonati o ai lead.

* Durante la creazione di un&#39;offerta Adobe Target (precedentemente Test&amp;Target):

   1. [Crea un&#39;esperienza di offerta Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience).
   1. [Procedi all’integrazione con Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)

>[!NOTE]
>
>Per istruzioni dettagliate sulla definizione dei segmenti, consulta [Segmentazione](/help/sites-administering/campaign-segmentation.md).

## Creazione di un nuovo marchio {#creating-a-new-brand}

1. Apri **MCM** e seleziona **Campagne** nel riquadro a sinistra.

1. Seleziona **Nuovo...** per immettere **Titolo** e **Nome** e il modello da utilizzare per il nuovo brand:

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Fai clic su **Crea**. Il nuovo brand viene visualizzato in MCM (con un’icona predefinita).

### Definizione delle proprietà per il nuovo marchio {#defining-the-properties-for-your-new-brand}

1. Da **Campagne** nel riquadro di sinistra, seleziona l&#39;icona del nuovo brand nel riquadro di destra e fai clic su **Proprietà...**

   È possibile immettere un **Titolo**, **Descrizione** e un&#39;immagine da utilizzare come icona.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Fare clic su **OK** per salvare.

### Creazione di una nuova campagna {#creating-a-new-campaign}

1. Da **Campagne**, seleziona il nuovo brand nel riquadro di sinistra oppure fai doppio clic sull&#39;icona nel riquadro di destra.

   Viene visualizzata la panoramica (vuota se il brand è nuovo).

1. Fai clic su **Nuovo...** e specifica il **Titolo**, **Nome** e il modello da utilizzare per la nuova campagna.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Fai clic su **Crea**. La nuova campagna viene visualizzata in MCM.

### Definizione delle proprietà per la nuova campagna {#defining-the-properties-for-your-new-campaign}

Configura le proprietà della campagna che controllano il comportamento:

* **Priorità:** la priorità di questa campagna rispetto ad altre campagne. Quando più campagne sono contemporaneamente attive, la campagna con priorità più alta controlla l’esperienza del visitatore.
* **Ora di attivazione e disattivazione:** queste proprietà controllano il periodo di tempo in cui la campagna controlla l&#39;esperienza del visitatore. La proprietà On Time controlla il momento in cui la campagna inizia a controllare l’esperienza. La proprietà Off Time controlla quando le campagne non controllano più l’esperienza.
* **Immagine:** l&#39;immagine che rappresenta la campagna in AEM.
* **Cloud Services:** le configurazioni di Cloud Service con cui è integrata la campagna. (Vedere [Integrazione con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md).)

* **Adobe Target:** proprietà che configurano le campagne integrate con Adobe Target. (Vedi [Integrazione con Adobe Target](/help/sites-administering/target.md).)

1. Da **Campagne**, seleziona il tuo marchio. Nel riquadro di destra, seleziona la campagna e fai clic su **Proprietà**.

   Puoi immettere varie proprietà, tra cui un **Titolo**, **Descrizione** e qualsiasi **Cloud Service** desiderato.

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Fare clic su **OK** per salvare.

### Creazione di una nuova esperienza {#creating-a-new-experience}

La procedura per la creazione di un’esperienza dipende dal tipo di esperienza:

* [Creazione di un teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [Creazione di una newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [Creazione di un’offerta Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>Come per le versioni precedenti, è ancora possibile creare l&#39;esperienza come pagina nella console **Siti Web** (e tutte le pagine create nelle versioni precedenti sono ancora completamente supportate).
>
>Ora si consiglia di utilizzare MCM per creare le esperienze.

### Configurazione della nuova esperienza {#configuring-your-new-experience}

Dopo aver creato l’ossatura di base per l’esperienza, devi continuare con le seguenti azioni, a seconda del tipo di esperienza:

* [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers):

   * [Connetti la pagina del teaser ai segmenti dei visitatori.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [Crea un punto di contatto per il teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (aggiungi il teaser a una pagina di contenuto).

* [Newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters):

   * [Aggiungi contenuto alla newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   * [Personalizza la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   * [Invia la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) agli abbonati o ai lead.
   * [Crea una pagina di destinazione interessante per le newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).

* [Offerta Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers):

   * [Procedi all’integrazione con Adobe Target](/help/sites-administering/target.md)

### Aggiunta di un nuovo punto di contatto {#adding-a-new-touchpoint}

Se disponi di esperienze esistenti, puoi aggiungere un punto di contatto direttamente dalla vista Calendario di MCM:

1. Seleziona la vista calendario per la campagna.

1. Fare clic su **Aggiungi punto di contatto...** per aprire la finestra di dialogo. Specifica l’esperienza da aggiungere:

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Fare clic su **OK** per salvare.

## Utilizzo dei lead {#working-with-leads}

>[!NOTE]
>
>Adobe non prevede di migliorare ulteriormente questa funzionalità (Gestione dei lead).
>Si consiglia di utilizzare [Adobe Campaign e l&#39;integrazione con AEM](/help/sites-administering/campaign.md).

In AEM MCM, puoi organizzare e aggiungere lead immettendoli manualmente o importando un elenco separato da virgole, ad esempio una mailing list. Ulteriori modi per generare i lead sono dalle iscrizioni a newsletter o community (se configurate, possono attivare un flusso di lavoro che popola i lead).

I lead vengono generalmente suddivisi in categorie e inseriti in un elenco, in modo da poter eseguire successivamente azioni sull’intero elenco, ad esempio l’invio di un’e-mail personalizzata a un determinato elenco.

Nel dashboard, puoi accedere a tutti i lead facendo clic su **Lead** nel riquadro a sinistra. Puoi accedere ai lead anche dal riquadro **Elenchi**.

![schermata_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>Per aggiungere o modificare gli avatar degli utenti, apri il cloud clickstream (Ctrl+Alt+c), carica il profilo e fai clic su **Modifica**.

### Creazione di nuovi lead {#creating-new-leads}

Dopo aver creato nuovi lead, assicurati di [attivarli](#activating-or-deactivating-leads) in modo da poter tenere traccia della loro attività nell&#39;istanza di pubblicazione e personalizzare la loro esperienza.

Per creare manualmente un lead:

1. In AEM, passa a MCM. Nel dashboard, fai clic su **Lead**.
1. Fare clic su **Nuovo**. Viene visualizzata la finestra **Crea nuovo**.

   ![schermata_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. Immettere le informazioni nei campi, a seconda delle necessità. Fare clic sulla scheda **Indirizzo**.

   ![schermata_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. Immettere le informazioni sull&#39;indirizzo, se necessario. Fai clic su **Salva** per salvare il lead. Se devi aggiungere altri lead, fai clic su **Salva e nuovo**.

   Il nuovo lead viene visualizzato nel riquadro Lead. Quando si fa clic sulla voce, tutte le informazioni immesse vengono visualizzate nel riquadro di destra. Dopo aver creato un lead, è possibile aggiungerlo a un elenco.

   ![schermata_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### Attivazione o disattivazione di lead {#activating-or-deactivating-leads}

L’attivazione dei lead consente di tenere traccia della loro attività sull’istanza Publish e di personalizzare la loro esperienza. Se non desideri più tenere traccia della loro attività, puoi disattivarle.

Per i lead attivi o disattivi:

1. In AEM, passa a MCM e fai clic su **Lead**.

1. Selezionare i lead da attivare o disattivare e fare clic su **Attiva** o **Disattiva**.

   ![schermata_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   Come per le pagine AEM, lo stato di pubblicazione è indicato nella colonna **Pubblicato**.

   ![schermata_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### Importazione di nuovi lead {#importing-new-leads}

Quando si importano nuovi lead, è possibile aggiungerli automaticamente a un elenco esistente o creare un elenco per includerli.

Per importare i lead da un elenco separato da virgole:

1. In AEM, passa a MCM e fai clic su **Lead**.

   >[!NOTE]
   >
   >In alternativa, è possibile importare i lead eseguendo una delle operazioni seguenti:
   >
   >* Nel dashboard, fai clic su **Importa lead** nel riquadro **Elenchi**
   >* Fai clic su **Elenchi** e nel menu **Strumenti** seleziona **Importa lead**.

1. Nel menu **Strumenti**, seleziona **Importa** **Lead**.

1. Immettere le informazioni come descritto in Dati di esempio. È possibile importare i campi seguenti: email,familyName,givenName,gender,aboutMe,city,country,phoneNumber,postalCode,region,streetAddress

   >[!NOTE]
   >
   >La prima riga nell’elenco CSV è costituita da etichette predefinite che devono essere scritte esattamente come nell’esempio:
   >
   >
   >`email,givenName,familyName` - se scritto come `givenname`, ad esempio, il sistema non lo riconoscerà.
   >
   >

   ![schermata_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. Fai clic su **Avanti**. Qui puoi visualizzare in anteprima i lead per assicurarti che siano accurati.

   ![schermata_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. Fai clic su **Avanti**. Selezionare l&#39;elenco a cui si desidera che appartengano i lead. Se non desideri che appartengano a un elenco, elimina le informazioni nel campo. Per impostazione predefinita, AEM crea un nome di elenco che include la data e l’ora. Fai clic su **Importa**.

   ![schermata_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   Il nuovo lead viene visualizzato nel riquadro Lead. Se si fa clic sulla voce, tutte le informazioni immesse vengono visualizzate nel riquadro di destra. Dopo aver creato un lead, è possibile aggiungerlo a un elenco.

### Aggiunta di lead agli elenchi {#adding-leads-to-lists}

Per aggiungere lead a elenchi preesistenti:

1. In MCM, fai clic su **Lead** per visualizzare tutti i lead disponibili.

1. Selezionare i lead da aggiungere a un elenco selezionando la casella di controllo accanto al lead. Puoi aggiungere tutti i lead che desideri.

   ![schermata_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. Nel menu **Strumenti**, seleziona **Aggiungi all&#39;elenco....** Viene aperta la finestra **Aggiungi all&#39;elenco**.

   ![schermata_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. Selezionare l&#39;elenco a cui aggiungere i lead e fare clic su **OK**. I lead vengono aggiunti agli elenchi appropriati.

### Visualizzazione delle informazioni sul lead {#viewing-lead-information}

Per visualizzare le informazioni sul lead, in MCM fare clic sulla casella di controllo accanto al lead e viene visualizzato un riquadro a destra con tutte le informazioni sul lead visualizzate, inclusa l&#39;affiliazione a un elenco.

![schermata_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### Modifica dei lead esistenti {#modifying-existing-leads}

Per modificare le informazioni sui lead esistenti:

1. In MCM, fare clic su **Lead**. Dall&#39;elenco dei lead, selezionare la casella di controllo accanto al lead che si desidera modificare. Tutte le informazioni sul lead vengono visualizzate nel riquadro di destra.

   ![schermata_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >È possibile modificare un solo lead alla volta. Se è necessario modificare i lead che fanno parte dello stesso elenco, è possibile modificare l&#39;elenco.

1. Fai clic su **Modifica**. Viene visualizzata la finestra **Modifica lead**.

   ![schermata_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. Apporta le modifiche necessarie e fai clic su **Salva** per salvare le modifiche.

   >[!NOTE]
   >
   >Per modificare l’avatar del lead, passa al profilo utenti. È possibile caricare il profilo nel cloud clickstream premendo CTRL+ALT+c, facendo clic su **Carica** e selezionando il profilo.

### Eliminazione di lead esistenti {#deleting-existing-leads}

Per eliminare i lead esistenti nel MCM, selezionare la casella di controllo accanto al lead e fare clic su **Elimina**. Il lead viene rimosso dall&#39;elenco dei lead e da tutti gli elenchi associati.

>[!NOTE]
>
>Prima di eliminarlo, AEM conferma che desideri eliminare il lead esistente. Una volta eliminato, non è più possibile recuperarlo.

## Utilizzo degli elenchi {#working-with-lists}

>[!NOTE]
>
>L’Adobe non prevede di migliorare ulteriormente questa funzionalità (gestione degli elenchi).
>Si consiglia di utilizzare [Adobe Campaign e l&#39;integrazione con AEM](/help/sites-administering/campaign.md).

Gli elenchi ti consentono di organizzare i lead in gruppi. Con gli elenchi, puoi indirizzare le tue campagne di marketing a un gruppo selezionato di persone, ad esempio puoi inviare una newsletter mirata a un elenco. Gli elenchi sono visibili in MCM, nel dashboard o facendo clic su **Elenchi**. Entrambi ti forniscono il nome dell’elenco e il numero di membri.

![schermata_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

Se si fa clic su **Elenchi**, è inoltre possibile verificare se l&#39;elenco è un membro di un altro elenco e visualizzare una descrizione.

![schermata_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### Creazione di nuovi elenchi {#creating-new-lists}

1. Nel dashboard MCM, fare clic su **Nuovo elenco ...** oppure in **Elenchi**, fare clic su **Nuovo**... Viene visualizzata la finestra Crea elenco.

   ![schermata_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. Immettere un nome (obbligatorio) e, se si desidera, una descrizione e fare clic su **Salva**. L&#39;elenco verrà visualizzato nel riquadro **Elenchi**.

   ![schermata_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### Modifica di elenchi esistenti {#modifying-existing-lists}

1. In MCM, fare clic su **Elenchi**.

1. Dall&#39;elenco selezionare la casella di controllo accanto all&#39;elenco che si desidera modificare e fare clic su **Modifica**. Viene visualizzata la finestra **Modifica elenco**.

   ![schermata_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >È possibile modificare un solo elenco alla volta.

1. Apporta le modifiche necessarie e fai clic su **Salva** per salvarle.

### Eliminazione di elenchi esistenti {#deleting-existing-lists}

Per eliminare gli elenchi esistenti, in MCM selezionare la casella di controllo accanto all&#39;elenco e fare clic su **Elimina**. L’elenco viene rimosso. I lead che erano affiliati all’elenco non vengono rimossi, ma solo l’affiliazione con l’elenco viene eliminata.

>[!NOTE]
>
>Prima di eliminarli, AEM conferma che desideri eliminare gli elenchi esistenti. Una volta eliminato, non è più possibile recuperarlo.

### Unione di elenchi {#merging-lists}

È possibile unire un elenco esistente con un altro elenco. In questo caso, l&#39;elenco che si sta unendo diventa un membro dell&#39;altro elenco. Esiste ancora come entità separata e non deve essere eliminata.

È possibile unire gli elenchi se si dispone della stessa conferenza in due posizioni diverse e si desidera unirli in un elenco dei partecipanti di tutte le conferenze.

Per unire gli elenchi esistenti:

1. In MCM, fare clic su **Elenchi**.

1. Selezionare l&#39;elenco con cui si desidera unire un altro elenco selezionando la casella di controllo accanto ad esso.

1. Nel menu **Strumenti**, seleziona **Elenco di unione**.

   >[!NOTE]
   >
   >È possibile unire un solo elenco alla volta.

1. Nella finestra **Elenco unione**, selezionare l&#39;elenco con cui si desidera eseguire l&#39;unione e fare clic su **OK**.

   ![schermata_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   L&#39;elenco unito deve essere aumentato di un membro. Per verificare che l&#39;elenco sia stato unito, selezionare l&#39;elenco unito e nel menu **Strumenti** selezionare **Mostra lead**.

1. Ripetere il passaggio fino a unire tutti gli elenchi desiderati.

   ![schermata_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>La rimozione di un elenco unito dalla sua appartenenza è identica alla rimozione di un lead da un elenco. Aprire la scheda **Elenchi**, selezionare l&#39;elenco che include l&#39;elenco unito e rimuovere l&#39;appartenenza facendo clic sul cerchio rosso accanto all&#39;elenco.

### Visualizzazione dei lead negli elenchi {#viewing-leads-in-lists}

In qualsiasi momento, è possibile visualizzare i lead che appartengono a un elenco specifico sfogliando o cercando i membri.

Per visualizzare i lead negli elenchi:

1. In MCM, fare clic su **Elenchi**.

1. Selezionare la casella di controllo accanto all&#39;elenco per il quale si desidera visualizzare i membri.

1. Nel menu **Strumenti**, seleziona **Mostra lead**. In AEM vengono visualizzati i lead che sono membri di tale elenco. È possibile sfogliare l&#39;elenco o cercare membri.

   >[!NOTE]
   >
   >È inoltre possibile eliminare i lead da un elenco selezionandoli e facendo clic su **Rimuovi appartenenza**.

   ![schermata_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. Fai clic su **Chiudi** per tornare a MCM.
