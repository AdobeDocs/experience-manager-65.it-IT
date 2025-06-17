---
title: Modifica di un’applicazione a pagina singola esterna all’interno di Adobe Experience Manager
description: Questo documento descrive i passaggi consigliati per caricare un’applicazione a pagina singola indipendente in un’istanza di Adobe Experience Manager, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.
exl-id: 25236af4-405a-4152-8308-34d983977e9a
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 0%

---


# Modifica di un’applicazione a pagina singola esterna all’interno di Adobe Experience Manager {#editing-external-spa-within-aem}

Quando decidi quale livello di integrazione desideri avere tra l’applicazione a pagina singola esterna e Adobe Experience Manager (AEM), spesso devi essere in grado di modificare e visualizzare l’applicazione a pagina singola in AEM.

{{ue-over-spa}}

## Panoramica {#overview}

Questo documento descrive i passaggi consigliati per caricare un’applicazione a pagina singola indipendente in un’istanza di AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.

## Prerequisiti {#prerequisites}

I prerequisiti sono semplici.

* Assicurati che un’istanza di AEM sia in esecuzione localmente.
* Creare un progetto SPA di base di AEM utilizzando [l&#39;archetipo del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties).
   * Questo costituisce la base del progetto AEM che verrà aggiornato per includere l’applicazione a pagina singola esterna.
   * Gli esempi in questo documento utilizzano il punto di partenza del [progetto SPA WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor).
* Avrai a portata di mano l’applicazione a pagina singola React funzionante ed esterna che desideri integrare.

## Carica applicazione a pagina singola in un progetto AEM {#upload-spa-to-aem-project}

Innanzitutto, devi caricare l’applicazione a pagina singola esterna nel progetto AEM.

1. Sostituisci `src` nella cartella dei progetti `/ui.frontend` con la cartella `src` dell&#39;applicazione React.
1. Includere eventuali dipendenze aggiuntive nel file `/ui.frontend/package.json` dell&#39;app `package.json`.
   * Verificare che le dipendenze di SPA SDK siano di [versioni consigliate](spa-getting-started-react.md#dependencies).
1. Includere eventuali personalizzazioni nella cartella `/public`.
1. Includere eventuali script o stili in linea aggiunti nel file `/public/index.html`.

## Configurare l’applicazione a pagina singola remota {#configure-remote-spa}

Ora che l’applicazione a pagina singola esterna fa parte del progetto AEM, deve essere configurata all’interno di AEM.

### Includi pacchetti SDK SPA di Adobe {#include-spa-sdk-packages}

Per sfruttare le funzioni di AEM SPA, esistono dipendenze dai tre pacchetti seguenti.

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager` fornisce l&#39;API per inizializzare Model Manager e recuperare il modello dall&#39;istanza di AEM. Questo modello può quindi essere utilizzato per eseguire il rendering dei componenti AEM utilizzando le API di `@adobe/aem-react-editable-components` e `@adobe/aem-spa-component-mapping`.

#### Installazione {#installation}

Esegui il seguente comando npm per installare i pacchetti richiesti.

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### Inizializzazione di ModelManager {#model-manager-initialization}

Prima del rendering dell&#39;app, è necessario inizializzare [`ModelManager`](spa-blueprint.md#pagemodelmanager) per gestire la creazione dell&#39;AEM `ModelStore`.

Questa operazione deve essere eseguita all&#39;interno del file `src/index.js` dell&#39;applicazione o ovunque venga eseguito il rendering della radice dell&#39;applicazione.

Per questo, utilizza l&#39;API `initializationAsync` fornita da `ModelManager`.

Nella schermata seguente viene illustrato come abilitare l&#39;inizializzazione di `ModelManager` in una semplice applicazione React. L&#39;unico vincolo è che `initializationAsync` deve essere chiamato prima di `ReactDOM.render()`.

![Inizializza ModelManager](assets/external-spa-initialize-modelmanager.png)

In questo esempio, `ModelManager` è inizializzato e viene creato un `ModelStore` vuoto.

`initializationAsync` può accettare un oggetto `options` come parametro:

* `path` - All&#39;inizializzazione, il modello nel percorso definito viene recuperato e memorizzato in `ModelStore`. Può essere utilizzato per recuperare `rootModel` all&#39;inizializzazione, se necessario.
* `modelClient` - Consente di fornire un client personalizzato responsabile del recupero del modello.
* `model` - Un oggetto `model` passato come parametro viene generalmente popolato quando si utilizza SSR.

### Componenti foglia compatibili con AEM {#authorable-leaf-components}

1. Crea/identifica un componente AEM per il quale verrà creato un componente React personalizzabile. In questo esempio, il progetto WKND utilizza il componente testo.

   ![Componente testo WKND](assets/external-spa-text-component.png)

1. Crea un componente di testo React semplice nell’applicazione a pagina singola. In questo esempio è stato creato un nuovo file `Text.js` con il contenuto seguente.

   ![Testo.js](assets/external-spa-textjs.png)

1. Crea un oggetto di configurazione per specificare gli attributi necessari per abilitare la modifica AEM.

   ![Crea oggetto configurazione](assets/external-spa-config-object.png)

   * `resourceType` è obbligatorio per mappare il componente React al componente AEM e abilitare la modifica quando si apre nell&#39;editor di AEM.

1. Utilizzare la funzione wrapper `withMappable`.

   ![Usa conMappable](assets/external-spa-withmappable.png)

   Questa funzione wrapper mappa il componente React all&#39;AEM `resourceType` specificato nella configurazione e abilita le funzionalità di modifica quando viene aperto nell&#39;editor di AEM. Per i componenti autonomi, recupera anche il contenuto del modello per il nodo specifico.

   >[!NOTE]
   >
   >In questo esempio, esistono versioni separate del componente: componenti AEM racchiusi e non racchiusi (unwrapped) in React. La versione racchiusa deve essere utilizzata quando si utilizza esplicitamente il componente. Quando il componente fa parte di una pagina, puoi continuare a utilizzare il componente predefinito come già fatto nell’editor di applicazioni a pagina singola.

1. Esegui il rendering del contenuto nel componente.

   In AEM, le proprietà JCR del componente testo vengono visualizzate come segue.

   ![Proprietà componente testo](assets/external-spa-text-properties.png)

   Questi valori vengono passati come proprietà al componente React `AEMText` appena creato e possono essere utilizzati per il rendering del contenuto.

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   Questo è il modo in cui il componente viene visualizzato quando le configurazioni di AEM sono completate.

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >In questo esempio, sono state apportate ulteriori personalizzazioni al componente di cui è stato eseguito il rendering, in modo che corrisponda al componente testo esistente. Tuttavia, questo non è correlato all’authoring in AEM.

#### Aggiungere componenti autorizzabili alla pagina {#add-authorable-component-to-page}

Una volta creati, i componenti React possono essere utilizzati in tutta l’applicazione.

Prendiamo una pagina di esempio in cui è necessario aggiungere il testo del progetto SPA WKND. In questo esempio, si desidera visualizzare il testo &quot;Hello World!&quot; il `/content/wknd-spa-react/us/en/home.html`.

1. Determina il percorso del nodo da visualizzare.

   * `pagePath`: la pagina che contiene il nodo, nell&#39;esempio `/content/wknd-spa-react/us/en/home`
   * `itemPath`: percorso del nodo all&#39;interno della pagina, nell&#39;esempio `root/responsivegrid/text`
      * È costituito dai nomi degli elementi che la contengono nella pagina.

   ![Percorso del nodo](assets/external-spa-path.png)

1. Aggiungi il componente nella posizione richiesta nella pagina.

   ![Aggiungi componente alla pagina](assets/external-spa-add-component.png)

   Il componente `AEMText` può essere aggiunto nella posizione richiesta all&#39;interno della pagina con valori `pagePath` e `itemPath` impostati come proprietà. `pagePath` è una proprietà obbligatoria.

#### Verificare la modifica del contenuto di testo su AEM {#verify-text-edit}

Ora testa il componente sull’istanza di AEM in esecuzione.

1. Eseguire il seguente comando Maven dalla directory `aem-guides-wknd-spa` per generare e distribuire il progetto in AEM.

```shell
mvn clean install -PautoInstallSinglePackage
```

1. Nell&#39;istanza di AEM, passa a `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`.

![Modifica dell&#39;applicazione a pagina singola in AEM](assets/external-spa-edit-aem.png)

Il componente `AEMText` è ora modificabile in AEM.

### Pagine AEM Authorable {#aem-authorable-pages}

1. Identifica una pagina da aggiungere per l’authoring nell’applicazione a pagina singola. Questo esempio utilizza `/content/wknd-spa-react/us/en/home.html`.
1. Creare un file (ad esempio, `Page.js`) per il componente Pagina modificabile. In questo caso, è possibile riutilizzare il componente Pagina fornito in `@adobe/cq-react-editable-components`.
1. Ripeti il passaggio quattro nella sezione [Componenti foglia modificabili da AEM](#authorable-leaf-components). Utilizzare la funzione wrapper `withMappable` sul componente.
1. Come già fatto in precedenza, applica `MapTo` ai tipi di risorse AEM per tutti i componenti secondari all&#39;interno della pagina.

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >In questo esempio, viene utilizzato il componente testo React decompresso al posto di `AEMText` creato in precedenza. Questo perché quando il componente fa parte di una pagina o di un contenitore e non è autonomo, il contenitore si occupa della mappatura ricorsiva del componente e dell’abilitazione delle funzionalità di authoring e il wrapper aggiuntivo non è necessario per ogni elemento secondario.

1. Per aggiungere una pagina modificabile nell&#39;applicazione a pagina singola, seguire gli stessi passaggi della sezione [Aggiungere componenti modificabili alla pagina](#add-authorable-component-to-page). In questo caso, tuttavia, è possibile ignorare la proprietà `itemPath`.

#### Verificare il contenuto della pagina in AEM {#verify-page-content}

Per verificare che la pagina possa essere modificata, seguire gli stessi passaggi della sezione [Verifica modifica del contenuto di testo in AEM](#verify-text-edit).

![Modifica di una pagina in AEM](assets/external-spa-edit-page.png)

La pagina è ora modificabile in AEM con un contenitore di layout e un componente testo figlio.

### Componenti foglia virtuale {#virtual-leaf-components}

Negli esempi precedenti, abbiamo aggiunto componenti all’applicazione a pagina singola con contenuto AEM esistente. Tuttavia, in alcuni casi il contenuto non è ancora stato creato in AEM, ma deve essere aggiunto successivamente dall’autore del contenuto. Per soddisfare questa esigenza, lo sviluppatore front-end può aggiungere componenti nelle posizioni appropriate all’interno dell’applicazione a pagina singola. Questi componenti visualizzano i segnaposto quando vengono aperti nell’editor in AEM. Una volta che il contenuto viene aggiunto all’interno di questi segnaposto dall’autore del contenuto, i nodi vengono creati nella struttura JCR e il contenuto viene mantenuto. Il componente creato consente di eseguire le stesse operazioni dei componenti foglia autonomi.

In questo esempio viene riutilizzato il componente `AEMText` creato in precedenza. Desideriamo che venga aggiunto nuovo testo sotto il componente testo esistente nella home page di WKND. L’aggiunta dei componenti è la stessa dei normali componenti foglia. Tuttavia, `itemPath` può essere aggiornato al percorso in cui è necessario aggiungere il nuovo componente.

Poiché è necessario aggiungere il nuovo componente sotto il testo esistente in `root/responsivegrid/text`, il nuovo percorso sarà `root/responsivegrid/{itemName}`.

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

Dopo l&#39;aggiunta del componente virtuale, il componente `TestPage` si presenta come segue.

![Verifica del componente virtuale](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>Assicurarsi che il componente `AEMText` abbia impostato `resourceType` nella configurazione per abilitare questa funzione.

È ora possibile distribuire le modifiche ad AEM seguendo i passaggi descritti nella sezione [Verifica modifica del contenuto di testo in AEM](#verify-text-edit). Viene visualizzato un segnaposto per il nodo `text_20` attualmente non esistente.

![Nodo text_20 in aem](assets/external-spa-text20-aem.png)

Quando l&#39;autore di contenuto aggiorna questo componente, viene creato un nuovo nodo `text_20` in `root/responsivegrid/text_20` in `/content/wknd-spa-react/us/en/home`.

![Nodo text20](assets/external-spa-text20-node.png)

#### Requisiti e limitazioni {#limitations}

Esistono diversi requisiti per aggiungere componenti foglia virtuali e alcune limitazioni.

* La proprietà `pagePath` è obbligatoria per creare un componente virtuale.
* Il nodo di pagina fornito nel percorso in `pagePath` deve esistere nel progetto AEM.
* Il nome del nodo da creare deve essere specificato in `itemPath`.
* Il componente può essere creato a qualsiasi livello.
   * Se si specifica `itemPath='text_20'` nell&#39;esempio precedente, il nuovo nodo verrà creato direttamente sotto la pagina, ovvero `/content/wknd-spa-react/us/en/home/jcr:content/text_20`
* Il percorso del nodo in cui viene creato un nuovo nodo deve essere valido quando fornito tramite `itemPath`.
   * In questo esempio, `root/responsivegrid` deve esistere in modo che il nuovo nodo `text_20` possa essere creato lì.
* È supportata solo la creazione di componenti foglia. Contenitore virtuale e pagina saranno supportati nelle versioni future.

### Contenitori virtuali {#virtual-containers}

È supportata la possibilità di aggiungere contenitori, anche se il contenitore corrispondente non è ancora stato creato in AEM. Il concetto e l&#39;approccio sono simili a [componenti foglia virtuali.](#virtual-leaf-components)

Lo sviluppatore front-end può aggiungere i componenti contenitore nelle posizioni appropriate all’interno dell’applicazione a pagina singola e tali componenti visualizzeranno dei segnaposto quando vengono aperti nell’editor in AEM. L’autore può quindi aggiungere componenti e il relativo contenuto al contenitore, che creerà i nodi richiesti nella struttura JCR.

Ad esempio, se in `/root/responsivegrid` esiste già un contenitore e lo sviluppatore desidera aggiungere un nuovo contenitore secondario:

![Percorso contenitore](assets/container-location.png)

`newContainer` non esiste ancora in AEM.

Durante la modifica della pagina che contiene questo componente in AEM, viene visualizzato un segnaposto vuoto per un contenitore in cui l’autore può aggiungere contenuti.

![Segnaposto contenitore](assets/container-placeholder.png)

![Percorso contenitore in JCR](assets/container-jcr-structure.png)

Una volta che l’autore aggiunge un componente secondario al contenitore, il nuovo nodo del contenitore viene creato con il nome corrispondente nella struttura JCR.

![Contenitore con contenuto](assets/container-with-content.png)

![Contenitore con contenuto in JCR](assets/container-with-content-jcr.png)

È ora possibile aggiungere al contenitore altri componenti e contenuti necessari all’autore e le modifiche verranno mantenute.

#### Requisiti e limitazioni {#container-limitations}

Esistono diversi requisiti per aggiungere contenitori virtuali e alcune limitazioni.

* Il criterio per determinare quali componenti possono essere aggiunti verrà ereditato dal contenitore principale.
* L’elemento principale immediato del contenitore da creare deve già esistere in AEM.
   * Se il contenitore `root/responsivegrid` esiste già nel contenitore AEM, è possibile creare un nuovo contenitore fornendo il percorso `root/responsivegrid/newContainer`.
   * Tuttavia `root/responsivegrid/newContainer/secondNewContainer` non è possibile.
* È possibile creare un solo nuovo livello di componente alla volta.

## Personalizzazioni aggiuntive {#additional-customizations}

Se hai seguito gli esempi precedenti, l’applicazione a pagina singola esterna ora è modificabile in AEM. Tuttavia, puoi personalizzare ulteriormente alcuni aspetti aggiuntivi dell’applicazione a pagina singola esterna.

### ID nodo principale {#root-node-id}

Per impostazione predefinita, si presuppone che l&#39;applicazione React sia rappresentata all&#39;interno di un `div` di ID elemento `spa-root`. Se necessario, questo può essere personalizzato.

Ad esempio, si supponga di disporre di un&#39;applicazione a pagina singola in cui l&#39;applicazione viene rappresentata all&#39;interno di un `div` di ID elemento `root`. Questo deve essere riflesso in tre file.

1. In `index.js` dell&#39;applicazione React (o dove viene chiamato `ReactDOM.render()`)

   ![ReactDOM.render() nel file index.js](assets/external-spa-root-index.png)

1. In `index.html` dell&#39;applicazione React

   ![Index.html dell&#39;applicazione](assets/external-spa-index.png)

1. Nel corpo del componente Pagina dell’app AEM, segui questi due passaggi:

   1. Crea un `body.html` per il componente pagina.

   ![Crea un file body.html](assets/external-spa-update-body.gif)

   1. Aggiungere il nuovo elemento radice nel nuovo file `body.html`.

   ![Aggiungi l&#39;elemento radice a body.html](assets/external-spa-add-root.png)

### Modifica di un’applicazione a pagina singola React con routing {#editing-react-spa-with-routing}

Se l&#39;applicazione SPA React esterna ha più pagine, [può usare il routing per determinare la pagina/componente da riprodurre](spa-routing.md). Il caso d’uso di base prevede che l’URL attualmente attivo corrisponda al percorso fornito per una route. Per abilitare la modifica nelle applicazioni abilitate per l’instradamento, il percorso da confrontare deve essere trasformato per adattarsi alle informazioni specifiche di AEM.

Nell’esempio seguente abbiamo una semplice applicazione React con due pagine. La pagina di cui eseguire il rendering viene determinata confrontando il percorso fornito al router con l’URL attivo. Ad esempio, se ci troviamo su `mydomain.com/test`, verrà eseguito il rendering di `TestPage`.

![Indirizzamento in un&#39;applicazione a pagina singola esterna](assets/external-spa-routing.png)

Per abilitare la modifica in AEM per questa applicazione a pagina singola di esempio, sono necessari i seguenti passaggi.

1. Identifica il livello che fungerebbe da root su AEM.

   * Per il nostro esempio, consideriamo `wknd-spa-react/us/en` come radice dell&#39;applicazione a pagina singola. Ciò significa che tutto ciò che precede quel percorso è costituito solo da pagine/contenuti AEM.

1. Crea una pagina al livello richiesto.

   * In questo esempio, la pagina da modificare è `mydomain.com/test`. `test` è nel percorso principale dell&#39;app. Questo deve essere mantenuto anche durante la creazione della pagina in AEM. Pertanto, puoi creare una pagina al livello principale definito nel passaggio precedente.
   * La nuova pagina creata deve avere lo stesso nome della pagina da modificare. In questo esempio per `mydomain.com/test`, la nuova pagina creata deve essere `/path/to/aem/root/test`.

1. Aggiungi helper all’interno del routing SPA.

   * La pagina appena creata non eseguirà ancora il rendering del contenuto previsto in AEM. Il router prevede un percorso di `/test`, mentre il percorso attivo di AEM è `/wknd-spa-react/us/en/test`. Per includere la porzione dell’URL specifica per AEM, è necessario aggiungere alcuni helper sul lato SPA.

   ![Helper di routing](assets/external-spa-router-helper.png)

   * È possibile utilizzare l&#39;helper `toAEMPath` fornito da `@adobe/cq-spa-page-model-manager`. Trasforma il percorso fornito per il routing in modo da includere parti specifiche di AEM quando l’applicazione è aperta su un’istanza di AEM. Accetta tre parametri:
      * Percorso necessario per il routing
      * URL di origine dell’istanza di AEM in cui viene modificata l’applicazione a pagina singola
      * Directory principale del progetto su AEM come determinato nel primo passaggio

   * Questi valori possono essere impostati come variabili di ambiente per maggiore flessibilità.

1. Verifica la modifica della pagina in AEM.

   * Distribuire il progetto in AEM e passare alla pagina `test` appena creata. Ora è stato eseguito il rendering del contenuto della pagina e i componenti AEM sono modificabili.

## Limitazioni del framework {#framework-limitations}

Il componente RemotePage prevede che l&#39;implementazione fornisca un manifesto delle risorse come [webpack-manifest-plugin su GitHub](https://github.com/shellscape/webpack-manifest-plugin). Il componente RemotePage, tuttavia, è stato testato per funzionare solo con il framework React (e Next.js tramite il componente remote-page-next ) e pertanto non supporta il caricamento remoto di applicazioni da altri framework, come Angular.

## Risorse aggiuntive {#additional-resources}

Il seguente materiale di riferimento può essere utile per comprendere le applicazioni a pagina singola nel contesto di AEM.

* [Archetipo Progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)
* [Progetto SPA WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=it)
* [Guida introduttiva alle applicazioni a pagina singola in AEM con React](spa-getting-started-react.md)
* [Materiali di riferimento SPA (riferimenti API)](spa-reference-materials.md)
* [Blueprint SPA e PageModelManager](spa-blueprint.md#pagemodelmanager)
* [Routing modello SPA](spa-routing.md)
