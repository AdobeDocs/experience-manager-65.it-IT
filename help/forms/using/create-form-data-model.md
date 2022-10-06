---
title: "Esercitazione: Crea modello dati modulo "
seo-title: Create Form Data Model Tutorial
description: Crea modello dati modulo
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 1%

---

# Esercitazione: Crea modello dati modulo {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Questa esercitazione è un passaggio nel [Creare il primo modulo adattivo](../../forms/using/create-your-first-adaptive-form.md) serie. Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

## Informazioni sull’esercitazione {#about-the-tutorial}

AEM [!DNL Forms] il modulo di integrazione dei dati consente di creare un modello di dati del modulo da diverse origini di dati di backend, come AEM profilo utente, servizi web RESTful, servizi web basati su SOAP, servizi OData e database relazionali. È possibile configurare oggetti modello dati e servizi in un modello dati modulo e associarlo a un modulo adattivo. I campi modulo adattivo sono associati alle proprietà dell’oggetto modello dati. I servizi consentono di precompilare il modulo adattivo e di riscrivere i dati del modulo inviato all’oggetto modello dati.

Per ulteriori informazioni sull’integrazione dei dati del modulo e sul modello di dati del modulo, consulta [Integrazione dei dati di AEM Forms](../../forms/using/data-integration.md).

Questa esercitazione descrive i passaggi necessari per preparare, creare, configurare e associare un modello di dati modulo a un modulo adattivo. Al termine di questa esercitazione, potrai:

* [Configurare il database MySQL come origine dati](#config-database)
* [Crea modello dati modulo utilizzando database MySQL](#create-fdm)
* [Configurare il modello dati del modulo](#config-fdm)
* [Test del modello dati del modulo](#test-fdm)

Il modello dati del modulo avrà un aspetto simile al seguente:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Origini dati configurate **B.** Schemi di origine dati **C.** Servizi disponibili **D.** Oggetti del modello dati **E.** Servizi configurati

## Prerequisiti {#prerequisites}

Prima di iniziare, assicurati di disporre dei seguenti elementi:

* [!DNL MySQL] database con dati di esempio come indicato nella sezione Prerequisiti di [Creare il primo modulo adattivo](../../forms/using/create-your-first-adaptive-form.md)
* Bundle OSGi per [!DNL MySQL] Driver JDBC come spiegato in [Bundling del driver di database JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Modulo adattivo come descritto nella prima esercitazione [Creare un modulo adattivo](/help/forms/using/create-adaptive-form.md)

## Passaggio 1: Configurare il database MySQL come origine dati {#config-database}

È possibile configurare diversi tipi di origini dati per creare un modello dati del modulo. Per questa esercitazione, configureremo il database MySQL configurato e popolato con dati di esempio. Per informazioni su altre origini dati supportate e su come configurarle, consulta [Integrazione dei dati di AEM Forms](../../forms/using/data-integration.md).

Effettua le seguenti operazioni per configurare il tuo [!DNL MySQL] database:

1. Installa il driver JDBC per [!DNL MySQL] database come bundle OSGi:

   1. Accedi a AEM [!DNL Forms] Istanza autore come amministratore e vai AEM bundle della console web. L’URL predefinito è [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Tocca **[!UICONTROL Installazione/aggiornamento]**. Un [!UICONTROL Caricare/installare i bundle] viene visualizzata la finestra di dialogo .

   1. Tocca **[!UICONTROL Scegli file]** per sfogliare e selezionare il [!DNL MySQL] Bundle OSGi del driver JDBC. Seleziona **[!UICONTROL Avvia bundle]** e **[!UICONTROL Aggiorna pacchetti]**, e tocca **[!UICONTROL Installa o aggiorna]**. Assicurati che [!DNL Oracle Corporation's] Driver JDBC per [!DNL MySQL] è attivo. Il driver è installato.

1. Configura [!DNL MySQL] database come origine dati:

   1. Vai AEM console Web all&#39;indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individua **Origine dati in pool di connessione Apache Sling** configurazione. Tocca per aprire la configurazione in modalità di modifica.
   1. Nella finestra di dialogo di configurazione, specifica i seguenti dettagli:

      * **Nome origine dati:** Puoi specificare un nome qualsiasi. Ad esempio, specifica **WeRetailMySQL**.
      * **Nome della proprietà del servizio DataSource**: Specifica il nome della proprietà del servizio contenente il nome DataSource. Viene specificato durante la registrazione dell&#39;istanza dell&#39;origine dati come servizio OSGi. Ad esempio: **datasource.name**.
      * **Classe del driver JDBC**: Specifica il nome della classe Java del driver JDBC. Per [!DNL MySQL] database, specificare **com.mysql.jdbc.Driver**.
      * **URI di connessione JDBC**: Specifica l&#39;URL di connessione del database. Per [!DNL MySQL] database in esecuzione sulla porta 3306 e schema weretail, l&#39;URL è: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nome utente:** Nome utente del database. È necessario per abilitare il driver JDBC per stabilire una connessione con il database.
      * **Password:** Password del database. È necessario per abilitare il driver JDBC per stabilire una connessione con il database.
      * **Prova su prestito:** Abilita la **[!UICONTROL Test su credito]** opzione .
      * **Test al ritorno:** Abilita la **[!UICONTROL Test al ritorno]** opzione .
      * **Query di convalida:** Specificare una query SQL SELECT per convalidare le connessioni dal pool. La query deve restituire almeno una riga. Ad esempio: **select &#42; dai dettagli del cliente**.
      * **Isolamento transazione**: Imposta il valore su **READ_COMMTED**.

         Lascia altre proprietà con impostazione predefinita [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) e toccare **[!UICONTROL Salva]**.

         Viene creata una configurazione simile a quella riportata di seguito.

         ![relazionale-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Passaggio 2: Crea modello dati modulo {#create-fdm}

AEM [!DNL Forms] fornisce un&#39;interfaccia utente intuitiva per [creare un modello dati modulo](data-integration.md) da origini dati configurate. È possibile utilizzare più origini dati in un modello dati modulo. Per il nostro caso d’uso, utilizzeremo il [!DNL MySQL] origine dati.

Per creare un modello dati modulo, procedere come segue:

1. In AEM’istanza di authoring, passa a **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**.
1. Tocca **[!UICONTROL Crea]** > **[!UICONTROL Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo , specifica un **name** per il modello dati del modulo. Ad esempio: **customer-shipping-billing-details**. Tocca **[!UICONTROL Successivo]**.
1. Nella schermata Seleziona origine dati sono elencate tutte le origini dati configurate. Seleziona **WeRetailMySQL** origine dati e tocca **[!UICONTROL Crea]**.

   ![selezione della sorgente dati](assets/data-source-selection.png)

La **customer-shipping-billing-details** viene creato il modello dati del modulo.

## Passaggio 3: Configurare il modello dati del modulo {#config-fdm}

La configurazione del modello dati del modulo comporta:

* aggiunta di oggetti e servizi del modello dati
* configurazione dei servizi di lettura e scrittura per gli oggetti del modello dati

Per configurare il modello dati del modulo, effettuare le seguenti operazioni:

1. Nell&#39;istanza AEM autore, passa a **[!UICONTROL Forms]** > **[!UICONTROL Integrazioni dati]**. L’URL predefinito è [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. La **customer-shipping-billing-details** il modello dati del modulo creato in precedenza è elencato qui. Aprirlo in modalità di modifica.

   Origine dati selezionata **WeRetailMySQL** è configurato nel modello dati del modulo.

   ![default-fdm](assets/default-fdm.png)

1. Espandere la struttura di origine dati WeRailMySQL. Selezionare i seguenti oggetti e servizi del modello dati da **weretail** > **dettagli cliente** schema per il modello dati del modulo:

   * **Oggetti del modello dati**:

      * id
      * name
      * shippingAddress
      * città
      * stadio
      * zipcode
   * **Servizi:**

      * get
      * aggiorna

   Tocca **Aggiungi selezionati** per aggiungere oggetti e servizi del modello dati selezionati al modello dati del modulo.

   ![Schema WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >I servizi get, update e insert predefiniti per le origini dati JDBC vengono forniti con il modello dati del modulo .

1. Configurare i servizi di lettura e scrittura per l&#39;oggetto modello dati.

   1. Seleziona la **dettagli cliente** oggetto modello dati e tocca **[!UICONTROL Modifica proprietà]**.
   1. Seleziona **[!UICONTROL get]** dal menu a discesa Read Service . La **id** argomento, che è la chiave primaria nell&#39;oggetto modello dati customerdetails viene aggiunto automaticamente. Tocca ![aem_6_3_edit](assets/aem_6_3_edit.png) e configura l’argomento come segue.

      ![read-default](assets/read-default.png)

   1. Analogamente, seleziona **[!UICONTROL update]** come servizio di scrittura. La **dettagli cliente** viene aggiunto automaticamente come argomento. L’argomento viene configurato come segue.

      ![predefinito di scrittura](assets/write-default.png)

      Aggiungi e configura le **id** argomento come segue.

      ![id-arg](assets/id-arg.png)

   1. Tocca **[!UICONTROL Fine]** per salvare le proprietà dell&#39;oggetto modello dati. Quindi, tocca **[!UICONTROL Salva]** per salvare il modello dati del modulo.

      La **[!UICONTROL get]** e **[!UICONTROL update]** i servizi vengono aggiunti come servizi predefiniti per l’oggetto modello dati.

      ![data-model-object](assets/data-model-object.png)

1. Vai a **[!UICONTROL Servizi]** scheda e configurazione **[!UICONTROL get]** e **[!UICONTROL update]** servizi.

   1. Seleziona la **[!UICONTROL get]** servizio e rubinetto **[!UICONTROL Modifica proprietà]**. Viene visualizzata la finestra di dialogo delle proprietà.
   1. Nella finestra di dialogo Modifica proprietà , specifica quanto segue:

      * **Titolo**: Specifica il titolo del servizio. Ad esempio: Recupera indirizzo di spedizione.
      * **Descrizione**: Specifica la descrizione contenente il funzionamento dettagliato del servizio. Esempio:

         Questo servizio recupera l&#39;indirizzo di spedizione e altri dettagli del cliente da [!DNL MySQL] database

      * **Oggetto modello di output**: Selezionare lo schema contenente i dati del cliente. Esempio:

         schema di dettaglio del cliente

      * **Matrice di ritorno**: Disattiva la **Matrice di ritorno** opzione .
      * **Argomenti**: Seleziona argomento denominato **ID**.

      Toccate **[!UICONTROL Chiudi]**. Il servizio per recuperare i dettagli del cliente dal database MySQL è configurato.

      ![spogliarello-indirizzo-recupero](assets/shiiping-address-retrieval.png)

   1. Seleziona la **[!UICONTROL update]** servizio e rubinetto **[!UICONTROL Modifica proprietà]**. Viene visualizzata la finestra di dialogo delle proprietà.

   1. Specifica quanto segue nella [!UICONTROL Modifica proprietà] finestra di dialogo:

      * **Titolo**: Specifica il titolo del servizio. Ad esempio, Aggiorna indirizzo di spedizione.
      * **Descrizione**: Specifica la descrizione contenente il funzionamento dettagliato del servizio. Esempio:

         Questo servizio aggiorna l&#39;indirizzo di spedizione e i campi correlati nel database MySQL

      * **Oggetto modello di input**: Selezionare lo schema contenente i dati del cliente. Esempio:

         schema di dettaglio del cliente

      * **Tipo di uscita**: Seleziona **BOOLEANO**.

      * **Argomenti**: Seleziona argomento denominato **ID** e **dettagli cliente**.
      Toccate **[!UICONTROL Chiudi]**. La **[!UICONTROL update]** per aggiornare i dettagli del cliente nel [!DNL MySQL] database configurato.

      ![invio-indirizzo-aggiornamento](assets/shiiping-address-update.png)



L’oggetto del modello dati e i servizi inclusi nel modello dati del modulo sono configurati. È ora possibile verificare il modello dati del modulo.

## Passaggio 4: Test del modello dati del modulo {#test-fdm}

È possibile verificare l’oggetto e i servizi del modello dati per verificare che il modello dati del modulo sia configurato correttamente.

Per eseguire il test, procedi come segue:

1. Vai a **[!UICONTROL Modello]** seleziona la scheda **dettagli cliente** oggetto modello dati e tocca **[!UICONTROL Oggetto modello di test]**.
1. In [!UICONTROL Modello/servizio di prova] finestra, seleziona **[!UICONTROL Oggetto modello lettura]** dal **[!UICONTROL Seleziona modello/servizio]** a discesa.
1. In **dettagli cliente** specifica un valore per **id** argomento esistente nella configurazione [!DNL MySQL] database e toccare **[!UICONTROL Test]**.

   I dettagli del cliente associati all’ID specificato vengono recuperati e visualizzati nella **[!UICONTROL Uscita]** come illustrato di seguito.

   ![modello a lettura di prova](assets/test-read-model.png)

1. Analogamente, è possibile verificare l&#39;oggetto e i servizi del modello Write.

   Nell’esempio seguente, il servizio di aggiornamento aggiorna correttamente i dettagli dell’indirizzo per l’id 7102715 nel database.

   ![modello di test-write](assets/test-write-model.png)

   Ora, se esegui nuovamente il test del servizio modello letto per l’id 7107215, recupererà e visualizzerà i dettagli aggiornati del cliente come mostrato di seguito.

   ![aggiornato in lettura](assets/read-updated.png)
