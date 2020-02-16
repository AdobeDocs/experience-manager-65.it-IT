---
title: Identificazione del contenuto da tradurre
seo-title: Identificazione del contenuto da tradurre
description: Scoprite come identificare i contenuti da tradurre.
seo-description: Scoprite come identificare i contenuti da tradurre.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Identificazione del contenuto da tradurre{#identifying-content-to-translate}

Le regole di traduzione identificano il contenuto da tradurre per le pagine, i componenti e le risorse inclusi o esclusi nei progetti di traduzione. Quando una pagina o una risorsa viene tradotta, AEM estrae il contenuto in modo che possa essere inviato al servizio di traduzione.

Le pagine e le risorse sono rappresentate come nodi nell’archivio JCR. Il contenuto estratto corrisponde a uno o più valori di proprietà dei nodi. Le regole di traduzione identificano le proprietà che contengono il contenuto da estrarre.

Le regole di traduzione sono espresse in formato XML e memorizzate nelle seguenti posizioni possibili:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

Il file si applica a tutti i progetti di traduzione.

>[!NOTE]
>
>Dopo un aggiornamento a 6.4, si consiglia di spostare il file da /etc. Per ulteriori informazioni, consultate Ristrutturazione [comune dell&#39;archivio in AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) .

Le regole includono le seguenti informazioni:

* Percorso del nodo a cui si applica la regola. La regola si applica anche ai discendenti del nodo.
* Nomi delle proprietà nodo che contengono il contenuto da tradurre. La proprietà può essere specifica per un tipo di risorsa specifico o per tutti i tipi di risorsa.

Ad esempio, potete creare una regola che traduca il contenuto aggiunto dagli autori a tutti i componenti di testo di base di AEM sulle pagine. La regola può identificare il `/content` nodo e la `text` proprietà per il `foundation/components/text` componente.

È stata aggiunta una [console](#translation-rules-ui) per la configurazione delle regole di traduzione. Le definizioni nell’interfaccia utente popoleranno il file.

 Per una panoramica delle funzioni di traduzione del contenuto in AEM, consultate [Traduzione del contenuto per siti](/help/sites-administering/translation.md)multilingue.

>[!NOTE]
>
>AEM supporta la mappatura uno-a-uno tra i tipi di risorse e gli attributi di riferimento per la traduzione del contenuto di riferimento in una pagina.

## Sintassi delle regole per pagine, componenti e risorse {#rule-syntax-for-pages-components-and-assets}

Una regola è un `node` elemento con uno o più `property` elementi secondari e zero o più `node` elementi secondari:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Ciascuno di questi `node` elementi presenta le seguenti caratteristiche:

* L&#39; `path` attributo contiene il percorso al nodo principale del ramo a cui si applicano le regole.
* Gli `property` elementi secondari identificano le proprietà del nodo da tradurre per tutti i tipi di risorse:

   * L&#39; `name` attributo contiene il nome della proprietà.
   * L&#39; `translate` attributo facoltativo è uguale `false` a se la proprietà non è convertita. By default the value is `true`. Questo attributo è utile per ignorare le regole precedenti.

* Gli `node` elementi secondari identificano le proprietà del nodo da tradurre per tipi di risorse specifici:

   * L&#39; `resourceType` attributo contiene il percorso che risolve il componente che implementa il tipo di risorsa.
   * Gli `property` elementi secondari identificano la proprietà node da tradurre. Utilizzate questo nodo nello stesso modo degli `property` elementi secondari per le regole dei nodi.

La regola di esempio seguente determina la conversione del contenuto di tutte `text` le proprietà per tutte le pagine sotto il `/content` nodo. La regola è valida per qualsiasi componente che memorizza il contenuto in una `text` proprietà, ad esempio il componente Testo di base e il componente Immagine di base.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

L’esempio seguente traduce il contenuto di tutte `text` le proprietà e anche altre proprietà del componente Immagine di base. Se altri componenti hanno proprietà con lo stesso nome, la regola non si applica ad essi.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="foundation/components/textimage">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## Sintassi regola per l&#39;estrazione di risorse dalle pagine {#rule-syntax-for-extracting-assets-from-pages}

Utilizzate la seguente sintassi di regola per includere risorse incorporate nei componenti o a cui fanno riferimento i componenti:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Ogni `assetNode` elemento ha le seguenti caratteristiche:

* Un `resourceType` attributo uguale al percorso che corrisponde al componente.
* Un `assetReferenceAttribute` attributo uguale al nome della proprietà che memorizza il binario della risorsa (per le risorse incorporate) o il percorso della risorsa di riferimento.

L’esempio seguente estrae le immagini dal componente Immagine di base:

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## Regole di sostituzione {#overriding-rules}

Il file translate_rules.xml è costituito da un `nodelist` elemento con diversi `node` elementi figlio. AEM legge l’elenco dei nodi dall’alto verso il basso. Quando più regole hanno come destinazione lo stesso nodo, viene utilizzata la regola che è inferiore nel file. Ad esempio, le regole seguenti determinano la conversione di tutto il contenuto delle `text` proprietà, ad eccezione del `/content/mysite/en` ramo di pagine:

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## Proprietà filtro {#filtering-properties}

È possibile filtrare i nodi con una specifica proprietà utilizzando un `filter` elemento.

Ad esempio, le regole seguenti determinano la conversione di tutto il contenuto delle `text` proprietà, ad eccezione dei nodi con la proprietà `draft` impostata su `true`.

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Interfaccia delle regole di traduzione {#translation-rules-ui}

È inoltre disponibile una console per configurare le regole di traduzione.

Per accedervi:

1. Passare a **Strumenti** e quindi a **Generale**.

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. Selezionate Configurazione **** traduzione.

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

Da qui è possibile **aggiungere contesto**. Consente di aggiungere un percorso.

![chlimage_1-57](assets/chlimage_1-57.jpeg)

Selezionate quindi il contesto e fate clic su **Modifica**. Viene aperto l&#39;Editor delle regole di traduzione.

![chlimage_1-58](assets/chlimage_1-58.jpeg)

È possibile modificare 4 attributi tramite l’interfaccia utente: `isDeep`, `inherit`, `translate` e `updateDestinationLanguage`.

**isDeep** Questo attributo è applicabile ai filtri dei nodi ed è true per impostazione predefinita. Controlla se il nodo (o i suoi predecessori) contiene tale proprietà con il valore della proprietà specificato nel filtro. Se false, controlla solo il nodo corrente.

Ad esempio, i nodi secondari vengono aggiunti a un processo di conversione anche quando il nodo principale ha la proprietà `draftOnly` impostata su true per contrassegnare il contenuto bozza. In questo `isDeep` caso viene riprodotto e verifica se i nodi padre hanno la proprietà `draftOnly` true ed esclude tali nodi figlio.

Nell’editor, è possibile selezionare o deselezionare **È profondo** nella scheda **Filtri** .

![chlimage_1-59](assets/chlimage_1-59.jpeg)

Di seguito è riportato un esempio del codice xml risultante quando **Is Deep (È profondo** ) viene deselezionato nell’interfaccia utente:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**inherit** Questo è applicabile alle proprietà. Per impostazione predefinita ogni proprietà viene ereditata, ma se si desidera che alcune proprietà non vengano ereditate dall&#39;elemento secondario, è possibile contrassegnare tale proprietà come false in modo che venga applicata solo a quel nodo specifico.

Nell’interfaccia utente, è possibile selezionare o deselezionare **Eredita** nella scheda **Proprietà** .

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**translate** L&#39;attributo translate viene utilizzato semplicemente per specificare se tradurre o meno una proprietà.

Nell’interfaccia utente, potete selezionare/deselezionare **Traduci** nella scheda **Proprietà** .

**updateDestinationLanguage** Questo attributo è utilizzato per le proprietà che non hanno testo ma codici lingua, ad esempio jcr:language. L&#39;utente non traduce il testo ma le impostazioni internazionali della lingua dall&#39;origine alla destinazione. Tali proprietà non vengono inviate per la traduzione.

Nell’interfaccia utente, è possibile selezionare o deselezionare **Traduci** nella scheda **Proprietà** , ma per le proprietà specifiche che hanno codici lingua come valore.

Per chiarire la differenza tra `updateDestinationLanguage` e `translate`, ecco un semplice esempio di contesto con solo due regole:

![chlimage_1-61](assets/chlimage_1-61.jpeg)

Il risultato nel file xml sarà simile al seguente:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Modifica manuale del file delle regole {#editing-the-rules-file-manually}

Il file translate_rules.xml installato con AEM contiene un set predefinito di regole di traduzione. Potete modificare il file per soddisfare i requisiti dei vostri progetti di traduzione. Ad esempio, è possibile aggiungere regole per tradurre il contenuto dei componenti personalizzati.

Se modificate il file translate_rules.xml, mantenete una copia di backup in un pacchetto di contenuto. L&#39;installazione di service pack AEM o la reinstallazione di alcuni pacchetti AEM può sostituire il file Translation_rules.xml corrente con l&#39;originale. Per ripristinare le regole in questa situazione, potete installare il pacchetto che contiene la copia di backup.

>[!NOTE]
>
>Dopo aver creato il pacchetto di contenuti, ricreate il pacchetto ogni volta che modificate il file.

## Esempio di file delle regole di conversione {#example-translation-rules-file}

```xml
<nodelist>
    <!-- translation rules for Geometrixx Demo site (example) -->
    <node path="/content/geometrixx">
        <!-- list all node properties that should be translated -->
        <property name="jcr:title" /> <!-- translation workflows running on content saved in /content/geometrixx, will extract jcr:title values independent of the component. -->
        <property name="jcr:description" />
        <node resourceType ="foundation/components/image"> <!-- translation workflows running on content saved in /content/geometrixx, will extract alternateText values only for Image component. -->
            <property name="alternateText"/>
        </node>
        <node resourceType ="geometrixx/components/title">
            <property name="richText"/>
            <property name="jcr:title" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract jcr:title for Title component, but instead use richText. -->
        </node>
        <node pathContains="/cq:annotations">
            <property name="text" translate="false"/> <!-- translation workflows running on content saved in /content/geometrixx, will not extract text if part of cq:annotations node. -->
        </node>
    </node>
    <!-- translation rules for Geometrixx Outdoors site (example) -->
    <node path="/content/geometrixx-outdoors">
        <node resourceType ="foundation/components/image">
            <property name="alternateText"/>
            <property name="jcr:title" />
        </node>
        <node resourceType ="geometrixx-outdoors/components/title">
            <property name="richText"/>
        </node>
    </node>
    <!-- translation rules for ASSETS (example) -->
    <node path="/content/dam">
        <!-- configure list of metadata properties here -->
        <property name="dc:title" />
        <property name="dc:description" />
    </node>
    <!-- translation rules for extracting ASSETS from SITES content, configure all components that embed or reference assets -->
    <assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/video" assetReferenceAttribute="asset"/>
    <assetNode resourceType="foundation/components/download" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="foundation/components/mobileimage" assetReferenceAttribute="fileReference"/>
    <assetNode resourceType="wcm/foundation/components/image" assetReferenceAttribute="fileReference"/>
</nodelist>
```

