---
title: Integrazione con  Adobe Campaign Standard
seo-title: Integrazione con  Adobe Campaign Standard
description: Integrazione con  Adobe Campaign Standard.
seo-description: Integrazione con  Adobe Campaign Standard.
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
translation-type: tm+mt
source-git-commit: f951c195c581f770dcc87fdf4a89d40ee6dd9ec0
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 1%

---


# Integrazione con  Adobe Campaign Standard{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>Questa documentazione descrive come integrare AEM con  Adobe Campaign Standard, la soluzione basata su abbonamento. Se utilizzate  Adobe Campaign 6.1, consultate [Integrazione con  Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) per tali istruzioni.

 Adobe Campaign consente di gestire i contenuti e i moduli per la distribuzione tramite e-mail direttamente in Adobe Experience Manager.

Per utilizzare entrambe le soluzioni insieme allo stesso tempo, è innanzitutto necessario configurarle per collegarsi tra loro. Ciò richiede passaggi di configurazione sia in  Adobe Campaign che in Adobe Experience Manager. Questi passaggi sono descritti in dettaglio in questo documento.

Lavorare con  Adobe Campaign in AEM include la possibilità di inviare e-mail e moduli tramite  Adobe Campaign ed è descritto in [Utilizzo  Adobe Campaign](/help/sites-authoring/campaign.md).

Inoltre, i seguenti argomenti possono interessare l&#39;integrazione di AEM con [ Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html):

* [Best practice per i modelli e-mail](/help/sites-administering/best-practices-for-email-templates.md)
* [Risoluzione dei problemi relativi all&#39;integrazione  Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md)

Se state estendendo l&#39;integrazione con  Adobe Campaign, potete visualizzare le pagine seguenti:

* [Creazione di estensioni personalizzate](/help/sites-developing/extending-campaign-extensions.md)
* [Creazione di mappature di moduli personalizzate](/help/sites-developing/extending-campaign-form-mapping.md)

## Configurazione  Adobe Campaign {#configuring-adobe-campaign}

La configurazione di  Adobe Campaign implica quanto segue:

1. Configurazione dell&#39;utente **aemserver**.
1. Creazione di un account esterno dedicato.
1. Verifica dell’opzione AEMResourceTypeFilter.
1. Creazione di un modello di consegna dedicato.

>[!NOTE]
>
>Per eseguire queste operazioni, è necessario avere il ruolo **administration** in  Adobe Campaign.

### Prerequisiti {#prerequisites}

Assicuratevi di disporre già dei seguenti elementi:

* [Un’istanza di authoring AEM](/help/sites-deploying/deploy.md#getting-started)
* [Un’istanza di pubblicazione AEM](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Un&#39;istanza  Adobe Campaign](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>Le operazioni descritte nelle sezioni [Configurazione  Adobe Campaign](#configuring-adobe-campaign) e [Configurazione di Adobe Experience Manager](#configuring-adobe-experience-manager) sono necessarie per il corretto funzionamento delle funzionalità di integrazione tra AEM e  Adobe Campaign.

### Configurazione dell&#39;utente di aemserver {#configuring-the-aemserver-user}

L&#39;utente **aemserver** deve essere configurato in  Adobe Campaign. **aemserver** è un utente tecnico che verrà utilizzato per collegare il server AEM a  Adobe Campaign.

Andate a **Amministrazione** > **Utenti e sicurezza** > **Utenti**, quindi selezionate l&#39;utente **aemserver**. Fate clic su di esso per aprire le impostazioni utente.

* È necessario impostare una password per questo utente. Questa operazione non può essere eseguita tramite l&#39;interfaccia utente. Questa configurazione deve essere eseguita in REST da un amministratore tecnico.
* È possibile assegnare ruoli specifici a questo utente, ad esempio **deliveryPrepare**, che consente all&#39;utente di creare e modificare le consegne.

### Configurazione di un account Adobe Experience Manager esterno {#configuring-an-adobe-experience-manager-external-account}

È necessario configurare un account esterno che consenta di collegare  Adobe Campaign all&#39;istanza AEM.

>[!NOTE]
>
>In AEM, accertatevi di impostare la password per l’utente remoto della campagna. È necessario impostare questa password per collegarsi  Adobe Campaign con AEM. Accedete come amministratore e nella console di amministrazione utente, cercate l&#39;utente remoto della campagna e fate clic su **Imposta password**.

Per configurare un account esterno AEM:

1. Vai a **Amministrazione** > **Impostazioni applicazione** > **Account esterni**.

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. Selezionare l&#39;account esterno **aemInstance** oppure crearne uno nuovo facendo clic sul pulsante **Crea**.
1. Selezionare **Adobe Experience Manager** i nel campo **Type** e immettere i parametri di accesso utilizzati per l&#39;istanza di authoring AEM: indirizzo del server, nome account e password.

   >[!NOTE]
   >
   >Accertatevi di non aggiungere una barra **/** finale alla fine dell&#39;URL, altrimenti la connessione non funzionerà.

1. Assicurarsi che la casella di controllo **Enabled** sia selezionata, quindi fare clic su **Save** per salvare le modifiche.

### Verifica dell&#39;opzione AEMResourceTypeFilter {#verifying-the-aemresourcetypefilter-option}

L&#39;opzione **AEMResourceTypeFilter** viene utilizzata per filtrare i tipi di risorse AEM che possono essere utilizzate in  Adobe Campaign. Questo consente  Adobe Campaign di recuperare AEM contenuti progettati specificamente per essere utilizzati solo  Adobe Campaign.

Questa opzione è preconfigurata; tuttavia, se modificate questa opzione, potrebbe causare un&#39;integrazione non funzionante.

Per verificare che l&#39;opzione **AEMResourceTypeFilter** sia configurata:

1. Vai a **Amministrazione** > **Impostazioni applicazione** > **Opzioni**.
1. Nell&#39;elenco, è possibile verificare che l&#39;opzione **AEMResourceTypeFilter** sia elencata e che i percorsi siano corretti.

### Creazione di un modello di consegna AEM e-mail specifico {#creating-an-aem-specific-email-delivery-template}

Per impostazione predefinita, la funzione AEM non è abilitata nei modelli di e-mail  Adobe Campaign. Potete configurare un nuovo modello di consegna delle e-mail che verrà utilizzato per creare e-mail con AEM contenuto.

Per creare un modello di consegna AEM e-mail specifico:

1. Vai a **Risorse** > **Modelli** > **Modelli di consegna**.
1. **Per attivare la** selezione, fate clic sul segno di spunta nella barra delle azioni e selezionate il modello e-mail  **standard (e-mail)** predefinito esistente, quindi duplicatelo facendo clic sull’icona  **** Copia e facendo clic su  **Conferma**.
1. Disattivate la modalità di selezione facendo clic sul modello **x** e aprite il modello appena creato **Copy of Standard email (mail)**, quindi selezionate **Edit properties** dalla barra delle azioni del dashboard del modello.

   È possibile modificare l&#39;etichetta **Label** del modello.

1. Nella sezione delle proprietà **Content**, modificare l&#39;origine **Contenuto** in **Adobe Experience Manager**. Selezionate quindi l&#39;account esterno precedentemente creato e fate clic su **Confirm**.

   Salvare le modifiche facendo clic su **Conferma** e facendo clic su **Salva.**

   Le consegne e-mail create da questo modello avranno la funzione di contenuto AEM attivata.

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## Configurazione di Adobe Experience Manager {#configuring-adobe-experience-manager}

Per configurare AEM, è necessario effettuare le seguenti operazioni:

* Configurare la replica tra le istanze.
* Collega AEM a  Adobe Campaign.
* Configurare l&#39;esternalizzatore.

### Configurazione della replica tra AEM istanze {#configuring-replication-between-aem-instances}

Il contenuto creato dall’istanza di creazione AEM viene inviato per la prima volta all’istanza di pubblicazione. Questa istanza di pubblicazione trasferisce quindi il contenuto a  Adobe Campaign. L&#39;agente di replica deve pertanto essere configurato per eseguire la replica dall&#39;istanza di creazione AEM all&#39;istanza di pubblicazione AEM.

>[!NOTE]
>
>Se non si desidera utilizzare l&#39;URL di replica ma utilizzare l&#39;URL rivolto al pubblico, è possibile impostare l&#39; **URL pubblico** nella seguente impostazione di configurazione in OSGi (**Strumenti** > **Console Web** > **Configurazione OSGi > Integrazione AEM campagna - Configurazione**):
**URL pubblico:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

Questo passaggio è inoltre necessario per replicare alcune configurazioni dell’istanza di creazione nell’istanza di pubblicazione.

Per configurare la replica tra AEM istanze:

1. Nell&#39;istanza di authoring, selezionare **AEM logo** **Strumenti** > **Distribuzione** > **Replica** > **Agenti sull&#39;autore**, quindi fare clic su **Agente predefinito**.

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   Evitate di usare localhost (ossia una copia locale di AEM) per configurare l’integrazione con  Adobe Campaign, a meno che l’istanza di pubblicazione e di creazione non si trovi entrambe sullo stesso computer.

1. Fare clic su **Modifica**, quindi selezionare la scheda **Trasporto**.
1. Configurate l&#39;URI sostituendo **localhost** con l&#39;indirizzo IP o l&#39;indirizzo dell&#39;istanza di pubblicazione AEM.

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### Collegamento AEM a  Adobe Campaign {#connecting-aem-to-adobe-campaign}

Prima di poter utilizzare AEM e  Adobe Campaign insieme, è necessario stabilire il collegamento tra entrambe le soluzioni in modo che possano comunicare.

1. Connettiti all’istanza di authoring AEM.
1. Selezionare **Strumenti** > **Operazioni** > **Cloud** > **Cloud Services**, quindi **Configura ora** nella sezione  Adobe Campaign.

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. Per creare una nuova configurazione, immetti un **Titolo** e fai clic su **Crea** oppure scegli la configurazione esistente da collegare all&#39;istanza di Adobe Campaign .
1. Modificate la configurazione in modo che corrisponda ai parametri dell’istanza di Adobe Campaign .

   * **Nome utente**:  **aemserver**, l&#39;operatore  del pacchetto di integrazione AEM Adobe Campaign utilizzato per stabilire il collegamento tra le due soluzioni.
   * **Password**:  la password dell&#39;operatore Adobe Campaign aemserver. Potrebbe essere necessario specificare nuovamente la password per questo operatore direttamente in  Adobe Campaign.
   * **Punto** finale API:  l’URL dell’istanza Adobe Campaign.

1. Selezionare **Connetti a  Adobe Campaign** e fare clic su **OK**.

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   Dopo aver [creato il messaggio e-mail e averlo pubblicato](/help/sites-authoring/campaign.md), è necessario ripubblicare la configurazione nell&#39;istanza di pubblicazione.

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
Se la connessione non riesce, verificate quanto segue:
* È possibile che si verifichi un problema relativo al certificato quando si utilizza una connessione protetta a un&#39;istanza Adobe Campaign  (https). Sarà necessario aggiungere il  certificato di istanza Adobe Campaign al file **cacerts **del JDK.
* Inoltre, vedere [Risoluzione dei problemi relativi all&#39;integrazione AEM/ Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md).



### Configurazione dell&#39;esternalizzatore {#configuring-the-externalizer}

È necessario [configurare l&#39;esternalizzatore](/help/sites-developing/externalizer.md) in AEM nell&#39;istanza di creazione. L’esternalizzatore è un servizio OSGi che consente di trasformare un percorso di risorsa in un URL esterno e assoluto. Questo servizio fornisce una posizione centrale per configurare gli URL esterni e crearli.

Per istruzioni generali, vedere [Configurare l&#39;esternalizzatore](/help/sites-developing/externalizer.md). Per l&#39;integrazione con Adobe Campaign , accertatevi di configurare il server di pubblicazione in `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` non puntando a `localhost:4503` ma a un server raggiungibile dalla console Adobe Campaign .

Se punta a `localhost:4503` o a un altro server che  Adobe Campaign non riesce a raggiungere, le immagini non verranno visualizzate nella console Adobe Campaign .

![chlimage_1-131](assets/chlimage_1-131a.png)

