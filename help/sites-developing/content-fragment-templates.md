---
title: Modelli per frammenti di contenuto
description: I modelli vengono selezionati durante la creazione di un frammento di contenuto e forniscono al nuovo frammento la struttura, l’elemento e la variante di base
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# Modelli per frammenti di contenuto{#content-fragment-templates}

>[!CAUTION]
>
>[I modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) sono consigliati per la creazione di tutti i nuovi frammenti di contenuto.
>
>I modelli per frammenti di contenuto vengono utilizzati per tutti gli esempi in WKND.

>[!NOTE]
>
>Prima di AEM 6.3, i frammenti di contenuto venivano creati in base a modelli anziché a modelli.
>
>I modelli per frammenti di contenuto sono ora obsoleti. Possono comunque essere utilizzati per la creazione di frammenti, ma si consiglia l’utilizzo di modelli per frammenti di contenuto. Non verranno aggiunte nuove funzioni ai modelli di frammenti e verranno rimosse in una versione futura.

I modelli vengono selezionati durante la creazione di un frammento di contenuto. Forniscono al nuovo frammento la struttura di base, gli elementi e la variante. I modelli utilizzati per i frammenti di contenuto sono soggetti a Granite Configuration Manager.

I modelli predefiniti sono disponibili in:

* `/libs/settings/dam/cfm/templates`

Puoi creare modelli specifici per il sito per i frammenti di contenuto in:

* `/apps/settings/dam/cfm/templates`
Posizione per la sovrapposizione di modelli predefiniti o per la fornitura di modelli specifici per il cliente, validi per l’intera applicazione e non destinati a essere estesi/modificati in fase di esecuzione.

* `/conf/global/settings/dam/cfm/templates`
Posizione dei modelli specifici del cliente a livello di istanza che devono essere modificati in fase di esecuzione.

L&#39;ordine di precedenza è (in ordine decrescente) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>***must*** non modificare nulla nel percorso `/libs`.
>
>Il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricrea l&#39;elemento richiesto (ovvero, poiché esiste in `/libs`) in `/apps`
>
>1. Apporta le modifiche in `/apps`
>

La struttura di base di un modello si trova in:

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

Con la struttura specifica:

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

Ulteriori dettagli sui nodi e sulle relative proprietà sono:

* **Modello**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valore</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Questo nodo è la radice di ciascun modello. È obbligatorio e deve avere un nome univoco.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obbligatorio<br /> </p> </td>
     <td>Titolo del modello visualizzato nella procedura guidata <strong>Crea frammento</strong>.</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> </td>
     <td>Testo che descrive lo scopo del modello (visualizzato nella procedura guidata <strong>Crea frammento</strong>).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>facoltativo</p> </td>
     <td>Array con percorsi di raccolte che devono essere associati a un frammento di contenuto appena creato per impostazione predefinita.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>obbligatorio</p> </td>
     <td><p><code>true</code>, se le risorse secondarie che rappresentano gli elementi (ad eccezione dell’elemento principale) del frammento di contenuto devono essere create al momento della creazione del frammento di contenuto; <em>false</em> se devono essere create "al volo".</p> <p><strong>Nota</strong>: al momento questo parametro deve essere impostato su <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>obbligatorio</p> </td>
     <td><p>Versione della struttura del contenuto; attualmente supportata:</p> <p><strong>Nota</strong>: al momento questo parametro deve essere impostato su <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **Elementi**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valore</th>
    </tr>
    <tr>
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>obbligatorio</p> </td>
     <td><p>Nodo che contiene la definizione degli elementi del frammento di contenuto. È obbligatorio e deve contenere almeno un nodo figlio per l'elemento <strong>Main</strong>, ma può contenere [1..n] nodi secondari.</p> <p>Quando si utilizza il modello, il ramo secondario degli elementi viene copiato nel ramo secondario del modello del frammento.</p> <p>Il primo elemento (come visualizzato in CRXDE Lite) viene automaticamente considerato come l'elemento <i>main</i>; il nome del nodo è irrilevante e il nodo stesso non ha un significato particolare, a parte il fatto che è rappresentato dalla risorsa principale; gli altri elementi vengono gestiti come risorse secondarie.</p> </td>
    </tr>
   </tbody>
  </table>

* **Nome elemento**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valore</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Questo nodo definisce un elemento. È obbligatorio e deve avere un nome univoco.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obbligatorio</p> </td>
     <td>Titolo dell’elemento (visualizzato nel selettore degli elementi dell’editor di frammenti).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: ""</p> </td>
     <td>Contenuto iniziale dell'elemento; utilizzato solo se <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: <code>text/html</code></p> </td>
     <td><p>Tipo di contenuto iniziale dell'elemento; utilizzato solo se <code>precreateElements</code><i> = </i><code>true</code>; attualmente supportato:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>obbligatorio</p> </td>
     <td>Nome interno dell’elemento; deve essere univoco per il tipo di frammento.</td>
    </tr>
   </tbody>
  </table>

* **Varianti**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valore</th>
    </tr>
    <tr>
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>facoltativo</p> </td>
     <td>Questo nodo facoltativo contiene la definizione delle varianti iniziali del frammento di contenuto.</td>
    </tr>
   </tbody>
  </table>

* **Nome variante**

  <table>
   <tbody>
    <tr>
     <th>Nome</th>
     <th>Tipo</th>
     <th>Valore</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>obbligatorio se è presente un nodo di variante</p> </td>
     <td><p>Definisce una variante iniziale.<br /> Per impostazione predefinita, la variante viene aggiunta a tutti gli elementi del frammento di contenuto.</p> <p>La variante avrà lo stesso contenuto iniziale del rispettivo elemento (vedere <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obbligatorio</p> </td>
     <td>Titolo della variante (visualizzato nella scheda <strong>Variante</strong> dell'editor di frammenti (barra a sinistra).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: ""</p> </td>
     <td>Testo che fornisce una descrizione della variante <span> (visualizzata nella scheda <strong>Variante</strong> dell'editor frammenti (barra a sinistra)).</code></td>
    </tr>
   </tbody>
  </table>
