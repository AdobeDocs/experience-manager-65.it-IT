---
title: Accesso ad Adobe Analytics e Adobe Target
seo-title: Opting Into Adobe Analytics and Adobe Target
description: Scopri come effettuare il consenso ad Adobe Analytics e Adobe Target.
seo-description: Learn how to opt into Adobe Analytics and Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 10%

---

# Accesso ad Adobe Analytics e Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM una procedura di consenso per l’integrazione con Adobe Analytics e Adobe Target. È disponibile come attività precaricata assegnata al gruppo di utenti amministratore.

Quando accedi come amministratore a questa attività (**Configurazione di Analytics e Targeting**) è disponibile dalla pagina [Inbox](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). In base alle credenziali fornite, consente di configurare e integrare questi servizi.

Per configurare l’integrazione sono disponibili le seguenti opzioni:

* Configura l’integrazione tramite l’attività .

   Questa operazione può essere eseguita immediatamente o successivamente, l’attività rimarrà nella casella in entrata fino a quando non viene eseguita alcuna azione. In entrambi i casi la configurazione può essere effettuata direttamente nell’interfaccia utente o con l’utilizzo di un `.properties` file.

* Rinuncia all’integrazione.

   Considera questa opzione se preferisci [configurare manualmente l’integrazione](/help/sites-administering/marketing-cloud.md). Vedi anche [Integrazione di AEM con Adobe Target e Adobe Analytics tramite DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* Configura la configurazione e il provisioning utilizzando uno script.

## Configurazione dell’integrazione {#configuring-the-integration}

Opt nell’integrazione con:

* Analytics per abilitare l’utilizzo delle funzionalità di tracciamento e analisi delle pagine.
* Target per abilitare l’utilizzo delle funzionalità di personalizzazione.

Per entrambe le opzioni è necessario fornire le informazioni sull’account utente e specificare le pagine che vengono tracciate.

>[!NOTE]
>
>Facoltativamente, puoi fornire informazioni sull’account Analytics e Target utilizzando un file di proprietà letto all’avvio del server. Vedi [Informazioni sull’account tramite un file di proprietà](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

Quando scegli l’integrazione, AEM esegue le seguenti attività:

* Crea le configurazioni cloud che abilitano la connessione ad Analytics e Target.
* Crea i framework che determinano i dati tracciati.
* Configura le pagine web per utilizzare questi servizi.

>[!NOTE]
>
>AT.js è la libreria client predefinita. Questa configurazione è configurata in [configurazione di target cloud services](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
>Adobe consiglia di utilizzare AT.js come libreria client.

Per effettuare il consenso dall’attività precaricata e preconfigurata:

1. Dal tuo [Casella in entrata, seleziona e **Apri** Configurare Analytics e Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item) compito.

   ![optin-01](assets/optin-01.png)

1. Per Analytics:

   1. Immetti le informazioni sull’account utente per Analytics, quindi fai clic sul corrispondente **Aggiungi** pulsante .
   1. Le credenziali appropriate sono autenticate.
   1. Quando l’account Analytics è autenticato, seleziona la suite di rapporti Analytics da utilizzare. AEM recupera le suite di rapporti di Analytics. Lo stato viene aggiornato in **Aggiunto**.

1. Per Target:

   1. Immetti le informazioni sull&#39;account utente per Target, quindi fai clic sul corrispondente **Aggiungi** pulsante .
   1. Le credenziali appropriate sono autenticate. Lo stato viene aggiornato in **Aggiunto**.

1. Seleziona **Avanti**.
1. Seleziona i siti per i quali Analytics e/o Target devono essere utilizzati.

1. Seleziona **Fine** da completare.

   >[!CAUTION]
   >
   >Dopo aver scelto di partecipare alla configurazione, devi pubblicare il sito o le pagine interessate per replicare queste modifiche all’istanza di pubblicazione.

## Rinuncia all&#39;integrazione {#opting-out-of-the-integration}

Rinuncia all’integrazione con Analytics e Target quando:

* Non eseguire l’integrazione con questi prodotti.
* Preferisci configurare le integrazioni manualmente.

   Per informazioni sulla configurazione manuale delle integrazioni, consulta [Integrazione con Adobe Analytics](/help/sites-administering/adobeanalytics.md) e [Integrazione con Adobe Target](/help/sites-administering/target.md).

Per rifiutare, devi completare l’attività precaricata:

* Dal tuo [Casella in entrata, seleziona e **Completa** Configurare Analytics e Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item) compito.

## Informazioni sull’account tramite un file di proprietà {#providing-account-information-using-a-properties-file}

Installa un file di proprietà che AEM letto all&#39;avvio del server per configurare le proprietà dell&#39;account per l&#39;integrazione con Analytics e Target. Quando utilizzi il file delle proprietà, la procedura guidata di consenso utilizza automaticamente le proprietà del file e la configurazione cloud viene creata di conseguenza.

Il file delle proprietà è un file di testo denominato marketingcloud.properties salvato nella directory di lavoro utilizzata dal processo di AEM (in genere la stessa directory del file JAR). Il file include le seguenti proprietà:

* analytics.server: URL del data center di Analytics utilizzato.
* analytics.company: Società associata al tuo account utente Analytics.
* analytics.username: Il nome utente di Analytics.
* analytics.secret: Il segreto associato al nome utente di Analytics.
* analytics.reportsuite: Nome della suite di rapporti di Analytics da utilizzare.
* target.clientcode: Il codice client associato al tuo account Target.
* target.email: L&#39;indirizzo e-mail che utilizzi per autenticare il tuo account Target.
* target.password: La password associata al tuo indirizzo e-mail.

Le proprietà e i valori sono separati con segni uguali (=). Le proprietà di Analytics hanno il prefisso `analytics`e le proprietà di Target hanno il prefisso `target`. Per configurare un servizio, fornisci valori per tutte le proprietà del servizio. Se non desideri configurare un servizio, non fornire valori per tale servizio.

Esempio `.properties` il file include i valori delle proprietà per la creazione di una configurazione cloud per Analytics:

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

La procedura seguente descrive come scegliere l’integrazione utilizzando il file delle proprietà.

1. Crea il `marketingcloud.properties` file nella directory di lavoro utilizzata dal processo di AEM (istanza autore).

   >[!NOTE]
   >
   >La directory di lavoro è solitamente la directory che contiene il jar o `license.properties` file.
   >
   >Tuttavia, può anche essere definito come percorso assoluto dalla proprietà di sistema:
   >
   >`mac.provisioning.file.container`

1. Aggiungi i valori delle proprietà in base agli account Analytics e/o Target.
1. Avviare o riavviare il server, quindi accedere utilizzando un account amministratore.
1. Apri l’attività Configura Analytics e Targeting come descritto in [Configurazione dell’integrazione](/help/sites-administering/opt-in.md#configuring-the-integration). Invece di richiedere le informazioni sul tuo account, la procedura guidata utilizza i valori della `.properties` file.

   Seleziona **Aggiungi** per il servizio appropriato, continua con la procedura guidata.

   ![optin-02](assets/optin-02.png)

## Informazioni sulle configurazioni cloud {#about-the-cloud-configurations}

Quando configuri l’integrazione con Analytics e Target, AEM crea automaticamente le configurazioni e i framework cloud richiesti. Ad esempio, la configurazione cloud di Analytics si chiama Account Analytics con provisioning .

Non è necessario modificare le configurazioni del cloud. Tuttavia, puoi configurare i framework in base alle esigenze. (Vedi [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md) e [Aggiungere un framework di Target](/help/sites-administering/target.md).)

>[!NOTE]
>
>Per impostazione predefinita, quando scegli di accedere alla procedura guidata di configurazione di Adobe Target, il targeting accurato è abilitato.
>
>Il targeting accurato significa che la configurazione del servizio cloud attende il caricamento del contesto prima di caricare il contenuto. Di conseguenza, in termini di prestazioni, un targeting accurato può creare un ritardo di alcuni millisecondi prima del caricamento del contenuto.
>
>Il targeting accurato è sempre abilitato nell’istanza di authoring. Tuttavia, nell’istanza di pubblicazione puoi scegliere di disattivare il targeting accurato a livello globale cancellando il segno di spunta accanto a Targeting accurato nella configurazione del servizio cloud (**http://localhost:4502/etc/cloudservices.html**). Puoi inoltre attivare e disattivare il targeting accurato per i singoli componenti indipendentemente dall’impostazione nella configurazione del servizio cloud.
>
>Se hai ***già*** creato i componenti di destinazione e modificato questa impostazione, le modifiche non influiscono su tali componenti. Devi apportare le modifiche direttamente a tali componenti.

>[!CAUTION]
>
>Quando scegli la configurazione di Analytics e un `reportsuite` viene selezionato, il framework è limitato alla modalità di esecuzione di pubblicazione. Questo significa che il tracciamento funziona solo sull&#39;istanza di pubblicazione.
>
>Se è necessario tenere traccia di un’istanza di authoring, anche il valore deve essere modificato in `all`.

## Configurazione dell’installazione e del provisioning tramite script {#configuring-the-setup-and-provisioning-via-script}

In qualità di amministratore, puoi attivare la configurazione e il provisioning con uno script anziché passare manualmente attraverso la procedura guidata. Puoi eseguire questa operazione:

* Invio di una richiesta POST a **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** con i parametri richiesti.

I parametri inviati dipendono dai seguenti elementi:

* Se desideri utilizzare il **marketingcloud.properties** file compilato con tutte le credenziali richieste, devi inviare i seguenti parametri:

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=percorso di una pagina AEM per allegare le configurazioni di Cloud Services create

   Ad esempio, una richiesta curl che crea configurazioni sia di Analytics che di Target e le allega alla pagina we.retail sarebbe:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* Se non desideri utilizzare il **marketingcloud.properties** file quindi sarà necessario inviare le credenziali e i parametri; ad esempio:

   * AutomaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path a una pagina AEM per allegare le configurazioni di cloud services create; è possibile definire più percorsi
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   In questo caso, la richiesta curl che crea configurazioni sia di Analytics che di Target e le allega alla pagina we-retail sarebbe:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```
