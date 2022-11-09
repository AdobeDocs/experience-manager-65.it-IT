---
title: Personalizzare i componenti core CIF
description: Scopri come personalizzare AEM componenti core CIF. L’esercitazione illustra come estendere in modo sicuro un componente core CIF per soddisfare i requisiti aziendali specifici. Scopri come estendere una query GraphQL per restituire un attributo personalizzato e visualizzare il nuovo attributo in un componente core CIF.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 8933942e-be49-49d3-bf0a-7225257e2803
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 24%

---

# Personalizzare i componenti core CIF di AEM {#customize-cif-components}

La [CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) è una base di codice di riferimento per l&#39;utilizzo di [Componenti core CIF](https://github.com/adobe/aem-core-cif-components). In questa esercitazione, estenderai ulteriormente la [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) per visualizzare un attributo personalizzato da Adobe Commerce. Ulteriori informazioni sull’integrazione GraphQL tra AEM e Adobe Commerce e gli hook di estensione forniti dai componenti core CIF.

>[!TIP]
>
>Utilizza la [Archetipo AEM progetto](https://github.com/adobe/aem-project-archetype) all’avvio dell’implementazione Commerce personalizzata.

## Cosa Verrà Generato

Il brand Venia ha recentemente iniziato a produrre alcuni prodotti utilizzando materiali sostenibili e l&#39;azienda desidera mostrare un **Ecologico** come parte del Product Teaser. In Adobe Commerce verrà creato un nuovo attributo personalizzato per indicare se un prodotto utilizza l’ **Ecologico** materiale. Questo attributo personalizzato verrà quindi aggiunto come parte della query GraphQL e visualizzato sul Product Teaser per prodotti specifici.

![Implementazione finale del badge eco-compatibile](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Prerequisiti {#prerequisites}

Per completare questa esercitazione è necessario un ambiente di sviluppo locale. Questo include un&#39;istanza in esecuzione di AEM configurata e connessa a un&#39;istanza Adobe Commerce. Rivedi i requisiti e le fasi per [creazione di uno sviluppo locale con AEM](../develop.md). Per seguire completamente l’esercitazione, dovrai disporre delle autorizzazioni per aggiungere [Attributi a un prodotto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) in Adobe Commerce.

Sarà inoltre necessario GraphQL IDE come [GraphiQL](https://github.com/graphql/graphiql) o un&#39;estensione del browser per eseguire gli esempi di codice e le esercitazioni. Se installi un&#39;estensione del browser, assicurati che sia in grado di impostare le intestazioni della richiesta. Su Google Chrome, [Client Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) è un&#39;estensione che può eseguire il lavoro.

## Clona il progetto Venia {#clone-venia-project}

Cloneremo il [Progetto Venia](https://github.com/adobe/aem-cif-guides-venia) quindi sovrascrivi gli stili predefiniti.

>[!NOTE]
>
>**Sentitevi liberi di utilizzare un progetto esistente** (in base al AEM Project Archetype con CIF incluso) e salta questa sezione.

1. Esegui il seguente comando git per clonare il progetto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza Adobe Commerce o aggiungi le configurazioni al progetto appena creato.

1. A questo punto, dovresti disporre di una versione funzionante di una vetrina connessa a un&#39;istanza di Adobe Commerce. Passa a `US` > `Home` pagina in: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandi il menu principale della vetrina, dovresti vedere diverse categorie, a indicare che la connessione ad Adobe Commerce funziona.

   ![Storefront configurato con il tema Venia](../assets/customize-cif-components/venia-store-configured.png)

## Creare il Product Teaser {#author-product-teaser}

Il componente Product Teaser verrà esteso durante l’esercitazione. Come primo passo, aggiungi una nuova istanza del Product Teaser alla home page per comprendere la funzionalità di base.

1. Passa alla **home page** del sito: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Inserisci un nuovo componente **Product Teaser** nel contenitore di layout principale della pagina.

   ![Inserire Product Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. Espandi il pannello laterale (se non è già attivato) e imposta il menu a discesa di ricerca risorse su **Prodotti**. Dovrebbe essere visualizzato un elenco di prodotti disponibili da un’istanza Adobe Commerce connessa. Seleziona un prodotto e **trascinalo** sul componente **Product Teaser** nella pagina.

   ![Trascinare su Product Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   >Puoi anche configurare il prodotto visualizzato impostando il componente tramite la finestra di dialogo (clic sull’icona a forma di _chiave inglese_).

4. Ora puoi vedere un prodotto visualizzato dal Product Teaser. Il nome del prodotto e il prezzo del prodotto sono attributi predefiniti visualizzati.

   ![Product Teaser - stile predefinito](../assets/customize-cif-components/product-teaser-default-style.png)

## Aggiungere un attributo personalizzato in Adobe Commerce {#add-custom-attribute}

I prodotti e i dati di prodotto visualizzati in AEM vengono memorizzati in Adobe Commerce. Aggiungere quindi un nuovo attributo per **Ecologico** come parte dell’attributo di prodotto impostato utilizzando l’interfaccia utente di Adobe Commerce.

>[!TIP]
>
>Disponi già di un **Sì/No** come parte del set di attributi del prodotto? Puoi usarlo e saltare questa sezione.

1. Accedi alla tua istanza Adobe Commerce.
1. Passa a **Catalogo** > **Prodotti**.
1. Aggiorna il filtro di ricerca per trovare il **Prodotto configurabile** utilizzato quando aggiunto al componente Teaser nell’esercizio precedente. Apri il prodotto in modalità di modifica.

   ![Cerca prodotto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. Dalla visualizzazione del prodotto, fai clic su **Aggiungi attributo** > **Crea nuovo attributo**.
1. Compila il **Nuovo attributo** modulo con i seguenti valori (lasciare le impostazioni predefinite per altri valori)

   | Set di campi | Etichetta campo | Valore |
   | ----------------------------- | ------------------ | ---------------- |
   | Proprietà attributo | Etichetta attributo | **Ecologico** |
   | Proprietà attributo | Tipo di ingresso catalogo | **Sì/No** |
   | Proprietà attributo avanzate | Codice attributo | **eco_friendly** |

   ![Nuovo modulo attributo](../assets/customize-cif-components/attribute-new-form.png)

   Fai clic su **Salva attributo** una volta finito.

1. Scorri fino alla parte inferiore del prodotto ed espandi il **Attributi** intestazione. Dovresti vedere il nuovo **Ecologico** campo . Passa a **Sì**.

   ![Passa a Sì](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Salva** le modifiche apportate al prodotto.

   >[!TIP]
   >
   >Ulteriori dettagli sulla gestione [Gli attributi del prodotto si trovano nella guida utente di Adobe Commerce](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Passa a **Sistema** > **Strumenti** > **Gestione cache**. Poiché è stato effettuato un aggiornamento allo schema dati, è necessario annullare la validità di alcuni tipi di cache in Adobe Commerce.
1. Seleziona la casella accanto a **Configurazione** e invia il tipo di cache per **Aggiorna**

   ![Aggiorna tipo di cache di configurazione](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   >Maggiori dettagli [Gestione della cache si trova nella guida utente di Adobe Commerce](https://docs.magento.com/user-guide/system/cache-management.html).

## Utilizzare un IDE GraphQL per verificare l&#39;attributo {#use-graphql-ide}

Prima di saltare nel codice AEM è utile esplorare [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) utilizzando un IDE GraphQL. L’integrazione di Adobe Commerce con AEM viene eseguita principalmente tramite una serie di query GraphQL. Comprendere e modificare le query GraphQL è uno dei modi principali in cui è possibile estendere i componenti core CIF.

Quindi, utilizza un IDE GraphQL per verificare che `eco_friendly` è stato aggiunto al set di attributi del prodotto. Le schermate in questa esercitazione utilizzano [Client Altair GraphQL](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Apri l’IDE GraphQL e immetti l’URL . `http://<server>/graphql` nella barra degli URL dell’IDE o dell’estensione.
2. Aggiungi quanto segue [query sui prodotti](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) dove `YOUR_SKU` è **SKU** del prodotto utilizzato nell&#39;esercizio precedente:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Esegui la query e ottieni una risposta come quella riportata di seguito:

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![Esempio di risposta GraphQL](../assets/customize-cif-components/sample-graphql-query.png)

   Tieni presente che il valore di **Sì** è un numero intero di **1**. Questo sarà utile quando scriviamo la query GraphQL in Java.

   >[!TIP]
   >
   >Documentazione più dettagliata su [Adobe Commerce GraphQL è disponibile qui](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Aggiornare il modello Sling per il Product Teaser {#updating-sling-model-product-teaser}

Ora estenderemo la logica di business del Product Teaser implementando un modello Sling. I [modelli Sling](https://sling.apache.org/documentation/bundles/models.html) sono “POJO” (Plain Old Java Objects) basati su annotazioni che implementano la logica di business necessaria per il componente. I modelli Sling vengono utilizzati insieme agli script HTL come parte del componente. Seguiremo il [pattern di delega per modelli Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) in modo da estendere solo parti del modello esistente di Product Teaser.

I modelli Sling sono implementati come Java e si trovano nel modulo **core** del progetto generato.

Utilizzo [l&#39;IDE che preferisci](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#set-up-the-development-ide) importare il progetto Venia. Le schermate utilizzate sono [IDE codice di Visual Studio](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?#microsoft-visual-studio-code).

1. Nell’IDE, naviga sotto la **nucleo centrale** modulo per: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE posizione core](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` è un’interfaccia Java che estende CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) interfaccia.

   È già stato aggiunto un nuovo metodo denominato `isShowBadge()` per visualizzare un badge se il prodotto è considerato &quot;Nuovo&quot;.

1. Aggiungi il nuovo metodo `isEcoFriendly()` all’interfaccia:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Questo è un nuovo metodo che introdurremo per incapsulare la logica per indicare se il prodotto ha `eco_friendly` attributo impostato su **Sì** o **No**.

1. Quindi, controlla il `MyProductTeaserImpl.java` a `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   La [pattern di delega per modelli Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) permette `MyProductTeaserImpl` riferimento `ProductTeaser` tramite `sling:resourceSuperType` proprietà:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Per tutti i metodi che non dovranno essere ignorati o modificati, possiamo semplicemente restituire il valore che `ProductTeaser` restituisce. Esempio:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Questo riduce al minimo la quantità di codice Java che un&#39;implementazione deve scrivere.

1. Uno dei punti di estensione aggiuntivi forniti dai componenti core CIF di AEM è il `AbstractProductRetriever` che fornisce l’accesso a attributi di prodotto specifici. Inspect `initModel()` metodo:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   La `@PostConstruct` l’annotazione assicura che questo metodo venga chiamato non appena viene inizializzato il modello Sling.

   La query GraphQL del prodotto è già stata estesa utilizzando la variabile `extendProductQueryWith` metodo per recuperare l&#39;ulteriore `created_at` attributo. Questo attributo viene successivamente utilizzato come parte del `isShowBadge()` metodo .

1. Aggiorna la query GraphQL per includere il `eco_friendly` attributo nella query parziale:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   Con l’aggiunta al metodo `extendProductQueryWith`, gli attributi di prodotto aggiuntivi saranno disponibili per il resto del modello. Inoltre si riduce la quantità di query eseguite.

   Nel codice di cui sopra, il`addCustomSimpleField` viene utilizzato per recuperare `eco_friendly` attributo. Questo illustra come eseguire una query per gli attributi personalizzati che fanno parte dello schema Adobe Commerce.

   >[!NOTE]
   >
   >La `createdAt()` è stato effettivamente implementato come parte del [Interfaccia prodotto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). La maggior parte degli attributi dello schema comunemente trovati è già stata implementata, quindi utilizza solo gli attributi `addCustomSimpleField` per gli attributi realmente personalizzati.

1. Aggiungi un logger per eseguire il debug del codice Java:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Quindi, implementa `isEcoFriendly()` metodo:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   Nel metodo precedente, la `productRetriever` viene utilizzato per recuperare il prodotto e `getAsInteger()` viene utilizzato per ottenere il valore del `eco_friendly` attributo. In base alle query GraphQL eseguite in precedenza, sappiamo che il valore previsto quando `eco_friendly` attributo impostato su &quot;**Sì**&quot; è in realtà un numero intero di **1**.

   Ora che il modello Sling è stato aggiornato, il markup del componente deve essere aggiornato per visualizzare effettivamente un indicatore di **Ecologico** basato sul modello Sling.

## Personalizzazione del markup del Product Teaser {#customize-markup-product-teaser}

I componenti AEM vengono spesso estesi per modificare il markup generato dal componente. A tal fine, sovrascrivi lo [script HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) utilizzato dal componente per eseguire il rendering del relativo markup. HTML Template Language (HTL) è un linguaggio per modelli leggero usato dai componenti di AEM per eseguire il rendering dinamico del markup in base al contenuto creato, in modo che sia possibile riutilizzare i componenti. Il Product Teaser, ad esempio, può essere riutilizzato più volte per visualizzare prodotti diversi.

Nel nostro caso, vogliamo eseguire il rendering di un banner sopra il teaser per indicare che il prodotto è &quot;eco-compatibile&quot; in base a un attributo personalizzato. Il modello di progettazione per [personalizzare il markup](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) di un componente è in realtà standard per tutti i componenti di AEM, non solo per i componenti core CIF di AEM.

>[!NOTE]
>
>Se personalizzi un componente utilizzando i selettori di prodotti CIF e categorie come questo Product Teaser o il componente di pagina CIF, accertati di includere il `cif.shell.picker` clientlib per le finestre di dialogo dei componenti. Vedi [Utilizzo del selettore di prodotti e categorie CIF](use-cif-pickers.md) per i dettagli.

1. Nell’IDE, naviga ed espandi la `ui.apps` modulo ed espandi la gerarchia delle cartelle per: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e ispezionare `.content.xml` file.

   ![ui.apps di Product Teaser](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   Questa è la definizione del componente Product Teaser usato nel nostro progetto. Osserva la proprietà `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Questo è un esempio di creazione di un [componente Proxy](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components). Invece di copiare e incollare tutti gli script HTL di Product Teaser dai componenti core CIF di AEM, possiamo utilizzare `sling:resourceSuperType` per ereditare tutte le funzionalità.

1. Aprire il file `productteaser.html`. Questa è una copia del `productteaser.html` dal [Product Teaser CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Si noti che il modello Sling per `MyProductTeaser` viene utilizzato e assegnato al `product` variabile.

1. Modifica `productteaser.html` per effettuare una chiamata al `isEcoFriendly` metodo applicato nell&#39;esercizio precedente:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   Quando si chiama un metodo Sling Model in HTL, la variabile `get` e `is` parte del metodo viene eliminata e la prima lettera viene minuscola. Quindi `isShowBadge()` diventa `.showBadge` e `isEcoFriendly` diventa `.ecoFriendly`. In base al valore booleano restituito da `.isEcoFriendly()` determina se la `<span>Eco Friendly</span>` viene visualizzato.

   Ulteriori informazioni `data-sly-test` e altri [Le istruzioni per il blocco HTL si trovano qui](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. Salva le modifiche e distribuisci gli aggiornamenti per AEM utilizzando le tue competenze Maven, da un terminale di riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Apri una nuova finestra del browser e passa a AEM e **Console OSGi** > **Stato** > **Modelli Sling**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Cerca `MyProductTeaserImpl` e dovresti vedere una riga come la seguente:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Questo indica che il modello Sling è stato distribuito correttamente e mappato al componente corretto.

1. Aggiorna a **Home page Venia** a [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) dove è stato aggiunto il Product Teaser.

   ![Messaggio eco-friendly visualizzato](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Se il prodotto ha il `eco_friendly` attributo impostato su **Sì**, dovresti vedere il testo &quot;Eco-friendly&quot; sulla pagina . Prova a passare a prodotti diversi per vedere il cambiamento di comportamento.

1. Apri il AEM `error.log` per visualizzare le istruzioni di registro aggiunte. La `error.log` si trova in `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Cerca nei registri AEM per visualizzare le istruzioni di registro aggiunte nel modello Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   >È inoltre possibile che vengano visualizzate delle tracce di stack se il prodotto utilizzato nel teaser non contiene `eco_friendly` come parte del set di attributi.

## Aggiungi stili per il badge eco-compatibile {#add-styles}

A questo punto, la logica che determina quando visualizzare il **Ecologico** il badge funziona, tuttavia il testo normale potrebbe utilizzare alcuni stili. Quindi aggiungi un’icona e gli stili al `ui.frontend` per completare l’implementazione.

1. Scarica la [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) file. Viene utilizzato come **Ecologico** badge.
1. Torna all’IDE e passa alla `ui.frontend` cartella.
1. Aggiungi il `eco_friendly.svg` al `ui.frontend/src/main/resources/images` cartella:

   ![SVG eco-compatibile aggiunto](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Apri il file . `productteaser.scss` a `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Aggiungi le seguenti regole Sass all&#39;interno della `.productteaser` Classe:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   >Consulta [Definizione dello stile dei componenti core CIF](./style-cif-component.md) per maggiori dettagli sui flussi di lavoro front-end.

1. Salva le modifiche e distribuisci gli aggiornamenti per AEM utilizzando le tue competenze Maven, da un terminale di riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Aggiorna a **Home page Venia** a [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) dove è stato aggiunto il Product Teaser.

   ![Implementazione finale del badge eco-compatibile](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Congratulazioni {#congratulations}

Hai appena personalizzato il tuo primo componente CIF di AEM. Scarica la [file della soluzione completati qui](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Sfida bonus {#bonus-challenge}

Esamina la funzionalità del **Nuovo** badge già implementato nel Product Teaser. Prova ad aggiungere una casella di controllo aggiuntiva per consentire agli autori di controllare quando il **Ecologico** deve essere visualizzato il badge . Sarà necessario aggiornare la finestra di dialogo del componente in `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Nuova sfida per l&#39;implementazione dei badge](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Risorse aggiuntive {#additional-resources}

- [AEM Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalizzazione dei componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [Personalizzazione dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [Guida introduttiva di AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)
- [Utilizzo del selettore di prodotti e categorie CIF](use-cif-pickers.md)
