---
title: Componenti compositi negli SPA
description: Scopri come creare componenti compositi personalizzati, componenti composti da altri componenti che funzionano con l’editor di applicazioni a pagina singola AEM (SPA).
exl-id: 02b6c698-d169-467a-9168-9fa6181bed6c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Componenti compositi negli SPA {#composite-components-in-spas}

I componenti compositi sfruttano la natura modulare dei componenti AEM combinando più componenti di base in un unico componente. Un caso d’uso comune di un componente composito è il componente a schede, composto da una combinazione di componenti immagine e testo.

Quando i componenti compositi vengono implementati correttamente nel framework dell’editor per applicazioni a pagina singola AEM (SPA), gli autori di contenuti possono trascinare e rilasciare tali componenti come qualsiasi altro componente, ma possono comunque modificare singolarmente ogni componente che costituisce il componente composito.

Questo articolo illustra come aggiungere un componente composito all’applicazione a pagina singola per lavorare senza problemi con l’editor di SPA AEM.

## Caso d’uso  {#use-case}

Questo articolo utilizza il tipico componente per schede come esempio di utilizzo. Le schede sono un elemento comune dell&#39;interfaccia utente per molte esperienze digitali e sono in genere costituite da un&#39;immagine e da un testo o una didascalia associati. Un autore desidera poter trascinare e rilasciare l&#39;intera scheda, ma può modificare singolarmente l&#39;immagine della scheda e personalizzare il testo associato.

## Prerequisiti {#prerequisites}

I seguenti modelli per supportare i casi di utilizzo dei componenti compositi richiedono i seguenti prerequisiti.

* L’istanza di sviluppo AEM viene eseguita localmente sulla porta 4502 con un progetto di esempio.
* Hai un’app React esterna funzionante [abilitato per la modifica in AEM.](spa-edit-external.md)
* L’app React viene caricata nell’editor AEM [mediante il componente RemotePage.](spa-remote-page.md)

## Aggiunta di componenti compositi a un SPA {#adding-composite-components}

Sono disponibili tre modelli diversi per l’implementazione del componente composito, a seconda dell’implementazione SPA in AEM.

* [Il componente non esiste nel progetto AEM.](#component-does-not-exist)
* [Il componente esiste nel progetto AEM, ma il contenuto richiesto non lo è.](#content-does-not-exist)
* [Il componente e il contenuto richiesto esistono entrambi nel progetto AEM.](#both-exist)

Le sezioni seguenti forniscono esempi di implementazione di ogni caso utilizzando come esempio il componente scheda .

### Il componente non esiste nel progetto AEM. {#component-does-not-exist}

Inizia creando i componenti che compongono il componente composito, ovvero i componenti per l’immagine e il relativo testo.

1. Crea il componente testo nel progetto AEM.
1. Aggiungi il corrispondente `resourceType` dal progetto nel componente `editConfig` nodo.

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. Utilizza la `withMappable` per abilitare la modifica del componente.

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

Il componente Testo sarà simile al seguente.

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

Se crei un componente immagine in modo simile, puoi combinarlo con il `AEMText` componente in un nuovo componente scheda, utilizzando i componenti immagine e testo come elementi secondari.

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

Questo componente composito risultante può ora essere posizionato in qualsiasi punto dell’app e aggiungerà segnaposto per un testo e un componente immagine nell’Editor di SPA. Nell’esempio seguente, il componente scheda viene aggiunto al componente principale sotto il titolo.

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

Verrà visualizzato un segnaposto vuoto per un testo e un’immagine nell’editor. Quando inserisci i valori per questi tramite l’editor, vengono memorizzati nel percorso di pagina specificato, ovvero `/content/wknd-spa/home`  al livello principale con i nomi specificati in `itemPath`.

![Componente scheda composita nell’editor](assets/composite-card.png)

### Il componente esiste nel progetto AEM, ma il contenuto richiesto non lo è. {#content-does-not-exist}

In questo caso, il componente scheda è già creato nel progetto AEM contenente nodi titolo e immagine. I nodi secondari (testo e immagine) hanno i tipi di risorse corrispondenti.

![Struttura del nodo del componente scheda](assets/composite-node-structure.png)

Puoi quindi aggiungerlo al tuo SPA e recuperarne il contenuto.

1. Crea un componente corrispondente nel SPA per questo. Assicurati che i componenti figlio siano mappati ai tipi di risorse AEM corrispondenti all’interno del progetto SPA. In questo esempio utilizziamo lo stesso `AEMText` e `AEMImage` componenti descritti in dettaglio [nel caso precedente.](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. Poiché non è presente alcun contenuto per il `imagecard` , aggiungi la scheda alla pagina. Includi il contenitore esistente da AEM nel SPA.
   * Se nel progetto AEM è già presente un contenitore, è possibile includerlo nel SPA e aggiungere invece il componente al contenitore da AEM.
   * Assicurati che il componente scheda sia mappato al tipo di risorsa corrispondente nel SPA.

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. Aggiungi il `wknd-spa/components/imagecard` ai componenti consentiti per il componente contenitore [nel modello di pagina.](/help/sites-authoring/templates.md)

Ora il `imagecard` può essere aggiunto direttamente al contenitore nell’editor di AEM.

![Scheda composita nell&#39;editor](assets/composite-card.gif)

### Il componente e il contenuto richiesto esistono entrambi nel progetto AEM. {#both-exist}

Se il contenuto esiste in AEM, può essere incluso direttamente nel SPA fornendo il percorso del contenuto.

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![Percorso composito nella struttura del nodo](assets/composite-path.png)

La `AEMCard` è lo stesso del componente definito [nel caso d’uso precedente.](#content-does-not-exist) In questo caso il contenuto definito nella posizione precedente nel progetto AEM è incluso nel SPA.
