---
title: '"Esercitazione: Crea modello dati modulo "'
seo-title: Esercitazione Crea modello dati modulo
description: Crea modello dati modulo
seo-description: Crea modello dati modulo
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 1%

---


# Tutorial: Create form data model {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Questa esercitazione è un passaggio della serie [Crea il primo modulo](../../forms/using/create-your-first-adaptive-form.md) adattivo. Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

## Informazioni sull&#39;esercitazione {#about-the-tutorial}

AEM modulo di integrazione [!DNL Forms] dei dati consente di creare un modello di dati del modulo da origini dati back-end diverse, come AEM profilo utente, servizi Web RESTful, servizi Web basati su SOAP, servizi OData e database relazionali. È possibile configurare oggetti e servizi del modello dati in un modello dati del modulo e associarlo a un modulo adattivo. I campi modulo adattivi sono associati alle proprietà dell&#39;oggetto modello dati. I servizi consentono di precompilare il modulo adattivo e di riscrivere i dati del modulo inviato all&#39;oggetto modello dati.

Per ulteriori informazioni sull&#39;integrazione dei dati del modulo e sul modello di dati del modulo, vedere [Integrazione](../../forms/using/data-integration.md)dei dati AEM Forms.

Questa esercitazione illustra i passaggi necessari per preparare, creare, configurare e associare un modello dati del modulo a un modulo adattivo. Al termine di questa esercitazione, potrete:

* [Configurare il database MySQL come origine dati](#config-database)
* [Creare un modello dati modulo utilizzando il database MySQL](#create-fdm)
* [Configurare il modello dati del modulo](#config-fdm)
* [Verifica modello dati modulo](#test-fdm)

Il modello dati del modulo sarà simile al seguente:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Origini dati configurate **B.** Schemi origine dati **C.** Servizi disponibili **D.** Oggetti del modello dati **E.** Servizi configurati

## Prerequisiti {#prerequisites}

Prima di iniziare, accertatevi di disporre dei seguenti elementi:

* [!DNL MySQL] database con dati di esempio come indicato nella sezione Prerequisiti di [Creazione del primo modulo adattivo](../../forms/using/create-your-first-adaptive-form.md)
* Pacchetto OSGi per il driver [!DNL MySQL] JDBC come spiegato in [Bundling del driver del database JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Modulo adattivo come descritto nella prima esercitazione [Creazione di un modulo adattivo](/help/forms/using/create-adaptive-form.md)

## Passaggio 1: Configurare il database MySQL come origine dati {#config-database}

È possibile configurare diversi tipi di origini dati per creare un modello dati del modulo. Per questa esercitazione, verrà configurato il database MySQL configurato e popolato con dati di esempio. Per informazioni su altre origini dati supportate e su come configurarle, vedere [Integrazione](../../forms/using/data-integration.md)dati di AEM Forms.

Per configurare il [!DNL MySQL] database, effettuate le seguenti operazioni:

1. Installare il driver JDBC per [!DNL MySQL] il database come bundle OSGi:

   1. Accedete a AEM Istanza [!DNL Forms] autore come amministratore e andate AEM bundle della console Web. L’URL predefinito è [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toccate **[!UICONTROL Installa/Aggiorna]**. Viene visualizzata una finestra di dialogo [!UICONTROL Carica/Installa pacchetti] .

   1. Toccate **[!UICONTROL Scegli file]** per sfogliare e selezionate il bundle OSGi del driver [!DNL MySQL] JDBC. Selezionate **[!UICONTROL Avvia pacchetto]** e **[!UICONTROL aggiorna pacchetti]**, quindi toccate **[!UICONTROL Installa o Aggiorna]**. Assicurarsi che il driver [!DNL Oracle Corporation's] JDBC per [!DNL MySQL] sia attivo. Il driver è installato.

1. Configura [!DNL MySQL] database come origine dati:

   1. Passate AEM console Web all’indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individua la configurazione DataSource **** in pool di connessione Apache Sling. Toccate per aprire la configurazione in modalità di modifica.
   1. Nella finestra di dialogo di configurazione, specificate i seguenti dettagli:

      * **Nome origine dati:** Potete specificare qualsiasi nome. Ad esempio, specificate **WeRetailMySQL**.
      * **Nome** proprietà del servizio DataSource: Specificare il nome della proprietà del servizio contenente il nome DataSource. Viene specificato durante la registrazione dell&#39;istanza dell&#39;origine dati come servizio OSGi. Ad esempio, **datasource.name**.
      * **Classe** driver JDBC: Specificate il nome della classe Java del driver JDBC. Per [!DNL MySQL] il database, specificate **com.mysql.jdbc.Driver**.
      * **URI** connessione JDBC: Specificate l&#39;URL di connessione del database. Per [!DNL MySQL] il database in esecuzione sulla porta 3306 e sullo schema weretail, l&#39;URL è: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nome utente:** Nome utente del database. È necessario per consentire al driver JDBC di stabilire una connessione con il database.
      * **Password:** Password del database. È necessario per consentire al driver JDBC di stabilire una connessione con il database.
      * **Test sul credito:** Abilitate l&#39;opzione **[!UICONTROL Prova in prestito]** .
      * **Test al ritorno:** Abilitate l&#39;opzione **[!UICONTROL Test on Return]** (Test su ritorno).
      * **Query di convalida:** Specificare una query SQL SELECT per convalidare le connessioni dal pool. La query deve restituire almeno una riga. Ad esempio, **selezionare * dai dettagli** del cliente.
      * **Isolamento** transazione: Impostare il valore su **READ_COMMTED**.

         Lasciate le altre proprietà con [i valori](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predefiniti e toccate **[!UICONTROL Salva]**.

         Viene creata una configurazione simile a quella riportata di seguito.

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Step 2: Create form data model {#create-fdm}

AEM [!DNL Forms] fornisce un&#39;interfaccia utente intuitiva per [creare un modello](data-integration.md) dati del modulo da origini dati configurate. È possibile utilizzare più origini dati in un modello dati del modulo. Per il nostro caso di utilizzo, utilizzeremo l&#39;origine [!DNL MySQL] dati configurata.

Per creare un modello dati modulo, effettuare le seguenti operazioni:

1. NellAEMistanza di creazione, accedi a **[!UICONTROL Forms]** > Integrazioni **[!UICONTROL dati]**.
1. Tap **[!UICONTROL Create]** > **[!UICONTROL Form Data Model]**.
1. Nella finestra di dialogo Crea modello dati modulo, specificare un **nome** per il modello dati del modulo. Ad esempio, **cliente-spedizione-fatturazione-dettagli**. Toccate **[!UICONTROL Avanti]**.
1. Nella schermata dell&#39;origine dati selezionata sono elencate tutte le origini dati configurate. Selezionate l&#39;origine dati **WeRetailMySQL** e toccate **[!UICONTROL Crea]**.

   ![data-source-selection](assets/data-source-selection.png)

Viene creato il modello di dati del modulo **per la spedizione del cliente-dettagli** di fatturazione.

## Passaggio 3: Configurare il modello dati del modulo {#config-fdm}

La configurazione del modello dati del modulo comporta:

* aggiunta di oggetti modello dati e servizi
* configurazione di servizi di lettura e scrittura per gli oggetti modello dati

Per configurare il modello dati del modulo, effettuare le seguenti operazioni:

1. NellAEMistanza di creazione, accedi a **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni]** dati. L’URL predefinito è [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Il modello di dati del modulo **per la spedizione dei clienti e la fatturazione** creato in precedenza è elencato di seguito. Aprirlo in modalità di modifica.

   L&#39;origine dati selezionata **WeRetailMySQL** è configurata nel modello dati del modulo.

   ![default-fdm](assets/default-fdm.png)

1. Espandere la struttura di origine dati WeRailMySQL. Selezionare i seguenti oggetti modello dati e servizi da **weretail** > **custom details** schema a form data model:

   * **Oggetti** del modello dati:

      * id
      * name
      * spesaIndirizzo
      * città
      * stadio
      * zipcode
   * **Servizi:**

      * get
      * aggiorna

   Toccare **Aggiungi selezionato** per aggiungere gli oggetti e i servizi del modello dati selezionati al modello dati del modulo.

   ![Schema WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >I servizi predefiniti get, update e insert per le origini dati JDBC vengono forniti out-of-the-box con il modello dati del modulo.

1. Configurare i servizi di lettura e scrittura per l&#39;oggetto modello dati.

   1. Selezionare l&#39;oggetto modello dati **custom details** e toccare **[!UICONTROL Modifica proprietà]**.
   1. Selezionate **[!UICONTROL Ottieni]** dal menu a discesa Servizio di lettura. L&#39;argomento **id** , che è la chiave primaria nell&#39;oggetto del modello di dati dei dettagli del cliente, viene aggiunto automaticamente. Toccate ![aem_6_3_edit](assets/aem_6_3_edit.png) e configurate l&#39;argomento come segue.

      ![read-default](assets/read-default.png)

   1. Analogamente, selezionate **[!UICONTROL update]** come servizio di scrittura. L&#39;oggetto **customerdetails** viene aggiunto automaticamente come argomento. L&#39;argomento è configurato come segue.

      ![write-default](assets/write-default.png)

      Aggiungete e configurate l&#39;argomento **id** come segue.

      ![id-arg](assets/id-arg.png)

   1. Toccare **[!UICONTROL Fine]** per salvare le proprietà dell&#39;oggetto modello dati. Quindi, toccare **[!UICONTROL Salva]** per salvare il modello dati del modulo.

      I servizi **[!UICONTROL get]** e **[!UICONTROL update]** vengono aggiunti come servizi predefiniti per l&#39;oggetto modello dati.

      ![data-model-object](assets/data-model-object.png)

1. Passate alla scheda **[!UICONTROL Servizi]** e configurate i servizi **[!UICONTROL get]** e **[!UICONTROL update]** .

   1. Selezionate il servizio **[!UICONTROL get]** e toccate **[!UICONTROL Modifica proprietà]**. Viene visualizzata la finestra di dialogo delle proprietà.
   1. Specificate quanto segue nella finestra di dialogo Modifica proprietà:

      * **Titolo**: Specificate il titolo del servizio. Ad esempio: Recupera indirizzo di spedizione.
      * **Descrizione**: Specificare la descrizione contenente il funzionamento dettagliato del servizio. Ad esempio:

         Questo servizio recupera l&#39;indirizzo di spedizione e altri dettagli cliente dal [!DNL MySQL] database

      * **Oggetto** modello di output: Selezionare lo schema contenente i dati del cliente. Ad esempio:

         schema dettaglio cliente

      * **Restituisce array**: Disattivate l&#39;opzione **Return array** (Restituisce array).
      * **Argomenti**: Selezionare l&#39;argomento denominato **ID**.

      Toccate **[!UICONTROL Chiudi]**. Il servizio per recuperare i dettagli del cliente dal database MySQL è configurato.

      ![ricerca dell&#39;indirizzo di spedizione](assets/shiiping-address-retrieval.png)

   1. Selezionate il servizio di **[!UICONTROL aggiornamento]** e toccate **[!UICONTROL Modifica proprietà]**. Viene visualizzata la finestra di dialogo delle proprietà.

   1. Specificate quanto segue nella finestra di dialogo [!UICONTROL Modifica proprietà] :

      * **Titolo**: Specificate il titolo del servizio. Ad esempio, Aggiorna indirizzo di spedizione.
      * **Descrizione**: Specificare la descrizione contenente il funzionamento dettagliato del servizio. Ad esempio:

         Questo servizio aggiorna l&#39;indirizzo di spedizione e i campi correlati nel database MySQL

      * **Oggetto** del modello di input: Selezionare lo schema contenente i dati del cliente. Ad esempio:

         schema dettaglio cliente

      * **Tipo** di output: Selezionare **BOOLEAN**.

      * **Argomenti**: Selezionate l’argomento denominato **ID** e i dettagli **** del cliente.
      Toccate **[!UICONTROL Chiudi]**. Il servizio di **[!UICONTROL aggiornamento]** per aggiornare i dettagli del cliente nel [!DNL MySQL] database è configurato.

      ![shiiping-address-update](assets/shiiping-address-update.png)



L&#39;oggetto e i servizi del modello dati nel modello dati del modulo sono configurati. È ora possibile verificare il modello dati del modulo.

## Step 4: Test form data model {#test-fdm}

È possibile verificare l&#39;oggetto del modello dati e i servizi per verificare che il modello dati del modulo sia configurato correttamente.

Per eseguire il test, effettuate le seguenti operazioni:

1. Fare clic sulla scheda **[!UICONTROL Modello]** , selezionare l&#39;oggetto modello dati **custom details** e toccare **[!UICONTROL Test Model Object]**.
1. Nella finestra [!UICONTROL Modello/Servizio] di prova, selezionare Oggetto **[!UICONTROL modello]** Lettura dal menu a discesa **[!UICONTROL Seleziona modello/servizio]** .
1. Nella sezione **Dettagli** cliente, specificate un valore per l&#39;argomento **id** presente nel [!DNL MySQL] database configurato e toccate **[!UICONTROL Test]**.

   I dettagli del cliente associati all&#39;ID specificato vengono recuperati e visualizzati nella sezione **[!UICONTROL Output]** come mostrato di seguito.

   ![test-read-model](assets/test-read-model.png)

1. Analogamente, è possibile verificare l&#39;oggetto e i servizi del modello di scrittura.

   Nell&#39;esempio seguente, il servizio di aggiornamento aggiorna correttamente i dettagli dell&#39;indirizzo per l&#39;ID 7102715 nel database.

   ![test-write-model](assets/test-write-model.png)

   Ora, se si esegue nuovamente il test del servizio modello di lettura per l&#39;ID 7107215, il servizio recupererà e visualizzerà i dettagli cliente aggiornati come mostrato di seguito.

   ![read-updated](assets/read-updated.png)
