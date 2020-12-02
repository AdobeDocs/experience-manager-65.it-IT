---
title: Configurare i plug-in Editor Rich Text
description: Scoprite come configurare i plug-in di Adobe Experience Manager Rich Text Editor per abilitare singole funzionalità.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6f5e650c99017c4b2f04ca8495eea8481b3236cd
workflow-type: tm+mt
source-wordcount: '4398'
ht-degree: 3%

---


# Configurare i plug-in Editor Rich Text {#configure-the-rich-text-editor-plug-ins}

Le funzionalità RTE sono disponibili tramite una serie di plug-in, ognuno dei quali dispone della proprietà features. È possibile configurare la proprietà features per attivare o disattivare una o più funzioni RTE. Questo articolo descrive come configurare in modo specifico i plug-in RTE.

Per informazioni dettagliate sulle altre configurazioni dell&#39;editor Rich Text, vedere [Configurare l&#39;editor Rich Text](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>Quando si lavora con CRXDE Lite, si consiglia di salvare regolarmente le modifiche utilizzando l&#39;opzione [!UICONTROL Salva tutto].

## Attivare un plug-in e configurare la proprietà features {#activateplugin}

Per attivare un plug-in, effettuate le seguenti operazioni. Alcuni passaggi sono necessari solo quando configurate un plug-in per la prima volta, in quanto i nodi corrispondenti non esistono.

Per impostazione predefinita, i plug-in `format`, `link`, `list`, `justify` e `control` e tutte le relative funzioni sono abilitati nell&#39;editor Rich Text.

>[!NOTE]
>
>Il rispettivo nodo `rtePlugins` è denominato `<rtePlugins-node>` per evitare duplicazioni in questo articolo.

1. Utilizzando CRXDE Lite, individuate il componente di testo per il progetto.
1. Crea il nodo padre di `<rtePlugins-node>` se non esiste, prima di configurare eventuali plug-in RTE:

   * A seconda del componente, i nodi principali sono:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * un nodo di configurazione alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * Sono di tipo: **jcr:PrimaryType** `cq:Widget`
   * Entrambe hanno la seguente proprietà:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valore** `./text`


1. A seconda dell&#39;interfaccia per la quale state configurando, create un nodo `<rtePlugins-node>`, se non esiste:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Di seguito, create un nodo per ciascun plug-in che desiderate attivare:

   * **Tipo** `nt:unstructured`
   * **Denominate** l&#39;ID plug-in del plug-in richiesto

Dopo aver attivato un plug-in, segui queste linee guida per configurare la proprietà `features`.

|  | Abilitare tutte le funzioni | Abilitare alcune funzionalità specifiche | Disattiva tutte le funzioni |
|---|---|---|---|
| Nome | funzionalità | funzionalità | funzionalità |
| Tipo | Stringa | String[] (multi-stringa; imposta Tipo su Stringa e fai clic su Più in CRXDE Lite) | Stringa |
| Valore | `*` (un asterisco) | impostare uno o più valori di feature | - |

## Informazioni sul plug-in più recente {#findreplace}

Il plug-in `findreplace` non richiede alcuna configurazione. Funziona fuori dagli schemi.

Quando si utilizza la funzionalità replace, la stringa replace da sostituire deve essere immessa contemporaneamente alla stringa find. È comunque possibile fare clic su find per cercare la stringa prima di sostituirla. Se la stringa di sostituzione viene immessa dopo aver fatto clic su Trova, la ricerca viene reimpostata all’inizio del testo.

La finestra di dialogo Trova e sostituisci diventa trasparente quando si fa clic su Trova e diventa opaca quando si fa clic su Sostituisci. Questo consente all’autore di rivedere il testo che verrà sostituito dall’autore. Se gli utenti fanno clic su replace all (Sostituisci tutto), la finestra di dialogo viene chiusa e viene visualizzato il numero di sostituzioni effettuate.

## Configurare le modalità Incolla {#pastemodes}

Quando si utilizza l’editor Rich Text, gli autori possono incollare il contenuto in una delle tre modalità seguenti:

* **Modalità** browser: Incolla il testo utilizzando l&#39;implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati.

* **Modalità** testo normale: Incolla il contenuto degli Appunti come testo normale. Rimuove tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserire AEM componente.

* **Modalità** MS Word: Incolla il testo, incluse le tabelle, con la formattazione durante la copia da MS Word. La copia e l&#39;incolla del testo da un&#39;altra origine, ad esempio una pagina Web o MS Excel, non è supportata e viene mantenuta solo la formattazione parziale.

### Configurare le opzioni Incolla disponibili nella barra degli strumenti dell&#39;editor Rich Text {#configure-paste-options-available-on-the-rte-toolbar}

Nella barra degli strumenti dell’editor Rich Text è possibile fornire agli autori alcune o nessuna di queste tre icone:

* **[!UICONTROL Incolla (Ctrl+V)]**: Può essere preconfigurata per corrispondere a una delle tre modalità Incolla elencate sopra.

* **[!UICONTROL Incolla come testo]**: Fornisce la funzionalità della modalità testo normale.

* **[!UICONTROL Incolla da Word]**: Fornisce la funzionalità della modalità MS Word.

Per configurare l’editor Rich Text in modo da visualizzare le icone richieste, attenetevi alla seguente procedura.

1. Individuate il componente, ad esempio `/apps/<myProject>/components/text`.
1. Individuare il nodo `rtePlugins/edit`. Vedere [attivare un plug-in](#activateplugin) se il nodo non esiste.
1. Creare la proprietà `features` sul nodo `edit` e aggiungere una o più funzioni. Salvate tutte le modifiche.

### Configurare il comportamento dell&#39;icona Incolla (Ctrl+V) e della scelta rapida {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

È possibile pre-configurare il comportamento dell&#39;icona **[!UICONTROL Incolla (Ctrl+V)]** utilizzando la procedura seguente. Questa configurazione definisce anche il comportamento della scelta rapida da tastiera Ctrl+V che verrà utilizzata dagli autori per incollare il contenuto.

La configurazione consente tre tipi di casi di utilizzo:

* Incolla il testo utilizzando l&#39;implementazione Incolla predefinita del browser. Non è un metodo consigliato in quanto potrebbe introdurre markup indesiderati. Configurato utilizzando `browser` di seguito.

* Incolla il contenuto degli Appunti come testo normale. Rimuove tutti gli elementi di stile e formattazione dal contenuto copiato prima di inserire AEM componente. Configurato utilizzando `plaintext` di seguito.

* Incolla il testo, incluse le tabelle, con la formattazione durante la copia da MS Word. La copia e l&#39;incolla del testo da un&#39;altra origine, ad esempio una pagina Web o MS Excel, non è supportata e viene mantenuta solo la formattazione parziale. Configurato utilizzando `wordhtml` di seguito.

1. Nel componente, andate al nodo `<rtePlugins-node>/edit`. Creare i nodi se questi non esistono. Per ulteriori informazioni, vedere [attivare un plug-in](#activateplugin).
1. Nel nodo `edit` create una proprietà utilizzando i seguenti dettagli:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **** Valore: una delle modalità Incolla  `browser`,  `plaintext`o  `wordhtml`.

### Configurare i formati consentiti per incollare il contenuto {#pasteformats}

La modalità Incolla come Microsoft Word (`paste-wordhtml`) può essere configurata ulteriormente in modo da poter definire in modo esplicito quali stili sono consentiti quando si incollano AEM da un altro programma, ad esempio Microsoft Word.

Ad esempio, se è consentito incollare AEM solo formati ed elenchi in grassetto, è possibile filtrare gli altri formati. Questa operazione è denominata filtro Incolla configurabile, che può essere eseguita per entrambi:

* [Testo](#pastemodes)
* [Collegamenti](#linkstyles)

Per i collegamenti è inoltre possibile definire i protocolli accettati automaticamente.

Per configurare quali formati sono consentiti quando si incolla testo in AEM da un altro programma:

1. Nel componente, andate al nodo `<rtePlugins-node>/edit`. Creare i nodi se questi non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Create un nodo sotto il nodo `edit` per contenere le regole di incolla HTML:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Create un nodo in `htmlPasteRules` per contenere i dettagli dei formati di base consentiti:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Per controllare i singoli formati accettati, creare una o più delle seguenti proprietà sul nodo `allowBasics`:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor`  (per collegamenti e ancoraggi denominati)
   * **Nome** `image`

   Tutte le proprietà sono di **Tipo** `Boolean`, quindi nel **Valore** appropriato è possibile selezionare o rimuovere il segno di spunta per abilitare o disabilitare la funzionalità.

   >[!NOTE]
   >
   >Se non viene definito in modo esplicito, viene utilizzato il valore predefinito true e il formato viene accettato.

1. Altri formati possono essere definiti anche utilizzando un intervallo di altre proprietà o nodi, applicati anche al nodo `htmlPasteRules`:

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>allowBlockTags</td>
   <td>Stringa[]</td>
   <td><p>Definisce l'elenco dei tag di blocco consentiti.</p> <p>Alcuni possibili tag di blocco:</p>
    <ul>
     <li>titoli (h1, h2, h3)</li>
     <li>paragrafo p)</li>
     <li>lists (ol, ul)</li>
     <li>tabelle (tabella)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>fallbackBlockTag</td>
   <td>Stringa</td>
   <td><p>Definisce il tag blocco utilizzato per tutti i blocchi con un tag blocco non incluso in allowBlockTags.</p> <p> Nella maggior parte dei casi è sufficiente.</p> </td>
  </tr>
  <tr>
   <td>tabella</td>
   <td>nt:unstructured</td>
   <td><p>Definisce il comportamento durante l'incollaggio delle tabelle.<br /> </p> <p>Questo nodo deve avere la proprietà <code>allow</code> (tipo <code>Boolean</code>) per definire se è consentito incollare tabelle.</p> <p>Se <code>allow</code> è impostato su <code>false</code>, è necessario specificare la proprietà <code>ignoreMode</code> (type<code> String</code>) per definire il modo in cui viene gestito il contenuto della tabella incollato. I valori validi per <code>ignoreMode</code> sono:</p>
    <ul>
     <li><code>remove</code>: Rimuove il contenuto della tabella.</li>
     <li><code>paragraph</code>: Trasforma le celle di tabella in paragrafi.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>elenco</td>
   <td>nt:non strutturato</td>
   <td><p>Definisce il comportamento durante l'incollaggio degli elenchi.<br /> </p> <p>Deve essere presente la proprietà <code>allow</code> (tipo <code>Boolean</code>) per definire se è consentito incollare elenchi.</p> <p>Se <code>allow</code> è impostato su <code>false</code>, è necessario specificare la proprietà <code>ignoreMode</code> (tipo <code>String</code>) per definire la modalità di gestione del contenuto dell'elenco incollato. I valori validi per <code>ignoreMode</code> sono:</p>
    <ul>
     <li><code>remove</code>: Rimuove il contenuto dell'elenco.</li>
     <li><code>paragraph</code>: Trasforma le voci di elenco in paragrafi.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Esempio di una struttura `htmlPasteRules` valida:

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

1. Salvate tutte le modifiche.

## Configurare gli stili di testo {#textstyles}

Gli autori possono applicare Stili per modificare l’aspetto di una parte del testo. Gli stili sono basati sulle classi CSS che avete precedentemente definito nel foglio di stile CSS. Il contenuto formattato è racchiuso tra tag `span` che utilizzano l&#39;attributo `class` per fare riferimento alla classe CSS. Esempio:

`<span class=monospaced>Monospaced Text Here</span>`

Quando il plug-in Stili è attivato per la prima volta, non è disponibile alcun Stili predefinito. L&#39;elenco a comparsa è vuoto. Per fornire agli autori Stili, effettuate le seguenti operazioni:

* Attiva il selettore a discesa Stile.
* Specificare le posizioni dei fogli di stile.
* Specificare i singoli stili che è possibile selezionare dall&#39;elenco a discesa Stile.

Per configurazioni successive (ri)aggiungere altri stili, seguire solo le istruzioni per fare riferimento a un nuovo foglio di stile e specificare gli stili aggiuntivi.

>[!NOTE]
>
>Gli stili possono essere definiti anche per [tabelle o celle di tabella](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). Queste configurazioni richiedono procedure separate.

### Attiva l&#39;elenco a discesa Stile del selettore {#styleselectorlist}

Questa operazione viene eseguita attivando il plug-in per gli stili.

1. Nel componente, andate al nodo `<rtePlugins-node>/styles`. Creare i nodi se questi non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` sul nodo `styles`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

1. Salvate tutte le modifiche.

>[!NOTE]
>
>Una volta abilitato il plug-in Stili, l&#39;elenco a discesa Stile viene visualizzato nella finestra di dialogo di modifica. Tuttavia, l&#39;elenco è vuoto in quanto non è configurato alcun stile.

### Specificare la posizione del foglio di stile {#locationofstylesheet}

Quindi, specificare le posizioni dei fogli di stile a cui si desidera fare riferimento:

1. Individuate il nodo principale del componente di testo, ad esempio `/apps/<myProject>/components/text`.
1. Aggiungete la proprietà `externalStyleSheets` al nodo padre di `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Type** `String[]` (multi-stringa; fate clic su  **** Multiin CRXDE)
   * **Valore(i)** Percorso e nome del file di ogni foglio di stile da includere. Utilizzare i percorsi dell&#39;archivio.

   >[!NOTE]
   >
   >È possibile aggiungere riferimenti a fogli di stile aggiuntivi in qualsiasi momento successivo.

1. Salvate tutte le modifiche.

>[!NOTE]
>
>Quando si utilizza l&#39;editor Rich Text in una finestra di dialogo (interfaccia classica) È possibile specificare fogli di stile ottimizzati per la modifica RTF. A causa di restrizioni tecniche, il contesto CSS viene perso nell&#39;editor, quindi potrebbe essere utile emulare questo contesto per migliorare l&#39;esperienza WYSIWYG.
>
>L’Editor Rich Text utilizza un elemento DOM contenitore con un ID `CQrte` che può essere utilizzato per fornire stili diversi per la visualizzazione e la modifica:
>
>
```
>#CQ td {
> // defines the style for viewing
> }
>```
>
>
```
>#CQrte td {
> // defines the style for editing
> }
>```

### Specificare gli stili disponibili nell&#39;elenco a comparsa {#stylesindropdown}

1. Nella definizione del componente, andate al nodo `<rtePlugins-node>/styles`, come creato in [Abilitazione del selettore a discesa dello stile](#styleselectorlist).
1. Sotto il nodo `styles`, creare un nuovo nodo (detto anche `styles`) per mantenere l&#39;elenco disponibile:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Create un nuovo nodo sotto il nodo `styles` per rappresentare un singolo stile:

   * **Nome**, è possibile specificare il nome, ma deve essere adatto allo stile
   * **Tipo** `nt:unstructured`

1. Aggiungete la proprietà `cssName` a questo nodo per fare riferimento alla classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **** Valore: il nome della classe CSS (senza un &#39;.&#39; precedente.; ad esempio, `cssClass` anziché `.cssClass`)

1. Aggiungete la proprietà `text` allo stesso nodo; definisce il testo visualizzato nella casella di selezione:

   * **Nome** `text`
   * **Tipo** `String`
   * **** ValueDescription dello stile; viene visualizzata nella casella di selezione a discesa Stile.

1. Salva le modifiche.

   Ripetere i passaggi indicati sopra per ogni stile richiesto.

### Configurare l&#39;editor Rich Text per interruzioni di parole ottimali in giapponese {#jpwordwrap}

Gli autori che utilizzano AEM per creare contenuti in lingua giapponese possono applicare uno stile ai caratteri per evitare interruzioni di riga nei casi in cui non è richiesta un&#39;interruzione. Questo permette agli autori di lasciare le frasi rompere nella posizione desiderata. Lo stile di questa funzionalità è basato sulla classe CSS predefinita nel foglio di stile CSS.

>[!NOTE]
>
>Questa funzione richiede almeno AEM 6.5 Service Pack 1.

Per creare lo stile che gli autori possono applicare al testo giapponese, effettuate le seguenti operazioni:

1. Crea un nuovo nodo sotto il nodo stili. Vedere [specificare un nuovo stile](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure

1. Aggiungete la proprietà `cssName` al nodo per fare riferimento alla classe CSS. Questo nome di classe è un nome riservato per la funzione di ritorno a capo automatico in giapponese.
   * Nome: `cssName`
   * Tipo: `String`
   * Valore: `jpn-word-wrap` (senza un `.` precedente)

1. Aggiungere il testo della proprietà allo stesso nodo. Il valore è il nome dello stile che gli autori vedono quando selezionano lo stile.
   * Nome: `text`
*Tipo: 
`String`
   * Valore: `Japanese word-wrap`

1. Creare un foglio di stile e specificarne il percorso. Vedere [specificare la posizione del foglio di stile](#locationofstylesheet). Aggiungere il contenuto seguente al foglio di stile. Modificate il colore di sfondo come desiderato.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Foglio di stile per rendere disponibile agli autori la funzione di ritorno a capo automatico in giapponese](assets/rte_jpwordwrap_stylesheet.jpg)

## Configurare i formati di paragrafo {#paraformats}

Qualsiasi testo creato nell’editor Rich Text viene inserito all’interno di un tag blocco, con il valore predefinito `<p>`. Attivando il plug-in `paraformat`, è possibile specificare tag di blocco aggiuntivi da assegnare ai paragrafi tramite un elenco a discesa di selezione. I formati di paragrafo determinano il tipo di paragrafo assegnando il tag blocco corretto. L&#39;autore può selezionarli e assegnarli mediante il selettore Formato. I tag blocco di esempio includono, tra l&#39;altro, il paragrafo standard &lt;p>, i titoli &lt;h1>, &lt;h2> e così via.

>[!CAUTION]
>
>Questo plug-in non è adatto per contenuti con struttura complessa, come elenchi o tabelle.

>[!NOTE]
>
>Se un tag blocco, ad esempio un tag &lt;hr>, non può essere assegnato a un paragrafo, non è un caso d&#39;uso valido per un plug-in in paraformat.

Quando il plug-in Formati paragrafo è attivato per la prima volta, non sono disponibili formati paragrafo predefiniti. L&#39;elenco a comparsa è vuoto. Per fornire agli autori i formati di paragrafo, effettuate le seguenti operazioni:

* Attiva l&#39;elenco a discesa Formato.
* Specificate i tag di blocco che possono essere selezionati come formati di paragrafo dall&#39;elenco a discesa.

Per configurazioni successive (ri)aggiungete altri formati, seguite solo la parte pertinente delle istruzioni.

### Attiva il selettore a discesa Formato {#formatselectorlist}

Innanzitutto, attivate il plug-in paraformat:

1. Nel componente, andate al nodo `<rtePlugins-node>/paraformat`. Creare i nodi se questi non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` sul nodo `paraformat`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*` (asterisco)

>[!NOTE]
Se il plug-in non è configurato ulteriormente, vengono attivati i seguenti formati predefiniti:
* Paragrafo ( `<p>`)
* Intestazione 1 ( `<h1>`)
* Intestazione 2 ( `<h2>`)
* Intestazione 3 ( `<h3>`)



>[!CAUTION]
Durante la configurazione dei formati di paragrafo dell’editor Rich Text, non rimuovere il tag di paragrafo &lt;p> come opzione di formattazione. Se il tag `<p>` viene rimosso, l&#39;autore del contenuto non può selezionare l&#39;opzione **Formati di paragrafo**, anche se sono configurati altri formati.

### Specificare i formati di paragrafo disponibili {#paraformatsindropdown}

I formati dei paragrafi possono essere resi disponibili per la selezione tramite:

1. Nella definizione del componente, andate al nodo `<rtePlugins-node>/paraformat`, come creato in [Abilitazione del selettore a discesa del formato](#styleselectorlist).
1. Sotto il nodo `paraformat` create un nuovo nodo, per contenere l&#39;elenco dei formati:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crea un nuovo nodo sotto il nodo `formats`, che contiene i dettagli per un singolo formato:

   * **Nome**, è possibile specificare il nome, ma deve essere adatto al formato (ad esempio, myparagraph, myheading1).
   * **Tipo** `nt:unstructured`

1. A questo nodo, aggiungere la proprietà per definire il tag blocco utilizzato:

   * **Nome** `tag`
   * **Tipo** `String`
   * **** ValueIl tag block per il formato; ad esempio: p, h1, h2, ecc.

      Non è necessario inserire le parentesi angolari di delimitazione.

1. Per visualizzare il testo descrittivo nell&#39;elenco a discesa, aggiungere un&#39;altra proprietà allo stesso nodo:

   * **Nome** `description`
   * **Tipo** `String`
   * **** Valore: il testo descrittivo per questo formato; ad esempio, Paragrafo, Intestazione 1, Intestazione 2 e così via. Questo testo viene visualizzato nell&#39;elenco di selezione Formato.

1. Salva le modifiche.

   Ripetere i passaggi per ciascun formato richiesto.

>[!CAUTION]
Se si definiscono formati personalizzati, i formati predefiniti (`<p>`, `<h1>`, `<h2>` e `<h3>`) vengono rimossi. Ricreate il formato `<p>` in quanto è il formato predefinito.

## Configurare i caratteri speciali {#spchar}

In un&#39;installazione AEM standard, quando il plug-in `misctools` è abilitato per caratteri speciali (`specialchars`), è immediatamente disponibile per l&#39;uso una selezione predefinita; ad esempio, i simboli di copyright e marchio.

È possibile configurare l’editor Rich Text per rendere disponibile la propria selezione di caratteri; mediante la definizione di caratteri distinti o di un&#39;intera sequenza.

>[!CAUTION]
Se si aggiungono caratteri speciali, la selezione predefinita viene ignorata. Se necessario, (ri)definite questi caratteri nella vostra selezione.

### Definire un singolo carattere {#definesinglechar}

1. Nel componente, andate al nodo `<rtePlugins-node>/misctools`. Creare i nodi se questi non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` sul nodo `misctools`:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valore** `specialchars`

          (o `String / *` se si applicano tutte le funzioni per questo plug-in)

1. In `misctools` creare un nodo che contenga le configurazioni dei caratteri speciali:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. In `specialCharsConfig` creare un altro nodo che contenga l&#39;elenco dei caratteri:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. In `chars` aggiungere un nuovo nodo per contenere una definizione di singolo carattere:

   * **Nome** è possibile specificare il nome, ma deve riflettere il carattere; ad esempio, metà.
   * **Tipo** `nt:unstructured`

1. A questo nodo aggiungere la seguente proprietà:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Valuta** la rappresentazione HTML del carattere richiesto; ad esempio,  `&189;` per la frazione una metà.

1. Salva le modifiche.

In CRXDE, una volta salvata la proprietà, viene visualizzato il carattere rappresentato. Vedi sotto l&#39;esempio della metà. Ripetete i passaggi indicati sopra per rendere disponibili agli autori altri caratteri speciali.

![In CRXDE, aggiungere un singolo carattere da rendere disponibile nella ](assets/chlimage_1-106.png "barra degli strumenti dell’editor Rich TextIn CRXDE, aggiungere un singolo carattere da rendere disponibile nella barra degli strumenti dell’editor Rich Text")

### Definire un intervallo di caratteri {#definerangechar}

1. Utilizzare i passaggi da 1 a 3 di [Definizione di un singolo carattere](#definesinglechar).
1. In `chars` aggiungere un nuovo nodo per contenere la definizione dell&#39;intervallo di caratteri:

   * **Nome** è possibile specificare il nome, ma deve riflettere l&#39;intervallo di caratteri; ad esempio, matite.
   * **Tipo** `nt:unstructured`

1. Sotto questo nodo (denominato in base all&#39;intervallo di caratteri speciale) aggiungere le due seguenti proprietà:

   * **Nome** `rangeStart`

      **Tipo** `Long`
      **Valore** della  [](https://unicode.org/) presentazione Unicode (decimale) del primo carattere nell&#39;intervallo

   * **Nome** `rangeEnd`

      **Tipo** `Long`
      **Valore** della  [](https://unicode.org/) presentazione Unicode (decimale) dell&#39;ultimo carattere nell&#39;intervallo

1. Salva le modifiche.

   Ad esempio, definire un intervallo compreso tra 9998 e 10000 contiene i seguenti caratteri.

   ![In CRXDE, definire un intervallo di caratteri da rendere disponibili in RTE](assets/chlimage_1-107.png)

   *Figura: In CRXDE, definire un intervallo di caratteri da rendere disponibili in RTE*

   ![I caratteri speciali disponibili nell’editor Rich Text vengono visualizzati dagli autori in una ](assets/rtepencil.png "finestra a comparsaI caratteri speciali disponibili nell’editor Rich Text vengono visualizzati dagli autori in una finestra a comparsa")

## Configurare gli stili di tabella {#tablestyles}

Gli stili vengono in genere applicati al testo, ma su una tabella o su alcune celle di tabella è possibile applicare un set separato di stili. Tali stili sono disponibili per gli autori dalla casella di selezione Stile della finestra di dialogo Proprietà cella o Proprietà tabella. Gli stili sono disponibili quando si modifica una tabella all’interno di un componente Testo (o derivato) e non nel componente Tabella standard.

>[!NOTE]
È possibile definire stili per tabelle e celle solo per l&#39;interfaccia classica.

>[!NOTE]
Copiare e incollare tabelle in o dal componente RTE dipende dal browser. Non è supportato out-of-box per tutti i browser. È possibile ottenere risultati variabili a seconda della struttura della tabella e del browser. Ad esempio, quando copiate e incollate una tabella in un componente RTE in Mozilla Firefox nell’interfaccia classica e Touch, il layout della tabella non viene mantenuto.

1. All&#39;interno del componente, andate al nodo `<rtePlugins-node>/table`. Creare i nodi se questi non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Creare la proprietà `features` sul nodo `table`:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valore** `*`

   >[!NOTE]
   Se non si desidera abilitare tutte le funzionalità della tabella, è possibile creare la proprietà `features` come:
   * **Tipo** `String[]`

   * **Valore** uno o entrambi dei valori seguenti, a seconda delle necessità:
      * `table` consentire la modifica delle proprietà della tabella; inclusi gli stili.
      * `cellprops` per consentire la modifica delle proprietà delle celle, inclusi gli stili.


1. Definire la posizione dei fogli di stile CSS per farvi riferimento. Vedere [Specifica della posizione del foglio di stile](#locationofstylesheet), così come per la definizione degli stili [per il testo](#textstyles). La posizione può essere definita se avete definito altri stili.
1. Sotto il nodo `table` create i seguenti nuovi nodi (come richiesto):

   * Per definire gli stili per l&#39;intera tabella (disponibile in **Proprietà tabella**):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Per definire gli stili per le singole celle (disponibili in **Proprietà cella**):

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Create un nuovo nodo (sotto il nodo `tableStyles` o `cellStyles` a seconda dei casi) per rappresentare un singolo stile:

   * **Nome** è possibile specificare il nome, ma deve riflettere lo stile.
   * **Tipo** `nt:unstructured`

1. In questo nodo creare le proprietà:

   * Definizione dello stile CSS a cui fare riferimento

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Valore** del nome della classe CSS (senza un precedente,  `.`ad esempio,  `cssClass` anziché  `.cssClass`)
   * Definizione di un testo descrittivo da visualizzare nel selettore a discesa

      * **Nome** `text`
      * **Tipo** `String`
      * **Valore** del testo da visualizzare nell&#39;elenco di selezione


1. Salvate tutte le modifiche.

Ripetere i passaggi indicati sopra per ogni stile richiesto.

### Configurare le intestazioni nascoste nelle tabelle per l&#39;accessibilità {#hiddenheader}

A volte è possibile creare tabelle di dati senza testo visivo in un&#39;intestazione di colonna, partendo dal presupposto che lo scopo dell&#39;intestazione sia determinato dalla relazione visiva della colonna con altre colonne. In questo caso, è necessario fornire testo interno nascosto all&#39;interno della cella nella cella di intestazione per consentire agli assistenti vocali e altre tecnologie di assistenza di aiutare i lettori con varie esigenze a comprendere lo scopo della colonna.

Per migliorare l’accessibilità in tali scenari, l’editor Rich Text supporta le celle di intestazione nascoste. Inoltre, fornisce le impostazioni di configurazione relative alle intestazioni nascoste nelle tabelle. Queste impostazioni consentono di applicare stili CSS alle intestazioni nascoste nelle modalità di modifica e anteprima. Per aiutare gli autori a identificare le intestazioni nascoste nella modalità di modifica, includete nel codice i seguenti parametri:

* `hiddenHeaderEditingCSS`: Specifica il nome della classe CSS applicata alla cella di intestazione nascosta quando viene modificato l&#39;editor Rich Text.
* `hiddenHeaderEditingStyle`: Specifica una stringa di stile applicata alla cella di intestazione nascosta quando viene modificato l&#39;editor Rich Text.

Se specificate sia il CSS che la stringa Stile nel codice, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche alla configurazione apportate dalla stringa Stile.

Per aiutare gli autori ad applicare CSS sulle intestazioni nascoste nella modalità di anteprima, potete includere nel codice i seguenti parametri:

* `hiddenHeaderClassName`: Specifica il nome della classe CSS applicata alla cella di intestazione nascosta in modalità di anteprima.
* `hiddenHeaderStyle`: Specifica una stringa di stile applicata alla cella di intestazione nascosta in modalità di anteprima.

Se specificate sia il CSS che la stringa Stile nel codice, la classe CSS ha la precedenza sulla stringa di stile e potrebbe sovrascrivere eventuali modifiche alla configurazione apportate dalla stringa Stile.

## Aggiunta di dizionari per il controllo ortografia {#adddict}

Quando il plug-in per il controllo ortografia è attivato, l&#39;editor Rich Text utilizza i dizionari per ciascuna lingua appropriata. Questi vengono quindi selezionati in base alla lingua del sito Web, ottenendo la proprietà language della struttura ad albero secondaria o estraendo la lingua dall’URL; ad esempio. il ramo `/en/` è controllato come inglese, il ramo `/de/` come tedesco.

>[!NOTE]
Il messaggio `Spell checking failed` viene visualizzato se si tenta di controllare una lingua non installata. I dizionari standard si trovano in `/libs/cq/spellchecker/dictionaries`, insieme ai file Leggimi appropriati. Non modificate i file.

Un&#39;installazione AEM standard include i dizionari per inglese americano (`en_us`) e inglese britannico (`en_gb`). Per aggiungere altri dizionari, procedere come segue.

1. Andate alla pagina [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. Per trovare un dizionario della lingua desiderata, effettuate una delle seguenti operazioni:

   * Cerca dizionario di tua scelta di lingua. Nella pagina del dizionario, individuate il collegamento alla pagina Web dell&#39;origine o dell&#39;autore originale. Individuare i file dizionario per v2.x su una pagina di questo tipo.
   * Cercate i file dizionario v2.x in [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. Scaricate l&#39;archivio con le definizioni dell&#39;ortografia. Estrarre il contenuto dell&#39;archivio nel file system.

   >[!CAUTION]
   Sono supportati solo i dizionari nel formato `MySpell` per OpenOffice.org v2.0.1 o versioni precedenti. Poiché i dizionari ora sono file di archivio, si consiglia di verificare l&#39;archivio dopo il download.

1. Individuate i file .aff e .dic. Mantieni il nome del file in lettere minuscole. Ad esempio, `de_de.aff` e `de_de.dic`.
1. Caricate i file .aff e .dic nella directory archivio in `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
Il controllo ortografia RTE è disponibile su richiesta. Non viene eseguito automaticamente quando si inizia a digitare del testo. Per eseguire il controllo ortografia, fare clic su [!UICONTROL Controllo ortografia] nella barra degli strumenti. L’editor Rich Text controlla l’ortografia delle parole ed evidenzia le parole errate.
Se si incorporano modifiche suggerite dal controllo ortografia, lo stato delle modifiche di testo e delle parole errate non vengono più evidenziati. Per eseguire il controllo ortografia, toccate o fate di nuovo clic sul pulsante Controllo ortografia.

## Configurare la dimensione della cronologia per le azioni di annullamento e ripristino {#undohistory}

L’editor Rich Text consente agli autori di annullare o ripristinare alcune ultime modifiche. Per impostazione predefinita, nella cronologia sono memorizzate 50 modifiche. Puoi configurare questo valore come necessario.

1. All&#39;interno del componente, andate al nodo `<rtePlugins-node>/undo`. Creare questi nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Sul nodo `undo` creare la proprietà:

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valore** del numero di operazioni di annullamento da salvare nella cronologia. Il valore predefinito è 50. Utilizzare `0` per disattivare completamente Annulla/Ripristina.

1. Salva le modifiche.

## Configurare la dimensione della scheda {#tabsize}

Quando il carattere di tabulazione viene premuto all&#39;interno di un testo, viene inserito un numero predefinito di spazi; per impostazione predefinita si tratta di tre spazi unificatori e uno spazio.

Per definire la dimensione della scheda:

1. Nel componente, andate al nodo `<rtePlugins-node>/keys`. Creare i nodi se questi non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Sul nodo `keys` creare la proprietà:

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valore** del numero di caratteri di spazio da utilizzare per la tabulazione.

1. Salva le modifiche.

## Imposta il margine di rientro {#indentmargin}

Quando il rientro è abilitato (impostazione predefinita), puoi definire la dimensione del rientro:

>[!NOTE]
Questa dimensione del rientro è applicata solo ai paragrafi (blocchi) di testo; non incide sul rientro degli elenchi effettivi.

1. All&#39;interno del componente, andate al nodo `<rtePlugins-node>/lists`. Creare questi nodi se non esistono. Per ulteriori dettagli, vedere [attivare un plug-in](#activateplugin).
1. Sul nodo `lists` create il parametro `identSize`:

   * **Nome**: `identSize`
   * **Tipo**: `Long`
   * **Valore**: numero di pixel necessari per il margine di rientro.

## Configurare l&#39;altezza dello spazio modificabile {#editablespace}

>[!NOTE]
Questo è applicabile solo quando si utilizza l’editor Rich Text in una finestra di dialogo (non durante la modifica locale nell’interfaccia classica).

È possibile definire l’altezza dello spazio modificabile visualizzato nella finestra di dialogo del componente:

1. Sul nodo `../items/text` nella definizione della finestra di dialogo per il componente, create una nuova proprietà:

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valore** dell’altezza del quadro di modifica, in pixel.

   >[!NOTE]
   L&#39;altezza della finestra di dialogo non viene modificata.

1. Salva le modifiche.

## Configurare stili e protocolli per i collegamenti {#linkstyles}

Quando aggiungete collegamenti in AEM, potete definire:

* Stili CSS da utilizzare
* I protocolli automaticamente accettati

Per configurare la modalità in cui i collegamenti vengono aggiunti in AEM da un altro programma, definire le regole HTML.

1. Utilizzando CRXDE Lite, individuate il componente di testo per il progetto.
1. Creare un nuovo nodo allo stesso livello di `<rtePlugins-node>`, ovvero creare il nodo sotto il nodo padre di `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   Il nodo `../items/text` ha la proprietà:
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valore** `richtext`

   La posizione del nodo `../items/text` può variare a seconda della struttura della finestra di dialogo; due esempi:
   * `/apps/myProject>/components/text/dialog/items/text`
   * `/apps/<myProject>/components/text/dialog/items/panel/items/text`


1. In `htmlRules`, creare un nuovo nodo.

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. Sotto il nodo `links` definire le proprietà come richiesto:

   * Stile CSS per collegamenti interni:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Valore** del nome della classe CSS (senza un &#39;.&#39; precedente; ad esempio, `cssClass` anziché `.cssClass`)
   * Stile CSS per collegamenti esterni

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Valore** del nome della classe CSS (senza un &#39;.&#39; precedente; ad esempio, `cssClass` anziché `.cssClass`)
   * Array di protocolli **validi**. I protocolli supportati sono `http://`, `https://`, `file://` e `mailto:`.

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valori** uno o più protocolli
   * **defaultProtocol** (proprietà di tipo  **String**): Protocollo da utilizzare se l&#39;utente non ne ha specificato uno in modo esplicito.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valori** uno o più protocolli predefiniti
   * Definizione di come gestire l&#39;attributo target di un collegamento. Crea un nuovo nodo:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

      Sul nodo `targetConfig`: definire le proprietà richieste:

      * Specificate la modalità di destinazione:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valore**:

            * `auto`: indica che è selezionata una destinazione automatica

               (specificata dalla proprietà `targetExternal` per i collegamenti esterni o `targetInternal` per i collegamenti interni).

            * `manual`: non applicabile in questo contesto
            * `blank`: non applicabile in questo contesto
      * Destinazione dei collegamenti interni:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Valore** della destinazione per i collegamenti interni (utilizzare solo quando la modalità è  `auto`)
      * Destinazione per i collegamenti esterni:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Valore** della destinazione per i collegamenti esterni (utilizzato solo quando la modalità è  `auto`).








1. Salvate tutte le modifiche.
