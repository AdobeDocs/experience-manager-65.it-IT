---
title: Personalizzare lo stile dei componenti core CIF di Adobe Experience Manager
description: Scopri come assegnare uno stile ai componenti core CIF di Adobe Experience Manager. Il tutorial illustra come le librerie lato client o clientlibs vengono utilizzate per distribuire e gestire CSS e JavaScript per un’implementazione Commerce di Adobe Experience Manager (AEM). Questo tutorial illustra anche come il modulo ui.frontend e un progetto Webpack vengono integrati nel processo di build end-to-end.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
exl-id: 04d553be-c67d-4ecb-a23f-2694c2adfc2b
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '2531'
ht-degree: 20%

---

# Personalizzare lo stile dei componenti core CIF di AEM {#style-aem-cif-core-components}

Il [Progetto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) è una base di codice di riferimento per l’utilizzo di [Componenti core CIF](https://github.com/adobe/aem-core-cif-components). In questo tutorial, analizzerai il progetto di riferimento Venia e capirai come sono organizzati i CSS e JavaScript utilizzati dai componenti core CIF dell’AEM. Creerai inoltre uno stile CSS con cui aggiornare lo stile predefinito del **Product Teaser** componente.

>[!TIP]
>
>Utilizza il [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype) all’avvio dell’implementazione di commerce.

## Cosa verrà creato

In questo tutorial, viene implementato un nuovo stile per il componente Product Teaser, che assomiglia a una scheda. Le lezioni apprese nell’esercitazione possono essere applicate ad altri Componenti core CIF.

![Cosa verrà creato](../assets/style-cif-component/what-you-will-build.png)

## Prerequisiti {#prerequisites}

Per completare questa esercitazione è necessario un ambiente di sviluppo locale. Ciò include un’istanza in esecuzione dell’AEM configurata e connessa a un’istanza Adobe Commerce. Rivedi i requisiti e i passaggi per [sviluppo locale con l&#39;AEM](../develop.md).

## Clonare il progetto Venia {#clone-venia-project}

Cloniamo il [Progetto Venia](https://github.com/adobe/aem-cif-guides-venia) e quindi ignorare gli stili predefiniti.

>[!NOTE]
>
>**Puoi utilizzare un progetto esistente** (in base all’archetipo del progetto AEM con CIF incluso) e salta questa sezione.

1. Esegui il seguente comando Git per clonare il progetto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza Adobe Commerce o aggiungi le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di una vetrina connessa a un’istanza di Adobe Commerce. Accedi a `US` > `Home` pagina in: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandendo il menu principale della vetrina, dovresti vedere diverse categorie, a indicare che la connessione ad Adobe Commerce funziona.

   ![Vetrina configurata con il tema Venia](../assets/style-cif-component/venia-store-configured.png)

## Librerie client e modulo ui.frontend {#introduction-to-client-libraries}

I CSS e JavaScript responsabili del rendering del tema o degli stili della vetrina sono gestiti in AEM da un [libreria client](/help/sites-developing/clientlibs.md) o clientlibs in breve. Le librerie client forniscono un meccanismo per organizzare CSS e JavaScript nel codice di un progetto e quindi distribuirli sulla pagina.

Gli stili specifici del brand possono essere applicati ai componenti core CIF dell’AEM aggiungendo e ignorando i CSS gestiti da queste librerie client. È fondamentale comprendere in che modo le librerie client sono strutturate e incluse nella pagina.

Il [ui.frontend](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) è un [webpack](https://webpack.js.org/) per gestire tutte le risorse front-end di un progetto. Questo consente agli sviluppatori front-end di utilizzare un numero qualsiasi di lingue e tecnologie come [TypeScript](https://www.typescriptlang.org/), [Sass](https://sass-lang.com/) e molto altro.

Il `ui.frontend` è anche un modulo Maven e integrato con il progetto più ampio utilizzando un modulo NPM [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator). Durante una build, il `aem-clientlib-generator` copia i file CSS e JavaScript compilati in una libreria client in `ui.apps` modulo.

![Architettura ui.frontend to ui.apps](../assets/style-cif-component/ui-frontend-architecture.png)

*I file CSS e JavaScript compilati vengono copiati dal file `ui.frontend` modulo in `ui.apps` come libreria client durante una build Maven*

## Aggiornare lo stile del teaser {#ui-frontend-module}

Quindi, apporta una piccola modifica allo stile Teaser per vedere come `ui.frontend` e le librerie client funzionano. Utilizzare [l&#39;IDE di tua scelta](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) per importare il progetto Venia. Le schermate utilizzate provengono da [IDE codice Visual Studio](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. Naviga ed espandi **ui.frontend** ed espandere la gerarchia delle cartelle in modo da: `ui.frontend/src/main/styles/commerce`:

   ![Cartella commerce ui.frontend](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   Si noti che sono presenti più istanze Sass (`.scss`) sotto la cartella. Si tratta degli stili specifici di Commerce per ciascuno dei componenti di Commerce.

1. Apri il file `_productteaser.scss`.

1. Aggiornare il `.item__image` e modificare la regola di bordo:

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
   }
   ```

   La regola di cui sopra deve aggiungere un bordo rosa grassetto al componente Product Teaser.

1. Apri una nuova finestra del terminale e passa alla `ui.frontend` cartella:

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. Esegui il seguente comando Maven:

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect l’uscita del terminale. Puoi vedere che il comando Maven ha eseguito diversi script NPM, tra cui `npm run build`. Il `npm run build` è definito nel `package.json` e ha l’effetto di compilare il progetto webpack e attivare la generazione della libreria client.

1. Inspect il file `ui.frontend/dist/clientlib-site/site.css`:

   ![CSS sito compilato](../assets/style-cif-component/comiled-site-css.png)

   Il file è la versione compilata e minimizzata di tutti i file Sass nel progetto.

   >[!NOTE]
   >
   >File di questo tipo vengono ignorati dal controllo del codice sorgente poiché devono essere generati durante il tempo di creazione.

1. Inspect il file `ui.frontend/clientlib.config.js`.

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   File di configurazione per [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator) e determina dove e come i file CSS e JavaScript compilati verranno trasformati in una libreria client AEM.

1. In `ui.apps` il modulo ispeziona il file: `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![CSS sito compilato in ui.apps](../assets/style-cif-component/comiled-css-ui-apps.png)

   Questo copia il `site.css` file in `ui.apps` progetto. Ora fa parte di una libreria client denominata `clientlib-site` con una categoria `venia.site`. Una volta che il file è parte di `ui.apps` può essere implementato in AEM.

   >[!NOTE]
   >
   >File di questo tipo vengono ignorati anche dal controllo del codice sorgente in quanto devono essere generati durante il tempo di creazione.

1. Quindi, esamina le altre librerie client generate dal progetto:

   ![Altre librerie client](../assets/style-cif-component/other-clientlibs.png)

   Queste librerie client non sono gestite da `ui.frontend` modulo. Queste librerie client includono invece le dipendenze CSS e JavaScript fornite da Adobe. La definizione di queste librerie client si trova in `.content.xml` sotto ogni cartella.

   **clientlib-base**: si tratta di una libreria client vuota che incorpora semplicemente le dipendenze necessarie dai [componenti core di AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it). La categoria è `venia.base`.

   **clientlib-cif** : si tratta anche di una libreria client vuota che incorpora semplicemente le dipendenze necessarie da [Componenti core CIF dell’AEM](https://github.com/adobe/aem-core-cif-components). La categoria è `venia.cif`.

   **clientlib-grid** - Questo include il CSS necessario per abilitare la funzione Griglia reattiva AEM. L&#39;utilizzo della griglia AEM consente [Modalità Layout](/help/sites-authoring/responsive-layout.md) nell’editor dell’AEM e consente agli autori di contenuti di ridimensionare i componenti. La categoria è `venia.grid` ed è incorporato nella `venia.base` libreria.

1. Inspect i file `customheaderlibs.html` e `customfooterlibs.html` sotto `ui.apps/src/main/content/jcr_root/apps/venia/components/page`:

   ![Script personalizzati per intestazione e piè di pagina](../assets/style-cif-component/custom-header-footer-script.png)

   Questi script includono **venia.base** e **venia.cif** come parte di tutte le pagine.

   >[!NOTE]
   >
   >Solo le librerie di base sono &quot;hardcoded&quot; come parte degli script di pagina. `venia.site` non è incluso in questi file, ma come parte del modello della pagina per una maggiore flessibilità. Questo viene ispezionato più avanti.

1. Dal terminale, crea e implementa l’intero progetto in un’istanza locale dell’AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## Creare un Product Teaser {#author-product-teaser}

Ora che gli aggiornamenti del codice sono stati distribuiti, aggiungi una nuova istanza del componente Product Teaser alla home page del sito utilizzando gli strumenti di creazione AEM. Questo consente di visualizzare gli stili aggiornati.

1. Apri una nuova scheda del browser e passa a **Home page** del sito: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Espandi il Finder risorse (la barra laterale) in **Modifica** modalità. Cambia il filtro Risorse in **Prodotti**.

   ![Espandere Asset Finder e filtrare per prodotti](../assets/style-cif-component/drag-drop-product-page.png)

1. Trascina e rilascia un nuovo prodotto nella home page nel Contenitore di layout principale:

   ![Product Teaser con bordo rosa](../assets/style-cif-component/pink-border-product-teaser.png)

   Dovresti notare che il Product Teaser ora presenta un bordo rosa brillante in base alla modifica della regola CSS creata in precedenza.

## Verificare le librerie client sulla pagina {#verify-client-libraries}

Verifica quindi l’inclusione delle librerie client nella pagina.

1. Accedi a **Home page** del sito: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleziona il menu **Informazioni pagina** e fai clic su **Visualizza come pubblicato**:

   ![Visualizza come pubblicato](../assets/style-cif-component/view-as-published.png)

   Viene aperta la pagina senza caricare alcun JavaScript di authoring dell’AEM, come apparirebbe sul sito pubblicato. Tieni presente che l’URL contiene il parametro di query `?wcmmode=disabled` aggiunto. Quando si sviluppano CSS e JavaScript, è buona norma utilizzare questo parametro per semplificare la pagina senza nulla che venga creato dall’AEM.

1. Visualizza il codice sorgente della pagina e individua diverse librerie client incluse:

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   Le librerie client consegnate alla pagina hanno il prefisso `/etc.clientlibs` e vengono serviti tramite una [proxy](/help/sites-developing/clientlibs.md) per evitare di esporre oggetti sensibili in `/apps` o `/libs`.

   Avviso `venia/clientlibs/clientlib-site.min.css` e `venia/clientlibs/clientlib-site.min.js`. Si tratta dei file CSS e JavaScript compilati derivati dal `ui.frontend` modulo.

## Inclusione della libreria client con i modelli di pagina {#client-library-inclusion-pagetemplates}

Sono disponibili diverse opzioni per includere una libreria lato client. Successivo: controlla come il progetto generato include `clientlib-site` librerie tramite [Modelli di pagina](/help/sites-developing/templates.md).

1. Accedi a **Home page** del sito nell’ambito dell’editor AEM: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleziona la **Informazioni pagina** e fai clic su **Modifica modello**:

   ![Modifica il modello](../assets/style-cif-component/edit-template.png)

   Verrà aperto il **Pagina di destinazione** modellare **Home** La pagina si basa su.

   >[!NOTE]
   >
   >Per visualizzare tutti i modelli disponibili nella schermata iniziale dell&#39;AEM, passare a **Strumenti** > **Generale** > **Modelli**.

1. Nell’angolo in alto a sinistra, seleziona l’icona **Informazioni pagina** e fai clic su **Criterio pagina**.

   ![Voce di menu Criterio pagina](../assets/style-cif-component/page-policy-menu.png)

1. Verrà visualizzato il criterio pagina per il modello Pagina di destinazione:

   ![Criterio pagina - pagina di destinazione](../assets/style-cif-component/page-policy-properties.png)

   Sul lato destro è disponibile un elenco delle librerie client **categorie** che verranno incluse in tutte le pagine che utilizzano questo modello.

   * `venia.dependencies` : fornisce librerie di fornitori che `venia.site` dipende da.
   * `venia.site` - Categoria per `clientlib-site` che il `ui.frontend` generata dal modulo.

   Altri modelli utilizzano lo stesso criterio, **Pagina contenuto**, **Pagina di destinazione** e così via. Riutilizzando lo stesso criterio, possiamo essere certi che le stesse librerie client vengano incluse in tutte le pagine.

   Quando si gestisce l’inclusione delle librerie client mediante l’uso di modelli e criteri di pagina, si può modificare il criterio a livello di modello. Ad esempio, supponiamo di dover gestire due marchi diversi nella stessa istanza di AEM. Ogni marchio ha un proprio stile o *tema* ma le librerie e il codice di base saranno gli stessi. Un altro esempio, nel caso di una libreria client più grande che si voglia visualizzare solo su determinate pagine, si può creare un criterio di pagina univoco solo per quel modello.

## Sviluppo Webpack locale {#local-webpack-development}

Nell’esercizio precedente, è stato effettuato un aggiornamento a un file Sass nel `ui.frontend` e quindi, dopo aver eseguito una build Maven, le modifiche vengono distribuite all’AEM. Ora esaminiamo l’utilizzo di un webpack-dev-server per sviluppare rapidamente gli stili front-end.

Il webpack-dev-server proxy le immagini e alcuni file CSS/JavaScript dell’istanza locale dell’AEM, ma consente allo sviluppatore di modificare gli stili e JavaScript nel `ui.frontend` modulo.

1. Nel browser passa a **Home** pagina e **Visualizza come pubblicato**: [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled).

1. Visualizza l’origine della pagina e **copia** il HTML non elaborato della pagina.

1. Torna all&#39;IDE che preferisci sotto `ui.frontend` modulo apri il file: `ui.frontend/src/main/static/index.html`

   ![File HTML statico](../assets/style-cif-component/static-index-html.png)

1. Sovrascrivi il contenuto di `index.html` e **incolla** HTML copiato nel passaggio precedente.

1. Trova le inclusioni per `clientlib-site.min.css`, `clientlib-site.min.js` e **rimuovere** loro.

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   Questi vengono rimossi perché rappresentano la versione compilata dei CSS e JavaScript generati dai `ui.frontend` modulo. Lascia le altre librerie client così come verranno proxy dall’istanza AEM in esecuzione.

1. Apri una nuova finestra del terminale e accedi al `ui.frontend` cartella. Esegui il comando `npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   Verrà avviato Webpack-dev-server su [http://localhost:8080/](Http://localhost:8080/)

   >[!CAUTION]
   >
   >Se si verifica un errore relativo a Sass, arrestare il server ed eseguire il comando `npm rebuild node-sass` e ripetere i passaggi precedenti. Ciò può verificarsi se disponi di una versione diversa di `npm` e `node` quindi specificato nel progetto `aem-cif-guides-venia/pom.xml`.

1. Accedi a [http://localhost:8080/](Http://localhost:8080/) in una nuova scheda con lo stesso browser di un’istanza di AEM registrata. Dovresti vedere la home page di Venia tramite il webpack-dev-server:

   ![Server di sviluppo Webpack sulla porta 80](../assets/style-cif-component/webpack-dev-server-port80.png)

   Lascia web pack-dev-server in esecuzione. Viene utilizzato nell&#39;esercizio successivo.

## Implementare lo stile della scheda per Product Teaser {#update-css-product-teaser}

Modificare i file Sass in `ui.frontend` per implementare uno stile di tipo scheda per il Product Teaser. Webpack-dev-server viene utilizzato per visualizzare rapidamente le modifiche.

Torna all’IDE e al progetto generato.

1. In **ui.frontend** riaprire il file `_productteaser.scss` a `ui.frontend/src/main/styles/commerce/_productteaser.scss`.

1. Apporta le seguenti modifiche al bordo del Product Teaser:

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
           display: block;
           grid-area: main;
           height: auto;
           opacity: 1;
           transition-duration: 512ms;
           transition-property: opacity, visibility;
           transition-timing-function: ease-out;
           visibility: visible;
           width: 100%;
       }
   ```

   Salva le modifiche; webpack-dev-server verrà aggiornato automaticamente con i nuovi stili.

1. Aggiungi un’ombra esterna e includi angoli arrotondati al Product Teaser.

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. Aggiorna il nome del prodotto in modo che venga visualizzato nella parte inferiore del teaser e modifica il colore del testo.

   ```css
   .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

1. Aggiorna il prezzo del prodotto in modo che venga visualizzato nella parte inferiore del teaser e modifica il colore del testo.

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. Aggiorna la query multimediale nella parte inferiore, in modo da sovrapporre il nome e il prezzo in schermi più piccoli di **992 px**.

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   Ora dovresti vedere lo stile della scheda riflesso nel webpack-dev-server:

   ![Modifiche al teaser del server di sviluppo Webpack](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   Tuttavia, le modifiche non sono ancora state implementate nell&#39;AEM. Puoi scaricare il [file della soluzione qui](../assets/style-cif-component/_productteaser.scss).

1. Distribuisci gli aggiornamenti a AEM utilizzando le tue competenze Maven, da un terminale della riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >Sono disponibili [strumenti e configurazione IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) aggiuntivi per sincronizzare i file di progetto direttamente con un’istanza AEM locale senza dover eseguire una generazione Maven completa.

## Visualizzare il Product Teaser aggiornato {#view-updated-product-teaser}

Dopo aver implementato il codice per il progetto nell’AEM, dovresti essere in grado di visualizzare le modifiche apportate al Product Teaser.

1. Torna al browser e aggiorna la home page: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html). Dovresti vedere gli stili del product teaser aggiornati.

   ![Stile del Product Teaser aggiornato](../assets/style-cif-component/product-teaser-new-style.png)

1. Prova ad aggiungere altri Product Teaser. Utilizza la modalità Layout per modificare la larghezza e l’offset dei componenti in modo da visualizzare più teaser su una riga.

   ![Product Teaser multipli](../assets/style-cif-component/multiple-teasers-final.png)

## Risoluzione dei problemi {#troubleshooting}

Puoi verificare in [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) che il file CSS aggiornato sia stato distribuito: [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

Durante la distribuzione di nuovi file CSS e/o JavaScript, è importante anche assicurarsi che il browser non distribuisca file non aggiornati. A tale scopo, cancella la cache del browser o avvia una nuova sessione del browser.

AEM inoltre tenta di memorizzare nella cache le librerie client per migliorare le prestazioni. A volte, dopo la distribuzione del codice, vengono distribuiti i file meno recenti. Puoi annullare manualmente la validità della cache della libreria client di AEM utilizzando lo strumento [Rigenera librerie client](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Se si sospetta che AEM abbia memorizzato nella cache una versione precedente di una libreria client, è meglio annullare la validità della cache. La rigenerazione delle librerie è infatti inefficiente e richiede molto tempo.*

## Congratulazioni {#congratulations}

Hai creato il tuo primo componente core CIF AEM e hai utilizzato un server di sviluppo Webpack.

## Sfida bonus {#bonus-challenge}

Usa il [Sistema di stili di AEM](/help/sites-authoring/style-system.md) per creare due stili che possono essere attivati/disattivati da un autore di contenuti. La sezione su come [sviluppare con il sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html?lang=it) include passaggi dettagliati e informazioni su come eseguire questa operazione.

![Sfida bonus - Sistema di stili](../assets/style-cif-component/bonus-challenge.png)

## Risorse aggiuntive {#additional-resources}

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
* [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
* [Configurare un ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=it)
* [Librerie lato client](/help/sites-developing/clientlibs.md)
* [Guida introduttiva di AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)
* [Sviluppo con il sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html?lang=it)
