---
title: Identificazione del contenuto da tradurre
seo-title: Identifying Content to Translate
description: Scopri come identificare i contenuti da tradurre.
seo-description: Learn how to identify content that needs translating.
uuid: 81b9575c-1c7a-4955-b03f-3f26cbd4f956
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: eedff940-4a46-4c24-894e-a5aa1080d23d
feature: Language Copy
exl-id: 8ca7bbcc-413a-49a8-a836-7083a9cadda1
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 67%

---

# Identificazione del contenuto da tradurre{#identifying-content-to-translate}

Le regole di traduzione identificano il contenuto da tradurre per le pagine, i componenti e le risorse inclusi o esclusi nei progetti di traduzione. Quando una pagina o una risorsa viene tradotta, AEM estrae questo contenuto in modo che possa essere inviato al servizio di traduzione.

Le pagine e le risorse sono rappresentate come nodi nell’archivio JCR. Il contenuto estratto è uno o più valori di proprietà dei nodi. Le regole di traduzione identificano le proprietà che contengono il contenuto da estrarre.

Le regole di traduzione sono espresse in formato XML e memorizzate nelle seguenti posizioni possibili:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

Il file si applica a tutti i progetti di traduzione.

>[!NOTE]
>
>Dopo un aggiornamento alla versione 6.4, si consiglia di spostare il file da /etc. Consulta [Ristrutturazione dell’archivio comune in AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules) per ulteriori dettagli.

Le regole includono le seguenti informazioni:

* Percorso del nodo a cui si applica la regola. La regola si applica anche ai discendenti del nodo.
* Nomi delle proprietà del nodo che contengono il contenuto da tradurre. La proprietà può essere specifica per un tipo di risorsa specifico o per tutti i tipi di risorsa.

Ad esempio, puoi creare una regola che traduca il contenuto aggiunto dagli autori a tutti i componenti Testo di base AEM sulle tue pagine. La regola può identificare il nodo `/content` e la proprietà `text` per il componente `foundation/components/text`.

C’è una [console](#translation-rules-ui) aggiunta per la configurazione delle regole di traduzione. Le definizioni nell’interfaccia utente compileranno il file per tuo conto.

Per una panoramica delle funzioni di traduzione dei contenuti di AEM, vedi [Traduzione di contenuti per siti multilingue](/help/sites-administering/translation.md).

>[!NOTE]
>
>AEM supporta la mappatura uno-a-uno tra i tipi di risorse e gli attributi di riferimento per la traduzione del contenuto di riferimento su una pagina.

## Sintassi delle regole per pagine, componenti e risorse {#rule-syntax-for-pages-components-and-assets}

Una regola è un `node` elemento con uno o più elementi secondari `property` e zero o più elementi figlio secondari`node`:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Ognuno di questi elementi `node` presentano le seguenti caratteristiche:

* L’attributo `path` contiene il percorso del nodo principale del ramo a cui si applicano le regole.
* Gli elementi secondari `property` identificano le proprietà del nodo da tradurre per tutti i tipi di risorse:

   * L’attributo `name` contiene il nome della proprietà.
   * L’attributo opzionale `translate` è uguale a `false` se la proprietà non è tradotta. Il valore per impostazione predefinita è `true`. Questo attributo è utile quando si ignorano le regole precedenti.

* Gli elementi secondari `node` identificano le proprietà del nodo da tradurre per tipi di risorsa specifici:

   * L’attributo `resourceType` contiene il percorso che viene risolto nel componente che implementa il tipo di risorsa.
   * Gli elementi secondari `property` identificano la proprietà nodo da tradurre. Usa questo nodo nello stesso modo degli elementi secondari `property` per le regole dei nodi.

La regola di esempio seguente causa il contenuto di tutte le proprietà `text` da tradurre per tutte le pagine al di sotto del nodo `/content`. La regola è efficace per qualsiasi componente che memorizza il contenuto in una `text` come il componente Testo di base e il componente Immagine di base.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

L’esempio seguente traduce il contenuto di tutti `text` e traduce anche altre proprietà del componente Immagine di base. Se altri componenti hanno proprietà con lo stesso nome, la regola non si applica a essi.

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

## Sintassi delle regole per l’estrazione delle risorse dalle pagine  {#rule-syntax-for-extracting-assets-from-pages}

Utilizza la sintassi della regola seguente per includere le risorse incorporate nei componenti o a cui si fa riferimento da essi:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Ogni elemento `assetNode` presenta le seguenti caratteristiche:

* Un attributo `resourceType` è uguale al percorso che viene risolto nel componente.
* Un attributo `assetReferenceAttribute` che è uguale al nome della proprietà che memorizza il binario della risorsa (per le risorse incorporate) o il percorso della risorsa di riferimento.

L’esempio seguente estrae le immagini dal componente Immagine di base:

```xml
<assetNode resourceType="foundation/components/image" assetReferenceAttribute="fileReference"/>
```

## Regole di sovrascrittura {#overriding-rules}

Il file translation_rules.xml è costituito da un `nodelist` elemento con diversi elementi figlio `node` elementi. AEM legge l’elenco dei nodi dall’alto verso il basso. Quando più regole sono indirizzate allo stesso nodo, viene utilizzata la regola inferiore nel file. Ad esempio, le seguenti regole causano la traduzione di tutto il contenuto in proprietà `text` ad eccezione del ramo `/content/mysite/en` di pagine:

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## Proprietà filtro {#filtering-properties}

Puoi filtrare i nodi con una proprietà specifica utilizzando un elemento `filter`.

Ad esempio, le seguenti regole causano la traduzione di tutto il contenuto in proprietà `text`, ad eccezione dei nodi che hanno la proprietà `draft` impostata su `true`.

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Interfaccia utente per le regole di traduzione {#translation-rules-ui}

È disponibile anche una console per configurare le regole di traduzione.

Per accedervi:

1. Passa a **Strumenti** e poi a **Generale**.

   ![chlimage_1-55](assets/chlimage_1-55.jpeg)

1. Seleziona **Configurazione traduzione**.

   ![chlimage_1-56](assets/chlimage_1-56.jpeg)

Da qui puoi **Aggiungi contesto**. Questo consente di aggiungere un percorso.

![chlimage_1-57](assets/chlimage_1-57.jpeg)

Poi devi selezionare il contesto e fare clic su **Modifica**. Verrà aperto l’Editor delle regole di traduzione.

![chlimage_1-58](assets/chlimage_1-58.jpeg)

È possibile modificare 4 attributi tramite l’interfaccia utente: `isDeep`, `inherit`, `translate` e `updateDestinationLanguage`.

**isDeep** Questo attributo è applicabile ai filtri dei nodi ed è true per impostazione predefinita. Controlla se il nodo (o i suoi predecessori) contiene tale proprietà con il valore della proprietà specificato nel filtro. Se false, controlla solo il nodo corrente.

Ad esempio, i nodi secondari vengono aggiunti a un processo di traduzione anche quando il nodo principale ha una proprietà `draftOnly` imposta su true per contrassegnare il contenuto della bozza. Qui `isDeep` entra in gioco e controlla se i nodi principali hanno proprietà `draftOnly` come true ed esclude tali nodi secondari.

Nell’editor, puoi selezionare/deselezionare **È profondo** nel **Filtri** scheda.

![chlimage_1-59](assets/chlimage_1-59.jpeg)

Ecco un esempio dell’xml risultante quando **È profondo** è deselezionato nell’interfaccia utente:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

**eredita** Questo è applicabile alle proprietà. Per impostazione predefinita, ogni proprietà viene ereditata, ma se desideri che alcune non vengano ereditate dall’elemento secondario, puoi contrassegnarle come false in modo che venga applicata solo a quel nodo specifico.

Nell’interfaccia utente, puoi selezionare/deselezionare **Eredita** nella scheda **Proprietà**.

![chlimage_1-60](assets/chlimage_1-60.jpeg)

**traduci** L’attributo translate viene utilizzato semplicemente per specificare se tradurre o meno una proprietà.

Nell’interfaccia utente, puoi selezionare/deselezionare **Traduci** nella scheda **Proprietà**.

**updateDestinationLanguage** Questo attributo viene utilizzato per le proprietà che non hanno testo ma codici di lingua, ad esempio jcr:language. L&#39;utente non traduce il testo, ma la lingua locale dal sorgente alla destinazione. Tali proprietà non vengono inviate per la traduzione.

Nell’interfaccia utente, puoi selezionare/deselezionare **Traduci** nel **Proprietà** , ma per le proprietà specifiche che hanno come valore i codici lingua.

Per chiarire la differenza tra `updateDestinationLanguage` e `translate`, ecco un semplice esempio di contesto con due sole regole:

![chlimage_1-61](assets/chlimage_1-61.jpeg)

Il risultato nel file xml sarà simile al seguente:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Modifica manuale del file delle regole {#editing-the-rules-file-manually}

Il file translation_rules.xml installato con AEM contiene un set predefinito di regole di traduzione. Puoi modificare il file per supportare i requisiti dei tuoi progetti di traduzione. Ad esempio, puoi aggiungere regole per tradurre il contenuto dei componenti personalizzati.

Se modifichi il file translation_rules.xml, conserva una copia di backup in un pacchetto di contenuti. L’installazione dei service pack dell’AEM o la reinstallazione di alcuni pacchetti AEM può sostituire l’attuale file translation_rules.xml con l’originale. Per ripristinare le regole in questa situazione, puoi installare il pacchetto che contiene la copia di backup.

>[!NOTE]
>
>Dopo aver creato il pacchetto di contenuti, ricostruisci il pacchetto ogni volta che modifichi il file.

## Esempio di file delle regole di traduzione {#example-translation-rules-file}

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
