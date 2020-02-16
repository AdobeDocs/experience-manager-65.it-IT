---
title: '"Esercitazione: Crea modello dati modulo"'
seo-title: Creare un modello dati modulo per la comunicazione interattiva
description: Creare un modello dati modulo per la comunicazione interattiva
seo-description: Creare un modello dati modulo per la comunicazione interattiva
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Tutorial: Create form data model{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Questa esercitazione è un passaggio della serie [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) (Creazione della prima serie di comunicazioni interattive). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

## Informazioni sull&#39;esercitazione {#about-the-tutorial}

Il modulo di integrazione dei dati di AEM Forms consente di creare un modello di dati del modulo da origini dati back-end diverse, quali profilo utente AEM, servizi Web RESTful, servizi Web basati su SOAP, servizi OData e database relazionali. È possibile configurare oggetti e servizi del modello dati in un modello dati modulo e associarlo a un modulo adattivo. I campi modulo adattivi sono associati alle proprietà dell&#39;oggetto modello dati. I servizi consentono di precompilare il modulo adattivo e di riscrivere i dati del modulo inviato all&#39;oggetto modello dati.

Per ulteriori informazioni sull&#39;integrazione dei dati del modulo e sul modello di dati del modulo, consultate Integrazione [dei dati di](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)AEM Forms.

Questa esercitazione illustra i passaggi necessari per preparare, creare, configurare e associare un modello dati del modulo a una comunicazione interattiva. Al termine di questa esercitazione, potrete:

* [Configurare il database](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [Configurare il database MySQL come origine dati](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [Crea modello dati modulo](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [Configurare il modello dati del modulo](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Verifica modello dati modulo](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

Il modello dati del modulo è simile al seguente:

![Modello dati modulo](assets/form_data_model_callouts_new.png)

**********A. Origini dati configurate** B. Schemi origine dati **C.** Servizi disponibili **D. Oggetti del modello dati** E. Servizi configurati

## Prerequisiti {#prerequisites}

Prima di iniziare, accertatevi di disporre dei seguenti elementi:

* Database MySQL con dati di esempio come indicato nella sezione [Imposta database](../../forms/using/create-form-data-model0.md#step-set-up-the-database) .
* Pacchetto OSGi per il driver JDBC MySQL come spiegato in [Bundling del driver del database JDBC](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## Passaggio 1: Configurare il database {#step-set-up-the-database}

Un database è essenziale per creare una comunicazione interattiva. Questa esercitazione utilizza un database per visualizzare il modello dati del modulo e le funzionalità di persistenza delle comunicazioni interattive. Configurate un database contenente tabelle cliente, fatture e chiamate.
L&#39;immagine seguente illustra i dati di esempio per la tabella cliente:

![sample_data_cust](assets/sample_data_cust.png)

La tabella delle chiamate include i dettagli delle chiamate, come la data di chiamata, l&#39;ora di chiamata, il numero di chiamata, la durata delle chiamate e le spese di chiamata. La tabella del cliente è collegata alla tabella delle chiamate utilizzando il campo Numero mobile (mobilenum). Per ogni numero di cellulare elencato nella tabella del cliente, nella tabella delle chiamate sono presenti più record. Ad esempio, puoi recuperare i dettagli della chiamata per il numero mobile **1457892541** facendo riferimento alla tabella delle chiamate.

La tabella delle fatture include i dettagli delle fatture, ad esempio data di fatturazione, periodo di fatturazione, spese mensili e spese di chiamata. La tabella cliente è collegata alla tabella delle fatture utilizzando il campo Piano fatture. Nella tabella cliente è presente un piano associato a ciascun cliente. La tabella delle fatture include i dettagli dei prezzi per tutti i piani esistenti. Ad esempio, è possibile recuperare i dettagli del piano per **Sarah** dalla tabella dei clienti e utilizzare tali dettagli per recuperare i dettagli dei prezzi dalla tabella delle fatture.

## Passaggio 2: Configurare il database MySQL come origine dati {#step-configure-mysql-database-as-data-source}

È possibile configurare diversi tipi di origini dati per creare un modello dati del modulo. Per questa esercitazione, configurerete il database MySQL configurato e compilato con i dati di esempio. Per informazioni su altre origini dati supportate e su come configurarle, consulta Integrazione [dati di](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)AEM Forms.

Per configurare il database MySQL, effettuate le seguenti operazioni:

1. Installare il driver JDBC per il database MySQL come bundle OSGi:

   1. Accedete ad AEM Forms Author Instance come amministratore e passate ai bundle della console Web di AEM. L’URL predefinito è [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. Toccate **Installa/Aggiorna**. Viene visualizzata una finestra di dialogo **Carica/Installa pacchetti** .

   1. Toccate **Scegli file** per sfogliare e selezionate il bundle OSGi del driver MySQL JDBC. Selezionate **Avvia pacchetto** e **aggiorna pacchetti**, quindi toccate **Installa** o **Aggiorna**. Assicurarsi che il driver JDBC di Oracle Corporation per MySQL sia attivo. Il driver è installato.

1. Configurare il database MySQL come origine dati:

   1. Andate alla console Web di AEM all&#39;indirizzo [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Individua la configurazione DataSource **** in pool di connessione Apache Sling. Toccate per aprire la configurazione in modalità di modifica.
   1. Nella finestra di dialogo di configurazione, specificate i seguenti dettagli:

      * **** Nome origine dati: Potete specificare qualsiasi nome. Ad esempio, specificare **MySQL**.

      * **Nome** proprietà del servizio DataSource: Specificare il nome della proprietà del servizio contenente il nome DataSource. Viene specificato durante la registrazione dell&#39;istanza dell&#39;origine dati come servizio OSGi. Ad esempio, **datasource.name**.

      * **Classe** driver JDBC: Specificate il nome della classe Java del driver JDBC. Per il database MySQL, specificate **com.mysql.jdbc.Driver**.

      * **URI** connessione JDBC: Specificate l&#39;URL di connessione del database. Per il database MySQL in esecuzione sulla porta 3306 e sullo schema teleca, l&#39;URL è: jdbc:mysql://[server]:3306/teleca?autoReconnect=true&amp;useUnicode=true&amp;characterEncoding=utf-8
      * **** Nome utente: Nome utente del database. È necessario per consentire al driver JDBC di stabilire una connessione con il database.
      * **** Password: Password del database. È necessario per consentire al driver JDBC di stabilire una connessione con il database.
      * **** Test sul credito: Abilitate l&#39;opzione **Prova in prestito** .

      * **** Test al ritorno: Abilitate l&#39;opzione **Test on Return** (Test su ritorno).

      * **** Query di convalida: Specificare una query SQL SELECT per convalidare le connessioni dal pool. La query deve restituire almeno una riga. Ad esempio, **selezionare * dal cliente**.

      * **Isolamento** transazione: Impostare il valore su **READ_COMMTED**.
   Lasciate le altre proprietà con [i valori](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predefiniti e toccate **Salva**.

   Viene creata una configurazione simile alla seguente.

   ![Configurazione Apache](assets/apache_configuration_new.png)

## Step 3: Create form data model {#step-create-form-data-model}

AEM Forms offre un&#39;interfaccia utente intuitiva per [creare un](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)modello di dati del modulo da origini dati configurate. È possibile utilizzare più origini dati in un modello dati del modulo. Per l&#39;utilizzo in questa esercitazione, verrà utilizzato MySQL come origine dati.

Per creare un modello dati modulo, effettuare le seguenti operazioni:

1. Nell’istanza di creazione di AEM, passa a **Forms** > Integrazioni **** dati.
1. Tap **Create** > **Form Data Model**.
1. Nella procedura guidata Crea modello dati modulo, specificare un **nome** per il modello dati del modulo. Ad esempio, **FDM_Create_First_IC**. Toccate **Avanti**.
1. Nella schermata dell&#39;origine dati selezionata sono elencate tutte le origini dati configurate. Selezionare l&#39;origine dati **MySQL** e toccare **Crea**.

   ![Origine dati MYSQL](assets/fdm_mysql_data_source_new.png)

1. Fate clic su **Fine**. Viene creato il modello di dati del modulo **FDM_Create_First_IC** .

## Passaggio 4: Configurare il modello dati del modulo {#step-configure-form-data-model}

La configurazione del modello dati del modulo include:

* [aggiunta di oggetti modello dati e servizi](#add-data-model-objects-and-services)
* [creazione di proprietà figlio calcolate per l&#39;oggetto modello dati](#create-computed-child-properties-for-data-model-object)
* [aggiunta di associazioni tra gli oggetti del modello dati](#add-associations-between-data-model-objects)
* [modifica delle proprietà dell&#39;oggetto modello dati](#edit-data-model-object-properties)
* [configurazione dei servizi per gli oggetti del modello dati](#configure-services)

### Aggiunta di oggetti e servizi del modello dati {#add-data-model-objects-and-services}

1. Nell’istanza di creazione di AEM, passa a **Forms** > Integrazioni **** dati. L’URL predefinito è [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Il modello di dati del modulo **FDM_Create_First_IC** creato in precedenza è elencato di seguito. Selezionatela e toccate **Modifica**.

   L&#39;origine dati selezionata **MySQL** viene visualizzata nel riquadro Origini **** dati.

   ![Origine dati MYSQL per FDM](assets/mysql_fdm_new.png)

1. Espandere la struttura dell&#39;origine dati **MySQL** . Selezionare i seguenti oggetti modello dati e servizi dallo schema **teleca** :

   * **Oggetti** del modello dati:

      * bollette
      * call
      * cliente
   * **Servizi:**

      * get
      * aggiorna
   Toccare **Aggiungi selezionato** per aggiungere gli oggetti e i servizi del modello dati selezionati al modello dati del modulo.

   ![Selezionare i servizi oggetto del modello dati](assets/select_data_model_object_services_new.png)

   Le fatture, le chiamate e gli oggetti modello dati cliente vengono visualizzati nel riquadro a destra della scheda **Modello** . I servizi get e update sono visualizzati nella scheda **Servizi** .

   ![Oggetti del modello dati](assets/data_model_objects_new.png)

### Creazione di proprietà figlio calcolate per l&#39;oggetto modello dati {#create-computed-child-properties-for-data-model-object}

Una proprietà calcolata è quella il cui valore viene calcolato in base a una regola o un&#39;espressione. Utilizzando una regola, è possibile impostare il valore di una proprietà calcolata su una stringa letterale, un numero, il risultato di un&#39;espressione matematica o il valore di un&#39;altra proprietà nel modello dati del modulo.

In base al caso d&#39;uso, creare la proprietà **usagecharge** figlio calcolata nell&#39;oggetto modello dati **distinte** utilizzando la seguente espressione matematica:

* tariffe di utilizzo = tariffe chiamate + tariffe chiamate conferenze + tariffe SMS + tariffe internet mobili + roaming nazionale + roaming internazionale + VAS (tutte queste proprietà esistono nell&#39;oggetto modello dati fatture)Per ulteriori informazioni sulle **tariffe** di utilizzo della proprietà calcolata per i bambini, vedere [Piano della comunicazione](/help/forms/using/planning-interactive-communications.md)interattiva.

Per creare proprietà figlio calcolate per l&#39;oggetto modello dati fatture, eseguire i passaggi seguenti:

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **distinte** per selezionarlo e toccare **Crea proprietà** figlia.
1. Nel riquadro **Crea proprietà** figlio:

   1. Immettere **usagecariche** come nome della proprietà figlio.
   1. Abilita **calcolato**.
   1. Selezionare **Mobile** come tipo e toccare **Fine** per aggiungere la proprietà figlio all&#39;oggetto modello dati **distinte** .
   ![Crea proprietà figlio](assets/create_child_property_new.png)

1. Toccate **Modifica regola** per aprire l&#39;Editor regole.
1. Toccate **Crea**. Viene visualizzata la finestra **Imposta regola valore** .
1. Dal menu a discesa Seleziona opzione, selezionate Espressione **** matematica.

   ![Editor regole di tariffazione](assets/usage_charges_rule_editor_new.png)

1. Nell&#39;espressione matematica, selezionare, rispettivamente, **callcharge** e **dolcallload** come primo e secondo oggetto. Selezionare **più** come operatore. Toccate all&#39;interno dell&#39;espressione matematica e toccate **Estendi espressione** per aggiungere **scharges**, **internetcarts**, **roamingnational**, **roamingintnl****** e vasoggetti all&#39;espressione.

   L&#39;immagine seguente rappresenta l&#39;espressione matematica nell&#39;editor di regole:

   ![Regola dei costi di utilizzo](assets/usage_charges_rule_all_new.png)

1. Toccate **Chiudi**. La regola viene creata nell&#39;Editor regole.
1. Toccate **Chiudi** per chiudere la finestra Editor regole.

### Aggiungere associazioni tra gli oggetti del modello dati {#add-associations-between-data-model-objects}

Una volta definiti gli oggetti del modello dati, è possibile creare associazioni tra di essi. L&#39;associazione può essere uno a uno o uno a molti. Ad esempio, possono essere associati più dipendenti a un dipendente. Viene definita associazione uno-molti e rappresentata da 1:n sulla linea che collega gli oggetti del modello dati associati. Tuttavia, se un&#39;associazione restituisce un nome univoco del dipendente per un dato ID dipendente, viene definita associazione uno-a-uno.

Quando si aggiungono oggetti del modello dati associati in un&#39;origine dati a un modello dati del modulo, le relative associazioni vengono mantenute e visualizzate come collegate dalle linee freccia.

In base al caso di utilizzo, creare le seguenti associazioni tra gli oggetti del modello dati:

| Association | Oggetti del modello dati |
|---|---|
| 1:n | cliente:chiamate (più chiamate possono essere associate a un cliente in una fattura mensile) |
| 1:1 | cliente:fatture (una fattura è associata a un cliente per un mese specifico) |

Per creare associazioni tra gli oggetti del modello dati, procedere come segue:

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **cliente** per selezionarlo e toccare **Aggiungi associazione**. Viene visualizzato il riquadro delle proprietà **Aggiungi associazione** .
1. Nel riquadro **Aggiungi associazione** :

   * Specificate un titolo per l&#39;associazione. È un campo facoltativo.
   * Selezionare **Da uno a molti** dall&#39;elenco a discesa **Tipo** .

   * Seleziona **le chiamate** dall&#39;elenco a discesa Oggetto **** modello.

   * Selezionate **Ottieni** dall’elenco a discesa **Servizio** .

   * Toccare **Aggiungi** per collegare l&#39;oggetto modello dati **cliente** all&#39;oggetto modello dati **chiamate** utilizzando una proprietà. In base al caso d&#39;uso, l&#39;oggetto modello dati delle chiamate deve essere collegato alla proprietà numero mobile nell&#39;oggetto modello dati cliente. Viene visualizzata la finestra di dialogo **Aggiungi argomento** .
   ![Aggiungi associazione](assets/add_association_new.png)

1. Nella finestra di dialogo **Aggiungi argomento** :

   * Selezionate **mobilenum** dall’elenco a discesa **Nome** . La proprietà mobile number è una proprietà comune disponibile nel cliente e chiama gli oggetti del modello dati. Di conseguenza, viene utilizzato per creare un&#39;associazione tra gli oggetti del modello dati cliente e chiama quelli del modello dati.
Per ciascun numero mobile disponibile nell&#39;oggetto modello dati cliente, nella tabella delle chiamate sono disponibili più record di chiamate.

   * Specificate un titolo e una descrizione facoltativi per l’argomento.
   * Selezionare **il cliente** dall&#39;elenco a discesa **Binding** a.

   * Selezionare **mobilenum** dall&#39;elenco a discesa Valore **** binding.

   * Toccate **Aggiungi**.
   ![Aggiungi associazione per un argomento](assets/add_association_argument_new.png)

   La proprietà mobilenum viene visualizzata nella sezione **Argomenti** .

   ![Aggiungi associazione di argomenti](assets/add_argument_association_new.png)

1. Toccate **Fine** per creare un&#39;associazione 1:n tra gli oggetti cliente e chiama gli oggetti modello dati.

   Dopo aver creato un&#39;associazione tra gli oggetti modello dati cliente e chiama, creare un&#39;associazione 1:1 tra gli oggetti modello dati cliente e distinta.

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **cliente** per selezionarlo e toccare **Aggiungi associazione**. Viene visualizzato il riquadro delle proprietà **Aggiungi associazione** .
1. Nel riquadro **Aggiungi associazione** :

   * Specificate un titolo per l&#39;associazione. È un campo facoltativo.
   * Selezionare **Uno a Uno** dall&#39;elenco a discesa **Tipo** .

   * Selezionare **fatture** dall&#39;elenco a discesa Oggetto **** modello.

   * Selezionate **Ottieni** dall’elenco a discesa **Servizio** . La proprietà **billplan** , che è la chiave primaria per la tabella delle fatture, è già disponibile nella sezione **Argomenti** .
Gli oggetti delle distinte e del modello dati cliente sono collegati utilizzando rispettivamente le proprietà del piano fatturabile (fatture) e del piano cliente (cliente). Creare un binding tra queste proprietà per recuperare i dettagli del piano per qualsiasi cliente disponibile nel database MySQL.

   * Selezionare **il cliente** dall&#39;elenco a discesa **Binding** a.

   * Selezionare **customerplan** dall&#39;elenco a discesa Valore **** binding.

   * Toccate **Fine** per creare un binding tra le proprietà billplan e customerplan.
   ![Aggiungi associazione per fattura cliente](assets/add_association_customer_bills_new.png)

   Nell&#39;immagine seguente sono illustrate le associazioni tra gli oggetti del modello dati e le proprietà utilizzate per creare associazioni tra di essi:

   ![fdm_associazioni](assets/fdm_associations.gif)

### Modifica delle proprietà dell&#39;oggetto modello dati {#edit-data-model-object-properties}

Dopo aver creato associazioni tra il cliente e altri oggetti modello dati, modificare le proprietà del cliente per definire la proprietà in base alla quale i dati vengono recuperati dall&#39;oggetto modello dati. In base al caso di utilizzo, il numero mobile viene utilizzato come proprietà per recuperare i dati dall&#39;oggetto modello dati cliente.

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **cliente** per selezionarlo e toccare **Modifica proprietà**. Viene visualizzato il riquadro **Modifica proprietà** .
1. Specificare **il cliente** come oggetto **modello di livello** principale.
1. Selezionare **get** dall&#39;elenco a discesa **Read Service** .
1. Nella sezione **Argomenti** :

   * Selezionare **Richiedi attributo** dall&#39;elenco a discesa **Binding** a.

   * Specificare **mobilenum** come valore di binding.

1. Selezionate **Aggiorna** dall&#39;elenco a discesa **Servizio scrittura** .
1. Nella sezione **Argomenti** :

   * Per la proprietà **mobilenum** , selezionare **cliente** dall&#39;elenco a discesa **Binding** a.

   * Selezionare **mobilenum** dall&#39;elenco a discesa Valore **** binding.

1. Toccate **Fine** per salvare le proprietà.

   ![Configurare i servizi](assets/configure_services_customer_new.png)

1. Selezionare la casella di controllo nella parte superiore dell&#39;oggetto modello dati **chiamate** per selezionarlo e toccare **Modifica proprietà**. Viene visualizzato il riquadro **Modifica proprietà** .
1. Disabilitare l&#39;oggetto **Modello di livello** principale per l&#39;oggetto modello dati **chiamate** .
1. Toccate **Chiudi**.

   Ripetere i passaggi da 8 a 10 per configurare le proprietà per l&#39;oggetto modello dati **distinte** .

### Configurare i servizi {#configure-services}

1. Passate alla scheda **Servizi** .
1. Selezionate il servizio **get** e toccate **Modifica proprietà**. Viene visualizzato il riquadro **Modifica proprietà** .
1. Nel riquadro **Modifica proprietà** :

   * Inserite un titolo e una descrizione facoltativi.
   * Selezionare **il cliente** dall&#39;elenco a discesa Oggetto **modello di** output.

   * Toccate **Fine** per salvare le proprietà.
   ![Modifica proprietà](assets/edit_properties_get_details_new.png)

1. Selezionate il servizio di **aggiornamento** e toccate **Modifica proprietà**. Viene visualizzato il riquadro **Modifica proprietà** .
1. Nel riquadro **Modifica proprietà** :

   * Inserite un titolo e una descrizione facoltativi.
   * Selezionare **il cliente** dall&#39;elenco a discesa Oggetto **modello di** input.

   * Toccate **Chiudi**.
   * Toccare **Salva** per salvare il modello dati del modulo.
   ![Aggiorna proprietà servizio](assets/update_service_properties_new.png)

## Passaggio 5: Verifica modello dati modulo e servizi {#step-test-form-data-model-and-services}

È possibile verificare l&#39;oggetto del modello dati e i servizi per verificare che il modello dati del modulo sia configurato correttamente.

Per eseguire il test, effettuate le seguenti operazioni:

1. Fare clic sulla scheda **Modello** , selezionare l&#39;oggetto modello dati **cliente** e toccare Oggetto **modello** test.
1. Nella finestra **Prova modello** dati modulo, selezionare **Leggi oggetto** modello dall&#39;elenco a discesa **Seleziona modello/servizio** .
1. Nella sezione **Input** , specificate un valore per la proprietà **mobilenum** presente nel database MySQL configurato e toccate **Test**.

   I dettagli del cliente associati alla proprietà mobilenum specificata vengono recuperati e visualizzati nella sezione Output come illustrato di seguito. Chiudete la finestra di dialogo.

   ![Test del modello dati](assets/test_data_model_new.png)

1. Passate alla scheda **Servizi** .
1. Selezionate il servizio **get** e toccate **Test Service.**
1. Nella sezione **Input** , specificate un valore per la proprietà **mobilenum** presente nel database MySQL configurato e toccate **Test**.

   I dettagli del cliente associati alla proprietà mobilenum specificata vengono recuperati e visualizzati nella sezione Output come illustrato di seguito. Chiudete la finestra di dialogo.

   ![Servizio di prova](assets/test_service_new.png)

### Modificare e salvare i dati di esempio {#edit-and-save-sample-data}

L&#39;editor dei modelli di dati modulo consente di generare dati di esempio per tutte le proprietà degli oggetti del modello di dati, incluse le proprietà calcolate, in un modello di dati del modulo. Si tratta di un insieme di valori casuali conformi al tipo di dati configurato per ciascuna proprietà. È inoltre possibile modificare e salvare i dati, che vengono conservati anche se si rigenerano i dati di esempio.

Per generare, modificare e salvare dati di esempio, effettuate le seguenti operazioni:

1. Nella pagina del modello dati del modulo, toccare **Modifica dati** di esempio. Genera e visualizza i dati di esempio nella finestra Modifica dati campione.

   ![Modifica dei dati di esempio](assets/edit_sample_data_new.png)

1. Nella finestra **Modifica dati** di esempio, modificare i dati in base alle esigenze e toccare **Salva**. Chiudi la finestra.


