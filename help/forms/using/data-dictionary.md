---
title: Dizionario dati
seo-title: Data Dictionary
description: Il dizionario dati in Gestione corrispondenza consente di integrare i dati back-end alle lettere come input da utilizzare nella corrispondenza del cliente.
seo-description: Data dictionary in Correspondence Management lets you integrate back-end data to letters as inputs for use in customer correspondence.
uuid: 178a285e-b4a4-4a36-a2aa-b43ecb0871ed
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a1a0ad6b-023a-4822-9cce-0618657c3f9d
docset: aem65
feature: Correspondence Management
exl-id: aaed75e6-8849-46a8-b986-896ad729adda
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3838'
ht-degree: 1%

---

# Dizionario dati{#data-dictionary}

## Introduzione {#introduction}

Un dizionario dati consente agli utenti aziendali di utilizzare informazioni provenienti da origini dati back-end senza conoscere i dettagli tecnici relativi ai modelli di dati sottostanti. Un dizionario dati è composto da elementi del dizionario dati (DDE). Puoi utilizzare questi elementi dati per integrare i dati back-end alle lettere come input da utilizzare nella corrispondenza di un cliente.

Un dizionario dati è una rappresentazione indipendente di metadati che descrive le strutture di dati sottostanti e gli attributi associati. Un dizionario dati viene creato utilizzando un vocabolario aziendale. Può essere mappato su uno o più modelli di dati sottostanti.

Il dizionario dati è composto da elementi di tre tipi: Elementi semplici, compositi e di raccolta. I DDE semplici sono elementi primitivi quali stringhe, numeri, date e valori booleani che contengono informazioni quali il nome di una città. Un DDE composito contiene altri DDE, che possono essere di tipo primitivo, composito o raccolta. Ad esempio, un indirizzo, costituito da un indirizzo, una città, una provincia, un paese e un codice postale. Una raccolta è un elenco di DDE semplici o composte simili. Ad esempio, un cliente con più posizioni o diversi indirizzi di fatturazione e spedizione.

Gestione della corrispondenza utilizza i dati back-end, cliente o destinatari specifici memorizzati in base alla struttura del dizionario dati per creare una corrispondenza destinata a clienti diversi. Ad esempio, è possibile creare un documento con nomi descrittivi, ad esempio &quot;Gentile {Nome}&quot;,&quot;Sig. {Cognome}&quot;.

In genere, gli utenti aziendali non richiedono la conoscenza delle rappresentazioni dei metadati come XSD (schema XML) e le classi Java. Tuttavia, in genere richiedono l&#39;accesso a queste strutture di dati e attributi per creare soluzioni.

### Flusso di lavoro del dizionario dati {#data-dictionary-workflow}

1. Autore [crea il dizionario dati](#createdatadictionary) caricando uno schema o da zero.
1. L’autore crea lettere e comunicazioni interattive in base al dizionario dati e associa gli elementi del dizionario dati in lettere e comunicazioni interattive, se necessario.
1. Un autore può scaricare un file XML di dati di esempio, basato sullo schema di un dizionario dati. L’autore può modificare il file XML di dati di esempio, che può essere associato come dati di prova al dizionario dati. Lo stesso viene utilizzato durante l&#39;anteprima della lettera.
1. Quando [anteprima di una lettera](../../forms/using/create-letter.md#p-types-of-linkage-available-for-each-of-the-fields-p), l’autore sceglie di visualizzare in anteprima la lettera con i dati (anteprima personalizzata). Viene aperta la lettera precompilata con i dati forniti dall’autore. Viene aperto nell’interfaccia per la creazione della corrispondenza. L&#39;agente che visualizza in anteprima questa lettera può modificare il contenuto, i dati e gli allegati in questa lettera e può inviare la lettera finale. Per ulteriori informazioni sulla creazione delle lettere, vedere [Crea corrispondenza](../../forms/using/create-letter.md).

## Prerequisito {#prerequisite}

Installa il [Pacchetto di compatibilità](compatibility-package.md) per visualizzare **Dizionari dati** l&#39;opzione **Forms** pagina.

## Creare un dizionario dati {#createdatadictionary}

Puoi utilizzare l’editor del dizionario dati per creare un dizionario dati oppure caricare un file di schema XSD per creare un dizionario dati basato su di esso. Puoi quindi estendere il dizionario dati aggiungendo ulteriori informazioni richieste, compresi i campi. Indipendentemente da come è stato creato il dizionario dati, il proprietario del processo aziendale non ha bisogno di conoscere i sistemi back-end. Il proprietario del processo aziendale deve conoscere solo gli oggetti del dominio e le relative definizioni per il loro processo.

>[!NOTE]
>
>Per più lettere che richiedono elementi simili, è possibile creare un dizionario dati comune. Un dizionario dati di grandi dimensioni con un numero elevato di elementi, tuttavia, può causare problemi di prestazioni durante l’utilizzo del dizionario dati e il caricamento degli elementi, ad esempio in lettere e frammenti di documento. In caso di problemi di prestazioni, provare a creare dizionari di dati separati per lettere diverse.

1. Seleziona **Forms** > **Dizionari dati**.
1. Tocca **Crea dizionario dati**.
1. Nella schermata Proprietà , aggiungi quanto segue:

   * **Titolo:** (Facoltativo) Immetti il titolo del dizionario dati. Il titolo non deve essere univoco e può contenere caratteri speciali e caratteri non inglesi. Alle lettere e ad altri frammenti di documento viene fatto riferimento il relativo titolo (se disponibile), ad esempio nelle miniature e nelle proprietà delle risorse. I dizionari di dati sono indicati con i loro nomi e non con i loro titoli.
   * **Nome:** Nome univoco del dizionario dati. Nel campo Nome è possibile immettere solo caratteri, numeri e trattini della lingua inglese. Il campo Nome viene compilato automaticamente in base al campo Titolo e i caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti con trattini. Anche se il valore nel campo Titolo viene copiato automaticamente nel campo Nome, è possibile modificarlo.

   * **Descrizione**: (Facoltativo) Descrizione del dizionario dati.
   * **Tag:** (Facoltativo) Per creare un tag personalizzato, immetti il valore nel campo di testo e premi Invio. Il tag viene visualizzato sotto il campo di testo dei tag. Quando salvi questo testo, vengono creati anche i nuovi tag aggiunti.
   * **Proprietà estese**: (Facoltativo) Tocca **Aggiungi campo** per specificare gli attributi dei metadati per il dizionario dati. Nella colonna Nome proprietà, immetti un nome di proprietà univoco. Nella colonna Valore, immettere un valore da associare alla proprietà.

   ![Proprietà del dizionario dati specificate in tedesco](do-not-localize/1_ddproperties.png)

1. (Facoltativo) Per caricare una definizione dello schema XSD per il dizionario dati, tocca nel riquadro Struttura dizionario dati . **Carica schema XML**. Sfoglia il file XSD, selezionalo e tocca **Apri**. Viene creato un dizionario dati in base allo schema XML caricato. È necessario modificare i nomi visualizzati e le descrizioni degli elementi nel dizionario dati. A questo scopo, seleziona i nomi degli elementi toccandoli e modificandone le descrizioni, i nomi visualizzati e altri dettagli nei campi del riquadro a destra.

   Per ulteriori informazioni sugli elementi DD calcolati, vedi [Elementi del dizionario dati calcolati](#computedddelements).

   >[!NOTE]
   >
   >Puoi saltare il caricamento del file di schema e creare il dizionario dati da zero utilizzando l’interfaccia utente. A questo scopo, salta questo passaggio e continua con i passaggi successivi.

1. Tocca **Successivo**.
1. Nella schermata Aggiungi proprietà , aggiungi gli elementi al dizionario dati. Puoi anche aggiungere/eliminare elementi e modificarne i dettagli se hai caricato uno schema per ottenere una struttura di base del dizionario dati.

   Puoi toccare i tre punti sul lato destro di un elemento e aggiungere un elemento alla struttura del dizionario dati.

   ![1_2_createanelement](assets/1_2_createanelement.png)

   Seleziona un elemento composito, un elemento raccolta o un elemento primitivo.

   * Un DDE composito contiene altri DDE, che possono essere di tipo primitivo, composito o raccolta. Ad esempio, un indirizzo, costituito da un indirizzo, una città, una provincia, un paese e un codice postale.
   * I DDE primitivi sono elementi quali stringhe, numeri, date e valori booleani che contengono informazioni quali il nome di una città.
   * Una raccolta è un elenco di DDE semplici o composte simili. Ad esempio, un cliente con più posizioni o diversi indirizzi di fatturazione e spedizione.

   Di seguito sono riportate alcune regole per la creazione di un dizionario dati:

   * Solo il tipo composito è consentito come DDE di livello superiore in un dizionario dati.
   * Nome, nome di riferimento e tipo di elemento sono campi obbligatori per un dizionario dati e DDE.
   * Il nome di riferimento deve essere univoco.
   * Un DDE padre (composito) non può avere due figli con lo stesso nome.
   * Gli enumerazioni contengono solo tipi di stringa primitivi.

   Per ulteriori informazioni sugli elementi Composite, Collection e Primitive e sull’utilizzo degli elementi del dizionario dati, consulta [Mappatura degli elementi del dizionario dati su uno schema XML](#mappingddetoschema).

   Per informazioni sulle convalide nel dizionario dati, consulta [Convalida dell’editor del dizionario dati](#ddvalidations).

   ![2_adddpropertiesbasic](assets/2_addddpropertiesbasic.png)

1. (Facoltativo) Dopo aver selezionato un elemento, nella scheda Avanzate puoi aggiungere proprietà (attributi). Puoi anche toccare **Aggiungi campo** ed estendere le proprietà di un elemento DD.

   ![3_adddpropertiesadvanced](assets/3_addddpropertiesadvanced.png)

1. (Facoltativo) Per rimuovere un elemento, tocca i tre punti sul lato destro e seleziona **Elimina**.

   ![4_deleteelement](assets/4_deleteelement.png)

   >[!NOTE]
   >
   >Se elimini un elemento composito/di raccolta con nodi figlio, vengono eliminati anche i relativi nodi figlio.

1. (Facoltativo) Selezionare un elemento nel riquadro Struttura dizionario dati e nel pannello Elenco campi e variabili. Modifica o aggiungi eventuali attributi richiesti associati all’elemento.
1. Tocca **Salva**.

### Creare copie di uno o più dizionari di dati {#create-copies-of-one-or-more-data-dictionary}

Per creare rapidamente uno o più dizionari di dati con proprietà ed elementi simili ai dizionari di dati esistenti, puoi copiarli e incollarli.

1. Dall’elenco dei dizionari di dati, selezionare i dizionari di dati appropriati. Nell’interfaccia utente viene visualizzata l’icona Copia .
1. Tocca Copia. Nell’interfaccia utente viene visualizzata l’icona Incolla .
1. Tocca Incolla. Viene visualizzata la finestra di dialogo Incolla. Il sistema assegna automaticamente nomi e titoli ai nuovi dizionari dati.
1. Se necessario, modifica il Titolo e il Nome con cui desideri salvare la copia del dizionario dati.
1. Tocca Incolla. Viene creata la copia del dizionario dati. Ora puoi apportare le modifiche necessarie nel dizionario dati appena creato.

## Vedere i frammenti di documento o i documenti che fanno riferimento a un elemento del dizionario dati {#see-the-document-fragments-or-documents-that-refer-to-a-data-dictionary-element}

Durante la modifica o la visualizzazione di un dizionario dati, puoi vedere quali elementi nel dizionario dati sono indicati in cui Testi, Condizioni, Lettere e Comunicazioni interattive.

1. Per modificare il dizionario dati, effettuare una delle seguenti operazioni:

   * Passa il puntatore del mouse su un dizionario dati e tocca Modifica.
   * Seleziona un dizionario dati e tocca Modifica nell’intestazione.
   * Passa il puntatore del mouse su un dizionario dati e tocca Seleziona. Quindi tocca Modifica nell’intestazione.

   Oppure tocca un dizionario dati per visualizzarlo.

1. Nel dizionario dati, tocca un elemento semplice per selezionarlo. Gli elementi compositi e di raccolta non hanno riferimenti.

   Oltre alle proprietà Base e Avanzate dell’elemento, viene visualizzato anche Contenuto prestato .

1. Tocca Contenuto prestato .

   Viene visualizzata la scheda Contenuto prestato con le seguenti opzioni: Testi, condizioni, lettere e comunicazioni interattive. Ciascuna di queste intestazioni visualizza anche il numero di riferimenti all&#39;elemento selezionato.

1. Tocca un’intestazione per visualizzare il nome delle risorse che fanno riferimento all’elemento.

   ![lentezza](assets/lentcontent.png)

1. Per visualizzare il contenuto prestato per un altro elemento, tocca l’elemento .
1. Per visualizzare una risorsa che fa riferimento all’elemento, tocca il suo nome. Il browser visualizza la risorsa, la lettera o la comunicazione interattiva.

## Utilizzo dei dati di test {#working-with-test-data}

1. Nella pagina Dizionari dati, tocca **Seleziona**.
1. Tocca un dizionario dati per il quale vuoi scaricare i dati di prova, quindi tocca **Scaricare dati XML di esempio**.
1. Tocca **OK** nel messaggio di avviso. Viene scaricato un file XML.
1. Apri il file XML con Blocco note o un altro editor XML. Il file XML ha la stessa struttura del dizionario dati e delle stringhe segnaposto negli elementi. Sostituire le stringhe segnaposto con i dati con cui si desidera sottoporre a test una lettera.

   ```xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <Company>
   <Name>string</Name>
   <Type>string</Type>
   <HeadOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </HeadOfficeAddress>
   <SalesOfficeAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </SalesOfficeAddress>
   <HeadCount>1.0</HeadCount>
   <CEO>
   <PersonName>
   <FirstName>string</FirstName>
   <MiddleName>string</MiddleName>
   <LastName>string</LastName>
   </PersonName>
   <DOB>string</DOB>
   <CurrAddress>
   <Street>string</Street>
   <City>string</City>
   <State>string</State>
   <Zip>string</Zip>
   </CurrAddress>
   <DOJ>14-04-1973</DOJ>
   <Phone>1.0</Phone>
   </CEO>
   </Company>
   ```

   >[!NOTE]
   >
   >In questo esempio, XML crea uno spazio per tre valori in un elemento di raccolta, ma il numero di valori può essere aumentato o diminuito in base al requisito.

1. Dopo aver immesso i dati, è possibile utilizzare questo file XML quando si visualizza in anteprima una lettera con i dati di prova.

   Puoi aggiungere questi dati di test con DD (Seleziona DD e tocca Carica dati di test e carica questo file xml) Quindi dopo questo quando si visualizza l&#39;anteprima della lettera normalmente (non personalizzata), questi dati XML vengono utilizzati in lettera. Puoi anche toccare Personalizzato e caricare questo XML.

## Esempi {#samples}

Gli esempi di codice seguenti mostrano i dettagli di implementazione per il dizionario dati.

### Schema di esempio che può essere caricato nel dizionario dati {#sample-schema-that-can-be-uploaded-to-the-data-dictionary}

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns="DCT" targetNamespace="DCT" xmlns:xs="https://www.w3.org/2001/XMLSchema"
  elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:element name="Company">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Type" type="xs:anySimpleType"/>
        <xs:element name="HeadOfficeAddress" type="Address"/>
        <xs:element name="SalesOfficeAddress" type="Address" minOccurs="0"/>
        <xs:element name="HeadCount" type="xs:integer"/>
        <xs:element name="CEO" type="Employee"/>
        <xs:element name="Workers" type="Employee" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:complexType name="Employee">
    <xs:complexContent>
      <xs:extension  base="Person">
        <xs:sequence>
          <xs:element name="CurrAddress" type="Address"/>
          <xs:element name="DOJ" type="xs:date"/>
          <xs:element name="Phone" type="xs:integer"/>
        </xs:sequence>
      </xs:extension>
    </xs:complexContent>
  </xs:complexType>
  <xs:complexType name="Person">
    <xs:sequence>
      <xs:element name="PersonName" type="Name"/>
      <xs:element name="DOB" type="xs:dateTime"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Name">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string"/>
      <xs:element name="MiddleName" type="xs:string"/>
      <xs:element name="LastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
  <xs:complexType name="Address">
    <xs:sequence>
      <xs:element name="Street" type="xs:string"/>
      <xs:element name="City" type="xs:string"/>
      <xs:element name="State" type="xs:string"/>
      <xs:element name="Zip" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

## Attributi comuni associati a un DDE {#common-attributes-associated-with-a-dde}

Nella tabella seguente sono descritti gli attributi comuni associati a un DDE:

<table>
 <tbody>
  <tr>
   <td><strong>Attributo</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>Stringa</td>
   <td>Obbligatorio.<br /> Nome del DDE. Deve essere unico.</td>
  </tr>
  <tr>
   <td>Riferimento<br /> Nome</td>
   <td>Stringa</td>
   <td>Obbligatorio. Nome di riferimento univoco per il DDE che consente i riferimenti al DDE indipendenti dalle modifiche alla gerarchia o alla struttura del dizionario dati. I moduli di testo mappati con questo nome</td>
  </tr>
  <tr>
   <td>nome visualizzato</td>
   <td>Stringa</td>
   <td>Un nome descrittivo opzionale del DDE.</td>
  </tr>
  <tr>
   <td>descrizione</td>
   <td>Stringa</td>
   <td>Descrizione del DDE.</td>
  </tr>
  <tr>
   <td>elementType</td>
   <td>Stringa</td>
   <td>Obbligatorio. Tipo di DDE: STRINGA, NUMERO, DATA, Booleano, COMPOSITO, RACCOLTA.</td>
  </tr>
  <tr>
   <td>elementSubType</td>
   <td>Stringa</td>
   <td>Il sottotipo per DDE: ENUM. È consentito solo per STRING e NUMBER elementType.</td>
  </tr>
  <tr>
   <td>Chiave</td>
   <td>Booleano</td>
   <td>Un campo booleano per indicare se un DDE è un elemento chiave.</td>
  </tr>
  <tr>
   <td>Calcolati</td>
   <td>Booleano</td>
   <td>Campo booleano per indicare se un DDE viene calcolato. Un valore DDE calcolato è una funzione di altri valori DDE. Per impostazione predefinita, le espressioni jsp sono supportate.</td>
  </tr>
  <tr>
   <td>espressione</td>
   <td>Stringa</td>
   <td>L'espressione per il DDE "calcolato". Il servizio di valutazione delle espressioni fornito per impostazione predefinita supporta le espressioni JSP EL. Puoi sostituire il servizio espressione con un’implementazione personalizzata.</td>
  </tr>
  <tr>
   <td>valueSet</td>
   <td>Elenco</td>
   <td>Un insieme di valori consentiti per un tipo Enum DDE. Ad esempio, il tipo di conto può avere solo valori (Salvataggio, Corrente).</td>
  </tr>
  <tr>
   <td>ExtendedProperties</td>
   <td>Oggetto</td>
   <td>Una mappa delle proprietà personalizzate aggiunte al DDE (interfaccia utente specifica o qualsiasi altra informazione).</td>
  </tr>
  <tr>
   <td>Obbligatorio</td>
   <td>Booleano</td>
   <td>Il flag indica che l'origine dei dati dell'istanza corrispondente al dizionario dati deve contenere il valore di questo particolare DDE.</td>
  </tr>
  <tr>
   <td>Associazione</td>
   <td>BindingElement</td>
   <td>Il binding XML o Java dell’elemento.</td>
  </tr>
 </tbody>
</table>

### Elementi del dizionario dati calcolati {#computedddelements}

Un dizionario dati può anche includere elementi calcolati. Un elemento del dizionario dati calcolato è sempre associato a un&#39;espressione. Questa espressione viene valutata per ottenere il valore di un elemento del dizionario dati in fase di runtime. Un valore DDE calcolato è una funzione di altri valori DDE o letterali. Per impostazione predefinita sono supportate le espressioni JSP Expression Language (EL) . Le espressioni EL utilizzano i caratteri ${ } e le espressioni valide possono includere letterali, operatori, variabili (riferimenti agli elementi del dizionario dati) e chiamate di funzioni. Durante il riferimento a un elemento del dizionario dati nell’espressione, viene utilizzato il nome di riferimento del DDE. Il nome di riferimento è univoco per ogni elemento del dizionario dati all’interno di un dizionario dati.

Un DDE PersonFullName calcolato può essere associato a un&#39;espressione di concatenazione EL come ${PersonFirstName} ${PersonLastName}.

## Mappatura del tipo di dati tra XSD e dizionario dati {#data-type-mapping-between-xsd-and-data-dictionary-br}

L&#39;esportazione di un file XSD richiede una mappatura dati specifica, descritta nella tabella seguente. La colonna DDI indica il tipo di valore DDE disponibile nel DDI.

<table>
 <tbody>
  <tr>
   <td>XSD <br /> </td>
   <td><p>Dizionario dati <br /> </p> </td>
   <td>DDI (tipo di dati del valore dell'istanza)<br /> </p> </td>
  </tr>
  <tr>
   <td><p>xs:elemento di tipo - Tipo composito<br /> </p> </td>
   <td>DDE di tipo - COMPOSITE<br /> </p> </td>
   <td>java.util.Map<br /> </td>
  </tr>
  <tr>
   <td><p>xs:elemento in cui maxEvents &gt; 1<br /> </p> </td>
   <td>DDE di tipo - COLLECTION-<br /> Viene creato un nodo DDE accanto al DDE COLLECTION che acquisisce informazioni dal nodo COLLECTION padre. Lo stesso viene creato per entrambe le raccolte di tipi di dati semplici/compositi. Ogni volta che si dispone di una RACCOLTA del tipo composito, la struttura del dizionario dati acquisisce i campi costituenti negli elementi secondari del DDE creato per l’acquisizione delle informazioni sul tipo.<br /> - DDE (RACCOLTA)<br /> - DDE(COMPOSITE per informazioni sul tipo)<br /> - Campo DDE(STRING)1<br /> - Campo DDE(STRING)2<br /> <br /> </p> </td>
   <td>java.util.List<br /> </td>
  </tr>
  <tr>
   <td>Attributo di tipo - xs:id <br /> </p> </td>
   <td>DDE di tipo - STRING <br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:elemento di tipo - xs:string</p> </td>
   <td>DDE di tipo - STRING<br /> </td>
   <td>java.lang.String<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element di tipo - xs: booleano <br /> </td>
   <td>DDE di tipo - booleano <br /> </td>
   <td>java.lang.Boolean<br /> </td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element di tipo - xs:date </td>
   <td>DDE of type - DATE </td>
   <td>java.lang.String</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:elemento di tipo - xs:integer </td>
   <td>DDE del tipo - NUMERO </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:elemento di tipo - xs:long</td>
   <td>DDE del tipo - NUMERO </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>xs:attribute /xs:element di tipo - xs:double</td>
   <td>DDE del tipo - NUMERO </td>
   <td>java.lang.Double</td>
  </tr>
  <tr>
   <td>Elemento di tipo enum e baseType - xs:string</td>
   <td>DDE di<br /> type - STRING<br /> sottotipo - ENUM<br /> valueSet - i valori consentiti per ENUM<br /> </td>
   <td>java.lang.String</td>
  </tr>
 </tbody>
</table>

## Scaricare un file di dati di esempio da un dizionario dati {#download-a-sample-data-file-from-a-data-dictionary}

Dopo aver creato un dizionario dati, puoi scaricarlo come file di dati di esempio XML per inserire voci di testo.

1. Nella pagina Dizionari dati , tocca **Seleziona** quindi tocca un dizionario dati per selezionarlo.
1. Seleziona **Scaricare dati XML di esempio**.
1. Tocca **OK** nel messaggio di avviso.

   Gestione corrispondenza crea un file XML basato sulla struttura del dizionario dati selezionato e lo scarica sul computer con il nome &lt;data-dictionary-name>-SampleData. Ora è possibile modificare questo file in un editor XML o di testo per inserire dati mentre [creazione di una lettera](../../forms/using/create-letter.md).

## Internazionalizzazione dei metadati {#internationalization-of-meta-data}

Se desideri inviare la stessa lettera in lingue diverse ai clienti, puoi localizzare il nome visualizzato, la descrizione e i set di valori enum del dizionario dati e degli elementi del dizionario dati.

### Localizzare il dizionario dati {#localize-data-dictionary}

1. Nella pagina Dizionari dati, tocca **Seleziona** quindi tocca un dizionario dati per selezionarlo.
1. Tocca **Download dei dati di localizzazione**.
1. Tocca **OK** nell&#39;avviso. Gestione corrispondenza scarica un file zip sul computer con il nome DataDictionary-&lt;ddname>.zip.
1. Il file ZIP contiene un file .properties . Questo file definisce il dizionario dati scaricato. Il contenuto del file di proprietà è simile al seguente:

   ```ini
   #Wed May 20 16:06:23 BST 2015
   DataDictionary.EmployeeDD.description=
   DataDictionary.EmployeeDD.displayName=EmployeeDataDictionary
   DataDictionaryElement.name.description=
   DataDictionaryElement.name.displayName=name
   DataDictionaryElement.person.description=
   DataDictionaryElement.person.displayName=person
   ```

   La struttura del file delle proprietà definisce una riga ciascuna per la descrizione e il nome visualizzato per il dizionario dati e per ogni elemento del dizionario dati. Inoltre, il file delle proprietà definisce una riga per un valore enum impostato per ogni elemento del dizionario dati. Come con un dizionario dati, il file delle proprietà corrispondente può avere più definizioni di elementi del dizionario dati. Inoltre, il file può contenere le definizioni di uno o più set di valori enum.

1. Per aggiornare il file .properties in un&#39;altra impostazione internazionale, aggiorna il nome visualizzato e i valori di descrizione nel file. Crea più istanze del file per ogni lingua in cui desideri localizzare. Sono supportate solo le lingue francese, tedesca, giapponese e inglese.

1. Salva i diversi file di proprietà aggiornati con i seguenti nomi:

   _fr_FR.properties Francese

   _de_DE.properties Tedesco

   _ja_JA.properties Giapponese

   _en_EN.properties English

1. Archivia il file .properties (o i file per più impostazioni internazionali) in un unico file .zip.

1. Nella pagina Dizionari dati, seleziona **Altro** > **Caricare dati di localizzazione** e selezionare il file zip con file di proprietà localizzati.
1. Per visualizzare le modifiche alla localizzazione, modifica le impostazioni internazionali del browser.

## Convalida del dizionario dati {#ddvalidations}

Durante la creazione o l’aggiornamento di un dizionario dati, l’Editor dizionario dati applica le seguenti convalide.

* Solo il tipo composito è consentito come elemento di primo livello in un dizionario dati.
* Gli elementi compositi e di raccolta non sono consentiti a livello di foglia. A livello di foglia sono consentiti solo gli elementi Primitivi (stringa, data, numero, booleano). Questa convalida assicura che non vi siano elementi compositi e di raccolta senza un DDE figlio.
* Durante il caricamento di un file XSD per creare un dizionario dati, l’Editor dizionario dati richiede la creazione di un elemento di livello principale, se esistono più elementi, per creare il dizionario dati.
* Il nome è l’unico parametro richiesto per un dizionario dati.
* Un DDE padre (composito) non può avere due figli con lo stesso nome
* Garantisce che un DDE sia contrassegnato come calcolato solo se non è un parametro obbligatorio. Non è possibile calcolare un elemento obbligatorio e non è possibile richiederlo. Inoltre, Collection e Composite Element non possono essere elementi calcolati.
* Assicura che un DDE sia contrassegnato come obbligatorio, solo quando non viene calcolato. Inoltre, assicura che non sia &quot;collectionElement&quot; a indicare il tipo di Collection (ovvero gli unici elementi secondari di un elemento di raccolta).
* Le chiavi vuote o duplicate non sono consentite in ExtendedProperties per un dizionario dati o DDE.
* Non utilizzare i caratteri due punti (:) o barre verticali(|) all&#39;interno della chiave o del valore di una proprietà estesa. Non esiste una convalida per l&#39;uso di questi caratteri non consentiti.

Convalida applicate a livello di dizionario dati

* Il nome del dizionario dati non deve essere null.
* Il nome del dizionario dati deve contenere solo caratteri alfanumerici.
* L’elenco degli elementi figlio nel dizionario dati non deve essere null o vuoto.
* Il dizionario dati non deve contenere più di un elemento del dizionario dati di livello superiore.
* Solo il tipo composito è consentito come elemento di livello principale in un dizionario dati.

Convalida applicate a livello di elemento del dizionario dati.

* Tutti i nomi DDE non devono essere nulli e non devono contenere spazi.
* Tutti i DDE devono avere un tipo di elemento &quot;non nullo/non nullo&quot;.
* Tutti i nomi di riferimento DDE non devono essere nulli.
* Tutti i nomi di riferimento DDE devono essere univoci.
* Tutti i riferimenti DDE devono contenere solo caratteri alfanumerici e &quot;_&quot;.
* Tutti i nomi visualizzati DDE devono contenere solo caratteri alfanumerici e &quot;_&quot;.
* Gli elementi compositi e di raccolta non sono consentiti a livello di foglia. A livello di foglia sono consentiti solo gli elementi Primitivi (stringa, data, numero, booleano). Questa convalida assicura che non vi siano elementi compositi e di raccolta senza un DDE figlio.
* Un DDE padre composito non deve avere due elementi secondari con lo stesso nome.
* Il sottotipo ENUM viene utilizzato solo per gli elementi String e Number.
* Impossibile calcolare gli elementi di raccolta e compositi.
* Un DDE non può essere calcolato e richiesto.
* I DDE calcolati devono contenere un&#39;espressione valida.
* Gli DDE calcolati non devono avere binding XML.
* Un DDE che denota il tipo per un DDE di raccolta non può essere calcolato o richiesto.
* I DDE del sottotipo ENUM non devono contenere set di valori nulli o vuoti.
* Il binding XML di un DDE di raccolta non deve essere associato a un attributo.
* La sintassi di binding XML deve essere valida, ad esempio viene visualizzata una sola @, la @ è consentita solo se seguita da un nome di attributo.

## Mappatura degli elementi del dizionario dati su uno schema XML {#mappingddetoschema}

È possibile creare un dizionario dati da uno schema XML o generarlo utilizzando l&#39;interfaccia utente del dizionario dati. Tutti gli elementi del dizionario dati (DDE, Data Dictionary Elements) all’interno di un dizionario dati dispongono di un campo di binding XML per memorizzare il binding del DDE a un elemento nello schema XML. Il binding in ogni DDE è relativo al DDE padre.

Di seguito sono riportati i modelli di esempio e gli esempi di codice che mostrano i dettagli di implementazione per il dizionario dati.

## Mappatura di elementi semplici (primitivi) {#mapping-simple-primitive-elements}

Un DDE primitivo rappresenta un campo o un attributo che è atomico in natura. I DDE primitivi definiti al di fuori dell&#39;ambito di un tipo complesso (DDE composito) o di un elemento ripetuto (DDE della raccolta) possono essere memorizzati in qualsiasi posizione all&#39;interno dello schema XML. La posizione dei dati corrispondenti a un DDE primitivo non dipende dalla mappatura del relativo DDE padre. DDE primitivo utilizza le informazioni di mappatura dal campo Binding XML per determinarne il valore e le mappature si traducono in uno dei seguenti elementi:

* un attributo
* un elemento
* un contesto testuale
* nulla (un DDE ignorato)

L&#39;esempio seguente mostra uno schema semplice.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="https://www.w3.org/2001/XMLSchema">
  <xs:element name='age' type='integer'/>
  <xs:element name='price' type='decimal'/>
</xs:schema>
```

| **Elemento dizionario dati** | **Binding XML predefinito** |
|---|---|
| age | /age |
| prezzo | /prezzo |

### Mappatura di elementi compositi {#mapping-composite-elements}

Il binding non è supportato per gli elementi compositi; se viene fornito il binding, questo viene ignorato. Il binding per tutti i DDE figlio costitutivi di tipo primitivo deve essere assoluto. Consentire la mappatura assoluta per gli elementi secondari di un DDE composito offre maggiore flessibilità in termini di Binding XPath. La mappatura di un DDE composito su un elemento di tipo complesso nello schema XML limita l’ambito del binding per i relativi elementi secondari.

L&#39;esempio seguente mostra lo schema di una nota.

```xml
<xs:element name="note">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="to" type="xs:string"/>
            <xs:element name="from" type="xs:string"/>
            <xs:element name="heading" type="xs:string"/>
            <xs:element name="body" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>
```

<table>
 <tbody>
  <tr>
   <td><strong>Elemento dizionario dati</strong></td>
   <td><strong>Binding XML predefinito</strong></td>
  </tr>
  <tr>
   <td>nota</td>
   <td>empty(null)<br /> </td>
  </tr>
  <tr>
   <td>a</td>
   <td>/note/a</td>
  </tr>
  <tr>
   <td>da</td>
   <td>/note/da</td>
  </tr>
  <tr>
   <td>intestazione</td>
   <td>/nota/intestazione</td>
  </tr>
  <tr>
   <td>corpo</td>
   <td>/note/corpo</td>
  </tr>
 </tbody>
</table>

### Mappatura degli elementi di raccolta {#mapping-collection-elements}

Un elemento di raccolta è mappato solo su un altro elemento di raccolta con cardinalità > 1. I DDE secondari di una raccolta DDE hanno un binding XML relativo (locale) rispetto al binding XML del relativo elemento padre. Poiché i DDE secondari di un elemento di raccolta devono avere la stessa cardinalità di quello dell&#39;elemento padre, il binding relativo è obbligatorio per garantire il vincolo di cardinalità in modo che i DDE secondari non puntino a un elemento schema XML non ripetuto. Nell’esempio seguente, la cardinalità di &quot;TokenID&quot; deve essere uguale a &quot;Token&quot; che è la sua raccolta padre DDE.

Durante la mappatura di un DDE di raccolta a un elemento dello schema XML:

* il binding per l’elemento DDE corrispondente all’elemento Collection deve essere l’XPath assoluto

* Non fornire alcun binding per il DDE che rappresenta il tipo di elemento Collection. Se viene fornito, il binding viene ignorato.

* Il binding per tutti i DDE figlio dell’elemento Collection deve essere relativo all’elemento Collection principale.

Lo schema XML seguente dichiara un elemento con il nome Token e un attributo maxOccurs di &quot;unbounded&quot;. Pertanto, Token è un elemento di raccolta.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Root>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
  <Tokens>
    <TokenID>string</TokenID>
    <TokenText>
      <TextHeading>string</TextHeading>
      <TextBody>string</TextBody>
    </TokenText>
  </Tokens>
</Root>
```

Il Token.xsd associato a questo esempio è il seguente:

```xml
<xs:element name="Root">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="Tokens" type="TokenType" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

<xs:complexType name="TokenType">
  <xs:sequence>
    <xs:element name="TokenID" type="xs:string"/>
    <xs:element name="TokenText">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="TextHeading" type="xs:string"/>
          <xs:element name="TextBody" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:sequence>
</xs:complexType>
```

| **Elemento dizionario dati** | **Binding XML predefinito** |
|---|---|
| Directory principale | empty(null) |
| Token | /Root/Token |
| Composito | empty(null) |
| TokenID | TokenID |
| TokenText | empty(null) |
| TokenIntestazione | TokenText/TextHeader |
| TokenBody | TokenText/TextBody |
