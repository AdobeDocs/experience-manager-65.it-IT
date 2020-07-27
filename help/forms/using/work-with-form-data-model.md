---
title: Uso del modello dati del modulo
seo-title: Uso del modello dati del modulo
description: Integrazione dei dati fornisce l'editor del modello dati del modulo per configurare e utilizzare i modelli di dati del modulo.
seo-description: Integrazione dei dati fornisce l'editor del modello dati del modulo per configurare e utilizzare i modelli di dati del modulo.
uuid: ed78f7f7-8123-4778-9252-89924cec09d6
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c47ef627-261e-4b4b-8846-873d3d84234b
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '4102'
ht-degree: 0%

---


# Uso del modello dati del modulo{#work-with-form-data-model}

![](do-not-localize/data-integeration.png)

L&#39;editor dei modelli di dati per i moduli offre un&#39;interfaccia utente intuitiva e strumenti per la modifica e la configurazione di un modello di dati per i moduli. Utilizzando l&#39;editor, è possibile aggiungere e configurare oggetti, proprietà e servizi del modello dati da origini dati associate nel modello dati del modulo. Inoltre, consente di creare oggetti e proprietà del modello dati senza origini dati e di eseguire successivamente un binding con i rispettivi oggetti e proprietà del modello dati. È inoltre possibile generare e modificare dati di esempio per le proprietà degli oggetti del modello dati che è possibile utilizzare per precompilare moduli adattivi e comunicazioni interattive durante la visualizzazione dell&#39;anteprima. È possibile sottoporre a test gli oggetti e i servizi del modello dati configurati in un modello dati del modulo per assicurarsi che sia correttamente integrato con le origini dati.

Se non si è esperti nell&#39;integrazione dei dati di Forms e non si è configurata un&#39;origine dati o non è stato creato un modello di dati del modulo, consultare i seguenti argomenti:

* [Integrazione dei dati AEM Forms](/help/forms/using/data-integration.md)
* [Configurare le origini dati](/help/forms/using/configure-data-sources.md)
* [Crea modello dati modulo](/help/forms/using/create-form-data-models.md)

Per informazioni dettagliate sulle varie attività e configurazioni che è possibile eseguire utilizzando l&#39;editor modelli dati del modulo, consultare.

>[!NOTE]
>
>È necessario essere membri sia dei gruppi **fdm-author** che **form-user** per poter creare e utilizzare il modello dati del modulo. Contatta il tuo amministratore AEM per diventare membro dei gruppi.

## Aggiunta di oggetti e servizi del modello dati {#add-data-model-objects-and-services}

Se si è creato un modello dati modulo con origini dati, è possibile utilizzare l&#39;editor modelli dati modulo per aggiungere oggetti e servizi del modello dati, configurarne le proprietà, creare associazioni tra gli oggetti del modello dati e verificare il modello dati e i servizi del modulo.

È possibile aggiungere oggetti e servizi del modello dati da origini dati disponibili nel modello dati del modulo. Mentre gli oggetti modello dati aggiunti vengono visualizzati nella scheda Modello, i servizi aggiunti vengono visualizzati nella scheda Servizi.

Per aggiungere oggetti e servizi del modello dati:

1. Accedi all’istanza di creazione di AEM, passa a **[!UICONTROL Forms > Integrazioni]** dati e apri il modello dati del modulo in cui desideri aggiungere oggetti del modello dati.
1. Nel riquadro Origini dati espandere le origini dati per visualizzare gli oggetti e i servizi del modello dati disponibili.
1. Selezionare gli oggetti del modello dati e i servizi che si desidera aggiungere al modello dati del modulo e toccare **[!UICONTROL Aggiungi selezionato]**.

   ![selected-objects](assets/selected-objects.png)

   Oggetti e servizi del modello dati selezionati

   La scheda Modello visualizza una rappresentazione grafica di tutti gli oggetti del modello dati e delle relative proprietà aggiunte al modello dati del modulo. Ciascun oggetto del modello dati è rappresentato da una casella nel modello dati del modulo.

   ![model-tab](assets/model-tab.png)

   Scheda Modello visualizza oggetti modello dati aggiunti

   >[!NOTE]
   >
   >È possibile tenere premuti e trascinare i riquadri oggetti del modello dati per organizzarli nell&#39;area contenuto. Tutti gli oggetti del modello dati aggiunti nel modello dati del modulo sono disabilitati nel riquadro Origini dati.

   Nella scheda Servizi sono elencati i servizi aggiunti.

   ![services-tab](assets/services-tab.png)

   La scheda Servizi visualizza i servizi del modello dati

   >[!NOTE]
   >
   >Oltre agli oggetti e ai servizi del modello dati, il documento di metadati del servizio OData include proprietà di navigazione che definiscono l&#39;associazione tra due oggetti del modello dati. Per ulteriori informazioni, vedere [Uso delle proprietà di navigazione dei servizi](#navigation-properties-odata)OData.

1. Toccare **[!UICONTROL Salva]** per salvare l&#39;oggetto modello di modulo.

   >[!NOTE]
   >
   >È possibile richiamare i servizi configurati nella scheda Servizi di un modello dati modulo utilizzando le regole del modulo adattivo. I servizi configurati sono disponibili nell&#39;azione di attivazione dei servizi dell&#39;editor delle regole. Per ulteriori informazioni sull&#39;utilizzo di questi servizi nelle regole dei moduli adattivi, vedere Invocare servizi e Impostare il valore delle regole nell&#39;editor [delle](/help/forms/using/rule-editor.md)regole.

## Creazione di oggetti modello dati e proprietà figlio {#create-data-model-objects-and-child-properties}

### Creazione di oggetti modello dati {#create-data-model-objects}

Anche se è possibile aggiungere oggetti modello dati da origini dati configurate, è anche possibile creare oggetti modello dati o entità senza origini dati. È utile soprattutto se non sono state configurate origini dati nel modello dati del modulo.

Per creare un oggetto modello dati senza origini dati:

1. Accedi all’istanza di creazione di AEM, passa a **[!UICONTROL Forms > Integrazioni]** dati e apri il modello dati del modulo in cui vuoi creare un oggetto o un’entità del modello dati.
1. Toccate **[!UICONTROL Crea entità]**.
1. Nella finestra di dialogo Crea modello dati, specificare un nome per l&#39;oggetto modello dati e toccare **[!UICONTROL Aggiungi]**. Un oggetto modello dati viene aggiunto al modello dati del modulo. L&#39;oggetto modello dati appena aggiunto non è associato a un&#39;origine dati e non dispone di proprietà come illustrato nell&#39;immagine seguente.

   ![nuova entità](assets/new-entity.png)

È quindi possibile aggiungere proprietà figlio negli oggetti modello dati non associati.

### Aggiungi proprietà figlio {#child-properties}

L&#39;editor dei modelli di dati modulo consente di creare proprietà figlio in un oggetto modello dati. La proprietà creata non è associata ad alcuna proprietà in un&#39;origine dati. In seguito è possibile eseguire un binding della proprietà figlia con un&#39;altra proprietà nell&#39;oggetto del modello dati contenitore.

Per creare una proprietà figlio:

1. In un modello dati modulo, selezionare un oggetto modello dati e toccare **[!UICONTROL Crea proprietà]** figlio.
1. Nella finestra di dialogo **[!UICONTROL Crea proprietà]** figlio, specificate un nome e un tipo di dati per la proprietà rispettivamente nei campi **[!UICONTROL Nome]** e **[!UICONTROL Tipo]** . Facoltativamente è possibile specificare un titolo e una descrizione per la proprietà.
1. Abilitare Computed se la proprietà è una proprietà calcolata. Il valore di una proprietà calcolata viene valutato in base a una regola o un&#39;espressione. Per ulteriori informazioni, vedere [Modificare le proprietà](#edit-properties).
1. Se l&#39;oggetto del modello dati è associato a un&#39;origine dati, la proprietà figlia aggiunta viene automaticamente associata alla proprietà dell&#39;oggetto modello dati padre con lo stesso nome e tipo di dati.

   Per eseguire un binding manuale di una proprietà figlia con una proprietà oggetto modello dati, toccare l&#39;icona Sfoglia accanto al campo Riferimento **** binding. Nella finestra di dialogo **[!UICONTROL Seleziona oggetto]** sono elencate tutte le proprietà dell&#39;oggetto modello dati principale. Selezionare una proprietà con cui eseguire il binding e toccare l&#39;icona del segno di spunta. È possibile selezionare solo una proprietà dello stesso tipo di dati della proprietà figlio.

1. Toccate **[!UICONTROL Fine]** per salvare la proprietà figlio e toccate **[!UICONTROL Salva]** per salvare il modello dati del modulo. La proprietà figlio viene ora aggiunta all&#39;oggetto modello dati.

Dopo aver creato oggetti e proprietà del modello dati, è possibile continuare a creare moduli adattivi e comunicazioni interattive basate sul modello dati del modulo. Successivamente, quando sono disponibili e configurate origini dati, è possibile eseguire il binding del modello dati del modulo con origini dati. Il binding viene aggiornato automaticamente nei moduli adattivi associati e nelle comunicazioni interattive. Per ulteriori informazioni sulla creazione di moduli adattivi e sulle comunicazioni interattive mediante il modello dati del modulo, vedere [Uso del modello](/help/forms/using/using-form-data-model.md)dati del modulo.

### Binding di oggetti del modello dati e proprietà {#bind-data-model-objects-and-properties}

Quando sono disponibili le origini dati che si desidera integrare con il modello dati del modulo, è possibile aggiungerle al modello dati del modulo come descritto in [Aggiorna origini](/help/forms/using/create-form-data-models.md#update)dati. Quindi, eseguire le operazioni seguenti per eseguire il binding degli oggetti e delle proprietà del modello dati non associati:

1. Nel modello dati del modulo, selezionare l&#39;origine dati non associata che si desidera associare a un&#39;origine dati.
1. Toccate **[!UICONTROL Modifica proprietà]**.
1. Nel riquadro **[!UICONTROL Modifica proprietà]** , toccare l&#39;icona Sfoglia accanto al campo **[!UICONTROL Binding]** . Si apre la finestra di dialogo **[!UICONTROL Seleziona oggetto]** in cui sono elencate le origini dati aggiunte nel modello dati del modulo.

   ![select-object](assets/select-object.png)

1. Espandere la struttura delle origini dati e selezionare un oggetto modello dati con cui eseguire il binding e toccare l&#39;icona di spunta.
1. Toccate **[!UICONTROL Fine]** per salvare le proprietà, quindi toccate **[!UICONTROL Salva]** per salvare il modello dati del modulo. L&#39;oggetto del modello dati è ora associato a un&#39;origine dati. Tenere presente che l&#39;oggetto del modello dati non è più contrassegnato come Non associato.

   ![bound-model-object](assets/bound-model-object.png)

## Configurare i servizi {#configure-services}

Per leggere e scrivere i dati per un oggetto modello dati, effettuare le seguenti operazioni per configurare i servizi di lettura e scrittura:

1. Selezionare la casella di controllo nella parte superiore di un oggetto modello dati per selezionarlo e toccare **[!UICONTROL Modifica proprietà]**.

   ![edit-properties](assets/edit-properties.png)

   Modifica delle proprietà per configurare i servizi di lettura e scrittura per un oggetto modello dati

   Viene visualizzata la finestra di dialogo Modifica proprietà.

   ![edit-properties-2](assets/edit-properties-2.png)

   Finestra di dialogo Modifica proprietà

   >[!NOTE]
   >
   >Oltre agli oggetti e ai servizi del modello dati, il documento di metadati del servizio OData include proprietà di navigazione che definiscono l&#39;associazione tra due oggetti del modello dati. Quando si aggiunge un&#39;origine dati del servizio OData a un modello dati modulo, è disponibile un servizio nel modello dati modulo per tutte le proprietà di navigazione in un oggetto modello dati. È possibile utilizzare questo servizio per leggere le proprietà di navigazione dell&#39;oggetto modello dati corrispondente.
   >
   >
   >Per ulteriori informazioni sull&#39;utilizzo del servizio, vedere [Uso delle proprietà di navigazione dei servizi](#navigation-properties-odata)OData.

1. Attiva/disattiva l&#39;oggetto **[!UICONTROL di livello]** superiore per specificare se l&#39;oggetto del modello dati è un oggetto modello di livello principale.

   Gli oggetti del modello dati configurati in un modello dati del modulo sono disponibili per l&#39;uso nella scheda Oggetti modello dati del browser Contenuto di un modulo adattivo basato sul modello dati del modulo. Quando si aggiunge un&#39;associazione tra due oggetti modello dati, l&#39;oggetto modello dati a cui si sta associando è nidificato sotto l&#39;oggetto modello dati da cui si sta associando nella scheda Oggetti modello dati. Se il modello dati nidificato è un oggetto di primo livello, verrà visualizzato anche separatamente nella scheda Oggetti modello dati. Di conseguenza, verranno visualizzate due voci di esso, una all&#39;interno e l&#39;altra all&#39;esterno della gerarchia nidificata, che potrebbero confondere gli autori dei moduli. Per fare in modo che l&#39;oggetto del modello dati associato venga visualizzato solo nella gerarchia nidificata, disabilitare la proprietà Oggetto di primo livello.

1. Selezionare Servizi di lettura e scrittura per gli oggetti del modello dati selezionati. Vengono visualizzati gli argomenti relativi ai servizi.

   ![servizi di lettura/scrittura](assets/read-write-services.png)

   Servizi di lettura e scrittura configurati per l&#39;origine dati dipendente

1. Toccate ![aem_6_3_edit](assets/aem_6_3_edit.png) per l&#39;argomento del servizio di lettura per [associare l&#39;argomento a un attributo di profilo utente, un attributo di richiesta o un valore](#bindargument) letterale e specificate il valore di binding.
1. Toccare **[!UICONTROL Fine]** per salvare l&#39;argomento, **[!UICONTROL Fine]** per salvare le proprietà, quindi **[!UICONTROL Salva]** per salvare il modello dati del modulo.

### Binding degli argomenti del servizio di lettura {#bindargument}

Associare l&#39;argomento del servizio di lettura a un attributo di profilo utente, un attributo di richiesta o un valore letterale in base a un valore di binding. Il valore viene passato al servizio come argomento per recuperare i dettagli associati al valore specificato dall&#39;origine dati.

#### Literal value {#literal-value}

Selezionare **[!UICONTROL Letterale]** dal menu a discesa **[!UICONTROL Binding a]** e immettere un valore nel campo Valore **** binding. I dettagli associati al valore vengono recuperati dall&#39;origine dati. Utilizzare questa opzione per recuperare i dettagli associati a un valore statico.

In questo esempio, i dettagli associati con **4367655678**, come valore per l&#39; `mobilenum` argomento, vengono recuperati dall&#39;origine dati. I dettagli associati se trasmettete il valore per un argomento relativo al numero di cellulare possono includere proprietà quali il nome del cliente, l&#39;indirizzo del cliente e la città.

![Valore letterale](assets/fdm_binding_literal_new.png)

#### Attributo profilo utente {#user-profile-attribute}

Selezionare Attributo **[!UICONTROL profilo]** utente dal menu a discesa **[!UICONTROL Binding a]** e immettere il nome dell&#39;attributo nel campo Valore **** binding. I dettagli dell’utente che ha eseguito l’accesso all’istanza di AEM vengono recuperati dall’origine dati in base al nome dell’attributo.

Il nome dell&#39;attributo specificato nel campo Valore **** di binding deve includere il percorso di binding completo fino al nome dell&#39;attributo per l&#39;utente. Aprite il seguente URL per accedere ai dettagli utente su CRXDE:

https://&lt;nome-server>:&lt;numero porta>/crx/de/index.jsp#/home/users/

![Profilo utente](assets/binding_crxde_user_profile_new.png)

In questo esempio, specificare `profile.empid` nel campo **[!UICONTROL Valore]** di binding per l&#39; `grios` utente.

![Modifica argomento](assets/edit_argument_user_profile_new.png)

L&#39; `id` argomento prende il valore dell&#39; `empid` attributo del profilo utente e lo trasmette come argomento al servizio di lettura. Legge e restituisce valori delle proprietà associate dall&#39;oggetto modello dati dipendente per l&#39;utente `empid` associato all&#39;utente connesso.

#### Richiedi attributo {#request-attribute}

Utilizzare l&#39;attributo request per recuperare le proprietà associate dall&#39;origine dati.

1. Selezionare **[!UICONTROL Richiedi attributo]** dal menu a discesa **[!UICONTROL Binding a]** e immettere il nome dell&#39;attributo nel campo Valore **** binding.

1. Aprite head.jsp per definire i dettagli attributo su CRXDE:\
   `https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`

1. Includete il testo seguente nel file head.jsp:

   ```jsp
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);%>
   ```

I dettagli vengono recuperati dall&#39;origine dati in base al nome attributo specificato nella richiesta.

Ad esempio, specificando l&#39;attributo come `petid=100` nella richiesta, si recupereranno dall&#39;origine dati le proprietà associate al valore dell&#39;attributo.

## Aggiungi associazioni {#add-associations}

In genere, esistono associazioni create tra gli oggetti del modello dati in un&#39;origine dati. L&#39;associazione può essere uno a uno o uno a molti. Ad esempio, possono essere associati più dipendenti a un dipendente. Viene definita associazione uno-a-molti e rappresentata dalla linea che collega `1:n` gli oggetti del modello dati associati. Tuttavia, se un&#39;associazione restituisce un nome univoco del dipendente per un dato ID dipendente, viene definita associazione uno-a-uno.

Quando si aggiungono oggetti del modello dati associati in un&#39;origine dati a un modello dati del modulo, le relative associazioni vengono mantenute e visualizzate come collegate dalle linee freccia. È possibile aggiungere associazioni tra gli oggetti del modello dati attraverso origini dati diverse in un modello dati del modulo.

>[!NOTE]
>
>Le associazioni predefinite in un&#39;origine dati JDBC non vengono mantenute nel modello dati del modulo. È necessario crearli manualmente.

Per aggiungere un&#39;associazione:

1. Selezionare la casella di controllo nella parte superiore di un oggetto modello dati per selezionarlo e toccare **[!UICONTROL Aggiungi associazione]**. Viene visualizzata la finestra di dialogo Aggiungi associazione.

   ![add-Association](assets/add-association.png)

   >[!NOTE]
   >
   >Oltre agli oggetti e ai servizi del modello dati, il documento di metadati del servizio OData include proprietà di navigazione che definiscono l&#39;associazione tra due oggetti del modello dati. È possibile utilizzare queste proprietà di navigazione quando si aggiungono associazioni nel modello dati modulo. Per ulteriori informazioni, vedere [Uso delle proprietà di navigazione dei servizi](#navigation-properties-odata)OData.

   Viene visualizzata la finestra di dialogo Aggiungi associazione.

   ![add-Association-2](assets/add-association-2.png)

   Aggiungi associazione, finestra di dialogo

1. Nel riquadro Aggiungi associazione:

   * Specificate un titolo per l&#39;associazione.
   * Selezionare il tipo di associazione — Da uno a uno o da uno a molti.
   * Selezionare l&#39;oggetto del modello dati a cui associarsi.
   * Selezionare il servizio di lettura per leggere i dati dall&#39;oggetto modello selezionato. Viene visualizzato l&#39;argomento del servizio di lettura. Modificare l&#39;argomento, se necessario, e associarlo alla proprietà dell&#39;oggetto modello dati da associare.

   Nell&#39;esempio seguente, l&#39;argomento predefinito per il servizio di lettura dell&#39;oggetto modello dati Dependents è `dependentid`.

   ![add-Association-example](assets/add-association-example.png)

   L&#39;argomento predefinito per il servizio di lettura Dipendenti è Dependentid

   Tuttavia, l&#39;argomento deve essere una proprietà comune tra l&#39;oggetto del modello dati associato, che in questo esempio è `Employeeid`. Pertanto, l&#39; `Employeeid` argomento deve essere associato alla `id` proprietà dell&#39;oggetto del modello dati Dipendente per recuperare i dettagli relativi ai dipendenti associati dall&#39;oggetto del modello dati Dipendenti.

   ![add-Association-example-2](assets/add-association-example-2.png)

   Argomento e binding aggiornati

   Toccate **[!UICONTROL Fine]** per salvare l’argomento.

1. Toccate **[!UICONTROL Fine]** per salvare l&#39;associazione, quindi **[!UICONTROL Salva]** per salvare il modello dati del modulo.
1. Ripetere i passaggi per creare ulteriori associazioni come necessario.

>[!NOTE]
>
>L&#39;associazione aggiunta viene visualizzata nella casella dell&#39;oggetto modello dati con il titolo specificato e una linea che collega gli oggetti del modello dati associati.
>
>Per modificare un&#39;associazione, selezionate la casella di controllo e toccate **[!UICONTROL Modifica associazione]**.

![associazione](assets/added-association.png)

## Modifica delle proprietà {#properties}

È possibile modificare le proprietà degli oggetti del modello dati, le relative proprietà e i servizi aggiunti nel modello dati del modulo.

Per modificare le proprietà:

1. Selezionare la casella di controllo accanto a un oggetto del modello dati, a una proprietà o a un servizio nel modello dati del modulo.
1. Toccate **[!UICONTROL Modifica proprietà]**. Viene visualizzato il riquadro **[!UICONTROL Modifica proprietà]** per l&#39;oggetto modello, la proprietà o il servizio selezionato.

   * **Oggetto** del modello dati: Specificare i servizi di lettura e scrittura e gli argomenti di modifica.
   * **Proprietà**: Specificare il tipo, il sottotipo e il formato della proprietà. È inoltre possibile specificare se la proprietà selezionata è la chiave primaria per l&#39;oggetto modello dati.
   * **Servizio**: Specificare l&#39;oggetto del modello di input, il tipo di output e gli argomenti per il servizio. Per un servizio Get, potete specificare se deve restituire un array.

   ![edit-properties-service](assets/edit-properties-service.png)

   Finestra di dialogo Modifica proprietà per un servizio get

1. Toccare **[!UICONTROL Fine]** per salvare le proprietà, quindi **[!UICONTROL Salva]** per salvare il modello dati del modulo.

### Creare proprietà calcolate {#computed}

Una proprietà calcolata è quella il cui valore viene calcolato in base a una regola o un&#39;espressione. Utilizzando una regola, è possibile impostare il valore di una proprietà calcolata su una stringa letterale, un numero, il risultato di un&#39;espressione matematica o il valore di un&#39;altra proprietà nel modello dati del modulo.

Ad esempio, è possibile creare una proprietà calcolata **FullName** il cui valore è il risultato della concatenazione delle proprietà esistenti **FirstName** e **LastName** . A questo scopo:

1. Creare una nuova proprietà con il nome `FullName` il cui tipo di dati è String.
1. Attivate **[!UICONTROL Calcolato]** e toccate **[!UICONTROL Fine]** per creare la proprietà.

   ![calcolato](assets/computed.png)

   Viene creata la proprietà calcolata FullName. Osservate l&#39;icona accanto alla proprietà per rappresentare una proprietà calcolata.

   ![computed-prop](assets/computed-prop.png)

1. Selezionate la proprietà FullName e toccate **[!UICONTROL Modifica regola]**. Si apre una finestra dell&#39;editor di regole.
1. Nella finestra Editor regole, toccate **[!UICONTROL Crea]**. Viene visualizzata la finestra **[!UICONTROL Imposta regola valore]** .

   Dal menu a discesa Seleziona opzione, selezionate Espressione **** matematica. Altre opzioni disponibili sono Oggetto **[!UICONTROL modello dati]** modulo e **[!UICONTROL Stringa]**.

1. Nell&#39;espressione matematica, selezionare **[!UICONTROL FirstName]** e **[!UICONTROL LastName]** rispettivamente nel primo e nel secondo oggetto. Selezionare **[!UICONTROL più]** come operatore.

   Toccate **[!UICONTROL Fine]** e quindi **[!UICONTROL Chiudi]** per chiudere la finestra dell&#39;editor di regole. La regola ha un aspetto simile al seguente.

   ![regola](assets/rule.png)

1. Nel modello dati del modulo, toccare **[!UICONTROL Salva]**. La proprietà computed è configurata.

## Operazioni con le proprietà di navigazione dei servizi OData {#work-with-navigation-properties-of-odata-services}

Nei servizi OData, le proprietà di navigazione vengono utilizzate per definire le associazioni tra due oggetti modello dati. Tali proprietà sono definite in un tipo di entità o in un tipo complesso. Ad esempio, nel seguente estratto dal file di metadati dei servizi di esempio di [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData, l&#39;entità persona contiene tre proprietà di navigazione: Amici, Migliori amici e Viaggi.

Per ulteriori informazioni sulle proprietà di navigazione, consulta la documentazione [](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)OData.

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

Quando si configura un servizio OData in un modello dati modulo, tutte le proprietà di navigazione in un contenitore entità vengono rese disponibili tramite un servizio nel modello dati modulo. In questo esempio di servizio TripPin OData, le tre proprietà di navigazione nel contenitore `Person` entità possono essere lette utilizzando un `GET LINK` servizio nel modello dati modulo.

Di seguito viene evidenziato il `GET LINK of Person /People` servizio nel modello dati modulo, che è un servizio combinato per le tre proprietà di navigazione nell&#39; `Person` entità del servizio TripPin OData.

![nav-prop-service](assets/nav-prop-service.png)

Dopo aver aggiunto il `GET LINK` servizio alla scheda Servizi nel modello dati modulo, è possibile modificare le proprietà per scegliere l&#39;oggetto modello di output e la proprietà di navigazione da utilizzare nel servizio. Ad esempio, il seguente `GET LINK of Person /People` servizio nell&#39;esempio seguente utilizza Trip come oggetto modello di output e la proprietà di navigazione come Trips.

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>I valori disponibili nel campo Valore **** predefinito dell&#39;argomento **NavigationPropertyName** dipendono dallo stato dell&#39;array **Return?** pulsante di attivazione/disattivazione. Quando è attivato, mostra le proprietà di navigazione del tipo Collection.

In questo esempio, è anche possibile scegliere l&#39;oggetto modello di output come argomento Persona e proprietà di navigazione come Amici o Migliore amico (a seconda se array **Return?** è abilitata o disabilitata).

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

Allo stesso modo, è possibile scegliere un `GET LINK` servizio e configurarne le proprietà di navigazione quando si aggiungono associazioni nel modello dati modulo. Tuttavia, per poter selezionare una proprietà di navigazione, assicurarsi che il campo **** Binding a sia impostato su **Letterale**.

![add-Association-nav-prop](assets/add-association-nav-prop.png)

## Generazione e modifica di dati di esempio {#sample}

L&#39;editor dei modelli di dati modulo consente di generare dati di esempio per tutte le proprietà degli oggetti del modello di dati, incluse le proprietà calcolate, in un modello di dati del modulo. Si tratta di un insieme di valori casuali conformi al tipo di dati configurato per ciascuna proprietà. È inoltre possibile modificare e salvare i dati, che vengono conservati anche se si rigenerano i dati di esempio.

Per generare e modificare dati di esempio, effettuate le seguenti operazioni:

1. Aprire un modello dati del modulo e toccare **[!UICONTROL Modifica dati]** di esempio. Genera e visualizza i dati di esempio nella finestra Modifica dati di esempio.

   ![Genera dati di esempio](assets/form_data_model_generate_sample_data_new.png)

1. Nella finestra **[!UICONTROL Modifica dati]** di esempio, modificare i dati in base alle esigenze e toccare **[!UICONTROL Salva]**.

È quindi possibile utilizzare i dati di esempio per precompilare e testare le comunicazioni interattive basate sul modello di dati del modulo. Per ulteriori informazioni, vedere [Uso del modello](/help/forms/using/using-form-data-model.md)dati del modulo.

## Test di oggetti e servizi del modello dati {#test-data-model-objects-and-services}

Il modello dati del modulo è configurato, ma prima di utilizzarlo, potrebbe essere necessario verificare se gli oggetti e i servizi del modello dati configurati funzionano come previsto. Per verificare gli oggetti e i servizi del modello dati:

1. Selezionare un oggetto modello dati o un servizio nel modello dati del modulo e toccare, rispettivamente, Oggetto **[!UICONTROL modello di]** prova o Servizio **[!UICONTROL di]** prova.

   Viene visualizzata la finestra Modello dati modulo di prova.

   ![test-data-model](assets/test-data-model.png)

1. Nella finestra Modello dati modulo di prova, selezionare l&#39;oggetto o il servizio del modello dati da verificare dal riquadro Input.

1. Specificate un valore di argomento nel codice di prova e toccate **[!UICONTROL Test]**. Un test di successo restituisce l&#39;output nel riquadro Output.

   ![Risultati della prova](assets/test_results_form_data_model_new.png)

Allo stesso modo, è possibile verificare altri oggetti e servizi del modello dati nel modello dati del modulo.

## Convalida automatizzata dei dati di input {#automated-validation-of-input-data}

Il modello dati del modulo convalida i dati ricevuti come input durante la chiamata dell&#39;API DermisBridge (in base ai criteri di convalida disponibili nel modello dati del modulo). La convalida si basa sul `ValidationOptions` flag impostato nell&#39;oggetto query utilizzato per richiamare l&#39;API.

Il flag può essere impostato su uno dei seguenti valori:

* **COMPLETO**: FDM esegue la convalida in base a tutti i vincoli
* **OFF**: Nessuna convalida
* **BASE**: FDM esegue la convalida in base ai vincoli &quot;obbligatori&quot; e &quot;nullable&quot;

Se non viene impostato alcun valore per il `ValidationOptions`flag, ai dati di input viene eseguita la convalida **BASIC** .

Di seguito è riportato un esempio di impostazione del flag di convalida su **FULL**:

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>Il valore fornito per un attributo nei dati di input deve corrispondere al tipo di dati definito per l&#39;attributo nel documento di metadati.\
>Se il valore non corrisponde al tipo di dati definito per l&#39;attributo, l&#39;API DermisBridge visualizza un&#39;eccezione indipendentemente dal valore del `ValidationOptions` flag. Se il livello di registro è impostato su Debug, viene registrato un errore nel file **error.log** .

Il modello dati del modulo convalida i dati di input in base a un elenco di vincoli relativi al tipo di dati. L&#39;elenco di vincoli per i dati di input può variare in base all&#39;origine dati.

Nella tabella seguente sono elencati i vincoli per i dati di input basati sull&#39;origine dati:

<table>
 <tbody> 
  <tr> 
   <td>Vincoli</td> 
   <td>Descrizione</td> 
   <td>Origine dati di input</td> 
  </tr> 
  <tr> 
   <td>required</td> 
   <td>Se true, il parametro deve essere incluso nei dati di input.</td> 
   <td>Swagger, WSDL e database</td> 
  </tr> 
  <tr> 
   <td>nullable</td> 
   <td>Se true, il valore del parametro può essere impostato su Null nei dati di input.</td> 
   <td>WSDL, Odata e database</td> 
  </tr> 
  <tr> 
   <td>massimo</td> 
   <td>Specifica il limite superiore per i valori numerici. Il valore massimo specificato come limite superiore può essere assegnato anche al parametro nei dati di input.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>minimo</td> 
   <td>Specifica il limite inferiore per i valori numerici. Il valore minimo specificato come limite inferiore può essere assegnato anche al parametro nei dati di input.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>excludeMaximum</td> 
   <td>Specifica il limite superiore per i valori numerici. Il valore massimo specificato come limite superiore non deve essere assegnato al parametro nei dati di input.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>excludeMinimum</td> 
   <td>Specifica il limite inferiore per i valori numerici. Il valore minimo specificato come limite inferiore non deve essere assegnato al parametro nei dati di input.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>Specifica il limite inferiore per il numero di caratteri inclusi in una stringa. Il valore minimo specificato come limite inferiore può essere assegnato anche al parametro nei dati di input.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>Specifica il limite superiore per il numero di caratteri inclusi in una stringa. Il valore massimo specificato come limite superiore può essere assegnato anche al parametro nei dati di input.</td> 
   <td>Swagger, WSDL, Odata e database</td> 
  </tr> 
  <tr> 
   <td>pattern</td> 
   <td>Specifica una sequenza fissa di caratteri. La stringa di input viene convalidata correttamente solo se i caratteri sono conformi al pattern specificato.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>Specifica il numero minimo di elementi in una matrice. Il valore minimo specificato come limite inferiore può essere assegnato anche al parametro nei dati di input.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>Specifica il numero massimo di elementi in una matrice. Il valore massimo specificato come limite superiore può essere assegnato anche al parametro nei dati di input.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>UniqueItems</td> 
   <td>Se true, tutti gli elementi dell'array devono essere univoci nei dati di input.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>enum (stringa)<br /> <br /> </td> 
   <td>Limita il valore di un parametro nei dati di input a un insieme fisso di valori stringa. Deve essere un array con almeno un elemento, dove ogni elemento è univoco.</td> 
   <td>Swagger, WSDL e Odata</td> 
  </tr> 
  <tr> 
   <td>enum (numero)<br /> <br /> </td> 
   <td>Limita il valore di un parametro nei dati di input a un insieme fisso di valori numerici. Deve essere un array con almeno un elemento, dove ogni elemento è univoco.</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

In questo esempio, i dati di input vengono convalidati in base ai vincoli massimi, minimi e obbligatori definiti nel file Swagger. I dati di input soddisfano i criteri di convalida solo se l&#39;ID ordine è presente e il suo valore è compreso tra 1 e 10.

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that needs to be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

Se i dati di input non soddisfano i criteri di convalida, viene visualizzata un&#39;eccezione. Se il livello di registro è impostato su **Debug**, viene registrato un errore nel file **error.log** . Ad esempio,

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## Passaggi successivi {#next-steps}

È disponibile un modello dati modulo di lavoro che è ora pronto per essere utilizzato nei moduli adattivi e nei flussi di lavoro di comunicazione interattiva. Per ulteriori informazioni, vedere [Uso del modello](/help/forms/using/using-form-data-model.md)dati del modulo.
