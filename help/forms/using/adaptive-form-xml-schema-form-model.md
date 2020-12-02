---
title: Creazione di moduli adattivi tramite lo schema XML
seo-title: Creazione di moduli adattivi tramite lo schema XML
description: I moduli adattivi possono utilizzare lo schema XML come modello di modulo, consentendo di utilizzare i modelli XSD esistenti per creare moduli adattivi. È possibile trascinare gli elementi dello schema da XSD al modulo adattivo.
seo-description: I moduli adattivi possono utilizzare lo schema XML come modello di modulo, consentendo di utilizzare i modelli XSD esistenti per creare moduli adattivi. È possibile trascinare gli elementi dello schema da XSD al modulo adattivo.
uuid: 84c35728-1b6c-4286-854b-51c03bfd0eac
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d6c12b3-3a70-48e9-a83b-974360a8b0b6
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 5%

---


# Creazione di moduli adattivi utilizzando lo schema XML{#creating-adaptive-forms-using-xml-schema}

## Prerequisiti {#prerequisites}

Per creare un modulo adattivo utilizzando uno schema XML come modello di modulo, è necessario conoscere gli schemi XML di base. Inoltre, si consiglia di consultare il contenuto seguente prima di questo articolo.

* [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md)
* [Schema XML](https://www.w3.org/TR/xmlschema-2/)

## Uso di uno schema XML come modello di modulo {#using-an-xml-schema-as-form-model}

 AEM Forms supporta la creazione di un modulo adattivo utilizzando uno schema XML esistente come modello di modulo. Questo schema XML rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell&#39;organizzazione.

Le caratteristiche principali dell&#39;utilizzo di uno schema XML sono:

* La struttura di XSD viene visualizzata come struttura ad albero nella scheda Content Finder nella modalità di creazione per un modulo adattivo. È possibile trascinare e aggiungere elementi dalla gerarchia XSD al modulo adattivo.
* È possibile precompilare il modulo utilizzando codice XML conforme allo schema associato.
* Al momento dell&#39;invio, i dati immessi dall&#39;utente vengono inviati come XML che si allinea allo schema associato.

Uno schema XML è costituito da tipi di elementi semplici e complessi. Gli elementi hanno attributi che aggiungono regole all&#39;elemento. Quando questi elementi e attributi vengono trascinati su un modulo adattivo, vengono mappati automaticamente sul componente modulo adattivo corrispondente.

La mappatura degli elementi XML con componenti per moduli adattivi è la seguente:

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
   <td>Drop (Giù)</td>
  </tr>
  <tr>
   <td>Qualsiasi elemento di tipo complesso</td>
   <td>Pannello</td>
  </tr>
 </tbody>
</table>

## Schema XML di esempio {#sample-xml-schema}

Esempio di uno schema XML.

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
>Verificare che lo schema XML abbia un solo elemento principale. Uno schema XML con più di un elemento principale non è supportato.

## Aggiunta di proprietà speciali ai campi utilizzando lo schema XML {#adding-special-properties-to-fields-using-xml-schema}

È possibile aggiungere i seguenti attributi agli elementi dello schema XML per aggiungere proprietà speciali ai campi del modulo adattivo associato.

<table>
 <tbody>
  <tr>
   <th><strong>Proprietà Schema</strong></th>
   <th><strong>Uso in modulo adattivo</strong></th>
   <th><strong>Supportato in </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>Contrassegna un campo obbligatorio<br /> </td>
   <td>Attributo</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>Aggiunge un valore predefinito</td>
   <td>Elemento e attributo</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>Specifica le occorrenze minime</p> <p>(Per sottomoduli ripetibili (tipi complessi)</p> </td>
   <td>Elemento (tipo complesso)</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>Specifica le occorrenze massime</p> <p>(Per sottomoduli ripetibili (tipi complessi)</p> </td>
   <td>Elemento (tipo complesso)</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Quando si trascina un elemento dello schema in un modulo adattivo, viene generata una didascalia predefinita tramite:
>
>* Capitalizzazione del primo carattere del nome dell&#39;elemento
>* Inserimento di spazio bianco ai bordi della cassa del cammello.

>
>
Ad esempio, se si aggiunge l&#39;elemento dello schema `userFirstName`, la didascalia generata nel modulo adattivo è `User First Name`.

## Limitare i valori accettabili per un componente modulo adattivo {#limit-acceptable-values-for-an-adaptive-form-component}

È possibile aggiungere le seguenti limitazioni agli elementi dello schema XML per limitare i valori accettabili per un componente modulo adattivo:

<table>
 <tbody>
  <tr>
   <td><p><strong> Proprietà Schema</strong></p> </td>
   <td><p><strong>Tipo di dati</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il numero massimo di cifre consentito in un componente. Il numero di cifre specificato deve essere maggiore di zero.</p> </td>
   <td>
    <ul>
     <li>Casella numerica</li>
     <li>Stepper numerico</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica il limite superiore per i valori numerici e le date. Per impostazione predefinita, è incluso il valore massimo.</p> </td>
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
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere inferiori al valore numerico o alla data specificati per la proprietà massima.</p> <p>Se è false, il valore numerico o la data specificati nel componente del modulo deve essere minore o uguale al valore numerico o alla data specificati per la proprietà massima.</p> </td>
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
   <td><p>Se true, il valore numerico o la data specificati nel componente del modulo devono essere maggiori del valore numerico o della data specificati per la proprietà minima.</p> <p>Se è false, il valore numerico o la data specificati nel componente del modulo deve essere maggiore o uguale al valore numerico o alla data specificati per la proprietà minima.</p> </td>
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
   <td><p>Specifica il numero minimo di caratteri consentiti in un componente. La lunghezza minima deve essere uguale o maggiore di zero.</p> </td>
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
   <td><p>Specifica il numero massimo di posizioni decimali consentite in un componente. Il numero fractionDigits deve essere uguale o maggiore di zero.</p> </td>
   <td>
    <ul>
     <li> Casella numerica con tipo di dati mobile o decimale</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Stringa</p> </td>
   <td><p>Specifica la sequenza dei caratteri. Un componente accetta i caratteri se questi sono conformi al pattern specificato.</p> <p>La proprietà pattern viene mappata sul pattern di convalida del componente modulo adattivo corrispondente.</p> </td>
   <td>
    <ul>
     <li>Tutti i componenti di moduli adattivi mappati a uno schema XSD </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Domande frequenti {#frequently-asked-questions}

**Come si fa a sapere quale elemento della struttura è associato a quale elemento XML?**

Quando si fa doppio clic su un elemento in Content Finder, in una finestra a comparsa vengono visualizzati il nome di un campo e una proprietà denominata `bindRef`. Questa proprietà associa l&#39;elemento struttura all&#39;elemento o all&#39;attributo nello schema.

![Un campo associato a un elemento dello schema XML](assets/dblclick.png)

Il campo bindRef</code> mostra l&#39;associazione tra un elemento ad albero e un elemento o un attributo in uno schema.

>[!NOTE]
>
>Gli attributi hanno un simbolo `@` nel relativo valore `bindRef`per distinguerli dagli elementi. Esempio, `/config/projectDetails/@duration`.

**Perché non è possibile trascinare singoli elementi di un sottomodulo (struttura generata da qualsiasi tipo complesso) per sottomoduli ripetibili (i valori minOccours o maxOccurs sono maggiori di 1)?**

In un sottomodulo ripetibile, è necessario utilizzare il sottomodulo completo. Se desiderate solo campi selettivi, utilizzate l&#39;intera struttura ed eliminate quelli indesiderati.

**In Content Finder ho una struttura complessa molto lunga. Come posso trovare un elemento specifico?**

Sono disponibili due opzioni:

* Scorrere la struttura ad albero
* Utilizzare la casella di ricerca per trovare un elemento

**Cos&#39;è un bindRef?**

Un `bindRef` è la connessione tra un componente modulo adattivo e un elemento o attributo dello schema. Determina il `XPath` dove il valore acquisito da questo componente o campo è disponibile nell&#39;XML di output. Un elemento `bindRef`viene utilizzato anche per precompilare un valore di campo da un XML precompilato (precompilato).
