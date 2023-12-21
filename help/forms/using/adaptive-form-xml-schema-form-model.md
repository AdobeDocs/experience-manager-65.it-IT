---
title: Come si crea un Forms adattivo utilizzando lo schema XML?
description: Scopri come utilizzare lo schema XML come modello di modulo in un modulo adattivo. Puoi applicare i modelli XSD esistenti per creare moduli adattivi e trascinare e rilasciare gli elementi dello schema da XSD al modulo adattivo. Approfondisci l’esempio di uno schema XML, aggiungi proprietà speciali ai campi utilizzando uno schema XML e limita i valori accettabili per un componente modulo adattivo.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 35d5859f-54c4-4d14-9c64-0d9291ef9029
source-git-commit: 4ecdcb2659b26043f95ba1dc3e907c33f65b8834
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 5%

---

# Creazione di moduli adattivi tramite lo schema XML {#creating-adaptive-forms-using-xml-schema}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Prerequisiti {#prerequisites}

Per creare un modulo adattivo utilizzando uno schema XML come modello di modulo è necessario conoscere a fondo gli schemi XML. Inoltre, si consiglia di leggere il seguente contenuto prima di questo articolo.

* [Creazione di un modulo adattivo](creating-adaptive-form.md)
* [Schema XML](https://www.w3.org/TR/xmlschema-2/)

## Utilizzo di uno schema XML come modello di modulo {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] supporta la creazione di un modulo adattivo utilizzando uno schema XML esistente come modello di modulo. Questo schema XML rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell&#39;organizzazione.

Le caratteristiche principali dell&#39;utilizzo di uno schema XML sono:

* La struttura dell’XSD viene visualizzata come una struttura nella scheda Content Finder nella modalità di authoring di un modulo adattivo. Puoi trascinare e aggiungere un elemento dalla gerarchia XSD al modulo adattivo.
* È possibile precompilare il modulo utilizzando XML conforme allo schema associato.
* Al momento dell’invio, i dati immessi dall’utente vengono inviati come XML in linea con lo schema associato.

Uno schema XML è costituito da tipi di elementi semplici e complessi. Gli elementi dispongono di attributi che aggiungono regole all’elemento. Quando questi elementi e attributi vengono trascinati in un modulo adattivo, vengono mappati automaticamente al corrispondente componente del modulo adattivo.

Di seguito è riportata la mappatura degli elementi XML con i componenti dei moduli adattivi:

<table>
 <tbody>
  <tr>
   <th><strong>Elemento o attributo XML </strong></th>
   <th><strong>Componente modulo adattivo</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>Casella di testo</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>Casella di selezione</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>Tutti i tipi di valori numerici</li>
    </ul> </td>
   <td>Casella numerica</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>Selettore data</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>Elenchi a discesa</td>
  </tr>
  <tr>
   <td>Qualsiasi elemento di tipo complesso</td>
   <td>Pannello</td>
  </tr>
 </tbody>
</table>

## Schema XML di esempio {#sample-xml-schema}

Di seguito è riportato un esempio di schema XML.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Verificare che lo schema XML contenga un solo elemento principale. Schema XML con più elementi radice non supportato.

## Aggiunta di proprietà speciali ai campi utilizzando lo schema XML {#adding-special-properties-to-fields-using-xml-schema}

È possibile aggiungere i seguenti attributi agli elementi dello schema XML per aggiungere proprietà speciali ai campi del modulo adattivo associato.

<table>
 <tbody>
  <tr>
   <th><strong>Proprietà schema</strong></th>
   <th><strong>Uso nei moduli adattivi</strong></th>
   <th><strong>Supportato in </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>Contrassegna un campo come obbligatorio<br /> </td>
   <td>Attributo</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>Aggiunge un valore predefinito</td>
   <td>Elemento e attributo</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>Specifica le occorrenze minime</p> <p>(Per sottomaschere ripetibili (tipi complessi))</p> </td>
   <td>Elemento (tipo complesso)</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>Specifica le occorrenze massime</p> <p>(Per sottomaschere ripetibili (tipi complessi))</p> </td>
   <td>Elemento (tipo complesso)</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Quando trascini un elemento schema in un modulo adattivo, viene generata una didascalia predefinita da:
>
>* Uso dell&#39;iniziale maiuscola nel nome dell&#39;elemento
>* Inserimento di uno spazio vuoto nei limiti della Camel Case.
>
>Ad esempio, se aggiungi il `userFirstName` schema, la didascalia generata nel modulo adattivo è `User First Name`.

## Limitare valori accettabili per un componente modulo adattivo {#limit-acceptable-values-for-an-adaptive-form-component}

Per limitare i valori accettabili per un componente modulo adattivo, è possibile aggiungere le seguenti restrizioni agli elementi dello schema XML:

<table>
 <tbody>
  <tr>
   <td><p><strong> Proprietà schema</strong></p> </td>
   <td><p><strong>Tipo di dati</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero massimo di cifre consentite in un componente. Il numero di cifre specificato deve essere maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite superiore per valori numerici e date. Per impostazione predefinita, il valore massimo è incluso.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico<br /> </li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite inferiore per i valori numerici e le date. Per impostazione predefinita, è incluso il valore minimo.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere inferiori al valore numerico o alla data specificati per la proprietà maximum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo deve essere minore o uguale al valore numerico o alla data specificati per la proprietà maximum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere maggiori del valore numerico o della data specificati per la proprietà minimum.</p> <p>Se false, il valore numerico o la data specificati nel componente del modulo devono essere maggiori o uguali al valore numerico o alla data specificati per la proprietà minimum.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
     <li>Selettore data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero minimo di caratteri consentito in un componente. La lunghezza minima deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero massimo di caratteri consentiti in un componente. La lunghezza massima deve essere maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero esatto di caratteri consentiti in un componente. La lunghezza deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella di testo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero massimo di posizioni decimali consentite in un componente. FractionDigits deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li> Casella numerica con tipo di dati float o decimal</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica la sequenza dei caratteri. Un componente accetta i caratteri se questi sono conformi al modello specificato.</p> <p>La proprietà pattern viene mappata sul pattern di convalida del componente del modulo adattivo corrispondente.</p> </td>
   <td>
    <ul>
     <li>Tutti i componenti di moduli adattivi mappati su uno schema XSD </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Domande frequenti {#frequently-asked-questions}

**Come è possibile sapere quale elemento della struttura è associato a quale elemento XML?**

Quando si fa doppio clic su un elemento in Content Finder, in una finestra popup viene visualizzato il nome di un campo e una proprietà denominata `bindRef`. Questa proprietà mappa l&#39;elemento della struttura all&#39;elemento o all&#39;attributo nello schema.

![Campo bindref di un elemento schema XML](assets/dblclick.png)

Il <code>bindRef</code> mostra l’associazione tra un elemento della struttura e un elemento o un attributo in uno schema.

>[!NOTE]
>
>Gli attributi hanno un `@` simbolo nel loro `bindRef`per distinguerli dagli elementi. Esempio: `/config/projectDetails/@duration`.

**Perché non è possibile trascinare singoli elementi di una sottomaschera (struttura generata da qualsiasi tipo complesso) per sottomaschere ripetibili (i valori minOccours o maxOccurs sono maggiori di 1)?**

In una sottomaschera ripetibile è necessario utilizzare la sottomaschera Completa. Se desideri solo campi selettivi, utilizza l’intera struttura ed elimina quelli indesiderati.

**In Content Finder ho una struttura lunga e complessa. Come posso trovare un elemento specifico?**

Sono disponibili due opzioni:

* Scorri nella struttura ad albero
* Utilizzare la casella di ricerca per trovare un elemento

**Che cos&#39;è un bindRef?**

A `bindRef` è la connessione tra un componente modulo adattivo e un elemento o un attributo dello schema. Determina la `XPath` dove il valore acquisito da questo componente o campo è disponibile nel codice XML di output. A `bindRef`viene utilizzato anche quando si precompila un valore di campo da XML precompilato (precompilato).
