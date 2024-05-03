---
title: Framework di aspetto per moduli adattivi e HTML5
description: Mobile Forms esegue il rendering dei modelli di modulo come moduli HTML5. Questi moduli utilizzano i file jQuery, Backbone.js e Underscore.js per l'aspetto e per abilitare gli script.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: 3458471a-9815-463e-8044-68631073863c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 2%

---

# Framework di aspetto per moduli adattivi e HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Utilizzo di Forms (moduli adattivi e moduli HTML5) [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) e [Underscore.js](https://underscorejs.org/) librerie per l&#39;aspetto e gli script. I moduli utilizzano anche [Interfaccia utente jQuery](https://jqueryui.com/) **Widget** architettura per tutti gli elementi interattivi del modulo, ad esempio campi e pulsanti. Questa architettura consente allo sviluppatore di moduli di utilizzare un set completo di widget e plug-in jQuery disponibili in Forms. Puoi anche implementare una logica specifica per il modulo durante l’acquisizione di dati da utenti come le restrizioni leadDigits/trailDigits o l’implementazione di clausole immagine. Gli sviluppatori di moduli possono creare e utilizzare le funzionalità personalizzate per migliorare l’esperienza di acquisizione dei dati e renderla più semplice da usare.

Questo articolo è destinato agli sviluppatori con una conoscenza sufficiente dei widget jQuery e jQuery. Fornisce informazioni approfondite sul framework dell&#39;aspetto e consente agli sviluppatori di creare un aspetto alternativo per un campo modulo.

Il framework dell&#39;aspetto si basa su varie opzioni, eventi (trigger) e funzioni per acquisire le interazioni dell&#39;utente con il modulo e risponde alle modifiche del modello per informare l&#39;utente finale. Inoltre:

* Il framework fornisce una serie di opzioni per l&#39;aspetto di un campo. Queste opzioni sono coppie chiave-valore e suddivise in due categorie: opzioni comuni e opzioni specifiche per il tipo di campo.
* L’aspetto, come parte del contratto, attiva una serie di eventi come l’entrata e l’uscita.
* L&#39;aspetto è necessario per implementare un insieme di funzioni. Alcune delle funzioni sono comuni, mentre altre sono specifiche delle funzioni di tipo campo.

## Opzioni comuni {#common-options}

Di seguito sono riportate le opzioni globali impostate. Queste opzioni sono disponibili per ogni campo.

<table>
 <tbody>
  <tr>
   <th>Proprietà </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>nome</td>
   <td>Identificatore utilizzato per specificare questo oggetto o evento nelle espressioni di script. Ad esempio, questa proprietà specifica il nome dell'applicazione host.</td>
  </tr>
  <tr>
   <td>valore</td>
   <td>Valore effettivo del campo. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>Questo valore del campo viene visualizzato. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>I Reader di schermate utilizzano questo valore per annotare informazioni sul campo. La maschera fornisce il valore e potete ignorarlo.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>Posizione del campo nella sequenza di tabulazione del modulo. Eseguire l'override di tabIndex solo se si desidera modificare l'ordine di tabulazione predefinito del modulo.</td>
  </tr>
  <tr>
   <td>ruolo</td>
   <td>Ruolo dell'elemento, ad esempio Titolo o Tabella.</td>
  </tr>
  <tr>
   <td>altezza</td>
   <td>Altezza del widget. È specificato in pixel. </td>
  </tr>
  <tr>
   <td>larghezza</td>
   <td>Larghezza del widget. È specificato in pixel.</td>
  </tr>
  <tr>
   <td>accesso</td>
   <td>Controlli utilizzati per accedere al contenuto di un oggetto contenitore, ad esempio una sottomaschera.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>La proprietà para di un elemento XFA per il widget.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>Direzione del testo. I valori possibili sono ltr (da sinistra a destra) e rtl (da destra a sinistra).</td>
  </tr>
 </tbody>
</table>

Oltre a queste opzioni, il framework fornisce alcune altre opzioni che variano a seconda del tipo di campo. Di seguito sono elencati i dettagli delle opzioni specifiche per i campi.

### Interazione con il framework dei moduli {#interaction-with-forms-framework}

Per interagire con il framework dei moduli, un widget attiva alcuni eventi per consentire il funzionamento dello script del modulo. Se il widget non genera questi eventi, alcuni degli script scritti nel modulo per quel campo non funzionano.

#### Eventi attivati dal widget {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Evento </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>Questo evento viene attivato ogni volta che il campo è attivo. Consente l’esecuzione dello script "Invio" sul campo. La sintassi per l’attivazione dell’evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>Questo evento viene attivato ogni volta che l’utente lascia il campo. Consente al motore di impostare il valore del campo ed eseguire il relativo script di "uscita". La sintassi per l’attivazione dell’evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>Questo evento viene attivato per consentire al motore di eseguire lo script "change" scritto sul campo. La sintassi per l’attivazione dell’evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>Questo evento viene attivato quando si fa clic sul campo. consente al motore di eseguire lo script "click" scritto sul campo. La sintassi per l’attivazione dell’evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### API implementate da widget {#apis-implemented-by-widget}

Il framework dell’aspetto richiama alcune funzioni del widget che vengono implementate nei widget personalizzati. Il widget deve implementare le seguenti funzioni:

<table>
 <tbody>
  <tr>
   <th>Funzione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>focus: function()</td>
   <td>Mette a fuoco il campo.</td>
  </tr>
  <tr>
   <td>click: function()</td>
   <td>Mette lo stato attivo sul campo e chiama XFA_CLICK_EVENT.</td>
  </tr>
  <tr>
   <td><p>markError:funzione(errorMessage, errorType)<br /> <br /> <em>errorMessage: string </em>che rappresenta l’errore<br /> <em>errorType: string ("warning"/"error")</em></p> <p><strong>Nota</strong>: applicabile solo per i moduli HTML5.</p> </td>
   <td>Invia al widget il messaggio di errore e il tipo di errore. Il widget visualizza l'errore.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>Nota</strong>: applicabile solo per i moduli HTML5.</p> </td>
   <td>Chiamata eseguita se gli errori nel campo vengono corretti. Il widget nasconde l'errore.</td>
  </tr>
 </tbody>
</table>

## Opzioni specifiche per il tipo di campo {#options-specific-to-type-of-field}

Tutti i widget personalizzati devono essere conformi alle specifiche precedenti. Per utilizzare le funzioni di campi diversi, il widget deve essere conforme alle linee guida per quel particolare campo.

### TextEdit: Campo di testo {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Opzione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>multiriga</td>
   <td>True se il campo supporta l'immissione di un carattere di nuova riga, altrimenti false.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Numero massimo di caratteri che possono essere immessi nel campo.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Nota</strong>: applicabile solo per i moduli HTML5</p> </td>
   <td>Specifica il comportamento del campo di testo quando la larghezza del testo supera la larghezza del widget.</td>
  </tr>
 </tbody>
</table>

### ChoiceList: DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>Opzione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>valore<br /> </td>
   <td>Matrice di valori selezionati.<br /> </td>
  </tr>
  <tr>
   <td>elementi<br /> </td>
   <td>Array di oggetti da visualizzare come opzioni. Ogni oggetto contiene due proprietà:<br /> salva: valore da salvare, visualizza: valore da visualizzare.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>modificabile</p> <p><strong>Nota</strong>: applicabile solo per i moduli HTML5.<br /> </p> </td>
   <td>Se il valore è true, l'immissione di testo personalizzato viene abilitata nel widget.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>Matrice di valori da visualizzare.<br /> </td>
  </tr>
  <tr>
   <td>selezione multipla<br /> </td>
   <td>True se sono consentite selezioni multiple, altrimenti false.<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>Funzione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues: oggetto contenente il valore di visualizzazione e salvataggio <br /> {sDisplayVal: &lt;displayvalue&gt;, sSaveVal: &lt;save value=""&gt;}</em></p> </td>
   <td>Aggiunge un elemento all'elenco.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndice: indice dell'elemento da rimuovere dall'elenco<br /> </em><br /> <br /> </td>
   <td>Elimina un'opzione dall'elenco.</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>Cancella tutte le opzioni dall'elenco.</td>
  </tr>
 </tbody>
</table>

### NumericEdit: NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| Opzioni | Descrizione |
|---|---|
| dataType | Stringa che rappresenta il tipo di dati del campo (numero intero/decimale). |
| leadDigits | Numero massimo di cifre iniziali consentito nel numero decimale. |
| fracDigits | Numero massimo di cifre decimali per frazione. |
| zero | Rappresentazione stringa di zero nelle impostazioni internazionali del campo. |
| decimale | Rappresentazione stringa dei decimali nelle impostazioni internazionali del campo. |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Opzioni</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>valori</td>
   <td><p>Array di valori (on/off/neutral).</p> <p>È una matrice di valori per i diversi stati del controllo CheckButton. values[0] è il valore quando lo stato è ON, values[1] è il valore quando lo stato è OFF,<br /> values[2] è il valore quando lo stato è NEUTRAL. La lunghezza della matrice dei valori è uguale al valore dell'opzione di stato.<br /> </p> </td>
  </tr>
  <tr>
   <td>stati</td>
   <td><p>Numero di stati consentiti. </p> <p>Due per i moduli adattivi (On, Off) e tre per i moduli HTML5 (On, Off, Neutral).</p> </td>
  </tr>
  <tr>
   <td>stato</td>
   <td><p>Stato corrente dell'elemento.</p> <p>Due per i moduli adattivi (On, Off) e tre per i moduli HTML5 (On, Off, Neutral).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| Opzione | Descrizione |
|---|---|
| giorni | Nome localizzato dei giorni per quel campo. |
| mesi | Nomi di mese localizzati per il campo. |
| zero | Testo localizzato per il numero 0. |
| clearText | Testo localizzato per il pulsante di cancellazione. |
