---
title: "Tutorial: creare un modello di dati modulo in AEM Forms"
description: Crea modello dati modulo per comunicazione interattiva
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 0%

---

# Tutorial: creare un modello di dati modulo in AEM Forms{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Questo tutorial è un passaggio della serie [Crea la tua prima comunicazione interattiva](/help/forms/using/create-your-first-interactive-communication.md). Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

## Informazioni sull’esercitazione {#about-the-tutorial}

Il modulo di integrazione dei dati di AEM Forms consente di creare un modello di dati modulo da diverse origini dati back-end, come il profilo utente dell’AEM, i servizi web RESTful, i servizi web basati su SOAP, i servizi OData e i database relazionali. È possibile configurare oggetti e servizi del modello dati in un modello dati del modulo e associarlo a un modulo adattivo. I campi del modulo adattivo sono associati alle proprietà dell’oggetto modello dati. I servizi consentono di precompilare il modulo adattivo e riscrivere i dati del modulo inviato nell’oggetto modello dati.

Per ulteriori informazioni sull&#39;integrazione dei dati del modulo e sul modello dati del modulo, vedere [Integrazione dati di AEM Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Questo tutorial illustra i passaggi necessari per preparare, creare, configurare e associare un modello di dati modulo a una comunicazione interattiva. Al termine di questa esercitazione, sarai in grado di:

* [Configurare il database](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [Configura database MySQL come origine dati](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [Crea modello dati modulo](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [Configura modello dati modulo](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Test modello dati modulo](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

Il modello dati del modulo è simile al seguente:

![Modello dati modulo](assets/form_data_model_callouts_new.png)

**A.** Origini dati configurate **B.** Schemi origine dati **C.** Servizi disponibili **D.** Oggetti modello dati **E.** Servizi configurati

## Prerequisiti {#prerequisites}

Prima di iniziare, assicurati di disporre dei seguenti elementi:

* Database MySQL con dati di esempio come indicato nella sezione [Configurare il database](../../forms/using/create-form-data-model0.md#step-set-up-the-database).
* Bundle OSGi per il driver JDBC MySQL come spiegato in [Bundling del driver di database JDBC](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## Passaggio 1: configurare il database {#step-set-up-the-database}

Una banca dati è essenziale per creare una comunicazione interattiva. Questa esercitazione utilizza un database per visualizzare il modello dati del modulo e le funzionalità di persistenza delle comunicazioni interattive. Impostare un database contenente le tabelle cliente, fatture e chiamate.
L’immagine seguente illustra alcuni dati di esempio per la tabella del cliente:

![sample_data_cust](assets/sample_data_cust.png)

Utilizzare l&#39;istruzione DDL seguente per creare la tabella **customer** nel database.

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Utilizzare l&#39;istruzione DDL seguente per creare la tabella **bills** nel database.

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Utilizza la seguente istruzione DDL per creare la tabella **calls** nel database.

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

La tabella **chiamate** include i dettagli della chiamata, ad esempio la data, l&#39;ora, il numero, la durata e le spese. La tabella **customer** è collegata alla tabella chiamate tramite il campo Mobile Number (mobilenum). Per ogni numero di cellulare elencato nella tabella **cliente**, sono presenti più record nella tabella **chiamate**. Ad esempio, puoi recuperare i dettagli della chiamata per il numero di cellulare **1457892541** facendo riferimento alla tabella **calls**.

La tabella **bills** include i dettagli della fattura come la data di fatturazione, il periodo di fatturazione, gli addebiti mensili e gli addebiti di chiamata. La tabella **customer** è collegata alla tabella **bills** utilizzando il campo Piano fatturazione. Esiste un piano associato a ciascun cliente nella tabella **cliente**. La tabella **bills** include i dettagli relativi ai prezzi per tutti i piani esistenti. Ad esempio, puoi recuperare i dettagli del piano per **Sarah** dalla tabella **customer** e utilizzarli per recuperare i dettagli dei prezzi dalla tabella **bills**.

## Passaggio 2: configurare il database MySQL come origine dati {#step-configure-mysql-database-as-data-source}

È possibile configurare diversi tipi di origini dati per creare un modello dati del modulo. Per questa esercitazione, si configurerà il database MySQL configurato e popolato con dati di esempio. Per informazioni sulle altre origini dati supportate e su come configurarle, vedere [Integrazione dei dati di AEM Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Per configurare il database MySQL, eseguire le operazioni seguenti:

1. Installa il driver JDBC per il database MySQL come bundle OSGi:

   1. Accedi all’istanza di authoring di AEM Forms come amministratore e passa ai bundle della console web AEM. URL predefinito: [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. Selezionare **Installa/Aggiorna**. Viene visualizzata la finestra di dialogo **Carica/Installa bundle**.

   1. Selezionare **Scegli file** per sfogliare e selezionare il bundle OSGi del driver JDBC MySQL. Selezionare **Avvia bundle** e **Aggiorna pacchetti**, quindi selezionare **Installa** o **Aggiorna**. Verificare che il driver JDBC di Oracle Corporation per MySQL sia attivo. Il driver è installato.

1. Configurare il database MySQL come origine dati:

   1. Vai alla console Web AEM all&#39;indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individua la configurazione dell&#39;origine dati in pool di connessione **Apache Sling**. Seleziona per aprire la configurazione in modalità di modifica.
   1. Nella finestra di dialogo di configurazione, specifica i dettagli seguenti:

      * **Nome origine dati:** È possibile specificare qualsiasi nome. Specificare ad esempio **MySQL**.

      * **Nome proprietà servizio DataSource**: specificare il nome della proprietà del servizio contenente il nome DataSource. Viene specificato durante la registrazione dell’istanza dell’origine dati come servizio OSGi. **datasource.name**.

      * **Classe driver JDBC**: specificare il nome della classe Java del driver JDBC. Per il database MySQL, specificare **com.mysql.jdbc.Driver**.

      * **URI connessione JDBC**: specificare l&#39;URL di connessione del database. Per il database MySQL in esecuzione sulla porta 3306 e sulla teleca dello schema, l&#39;URL è: `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nome utente:** Nome utente del database. È necessario per abilitare il driver JDBC per stabilire una connessione con il database.
      * **Password:** Password del database. È necessario per abilitare il driver JDBC per stabilire una connessione con il database.
      * **Test sul prestito:** Abilitare l&#39;opzione **Test sul prestito**.

      * **Test su restituzione:** Abilita l&#39;opzione **Test su restituzione**.

      * **Query di convalida:** Specificare una query SQL SELECT per convalidare le connessioni dal pool. La query deve restituire almeno una riga. Ad esempio, **seleziona &#42; dal cliente**.

      * **Isolamento transazione**: impostare il valore su **READ_COMMitted**.

   Lascia altre proprietà con [valori](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predefiniti e seleziona **Salva**.

   Viene creata una configurazione simile alla seguente.

   ![Configurazione Apache](assets/apache_configuration_new.png)

## Passaggio 3: creare il modello dati del modulo {#step-create-form-data-model}

AEM Forms fornisce un&#39;interfaccia utente intuitiva per [creare una modalità dati modulo](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l da origini dati configurate. È possibile utilizzare più origini dati in un modello dati del modulo. Per il caso d&#39;uso di questa esercitazione, verrà utilizzato MySQL come origine dati.

Per creare il modello dati del modulo, effettua le seguenti operazioni:

1. Nell&#39;istanza di authoring AEM, passa a **Forms** > **Integrazioni dati**.
1. Seleziona **Crea** > **Modello dati modulo**.
1. Nella procedura guidata Crea modello dati modulo, specifica un **nome** per il modello dati del modulo. Ad esempio, **FDM_Create_First_IC**. Seleziona **Avanti**.
1. Nella schermata Seleziona origine dati sono elencate tutte le origini dati configurate. Selezionare l&#39;origine dati **MySQL** e selezionare **Crea**.

   ![Origine dati MYSQL](assets/fdm_mysql_data_source_new.png)

1. Fai clic su **Fine**. Il modello dati del modulo **FDM_Create_First_IC** è stato creato.

## Passaggio 4: configurare il modello dati del modulo {#step-configure-form-data-model}

La configurazione del modello dati del modulo include:

* [aggiunta di servizi e oggetti modello dati](#add-data-model-objects-and-services)
* [creazione di proprietà figlio calcolate per l’oggetto modello dati](#create-computed-child-properties-for-data-model-object)
* [aggiunta di associazioni tra oggetti modello dati](#add-associations-between-data-model-objects)
* [modifica delle proprietà di un oggetto modello dati](#edit-data-model-object-properties)
* [configurazione dei servizi per gli oggetti modello dati](#configure-services)

### Aggiungere oggetti e servizi del modello dati {#add-data-model-objects-and-services}

1. Nell&#39;istanza di authoring AEM, passa a **Forms** > **Integrazioni dati**. URL predefinito: [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Il modello dati del modulo **FDM_Create_First_IC** creato in precedenza è elencato qui. Selezionala e seleziona **Modifica**.

   L&#39;origine dati selezionata **MySQL** viene visualizzata nel riquadro **Origini dati**.

   ![Origine dati MYSQL per FDM](assets/mysql_fdm_new.png)

1. Espandere la struttura dell&#39;origine dati **MySQL**. Selezionare i servizi e gli oggetti modello dati seguenti dallo schema **teleca**:

   * **Oggetti modello dati**:

      * effetti
      * chiamate
      * cliente

   * **Servizi:**

      * ottenere
      * aggiorna

   Selezionare **Aggiungi selezionati** per aggiungere gli oggetti e i servizi del modello dati selezionati al modello dati del modulo.

   ![Seleziona servizi oggetto modello dati](assets/select_data_model_object_services_new.png)

   Gli oggetti modello dati relativi a fatture, chiamate e clienti vengono visualizzati nel riquadro di destra nella scheda **Modello**. I servizi di recupero e aggiornamento sono visualizzati nella scheda **Servizi**.

   ![Oggetti modello dati](assets/data_model_objects_new.png)

### Creare proprietà figlio calcolate per l’oggetto modello dati {#create-computed-child-properties-for-data-model-object}

Una proprietà calcolata è quella il cui valore viene calcolato in base a una regola o a un&#39;espressione. Utilizzando una regola è possibile impostare il valore di una proprietà calcolata su una stringa letterale, un numero, il risultato di un&#39;espressione matematica o il valore di un&#39;altra proprietà nel modello dati del modulo.

In base al caso d&#39;uso, crea la proprietà calcolata figlio **usagecharge** nell&#39;oggetto modello dati **bills** utilizzando la seguente espressione matematica:

* costi di utilizzo = spese di chiamata + spese di conferenza telefonica + spese SMS + spese internet mobile + roaming nazionale + roaming internazionale + VAS (tutte queste proprietà esistono nell’oggetto modello dati fatture)
Per ulteriori informazioni sulla proprietà calcolata dall&#39;elemento secondario **usagecharge**, vedere [Pianificare la comunicazione interattiva](/help/forms/using/planning-interactive-communications.md).

Per creare proprietà figlio calcolate per l&#39;oggetto modello dati distinte, eseguire la procedura seguente:

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **bills** per selezionarlo e selezionare **Crea proprietà figlio**.
1. Nel riquadro **Crea proprietà figlio**:

   1. Immetti **usagecharge** come nome della proprietà figlio.
   1. Abilita **Calcolato**.
   1. Seleziona **Mobile** come tipo e seleziona **Fine** per aggiungere la proprietà figlio all&#39;oggetto modello dati **bills**.

   ![Crea proprietà figlio](assets/create_child_property_new.png)

1. Seleziona **Modifica regola** per aprire l&#39;editor di regole.
1. Seleziona **Crea**. Viene visualizzata la finestra della regola **Imposta valore**.
1. Dall&#39;elenco a discesa Seleziona opzione, selezionare **Espressione matematica**.

   ![Editor regole spese di utilizzo](assets/usage_charges_rule_editor_new.png)

1. Nell&#39;espressione matematica, selezionare **callcharge** e **confcallcharge** rispettivamente come primo e secondo oggetto. Seleziona **più** come operatore. Selezionare nell&#39;espressione matematica e selezionare **Estendi espressione** per aggiungere **smscharges**, **internetcharge**, **roamingnational**, **roamingintl** e **vas** oggetti all&#39;espressione.

   L’immagine seguente illustra l’espressione matematica nell’editor di regole:

   ![Regola costi di utilizzo](assets/usage_charges_rule_all_new.png)

1. Seleziona **Fine**. La regola viene creata nell’Editor di regole.
1. Seleziona **Chiudi** per chiudere la finestra Editor regole.

### Aggiungere associazioni tra oggetti modello dati {#add-associations-between-data-model-objects}

Una volta definiti gli oggetti modello dati, puoi creare delle associazioni tra di essi. L’associazione può essere uno a uno o uno a molti. Ad esempio, a un dipendente possono essere associate più persone a carico. È definita associazione uno-a-molti ed è rappresentata da 1:n sulla linea che collega gli oggetti modello dati associati. Tuttavia, se un&#39;associazione restituisce un nome di dipendente univoco per un determinato ID dipendente, viene definita associazione uno-a-uno.

Quando si aggiungono oggetti modello dati associati in un&#39;origine dati a un modello dati del modulo, le relative associazioni vengono mantenute e visualizzate come collegate da linee freccia.

In base al caso d’uso, crea le seguenti associazioni tra gli oggetti del modello di dati:

| Associazione | Oggetti modello dati |
|---|---|
| 1:n | cliente:chiamate (è possibile associare più chiamate a un cliente con una fattura mensile) |
| 1:1 | cliente:fatture (una fattura è associata a un cliente per un mese specifico) |

Per creare associazioni tra oggetti modello dati, effettuare le operazioni riportate di seguito.

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **cliente** per selezionarlo e selezionare **Aggiungi associazione**. Verrà aperto il riquadro delle proprietà **Aggiungi associazione**.
1. Nel riquadro **Aggiungi associazione**:

   * Specificare un titolo per l&#39;associazione. È un campo facoltativo.
   * Selezionare **Da uno a molti** dall&#39;elenco a discesa **Tipo**.

   * Selezionare **chiamate** dall&#39;elenco a discesa **Oggetto modello**.

   * Selezionare **get** dall&#39;elenco a discesa **Service**.

   * Seleziona **Aggiungi** per collegare l&#39;oggetto modello dati **cliente** all&#39;oggetto modello dati **chiamate** tramite una proprietà. In base al caso d’uso, l’oggetto modello dati chiamate deve essere collegato alla proprietà mobile number nell’oggetto modello dati cliente. Viene visualizzata la finestra di dialogo **Aggiungi argomento**.

   ![Aggiungi associazione](assets/add_association_new.png)

1. Nella finestra di dialogo **Aggiungi argomento**:

   * Seleziona **mobilenum** dall&#39;elenco a discesa **Name**. La proprietà mobile number è una proprietà comune disponibile negli oggetti modello dati del cliente e delle chiamate. Di conseguenza, viene utilizzato per creare un’associazione tra il cliente e chiama oggetti modello dati.
Per ogni numero di cellulare disponibile nell’oggetto modello dati del cliente, nella tabella chiamate sono disponibili più record di chiamata.

   * Specificare un titolo e una descrizione facoltativi per l&#39;argomento.
   * Seleziona **cliente** dall&#39;elenco a discesa **Associazione a**.

   * Selezionare **mobilenum** dall&#39;elenco a discesa **Valore associazione**.

   * Seleziona **Aggiungi**.

   ![Aggiungi associazione per un argomento](assets/add_association_argument_new.png)

   La proprietà mobilenum viene visualizzata nella sezione **Arguments**.

   ![Aggiungi associazione argomento](assets/add_argument_association_new.png)

1. Seleziona **Fine** per creare un&#39;associazione 1:n tra il cliente e gli oggetti modello dati delle chiamate.

   Dopo aver creato un&#39;associazione tra il cliente e gli oggetti modello dati di chiamata, creare un&#39;associazione 1:1 tra gli oggetti modello dati cliente e fatturazione.

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **cliente** per selezionarlo e selezionare **Aggiungi associazione**. Verrà aperto il riquadro delle proprietà **Aggiungi associazione**.
1. Nel riquadro **Aggiungi associazione**:

   * Specificare un titolo per l&#39;associazione. È un campo facoltativo.
   * Selezionare **Da uno a uno** dall&#39;elenco a discesa **Tipo**.

   * Selezionare **distinte** dall&#39;elenco a discesa **Oggetto modello**.

   * Selezionare **get** dall&#39;elenco a discesa **Service**. La proprietà **billplan**, che è la chiave primaria per la tabella delle distinte, è già disponibile nella sezione **Arguments**.
Gli oggetti modello dati fatture e cliente vengono collegati utilizzando rispettivamente le proprietà billplan (fatture) e customerplan (cliente). Creare un&#39;associazione tra queste proprietà per recuperare i dettagli del piano per qualsiasi cliente disponibile nel database MySQL.

   * Seleziona **cliente** dall&#39;elenco a discesa **Associazione a**.

   * Selezionare **customerplan** dall&#39;elenco a discesa **Valore associazione**.

   * Selezionare **Fine** per creare un&#39;associazione tra le proprietà billplan e customerplan.

   ![Aggiungi associazione per fattura cliente](assets/add_association_customer_bills_new.png)

   L’immagine seguente illustra le associazioni tra gli oggetti modello dati e le proprietà utilizzate per creare associazioni tra di essi:

   ![associazioni_fdm](assets/fdm_associations.gif)

### Modifica proprietà oggetto modello dati {#edit-data-model-object-properties}

Dopo aver creato le associazioni tra il cliente e altri oggetti modello dati, modifica le proprietà del cliente per definire la proprietà in base alla quale i dati vengono recuperati dall’oggetto modello dati. In base al caso d’uso, il numero di cellulare viene utilizzato come proprietà per recuperare i dati dall’oggetto modello dati del cliente.

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **customer** per selezionarlo e selezionare **Modifica proprietà**. Verrà visualizzato il riquadro **Modifica proprietà**.
1. Specifica **cliente** come **oggetto modello di primo livello**.
1. Selezionare **get** dall&#39;elenco a discesa **Servizio di lettura**.
1. Nella sezione **Arguments**:

   * Selezionare **Richiedi attributo** dall&#39;elenco a discesa **Associazione a**.

   * Specificare **mobilenum** come valore di associazione.

1. Seleziona **aggiornamento** dall&#39;elenco a discesa **Scrivi** servizio.
1. Nella sezione **Arguments**:

   * Per la proprietà **mobilenum**, selezionare **cliente** dall&#39;elenco a discesa **Associazione a**.

   * Selezionare **mobilenum** dall&#39;elenco a discesa **Valore associazione**.

1. Seleziona **Fine** per salvare le proprietà.

   ![Configura servizi](assets/configure_services_customer_new.png)

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **calls** per selezionarlo e selezionare **Modifica proprietà**. Verrà visualizzato il riquadro **Modifica proprietà**.
1. Disattiva l&#39;**oggetto modello di primo livello** per l&#39;oggetto modello dati **calls**.
1. Seleziona **Fine**.

   Ripetere i passaggi da 8 a 10 per configurare le proprietà per l&#39;oggetto modello dati **bills**.

### Configurare i servizi {#configure-services}

1. Passa alla scheda **Servizi**.
1. Selezionare il servizio **get** e selezionare **Modifica proprietà**. Verrà visualizzato il riquadro **Modifica proprietà**.
1. Nel riquadro **Modifica proprietà**:

   * Immettere un titolo e una descrizione facoltativi.
   * Seleziona **cliente** dall&#39;elenco a discesa **Oggetto modello di output**.

   * Seleziona **Fine** per salvare le proprietà.

   ![Modifica delle proprietà](assets/edit_properties_get_details_new.png)

1. Seleziona il servizio **update** e seleziona **Modifica proprietà**. Verrà visualizzato il riquadro **Modifica proprietà**.
1. Nel riquadro **Modifica proprietà**:

   * Immettere un titolo e una descrizione facoltativi.
   * Seleziona **cliente** dall&#39;elenco a discesa **Oggetto modello di input**.

   * Seleziona **Fine**.
   * Seleziona **Salva** per salvare il modello dati del modulo.

   ![Aggiorna proprietà del servizio](assets/update_service_properties_new.png)

## Passaggio 5: testare il modello di dati del modulo e i servizi {#step-test-form-data-model-and-services}

È possibile eseguire il test dell&#39;oggetto modello dati e dei servizi per verificare che il modello dati del modulo sia configurato correttamente.

Per eseguire il test, eseguire le operazioni seguenti:

1. Vai alla scheda **Modello**, seleziona l&#39;oggetto modello dati **cliente** e seleziona **Oggetto modello di test**.
1. Nella finestra **Test modello dati modulo**, selezionare **Leggi oggetto modello** dall&#39;elenco a discesa **Seleziona modello/servizio**.
1. Nella sezione **Input** specificare un valore per la proprietà **mobilenum** esistente nel database MySQL configurato e selezionare **Test**.

   I dettagli del cliente associati alla proprietà mobilenum specificata vengono recuperati e visualizzati nella sezione Output come mostrato di seguito. Chiudete la finestra di dialogo.

   ![Modello dati di prova](assets/test_data_model_new.png)

1. Passa alla scheda **Servizi**.
1. Selezionare il servizio **get** e selezionare il servizio **Test.**
1. Nella sezione **Input** specificare un valore per la proprietà **mobilenum** esistente nel database MySQL configurato e selezionare **Test**.

   I dettagli del cliente associati alla proprietà mobilenum specificata vengono recuperati e visualizzati nella sezione Output come mostrato di seguito. Chiudete la finestra di dialogo.

   ![Servizio di prova](assets/test_service_new.png)

### Modificare e salvare i dati di esempio {#edit-and-save-sample-data}

L’editor del modello dati modulo consente di generare dati di esempio per tutte le proprietà dell’oggetto modello dati, incluse le proprietà calcolate, in un modello dati modulo. Si tratta di un set di valori casuali conformi al tipo di dati configurato per ogni proprietà. È inoltre possibile modificare e salvare i dati, che vengono mantenuti anche se si rigenerano i dati di esempio.

Per generare, modificare e salvare dati di esempio, effettuare le seguenti operazioni:

1. Nella pagina del modello dati del modulo, selezionare **Modifica dati di esempio**. Genera e visualizza i dati di esempio nella finestra Modifica dati di esempio.

   ![Modifica dati di esempio](assets/edit_sample_data_new.png)

1. Nella finestra **Modifica dati di esempio**, modificare i dati in base alle esigenze e selezionare **Salva**. Chiudete la finestra.
