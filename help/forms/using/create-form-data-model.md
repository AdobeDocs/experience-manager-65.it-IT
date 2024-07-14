---
title: "Tutorial: creare un modello di dati modulo"
description: Scopri come configurare MySQL come origine dati, creare un modello dati del modulo (FDM), configurarlo e testare per AEM Forms.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---

# Tutorial: creare un modello di dati modulo {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Questo tutorial è un passaggio della serie [Creare il primo modulo adattivo](../../forms/using/create-your-first-adaptive-form.md). L’Adobe consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

## Informazioni sull’esercitazione {#about-the-tutorial}

Il modulo di integrazione dei dati [!DNL Forms] dell&#39;AEM consente di creare un modello di dati modulo da diverse origini dati back-end, ad esempio il profilo utente dell&#39;AEM, i servizi Web RESTful, i servizi Web basati su SOAP, i servizi OData e i database relazionali. È possibile configurare oggetti e servizi del modello dati in un modello dati del modulo e associarlo a un modulo adattivo. I campi del modulo adattivo sono associati alle proprietà dell’oggetto modello dati. I servizi consentono di precompilare il modulo adattivo e riscrivere i dati del modulo inviato nell’oggetto modello dati.

Per ulteriori informazioni sull&#39;integrazione dei dati del modulo e sul modello dati del modulo, vedere [Integrazione dati di AEM Forms](../../forms/using/data-integration.md).

Questo tutorial illustra i passaggi necessari per preparare, creare, configurare e associare un modello di dati modulo a un modulo adattivo. Al termine di questa esercitazione, sarai in grado di:

* [Configura database MySQL come origine dati](#config-database)
* [Crea modello dati modulo tramite database MySQL](#create-fdm)
* [Configura modello dati modulo](#config-fdm)
* [Test modello dati modulo](#test-fdm)

Il modello dati del modulo sarà simile al seguente:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Origini dati configurate **B.** Schemi origine dati **C.** Servizi disponibili **D.** Oggetti modello dati **E.** Servizi configurati

## Prerequisiti {#prerequisites}

Prima di iniziare, assicurati di disporre dei seguenti elementi:

* [!DNL MySQL] database con dati di esempio come indicato nella sezione Prerequisiti di [Crea il tuo primo modulo adattivo](../../forms/using/create-your-first-adaptive-form.md)
* Bundle OSGi per il driver JDBC [!DNL MySQL] come spiegato in [Bundling del driver di database JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Modulo adattivo come spiegato nel primo tutorial [Creare un modulo adattivo](/help/forms/using/create-adaptive-form.md)

## Passaggio 1: configurare il database MySQL come origine dati {#config-database}

È possibile configurare diversi tipi di origini dati per creare un modello dati del modulo. Per questa esercitazione, configurare il database MySQL configurato e popolato con dati di esempio. Per informazioni sulle altre origini dati supportate e su come configurarle, vedere [Integrazione dei dati di AEM Forms](../../forms/using/data-integration.md).

Per configurare il database [!DNL MySQL], eseguire le operazioni seguenti:

1. Installa il driver JDBC per [!DNL MySQL] il database come bundle OSGi:

   1. Scarica [!DNL MySQL] JDBC Driver OSGi Bundle da `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html`. <!-- This URL is an insecure link but using https is not possible -->
   1. Accedere all&#39;istanza dell&#39;autore [!DNL Forms] dell&#39;AEM come amministratore e passare ai bundle della console Web dell&#39;AEM. URL predefinito: [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Selezionare **[!UICONTROL Installa/Aggiorna]**. Viene visualizzata la finestra di dialogo [!UICONTROL Carica/Installa bundle].

   1. Selezionare **[!UICONTROL Scegli file]** per sfogliare e selezionare il bundle OSGi del driver JDBC [!DNL MySQL]. Selezionare **[!UICONTROL Avvia bundle]** e **[!UICONTROL Aggiorna pacchetti]**, quindi selezionare **[!UICONTROL Installa o aggiorna]**. Assicurati che il [!DNL Oracle Corporation's] driver JDBC per [!DNL MySQL] sia attivo. Il driver è installato.

1. Configurare [!DNL MySQL] il database come origine dati:

   1. Vai a AEM console Web all&#39;indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individua **la configurazione Apache Sling Connection Pooled DataSource** . Selezionare questa opzione per aprire la configurazione in modalità di modifica.
   1. Nella finestra di dialogo di configurazione, specifica i dettagli seguenti:

      * **Nome origine dati:** È possibile specificare qualsiasi nome. Specificare ad esempio **WeRetailMySQL**.
      * **Nome proprietà servizio DataSource**: specificare il nome della proprietà del servizio contenente il nome DataSource. Viene specificato durante la registrazione dell’istanza dell’origine dati come servizio OSGi. **datasource.name**.
      * **Classe driver JDBC**: specificare il nome della classe Java™ del driver JDBC. Per il database [!DNL MySQL], specificare **com.mysql.jdbc.Driver**.
      * **URI** connessione JDBC: specifica il URL di connessione del database. Per [!DNL MySQL] il database in esecuzione su porta 3306 e lo schema `weretail`, il URL è: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > Quando il [!DNL MySQL] database è protetto da un firewall, il nome host del database non è un DNS pubblico. L&#39;indirizzo *IP del database deve essere aggiunto nel file /etc/hosts* del computer host AEM.

      * **Nome utente:** Nome utente del database. È necessario per consentire al driver JDBC di stabilire una connessione con il database.
      * **Password:** Password del database. È necessario per abilitare il driver JDBC per stabilire una connessione con il database.

      >[!NOTE]
      >
      >AEM Forms non supporta l&#39;autenticazione NT per [!DNL MySQL]. Vai alla console Web all AEM indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) e ricerca &quot;Apache Sling Connection Pooled Datasource&quot;. Per la proprietà &quot;JDBC connection URI&quot;, imposta il valore di &quot;integratedSecurity&quot; su False e utilizza il nome utente e il password creati per la connessione al [!DNL MySQL] database.

      * **Test in prestito:** attiva l&#39;opzione **[!UICONTROL Test su prestito]** .
      * **Test on Return:** consente di abilitare l&#39;opzione **[!UICONTROL Test on Return.]**
      * **Query di convalida:** Specificare una query SQL SELECT per convalidare le connessioni dal pool. La query deve restituire almeno una riga. **selezionare &#42; da customerdetails**.
      * **Isolamento transazione**: impostare il valore su **READ_COMMitted**.

        Lascia altre proprietà con [valori](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predefiniti e seleziona **[!UICONTROL Salva]**.

        Viene creata una configurazione simile alla seguente.

        ![configurazione origine dati database relazionale](assets/relational-database-data-source-configuration.png)

## Passaggio 2: creare il modello dati del modulo {#create-fdm}

AEM [!DNL Forms] fornisce un&#39;interfaccia utente intuitiva per [creare un modello dati modulo](data-integration.md) da origini dati configurate. È possibile utilizzare più origini dati in un modello dati del modulo. Per questo caso d&#39;uso, è possibile utilizzare l&#39;origine dati [!DNL MySQL] configurata.

Per creare il modello dati del modulo, effettua le seguenti operazioni:

1. Nell&#39;istanza di authoring AEM, passa a **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**.
1. Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo, specifica un **nome** per il modello dati del modulo. Ad esempio, **dettagli-fatturazione-spedizione-cliente**. Seleziona **[!UICONTROL Avanti]**.
1. Nella schermata Seleziona origine dati sono elencate tutte le origini dati configurate. Selezionare l&#39;origine dati **WeRetailMySQL** e selezionare **[!UICONTROL Crea]**.

   ![selezione origine dati](assets/data-source-selection.png)

Il modello dati del modulo **customer-shipping-billing-details** è stato creato.

## Passaggio 3: configurare il modello dati del modulo {#config-fdm}

La configurazione del modello dati del modulo prevede:

* aggiunta di servizi e oggetti modello dati
* configurazione dei servizi di lettura e scrittura per gli oggetti modello dati

Per configurare il modello dati del modulo, eseguire le operazioni seguenti:

1. Nell&#39;istanza di authoring AEM, passa a **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**. URL predefinito: [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Il modello dati del modulo **customer-shipping-billing-details** creato in precedenza è elencato qui. Apri in modalità di modifica.

   L&#39;origine dati selezionata **WeRetailMySQL** è configurata nel modello dati del modulo.

   ![default-fdm](assets/default-fdm.png)

1. Espandere la struttura dell&#39;origine dati WeRailMySQL. Seleziona i seguenti oggetti e servizi del modello dati dallo schema **weretail** > **customerdetails** in modo da poter formare il modello dati:

   * **Oggetti modello dati**:

      * id
      * nome
      * shippingAddress
      * città
      * stato
      * zipcode

   * **Servizi:**

      * ottenere
      * aggiorna

   Selezionare **Aggiungi selezionati** per aggiungere gli oggetti e i servizi del modello dati selezionati al modello dati del modulo.

   ![Schema WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >I servizi predefiniti di recupero, aggiornamento e inserimento per le origini dati JDBC vengono forniti con il modello dati del modulo pronto all’uso.

1. Configurare i servizi di lettura e scrittura per l&#39;oggetto modello dati.

   1. Selezionare l&#39;oggetto modello dati **customerdetails** e selezionare **[!UICONTROL Modifica proprietà]**.
   1. Seleziona **[!UICONTROL get]** dal menu a discesa Servizio di lettura. L&#39;argomento **id**, che rappresenta la chiave primaria nell&#39;oggetto modello dati customerdetails, viene aggiunto automaticamente. Seleziona ![aem_6_3_edit](assets/aem_6_3_edit.png) e configura l&#39;argomento come segue.

      ![valore predefinito per lettura](assets/read-default.png)

   1. Analogamente, selezionare **[!UICONTROL update]** come servizio di scrittura. L&#39;oggetto **customerdetails** viene aggiunto automaticamente come argomento. L’argomento viene configurato come segue.

      ![write-default](assets/write-default.png)

      Aggiungi e configura l&#39;argomento **id** come segue.

      ![id-arg](assets/id-arg.png)

   1. Selezionare **[!UICONTROL Fine]** per salvare le proprietà dell&#39;oggetto modello dati. **[!UICONTROL Selezionare quindi Salva]** per salvare il modello dati modulo.

      I servizi **[!UICONTROL get]** e **[!UICONTROL update]** vengono aggiunti come servizi predefiniti per l&#39;oggetto modello dati.

      ![oggetto-modello-dati](assets/data-model-object.png)

1. Vai alla scheda **[!UICONTROL Servizi]** e configura i servizi **[!UICONTROL get]** e **[!UICONTROL update]**.

   1. Selezionare il servizio **[!UICONTROL get]** e selezionare **[!UICONTROL Modifica proprietà]**. Viene visualizzata la finestra di dialogo delle proprietà.
   1. Nella finestra di dialogo Modifica Proprietà, specifica quanto segue:

      * **Titolo**: specifica il titolo del servizio. Ad esempio: Recupera indirizzo di spedizione.
      * **Descrizione**: specificare la descrizione contenente il funzionamento dettagliato del servizio. Ad esempio:

        Questo servizio recupera l&#39;indirizzo di spedizione e altri dettagli del cliente dal database [!DNL MySQL]

      * **Oggetto modello di output**: selezionare uno schema contenente i dati del cliente. Ad esempio:

        schema customerdetail

      * **Array restituito**: disabilitare l&#39;opzione **Array restituito**.
      * **Argomenti**: Selezionare l&#39;argomento denominato **ID**.

      Seleziona **[!UICONTROL Fine]**. Il servizio per il recupero dei dettagli del cliente dal database MySQL è configurato.

      ![recupero indirizzo-spedizione](assets/shiiping-address-retrieval.png)

   1. Seleziona il servizio **[!UICONTROL update]** e seleziona **[!UICONTROL Modifica proprietà]**. Viene visualizzata la finestra di dialogo delle proprietà.

   1. Specificare quanto segue nella finestra di dialogo [!UICONTROL Modifica proprietà]:

      * **Titolo**: specifica il titolo del servizio. Ad esempio, Aggiorna Indirizzo di spedizione.
      * **Descrizione**: specificare la descrizione contenente il funzionamento dettagliato del servizio. Ad esempio:

        Questo servizio aggiorna l&#39;indirizzo di spedizione e i campi correlati nel database MySQL

      * **Oggetto modello di input**: selezionare uno schema contenente i dati del cliente. Ad esempio:

        schema customerdetail

      * **Tipo di output**: selezionare **BOOLEAN**.

      * **Argomenti**: selezionare il nome argomento **ID** e **customerdetails**.

      Seleziona **[!UICONTROL Fine]**. Il servizio **[!UICONTROL update]** per l&#39;aggiornamento dei dettagli del cliente nel database [!DNL MySQL] è configurato.

      ![indirizzo-spedizione-aggiornamento](assets/shiiping-address-update.png)

L’oggetto modello dati e i servizi nel modello dati del modulo sono configurati. È ora possibile verificare il modello dati del modulo.

## Passaggio 4: testare il modello di dati del modulo {#test-fdm}

È possibile eseguire il test dell&#39;oggetto modello dati e dei servizi per verificare che il modello dati del modulo sia configurato correttamente.

Per eseguire il test, eseguire le operazioni seguenti:

1. Vai alla scheda **[!UICONTROL Modello]**, seleziona l&#39;oggetto modello dati **customerdetails** e seleziona **[!UICONTROL Oggetto modello di test]**.
1. Nella finestra [!UICONTROL Modello di test/Servizio], selezionare **[!UICONTROL Leggi oggetto modello]** dal menu a discesa **[!UICONTROL Seleziona modello/Servizio]**.
1. Nella sezione **customerdetails**, specifica un valore per l&#39;argomento **id** esistente nel database [!DNL MySQL] configurato e seleziona **[!UICONTROL Test]**.

   I dettagli del cliente associati all&#39;ID specificato vengono recuperati e visualizzati nella sezione **[!UICONTROL Output]** come mostrato di seguito.

   ![test-read-model](assets/test-read-model.png)

1. Analogamente, è possibile testare l&#39;oggetto e i servizi del modello Write.

   Nell’esempio seguente, il servizio di aggiornamento aggiorna correttamente i dettagli dell’indirizzo per l’ID 7102715 nel database.

   ![test-write-model](assets/test-write-model.png)

   Ora, se verifichi di nuovo la lettura del servizio modello per 7107215 ID, questo recupera e visualizza i dettagli del cliente aggiornati come mostrato di seguito.

   ![aggiornato](assets/read-updated.png)


>[!NOTE]
>
> Puoi creare e utilizzare la configurazione Elenco SharePoint utilizzando Modello dati modulo in un modulo adattivo, per salvare dati o documenti di record generati in un elenco SharePoint. Per ulteriori informazioni, vedere [Collegare un modulo adattivo all&#39;elenco di Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#create-a-sharepoint-list-configuration).