---
title: Modelli di frammento di contenuto
seo-title: Modelli di frammento di contenuto
description: Quando si crea un frammento di contenuto, i modelli vengono selezionati e forniscono al nuovo frammento struttura, elemento e variante di base
seo-description: Quando si crea un frammento di contenuto, i modelli vengono selezionati e forniscono al nuovo frammento struttura, elemento e variante di base
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 5%

---


# Modelli di frammento di contenuto{#content-fragment-templates}

>[!CAUTION]
>
>[Per la creazione di tutti i frammenti è ora consigliabile utilizzare ](/help/assets/content-fragments/content-fragments-models.md) i modelli di frammento di contenuto.
>
>I modelli di frammento di contenuto vengono utilizzati per tutti gli esempi in We.Retail.

I modelli vengono selezionati al momento della creazione di un frammento di contenuto. Forniscono al nuovo frammento la struttura di base, gli elementi e la variante. I modelli utilizzati per i frammenti di contenuto sono soggetti a Granite Configuration Manager.

I modelli predefiniti sono disponibili in:

* `/libs/settings/dam/cfm/templates`

È possibile creare modelli specifici per il sito per i frammenti di contenuto in:

* `/apps/settings/dam/cfm/templates`
Posizione per sovrapporre i modelli out-of-the-box o fornire modelli specifici per i clienti a livello di applicazione che non devono essere estesi o modificati in fase di esecuzione.

* `/conf/global/settings/dam/cfm/templates`
Il percorso per i modelli specifici per i clienti dell&#39;istanza che devono essere modificati in fase di esecuzione.

L&#39;ordine di precedenza è (in ordine decrescente) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>***non è necessario*** modificare nulla nel percorso `/libs`.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
   >
   >
1. Apportare modifiche all&#39;interno di `/apps`

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

La struttura specifica è:

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

Ulteriori dettagli sui nodi e le relative proprietà sono:

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
     <td>Questo nodo è il nodo principale per ciascun modello. È obbligatorio e deve avere un nome univoco.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>Titolo del modello (visualizzato nella procedura guidata <strong>Crea frammento</strong>).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> </td>
     <td>Testo che descrive lo scopo del modello (visualizzato nella procedura guidata <strong>Crea frammento</strong>).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>facoltativo</p> </td>
     <td>Un array con percorsi alle raccolte che per impostazione predefinita dovrebbero essere associate a un frammento di contenuto appena creato.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, se le risorse secondarie che rappresentano gli elementi (tranne l'elemento principale) del frammento di contenuto devono essere create al momento della creazione del frammento di contenuto; <em>false</em> se devono essere create "al volo".</p> <p><strong>Nota</strong>: al momento questo parametro deve essere impostato su  <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>mandatory</p> </td>
     <td><p>Versione della struttura del contenuto; attualmente supportato:</p> <p><strong>Nota</strong>: al momento questo parametro deve essere impostato su  <code>2</code>.<br /> </p> </td>
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
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>mandatory</p> </td>
     <td><p>Nodo che contiene la definizione degli elementi del frammento di contenuto. È obbligatorio e deve contenere almeno un nodo secondario per l'elemento <strong>Main</strong>, ma può contenere [1.n] nodi secondari.</p> <p>Quando il modello viene utilizzato, il ramo secondario degli elementi viene copiato nel ramo del modello del frammento.</p> <p>Il primo elemento (visualizzato in CRXDE Lite) viene automaticamente considerato l'elemento <i>main</i>; il nome del nodo è irrilevante e il nodo stesso non ha una rilevanza particolare, a parte il fatto che è rappresentato dalla risorsa principale; gli altri elementi sono gestiti come risorse secondarie.</p> </td>
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
     <td><p><code>String</code></p> <p>mandatory</p> </td>
     <td>Titolo dell’elemento (visualizzato nel selettore di elementi dell’editor di frammenti).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: ""</p> </td>
     <td>Contenuto iniziale dell’elemento; utilizzato solo se <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: <code>text/html</code></p> </td>
     <td><p>Tipo di contenuto iniziale dell’elemento; utilizzato solo se <code>precreateElements</code><i> = </i><code>true</code>; attualmente supportato:</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>mandatory</p> </td>
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
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>facoltativo</p> </td>
     <td>Questo nodo facoltativo contiene la definizione delle variazioni iniziali del frammento di contenuto.</td>
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
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>obbligatorio se è presente un nodo di variante</p> </td>
     <td><p>Definisce una variante iniziale.<br /> Per impostazione predefinita, la variante viene aggiunta a tutti gli elementi del frammento di contenuto.</p> <p>La variante avrà lo stesso contenuto iniziale del rispettivo elemento (vedere <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>mandatory</p> </td>
     <td>Titolo della variante (visualizzata nella scheda <strong>Variation</strong> dell'editor frammenti (barra a sinistra)).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: ""</p> </td>
     <td>Testo che fornisce una descrizione della variante <span> (visualizzata nella scheda <strong>Variation</strong> dell'editor frammento).</code></td>
    </tr>
   </tbody>
  </table>
