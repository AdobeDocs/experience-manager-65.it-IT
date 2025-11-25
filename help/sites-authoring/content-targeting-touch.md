---
title: Creazione di contenuti di destinazione utilizzando la modalità di targeting
description: La modalità di targeting e il componente Target forniscono gli strumenti per la creazione di contenuti per esperienze
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: edde225d-0be7-4306-8dda-d18d46fae977
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '5284'
ht-degree: 72%

---

# Creazione di contenuti di destinazione utilizzando la modalità di targeting{#authoring-targeted-content-using-targeting-mode}

Puoi creare contenuti mirati (di destinazione) utilizzando la modalità di targeting di AEM. La modalità di targeting e il componente Target forniscono gli strumenti per la creazione di contenuti per esperienze:

* Facile riconoscimento del contenuto di destinazione presente sulla pagina. Tutti i contenuti di destinazione sono contrassegnati da un bordo tratteggiato.
* Selezione di un marchio e un’attività per visualizzare le esperienze.
* Aggiunta o rimozione di esperienze a un’attività.
* Esecuzione di test A/B e conversione dei vincitori (solo Adobe Target).
* Aggiunta di offerte a un’esperienza creando offerte o utilizzando offerte da una libreria.
* Configurazione di obiettivi e monitoraggio delle prestazioni.
* Simulazione dell’esperienza utente.
* Per ulteriori personalizzazioni, configura il componente Target.

Puoi utilizzare AEM o Adobe Target come motore di targeting (per utilizzare Adobe Target devi disporre di un account Adobe Target valido). Se utilizzi Adobe Target, devi prima di tutto configurare l’integrazione. Consulta [istruzioni per l&#39;integrazione con Adobe Target](/help/sites-administering/target.md).

![chlimage_1-8](assets/chlimage_1-8.png)

Le attività ed esperienze visualizzate in modalità Target riflettono la [console Attività](/help/sites-authoring/activitylib.md):

* Le modifiche apportate alle attività e alle esperienze utilizzando la modalità di targeting si riflettono nella console Attività.
* Le modifiche apportate nella console Attività vengono riflesse nella modalità di targeting.

>[!NOTE]
>
>Quando crei una campagna in Adobe Target, questo assegna una proprietà denominata `thirdPartyId` a ogni campagna. Quando elimini la campagna in Adobe Target, thirdPartyId non viene eliminato. Non è possibile riutilizzare `thirdPartyId` per campagne di tipo diverso (AB, XT) e non può essere rimosso manualmente. Per evitare questo problema, assegna a ciascuna campagna un nome univoco; i nomi delle campagne non possono essere riutilizzati in diversi tipi di campagna.
>
>Se utilizzi lo stesso nome nello stesso tipo di campagna, sovrascrivi la campagna esistente.
>
>Se durante la sincronizzazione si verifica l’errore “Richiesta non riuscita. `thirdPartyId` esiste già”, modifica il nome della campagna ed esegui di nuovo la sincronizzazione.

>[!NOTE]
>
>Nelle operazioni di targeting, la combinazione di branding e attività viene mantenuta a livello di utente non a livello di canale.

## Passaggio alla modalità di targeting {#switching-to-targeting-mode}

Passa alla modalità di targeting per accedere agli strumenti per la creazione di contenuti mirati.

Per passare alla modalità di targeting:

1. Apri la pagina per la quale desideri creare il targeting dei contenuti.
1. Sulla barra degli strumenti nella parte superiore della pagina, fai clic sul menu a discesa delle modalità per visualizzare i tipi di modalità disponibili.

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Fare clic su **Targeting**. Le opzioni di targeting vengono visualizzate nella parte superiore della pagina.

   ![chlimage_1-10](assets/chlimage_1-10.png)

## Aggiunta di un’attività tramite la modalità di targeting {#adding-an-activity-using-targeting-mode}

Utilizza la modalità di targeting per aggiungere un’attività a un marchio. Quando aggiungi un’attività, questa contiene l’esperienza predefinita. Dopo aver aggiunto l’attività, puoi avviare il processo di targeting dei contenuti per l’attività.

Puoi inoltre creare e gestire attività di Adobe Target da AEM con la possibilità di selezionare il motore di targeting, AEM o Adobe Target, e il tipo di attività, targeting delle esperienze o test A/B.

Inoltre, puoi gestire gli obiettivi e le metriche per tutte le attività di Adobe Target e gestire il pubblico di Adobe Target. È incluso anche il reporting delle attività di Adobe Target, tra cui la conversione dei vincitori per test A/B.

Quando aggiungi un’attività, questa viene visualizzata anche nella [console Attività](/help/sites-authoring/activitylib.md).

Per aggiungere un’attività:

1. Utilizza il menu a discesa **Marchio** per selezionare il marchio per il quale desideri creare l’attività.

   >[!NOTE]
   >
   >Adobe consiglia di [creare marchi tramite la console attività](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console).
   >
   >
   >Se crei un marchio in un altro modo, assicurati che il nodo `/campaigns/<brand>/master` esista, per evitare errori quando tenterai di creare un’attività.

1. Fai clic su + accanto al menu a discesa **Attività**.
1. Digita un nome per l’attività.

   >[!NOTE]
   >
   >Quando crei un’attività e disponi di una configurazione cloud di Adobe Target associata alla pagina o a una delle pagine principali, AEM assume automaticamente Adobe Target come motore.

1. Nel menu a comparsa del motore di **targeting**, seleziona il motore di targeting.

   * Se selezioni **ContextHub AEM**, i campi rimanenti vengono oscurati e non sono disponibili. Fai clic su **Crea**.

   * Se selezioni **Adobe Target**, puoi selezionare una configurazione (per impostazione predefinita, è quella fornita quando [hai configurato l&#39;account](/help/sites-administering/opt-in.md)) e il tipo di attività.

   * Se utilizzi l&#39;integrazione AEM/Adobe Campaign e invii contenuto di destinazione (newsletter), seleziona **Adobe Campaign**. Per ulteriori informazioni, vedere [Integrazione con Adobe Campaign](/help/sites-administering/campaign.md).

1. Nel menu Attività, seleziona **Targeting dell&#39;esperienza** o **Test A/B**.

   * Targeting dell’esperienza: gestione delle attività di Adobe Target da AEM.
   * Test A/B: creazione e gestione delle attività di test A/B in Adobe Target da AEM.

## Il processo di targeting: creazione, targeting, obiettivi e impostazioni {#the-targeting-process-create-target-and-goals-settings}

La modalità di targeting ti consente di configurare diversi aspetti di un’attività. Utilizza il seguente processo in tre fasi per creare contenuti mirati per un’attività del marchio:

1. [Creazione:](#create-authoring-the-experiences) consente di aggiungere o rimuovere le esperienze e di aggiungere le offerte a ogni esperienza.
1. [Targeting:](#diagramtargetconfiguringtheaudiences) consente di specificare il pubblico al quale è mirata ciascuna esperienza. Puoi eseguire il targeting a un pubblico specifico e, se utilizzi il test A/B decidere quale percentuale di traffico è riservata a quale esperienza.
1. [Obiettivi e impostazioni](#settingsgoalssettingsconfiguringtheactivityandsettinggoals): consente di programmare l’attività e impostare la priorità. Puoi anche definire gli obiettivi della metrica di successo.

Per avviare il processo di targeting dei contenuti di un’attività, utilizza la procedura seguente.

>[!NOTE]
>
>Per utilizzare il processo di targeting, devi essere membro del gruppo utente Autori delle attività di Target.

Per aggiungere un’attività:

1. Nel menu a discesa **Marchio**, seleziona il marchio che contiene l’attività su cui stai lavorando.
1. Nel menu a discesa **Attività**, seleziona l’attività per la quale stai creando contenuti mirati.
1. Per visualizzare i controlli che ti guidano attraverso il processo di targeting, fai clic su **Inizia targeting**.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >Per modificare l&#39;attività con cui si sta lavorando, fare clic su **Indietro**.

## Creazione: authoring di esperienze {#create-authoring-the-experiences}

Il passaggio Crea del targeting dei contenuti comporta la creazione di esperienze. Durante questo passaggio puoi creare o eliminare le esperienze nell’attività e aggiungere offerte in ogni esperienza.

### Visualizzazione delle offerte di esperienza in modalità di targeting {#seeing-experience-offers-in-targeting-mode}

Dopo aver [avviato il processo di targeting](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings), seleziona un’esperienza per visualizzare le offerte fornite per tale esperienza. Quando selezioni un’esperienza, i componenti soggetti a targeting nella pagina si modificano in modo da mostrare l’offerta per questa esperienza.

>[!CAUTION]
>
>Presta attenzione quando disattivi il targeting per un componente che è già assegnato nell’istanza di authoring. La rispettiva attività viene automaticamente eliminata anche dall’istanza di pubblicazione.

>[!NOTE]
>
>Un’offerta è il contenuto di un componente di cui è stato eseguito il targeting.

Le esperienze vengono visualizzate nel riquadro Tipi di pubblico. Nell’esempio seguente, le esperienze includono **Predefinita**, **Femmina**, **Femmina oltre 30** e **Femmina sotto 30**. Questo esempio mostra l’offerta Predefinita di un componente **Immagine** di destinazione.

![chlimage_1-12](assets/chlimage_1-12.png)

Quando è selezionata un’esperienza diversa, il componente immagine mostra l’offerta per l’esperienza.

![chlimage_1-13](assets/chlimage_1-13.png)

Quando un’esperienza è selezionata e il componente di destinazione non include un’offerta per tale esperienza, il componente visualizza la scritta **Aggiungi offerta** come sovrapposta all’offerta semitrasparente predefinita. Quando non è stata creata alcuna offerta per un’esperienza, l’offerta **Predefinita** viene visualizzata per il segmento mappato all’esperienza.

![chlimage_1-14](assets/chlimage_1-14.png)

L’esperienza predefinita viene visualizzata anche quando le proprietà del visitatore non corrispondono a nessun segmento mappato per le esperienze. Consulta [Aggiunta di esperienze utilizzando la modalità di targeting](#adding-and-removing-experiences-using-targeting-mode).

### Offerte personalizzate e offerte dalla libreria {#custom-offers-and-library-offers}

Offerte che sono [create sulla pagina](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) e vengono utilizzate per una singola esperienza sono denominate offerte personalizzate. L’immagine seguente è sovrapposta al contenuto di un’offerta personalizzata:

![chlimage_1-15](assets/chlimage_1-15.png)

Le offerte che vengono [aggiunte da una libreria di offerte](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library) sono sovrapposte con l’immagine seguente:

![chlimage_1-16](assets/chlimage_1-16.png)

Puoi salvare le offerte personalizzate in una libreria di offerte se desideri riutilizzarle. Puoi anche convertire un’offerta dalla libreria in un’offerta personalizzata se desideri modificare il contenuto di un’esperienza. Dopo la modifica, puoi salvare nuovamente l’offerta nella libreria.

### Aggiunta e rimozione di esperienze utilizzando la modalità di targeting {#adding-and-removing-experiences-using-targeting-mode}

Utilizzando il passaggio Crea del [processo di targeting](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings), puoi aggiungere e rimuovere esperienze. Inoltre, puoi duplicare un’esperienza e rinominarla.

#### Aggiunta di esperienze utilizzando la modalità di targeting {#adding-experiences-using-targeting-mode}

Per aggiungere un&#39;esperienza:

1. Per aggiungere un&#39;esperienza, fai clic su **+** **Aggiungi targeting esperienza** che viene visualizzato sotto le esperienze esistenti nel riquadro **Tipi di pubblico**.
1. Seleziona un pubblico. Per impostazione predefinita, questo nome è il nome dell’esperienza. Se necessario, puoi digitare un altro nome. Fai clic su **OK**.

#### Rimozione di esperienze utilizzando la modalità di targeting {#removing-experiences-using-targeting-mode}

Per eliminare un’esperienza:

1. Fai clic sulla freccia accanto al nome dell’esperienza.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Fai clic su **Elimina**.

#### Rinominare esperienze con la modalità di targeting {#renaming-experiences-using-targeting-mode}

Per rinominare le esperienze utilizzando la modalità di targeting:

1. Fai clic sulla freccia accanto al nome dell’esperienza.
1. Fai clic su **Rinomina esperienza** e digita il nuovo nome.
1. Fai clic in un altro punto dello schermo per salvare le modifiche.

#### Modifica dei tipi di pubblico utilizzando la modalità di targeting {#editing-audiences-using-targeting-mode}

Per modificare i tipi di pubblico utilizzando la modalità di targeting:

1. Fai clic sulla freccia accanto al nome dell’esperienza.
1. Fai clic su **Modifica pubblico** e seleziona un nuovo pubblico.
1. Fai clic su **OK**.

#### Duplicazione delle esperienze utilizzando la modalità di targeting {#duplicating-experiences-using-targeting-mode}

Per copiare le esperienze utilizzando la modalità di targeting:

1. Fai clic sulla freccia accanto al nome dell’esperienza.
1. Fai clic su **Duplica** e scegli il pubblico.
1. Se necessario, rinomina l’esperienza e fai clic su **OK**.

### Creazione di offerte utilizzando la modalità di targeting {#creating-offers-using-targeting-mode}

Esegui il targeting di un componente per creare offerte per le esperienze. I componenti di destinazione forniscono il contenuto che viene utilizzato come offerta per le esperienze.

* [Eseguire il targeting di un componente esistente](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component). Il contenuto diventa l’offerta dell’esperienza predefinita.
* [Aggiungi un componente Target](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component), quindi aggiungi il contenuto al componente.

Dopo che è stato eseguito il targeting di un componente, puoi aggiungere le offerte per ogni esperienza:

* [Aggiungi offerte personalizzate](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer).
* [Aggiungi offerte da una libreria](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

Per lavorare con le offerte sono disponibili i seguenti strumenti:

* [Aggiungere un’offerta personalizzata a una libreria di offerte](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library).
* [Convertire l’offerta dalla libreria in offerta personalizzata](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library).
* [Aprire un’offerta dalla libreria e modificare il contenuto](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer).

#### Creazione di un’offerta predefinita tramite il targeting di un componente esistente {#creating-a-default-offer-by-targeting-an-existing-component}

Esegui il targeting di un componente nella pagina per utilizzarlo come offerta per l’esperienza predefinita dell’attività. Quando si esegue il targeting di un componente, questo viene racchiuso in un componente Target e il suo contenuto diventa l’offerta per l’esperienza predefinita.

Quando si esegue il targeting di un componente, solo il componente può essere utilizzato nell’offerta. Non è possibile rimuovere il componente dall’offerta o aggiungere altri componenti all’offerta.

Esegui la seguente procedura dopo [aver avviato il processo di targeting](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings).

1. Fai clic sul componente di destinazione. Viene visualizzata la barra degli strumenti per il componente, come nell’esempio seguente.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Fai clic sull’icona Target.

   ![Destinazione](do-not-localize/chlimage_1.png)

   Il contenuto del componente è l’offerta dell’esperienza predefinita. Quando viene eseguito il targeting di un componente, il suo nodo predefinito viene replicato per ogni esperienza. Questo è necessario per modificare il nodo del contenuto corretto durante la creazione specifica dell’esperienza. Per tali esperienze non predefinite, [aggiungi un’offerta personalizzata](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) oppure [aggiungi un’offerta dalla libreria](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Creazione di un’offerta aggiungendo un componente Target {#creating-an-offer-by-adding-a-target-component}

Aggiungi un componente Target per creare l’offerta per l’esperienza predefinita. Il componente Target è un contenitore per altri componenti e viene eseguito il targeting di componenti che si trovano al suo interno. Quando utilizzi il componente Target, puoi aggiungere numerosi componenti per creare un’offerta. Inoltre, puoi usare i diversi componenti in ogni esperienza per creare le diverse offerte.

Per ulteriori informazioni su come personalizzare questo componente, consulta [Configurazione delle opzioni dei componenti Target](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options).

>[!NOTE]
>
>Le offerte create mediante la [console delle offerte](/help/sites-authoring/offerlib.md) possono anche contenere diversi componenti. Queste offerte appartengono a una libreria di offerte e possono essere utilizzate per più esperienze.

Poiché il componente Target è un contenitore, viene visualizzato come area di rilascio per altri componenti.

In modalità di targeting, il componente di destinazione ha un bordo blu e il messaggio di destinazione indica la natura del target.

![chlimage_1-19](assets/chlimage_1-19.png)

In modalità di modifica, il componente Target dispone di un’icona a forma di centro del bersaglio.

![Componente di destinazione in modalità di modifica](do-not-localize/chlimage_1-1.png)

Quando trascini componenti nel componente Target, si tratta di componenti di cui è stato eseguito il targeting.

![chlimage_1-20](assets/chlimage_1-20.png)

Quando aggiungi un componente al componente di destinazione, questo fornisce contenuti per un’esperienza specifica. Per specificare l’esperienza, selezionala prima di aggiungere i componenti.

Puoi aggiungere un componente di destinazione alla pagina in modalità Modifica o Target. Puoi aggiungere componenti al componente di destinazione solo in modalità Target. Il componente di destinazione appartiene al gruppo di componenti Personalizzazione.

In caso di modifica del contenuto con targeting, è necessario fare clic su **Inizia targeting** prima di poter procedere.

1. Trascina il componente di destinazione nella pagina in cui desideri visualizzare l’offerta.
1. Per impostazione predefinita, non è impostato alcun ID posizione. Fate clic sulla rotellina di configurazione per impostare la posizione.

   >[!NOTE]
   >
   >Se configurato dall’amministratore, potrebbe essere necessario impostare esplicitamente la posizione.
   >
   >
   >Gli amministratori possono decidere se impostare questa configurazione è necessario in **https://&lt;host>:&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet**
   >
   >
   >Per richiedere agli utenti di immettere una posizione, selezionare la casella di controllo **Forza posizione &#x200B;** Force).

1. Seleziona l’esperienza per la quale desideri creare l’offerta.
1. Crea l’offerta:

   * Per l’esperienza predefinita, trascina i componenti nell’area di rilascio desiderata e modificane le proprietà come di consueto per creare il contenuto dell’offerta.
   * Per esperienze non predefinite, [aggiungi un’offerta personalizzata](#adding-a-custom-offer) oppure [aggiungi un’offerta dalla libreria](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Aggiunta di un’offerta personalizzata {#adding-a-custom-offer}

Crea un’offerta creando il contenuto di un componente di destinazione in modalità di targeting. Quando crei un’offerta personalizzata, questa viene utilizzata come offerta per una singola esperienza.

Se decidi che l’offerta può essere utilizzata per altre esperienze, puoi creare un’offerta personalizzata e [aggiungerla alla libreria](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library). Per ulteriori informazioni sull’uso della console delle offerte per creare un’offerta riutilizzabile, consulta [Aggiunta di un’offerta a una libreria di offerte](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Seleziona l’esperienza a cui stai aggiungendo l’offerta.
1. Per visualizzare il menu del componente, fai clic sul componente di destinazione a cui stai aggiungendo l’offerta.

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Fai clic sull’icona +.

   Il contenuto dell’offerta predefinita viene utilizzato come offerta per l’esperienza corrente.

1. Fai clic sull’offerta per visualizzare il menu dell’offerta, quindi fai clic sull’icona Modifica.

   ![Menu offerte](do-not-localize/chlimage_1-2.png)

1. Modifica il contenuto del componente. 

#### Aggiunta di un’offerta da una libreria di offerte {#adding-an-offer-from-an-offer-library}

Aggiungi un’offerta dalla [libreria di offerte](/help/sites-authoring/offerlib.md) a un’esperienza. Puoi aggiungere tutte le offerte dalla libreria del marchio di cui attualmente stai eseguendo il targeting.

Non è possibile aggiungere offerte dalla libreria all’esperienza predefinita.

1. Seleziona l’esperienza a cui stai aggiungendo l’offerta.
1. Per visualizzare il menu del componente, fai clic sul componente di destinazione a cui stai aggiungendo l’offerta.

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Fai clic sull’icona della cartella.

   ![Icona della cartella](do-not-localize/chlimage_1-3.png)

1. Seleziona l’offerta dalla libreria, quindi fai clic sull’icona del segno di spunta.

   ![chlimage_1-23](assets/chlimage_1-23.png)

   Il selettore delle offerte consente di sfogliare o filtrare le offerte. Durante la navigazione o il filtraggio, puoi anche ordinare le offerte e modificarne la modalità di visualizzazione. Il numero in alto a destra indica quante offerte sono disponibili nella libreria corrente.

   * Fai clic su **Sfoglia** per passare a un&#39;altra cartella. Il pannello di navigazione si apre e puoi fare clic sulla freccia per analizzare in profondità le cartelle. Fai di nuovo clic su **Sfoglia** per chiudere il pannello di navigazione.

   ![chlimage_1-24](assets/chlimage_1-24.png)

   * Fai clic su **Filtro** per filtrare le offerte in base alle parole chiave o ai tag. Immetti le parole chiave e seleziona i tag dal menu a discesa. Fai di nuovo clic su **Filtro** per chiudere il riquadro di filtraggio.

   ![chlimage_1-25](assets/chlimage_1-25.png)

   * Puoi modificare l’ordine delle offerte toccando o facendo clic sulla freccia accanto a **Dal più recente al meno recente**. Le offerte possono essere ordinate dalla più recente alla meno recente o dalla meno recente alla più recente.

   ![chlimage_1-26](assets/chlimage_1-26.png)

   Fai clic sull&#39;icona accanto a **Visualizza come** per visualizzare le offerte come riquadri o come elenco.

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### Aggiunta di un’offerta personalizzata a una libreria {#adding-a-custom-offer-to-a-library}

Aggiungi un’offerta personalizzata alla [libreria di offerte](/help/sites-authoring/offerlib.md) quando desideri riutilizzarla come offerta per più esperienze. Puoi aggiungere offerte alla libreria del marchio corrente di cui stai eseguendo il targeting.

Per ulteriori informazioni sull’uso della console delle offerte per creare un’offerta riutilizzabile, consulta [Aggiunta di un’offerta a una libreria di offerte](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Seleziona l’esperienza per visualizzare l’offerta personalizzata.
1. Fai clic sull&#39;offerta personalizzata per visualizzare il menu dell&#39;offerta, quindi fai clic sull&#39;icona **Salva offerta nella libreria di offerte**.

   ![Salva offerta nella libreria di offerte](do-not-localize/chlimage_1-4.png)

1. Digita un nome per l’offerta e seleziona la libreria a cui stai aggiungendo l’offerta, quindi fai clic sull’icona del segno di spunta.

#### Conversione di un’offerta dalla libreria in una libreria personalizzata {#converting-a-library-offer-to-a-custom-library}

Converti un’offerta dalla libreria in un’offerta personalizzata per modificare l’offerta per l’esperienza corrente e senza modificare l’offerta nelle altre esperienze.

1. Seleziona l’esperienza per visualizzare l’offerta dalla libreria.
1. Fai clic sull’offerta dalla libreria per visualizzare il menu dell’offerta, quindi fai clic sull’icona Converti in offerta in linea.

   ![Converti in offerta in linea](do-not-localize/chlimage_1-5.png)

#### Modifica di un’offerta dalla libreria {#editing-a-library-offer}

Apri un’offerta dalla libreria da un’esperienza in modalità targeting per modificare l’offerta. Le modifiche apportate vengono visualizzate in tutte le esperienze che utilizzano l’offerta.

1. Seleziona l’esperienza per visualizzare l’offerta dalla libreria.
1. Converti l’offerta dalla libreria in offerta personalizzata/locale. Consulta [Convertire un’offerta dalla libreria in una libreria personalizzata](#converting-a-library-offer-to-a-custom-library).
1. Modifica il contenuto dell’offerta. 

1. Salvalo nuovamente nella libreria. Consulta [Aggiunta di un’offerta personalizzata a una libreria](#adding-a-custom-offer-to-a-library).

## Target: configurazione dei tipi di pubblico {#target-configuring-the-audiences}

Il passaggio di destinazione del [iprocesso di targeting](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) implica la mappatura dei tipi di pubblico con le esperienze con cui hai lavorato nel passaggio Crea. La pagina di targeting mostra il pubblico per ogni esperienza di cui stai eseguendo il targeting. Puoi specificare o modificare il pubblico per ogni esperienza. Se utilizzi Adobe Target, puoi anche creare test A/B che ti consentono di eseguire il targeting della percentuale di traffico per un pubblico per una particolare esperienza.

### Se utilizzi il targeting di AEM o Adobe Target (targeting delle esperienze) ... {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

Il pubblico viene visualizzato sul lato sinistro del diagramma di mappatura, mentre le esperienze vengono visualizzate sul lato destro.

![chlimage_1-28](assets/chlimage_1-28.png)

Definisci un pubblico utilizzando un segmento. La configurazione cloud della pagina determina i segmenti disponibili. Quando la pagina non è associata a una configurazione cloud di Adobe Target, sono disponibili segmenti AEM per la definizione dei tipi di pubblico. Quando la pagina è associata a una configurazione cloud di Adobe Target, utilizzi i segmenti target.

Per informazioni sui motori di targeting, consulta [Motore di targeting](/help/sites-authoring/personalization.md#targeting-engine).

Non utilizzare un pubblico per più di un’esperienza. Accanto a un’esperienza viene visualizzato un simbolo di avviso quando questa è mappata a un pubblico mappato a un’altra esperienza.

![Simbolo di avviso quando viene mappato a un pubblico mappato a un&#39;altra esperienza](do-not-localize/chlimage_1-6.png)

### Associazione di esperienze con un pubblico (AEM o Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

Utilizza la procedura seguente per associare un’esperienza a un pubblico quando utilizzi il targeting AEM (o il targeting dell’esperienza Adobe Target):

1. Fai clic sulla freccia a discesa accanto nella casella del pubblico mappata all’esperienza.
1. (Facoltativo) Fare clic su **Modifica** e quindi digitare una parola chiave per cercare il segmento desiderato.
1. Nell&#39;elenco dei tipi di pubblico selezionare il pubblico e fare clic su **OK**.

### Se utilizzi i test A/B (Adobe Target) ... {#if-you-are-using-a-b-testing-adobe-target}

Se hai un’attività di test A/B, i tipi di pubblico sono alla tua sinistra, la percentuale di visualizzazione di ogni esperienza al centro e le esperienze sulla destra.

Puoi modificare le percentuali purché la loro somma raggiunga il 100%. Un pubblico può essere utilizzato da più esperienze in test A/B.

![chlimage_1-29](assets/chlimage_1-29.png)

### Associazione di tipi di pubblico e percentuali di traffico con test A/B {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. Fai clic sulla casella a discesa accanto al pubblico mappato all’esperienza.
1. (Facoltativo) Tocca o fai clic su **Modifica**, quindi digita una parola chiave per la ricerca del segmento desiderato.
1. Fare clic su **OK.**
1. Immetti le percentuali per configurare il modo in cui il traffico del pubblico viene indirizzato a ogni esperienza. Il numero totale deve essere uguale a 100.
1. (Facoltativo) Modifica il nome dell’esperienza facendo clic sul menu a discesa accanto al nome dell’esperienza.

## Obiettivi e impostazioni: configurazione dell’attività e impostazione degli obiettivi {#goals-settings-configuring-the-activity-and-setting-goals}

La fase Obiettivi e impostazioni del [processo di targeting](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) comporta la configurazione del comportamento dell’attività del marchio. Specifica quando inizia e termina l’attività e la priorità dell’attività. Inoltre, tieni traccia degli obiettivi. In particolare, puoi decidere cosa misurare con le attività.

Le metriche obiettivo sono disponibili solo se utilizzi Adobe Target per il motore di targeting. Definisci almeno una metrica di obiettivo. Se hai configurato Adobe Analytics e disponi di una configurazione cloud A4T Analytics, puoi scegliere se desideri che l’origine per la generazione di rapporti sia Adobe Target o Adobe Analytics.

Le metriche dell’obiettivo vengono misurate solo per la campagna pubblicata.

Se utilizzi AEM come motore di targeting:

![chlimage_1-30](assets/chlimage_1-30.png)

Se utilizzi Adobe Target come motore di targeting:

![chlimage_1-31](assets/chlimage_1-31.png)

Se utilizzi Adobe Target come motore di targeting e disponi di A4T Analytics configurato per l’account, avrai accesso a un menu a discesa aggiuntivo **Origine per la generazione di rapporti**:

![chlimage_1-32](assets/chlimage_1-32.png)

Sono disponibili le seguenti metriche di successo (utilizzate solo per la pubblicazione):

<table>
 <tbody>
  <tr>
   <td><strong>Conversione</strong></td>
   <td><p>Percentuale di visitatori che hanno fatto clic su una qualsiasi parte dell’esperienza in fase di test. Una conversione può essere conteggiata una volta per ogni visitatore o ogni volta che un visitatore completa una conversione. La metrica di conversione è impostata su una delle seguenti opzioni:</p>
    <ul>
     <li><strong>Visualizzazione di una pagina</strong> - È possibile definire la pagina visualizzata dal pubblico selezionando <strong>URL è</strong> e quindi definendo l'URL o più URL oppure selezionando <strong>URL contiene</strong> e quindi aggiungendo un percorso o una parola chiave.</li>
     <li><strong>Visualizzazione di una mbox</strong> - È possibile definire la mbox visualizzata dal pubblico immettendo il nome della mbox. Per immettere più mbox, fai clic su <strong>Aggiungi un mbox</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Ricavo</strong></td>
   <td><p>Entrate generate dalla visita. Puoi scegliere una delle metriche di ricavo seguenti:</p>
    <ul>
     <li>Ricavo per visitatore (RPV)</li>
     <li>Valore medio dell'ordine (AOV)</li>
     <li>Vendite totali </li>
     <li>Ordini</li>
    </ul> <p>Per una qualsiasi di queste opzioni, se una mBox è stata visualizzata indica che l'obiettivo è stato raggiunto. Puoi definire la mbox o più mbox.</p> </td>
  </tr>
  <tr>
   <td><strong>Coinvolgimento</strong></td>
   <td><p>È possibile misurare tre tipi di coinvolgimento:</p>
    <ul>
     <li>Visualizzazioni pagina</li>
     <li>Punteggio personalizzato</li>
     <li>Tempo sul sito</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Inoltre, esistono impostazioni avanzate che consentono di determinare come contare le metriche di successo. Le opzioni includono il conteggio della metrica per impression o una volta per visitatore e la scelta se mantenere o meno l’utente nell’attività.

Utilizza le impostazioni avanzate per determinare cosa accade **dopo** che un utente rileva la metrica obiettivo. Nella tabella seguente sono illustrate le opzioni disponibili.

<table>
 <tbody>
  <tr>
   <td><strong>Quando un utente si imbatte questa metrica di obiettivo...</strong></td>
   <td><strong>Seleziona l’azione seguente...</strong></td>
  </tr>
  <tr>
   <td><strong>Incrementa il conteggio e mantieni utente attivo</strong></td>
   <td>Specifica la modalità di incremento del conteggio:
    <ul>
     <li>Una volta per partecipante</li>
     <li>A ogni impression, esclusi gli aggiornamenti della pagina</li>
     <li>A ogni impression</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Incrementa il conteggio, rilascia l'utente e consenti nuovo accesso</strong></td>
   <td>Seleziona l’esperienza che il visitatore vede se accede nuovamente all’attività:
    <ul>
     <li>Stessa esperienza</li>
     <li>Esperienza casuale</li>
     <li>Esperienza non vista</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Incrementa il conteggio, rilascia l'utente e impedisci nuovo accesso</strong></td>
   <td>Determina cosa vede l’utente al posto del contenuto dell’attività:
    <ul>
     <li>Stessa esperienza, senza tracciamento</li>
     <li>Contenuto predefinito o altro contenuto attività</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Consulta [Documentazione di Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=it) per ulteriori informazioni sulle metriche di successo.

### Configurazione delle impostazioni (targeting AEM) {#configuring-settings-aem-targeting}

Per configurare le impostazioni se si utilizza il targeting AEM:

1. Per specificare quando inizia l’attività, utilizza il menu a discesa **Inizio** per selezionare uno dei seguenti valori:

   * **Quando è attivata**: l’attività inizia quando viene attivata la pagina con il contenuto di destinazione.
   * **Data e ora specificata**: un tempo specifico. Quando selezioni questa opzione, fai clic sull’icona del calendario, seleziona una data e specifica l’ora in cui avviare l’attività.

1. Per specificare quando termina l’attività, utilizza il menu a discesa **Fine** per selezionare uno dei seguenti valori:

   * **Quando è disattivata**: l’attività termina quando viene disattivata la pagina con il contenuto di destinazione.
   * **Data e ora specificata**: un tempo specifico. Quando selezioni questa opzione, fai clic sull’icona del calendario, seleziona una data e specifica l’ora in cui terminare l’attività.

1. Per specificare una priorità per l’attività, utilizza il cursore per selezionare **Bassa**, **Normale** o **Alta**.

### Configurazione di obiettivi e impostazioni (Adobe Target) {#configuring-goals-settings-adobe-target}

Per configurare obiettivi e impostazioni se si utilizza Adobe Target:

1. Per specificare quando inizia l’attività, utilizza il menu a discesa **Inizio** per selezionare uno dei seguenti valori:

   * **Quando è attivata**: l’attività inizia quando viene attivata la pagina con il contenuto di destinazione.
   * **Data e ora specificata**: un tempo specifico. Quando selezioni questa opzione, fai clic sull’icona del calendario, seleziona una data e specifica l’ora in cui avviare l’attività.

1. Per specificare quando termina l’attività, utilizza il menu a discesa **Fine** per selezionare uno dei seguenti valori:

   * **Quando è disattivata**: l’attività termina quando viene disattivata la pagina con il contenuto di destinazione.
   * **Data e ora specificata**: un tempo specifico. Quando selezioni questa opzione, fai clic sull’icona del calendario, seleziona una data e specifica l’ora in cui terminare l’attività.

1. Per specificare una priorità per l’attività, utilizza il cursore per selezionare **Bassa**, **Normale** o **Alta**.
1. Se hai configurato Adobe Analytics con il tuo account Adobe Target, viene visualizzato il menu a discesa **Source** per la generazione di rapporti. Seleziona **Adobe Target** o **Adobe Analytics** come origine.

   Se si seleziona **Adobe Analytics**, seleziona la società e la suite di rapporti. Se si seleziona **Adobe Target**, non è richiesta alcuna azione.

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. Da **Obiettivo principale**, vai all’area **Metrica per obiettivo** e seleziona la metrica di successo che desideri monitorare: Conversione, Entrate, Coinvolgimento. Quindi inserisci come viene misurata la metrica (o quale azione intraprende il pubblico per indicare che un obiettivo è stato raggiunto). Vedi la definizione delle metriche dell’obiettivo nella tabella precedente e consulta la [documentazione di Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=it) sulle metriche di successo.

   Per rinominare l’obiettivo, fai clic sui tre punti nell’angolo in alto a destra e seleziona **Rinomina**.

   Per cancellare tutti i campi, fai clic sui tre punti nell’angolo superiore destro e seleziona **Cancella tutti i campi**.

   Tutte le metriche dispongono anche di impostazioni avanzate che puoi definire. Seleziona **Impostazioni avanzate** per accedervi. Vedi la definizione del conteggio delle metriche di successo nella tabella precedente e consulta la [documentazione di Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=it).

   >[!NOTE]
   >
   >Devi avere almeno un obiettivo definito.

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   >
   >Se mancano informazioni nella metrica, una linea rossa la circonda.

1. Fai clic su **Aggiungi una nuova metrica** per configurare ulteriori metriche di successo.

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   >
   >Per rimuovere altri obiettivi, tocca o fai clic sui tre punti e poi tocca o fai clic su **Elimina**. AEM richiede che tu abbia almeno un obiettivo definito.

1. Se desideri un maggiore controllo sul conteggio delle metriche di successo, fai clic su **Impostazioni avanzate** per accedere a queste impostazioni.
1. Fai clic su **Salva**.

Dopo la configurazione, puoi [visualizzare le prestazioni delle attività](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test) che utilizzano Adobe Target (targeting dell’esperienza o del test A/B). Inoltre, con il targeting di test A/B, puoi [convertire i vincitori.](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test)

## Simulazione di un’esperienza {#simulating-an-experience}

Simula l’esperienza di un visitatore per verificare che il contenuto della pagina sia visualizzato come previsto in base alla progettazione del contenuto di destinazione. Durante la simulazione, carica profili utente diversi e visualizza il contenuto di destinazione per tale utente.

I seguenti criteri determinano il contenuto visualizzato durante la simulazione dell’esperienza di un visitatore:

* I dati nell’archivio della sessione dell’utente (tramite Context Hub).
* Le [Attività che sono in corso](/help/sites-authoring/activitylib.md).
* Le [regole che definiscono i segmenti](/help/sites-administering/campaign-segmentation.md).
* Il contenuto delle esperienze nei componenti Target.
* La [configurazione del motore di targeting](/help/sites-authoring/activitylib.md).

Se durante il caricamento di un profilo nella pagina viene visualizzato contenuto imprevisto, controlla la configurazione di ogni elemento dell’elenco.

>[!NOTE]
>
>Se utilizzi i test A/B, durante la simulazione le esperienze vengono visualizzate in base alla percentuale di traffico. Questa funzione è controllata da Adobe Target e può causare risultati imprevisti per gli autori. L&#39;attività _author è sincronizzata con impostazioni specifiche che consentono la rivalutazione durante la simulazione. Gli autori potrebbero dover eseguire un aggiornamento per visualizzare le altre esperienze in base alle impostazioni del traffico.

Per simulare l’esperienza del visitatore, utilizza i seguenti strumenti:

* Attività di simulazione in modalità Targeting: la pagina visualizza le offerte per l’utente attualmente selezionate in Context Hub. Puoi modificare le offerte con targeting per l’utente.
* Modalità Anteprima: utilizza Context Hub per selezionare gli utenti e le posizioni che soddisfano i criteri dei segmenti su cui si basano le esperienze. Quando le selezioni di ContextHub cambiano, il contenuto di destinazione cambia di conseguenza.

1. Per passare alla modalità Anteprima, sulla barra degli strumenti fare clic su **Anteprima**.
1. Sulla barra degli strumenti, fai clic sull’icona Context Hub.

   ![Hub contesto](do-not-localize/chlimage_1-7.png)

1. Utilizza Context Hub per modificare le proprietà di contesto. Ad esempio, fare clic sulla proprietà Persona per selezionare un altro utente.

   ![chlimage_1-36](assets/chlimage_1-36.png)

   La pagina cambia per mostrare il contenuto di destinazione per il contesto corrente.

1. Per modificare le offerte visualizzate, passa alla modalità Targeting. Con l’attività di simulazione selezionata, modifica le offerte per il contesto configurato in modalità Anteprima.

## Configurazione delle opzioni dei componenti di destinazione {#configuring-target-component-options}

Puoi personalizzare il componente Target accedendo alle opzioni del componente in uno dei due modi seguenti:

1. Dopo aver eseguito il targeting del componente, nel componente Target, fai clic sul componente e quindi sull’icona delle impostazioni (cog).

   ![Menu del componente di destinazione](do-not-localize/chlimage_1-8.png)

   AEM mostra la finestra delle opzioni del componente Target.

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. In alternativa, per accedere a queste impostazioni in modalità a tutto schermo, nella finestra delle opzioni del componente Target, fai clic sull’icona a tutto schermo.

   ![Finestra delle opzioni del componente di destinazione](do-not-localize/chlimage_1-9.png)

   AEM mostra la finestra delle opzioni del componente Target a schermo intero.

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Configura le impostazioni del componente Target come descritto nelle tabelle seguenti.

<table>
 <tbody>
  <tr>
   <td><strong>Opzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Dove si trova</strong></td>
   <td><p>La posizione è una stringa che assegna un nome alla posizione del contenuto di destinazione e collega le offerte con i punti (o posizioni o componenti) della pagina in cui tali offerte devono essere posizionate.</p> <p>Questo campo è un valore generico.</p> <p>Se inserisci un’offerta in un componente, l’offerta ricorda l’ID della posizione. Quando la pagina viene eseguita, il motore valuta i segmenti dell’utente e, in base a questo, risolve le esperienze delle campagne attive che devono essere visualizzate. Quindi, controlla gli ID posizione sulla pagina e tenta di far corrispondere le offerte con tali ID posizione.</p> </td>
  </tr>
  <tr>
   <td><strong>Motore</strong></td>
   <td>Seleziona tra <strong>Regole lato client (senza tracciamento), Adobe Target, ContextHub, </strong>e<strong> Adobe Campaign </strong>a seconda del motore che desideri utilizzare.</td>
  </tr>
 </tbody>
</table>

Se hai selezionato Adobe Target come motore:

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>Opzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Targeting preciso</strong></td>
   <td><p>L’abilitazione di un targeting accurato indica al componente di attendere che i dati contestuali o del context hub siano disponibili prima di inviare la richiesta ad Adobe Target. Può aumentare il tempo di caricamento. Per l’authoring, il targeting accurato è sempre abilitato.</p> <p>Se selezioni la casella di controllo <strong>Targeting accurato</strong>, la mbox esegue prima un <code>mboxDefine</code> e poi un <code>mboxUpdate</code>, dando luogo a una richiesta Ajax una volta che i dati sono disponibili.</p> <p>Se non selezioni la casella di controllo <strong>Targeting accurato</strong>, la mbox esegue <code>mboxCreate</code> generando immediatamente una richiesta sincrona (in questo caso, non tutti i dati contestuali potrebbero essere ancora disponibili).</p> <p><strong>Nota:</strong> l'abilitazione o la disabilitazione del targeting accurato su un componente specifico non influisce sulle impostazioni impostate a livello globale. Puoi sempre ignorare le impostazioni globali selezionando Targeting accurato nel componente.</p> </td>
  </tr>
  <tr>
   <td><strong>Includi segmenti risolti</strong></td>
   <td><p>La selezione di questa casella di controllo include tutti i segmenti risolti nella chiamata mbox ed eventuali parametri configurati nella pagina e nel framework.</p> <p>Questo funziona solo in situazioni con API XML dove stai sincronizzando i segmenti AEM. Se disponi di segmenti in AEM che non sono gestiti da Adobe Target (come i segmenti di script), questa opzione consente di risolvere il segmento in AEM e di inviare ad Adobe Target le informazioni che indicano che il segmento è attivo.</p> </td>
  </tr>
  <tr>
   <td><strong>Parametri di contesto ereditati</strong></td>
   <td>Elenca i parametri di contesto ereditati dal framework Adobe Target, se presenti, associati alla pagina selezionata.</td>
  </tr>
  <tr>
   <td><strong>Parametri di contesto</strong></td>
   <td>Fai clic su <strong>Aggiungi campo</strong> per configurare parametri di contesto aggiuntivi (come quelli disponibili nel framework di Target). I parametri di contesto aggiunti al componente si applicano <i>solo</i> al componente e non a un altro componente, come accadrebbe se si aggiungessero parametri di contesto direttamente al framework.</td>
  </tr>
  <tr>
   <td><strong>Parametri statici</strong></td>
   <td>Fai clic su <strong>Aggiungi campo</strong> per configurare parametri statici aggiuntivi (come quelli disponibili nel framework di Target). I parametri statici aggiunti al componente si applicano <i>solo</i> al componente e non a un altro componente, come accadrebbe se si aggiungessero parametri statici direttamente al framework. I parametri statici non sono contenuti nel contesto (contesto cliente del Content Hub).</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Quando selezioni un componente e lo rendi utilizzabile come destinazione, AEM inoltre sostituisce il componente e inserisce un componente Adobe Target. (Il componente Adobe Target viene utilizzato non solo quando lo aggiungi manualmente alla pagina, ma anche quando esegui il targeting di un componente esistente).

Se si seleziona ClientContext (lato client) come motore:

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>Opzione</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><strong>Opzioni per lato client: strategia</strong></td>
   <td><p>Selezionare una delle opzioni seguenti:</p>
    <ul>
     <li><strong>Primo</strong>: l'esperienza più in alto nell'elenco, come ordinato nella campagna.</li>
     <li><strong>Casuale</strong>: è utilizzata qualsiasi esperienza.</li>
     <li><strong>Punteggio clickstream</strong>: vengono utilizzati i tag e gli hit di tag correlati tracciati nel contesto client. Vengono confrontate le percentuali di hit per i tag definiti nella pagina teaser.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Seleziona **Adobe Campaign** come motore se stai integrando AEM con Adobe Campaign. Per ulteriori informazioni, vedere [Integrazione di AEM con Adobe Campaign](/help/sites-administering/campaign.md).

Seleziona **ContextHub** come motore se stai utilizzando ContextHub per il targeting. Vedere [Configurazione di ContextHub.](/help/sites-developing/ch-configuring.md)
