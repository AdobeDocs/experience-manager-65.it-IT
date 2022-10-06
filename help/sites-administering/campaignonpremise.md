---
title: Integrazione con Adobe Campaign Classic
seo-title: Integrating with Adobe Campaign Classic
description: Scopri come integrare AEM con Adobe Campaign Classic
seo-description: Learn how to integrate AEM with Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 1%

---

# Integrazione con Adobe Campaign Classic{#integrating-with-adobe-campaign-classic}

>[!NOTE]
>
>Questa documentazione descrive come integrare AEM con Adobe Campaign Classic, la soluzione on-premise. Se utilizzi Adobe Campaign Standard, consulta [Integrazione con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) per quelle istruzioni.

Adobe Campaign ti consente di gestire i contenuti e i moduli delle e-mail di consegna direttamente in Adobe Experience Manager.

Per utilizzare entrambe le soluzioni contemporaneamente, è necessario prima configurarle per la connessione reciproca. Ciò comporta passaggi di configurazione sia in Adobe Campaign che in Adobe Experience Manager. Questi passaggi sono descritti in dettaglio in questo documento.

L’utilizzo di Adobe Campaign in AEM include la possibilità di inviare e-mail tramite Adobe Campaign ed è descritto in [Utilizzo di Adobe Campaign](/help/sites-authoring/campaign.md). Include inoltre l’uso di moduli su AEM pagine per manipolare i dati.

Inoltre, i seguenti argomenti possono essere di interesse per l&#39;integrazione di AEM con [Adobe Campaign](https://helpx.adobe.com/support/campaign/classic.html):

* [Tecniche consigliate per i modelli e-mail](/help/sites-administering/best-practices-for-email-templates.md)
* [Risoluzione dei problemi relativi all’integrazione di Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md)

Se estendi l’integrazione con Adobe Campaign, potresti voler vedere le pagine seguenti:

* [Creazione di estensioni personalizzate](/help/sites-developing/extending-campaign-extensions.md)
* [Creazione di mappature di moduli personalizzate](/help/sites-developing/extending-campaign-form-mapping.md)

## Flusso di lavoro di integrazione di AEM e Adobe Campaign {#aem-and-adobe-campaign-integration-workflow}

Questa sezione descrive un flusso di lavoro tipico tra AEM e Adobe Campaign per la creazione di campagne e la distribuzione di contenuti.

Il flusso di lavoro tipico include quanto segue ed è descritto in dettaglio:

1. Inizia a creare la tua campagna (sia in Adobe Campaign che in AEM).
1. Prima di collegare contenuti e consegne, personalizza i contenuti in AEM e crea una consegna in Adobe Campaign.
1. Collega contenuti e consegne in Adobe Campaign.

### Inizia a creare la tua campagna {#start-building-your-campaign}

Si inizia a creare una campagna in qualsiasi momento. Prima di collegare i contenuti, AEM e AC sono indipendenti Ciò significa che gli esperti di marketing possono iniziare a creare le campagne e il targeting in Adobe Campaign, mentre i creatori di contenuti stanno lavorando alla progettazione in AEM.

### Prima di collegare contenuti e consegne {#before-linking-content-and-delivery}

Prima di collegare il contenuto e creare un meccanismo di consegna, devi effettuare le seguenti operazioni:

**In AEM**

* Personalizza utilizzando i campi di personalizzazione nella sezione **Testo e personalizzazione** component

**In Adobe Campaign**

* Creare una consegna di tipo **aemContent**

### Collegamento del contenuto e impostazione della consegna {#linking-content-and-setting-delivery}

Dopo aver preparato il contenuto per il collegamento e la consegna, puoi determinare esattamente come e dove collegare il contenuto.

Tutti questi passaggi sono completati in Adobe Campaign.

1. Specifica AEM&#39;istanza da utilizzare.
1. Sincronizza il contenuto facendo clic sul pulsante Sincronizza.
1. Apri il selettore dei contenuti per scegliere il contenuto.

### Se sei nuovo a AEM {#if-you-are-new-to-aem}

Se hai poca esperienza con AEM, puoi trovare i seguenti collegamenti utili per comprendere AEM:

* [Avvio AEM](/help/sites-deploying/deploy.md)
* [Informazioni sugli agenti di replica](/help/sites-deploying/replication.md)
* [Ricerca e utilizzo dei file di registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)
* [Introduzione alla piattaforma AEM](/help/sites-deploying/platform.md)

## Configurazione di Adobe Campaign {#configuring-adobe-campaign}

La configurazione di Adobe Campaign prevede quanto segue:

1. Installazione del pacchetto di integrazione AEM in Adobe Campaign.
1. Configurazione di un account esterno.
1. Verifica che AEMResourceTypeFilter sia configurato correttamente.

Inoltre, puoi effettuare configurazioni avanzate, tra cui:

* Gestione dei blocchi di contenuto
* Gestione dei campi di personalizzazione

Vedi [Configurazioni avanzate](#advanced-configurations).

>[!NOTE]
>
>Per eseguire queste operazioni, è necessario disporre della **amministrazione** ruolo in Adobe Campaign.

### Prerequisiti {#prerequisites}

Assicurati di avere in precedenza i seguenti elementi:

* [Un’istanza di authoring AEM](/help/sites-deploying/deploy.md#getting-started)
* [Un’istanza di pubblicazione AEM](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Un&#39;istanza Adobe Campaign Classic](https://helpx.adobe.com/support/campaign/classic.html) - compreso un client e un server
* Internet Explorer 11

>[!NOTE]
>
>Se esegui una versione precedente alla build 8640 di Adobe Campaign Classic, consulta la [documentazione di aggiornamento](https://docs.campaign.adobe.com/doc/AC6.1/en/PRO_Updating_Adobe_Campaign_Upgrading.html) per ulteriori informazioni. È necessario aggiornare sia il client che il database alla stessa build.

>[!CAUTION]
>
>Operazioni descritte nel [Configurazione di Adobe Campaign](#configuring-adobe-campaign) e [Configurazione di Adobe Experience Manager](#configuring-adobe-experience-manager) Affinché le funzionalità di integrazione tra AEM e Adobe Campaign funzionino correttamente, sono necessarie delle sezioni .

### Installazione del pacchetto di integrazione AEM {#installing-the-aem-integration-package}

È necessario installare **Integrazione AEM** in Adobe Campaign. Per effettuare questo collegamento:

1. Vai all&#39;istanza Adobe Campaign con cui desideri effettuare il collegamento a AEM.
1. Seleziona *Strumenti* > *Avanzate* > *Importa pacchetto..*.

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. Fai clic su **Installare un pacchetto standard**, quindi seleziona la **Integrazione AEM** pacchetto.

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. Fai clic su **Successivo** e quindi **Inizio**.

   Questo pacchetto contiene **aemserver** che verrà utilizzato per collegare il server AEM ad Adobe Campaign.

   >[!CAUTION]
   >
   >Per impostazione predefinita, per questo operatore non è configurata alcuna zona di protezione. Per connettersi ad Adobe Campaign tramite AEM, devi selezionarne una.
   >
   >In **serverConf.xml** file, **allowUserPassword** l&#39;attributo della zona di sicurezza selezionata deve essere impostato su **true** per autorizzare AEM a collegare Adobe Campaign tramite login/password.
   >
   >Consigliamo vivamente di creare una zona di sicurezza dedicata a AEM per evitare problemi di sicurezza. Per ulteriori informazioni, consulta la sezione [Guida all’installazione](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html).

   ![chlimage_1-134](assets/chlimage_1-134a.png)

### Configurazione di un account esterno AEM {#configuring-an-aem-external-account}

Devi configurare un account esterno che ti consenta di collegare Adobe Campaign all’istanza AEM.

>[!NOTE]
>
>* Quando installi **Integrazione AEM** pacchetto, viene creato un account AEM esterno. Puoi configurare la connessione all’istanza AEM da essa oppure crearne una nuova.
>* In AEM, accertati di impostare la password per l’utente remoto della campagna. Devi impostare questa password per collegare Adobe Campaign a AEM. Accedi come amministratore e, nella console di amministrazione utente, cerca l’utente remoto della campagna e fai clic su **Imposta password**.
>


Per configurare un account AEM esterno:

1. Vai a **Amministrazione** > **Piattaforma** > **Account esterni** nodo.
1. Crea un nuovo account esterno e seleziona la **AEM** digitare.
1. Immetti i parametri di accesso per la tua istanza di authoring AEM: l&#39;indirizzo del server, nonché l&#39;ID e la password utilizzati per connettersi a questa istanza. La password dell&#39;account utente campaign-api è la stessa dell&#39;utente remoto della campagna per cui hai impostato una password in AEM.

   >[!NOTE]
   >
   >Assicurati che l&#39;indirizzo del server funzioni **not** finisce in una barra finale. Ad esempio, immetti `https://yourserver:4502` anziché `https://yourserver:4502/`

   ![chlimage_1-135](assets/chlimage_1-135a.png) ![chlimage_1-136](assets/chlimage_1-136a.png)

1. Assicurati che il **Abilitato** casella di controllo selezionata.

### Verifica dell&#39;opzione AEMResourceTypeFilter {#verifying-the-aemresourcetypefilter-option}

La **AEMResourceTypeFilter** viene utilizzata per filtrare i tipi di risorse AEM che possono essere utilizzate in Adobe Campaign. Questo consente ad Adobe Campaign di recuperare AEM contenuti appositamente progettati per essere utilizzati solo in Adobe Campaign.

Questa opzione deve essere preconfigurata; tuttavia, se modifichi questa opzione, potrebbe causare un’integrazione non funzionante.

Per verificare la **AEMResourceTypeFilter** è configurata:

1. Vai a **Piattaforma** >**Opzioni**.
1. In **AEMResourceTypeFilter** controlla che i percorsi siano corretti. Questo campo deve contenere il valore:

   **mcm/campaign/components/newsletter,mcm/campaign/components/campaign_newsletterpage,mcm/neolane/components/newsletter**

   In alcuni casi, il valore è il seguente:

   **mcm/campaign/components/newsletter**

   ![chlimage_1-137](assets/chlimage_1-137a.png)

## Configurazione di Adobe Experience Manager {#configuring-adobe-experience-manager}

Per configurare AEM, è necessario effettuare le seguenti operazioni:

* Configura la replica tra le istanze.
* Collega AEM ad Adobe Campaign tramite Cloud Services.
* Configura l&#39;esternalizzatore.

### Configurazione della replica tra istanze AEM {#configuring-replication-between-aem-instances}

Il contenuto creato dall’istanza di authoring AEM viene inviato per la prima volta all’istanza di pubblicazione. Devi pubblicare affinché le immagini nella newsletter siano disponibili nell’istanza di pubblicazione e nei destinatari della newsletter. L’agente di replica deve pertanto essere configurato per replicare dall’istanza di authoring AEM all’istanza di pubblicazione AEM.

>[!NOTE]
>
>Se non desideri utilizzare l&#39;URL di replica ma invece utilizzare l&#39;URL rivolto al pubblico, puoi impostare la **URL pubblico** nella seguente impostazione di configurazione in OSGi (**Logo AEM** >  **Strumenti** icona >  **Operazioni** > **Console web** > **Configurazione OSGi** > **Integrazione di AEM Campaign - Configurazione**):
**URL pubblico:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

Questo passaggio è necessario anche per replicare alcune configurazioni di istanze di authoring nell’istanza di pubblicazione.

Per configurare la replica tra istanze AEM:

1. Dall’istanza di authoring, seleziona **Logo AEM**> **Strumenti** icona > **Distribuzione** > **Replica** > **Agenti sull&#39;autore**, quindi fai clic su **Agente predefinito**.

   ![chlimage_1-138](assets/chlimage_1-138a.png)

   >[!NOTE]
   Evita di utilizzare localhost (ovvero una copia locale di AEM) durante la configurazione dell’integrazione con Adobe Campaign, a meno che l’istanza di pubblicazione e authoring non si trovi entrambi sullo stesso computer.

1. Tocca o fai clic su **Modifica** quindi seleziona la **Trasporti** scheda .
1. Configura l’URI sostituendo **localhost** con l’indirizzo IP o l’indirizzo dell’istanza di pubblicazione AEM.

   ![chlimage_1-139](assets/chlimage_1-139a.png)

### Collegamento AEM ad Adobe Campaign {#connecting-aem-to-adobe-campaign}

Prima di poter utilizzare AEM e Adobe Campaign insieme, è necessario stabilire il collegamento tra entrambe le soluzioni in modo che possano comunicare.

1. Collegati all’istanza di authoring AEM.
1. Seleziona **Logo AEM** > **Strumenti** icona > **Distribuzione** > **Cloud Services**, quindi **Configura ora** nella sezione Adobe Campaign .

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. Crea una nuova configurazione immettendo un **Titolo** e fai clic su **Crea** oppure scegli la configurazione esistente da collegare alla tua istanza Adobe Campaign.
1. Modifica la configurazione in modo che corrisponda ai parametri dell’istanza Adobe Campaign.

   * **Nome utente**: **aemserver**, l’operatore del pacchetto di integrazione di Adobe Campaign AEM utilizzato per stabilire il collegamento tra le due soluzioni.
   * **Password**: Password dell&#39;operatore aemserver Adobe Campaign. Potrebbe essere necessario specificare nuovamente la password per questo operatore direttamente in Adobe Campaign.
   * **Punto finale API**: URL dell’istanza di Adobe Campaign.

1. Seleziona **Connettersi ad Adobe Campaign** e fai clic su **OK**.

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   >[!NOTE]
   Dopo [crea l’e-mail e pubblicala](/help/sites-authoring/campaign.md), devi ripubblicare la configurazione nell’istanza di pubblicazione.

   ![chlimage_1-142](assets/chlimage_1-142a.png)

>[!NOTE]
Se la connessione non riesce, verifica quanto segue:
* È possibile che si verifichi un problema di certificato quando si utilizza una connessione sicura a un&#39;istanza Adobe Campaign (https). Dovrai aggiungere il certificato dell’istanza Adobe Campaign al **cactus** file del JDK dell&#39;istanza AEM.
* È necessario configurare un&#39;area di protezione per il [operatore aemserver](#connecting-aem-to-adobe-campaign) in Adobe Campaign. Inoltre, nella **serverConf.xml** file, **allowUserPassword** l&#39;attributo della zona di sicurezza deve essere impostato su **true** per autorizzare AEM connessione ad Adobe Campaign utilizzando la modalità login/password.
>
Inoltre, vedi [Risoluzione dei problemi relativi all’integrazione AEM/Adobe Campaign](/help/sites-administering/troubleshooting-campaignintegration.md).

### Configurazione dell’esternalizzatore {#configuring-the-externalizer}

Devi [configurare l&#39;esternalizzatore](/help/sites-developing/externalizer.md) in AEM sull’istanza di authoring. L’esternalizzatore è un servizio OSGi che consente di trasformare un percorso di risorsa in un URL esterno e assoluto. Questo servizio fornisce una posizione centrale per configurare gli URL esterni e generarli.

Vedi [Configurare l’esternalizzatore](/help/sites-developing/externalizer.md) per istruzioni generali. Per l’integrazione con Adobe Campaign, accertati di configurare il server di pubblicazione in `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`non indicare `localhost:4503` ma a un server raggiungibile dalla console Adobe Campaign.

Se indica `localhost:4503` Per un altro server che Adobe Campaign non è in grado di raggiungere, le immagini non verranno visualizzate nella console Adobe Campaign.

![chlimage_1-143](assets/chlimage_1-143a.png)

## Configurazioni avanzate {#advanced-configurations}

Puoi anche eseguire alcune configurazioni avanzate, ovvero:

* Gestisci campi e blocchi di personalizzazione.
* Disattiva un blocco di personalizzazione.
* Gestisci i dati dell&#39;estensione target.

### Gestione di campi e blocchi di personalizzazione {#managing-personalization-fields-and-blocks}

I campi e i blocchi disponibili per aggiungere personalizzazioni al contenuto delle e-mail in AEM sono gestiti da Adobe Campaign.

Viene fornito un elenco predefinito ma è possibile modificarlo. Puoi anche aggiungere o nascondere campi e blocchi di personalizzazione.

#### Aggiunta di un campo di personalizzazione {#adding-a-personalization-field}

Per aggiungere un nuovo campo di personalizzazione a quelli già disponibili, devi estendere Adobe Campaign **nms:seedMember** schema come segue:

>[!CAUTION]
Il campo da aggiungere deve essere già stato aggiunto tramite un’estensione dello schema destinatario (**nms:recipient**). Per ulteriori informazioni, consulta la sezione [Configurazione](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Editing_schemas.html) guida.

1. Vai a **Amministrazione** > **Configurazione** > **Schemi di dati** nella navigazione Adobe Campaign.
1. Seleziona **Nuovo**.

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. Nella finestra a comparsa, seleziona **Estendi i dati nella tabella utilizzando uno schema di estensione** e fai clic su **Successivo**.

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. Immetti i diversi parametri dello schema esteso:

   * **Schema**: seleziona la **nms:seedMember** schema. Gli altri campi della finestra vengono completati automaticamente.
   * **Namespace**: personalizzare lo spazio dei nomi dello schema esteso.

1. Modificare il codice XML dello schema per specificare il campo da aggiungere. Per ulteriori informazioni sull’estensione degli schemi in Adobe Campaign, consulta la [Guida alla configurazione](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Extending_a_schema.html).
1. Salva lo schema, quindi aggiorna la struttura del database Adobe Campaign tramite la **Strumenti** > **Avanzate** > **Aggiorna struttura del database** nella console.
1. Per salvare le modifiche, disconnettiti e riconnettiti alla console Adobe Campaign. Il nuovo campo viene ora visualizzato nell’elenco dei campi di personalizzazione disponibili in AEM.

#### Esempio {#example}

Per aggiungere una **Numero di registrazione** è necessario disporre dei seguenti elementi:

* La **nms:recipient** estensione dello schema denominata **cus:recipient** contiene:

```xml
<element desc="Recipient table (profiles)" img="nms:recipient.png" label="Recipients" labelSingular="Recipient" name="recipient">

  <attribute dataPolicy="smartCase" desc="Recipient registration number"
  label="Registration Number"
  length="50" name="registrationNumber" type="string"/>

</element>
```

La **nms:seedMember** estensione dello schema denominata **cus:seedMember** contiene:

```xml
<element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">

  <element name="custom_nms_recipient">
    <attribute name="registrationNumber"
    template="cus:recipient:recipient/@registrationNumber"/>
  </element>

</element>
```

La **Numero di registrazione** Il campo è ora parte dei campi di personalizzazione disponibili:

![chlimage_1-146](assets/chlimage_1-146.png)

#### Nascondere un campo di personalizzazione {#hiding-a-personalization-field}

Per nascondere un campo di personalizzazione tra quelli già disponibili, devi estendere l’Adobe Campaign **nms:seedMember** schema come descritto in [Aggiunta di un campo di personalizzazione](#adding-a-personalization-field) sezione . Applica i seguenti passaggi:

1. Copia il campo che desideri rimuovere dal **nms:seedMember** schema nello schema esteso (**cus:seedMember** ad esempio).
1. Aggiungi il **advanced=&quot;true&quot;** Attributo XML al campo. Non viene più visualizzato nell’elenco dei campi di personalizzazione disponibili in AEM.

   Ad esempio, per nascondere il **Nome centrale** campo **cud:seedMember** Lo schema deve contenere l&#39;elemento seguente:

   ```xml
   <element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">
   
     <element name="custom_nms_recipient">
       <attribute advanced="true" name="middleName"/>
     </element>
   
   </element>
   ```

### Disattivazione di un blocco di personalizzazione {#deactivating-a-personalization-block}

Per disattivare un blocco di personalizzazione tra quelli disponibili:

1. Vai a **Risorse** > **Campaign Management** > **Blocchi di personalizzazione** nella navigazione Adobe Campaign.
1. Seleziona il blocco di personalizzazione da disattivare in AEM.
1. Elimina **Visibile nei menu di personalizzazione** seleziona e salva le modifiche. Il blocco non viene più visualizzato nell’elenco dei blocchi di personalizzazione disponibili in Adobe Campaign.

   ![chlimage_1-147](assets/chlimage_1-147a.png)

### Gestione dei dati dell’estensione di destinazione {#managing-target-extension-data}

Puoi anche inserire i dati dell’estensione di destinazione per la personalizzazione. I dati di estensione Target (denominati anche &quot;Dati di Target&quot;) derivano, ad esempio, dall’arricchimento o dall’aggiunta di dati in una query in un flusso di lavoro della campagna. Per ulteriori informazioni, consulta la [Creazione di query](https://docs.campaign.adobe.com/doc/AC/en/PTF_Creating_queries_About_queries_in_Campaign.html) e [Arricchimento dei dati](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Enriching_data.html) sezioni.

>[!NOTE]
I dati nella destinazione sono disponibili solo se il contenuto AEM è sincronizzato con una consegna Adobe Campaign. Vedi [Sincronizzazione del contenuto creato in AEM con una consegna da Adobe Campaign](/help/sites-authoring/campaign.md#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic).

![chlimage_1-148](assets/chlimage_1-148a.png)
