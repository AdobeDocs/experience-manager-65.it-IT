---
title: Configurare i plug-in dell’Editor Rich Text
description: Scopri come configurare i plug-in dell’Editor Rich Text di Adobe Experience Manager per abilitare singole funzionalità.
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
source-git-commit: 11cda989e6a28428f03a269c407a7672e6eab747
workflow-type: tm+mt
source-wordcount: '4406'
ht-degree: 5%

---


# Configurare i plug-in dell’Editor Rich Text {#configure-the-rich-text-editor-plug-ins}

Le funzionalità dell’editor Rich Text sono disponibili tramite una serie di plug-in, ciascuno con la proprietà Features. È possibile configurare la proprietà features per attivare o disattivare una o più funzionalità dell’editor Rich Text. Questo articolo descrive come configurare in modo specifico i plug-in dell’editor Rich Text.

Per informazioni dettagliate sulle altre configurazioni dell’editor Rich Text, consulta [Configurare l’editor Rich Text](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Quando si lavora con CRXDE Lite, si consiglia di salvare le modifiche regolarmente utilizzando [!UICONTROL Salva tutto] opzione.

## Attivare un plug-in e configurare la proprietà features {#activateplugin}

Per attivare un plug-in, segui la procedura riportata di seguito. Alcuni passaggi sono necessari solo quando configuri un plug-in per la prima volta, in quanto i nodi corrispondenti non esistono.

Per impostazione predefinita, `format`, `link`, `list`, `justify`, e `control` I plug-in e tutte le relative funzioni sono abilitati nell’editor Rich Text.

>[!NOTE]
>
>I rispettivi `rtePlugins` il nodo è denominato `<rtePlugins-node>` per evitare duplicazioni in questo articolo.

1. Con CRXDE Lite, individua il componente testo per il progetto.
1. Crea il nodo principale di `<rtePlugins-node>` se non esiste, prima di configurare qualsiasi plug-in RTE:

   * A seconda del componente, i nodi principali sono:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo di configurazione alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Sono di tipo: **jcr:primaryType** `cq:Widget`
   * Entrambi hanno la seguente proprietà:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valore** `./text`


1. A seconda dell’interfaccia per la quale stai configurando, crea un nodo `<rtePlugins-node>`, se non esiste:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Crea un nodo per ogni plug-in da attivare:

   * **Tipo** `nt:unstructured`
   * **Nome** l&#39;ID del plug-in richiesto

Dopo aver attivato un plug-in, segui queste linee guida per configurare `features` proprietà.

|  | Abilita tutte le funzioni | Abilita alcune funzioni specifiche | Disattiva tutte le funzionalità |
|---|---|---|---|
| Nome | funzioni | funzioni | funzioni |
| Tipo | Stringa | Stringa[] (multi-string; imposta Type su String e fai clic su Multi in CRXDE Lite) | Stringa |
| Valore | `*` (un asterisco) | imposta su uno o più valori di feature | - |

## Comprendere il plug-in Findreplace {#findreplace}

Il `findreplace` Il plug-in non richiede alcuna configurazione. Funziona immediatamente.

Quando si utilizza la funzionalità di sostituzione, la stringa sostitutiva deve essere immessa contemporaneamente alla stringa da trovare. Tuttavia, è ancora possibile fare clic su Trova per cercare la stringa prima di sostituirla. Se la stringa sostitutiva viene immessa dopo aver fatto clic su Trova, la ricerca riprende dall’inizio del testo.

La finestra di dialogo Trova e sostituisci diventa trasparente quando si fa clic su Trova e diventa opaca quando si fa clic su Sostituisci. Ciò consente all’autore di rivedere il testo che verrà sostituito. Se si fa clic su Sostituisci tutto, la finestra di dialogo si chiude e viene visualizzato il numero di sostituzioni effettuate.

## Configurare le modalità Incolla {#paste-modes}

Quando si utilizza l’editor Rich Text, gli autori possono incollare il contenuto in una delle tre modalità seguenti:

* **Modalità browser**: incolla il testo utilizzando l’implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati.

* **Modalità testo normale**: incolla il contenuto degli Appunti come testo normale. Elimina tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserirli in [!DNL Experience Manager] componente.

* **Modalità MS Word**: quando si copia da MS Word, incolla il testo con formattazione, incluse le tabelle. La copia e l’incolla di testo da un’altra origine, ad esempio una pagina web o MS Excel, non sono supportate e mantengono solo una formattazione parziale.

### Configurare le opzioni Incolla disponibili nella barra degli strumenti dell’editor Rich Text  {#configure-paste-options-available-on-the-rte-toolbar}

Nella barra degli strumenti dell’editor Rich Text è possibile fornire agli autori alcune o nessuna delle tre icone seguenti:

* **[!UICONTROL Incolla (Ctrl+V)]**: può essere preconfigurato in modo da corrispondere a una delle tre modalità Incolla precedenti.

* **[!UICONTROL Incolla come testo]**: fornisce funzionalità in modalità testo normale.

* **[!UICONTROL Incolla da Word]**: fornisce la funzionalità della modalità MS Word.

Per configurare l’editor Rich Text in modo da visualizzare le icone richieste, effettua le seguenti operazioni.

1. Passa al componente, ad esempio `/apps/<myProject>/components/text`.
1. Passa al nodo `rtePlugins/edit`. Consulta [attivare un plug-in](#activateplugin) se il nodo non esiste.
1. Creare `features` proprietà sul `edit` e aggiungi una o più funzionalità. Salva tutte le modifiche.

### Configurare il comportamento dell&#39;icona e della scelta rapida Incolla (Ctrl+V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Puoi preconfigurare il comportamento di **[!UICONTROL Incolla (Ctrl+V)]** , utilizzando i passaggi seguenti. Questa configurazione definisce anche il comportamento della scelta rapida da tastiera Ctrl+V utilizzata dagli autori per incollare il contenuto.

La configurazione consente i tre tipi di casi di utilizzo seguenti:

* Incolla il testo utilizzando l’implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati. Configurato con `browser` di seguito.

* Incolla il contenuto degli Appunti come testo normale. Elimina tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserirli nel componente AEM. Configurato con `plaintext` di seguito.

* Incolla il testo, incluse le tabelle, con formattazione durante la copia da MS Word. La copia e l’incolla di testo da un’altra origine, ad esempio una pagina web o MS Excel, non sono supportate e mantengono solo una formattazione parziale. Configurato con `wordhtml` di seguito.

1. Nel componente, passa a `<rtePlugins-node>/edit` nodo. Crea i nodi se non esistono. Per ulteriori informazioni, consulta [attivare un plug-in](#activateplugin).
1. In `edit` nodo creare una proprietà utilizzando i dettagli seguenti:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **Valore** Una delle modalità di incollamento richieste `browser`, `plaintext`, o `wordhtml`.

### Configurare i formati consentiti quando si incollano i contenuti {#pasteformats}

Incolla-come-Microsoft-Word (`paste-wordhtml`) può essere ulteriormente configurata in modo da poter definire esplicitamente quali stili sono consentiti quando si incollano in AEM da un altro programma, ad esempio Microsoft Word.

Ad esempio, se solo i formati e gli elenchi in grassetto devono essere consentiti quando si incolla in AEM, puoi filtrare gli altri formati. Questa operazione è denominata filtro di incollamento configurabile e può essere eseguita per entrambi:

* [Testo](#paste-modes)
* [Collegamenti](#linkstyles)

Per i collegamenti, puoi anche definire i protocolli che vengono accettati automaticamente.

Per configurare i formati consentiti quando si incolla testo in AEM da un altro programma:

1. Nel componente, passa al nodo `<rtePlugins-node>/edit`. Crea i nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Crea un nodo sotto `edit` nodo in cui inserire le regole HTML incolla:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Crea un nodo sotto `htmlPasteRules`, per contenere i dettagli dei formati di base consentiti:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Per controllare i singoli formati accettati, crea una o più delle seguenti proprietà sul `allowBasics` nodo:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (sia per i collegamenti che per gli ancoraggi denominati)
   * **Nome** `image`

   Tutte le proprietà sono di **Tipo** `Boolean`, quindi nel caso **Valore** è possibile selezionare o rimuovere il segno di spunta per abilitare o disabilitare la funzionalità.

   >[!NOTE]
   >
   >Se non è definito in modo esplicito, viene utilizzato il valore predefinito true e il formato viene accettato.

1. Altri formati possono essere definiti utilizzando un intervallo di altre proprietà o nodi, anch&#39;essi applicati al `htmlPasteRules` nodo. Salva tutte le modifiche.

Puoi utilizzare le seguenti proprietà per `htmlPasteRules`.

| Proprietà | Tipo | Descrizione |
|---|---|---|
| `allowBlockTags` | Stringa | Definisce l’elenco dei tag di blocco consentiti. Alcuni tag di blocco possibili includono: <ul> <li>titoli (h1, h2, h3)</li> <li>lettere p)</li> <li>elenchi (ol, ul)</li> <li>tabelle (tabella)</li> </ul> |
| `fallbackBlockTag` | Stringa | Definisce il tag di blocco utilizzato per tutti i blocchi con un tag di blocco non incluso in `allowBlockTags`. `p` nella maggior parte dei casi. |
| tabella | nt:unstructured | Definisce il comportamento quando si incollano le tabelle. Questo nodo deve avere la proprietà `allow` (tipo booleano) per definire se è consentito incollare tabelle. Se consenti è impostato su `false`, è necessario specificare la proprietà `ignoreMode` (tipo String) per definire la modalità di gestione del contenuto della tabella incollato. Valori validi per `ignoreMode` sono: <ul> <li>`remove`: rimuove il contenuto della tabella.</li> <li>`paragraph`: trasforma le celle della tabella in paragrafi.</li> </ul> |
| list | nt:unstructured | Definisce il comportamento quando si incollano gli elenchi. Deve avere la proprietà `allow` (tipo booleano) per definire se è consentito incollare gli elenchi. Se `allow` è impostato su `false`, è necessario specificare la proprietà `ignoreMode` (tipo Stringa) per definire come gestire il contenuto dell’elenco incollato. Valori validi per `ignoreMode` sono: <ul><li> `remove`: rimuove il contenuto dell’elenco.</li> <li>`paragraph`: trasforma le voci di elenco in paragrafi.</li> </ul> |

Un esempio di valida `htmlPasteRules` La struttura è riportata di seguito.

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

## Configurare gli stili di testo {#textstyles}

Gli autori possono applicare gli stili per modificare l&#39;aspetto di una parte di testo. Gli stili sono basati su classi CSS predefinite nel foglio di stile CSS. Il contenuto stilizzato è racchiuso in `span` tag che utilizzano `class` attributo per fare riferimento alla classe CSS. Esempio: `<span class=monospaced>Monospaced Text Here</span>`.

Quando il plug-in Stili viene attivato per la prima volta, non sono disponibili stili predefiniti. L&#39;elenco popup è vuoto. Per fornire agli autori stili, effettuare le seguenti operazioni:

* Abilita il selettore a discesa Stile.
* Specificare la posizione dei fogli di stile.
* Specificare i singoli stili che possono essere selezionati dall&#39;elenco a discesa Stile.

Per le configurazioni successive, per aggiungere altri stili, seguire solo le istruzioni per fare riferimento a un nuovo foglio di stile e specificare gli stili aggiuntivi.

>[!NOTE]
>
>Puoi definire gli stili per [tabelle o celle di tabella](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Queste configurazioni richiedono procedure separate.

### Abilitare l’elenco di selettori a discesa Stile {#styleselectorlist}

Questa operazione viene eseguita abilitando il plug-in stili.

1. Nel componente, passa al nodo `<rtePlugins-node>/styles`. Crea i nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Creare `features` proprietà sul `styles` nodo:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

1. Salva tutte le modifiche.

>[!NOTE]
>
>Una volta attivato il plug-in Stili, l’elenco a discesa Stile viene visualizzato nella finestra di dialogo per modifica. Tuttavia, l’elenco è vuoto perché non è configurato alcuno stile.

### Specificare la posizione del foglio di stile {#locationofstylesheet}

Specificare quindi la posizione dei fogli di stile a cui si desidera fare riferimento:

1. Passa al nodo principale del componente testo, ad esempio `/apps/<myProject>/components/text`.
1. Aggiungi la proprietà `externalStyleSheets` al nodo principale di `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Tipo** `String[]` (stringa multipla; fare clic su **Più** in CRXDE)
   * **Valore/i** Percorso e nome di ogni foglio di stile che si desidera includere. Utilizza i percorsi dell’archivio.

   >[!NOTE]
   >
   >È possibile aggiungere riferimenti ad altri fogli di stile in qualsiasi momento successivo.

1. Salva tutte le modifiche.

>[!NOTE]
>
>Quando si utilizza l’editor Rich Text in una finestra di dialogo (interfaccia classica), è possibile specificare fogli di stile ottimizzati per la modifica di testo RTF. A causa di restrizioni tecniche, il contesto CSS viene perso nell’editor, pertanto potrebbe essere utile emulare questo contesto per migliorare l’esperienza WYSIWYG.
>
>L’editor Rich Text utilizza un elemento DOM contenitore con un ID di `CQrte` che può essere utilizzato per fornire stili diversi per la visualizzazione e la modifica:
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### Specificare gli stili disponibili nell&#39;elenco a comparsa {#stylesindropdown}

1. Nella definizione del componente, passa al nodo `<rtePlugins-node>/styles`, come creato in [Abilitazione del selettore a discesa dello stile](#styleselectorlist).
1. Sotto il nodo `styles`, crea un nuovo nodo (chiamato anche `styles`) per mantenere disponibile l&#39;elenco:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Crea un nuovo nodo sotto `styles` per rappresentare un singolo stile:

   * **Nome**, è possibile specificare il nome, ma deve essere adatto allo stile
   * **Tipo** `nt:unstructured`

1. Aggiungi la proprietà `cssName` a questo nodo per fare riferimento alla classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valore** Il nome della classe CSS (senza un &quot;.&quot; precedente).ad esempio, `cssClass` invece di `.cssClass`)

1. Aggiungi la proprietà `text` sullo stesso nodo; questo definisce il testo visualizzato nella casella di selezione:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valore** Descrizione dello stile; viene visualizzata nella casella di selezione a discesa Stile.

1. Salva le modifiche.

   Ripeti i passaggi precedenti per ogni stile richiesto.

### Configurare l’editor Rich Text per interruzioni di parola ottimali in giapponese {#jpwordwrap}

Gli autori che utilizzano l’AEM per creare contenuti in lingua giapponese possono applicare uno stile ai caratteri per evitare interruzioni di riga laddove non siano necessarie. Questo consente agli autori di lasciare che le frasi si interrompano nella posizione desiderata. Lo stile di questa funzionalità si basa sulla classe CSS predefinita nel foglio di stile CSS.

>[!NOTE]
>
>Questa funzione richiede almeno AEM 6.5 Service Pack 1.

Per creare lo stile che gli autori possono applicare al testo giapponese, effettuare le seguenti operazioni:

1. Crea un nuovo nodo sotto il nodo degli stili. Consulta [specifica un nuovo stile](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Aggiungi la proprietà `cssName` al nodo per fare riferimento alla classe CSS. Questo nome di classe è un nome riservato per la funzione di ritorno a capo automatico giapponese.
   * Nome: `cssName`
   * Tipo: `String`
   * Valore: `jpn-word-wrap` (senza precedenti `.`)

1. Aggiungi il testo della proprietà allo stesso nodo. Il valore è il nome dello stile visualizzato dagli autori durante la selezione dello stile.
   * Nome: `text`
*Tipo: 
`String`
   * Valore: `Japanese word-wrap`

1. Creare un foglio di stile e specificarne il percorso. Consulta [specificare la posizione del foglio di stile](#locationofstylesheet). Aggiungere il contenuto seguente al foglio di stile. Modifica il colore di sfondo come desiderato.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Foglio di stile per rendere disponibile agli autori la funzione di disposizione del testo in giapponese](assets/rte_jpwordwrap_stylesheet.jpg)

## Configurare i formati di paragrafo {#paraformats}

Qualsiasi testo creato nell’editor Rich Text viene inserito all’interno di un tag di blocco, il cui valore predefinito è `<p>`. Attivando `paraformat` plug-in, è possibile specificare ulteriori tag di blocco che possono essere assegnati ai paragrafi utilizzando un elenco a discesa. I formati di paragrafo determinano il tipo di paragrafo assegnando il tag di blocco corretto. L’autore può selezionarli e assegnarli utilizzando il selettore Formato. I tag di blocco di esempio includono, tra gli altri, il paragrafo standard &lt;p> e intestazioni &lt;h1>, &lt;h2>e così via.

>[!CAUTION]
>
>Questo plug-in non è adatto per contenuti con struttura complessa, ad esempio elenchi o tabelle.

>[!NOTE]
>
>Se un tag di blocco, ad esempio &lt;hr> , non può essere assegnato a un paragrafo, non è un caso d’uso valido per un plug-in paraformat.

Quando il plug-in Formati di paragrafo viene attivato per la prima volta, non sono disponibili formati di paragrafo predefiniti. L&#39;elenco popup è vuoto. Per fornire agli autori formati di paragrafo, effettuare le seguenti operazioni:

* Abilitare l&#39;elenco dei selettori a discesa Formato.
* Specifica i tag di blocco che possono essere selezionati come formati di paragrafo dal menu a discesa.

Per le configurazioni successive, ad esempio per aggiungere altri formati, segui solo la parte pertinente delle istruzioni.

### Abilita il selettore a discesa Formato {#formatselectorlist}

Innanzitutto, abilita il plug-in paraformat:

1. Nel componente, passa al nodo `<rtePlugins-node>/paraformat`. Crea i nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Creare `features` proprietà sul `paraformat` nodo:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

>[!NOTE]
Se il plug-in non viene configurato ulteriormente, vengono attivati i seguenti formati predefiniti:
* Paragrafo ( `<p>`)
* Intestazione 1 ( `<h1>`)
* Intestazione 2 ( `<h2>`)
* Intestazione 3 ( `<h3>`)
>


>[!CAUTION]
Durante la configurazione dei formati di paragrafo dell’editor Rich Text, non rimuovere il tag di paragrafo &lt;p> come opzione di formattazione. Se il `<p>` viene rimosso, l’autore di contenuto non può selezionare il tag **Formati dei paragrafi** anche se sono configurati altri formati.

### Specificare i formati di paragrafo disponibili {#paraformatsindropdown}

I formati dei paragrafi possono essere resi disponibili per la selezione:

1. Nella definizione del componente, passa al nodo `<rtePlugins-node>/paraformat`, come creato in [Abilitazione del selettore a discesa Formato](#styleselectorlist).
1. Sotto `paraformat` node crea un nuovo nodo, che contiene l’elenco dei formati:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crea un nuovo nodo sotto `formats` , contiene i dettagli per un singolo formato:

   * **Nome**, è possibile specificare il nome, ma deve essere appropriato per il formato (ad esempio, myParagraph, myheader1).
   * **Tipo** `nt:unstructured`

1. A questo nodo, aggiungi la proprietà per definire il tag di blocco utilizzato:

   * **Nome** `tag`
   * **Tipo** `String`
   * **Valore** Il tag di blocco per il formato; ad esempio: p, h1, h2, ecc.

      Non è necessario inserire le parentesi angolari di delimitazione.

1. Per visualizzare il testo descrittivo nell’elenco a discesa, aggiungi un’altra proprietà allo stesso nodo:

   * **Nome** `description`
   * **Tipo** `String`
   * **Valore** Testo descrittivo per questo formato, ad esempio Paragrafo, Titolo 1, Titolo 2 e così via. Questo testo viene visualizzato nell&#39;elenco di selezione Formato.

1. Salva le modifiche.

   Ripeti i passaggi per ogni formato richiesto.

>[!CAUTION]
Se si definiscono formati personalizzati, i formati predefiniti (`<p>`, `<h1>`, `<h2>`, e `<h3>`) vengono rimossi. Ricrea `<p>` in quanto è il formato predefinito.

## Configurare caratteri speciali {#spchar}

In un impianto AEM standard, quando `misctools` il plug-in è abilitato per i caratteri speciali (`specialchars`) è immediatamente disponibile una selezione predefinita, ad esempio i simboli di copyright e marchio.

È possibile configurare l’editor Rich Text in modo da rendere disponibile una selezione personalizzata di caratteri, definendo caratteri distinti o un’intera sequenza.

>[!CAUTION]
L’aggiunta di caratteri speciali sostituisce la selezione predefinita. Se necessario, ridefinisci questi caratteri nella tua selezione.

### Definisci un singolo carattere {#definesinglechar}

1. Nel componente, passa al nodo `<rtePlugins-node>/misctools`. Crea i nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Creare `features` proprietà sul `misctools` nodo:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valore** `specialchars`

          (o `String / *` se si applicano tutte le funzioni di questo plug-in)

1. Sotto `misctools` crea un nodo che contenga le configurazioni dei caratteri speciali:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. Sotto `specialCharsConfig` crea un altro nodo per l’elenco dei caratteri:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. Sotto `chars` aggiungi un nuovo nodo per contenere una singola definizione di carattere:

   * **Nome** è possibile specificare il nome, ma deve riflettere il carattere, ad esempio metà.
   * **Tipo** `nt:unstructured`

1. A questo nodo aggiungi la seguente proprietà:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Valore** la rappresentazione HTML del carattere richiesto; ad esempio, `&189;` per la frazione metà.

1. Salva le modifiche.

In CRXDE, una volta salvata la proprietà, viene visualizzato il carattere rappresentato. Vedi sotto l&#39;esempio di mezzo. Ripeti i passaggi precedenti per rendere disponibili agli autori caratteri più speciali.

![In CRXDE, aggiungi un singolo carattere da rendere disponibile nella barra degli strumenti dell’editor Rich Text](assets/chlimage_1-106.png "In CRXDE, aggiungi un singolo carattere da rendere disponibile nella barra degli strumenti dell’editor Rich Text")

### Definire un intervallo di caratteri {#definerangechar}

1. Utilizza i passaggi da 1 a 3 da [Definizione di un singolo carattere](#definesinglechar).
1. Sotto `chars` aggiungi un nuovo nodo che contenga la definizione dell’intervallo di caratteri:

   * **Nome** è possibile specificare il nome, ma deve riflettere l&#39;intervallo di caratteri, ad esempio le matite.
   * **Tipo** `nt:unstructured`

1. Sotto questo nodo (denominato in base all’intervallo di caratteri speciali) aggiungi le due proprietà seguenti:

   * **Nome** `rangeStart`

      **Tipo** `Long`
      **Valore** il [Unicode](https://unicode.org/) rappresentazione (decimale) del primo carattere dell&#39;intervallo

   * **Nome** `rangeEnd`

      **Tipo** `Long`
      **Valore** il [Unicode](https://unicode.org/) rappresentazione (decimale) dell’ultimo carattere nell’intervallo

1. Salva le modifiche.

   Ad esempio, definisci un intervallo da 9998 - 10000 fornisce i seguenti caratteri.

   ![In CRXDE, definisci un intervallo di caratteri da rendere disponibili nell’editor Rich Text](assets/chlimage_1-107.png)

   *Figura: In CRXDE, definisci un intervallo di caratteri da rendere disponibili nell’editor Rich Text*

   ![I caratteri speciali disponibili nell’editor Rich Text vengono visualizzati agli autori in una finestra popup](assets/rtepencil.png "I caratteri speciali disponibili nell’editor Rich Text vengono visualizzati agli autori in una finestra popup")

## Configurare gli stili di tabella {#tablestyles}

Gli stili vengono in genere applicati al testo, ma è possibile applicare un set separato di stili anche a una tabella o ad alcune celle di tabella. Tali stili sono disponibili per gli autori dalla casella del selettore Stile nella finestra di dialogo Proprietà cella o Proprietà tabella. Gli stili sono disponibili quando si modifica una tabella all’interno di un componente Testo (o derivata) e non nel componente Tabella standard.

>[!NOTE]
Puoi definire stili per tabelle e celle solo per l’interfaccia classica.

>[!NOTE]
Copiare e incollare tabelle nel componente Editor Rich Text o da esso dipende dal browser. Non è supportato per tutti i browser. Puoi ottenere risultati diversi a seconda della struttura della tabella e del browser. Ad esempio, quando copi e incolla una tabella in un componente Editor Rich Text in Mozilla Firefox nell’interfaccia classica e nell’interfaccia touch, il layout della tabella non viene mantenuto.

1. All’interno del componente passa al nodo `<rtePlugins-node>/table`. Crea i nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Creare `features` proprietà sul `table` nodo:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

   >[!NOTE]
   Se non desiderate attivare tutte le feature di tabella, potete creare `features` proprietà come:
   * **Tipo** `String[]`
   * **Valore** s) uno dei seguenti elementi o entrambi, a seconda dei casi:
      * `table` per consentire la modifica delle proprietà della tabella, inclusi gli stili.
      * `cellprops` per consentire la modifica delle proprietà delle celle, inclusi gli stili.


1. Definisci la posizione dei fogli di stile CSS in modo che facciano riferimento a essi. Consulta [Specifica della posizione del foglio di stile](#locationofstylesheet) come quando definisci [stili per il testo](#textstyles). La posizione può essere definita se sono stati definiti altri stili.
1. Sotto `table` nodo creare i seguenti nuovi nodi (come richiesto):

   * Per definire gli stili per l&#39;intera tabella (disponibile in **Proprietà tabella**):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Per definire gli stili per le singole celle (disponibili in **Proprietà cella**):

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Crea un nuovo nodo (sotto il `tableStyles` o `cellStyles` a seconda dei casi) per rappresentare un singolo stile:

   * **Nome** è possibile specificare il nome, ma deve riflettere lo stile.
   * **Tipo** `nt:unstructured`

1. In questo nodo crea le proprietà:

   * Per definire lo stile CSS a cui fare riferimento

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un precedente `.`ad esempio: `cssClass` invece di `.cssClass`)
   * Per definire un testo descrittivo da visualizzare nel selettore a discesa

      * **Nome** `text`
      * **Tipo** `String`
      * **Valore** testo da visualizzare nell&#39;elenco di selezione


1. Salva tutte le modifiche.

Ripeti i passaggi precedenti per ogni stile richiesto.

### Configurare le intestazioni nascoste nelle tabelle per l’accessibilità {#hiddenheader}

Talvolta è possibile creare tabelle di dati senza testo visivo in un&#39;intestazione di colonna presupponendo che lo scopo dell&#39;intestazione sia implicito dalla relazione visiva della colonna con altre colonne. In questo caso, è necessario fornire testo interno nascosto nella cella dell’intestazione per consentire agli assistenti vocali e altre tecnologie per aiutare i lettori con varie esigenze a comprendere lo scopo della colonna.

Per migliorare l’accessibilità in tali scenari, l’editor Rich Text supporta le celle di intestazione nascoste. Inoltre, fornisce le impostazioni di configurazione relative alle intestazioni nascoste nelle tabelle. Queste impostazioni consentono di applicare stili CSS alle intestazioni nascoste nelle modalità di modifica e anteprima. Per aiutare gli autori a identificare le intestazioni nascoste nella modalità di modifica, includi i seguenti parametri nel codice:

* `hiddenHeaderEditingCSS`: specifica il nome della classe CSS applicata alla cella di intestazione nascosta quando viene modificato l’editor Rich Text.
* `hiddenHeaderEditingStyle`: specifica una stringa di stile applicata alla cella di intestazione nascosta quando viene modificato l’editor Rich Text.

Se nel codice specifichi sia CSS che la stringa di stile, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche di configurazione apportate dalla stringa di stile.

Per consentire agli autori di applicare CSS sulle intestazioni nascoste nella modalità di anteprima, puoi includere i seguenti parametri nel codice:

* `hiddenHeaderClassName`: specifica il nome della classe CSS applicata alla cella di intestazione nascosta in modalità anteprima.
* `hiddenHeaderStyle`: specifica una stringa di stile applicata alla cella di intestazione nascosta in modalità anteprima.

Se nel codice specifichi sia CSS che la stringa di stile, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche di configurazione apportate dalla stringa di stile.

## Aggiungere dizionari per il controllo ortografico {#adddict}

Quando il plug-in spellcheck è attivato, l&#39;editor Rich Text utilizza dizionari per ogni lingua appropriata. Questi vengono quindi selezionati in base alla lingua del sito web utilizzando la proprietà language della sottostruttura o estraendo la lingua dall’URL; ad esempio. il `/en/` la filiale viene selezionata come inglese, il `/de/` filiale come tedesco.

>[!NOTE]
Il messaggio `Spell checking failed` viene visualizzato se si tenta di controllare una lingua non installata. I dizionari standard si trovano in `/libs/cq/spellchecker/dictionaries`, insieme ai file readme appropriati. Non modificare i file.

Un&#39;installazione standard per AEM include i dizionari per l&#39;inglese americano (`en_us`) e inglese britannico (`en_gb`). Per aggiungere altri dizionari, eseguire la procedura seguente.

1. Passa alla pagina [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Effettuare una delle seguenti operazioni per trovare un dizionario della lingua scelta:

   * Cerca il dizionario della tua lingua. Nella pagina del dizionario individuare il collegamento alla pagina Web dell&#39;autore o della sorgente originale. Individua i file del dizionario per v2.x in tale pagina.
   * Cerca i file del dizionario v2.x in [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Scarica l’archivio con le definizioni di ortografia. Estrarre il contenuto dell&#39;archivio nel file system.

   >[!CAUTION]
   Solo dizionari nel `MySpell` per OpenOffice.org v2.0.1 o versioni precedenti, sono supportati. Poiché i dizionari sono ora file di archivio, si consiglia di verificare l&#39;archivio dopo averlo scaricato.

1. Individua i file .aff e .dic. Mantieni il nome del file in minuscolo. Ad esempio: `de_de.aff` e `de_de.dic`.
1. Carica i file .aff e .dic nell’archivio in `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
Il controllo ortografico dell’editor Rich Text è disponibile su richiesta. Non viene eseguito automaticamente quando si inizia a digitare il testo. Per eseguire il controllo ortografico, fare clic su [!UICONTROL Controllo ortografia] dalla barra degli strumenti. L’editor Rich Text controlla l’ortografia delle parole ed evidenzia le parole errate.
Se si incorporano le modifiche suggerite dal correttore ortografico, lo stato del testo cambia e le parole errate non vengono più evidenziate. Per eseguire il controllo ortografico, toccare o fare di nuovo clic sul pulsante Controllo ortografia.

## Configurare la dimensione della cronologia per le azioni Annulla e Ripristina {#undohistory}

L’editor Rich Text consente agli autori di annullare o ripristinare alcune delle ultime modifiche. Per impostazione predefinita, nella cronologia sono memorizzate 50 modifiche. Puoi configurare questo valore come richiesto.

1. All’interno del componente passa al nodo `<rtePlugins-node>/undo`. Crea questi nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Il giorno `undo` nodo creare la proprietà:

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valore** il numero di passaggi di annullamento che si desidera salvare nella cronologia. Il valore predefinito è 50. Utilizzare `0` per disattivare completamente l&#39;operazione Annulla/Ripristina.

1. Salva le modifiche.

## Configurare le dimensioni della scheda {#tabsize}

Quando il carattere di tabulazione viene premuto all&#39;interno di un testo, viene inserito un numero predefinito di spazi; per impostazione predefinita, si tratta di tre spazi unificatori e di uno spazio.

Per definire le dimensioni della scheda:

1. Nel componente, passa al nodo `<rtePlugins-node>/keys`. Crea i nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Il giorno `keys` nodo creare la proprietà:

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valore** il numero di spazi da utilizzare per il tabulatore

1. Salva le modifiche.

## Imposta margine rientro {#indentmargin}

Quando il rientro è abilitato (impostazione predefinita), è possibile definire la dimensione del rientro:

>[!NOTE]
Questa dimensione di rientro viene applicata solo ai paragrafi (blocchi) di testo e non influisce sul rientro degli elenchi effettivi.

1. All’interno del componente passa al nodo `<rtePlugins-node>/lists`. Crea questi nodi se non esistono. Per ulteriori dettagli, consulta [attivare un plug-in](#activateplugin).
1. Il giorno `lists` nodo creare il `identSize` parametro:

   * **Nome**: `identSize`
   * **Tipo**: `Long`
   * **Valore**: numero di pixel necessari per il margine di rientro.

## Configurare l&#39;altezza dello spazio modificabile {#editablespace}

>[!NOTE]
Questa opzione è applicabile solo quando si utilizza l’editor Rich Text in una finestra di dialogo (non la modifica diretta nell’interfaccia classica).

Puoi definire l’altezza dello spazio modificabile mostrato nella finestra di dialogo del componente:

1. Il giorno `../items/text` nella definizione della finestra di dialogo del componente, crea una nuova proprietà:

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valore** altezza in pixel dell’area di lavoro per la modifica.

   >[!NOTE]
   L&#39;altezza della finestra di dialogo non viene modificata.

1. Salva le modifiche.

## Configurare stili e protocolli per i collegamenti {#linkstyles}

Quando aggiungi collegamenti in AEM, puoi definire:

* Stili CSS da utilizzare
* I protocolli sono stati accettati automaticamente

Per configurare il modo in cui i collegamenti vengono aggiunti in AEM da un altro programma, definisci le regole di HTML.

1. Con CRXDE Lite, individua il componente testo per il progetto.
1. Crea un nuovo nodo allo stesso livello di `<rtePlugins-node>`, ovvero crea il nodo sotto il nodo principale di `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   Il `../items/text` il nodo ha la proprietà:
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valore** `richtext`

   La posizione del `../items/text` può variare a seconda della struttura della finestra di dialogo; due esempi sono `/apps/myProject>/components/text/dialog/items/text` e `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Sotto `htmlRules`, crea un nuovo nodo.

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. Sotto `links` Il nodo definisce le proprietà come richiesto:

   * Stile CSS per collegamenti interni:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un &quot;.&quot; precedente).ad esempio, `cssClass` invece di `.cssClass`)
   * Stile CSS per collegamenti esterni

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Valore** il nome della classe CSS (senza un &quot;.&quot; precedente).ad esempio, `cssClass` invece di `.cssClass`)
   * Array di validi **protocolli**. I protocolli supportati sono `http://`, `https://`, `file://`, e `mailto:`.

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valore**(s) uno o più protocolli
   * **defaultProtocol** (proprietà di tipo **Stringa**): protocollo da utilizzare se l’utente non ne ha specificato esplicitamente uno.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valore**(s) uno o più protocolli predefiniti
   * Definizione di come gestire l’attributo target di un collegamento. Crea un nuovo nodo:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

      Sul nodo `targetConfig`: definisci le proprietà richieste:

      * Specifica la modalità di destinazione:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valore** s) :

            * `auto`: indica che viene scelto un target automatico

               (specificato da `targetExternal` proprietà per collegamenti esterni o `targetInternal` per collegamenti interni).

            * `manual`: non applicabile in questo contesto
            * `blank`: non applicabile in questo contesto
      * Destinazione dei collegamenti interni:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Valore** destinazione per i collegamenti interni (da utilizzare solo quando la modalità è `auto`)
      * Destinazione per i collegamenti esterni:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Valore** destinazione per i collegamenti esterni (utilizzata solo quando la modalità è `auto`).








1. Salva tutte le modifiche.
