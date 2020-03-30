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
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Tutorial: Create form data model {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Questa esercitazione è un passaggio della serie [Crea il primo modulo](../../forms/using/create-your-first-adaptive-form.md) adattivo. Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

## Informazioni sull&#39;esercitazione {#about-the-tutorial}

Il modulo di integrazione dei dati di AEM Forms consente di creare un modello di dati del modulo da origini dati back-end diverse, quali profilo utente AEM, servizi Web RESTful, servizi Web basati su SOAP, servizi OData e database relazionali. È possibile configurare oggetti e servizi del modello dati in un modello dati del modulo e associarlo a un modulo adattivo. I campi modulo adattivi sono associati alle proprietà dell&#39;oggetto modello dati. I servizi consentono di precompilare il modulo adattivo e di riscrivere i dati del modulo inviato all&#39;oggetto modello dati.

Per ulteriori informazioni sull&#39;integrazione dei dati del modulo e sul modello di dati del modulo, consultate Integrazione [dei dati di](../../forms/using/data-integration.md)AEM Forms.

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

* Database MySQL con dati di esempio come indicato nella sezione Prerequisiti di [Creare il primo modulo adattivo](../../forms/using/create-your-first-adaptive-form.md)
* Pacchetto OSGi per il driver JDBC MySQL come spiegato in [Bundling del driver del database JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Modulo adattivo come descritto nella prima esercitazione [Creazione di un modulo adattivo](/help/forms/using/create-adaptive-form.md)

## Passaggio 1: Configurare il database MySQL come origine dati {#config-database}

È possibile configurare diversi tipi di origini dati per creare un modello dati del modulo. Per questa esercitazione, verrà configurato il database MySQL configurato e popolato con dati di esempio. Per informazioni su altre origini dati supportate e su come configurarle, consulta Integrazione [dati di](../../forms/using/data-integration.md)AEM Forms.

Per configurare il database MySQL, effettuate le seguenti operazioni:

1. Installare il driver JDBC per il database MySQL come bundle OSGi:

   1. Accedete ad AEM Forms Author Instance come amministratore e passate ai bundle della console Web di AEM. L’URL predefinito è [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Toccate **Installa/Aggiorna**. Viene visualizzata una finestra di dialogo **Carica/Installa pacchetti** .

   1. Toccate **Scegli file** per sfogliare e selezionate il bundle OSGi del driver MySQL JDBC. Selezionate **Avvia pacchetto** e **aggiorna pacchetti**, quindi toccate **Installa o Aggiorna**. Assicurarsi che il driver JDBC di Oracle Corporation per MySQL sia attivo. Il driver è installato.

1. Configurare il database MySQL come origine dati:

   1. Andate alla console Web di AEM all&#39;indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individua la configurazione DataSource **** in pool di connessione Apache Sling. Toccate per aprire la configurazione in modalità di modifica.
   1. Nella finestra di dialogo di configurazione, specificate i seguenti dettagli:

      * **Nome origine dati:** Potete specificare qualsiasi nome. Ad esempio, specificate **WeRetailMySQL**.
      * **Nome** proprietà del servizio DataSource: Specificare il nome della proprietà del servizio contenente il nome DataSource. Viene specificato durante la registrazione dell&#39;istanza dell&#39;origine dati come servizio OSGi. Ad esempio, **datasource.name**.
      * **Classe** driver JDBC: Specificate il nome della classe Java del driver JDBC. Per il database MySQL, specificate **com.mysql.jdbc.Driver**.
      * **URI** connessione JDBC: Specificate l&#39;URL di connessione del database. Per il database MySQL in esecuzione sulla porta 3306 e lo schema weretail, l&#39;URL è: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nome utente:** Nome utente del database. È necessario per consentire al driver JDBC di stabilire una connessione con il database.
      * **Password:** Password del database. È necessario per consentire al driver JDBC di stabilire una connessione con il database.
      * **Test sul credito:** Abilitate l&#39;opzione **Prova in prestito** .
      * **Test al ritorno:** Abilitate l&#39;opzione **Test on Return** (Test su ritorno).
      * **Query di convalida:** Specificare una query SQL SELECT per convalidare le connessioni dal pool. La query deve restituire almeno una riga. Ad esempio, **selezionare * dai dettagli** del cliente.
      * **Isolamento** transazione: Impostare il valore su **READ_COMMTED**.
      Lasciate le altre proprietà con [i valori](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predefiniti e toccate **Salva**.
   Viene creata una configurazione simile a quella riportata di seguito.

   ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Step 2: Create form data model {#create-fdm}

AEM Forms offre un&#39;interfaccia utente intuitiva per [creare un](../../forms/using/data-integration.md#main-pars-header-1524967585)modello di dati del modulo da origini dati configurate. È possibile utilizzare più origini dati in un modello dati del modulo. Per il nostro caso di utilizzo, utilizzeremo l&#39;origine dati MySQL configurata.

Per creare un modello dati modulo, effettuare le seguenti operazioni:

1. Nell’istanza di creazione di AEM, passa a **Forms** > Integrazioni **** dati.
1. Tap **Create** > **Form Data Model**.
1. Nella finestra di dialogo Crea modello dati modulo, specificare un **nome** per il modello dati del modulo. Ad esempio, **cliente-spedizione-fatturazione-dettagli**. Toccate **Avanti**.
1. Nella schermata dell&#39;origine dati selezionata sono elencate tutte le origini dati configurate. Selezionate l&#39;origine dati **WeRetailMySQL** e toccate **Crea**.

   ![data-source-selection](assets/data-source-selection.png)

Viene creato il modello di dati del modulo **per la spedizione del cliente-dettagli** di fatturazione.

## Passaggio 3: Configurare il modello dati del modulo {#config-fdm}

La configurazione del modello dati del modulo comporta:

* aggiunta di oggetti modello dati e servizi
* configurazione di servizi di lettura e scrittura per gli oggetti modello dati

Per configurare il modello dati del modulo, effettuare le seguenti operazioni:

1. Nell’istanza di creazione di AEM, passa a **Forms** > Integrazioni **** dati. L’URL predefinito è [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Il modello di dati del modulo **per la spedizione dei clienti e la fatturazione** creato in precedenza è elencato di seguito. Aprirlo in modalità di modifica.

   L&#39;origine dati selezionata **WeRetailMySQL** è configurata nel modello dati del modulo.

   ![default-fdm](assets/default-fdm.png)

1. Espandere la struttura di origine dati WeRailMySQL. Selezionare i seguenti oggetti modello dati e servizi da **weretail** > **custom details** schema a form data model:

   * **Oggetti** del modello dati:

      * id
      * nome
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

   1. Selezionare l&#39;oggetto modello dati **custom details** e toccare **Modifica proprietà**.
   1. Selezionate **Ottieni** dal menu a discesa Servizio di lettura. L&#39;argomento **id** , che è la chiave primaria nell&#39;oggetto del modello di dati dei dettagli del cliente, viene aggiunto automaticamente. Toccate ![aem_6_3_edit](assets/aem_6_3_edit.png) e configurate l&#39;argomento come segue.

      ![read-default](assets/read-default.png)

   1. Analogamente, selezionate **update** come servizio di scrittura. L&#39;oggetto **customerdetails** viene aggiunto automaticamente come argomento. L&#39;argomento è configurato come segue.

      ![write-default](assets/write-default.png)

      Aggiungete e configurate l&#39;argomento **id** come segue.

      ![id-arg](assets/id-arg.png)

   1. Toccare **Fine** per salvare le proprietà dell&#39;oggetto modello dati. Quindi, toccare **Salva** per salvare il modello dati del modulo.

      I servizi **get** e **update** vengono aggiunti come servizi predefiniti per l&#39;oggetto modello dati.

      ![data-model-object](assets/data-model-object.png)

1. Passate alla scheda **Servizi** e configurate i servizi **get** e **update** .

   1. Selezionate il servizio **get** e toccate **Modifica proprietà**. Viene visualizzata la finestra di dialogo delle proprietà.
   1. Specificate quanto segue nella finestra di dialogo Modifica proprietà:

      * **Titolo**: Specificate il titolo del servizio. Ad esempio: Recupera indirizzo di spedizione.
      * **Descrizione**: Specificare la descrizione contenente il funzionamento dettagliato del servizio. Esempio:

         Questo servizio recupera l&#39;indirizzo di spedizione e altri dettagli cliente dal database MySQL

      * **Oggetto** modello di output: Selezionare lo schema contenente i dati del cliente. Esempio:

         schema dettaglio cliente

      * **Restituisce array**: Disattivate l&#39;opzione **Return array** (Restituisce array).
      * **Argomenti**: Selezionare l&#39;argomento denominato **ID**.
      Toccate **Chiudi**. Il servizio per recuperare i dettagli del cliente dal database MySQL è configurato.

      ![ricerca dell&#39;indirizzo di spedizione](assets/shiiping-address-retrieval.png)

   1. Selezionate il servizio di **aggiornamento** e toccate **Modifica proprietà**. Viene visualizzata la finestra di dialogo delle proprietà.

   1. Specificate quanto segue nella finestra di dialogo Modifica proprietà:

      * **Titolo**: Specificate il titolo del servizio. Ad esempio, Aggiorna indirizzo di spedizione.
      * **Descrizione**: Specificare la descrizione contenente il funzionamento dettagliato del servizio. Esempio:

         Questo servizio aggiorna l&#39;indirizzo di spedizione e i campi correlati nel database MySQL

      * **Oggetto** del modello di input: Selezionare lo schema contenente i dati del cliente. Esempio:

         schema dettaglio cliente

      * **Tipo** di output: Selezionare **BOOLEAN**.

      * **Argomenti**: Selezionate l’argomento denominato **ID** e i dettagli **** del cliente.
      Toccate **Chiudi**. Il servizio di **aggiornamento** per aggiornare i dettagli del cliente nel database MySQL è configurato.

      ![shiiping-address-update](assets/shiiping-address-update.png)



L&#39;oggetto e i servizi del modello dati nel modello dati del modulo sono configurati. È ora possibile verificare il modello dati del modulo.

## Step 4: Test form data model {#test-fdm}

È possibile verificare l&#39;oggetto del modello dati e i servizi per verificare che il modello dati del modulo sia configurato correttamente.

Per eseguire il test, effettuate le seguenti operazioni:

1. Fare clic sulla scheda **Modello** , selezionare l&#39;oggetto modello dati **custom details** e toccare **Test Model Object**.
1. Nella finestra **Modello/Servizio** di prova, selezionare Oggetto **modello** Lettura dal menu a discesa **Seleziona modello/servizio** .
1. Nella sezione **Dettagli** cliente, specificate un valore per l&#39;argomento **id** presente nel database MySQL configurato e toccate **Test**.

   I dettagli del cliente associati all&#39;ID specificato vengono recuperati e visualizzati nella sezione **Output** come mostrato di seguito.

   ![test-read-model](assets/test-read-model.png)

1. Analogamente, è possibile verificare l&#39;oggetto e i servizi del modello di scrittura.

   Nell&#39;esempio seguente, il servizio di aggiornamento aggiorna correttamente i dettagli dell&#39;indirizzo per l&#39;ID 7102715 nel database.

   ![test-write-model](assets/test-write-model.png)

   Ora, se si esegue nuovamente il test del servizio modello di lettura per l&#39;ID 7107215, il servizio recupererà e visualizzerà i dettagli cliente aggiornati come mostrato di seguito.

   ![read-updated](assets/read-updated.png)
