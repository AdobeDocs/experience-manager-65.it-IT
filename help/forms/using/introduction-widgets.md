---
title: Framework di aspetto per i moduli adattivi e HTML5
seo-title: Appearance framework for adaptive and HTML5 forms
description: I modelli di modulo di rendering per Forms mobile vengono resi come moduli di HTML5. Questi moduli utilizzano file jQuery, Backbone.js e Underscore.js per l’aspetto e per abilitare gli script.
seo-description: Mobile Forms render Form Templates as HTML5 forms. These forms use jQuery, Backbone.js and Underscore.js files for the appearance and to enable scripting.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
exl-id: 3458471a-9815-463e-8044-68631073863c
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 3%

---

# Framework di aspetto per i moduli adattivi e HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Forms (moduli adattivi e moduli HTML5) utilizza [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) e [Underscore.js](https://underscorejs.org/) librerie per aspetto e script. Nei moduli viene inoltre utilizzato il [Interfaccia utente jQuery](https://jqueryui.com/) **Widget** architettura per tutti gli elementi interattivi (ad esempio campi e pulsanti) del modulo. Questa architettura consente agli sviluppatori di Form di utilizzare un set completo di widget e plug-in jQuery disponibili in Forms. È inoltre possibile implementare una logica specifica per i moduli durante l’acquisizione di dati da utenti quali le restrizioni leadDigits/trailDigits o l’implementazione di clausole illustrazione. Gli sviluppatori di moduli possono creare e utilizzare apparenze personalizzate per migliorare l’esperienza di acquisizione dei dati e renderla più semplice da usare.

Questo articolo è per gli sviluppatori con sufficiente conoscenza dei widget jQuery e jQuery. Fornisce informazioni approfondite sul framework di aspetto e consente agli sviluppatori di creare un aspetto alternativo per un campo modulo.

Il framework di aspetto si basa su varie opzioni, eventi (trigger) e funzioni per acquisire le interazioni dell’utente con il modulo e risponde alle modifiche del modello per informare l’utente finale. Inoltre:

* Il framework fornisce una serie di opzioni per l&#39;aspetto di un campo. Queste opzioni sono coppie chiave-valore e sono suddivise in due categorie: opzioni comuni e opzioni specifiche per il tipo di campo.
* L’aspetto, come parte del contratto, attiva un set di eventi come enter e exit.
* L’aspetto è necessario per implementare un set di funzioni. Alcune delle funzioni sono comuni, altre specifiche delle funzioni del tipo di campo.

## Opzioni comuni {#common-options}

Di seguito sono riportate le opzioni globali impostate. Queste opzioni sono disponibili per ogni campo.

<table>
 <tbody>
  <tr>
   <th>Proprietà </th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>name</td>
   <td>Identificatore utilizzato per specificare questo oggetto o evento nelle espressioni di script. Ad esempio, questa proprietà specifica il nome dell'applicazione host.</td>
  </tr>
  <tr>
   <td>valore</td>
   <td>Valore effettivo del campo. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>Viene visualizzato il valore del campo. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>I Reader di schermo utilizzano questo valore per narrare le informazioni sul campo. Il modulo fornisce il valore ed è possibile ignorarlo.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>Posizione del campo nella sequenza di tabulazione del modulo. Ignorare tabIndex solo se si desidera modificare l'ordine di tabulazione predefinito del modulo.</td>
  </tr>
  <tr>
   <td>role</td>
   <td>Ruolo dell’elemento, ad esempio Intestazione o Tabella.</td>
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
   <td>access</td>
   <td>Controlli utilizzati per accedere al contenuto di un oggetto contenitore, ad esempio un sottomodulo.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>La proprietà para di un elemento XFA al widget.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>La direzione del testo. I valori possibili sono ltr (da sinistra a destra) e rtl (da destra a sinistra).</td>
  </tr>
 </tbody>
</table>

Oltre a queste opzioni, il framework fornisce altre opzioni che variano a seconda del tipo di campo. Di seguito sono elencati i dettagli relativi alle opzioni specifiche dei campi.

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
   <td>Questo evento viene attivato ogni volta che il campo è attivo. Consente l’esecuzione dello script "enter" sul campo. La sintassi per attivare l'evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>Questo evento viene attivato ogni volta che l'utente lascia il campo. Consente al motore di impostare il valore del campo ed eseguire il suo script "exit". La sintassi per attivare l'evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>Questo evento viene attivato per consentire al motore di eseguire lo script "change" scritto sul campo. La sintassi per attivare l'evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>Questo evento viene attivato ogni volta che si fa clic sul campo. consente al motore di eseguire lo script "click" scritto sul campo. La sintassi per attivare l'evento è<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### API implementate da widget {#apis-implemented-by-widget}

Il framework di aspetto richiama alcune funzioni del widget che sono implementate nei widget personalizzati. Il widget deve implementare le seguenti funzioni:

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
   <td>fai clic su: function()</td>
   <td>Attiva il campo e chiama XFA_CLICK_EVENT.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>errorMessage: string </em>rappresenta l’errore<br /> <em>errorType: string ("warning"/"error")</em></p> <p><strong>Nota</strong>: Applicabile solo ai moduli HTML5.</p> </td>
   <td>Invia un messaggio di errore e un tipo di errore al widget. Il widget visualizza l'errore.</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>Nota</strong>: Applicabile solo ai moduli HTML5.</p> </td>
   <td>Chiamata eseguita se gli errori nel campo sono corretti. Il widget nasconde l'errore.</td>
  </tr>
 </tbody>
</table>

## Opzioni specifiche per il tipo di campo {#options-specific-to-type-of-field}

Tutti i widget personalizzati devono essere conformi alle specifiche di cui sopra. Per utilizzare le caratteristiche dei diversi campi, il widget deve conformarsi alle linee guida per quel particolare campo.

### Modifica testo: Campo di testo {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Opzione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>multiline</td>
   <td>True se il campo supporta l'immissione di un carattere di nuova riga, altrimenti false.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Numero massimo di caratteri che è possibile immettere nel campo.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Nota</strong>: Applicabile solo ai moduli HTML5</p> </td>
   <td>Specifica il comportamento del campo di testo quando la larghezza del testo supera la larghezza del widget.</td>
  </tr>
 </tbody>
</table>

### ListaScelta: ElencoA Discesa, CasellaElenco {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>Opzione</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>valore<br /> </td>
   <td>Array di valori selezionati.<br /> </td>
  </tr>
  <tr>
   <td>items<br /> </td>
   <td>Array di oggetti da visualizzare come opzioni. Ogni oggetto contiene due proprietà:<br /> salva: valore da salvare, visualizzare: da visualizzare.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>modificabile</p> <p><strong>Nota</strong>: Applicabile solo ai moduli HTML5.<br /> </p> </td>
   <td>Se il valore è true, la voce di testo personalizzato è abilitata nel widget.<br /> </td>
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
   <td>Aggiunge un elemento all’elenco.</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndice: indice della voce da rimuovere dall'elenco<br /> </em><br /> <br /> </td>
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
| fracDigits | Numero massimo di cifre della frazione consentito nel numero decimale. |
| zero | Rappresentazione stringa pari a zero nelle impostazioni internazionali del campo. |
| decimale | Rappresentazione stringa del decimale nelle impostazioni internazionali del campo. |

### CheckButton: Pulsante di scelta, casella di controllo {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Opzioni</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>Matrice di valori (on/off/neutrale).</p> <p>Si tratta di una matrice di valori per i diversi stati del controlloButton. values[0] è il valore quando lo stato è ON, values[1] è il valore quando lo stato è OFF,<br /> values[2] è il valore quando lo stato è NEUTRAL. La lunghezza della matrice dei valori è uguale al valore dell'opzione state.<br /> </p> </td>
  </tr>
  <tr>
   <td>stati</td>
   <td><p>Numero di stati consentiti. </p> <p>Due per i moduli adattivi (On, Off) e tre per i moduli HTML5 (On, Off, Neutral).</p> </td>
  </tr>
  <tr>
   <td>stadio</td>
   <td><p>Stato corrente dell’elemento.</p> <p>Due per i moduli adattivi (On, Off) e tre per i moduli HTML5 (On, Off, Neutral).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| Opzione | Descrizione |
|---|---|
| giorni | Nome localizzato dei giorni per quel campo. |
| mesi | Nomi di mese localizzati per quel campo. |
| zero | Testo localizzato per il numero 0. |
| clearText | Testo localizzato per cancellare il pulsante. |
