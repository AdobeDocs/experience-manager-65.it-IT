---
title: Integrazione con Salesforce
seo-title: Integrazione con Salesforce
description: Scopri come integrare AEM con Salesforce.
seo-description: Scopri come integrare AEM con Salesforce.
uuid: 3d6a249d-082f-4a10-b255-96482ccd2c65
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bee7144e-4276-4e81-a3a0-5b7273af34fe
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Integrazione con Salesforce {#integrating-with-salesforce}

L’integrazione di Salesforce con AEM offre funzionalità di gestione dei lead e sfrutta le funzionalità già esistenti fornite da Salesforce. Puoi configurare AEM per la pubblicazione dei lead su Salesforce e creare componenti che accedono ai dati direttamente da Salesforce.

L’integrazione bidirezionale ed estensibile tra AEM e Salesforce consente di:

* Organizzazioni per utilizzare e aggiornare completamente i dati per migliorare l&#39;esperienza del cliente.
* Coinvolgimento dal marketing alle attività di vendita.
* Organizzazioni per trasmettere e ricevere automaticamente i dati da un archivio dati Salesforce.

Il presente documento descrive quanto segue:

* come configurare i servizi Salesforce Cloud (configurare AEM per l’integrazione con Salesforce).
* come utilizzare le informazioni di contatto/lead Salesforce in ClientContext e per la personalizzazione.
* come utilizzare il modello di flusso di lavoro Salesforce per pubblicare gli utenti AEM come lead per Salesforce.
* come creare un componente che mostri i dati da Salesforce.

## Configurazione di AEM per l’integrazione con Salesforce {#configuring-aem-to-integrate-with-salesforce}

Per configurare AEM per l’integrazione con Salesforce, devi prima configurare un’applicazione di accesso remoto in Salesforce. Quindi configuri il servizio cloud Salesforce per puntare a questa applicazione di accesso remoto.

>[!NOTE]
>
>Puoi creare un account sviluppatore gratuito in Salesforce.

Per configurare AEM per l’integrazione con Salesforce:

>[!CAUTION]
>
>Prima di continuare con la procedura, devi installare il pacchetto di integrazione API [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/featurepack/com.adobe.cq.mcm.salesforce.content#) Salesforce Force. Per ulteriori dettagli su come lavorare con i pacchetti, consultate la pagina [Come lavorare con i pacchetti](/help/sites-administering/package-manager.md#package-share) .

1. In AEM, passa a Servizi **** Cloud. In Servizi di terze parti, fai clic su **Configura ora** in **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Create una nuova configurazione, ad esempio **sviluppatore**.

   >[!NOTE]
   >
   >La nuova configurazione reindirizza a una nuova pagina: **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. Si tratta dello stesso valore che è necessario specificare nell’URL di callback durante la creazione dell’applicazione di accesso remoto in Salesforce. Questi valori devono corrispondere.

1. Accedi al tuo account di vendita (o, se non ne hai uno, creane uno all&#39;indirizzo [https://developer.force.com](https://developer.force.com).)
1. In Salesforce, passa a **Crea** > **App** per accedere alle app **** collegate (nelle versioni precedenti di Salesforce, il flusso di lavoro era **Distribuisci** > Accesso **** remoto).
1. Fate clic su **Nuovo** per collegare AEM con Salesforce.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Immettete il Nome **app** connesso, il Nome **** API e l&#39;E-mail **di** contatto. Selezionate la casella di controllo **Abilita impostazioni** OAuth e immettete l’URL **per il** callback, quindi aggiungete un ambito OAuth (ad esempio, accesso completo). L’URL di callback è simile al seguente: `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   Modificate il nome del server, il numero della porta e il nome della pagina in modo che corrisponda alla configurazione.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Fai clic su **Salva** per salvare la configurazione di Salesforce. Salesforce crea una chiave **** consumer e un segreto **** consumer, necessari per la configurazione di AEM.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Potrebbe essere necessario attendere alcuni minuti (fino a 15 minuti) per attivare l’applicazione di accesso remoto in Salesforce.

1. In AEM, andate a Servizi **** Cloud e andate alla configurazione di Salesforce creata in precedenza (ad esempio, **sviluppatore**). Fai clic su **Modifica** e immetti la chiave cliente e il segreto cliente da salesforce.com.

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | Url di accesso | Questo è l&#39;endpoint di autorizzazione di Salesforce. Il suo valore è precompilato e serve la maggior parte dei casi. |
   |---|---|
   | Chiave cliente | Immettete il valore ottenuto dalla pagina Registrazione dell&#39;applicazione di accesso remoto in salesforce.com |
   | Segreto cliente | Immettete il valore ottenuto dalla pagina Registrazione dell&#39;applicazione di accesso remoto in salesforce.com |

1. Fate clic su **Connetti a Salesforce** per connettersi. Salesforce richiede che la configurazione sia connessa a Salesforce.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   In AEM si apre una finestra di dialogo di conferma che indica che la connessione è stata completata.

1. Andate alla pagina principale del sito Web e fate clic su Proprietà **** pagina. Quindi seleziona Servizi **** Cloud e aggiungi **Salesforce** , quindi seleziona la configurazione corretta (ad esempio, **sviluppatore**).

   ![chlimage_1-75](assets/chlimage_1-75.png)

   Ora puoi usare il modello di workflow per pubblicare i lead su Salesforce e creare componenti che accedono ai dati da Salesforce.

## Esportazione di utenti AEM come lead Salesforce {#exporting-aem-users-as-salesforce-leads}

Se desiderate esportare un utente AEM come lead di Salesforce, dovete configurare il flusso di lavoro per pubblicare i lead a Salesforce.

Per esportare gli utenti AEM come lead Salesforce:

1. Andate al flusso di lavoro Salesforce `http://localhost:4502/workflow` facendo clic con il pulsante destro del mouse sul flusso di lavoro **Salesforce.com Export** e facendo clic su **Start**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Selezionate l’utente AEM che desiderate creare come lead come **payload** per questo flusso di lavoro (home -> utenti). Assicurati di selezionare il nodo del profilo dell&#39;utente, in quanto contiene informazioni come **givenName**, **familyName** e così via, mappate sui campi **FirstName** e **LastName** del lead Salesforce.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Prima di avviare questo flusso di lavoro, prima di pubblicare contenuti in Salesforce devono essere presenti alcuni campi obbligatori per un nodo lead in AEM. Questi sono **datiName**, **familyName**, **** companyName ed **email**. Per visualizzare un elenco completo della mappatura tra utente AEM e lead Salesforce, consultate Configurazione [mappatura tra utente AEM e lead Slaesforce.](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. Fai clic su **OK**. Le informazioni utente vengono esportate in salesforce.com. Potete verificarlo su salesforce.com.

   >[!NOTE]
   >
   >I registri errori mostrano se un lead viene importato. Per ulteriori informazioni, controllare il registro errori.

### Configurazione del flusso di lavoro di esportazione Salesforce.com {#configuring-the-salesforce-com-export-workflow}

Potrebbe essere necessario configurare il flusso di lavoro di esportazione Salesforce.com in modo che corrisponda alla configurazione Salesforce.com corretta o per apportare altre modifiche.

Per configurare il flusso di lavoro di esportazione Salesforce.com:

1. Accedi a `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. Aprite il passaggio Salesforce.com Export, selezionate la scheda **Argomenti** , selezionate la configurazione corretta e fate clic su **OK**. Inoltre, se desiderate che il flusso di lavoro ricrei un lead eliminato in Salesforce, selezionate la casella di controllo.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Click **Save** to save your changes.

   ![chlimage_1-79](assets/chlimage_1-79.png)

### Mappatura della configurazione tra utente AEM e lead Salesforce {#mapping-configuration-between-aem-user-and-salesforce-lead}

Per visualizzare o modificare la configurazione di mappatura corrente tra un utente AEM e un lead Salesforce, apri Gestione configurazione: `https://<hostname>:<port>/system/console/configMgr` e cerca la configurazione **della mappatura dei lead** Salesforce.

1. Aprire Gestione configurazione facendo clic su Console **** Web o andando direttamente a `https://<hostname>:<port>/system/console/configMgr.`
1. Cerca configurazione **mappatura lead** Salesforce.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Modificate le mappature, come necessario. Il mapping predefinito segue il pattern **aemUserAttribute=sfLeadAttribute**. Click **Save** to save your changes.

## Configurazione dell&#39;archivio Contesto Client Salesforce {#configuring-salesforce-client-context-store}

L&#39;archivio contestuale del client Salesforce mostra informazioni aggiuntive sull&#39;utente attualmente connesso rispetto a quanto è già disponibile in AEM. Richiama queste informazioni aggiuntive da Salesforce a seconda della connessione dell&#39;utente con Salesforce.

A questo scopo, è necessario configurare quanto segue:

1. Collegate un utente AEM con un ID Salesforce tramite il componente Salesforce Connect.
1. Aggiungi i dati del profilo Salesforce nella pagina del contesto del client per configurare le proprietà che desideri visualizzare.
1. (Facoltativo) Crea un segmento che utilizza i dati dallo store Client Context di Salesforce.

### Collegamento di un utente AEM con un ID Salesforce {#linking-an-aem-user-with-a-salesforce-id}

Per poter caricare un utente AEM con un ID Salesforce nel contesto client, devi mappare un utente AEM con un ID Salesforce. In uno scenario reale, il collegamento si basa su dati utente noti con la convalida. A scopo dimostrativo, in questa procedura viene utilizzato il componente **Salesforce Connect** .

1. Andate a un sito Web in AEM, effettuate l’accesso, trascinate e rilasciate il componente **Salesforce Connect** dalla barra laterale.

   >[!NOTE]
   >
   >Se il componente **Salesforce Connect** non è disponibile, andate alla visualizzazione **Struttura** e selezionatelo per renderlo disponibile nella visualizzazione **Modifica** .

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   Quando trascinate il componente sulla pagina, viene visualizzato **Collega a Salesforce=Disattivato**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >Questo componente è solo a scopo dimostrativo. Per gli scenari reali, ci sarebbe un altro processo per collegare/far corrispondere gli utenti ai lead.

1. Dopo aver trascinato il componente sulla pagina, apritelo per configurarlo. Seleziona la configurazione, il tipo di contatto e il lead o il contatto Salesforce, quindi fai clic su **OK**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM collega l’utente al contatto o al lead di Salesforce.

   ![chlimage_1-83](assets/chlimage_1-83.png)

### Aggiunta di dati Salesforce a ClientContext {#adding-salesforce-data-to-client-context}

Puoi caricare i dati utente da Salesforce nel ClientContext per utilizzarli per la personalizzazione:

1. Aprite il contesto client da estendere, ad esempio, navigando in tale posizione `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. Trascina il componente Dati **profilo di** Salesforce nel contesto client.

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. Fate doppio clic sul componente per aprirlo. Selezionare **Aggiungi elemento** e selezionare una proprietà dall&#39;elenco a discesa. Aggiungete tutte le proprietà desiderate e selezionate **OK**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Ora vengono visualizzate le proprietà specifiche di Salesforce di Salesforce nel contesto client.

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Creazione di un segmento utilizzando i dati dallo store Client Context di Salesforce {#building-a-segment-using-data-from-salesforce-client-context-store}

Puoi creare un segmento che utilizza i dati dall&#39;archivio di contesto client Salesforce. Per effettuare ciò:

1. Andate alla segmentazione in AEM da **Strumenti** > **Segmentazione** oppure da [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. Crea o aggiorna un segmento per includere dati da Salesforce. For more information, see [Segmentation](/help/sites-administering/campaign-segmentation.md).

## Ricerca di lead {#searching-leads}

AEM viene fornito con un componente Ricerca di esempio che esegue la ricerca dei lead in Salesforce in base ai criteri specificati. Questo componente mostra come utilizzare l’API REST di Salesforce per cercare oggetti Salesforce. Devi collegare una pagina con una configurazione Salesforce per avviare una chiamata a salesforce.com.

>[!NOTE]
>
>Questo è un componente di esempio che mostra come utilizzare l&#39;API REST di Salesforce per eseguire query sugli oggetti Salesforce. Utilizzatelo come esempio per creare componenti più complessi in base alle vostre esigenze.

Per utilizzare questo componente:

1. Passate alla pagina in cui desiderate utilizzare questa configurazione. Apri le proprietà della pagina e seleziona Servizi **cloud.** Fai clic su **Aggiungi servizi** , seleziona **Salesforce** e la configurazione appropriata, quindi fai clic su **OK**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Trascina il componente di ricerca Salesforce sulla pagina (purché sia stato abilitato. Per attivarla, passare alla modalità Progettazione e aggiungerla all&#39;area appropriata.

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. Aprite il componente Ricerca e specificate i parametri di ricerca e fate clic su **OK.**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM visualizza i lead specificati nel componente di ricerca che corrispondono ai criteri specificati.

   ![chlimage_1-87](assets/chlimage_1-87.png)

