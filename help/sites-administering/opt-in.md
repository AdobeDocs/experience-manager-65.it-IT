---
title: Opzione per  Adobe Analytics e  Adobe Target
seo-title: Opzione per  Adobe Analytics e  Adobe Target
description: Scoprite come scegliere  Adobe Analytics e  Adobe Target.
seo-description: Scoprite come scegliere  Adobe Analytics e  Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 0%

---


# Scelta  Adobe Analytics e  Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM una procedura di consenso per l&#39;integrazione con  Adobe Analytics e  Adobe Target. Questo è disponibile out-of-the-box, come attività precaricata assegnata al gruppo di utenti amministratore.

Quando effettuate l&#39;accesso come amministratore, l&#39;attività (**Configuring Analytics &amp; Targeting**) è disponibile dalla [Inbox](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). In base alle credenziali fornite, è utile configurare e integrare questi servizi.

Sono disponibili le seguenti opzioni per configurare l&#39;integrazione:

* Configurare l&#39;integrazione tramite l&#39;attività.

   Questa operazione può essere eseguita immediatamente o successivamente, l&#39;attività rimarrà nella Posta in arrivo fino a quando non viene eseguita alcuna azione. In entrambi i casi, la configurazione può essere effettuata direttamente nell&#39;interfaccia utente o con un file `.properties` predefinito.

* Rifiuta l&#39;integrazione.

   Considerate questa opzione se preferite [configurare manualmente l&#39;integrazione](/help/sites-administering/marketing-cloud.md). Vedere anche [Integrazione AEM con  Adobe Target e  Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* Configurare la configurazione e il provisioning utilizzando uno script.

## Configurazione dell&#39;integrazione {#configuring-the-integration}

Scegli l&#39;integrazione con:

* Analisi per consentire l’utilizzo delle funzionalità di tracciamento delle pagine e analisi.
* Target per consentire l&#39;utilizzo delle loro funzionalità di personalizzazione.

Per entrambe le opzioni è necessario fornire le informazioni sull&#39;account utente e specificare le pagine che vengono tracciate.

>[!NOTE]
>
>Facoltativamente potete fornire informazioni sull&#39;account Analytics e Target utilizzando un file delle proprietà che viene letto all&#39;avvio del server. Vedere [Informazioni sull&#39;account mediante un file delle proprietà](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

Quando decidete di partecipare all&#39;integrazione, AEM eseguire le seguenti attività:

* Crea le configurazioni cloud che abilitano la connessione ad Analytics e Target.
* Crea i framework che determinano i dati tracciati.
* Configura le pagine Web per utilizzare questi servizi.

>[!NOTE]
>
>AT.js è la libreria client predefinita. Questo è configurato nella [configurazione dei servizi cloud di destinazione](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
> Adobe consiglia di utilizzare AT.js come libreria client.

Per rifiutare l&#39;attività precaricata e non disponibile:

1. Dalla [Casella in entrata, selezionate e **Apri** l&#39;attività Configura Analytics &amp; Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item).

   ![optin-01](assets/optin-01.png)

1. Per Analytics:

   1. Immettete le informazioni sull&#39;account utente per Analytics, quindi fate clic sul pulsante **Aggiungi** corrispondente.
   1. Le credenziali appropriate sono autenticate.
   1. Quando l&#39;account Analytics è autenticato, seleziona la suite di rapporti Analytics da utilizzare. AEM recupera le suite di rapporti di Analytics. Lo stato viene aggiornato a **Aggiunto**.

1. Per Target:

   1. Immettete le informazioni sull&#39;account utente per Target, quindi fate clic sul pulsante corrispondente **Aggiungi**.
   1. Le credenziali appropriate sono autenticate. Lo stato viene aggiornato a **Aggiunto**.

1. Seleziona **Avanti**.
1. Seleziona i siti per i quali Analytics e/o Target devono essere utilizzati.

1. Selezionare **Fine** per completare.

   >[!CAUTION]
   >
   >Dopo aver scelto di partecipare alla configurazione, è necessario pubblicare il sito o le pagine interessati per replicare le modifiche nell’istanza di pubblicazione.

## Rifiuto dell&#39;integrazione {#opting-out-of-the-integration}

Rifiuta l&#39;integrazione con Analytics e Target se:

* Non desiderate effettuare l&#39;integrazione con questi prodotti.
* Preferisci configurare manualmente le integrazioni.

   Per informazioni sulla configurazione manuale delle integrazioni, consultate [Integrazione con  Adobe Analytics](/help/sites-administering/adobeanalytics.md) e [Integrazione con  Adobe Target](/help/sites-administering/target.md).

Per rifiutare, è necessario completare l&#39;attività precaricata:

* Dalla [Casella in entrata, selezionare e **Completa** l&#39;attività Configura Analytics &amp; Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item).

## Informazioni sull&#39;account mediante un file delle proprietà {#providing-account-information-using-a-properties-file}

Installa un file di proprietà che AEM letto all&#39;avvio del server per configurare le proprietà dell&#39;account per l&#39;integrazione con Analytics e Target. Quando si utilizza il file delle proprietà, la procedura guidata di consenso utilizza automaticamente le proprietà del file e la configurazione cloud viene creata di conseguenza.

Il file delle proprietà è un file di testo denominato marketingcloud.properties salvato nella directory di lavoro utilizzata dal processo di AEM (in genere la stessa directory del file JAR). Il file include le proprietà seguenti:

* analytics.server: L&#39;URL del centro dati di Analytics utilizzato.
* analytics.company: Società associata al tuo account utente Analytics.
* analytics.username: Il nome utente di Analytics.
* analytics.secret: Segreto associato al nome utente di Analytics.
* analytics.reportsuite: Nome della suite di rapporti di Analytics da utilizzare.
* target.clientcode: Il codice client associato all&#39;account Target.
* target.email: L&#39;indirizzo e-mail che utilizzate per autenticare l&#39;account Target.
* target.password: La password associata al tuo indirizzo e-mail.

Le proprietà e i valori sono separati con segni di uguale (=). Le proprietà di Analytics hanno il prefisso `analytics` e le proprietà di Target hanno il prefisso `target`. Per configurare un servizio, immetti valori per tutte le proprietà del servizio. Se non si desidera configurare un servizio, non fornire valori per tale servizio.

Il seguente file di esempio `.properties` include i valori delle proprietà per la creazione di una configurazione cloud per Analytics:

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

La procedura seguente descrive come scegliere l&#39;integrazione utilizzando il file delle proprietà.

1. Creare il file `marketingcloud.properties` nella directory di lavoro che il processo di AEM sta utilizzando (istanza di creazione).

   >[!NOTE]
   >
   >La directory di lavoro è in genere la directory che contiene il file jar o `license.properties`.
   >
   >Tuttavia, può essere definito anche come percorso assoluto dalla proprietà system:
   >
   >`mac.provisioning.file.container`

1. Aggiungete i valori delle proprietà in base agli account Analytics e/o Target.
1. Avviate o riavviate il server, quindi effettuate l&#39;accesso utilizzando un account amministratore.
1. Aprite l&#39;attività Configura analisi e targeting come descritto in [Configurazione dell&#39;integrazione](/help/sites-administering/opt-in.md#configuring-the-integration). Invece di richiedere le informazioni sull&#39;account, la procedura guidata utilizza i valori del file `.properties`.

   Selezionare **Aggiungi** per il servizio appropriato, quindi continuare con la procedura guidata.

   ![optin-02](assets/optin-02.png)

## Informazioni sulle configurazioni cloud {#about-the-cloud-configurations}

Quando configurate l&#39;integrazione con Analytics e Target, AEM crea automaticamente le configurazioni e i framework cloud richiesti. Ad esempio, la configurazione cloud di Analytics è denominata Account Analytics con provisioning.

Non è necessario modificare le configurazioni cloud. Tuttavia, potete configurare i framework in base alle esigenze. (Vedere [Mappatura dei dati dei componenti con  proprietà Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md) e [Aggiunta di un framework di destinazione](/help/sites-administering/target.md).)

>[!NOTE]
>
>Per impostazione predefinita, quando si sceglie di accedere alla  procedura guidata di configurazione di Adobe Target, viene attivato il targeting accurato.
>
>Con targeting accurato, la configurazione del servizio cloud attende che il contesto venga caricato prima di caricare il contenuto. Di conseguenza, in termini di prestazioni, un targeting accurato potrebbe creare un ritardo di alcuni millisecondi prima del caricamento del contenuto.
>
>Il targeting accurato è sempre abilitato nell&#39;istanza di creazione. Tuttavia, nell&#39;istanza di pubblicazione potete scegliere di disattivare il targeting accurato a livello globale deselezionando il segno di spunta accanto a Accurata Targeting nella configurazione del servizio cloud (**http://localhost:4502/etc/cloudservices.html**). Potete inoltre attivare e disattivare il targeting accurato per i singoli componenti, indipendentemente dall&#39;impostazione nella configurazione del servizio cloud.
>
>Se ***già*** sono stati creati componenti di destinazione e modificate questa impostazione, le modifiche apportate non influiscono su tali componenti. È necessario apportare direttamente modifiche a tali componenti.

>[!CAUTION]
>
>Quando scegliete di partecipare alla configurazione di Analytics e selezionate un `reportsuite` specifico, il framework è limitato alla modalità di esecuzione della pubblicazione. Questo significa che il tracciamento funziona solo sull’istanza di pubblicazione.
>
>Se è necessario eseguire il tracciamento anche su un’istanza di authoring, il valore deve essere cambiato in `all`.

## Configurazione dell&#39;installazione e del provisioning tramite script {#configuring-the-setup-and-provisioning-via-script}

In qualità di amministratore, potete attivare la configurazione e il provisioning con uno script anziché passare manualmente alla procedura guidata. È possibile eseguire questa operazione tramite:

* Invio di una richiesta di POST a **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** con i parametri richiesti.

I parametri inviati dipendono da quanto segue:

* Se si desidera utilizzare il file **marketingcloud.properties** compilato con tutte le credenziali richieste, è necessario inviare i seguenti parametri:

   * `automaticProvisioning`= `true`
   * `servicename`=  `analytics|target`
   * `path`=percorso di una pagina AEM per allegare le configurazioni dei servizi cloud creati

   Ad esempio, una richiesta curl che crea configurazioni Analytics e Target e le allega alla pagina we.retail sarebbe:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* Se non si desidera utilizzare il file **marketingcloud.properties**, sarà necessario inviare sia le credenziali che i parametri; ad esempio:

   * AutomaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=percorso a una pagina AEM per allegare le configurazioni dei servizi cloud creati; più percorsi possono essere definiti
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   In questo caso, la richiesta curl che crea configurazioni Analytics e Target e le collega alla pagina di vendita al dettaglio sarebbe:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

