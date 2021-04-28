---
title: Personalizzare lo stile dei componenti core CIF di AEM
description: Scopri come assegnare uno stile AEM componenti core CIF. L’esercitazione illustra come le librerie lato client o le librerie client vengono utilizzate per distribuire e gestire CSS e JavaScript per un’implementazione Commerce di Adobe Experience Manager (AEM). Questa esercitazione riguarderà anche il modo in cui il modulo ui.frontend e un progetto webpack sono integrati nel processo di compilazione end-to-end.
sub-product: Commerce
topics: Development
version: cloud-service
doc-type: tutorial
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '2566'
ht-degree: 28%

---

# Personalizzare lo stile dei componenti core CIF di AEM {#style-aem-cif-core-components}

Il [CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) è una base di codice di riferimento per l’utilizzo dei [componenti core CIF](https://github.com/adobe/aem-core-cif-components). In questa esercitazione esaminerai il progetto di riferimento Venia e comprenderai come sono organizzati i CSS e JavaScript utilizzati dai componenti core CIF di AEM. Inoltre, creerai un nuovo stile utilizzando CSS per aggiornare lo stile predefinito del componente **Product Teaser**.

>[!TIP]
>
> Utilizza l’ [AEM archetipo di progetto](https://github.com/adobe/aem-project-archetype) all’avvio dell’implementazione di e-commerce.

## Cosa Verrà Generato

In questa esercitazione verrà implementato un nuovo stile per il componente Product Teaser che assomiglia a una scheda. Le lezioni apprese nell’esercitazione possono essere applicate ad altri componenti core CIF.

![Cosa verrà creato](../assets/style-cif-component/what-you-will-build.png)

## Prerequisiti {#prerequisites}

Per completare questa esercitazione è necessario un ambiente di sviluppo locale. Questo include un&#39;istanza in esecuzione di AEM configurata e connessa a un&#39;istanza di Magento. Rivedi i requisiti e i passaggi per [configurare uno sviluppo locale con AEM](../develop.md).

## Clona il progetto Venia {#clone-venia-project}

Dupliceremo il [Progetto Venia](https://github.com/adobe/aem-cif-guides-venia) e quindi sovrascriveremo gli stili predefiniti.

>[!NOTE]
>
> **Puoi anche utilizzare un progetto esistente**  (basato su AEM Project Archetype con CIF incluso) e saltare questa sezione.

1. Esegui il seguente comando git per clonare il progetto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crea e implementa il progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Aggiungi le configurazioni OSGi necessarie per collegare l’istanza AEM a un’istanza di Magento o aggiungi le configurazioni al progetto appena creato.

1. A questo punto è necessario disporre di una versione funzionante di una vetrina che sia collegata a un’istanza di Magento. Passa alla pagina `US` > `Home` in: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Dovresti vedere che la vetrina si basa al momento sul tema Venia. Espandi il menu principale della vetrina: dovresti vedere diverse categorie, a indicare che la connessione a Magento funziona.

   ![Storefront configurato con il tema Venia](../assets/style-cif-component/venia-store-configured.png)

## Librerie client e modulo ui.frontend {#introduction-to-client-libraries}

I CSS e JavaScript responsabili del rendering del tema o degli stili della vetrina sono gestiti in AEM da una [libreria client](/help/sites-developing/clientlibs.md) o clientlibs in breve. Le librerie client consentono di organizzare CSS e JavaScript nel codice di un progetto e quindi di distribuirli sulla pagina.

Gli stili specifici per il marchio possono essere applicati AEM componenti core CIF aggiungendo ed ignorando i CSS gestiti da queste librerie client. È fondamentale comprendere in che modo le librerie client sono strutturate e incluse nella pagina.

Il [ui.frontend](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/uifrontend.html) è un progetto [webpack](https://webpack.js.org/) dedicato per gestire tutte le risorse front-end di un progetto. Questo consente agli sviluppatori front-end di utilizzare un numero qualsiasi di linguaggi e tecnologie come [TypeScript](https://www.typescriptlang.org/), [Sass](https://sass-lang.com/) e molto altro.

Il modulo `ui.frontend` è anche un modulo Maven e integrato con il progetto più grande tramite l&#39;utilizzo di un modulo NPM [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator). Durante una build, il `aem-clientlib-generator` copia i file CSS e JavaScript compilati in una libreria client nel modulo `ui.apps` .

![architettura ui.frontend a ui.apps](../assets/style-cif-component/ui-frontend-architecture.png)

*I CSS e Javascript compilati vengono copiati dal  `ui.frontend` modulo nel  `ui.apps` modulo come libreria client durante una build Maven*

## Aggiornare lo stile del teaser {#ui-frontend-module}

Quindi, apporta una piccola modifica allo stile Teaser per vedere come funzionano il modulo `ui.frontend` e le librerie client. Utilizza [l&#39;IDE che preferisci](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) per importare il progetto Venia. Le schermate utilizzate provengono dall&#39; [IDE di Visual Studio Code](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. Naviga ed espandi il modulo **ui.frontend** ed espandi la gerarchia delle cartelle fino a: `ui.frontend/src/main/styles/commerce`:

   ![cartella di e-commerce ui.frontend](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   Tieni presente che la cartella contiene più file Sass (`.scss`). Si tratta degli stili specifici Commerce per ciascuno dei componenti Commerce .

1. Aprire il file `_productteaser.scss`.

1. Aggiorna la regola `.item__image` e modifica la regola del bordo:

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

   La regola di cui sopra deve aggiungere un bordo rosa molto grassetto al componente Product Teaser.

1. Apri una nuova finestra terminale e passa alla cartella `ui.frontend` :

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

   Inspect l&#39;uscita terminale. Il comando Maven esegue diversi script NPM, tra cui `npm run build`. Il comando `npm run build` è definito nel file `package.json` e ha l&#39;effetto di compilare il progetto webpack e di attivare la generazione della libreria client.

1. Inspect il file `ui.frontend/dist/clientlib-site/site.css`:

   ![CSS del sito compilato](../assets/style-cif-component/comiled-site-css.png)

   Il file è la versione compilata e minimizzata di tutti i file Sass nel progetto.

   >[!NOTE]
   >
   > File come questo vengono ignorati dal controllo del codice sorgente poiché dovrebbero essere generati durante il tempo di creazione.

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

   Questo è il file di configurazione per [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator) e determina dove e come i CSS e JavaScript compilati verranno trasformati in una libreria client AEM.

1. Nel modulo `ui.apps` esamina il file: `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![CSS del sito compilato in ui.apps](../assets/style-cif-component/comiled-css-ui-apps.png)

   Questo copia il file `site.css` nel progetto `ui.apps`. Ora fa parte di una libreria client denominata `clientlib-site` con una categoria `venia.site`. Una volta che il file fa parte del modulo `ui.apps`, può essere distribuito a AEM.

   >[!NOTE]
   >
   > File come questo vengono anche ignorati dal controllo del codice sorgente, in quanto dovrebbero essere generati durante il tempo di creazione.

1. Ispeziona quindi le altre librerie client generate dal progetto:

   ![Altre librerie client](../assets/style-cif-component/other-clientlibs.png)

   Queste librerie client non sono gestite dal modulo `ui.frontend` . Queste librerie client includono invece dipendenze CSS e JavaScript fornite da Adobe. La definizione di queste librerie client si trova nel file `.content.xml` sotto ogni cartella.

   **clientlib-base**: si tratta di una libreria client vuota che incorpora semplicemente le dipendenze necessarie dai [componenti core di AEM](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html). La categoria è `venia.base`.

   **clientlib-cif** : si tratta anche di una libreria client vuota che incorpora semplicemente le dipendenze necessarie dai componenti core CIF di  [AEM](https://github.com/adobe/aem-core-cif-components). La categoria è `venia.cif`.

   **clientlib-grid** : include il CSS necessario per abilitare AEM funzione Griglia reattiva. L’utilizzo della griglia AEM abilita [Modalità layout](/help/sites-authoring/responsive-layout.md) nell’editor AEM e consente agli autori di contenuti di ridimensionare i componenti. La categoria è `venia.grid` ed è incorporata nella libreria `venia.base`.

1. Inspect i file `customheaderlibs.html` e `customfooterlibs.html` sotto `ui.apps/src/main/content/jcr_root/apps/venia/components/page`:

   ![Script personalizzati di intestazione e piè di pagina](../assets/style-cif-component/custom-header-footer-script.png)

   Questi script includono le librerie **venia.base** e **venia.cif** come parte di tutte le pagine.

   >[!NOTE]
   >
   > Solo le librerie di base sono &quot;hard-coded&quot; come parte degli script di pagina. `venia.site` non è incluso in questi file, ma è incluso come parte del modello di pagina per una maggiore flessibilità. Questo verrà esaminato successivamente.

1. Dal terminale, crea e implementa l’intero progetto in un’istanza locale di AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## Creare un Product Teaser {#author-product-teaser}

Dopo aver distribuito gli aggiornamenti di codice, aggiungi una nuova istanza del componente Product Teaser nella home page del sito utilizzando gli strumenti di authoring AEM. Questo ci consentirà di visualizzare gli stili aggiornati.

1. Apri una nuova scheda del browser e passa alla **Home Page** del sito: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Espandi il Asset Finder (barra laterale) in modalità **Modifica** . Cambia il filtro Risorsa in **Prodotti**.

   ![Espandi Asset Finder e filtra per prodotti](../assets/style-cif-component/drag-drop-product-page.png)

1. Trascina un nuovo prodotto nella home page del contenitore di layout principale:

   ![Product Teaser con bordo rosa](../assets/style-cif-component/pink-border-product-teaser.png)

   Dovresti vedere che Product Teaser ora ha un bordo rosa brillante in base alla modifica della regola CSS creata in precedenza.

## Verificare le librerie client sulla pagina {#verify-client-libraries}

Quindi verifica l’inclusione delle librerie client nella pagina.

1. Passa alla **home page** del sito: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleziona il menu **Informazioni pagina** e fai clic su **Visualizza come pubblicato**:

   ![Visualizza come pubblicato](../assets/style-cif-component/view-as-published.png)

   La pagina viene aperta senza caricare alcun JavaScript di authoring di AEM, come apparirebbe sul sito pubblicato. All’URL è stato aggiunto il parametro di query `?wcmmode=disabled` . Quando si sviluppano CSS e JavaScript, è buona norma utilizzare questo parametro per semplificare la pagina senza l’AEM dell’autore.

1. Visualizza l’origine della pagina e individua diverse librerie client incluse:

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

   Le librerie client distribuite alla pagina hanno il prefisso `/etc.clientlibs` e vengono servite tramite un [proxy](/help/sites-developing/clientlibs.md) per evitare di esporre qualsiasi elemento sensibile in `/apps` o `/libs`.

   Avviso `venia/clientlibs/clientlib-site.min.css` e `venia/clientlibs/clientlib-site.min.js`. Si tratta dei file CSS e Javascript compilati derivati dal modulo `ui.frontend` .

## Inclusione della libreria client con i modelli di pagina {#client-library-inclusion-pagetemplates}

Sono disponibili diverse opzioni per includere una libreria lato client. Nella sezione che segue viene esaminato come il progetto generato include le librerie `clientlib-site` tramite [Modelli di pagina](/help/sites-developing/templates.md).

1. Passa alla **Home Page** del sito all&#39;interno dell&#39;Editor di AEM: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Seleziona il menu **Informazioni pagina** e fai clic su **Modifica modello**:

   ![Modificare il modello](../assets/style-cif-component/edit-template.png)

   Verrà aperto il modello **Pagina di destinazione** su cui si basa la pagina **Home**.

   >[!NOTE]
   >
   > Per visualizzare tutti i modelli disponibili dalla schermata iniziale AEM, passa a **Strumenti** > **Generale** > **Modelli**.

1. Nell’angolo in alto a sinistra, seleziona l’icona **Informazioni pagina** e fai clic su **Criterio pagina**.

   ![Voce di menu Criterio pagina](../assets/style-cif-component/page-policy-menu.png)

1. Verrà aperto il Criterio pagina per il modello Pagina di destinazione:

   ![Criterio pagina : pagina di destinazione](../assets/style-cif-component/page-policy-properties.png)

   Sul lato destro è disponibile un elenco delle librerie client **categories** che verranno incluse in tutte le pagine che utilizzano questo modello.

   * `venia.dependencies` - Fornisce tutte le librerie di fornitori da cui  `venia.site` dipende.
   * `venia.site` - Questa è la categoria per  `clientlib-site` la quale il  `ui.frontend` modulo genera.

   Altri modelli utilizzano lo stesso criterio, **Pagina di contenuto**, **Pagina di destinazione** e così via. Riutilizzando lo stesso criterio, possiamo assicurarci che le stesse librerie client siano incluse in tutte le pagine.

   Quando si gestisce l’inclusione delle librerie client mediante l’uso di modelli e criteri di pagina, si può modificare il criterio a livello di modello. Ad esempio, supponiamo di dover gestire due marchi diversi nella stessa istanza di AEM. Ogni marchio avrà un proprio stile o un proprio *tema*, ma le librerie e il codice di base saranno gli stessi. Un altro esempio, nel caso di una libreria client più grande che si voglia visualizzare solo su determinate pagine, si può creare un criterio di pagina univoco solo per quel modello.

## Sviluppo webpack locale {#local-webpack-development}

Nell’esercizio precedente, è stato effettuato un aggiornamento a un file Sass nel modulo `ui.frontend` e dopo aver eseguito una build Maven le modifiche vengono distribuite in AEM. Ora cercheremo di sfruttare un webpack-dev-server per sviluppare rapidamente gli stili front-end.

Il webpack-dev-server proxy le immagini e alcuni dei CSS/JavaScript dell&#39;istanza locale di AEM, ma consente allo sviluppatore di modificare gli stili e JavaScript nel modulo `ui.frontend` .

1. Nel browser passa alla pagina **Home** e **Visualizza come pubblicato**: [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled).

1. Visualizzare l&#39;origine della pagina e **copiare** l&#39;HTML non elaborato della pagina.

1. Torna all’IDE che preferisci sotto il modulo `ui.frontend` per aprire il file: `ui.frontend/src/main/static/index.html`

   ![File HTML statico](../assets/style-cif-component/static-index-html.png)

1. Sovrascrivi il contenuto di `index.html` e **incolla** il codice HTML copiato nel passaggio precedente.

1. Trova gli &quot;include&quot; per `clientlib-site.min.css`, `clientlib-site.min.js` e **rimuovili**.

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

   Questi vengono rimossi perché rappresentano la versione compilata dei CSS e JavaScript generati dal modulo `ui.frontend` . Lascia le altre librerie client così come verranno proxy dall&#39;istanza AEM in esecuzione.

1. Apri una nuova finestra terminale e passa alla cartella `ui.frontend` . Esegui il comando `npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   Questo avvierà il webpack-dev-server su [http://localhost:8080/](Http://localhost:8080/)

   >[!CAUTION]
   >
   > Se ricevi un errore relativo a Sass, interrompi il server ed esegui il comando `npm rebuild node-sass` e ripeti i passaggi precedenti. Questo può verificarsi se disponi di una versione diversa di `npm` e `node` e quindi specificata nel progetto `aem-cif-guides-venia/pom.xml`.

1. Passa a [http://localhost:8080/](Http://localhost:8080/) in una nuova scheda con lo stesso browser di un’istanza di AEM registrata. Dovresti vedere la home page di Venia tramite il webpack-dev-server:

   ![Server di sviluppo Webpack sulla porta 80](../assets/style-cif-component/webpack-dev-server-port80.png)

   Lasciare in esecuzione il webpack-dev-server. Sarà utilizzato nel prossimo esercizio.

## Implementare lo stile della scheda per Product Teaser {#update-css-product-teaser}

Quindi, modifica i file Sass nel modulo `ui.frontend` per implementare uno stile tipo scheda per Product Teaser. Il webpack-dev-server verrà utilizzato per vedere rapidamente le modifiche.

Torna all’IDE e al progetto generato.

1. Nel modulo **ui.frontend** riapri il file `_productteaser.scss` in `ui.frontend/src/main/styles/commerce/_productteaser.scss`.

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

   Salvare le modifiche e il webpack-dev-server dovrebbe aggiornarsi automaticamente con i nuovi stili.

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

1. Aggiorna la query multimediale in basso per impilare il nome e il prezzo in schermate più piccole di **992px**.

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

   ![Modifiche al teaser di Webpack Dev Server](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   Tuttavia, le modifiche non sono state ancora distribuite AEM. Puoi scaricare il [file della soluzione qui](../assets/style-cif-component/_productteaser.scss).

1. Distribuisci gli aggiornamenti per AEM utilizzando le tue competenze Maven, da un terminale a riga di comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >Sono disponibili [strumenti e configurazione IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) aggiuntivi per sincronizzare i file di progetto direttamente con un’istanza AEM locale senza dover eseguire una generazione Maven completa.

## Visualizzare il Product Teaser aggiornato {#view-updated-product-teaser}

Una volta implementato in AEM il codice per il progetto, dovrebbe essere possibile vedere le modifiche apportate al Product Teaser.

1. Torna al browser e aggiorna la home page: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html). Dovresti vedere gli stili del product teaser aggiornati.

   ![Stile del Product Teaser aggiornato](../assets/style-cif-component/product-teaser-new-style.png)

1. Prova ad aggiungere altri Product Teaser. Utilizza la modalità Layout per modificare la larghezza e l’offset dei componenti in modo da visualizzare più teaser su una riga.

   ![Product Teaser multipli](../assets/style-cif-component/multiple-teasers-final.png)

## Risoluzione dei problemi {#troubleshooting}

In [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) puoi verificare che il file CSS aggiornato sia stato distribuito: [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

Quando si distribuiscono nuovi file CSS e/o JavaScript, è importante anche assicurarsi che il browser non distribuisca file non aggiornati. A tale scopo, cancella la cache del browser o avvia una nuova sessione del browser.

AEM inoltre tenta di memorizzare nella cache le librerie client per migliorare le prestazioni. A volte, dopo la distribuzione del codice, vengono distribuiti i file meno recenti. Puoi annullare manualmente la validità della cache della libreria client di AEM utilizzando lo strumento [Rigenera librerie client](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Se si sospetta che AEM abbia memorizzato nella cache una versione precedente di una libreria client, è meglio annullare la validità della cache. La rigenerazione delle librerie è infatti inefficiente e richiede molto tempo.*

## Congratulazioni {#congratulations}

Hai appena formattato il tuo primo componente core CIF AEM e hai utilizzato un server di sviluppo webpack!

## Sfida bonus {#bonus-challenge}

Usa il [Sistema di stili di AEM](/help/sites-authoring/style-system.md) per creare due stili che possono essere attivati/disattivati da un autore di contenuti. La sezione su come [sviluppare con il sistema di stili](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) include passaggi dettagliati e informazioni su come eseguire questa operazione.

![Sfida bonus - Sistema di stili](../assets/style-cif-component/bonus-challenge.png)

## Risorse aggiuntive {#additional-resources}

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
* [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components)
* [Configurare un ambiente di sviluppo AEM locale](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [Librerie lato client](/help/sites-developing/clientlibs.md)
* [Guida introduttiva di AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [Sviluppo con il sistema di stili](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
