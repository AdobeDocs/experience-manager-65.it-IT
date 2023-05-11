---
title: Configura l’editor Rich Text per creare contenuti in Adobe Experience Manager.
description: Scopri come configurare l’editor Rich Text di Adobe Experience Manager per creare contenuti in Adobe Experience Manager.
contentOwner: AG
exl-id: 2e7ec22f-0856-44c4-bb15-1086dae0b85a
source-git-commit: 53a18ec48331f1c25c15e8f7a59bd57e95639895
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 1%

---

# Configurare l’editor Rich Text {#configure-the-rich-text-editor}

L’editor Rich Text offre agli autori numerose funzionalità per modificare il contenuto del testo. Icone, caselle di selezione, barra degli strumenti e menu sono disponibili per un’esperienza di modifica del testo WYSIWYG.

Per informazioni su come utilizzare le funzioni dell’editor Rich Text per l’authoring, consulta [Utilizza l’editor Rich Text per l’authoring](/help/sites-authoring/rich-text-editor.md). L’editor Rich Text può essere configurato per abilitare, disabilitare ed estendere le funzioni disponibili nei componenti di authoring. Il flusso di lavoro seguente illustra un ordine consigliato per il completamento delle attività di configurazione dell’editor Rich Text in Experience Manager.

![Sequenza di passaggi per imparare a configurare l’editor Rich Text](assets/rte_workflow_v1.png)

*Figura: Sequenza di passaggi per imparare a configurare l’editor Rich Text*

## Comprendere l’interfaccia touch e l’interfaccia classica {#understand-touch-enabled-ui-and-classic-ui}

L’interfaccia touch è ad Experience Manager l’interfaccia utente standard. Adobe di interfaccia utente touch con [design dinamico](/help/sites-authoring/responsive-layout.md) per ambiente di authoring. L’interfaccia touch è progettata per i dispositivi touch e desktop. L’interfaccia è molto diversa dall’interfaccia classica originale.

![Barra degli strumenti dell’Editor Rich Text nell’interfaccia Touch](assets/chlimage_1-35.png)

*Figura: Barra degli strumenti dell’Editor Rich Text nell’interfaccia touch*

![Barra degli strumenti dell’Editor Rich Text nell’interfaccia classica](assets/rtedefault.png)

*Figura: Barra degli strumenti dell’Editor Rich Text nell’interfaccia classica*

>[!MORELIKETHIS]
>
>* [Raccomandazioni per l&#39;interfaccia utente](/help/sites-deploying/ui-recommendations.md)
>* Informazioni sulla deprecazione dell’interfaccia classica, consulta [Note sulla versione di Experience Manager 6.5](/help/release-notes/deprecated-removed-features.md)
>* Per informazioni sulle differenze tra le interfacce, consulta [Interfaccia touch e interfaccia classica](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* Per comprendere in dettaglio l’interfaccia touch, vedi [Concetti di interfaccia utente touch Experience Manager](/help/sites-developing/touch-ui-concepts.md)


## Varie modalità di editing {#editingmodes}

Gli autori possono creare e modificare contenuti di testo in Experience Manager utilizzando le diverse modalità dei componenti. Le opzioni della barra degli strumenti per l’authoring e la formattazione dei contenuti e l’esperienza utente dei componenti abilitati per l’editor Rich Text in diverse modalità di modifica variano a seconda delle configurazioni dell’editor Rich Text.

| Modalità di modifica | Area di editing | Funzioni consigliate da abilitare | Interfaccia utente touch | Interfaccia classica |
|--- |--- |--- |--- |--- |
| In linea | Modifica diretta per modifiche rapide e minori; Formato senza aprire una finestra di dialogo | Funzioni RTE minime | Y | Y |
| Schermo intero dell’Editor Rich Text | Copertura di tutta la pagina | Tutte le funzioni RTE richieste | Y | N |
| Finestra di dialogo | Finestra di dialogo sul contenuto della pagina, ma non copre l’intera pagina | Tutte le funzioni RTE richieste nell’interfaccia classica; Abilitare in modo giudizioso le funzioni nell&#39;interfaccia utente touch | Y | Y |
| Finestra di dialogo a schermo intero | Come per la modalità a schermo intero; contiene i campi della finestra di dialogo accanto all’editor Rich Text | Tutte le funzioni RTE richieste | Y | N |

>[!NOTE]
>
>La funzione di modifica sorgente non è disponibile in modalità di modifica in linea nell’interfaccia touch. Non è possibile trascinare immagini in modalità a schermo intero. Tutte le altre funzioni funzionano in tutte le modalità.

### Modifica in linea {#inline-editing}

Quando il contenuto viene aperto (con un doppio tocco o clic lento), è possibile modificarlo all’interno della pagina. Viene presentata una barra degli strumenti compatta con opzioni molto semplici.

![Modifica in linea con la barra degli strumenti di base nell’interfaccia touch](assets/chlimage_1-36.png)

*Figura: Modifica in linea con la barra degli strumenti di base nell’interfaccia touch*

Nell’interfaccia classica, un doppio clic lento sul componente consente la modifica in linea e una struttura arancione evidenzia il contenuto. Se Content Finder è aperto, nella parte superiore della finestra viene visualizzata una barra degli strumenti con le opzioni di formattazione dell’editor Rich Text disponibili. Se Content Finder non è aperto, le opzioni di formattazione non vengono visualizzate ed è possibile eseguire solo modifiche di testo di base.

### Modifica a tutto schermo {#full-screen-editing}

I componenti di Experience Manager possono essere aperti nella visualizzazione a schermo intero che nasconde il contenuto della pagina e occupa la schermata disponibile. Considera la modifica a schermo intero una versione dettagliata della modifica in linea in quanto offre il maggior numero di opzioni di modifica. Può essere aperto facendo clic su ![rte_fullscreen](assets/rte_fullscreen.png), dalla barra degli strumenti compatta quando si utilizza la modalità di editing in linea.

Nella finestra di dialogo a schermo intero, insieme a una barra degli strumenti dettagliata dell’Editor Rich Text, sono disponibili anche le opzioni e i componenti disponibili in una finestra di dialogo. È applicabile solo per una finestra di dialogo che contiene l’editor Rich Text e altri componenti.

![Barra degli strumenti dettagliata dell’editor Rich Text durante la modifica in modalità a schermo intero nell’interfaccia touch](assets/chlimage_1-37.png)

*Figura: Barra degli strumenti dettagliata dell’editor Rich Text durante la modifica in modalità a schermo intero nell’interfaccia touch*

### Modifica finestra di dialogo {#dialog-editing}

Quando si fa doppio clic su un componente, viene visualizzata una finestra di dialogo per la modifica del contenuto. Viene visualizzata la finestra di dialogo sopra la pagina esistente. In alcuni scenari specifici, la finestra di dialogo si apre come finestra a comparsa. Ad esempio, quando un componente Testo fa parte di una colonna in un layout di pagina a più colonne e l’area disponibile per la finestra di dialogo è inferiore.

![Modalità di modifica delle finestre di dialogo nell’interfaccia touch](assets/dialog_editing_modetouchui.png)

*Figura: Modalità di modifica delle finestre di dialogo nell’interfaccia touch*

![Finestra di dialogo nell’interfaccia classica che contiene una barra degli strumenti dettagliata per la modifica](assets/chlimage_1-38.png)

*Figura: Finestra di dialogo nell’interfaccia classica che contiene una barra degli strumenti dettagliata per la modifica*

## Informazioni sui plug-in RTE e sulle funzioni associate {#aboutplugins}

La funzionalità è resa disponibile tramite una serie di plug-in, ciascuno con:

* A `features` proprietà:

   * Utilizzato per attivare o disattivare le funzionalità di base del plug-in
   * Può essere configurato utilizzando una procedura standard

* Se del caso, ulteriori proprietà e opzioni che richiedono una configurazione specifica.

Le funzioni di base dell’editor Rich Text vengono attivate o disattivate dal valore `features` su un nodo specifico del plug-in appropriato.

Nella tabella seguente sono elencati i plug-in correnti, che mostrano:

* ID dei plug-in con un collegamento alla documentazione API. L&#39;ID viene utilizzato come nome del nodo quando [attivazione di un plug-in](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valori consentiti per `features` proprietà.
* Una descrizione delle funzionalità fornite dal plug-in.

| ID plug-in | caratteristiche | Descrizione |
|--- |--- |--- |
| modifica | taglia copia incolla-default-paste-plintext paste-wordhtml | [Taglia, copia e incolla le tre modalità](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| punto di arrivo | trova sostituzione | Trova e sostituisci. |
| format | sottolineato in corsivo grassetto | [Formattazione testo di base](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| immagine | immagine | Supporto immagini di base (trascinamento da contenuto o Content Finder). A seconda del browser, il supporto offre diversi comportamenti per gli autori |
| chiavi |  | Per definire questo valore, vedi [dimensione della scheda](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| giustificare | justifyleft justifycenter copyright | Allineamento paragrafo. |
| collegamenti | ancoraggio di scollegamento modifica collegamento | [Collegamenti ipertestuali e ancoraggi](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| elenchi | rientro fuori linea ordinato | Questo plug-in controlla entrambi [rientri ed elenchi](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin); inclusi gli elenchi nidificati. |
| strumenti cattivi | specialchars sourceedit | Gli strumenti vari consentono agli autori di accedere [caratteri speciali](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) o modificare l&#39;origine di HTML. Inoltre, puoi aggiungere un intero [intervallo di caratteri speciali](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) per definire un proprio elenco. |
| Paraformato | paraformato | I formati di paragrafo predefiniti sono Paragrafo, Intestazione 1, Intestazione 2 e Intestazione 3 (`<p>`, `<h1>`, `<h2>`e `<h3>`). È possibile [aggiungere altri formati paragrafo](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) o estendere l’elenco. |
| controllo ortografico | spunta | [Controllo ortografico basato sulla lingua](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| stili | stili | Supporto per lo stile utilizzando una classe CSS. [Aggiungi nuovi stili di testo](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) per aggiungere (o estendere) un proprio intervallo di stili da utilizzare con il testo. |
| pedice | pedice | Estensioni ai formati di base, aggiunta di script secondari e super. |
| tabella | insertrow removerow insertcolumn removecolumn cellprop mergecells splitcell selectrow selectcolumns | Vedi [configurare gli stili di tabella](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles), se si desidera aggiungere stili personalizzati per tabelle intere o celle singole. |
| annulla | annulla ripristino | Dimensione della cronologia [annullare e ripristinare](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) operazioni. |

>[!NOTE]
>
>Il plug-in a schermo intero non è supportato in modalità finestra di dialogo. Uso del `dialogFullScreen` impostazione per configurare la barra degli strumenti per la modalità a schermo intero.

## Comprendere i percorsi e le posizioni di configurazione {#understand-the-configuration-paths-and-locations}

La [modalità di modifica dell’editor Rich Text (e dell’interfaccia utente)](#editingmodes) che vengono forniti agli autori e che determinano la posizione dei dettagli di configurazione quando [attivazione dei plug-in RTE](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin):

| Modalità di modifica | Posizione per l’interfaccia utente touch | Posizione per l’interfaccia classica |
|---|---|---|
| In linea | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| Schermo intero | `cq:editConfig/cq:inplaceEditing` | Non applicabile |
| Finestra di dialogo | `cq:dialog` | `dialog` |
| Finestra di dialogo a schermo intero | `cq:dialog` | Non applicabile |

>[!NOTE]
>
>Non denominare il nodo sotto `cq:inplaceEditing` come `config`. On `cq:inplaceEditing` , definire le seguenti proprietà:
>* **Nome**: `configPath`
>* **Tipo**: `String`
>* **Valore**: percorso del nodo contenente la configurazione effettiva
>
>Non denominare il nodo di configurazione dell’editor Rich Text come `config`. In caso contrario, le configurazioni dell’editor Rich Text hanno effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

Configura le seguenti proprietà che si applicano nella modalità di modifica della finestra di dialogo solo nell’interfaccia utente touch:

* `useFixedInlineToolbar`: Imposta questa proprietà booleana definita sul nodo RTE (una con sling:resourceType= `cq/gui/components/authoring/dialog/richtext`) a `True`, per correggere la barra degli strumenti dell’Editor Rich Text anziché fluttuare.

   Quando questa proprietà è true, per impostazione predefinita la modifica Richtext viene avviata sull&#39;evento &quot;foundation-contentloaded&quot;.

   Per evitare questo problema, impostare la proprietà `customStart` a `True`e attiva l’evento &quot;rte-start&quot; per avviare la modifica dell’editor Rich Text. Quando questa proprietà è &quot;true&quot;, il comportamento predefinito, rte start on click, non funziona.

* `customStart`: Imposta questa proprietà booleana definita sul nodo dell’editor Rich Text su `True`, per controllare quando avviare l’editor Rich Text attivando l’evento `rte-start`.

* `rte-start`: Attiva questo evento nella `contenteditable-div` dell’editor Rich Text, quando iniziare a modificare l’editor Rich Text. Questo funziona solo se `customStart` è stato impostato su true.

Quando l’editor Rich Text viene utilizzato nella finestra di dialogo touch, impostare la proprietà `useFixedInlineToolbar` su true è obbligatorio per evitare problemi.

## Personalizzazione della modifica diretta {#customizing-in-place-editing}

Per definire quale selettore HTML avvia l’editor di testo, configura le seguenti proprietà:

* **`editElementQuery`** - Definito in `cq:InplaceEditingConfig`, questa proprietà viene utilizzata per specificare un selettore dell’elemento HTML in cui verrà avviata la modifica in linea per il componente testo. Se non viene specificato, la modifica in linea viene avviata direttamente sul HTML Text Component (Componente testo).
* **`textPropertyName`** - Definito in `cq:InplaceEditingConfig`, questa proprietà viene utilizzata per specificare il nome della proprietà che verrà salvata sul nodo del contenuto in cui il valore HTML del componente di testo verrà mantenuto dopo la modifica in linea.

La proprietà corrispondente per la modalità di dialogo è `name`.

## Abilitare le funzionalità RTE attivando i plug-in {#enable-rte-functionalities-by-activating-plug-ins}

Le funzionalità dell’editor Rich Text sono disponibili tramite una serie di plug-in, ciascuno con proprietà features . Puoi configurare la proprietà features per attivare o disattivare le varie funzioni di ciascun plug-in.

Per configurazioni dettagliate dei plug-in RTE, consulta [come attivare e configurare i plug-in RTE](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**Esempio**: Scarica [questa configurazione di esempio](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) che illustra come configurare l’editor Rich Text. In questo pacchetto tutte le funzioni sono abilitate.

>[!NOTE]
>
>La [Componente testo Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html?lang=en#the-text-component-and-the-rich-text-editor) consente agli editor di modelli di configurare molti plug-in RTE in un’interfaccia grafica come criteri di contenuto, eliminando la necessità di configurazioni tecniche. I criteri dei contenuti possono funzionare con le configurazioni dell’interfaccia utente RTE come descritto in questo documento.
>
>Per ulteriori informazioni, consulta la sezione [Impostazioni dell’interfaccia utente RTE e criteri dei contenuti](/help/sites-administering/rich-text-editor.md) sezione del presente documento e [Creazione di modelli di pagina](/help/sites-authoring/templates.md) e [Documentazione per gli sviluppatori dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>A scopo di riferimento, i componenti Testo predefiniti (forniti nell’ambito di un’installazione standard) sono disponibili all’indirizzo:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Per creare un componente di testo personalizzato, copia il componente di cui sopra invece di modificare questi componenti.

## Configura RTE, barra degli strumenti {#dialogfullscreen}

AEM consente di configurare l’interfaccia per l’Editor Rich Text in modo diverso per le diverse modalità di modifica. Le impostazioni predefinite sono fornite di seguito. Puoi ignorare queste impostazioni predefinite in base alle tue esigenze. È possibile personalizzare solo le funzioni della barra degli strumenti che si desidera fornire agli autori. Non è necessario specificare tutte le configurazioni della barra degli strumenti.

Per configurare la barra degli strumenti per `dialogFullScreen`, utilizza la seguente configurazione di esempio.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Per la modalità in linea e la modalità a schermo intero vengono utilizzate diverse impostazioni dell’interfaccia utente. La proprietà della barra degli strumenti consente di specificare i pulsanti della barra degli strumenti.

Ad esempio, se il pulsante è esso stesso una funzione (ad esempio, `Bold`), viene specificato come `PluginName#FeatureName` (ad esempio, `links#modifylink`).

Se il pulsante è un pover (contenente alcune caratteristiche di un plug-in), viene specificato come `#PluginName` (ad esempio, `#format`).

Separatori (`|`) tra un gruppo di pulsanti può essere specificato con `-`.

Il nodo a comparsa in modalità in linea o a schermo intero contiene un elenco dei popovers in uso. Ogni nodo figlio sotto il nodo &quot;popovers&quot; prende il nome dal plug-in (ad esempio, formato). Ha una proprietà &quot;items&quot; contenente un elenco delle funzioni del plug-in (ad esempio, format#bold).

## Impostazioni dell’interfaccia utente e criteri del contenuto dell’editor Rich Text {#rtecontentpolicies}

Gli amministratori possono controllare le opzioni dell’editor Rich Text utilizzando i criteri dei contenuti, ad esempio anziché eseguire la configurazione come descritto in precedenza. I criteri dei contenuti definiscono le proprietà di progettazione di un componente quando viene utilizzato come parte di un [modello modificabile](/help/sites-authoring/templates.md). Ad esempio, se un componente di testo che utilizza l’editor Rich Text viene utilizzato con un modello modificabile, i criteri per i contenuti possono definire che l’opzione in grassetto è disponibile e che sono disponibili alcune opzioni di formattazione dei paragrafi. I criteri del contenuto sono riutilizzabili e possono essere applicati a più modelli.

Le opzioni disponibili nell’editor Rich Text scorrono a valle dalle configurazioni dell’interfaccia utente ai criteri dei contenuti.

* Le impostazioni di configurazione dell’interfaccia utente definiscono quali opzioni sono disponibili per i criteri dei contenuti.
* Se la configurazione dell’interfaccia utente dell’editor Rich Text è stata rimossa o non abilita un elemento, il criterio del contenuto non è in grado di configurarlo.
* Un autore ha accesso solo alle funzionalità rese disponibili dalle configurazioni dell’interfaccia utente e dai criteri dei contenuti.

Ad esempio, puoi visualizzare il [Documentazione sui componenti core di testo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html?lang=en#the-text-component-and-the-rich-text-editor).

## Personalizzare la mappatura tra icone e comandi della barra degli strumenti {#iconstoolbar}

Puoi personalizzare la mappatura tra le icone Coral visualizzate sulla barra degli strumenti dell’Editor Rich Text e i comandi disponibili. Non è possibile utilizzare altre icone oltre alle icone Coral.

1. Crea un nodo denominato `icons` sotto `uiSettings/cui`.

1. Crea nodi per singole icone sotto di esso.
1. Su ciascuno dei singoli nodi icona, specifica un’icona Coral e un comando da mappare sull’icona.

Di seguito è riportato uno snippet di esempio per mappare il comando Grassetto sull&#39;icona Corallo denominata `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Passa all’editor Rich Text CoralUI 2 {#switch-to-coralui-rich-text-editor}

In una pagina puoi includere la clientlib dell’editor Rich Text CoralUI 2 o CoralUI 3. Per impostazione predefinita, l’editor Rich Text include la clientlib dell’editor Rich Text CoralUI 3. Per passare all’editor Rich Text CoralUI 2, effettua le seguenti operazioni.

>[!NOTE]
>
>L’Adobe non lo consiglia come best practice. Passa all’editor Rich Text CoralUI 2 come ultima risorsa. I plug-in personalizzati per l’editor Rich Text CoralUI 2 funzionano con l’editor Rich Text CoralUI 3 se i plug-in non dipendono da elementi interni dell’editor Rich Text, ad esempio le classi.
>
>Se utilizzi plug-in personalizzati per l’editor Rich Text CoralUI3, utilizza `rte.coralui3` libreria.


1. Sovrapponi nodo `/libs/cq/gui/components/authoring/editors/clientlibs/core` sotto `/apps`e procedi come segue:

   * Sostituisci `rte.coralui3` con `rte.coralui2` per la proprietà dependencies .
   * Sostituisci `cq.authoring.editor.core.inlineediting.rte.coralui3` con `cq.authoring.editor.core.inlineediting.rte.coralui2` per la proprietà embed .
   * Sostituisci `cq.authoring.rte.coralui3` con `cq.authoring.rte.coralui2` per la proprietà embed .

1. Sovrapponi nodi `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` e `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` sotto `/apps`.

   Rimuovi categoria `cq.authoring.dialog` da `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` e aggiungilo a `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. Modificare qualsiasi altra dipendenza che viene inclusa nella pagina da `rte.coralui3` a `rte.coralui2`. Ad esempio, dopo la sovrapposizione del nodo `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` sotto `/apps`, modifica qualsiasi dipendenza da `rte.coralui3` a `rte.coralui2`.

1. Sovrapponi nodo `cq/ui/widgets` sotto `/apps`. Sostituire la dipendenza `cq.rte` nel nodo `/apps/cq/ui/widgets` con `cq.coralui2.rte`.

>[!NOTE]
>
>L’editor Rich Text CoralUI 2 utilizza modelli handlebars per le finestre di dialogo dei plug-in. Pertanto, la clientlib dell’editor Rich Text CoralUI 2 aveva una dipendenza dalla clientlib handlebars. L’editor Rich Text CoralUI 3 non utilizza modelli handlebars e non presenta alcuna dipendenza associata. Se i plug-in personalizzati utilizzano modelli handlebars, includi la clientlib handlebars nella pagina web.

## Ulteriori informazioni {#further-information}

Per ulteriori informazioni sulla configurazione dell’editor Rich Text, consulta la [API per i Widget AEM](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) riferimento.

In particolare, per visualizzare i plug-in e le relative opzioni disponibili:

* La [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) Il componente fornisce un campo modulo per la modifica di informazioni di testo formattate (testo RTF). Per conoscere tutti i parametri disponibili per il modulo RTF, vedere Opzioni di configurazione.
* Il componente RichText fornisce un’ampia gamma di funzionalità utilizzando i plug-in elencati in [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). Per ogni plug-in:

   * per informazioni dettagliate sulle funzionalità che possono essere abilitate (o disabilitate), consulta Funzioni .
   * Consulta Opzioni di configurazione per tutti i parametri disponibili per una configurazione dettagliata del plug-in appropriato

* Sono inoltre disponibili ulteriori informazioni sulle Regole di HTML per i collegamenti.

Questi possono essere utilizzati per estendere e personalizzare l’editor Rich Text. Ad esempio, per elencare gli ancoraggi disponibili nella pagina durante la creazione di un collegamento, puoi fornire la tua implementazione della `LinkPlugin`.

## Limitazioni note {#known-limitations}

AEM funzionalità RTE presenta le seguenti limitazioni:

* Le funzionalità dell’editor Rich Text sono supportate solo nelle finestre di dialogo AEM componente. L’editor Rich Text non è supportato nelle procedure guidate o nei moduli di base come [Proprietà pagina](/help/sites-developing/page-properties-views.md) e [Scaffolding](/help/sites-authoring/scaffolding.md) nell’interfaccia touch.

* AEM non funziona su [Dispositivi ibridi](/help/release-notes/release-notes.md).

* Non denominare il nodo di configurazione dell’editor Rich Text `config`. In caso contrario, la configurazione dell’editor Rich Text ha effetto solo per gli amministratori e non per gli utenti del gruppo `content-author`.

* L’editor Rich Text non supporta frame in linea o iframe per incorporare contenuti.

## Best practice e suggerimenti {#best-practices-and-tips}

* Abilitare solo i plug-in senza pop-up per una finestra di dialogo mobile. I plug-in senza pop-up sono di dimensioni più piccole e sono più adatti per una finestra di dialogo mobile.
* Abilita i plug-in con pop-up più grandi, ad esempio `Paste` plug-in, solo in modalità a schermo intero o a schermo intero. I plug-in con grandi pop-up necessitano di più spazio disponibile sullo schermo per fornire una buona esperienza di authoring.
* Se utilizzi plug-in personalizzati per l’editor Rich Text CoralUI3, utilizza `rte.coralui3` libreria.

## Risolvere i problemi con l’editor Rich Text {#troubleshoot-issues-with-aem-rich-text-editor}

**Come selezionare più celle di tabella?**

Per selezionare più celle in una tabella, premere `Ctrl` o `Cmd` quindi fare clic sulle celle della tabella una per una.

Esegui l&#39;operazione sulla selezione, ad esempio imposta le proprietà delle celle selezionate.

**I collegamenti ipertestuali vengono persi quando si modifica un componente utilizzando il pulsante Configura**

Aggiungere un collegamento ipertestuale in un componente di testo modificandolo utilizzando il pulsante Configura . Se si modifica nuovamente il collegamento ipertestuale e si convalida il collegamento ipertestuale per la seconda volta, il collegamento potrebbe risultare danneggiato.

Una soluzione consiste nel fare clic sul componente testo quando la finestra di dialogo di modifica viene visualizzata la seconda volta ed eseguire la convalida del collegamento.

Questo problema viene risolto in AEM 6.3 e versioni successive.

**Il contenuto di HTML aggiunto in modalità di modifica sorgente viene perso**

Non aggiungere un HTML soggetto a XSS. AEM, e non l’editor Rich Text, può rimuovere alcuni contenuti di HTML per aderire alle regole antisommossa XSS.

Per verificare che HTML incollato sia salvato, controlla il contenuto salvato in CRXDE (nel nodo del contenuto).

Se non viene salvato, il HTML deve essere stato rimosso dall’editor Rich Text in quanto non rispettava le regole dell’editor Rich Text.

Se salvato in CRXDE ma non sottoposto a rendering nella pagina (per controllare il rendering, consulta la pagina [anteprima](/help/sites-authoring/editing-content.md#preview-mode), viene rimosso dalle regole XSS AEM.

**Il componente multicampo non funziona come previsto**

Per creare un componente multicampo, utilizza esclusivamente CoralUI 3. Non utilizzare le finestre di dialogo dei componenti CoralUI 2.

Inoltre, verifica che il codice di implementazione multicampo e la struttura del nodo siano corretti.

**La configurazione disponibile per gli amministratori non è disponibile per gli autori**

Se gli aggiornamenti delle configurazioni dell’interfaccia vengono rispecchiati per gli amministratori ma non per gli account di authoring, assicurati che il nodo di configurazione non sia denominato `config`. Utilizza la [`configPath` property](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [Configurare i plug-in RTE](configure-rich-text-editor-plug-ins.md)
>* [Utilizza l’editor Rich Text per l’authoring](../sites-authoring/rich-text-editor.md)
>* [Configurare l’editor Rich Text per i siti accessibili](rte-accessible-content.md)
>* [Parità delle funzioni per l’interfaccia touch e l’interfaccia classica](../release-notes/touch-ui-features-status.md)
>* [Esempio di esercitazione per creare un componente composito a più campi](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

