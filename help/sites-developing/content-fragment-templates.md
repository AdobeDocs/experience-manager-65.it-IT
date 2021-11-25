---
title: Modelli per frammenti di contenuto
seo-title: Content Fragment Templates
description: I modelli vengono selezionati al momento della creazione di un frammento di contenuto e forniscono al nuovo frammento la struttura, l’elemento e la variante di base
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: a2b1bd5462ae1837470e31cfeb87a95af1c69be5
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 5%

---

# Modelli per frammenti di contenuto{#content-fragment-templates}

>[!CAUTION]
>
>[Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) sono consigliati per la creazione di tutti i nuovi frammenti di contenuto.
>
>I modelli di frammento di contenuto vengono utilizzati per tutti gli esempi in WKND.

>[!NOTE]
>
>Prima di AEM 6.3, i frammenti di contenuto venivano creati in base a modelli anziché a modelli.
>
>I modelli per frammenti di contenuto sono diventati obsoleti. Possono ancora essere utilizzati per creare frammenti, ma si consiglia invece di utilizzare Modelli per frammenti di contenuto . Non verranno aggiunte nuove funzioni ai modelli di frammento e verranno rimosse in una versione futura.

I modelli vengono selezionati al momento della creazione di un frammento di contenuto. Forniscono al nuovo frammento la struttura di base, gli elementi e la variante. I modelli utilizzati per i frammenti di contenuto sono soggetti a Granite Configuration Manager.

I modelli predefiniti si trovano in:

* `/libs/settings/dam/cfm/templates`

Puoi creare modelli specifici per il sito per frammenti di contenuto in:

* `/apps/settings/dam/cfm/templates`
Posizione per sovrapporre i modelli predefiniti o fornire modelli specifici a livello di applicazione per i clienti che non sono destinati ad essere estesi o modificati in fase di runtime.

* `/conf/global/settings/dam/cfm/templates`
La posizione dei modelli specifici per i clienti a livello di istanza che devono essere modificati in fase di runtime.

L&#39;ordine di precedenza è (in ordine decrescente) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>You ***deve*** non modificare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricrea l&#39;elemento richiesto (ovvero così come esiste in `/libs`) `/apps`
>
>1. Apporta modifiche a `/apps`

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

Maggiori dettagli sui nodi e sulle loro proprietà sono:

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
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>Il titolo del modello (visualizzato nel <strong>Crea frammento</strong> procedura guidata).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> </td>
     <td>Un testo che descrive lo scopo del modello (visualizzato nel <strong>Crea frammento</strong> procedura guidata).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>facoltativo</p> </td>
     <td>Matrice con percorsi alle raccolte che per impostazione predefinita devono essere associate a un frammento di contenuto appena creato.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>required</p> </td>
     <td><p><code>true</code>, se è necessario creare le risorse secondarie che rappresentano gli elementi (eccetto l’elemento principale) del frammento di contenuto al momento della creazione del frammento di contenuto; <em>false</em> se dovrebbero essere creati "al volo".</p> <p><strong>Nota</strong>: al momento questo parametro deve essere impostato su <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>obbligatorio</p> </td>
     <td><p>Versione della struttura del contenuto; attualmente supportato:</p> <p><strong>Nota</strong>: al momento questo parametro deve essere impostato su <code>2</code>.<br /> </p> </td>
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
     <td><p><code>nt:unstructured</code></p> <p>obbligatorio</p> </td>
     <td><p>Nodo che contiene la definizione degli elementi del frammento di contenuto. È obbligatorio e deve contenere almeno un nodo figlio per <strong>Principale</strong> ma può contenere [1.n] nodi figlio.</p> <p>Quando il modello viene utilizzato, il ramo secondario degli elementi viene copiato nel ramo del modello del frammento.</p> <p>Il primo elemento (visualizzato in CRXDE Lite) viene automaticamente considerato come il <i>principale</i> elemento; il nome del nodo è irrilevante e il nodo stesso non ha un significato speciale, a parte il fatto che è rappresentato dalla risorsa principale; gli altri elementi sono gestiti come attività secondarie.</p> </td>
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
     <td>Titolo dell’elemento (visualizzato nel selettore di elementi dell’editor frammento).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: ""</p> </td>
     <td>Contenuto iniziale dell’elemento; solo se utilizzato <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: <code>text/html</code></p> </td>
     <td><p>tipo di contenuto iniziale dell’elemento; solo se utilizzato <code>precreateElements</code><i> = </i><code>true</code>; attualmente supportato:</p>
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
     <td><code>variations</code> </td>
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
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>obbligatorio se è presente un nodo di variante</p> </td>
     <td><p>Definisce una variante iniziale.<br /> Per impostazione predefinita, la variante viene aggiunta a tutti gli elementi del frammento di contenuto.</p> <p>La variante avrà lo stesso contenuto iniziale del rispettivo elemento (vedi <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>obbligatorio</p> </td>
     <td>Il titolo della variante (visualizzato nell’editor frammenti) <strong>Variazione</strong> (barra a sinistra).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>facoltativo</p> <p>impostazione predefinita: ""</p> </td>
     <td>Testo che fornisce una descrizione della variante <span>(visualizzato nell’editor frammenti <strong>Variazione</strong> (barra a sinistra).</code></td>
    </tr>
   </tbody>
  </table>
