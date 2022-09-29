---
title: Domande frequenti per HTML5 forms
seo-title: Frequently asked questions (FAQ) for HTML5 forms
description: Domande frequenti sul layout, il supporto degli script e l’ambito dei moduli HTML5.
seo-description: Frequently Asked Questions (FAQ) about layout, scripting support, and scope of HTML5 forms.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
feature: Mobile Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
source-git-commit: a90ea57142110ebd11a8a9580c29df1698b8dce1
workflow-type: tm+mt
source-wordcount: '2005'
ht-degree: 0%

---

# Domande frequenti per HTML5 forms{#frequently-asked-questions-faq-for-html-forms}

Sono presenti alcune domande frequenti sul layout, il supporto degli script e l’ambito dei moduli HTML5.

## Layout {#layout}

1. Perché i codici a barre e i campi firma non vengono visualizzati nel modulo?

   Risposta: I campi dei codici a barre e delle firme non sono pertinenti in scenari HTML o mobili. Questi campi vengono visualizzati come area non interattiva. Tuttavia, AEM Forms Designer fornisce un nuovo campo di script della firma che può essere utilizzato al posto del campo firma. È inoltre possibile aggiungere un [widget personalizzato](../../forms/using/custom-widgets.md) per codici a barre e integralo.

1. Il formato RTF è supportato per il campo di testo XFA?

   Risposta: Il campo XFA, che consente l’uso di contenuti avanzati in AEM Forms Designer, non è supportato e viene riprodotto come testo normale senza il supporto per lo stile del testo dall’interfaccia utente. Inoltre, i campi XFA con proprietà comb vengono visualizzati come un campo normale, anche se esistono ancora restrizioni sul numero di caratteri consentiti in base al valore delle cifre comb.

1. Esistono limitazioni nell’utilizzo di sottomoduli ripetibili?

   Risposta: I sottomoduli ripetibili devono avere un conteggio iniziale pari a 1 o più. I sottomoduli ripetibili con un conteggio iniziale pari a zero non sono supportati. È inoltre possibile scegliere di utilizzare un sottomodulo ripetibile e non visualizzarlo al caricamento del modulo. Per ottenere il caso d’uso:

   1. Impostare il conteggio iniziale del sottomodulo ripetibile su 1.

      ![conteggio iniziale](assets/intial-count.png)

   1. Utilizzare l’evento initialize del modulo per nascondere l’istanza primaria del sottomodulo. Ad esempio, il codice seguente nasconde l’istanza primaria del sottomodulo all’avvio del modulo. Inoltre, verifica il tipo di app per garantire che lo script venga eseguito solo sul lato client:

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Aprire lo script per aggiungere un’istanza del sottomodulo per la modifica. Aggiungere il codice come riportato di seguito per aggiungere un’istanza dello script del sottomodulo.

      Il codice seguente controlla l’istanza nascosta del sottomodulo. Se si trova l’istanza nascosta del sottomodulo, eliminare l’istanza nascosta del sottomodulo e inserire una nuova istanza del sottomodulo. Se l’istanza nascosta del sottomodulo non viene trovata, è sufficiente inserire una nuova istanza del sottomodulo.

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. Aprire lo script per rimuovere un&#39;istanza del sottomodulo da modificare. Aggiungere il codice come segue per rimuovere un’istanza dello script del sottomodulo.

      Il codice controlla il conteggio dei sottomoduli. Se il conteggio del sottomodulo ha raggiunto 1, il codice nasconde il sottomodulo invece di eliminare il sottomodulo.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Aprire l&#39;evento di pre-invio del modulo per la modifica. Aggiungi all’evento il seguente script per rimuovere l’istanza nascosta dello script prima della modifica. Impedisce l’invio dei dati del sottomodulo nascosto al momento dell’invio.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. Esistono limitazioni nell’utilizzo di sottomoduli nascosti?

   Risposta: Un sottomodulo nascosto con una gerarchia complessa divisa tra le pagine causa problemi di layout. Una soluzione consiste nel contrassegnare il sottomodulo inizialmente visibile e quindi nasconderlo in uno script di inizializzazione basato su alcuni dati o logici.

1. Perché alcuni testi vengono troncati o visualizzati in modo errato in HTML5?

   Risposta: Se a un elemento di testo Disegno o Didascalia non è stato dato spazio sufficiente per visualizzare il contenuto, il testo viene troncato nel rendering del modulo mobile. Questo troncamento è visibile anche nella vista Progettazione di AEM Forms Designer. Anche se questo troncamento può essere gestito nei PDF, non può essere gestito nei moduli HTML5. Per evitare il problema, lasciare spazio sufficiente a Disegno o Testo didascalia in modo che non venga troncato nella modalità di progettazione di AEM Forms Designer.

1. Osservo problemi di layout relativi a contenuti mancanti o sovrapposti. Qual è la ragione?

   Risposta: Se è presente un elemento Disegno testo o Disegno immagine insieme a un altro elemento sovrapposto nella stessa posizione (ad esempio un rettangolo), il contenuto Disegno testo non è visibile se si trova successivamente nell’ordine del documento (nella vista Gerarchia di AEM Forms Designer). PDF supporta la trasparenza dei livelli, ma HTML/browser non supporta la trasparenza dei livelli.

1. Perché alcuni font visualizzati nel modulo HTML sono diversi da quelli utilizzati durante la progettazione del modulo?

   Risposta: HTML5 Forms non consente l’incorporazione di font (a differenza dei PDF forms in cui i font sono incorporati nel modulo). Affinché il rendering della versione HTML di un modulo sia eseguito come previsto, assicurati che i font siano disponibili nell’archivio CRX (AEM Content Repository) del server AEM Forms e nel computer in cui è installato AEM Designer. Se i font non sono disponibili nel CRX Repository del server AEM Forms o nel percorso in cui è installato AEM Designer, viene eseguito il rendering del modulo con font di fallback.

1. Nei moduli di HTML sono supportati gli attributi vAlign e hAlign?

   Risposta: Sì, gli attributi vAlign e hAlign sono supportati. L&#39;attributo vAlign non è supportato in Internet Explorer e nel campo su più righe.

1. I moduli di HTML5 supportano i caratteri ebraici?

   Risposta: I moduli HTML5 supportano i caratteri ebraici in tutti i browser, ad eccezione di Microsoft Internet Explorer.

1. I moduli di HTML5 hanno limitazioni ai campi numerici?

   Risposta: Sì, HTML5 forms presenta alcune limitazioni. Se il numero di cifre è superiore al conteggio specificato nella clausola illustrazione, i numeri non vengono localizzati e vengono visualizzati in lingua inglese.

1. Perché i moduli HTML hanno dimensioni superiori ai PDF forms?

   Risposta: Per eseguire il rendering di un file XDP in un modulo HTML, sono necessarie molte strutture e oggetti di dati intermedi, ad esempio dom di moduli, dom di dati e dom di layout.

   Per gli PDF forms, Adobe Acrobat dispone di un motore XTG integrato per creare strutture e oggetti di dati intermedi. Acrobat si occupa anche del layout e degli script.

   Per i moduli HTML5, i browser non dispongono di un motore XTG integrato per creare strutture di dati intermedie e oggetti da byte XDP non elaborati. Pertanto, per i moduli HTML5, le strutture intermedie vengono generate sul server e inviate al client. Sul client, i motori di script e layout basati su JavaScript utilizzano queste strutture intermedie.

   La dimensione della struttura intermedia dipende dalle dimensioni dell&#39;XDP originale e dai dati uniti all&#39;XDP.

1. Ci sono limitazioni riguardo all&#39;utilizzo di tabelle nel mio xdp?

   Risposta: Le tabelle complesse causano problemi nel rendering.

   * La sezione (SubformSet) all’interno di una tabella non è supportata.
   * Le righe di intestazione o piè di pagina in alcune tabelle sono contrassegnate per la ripetizione. La suddivisione di tali tabelle su più pagine può causare alcuni problemi.

1. Le tabelle accessibili presentano limitazioni?

   Risposta: Sì, le tabelle accessibili presentano le seguenti limitazioni:

   * Le tabelle e i sottomoduli nidificati all’interno di una tabella non sono supportati.
   * Le intestazioni sono supportate solo per le colonne superiori o sinistre della tabella. Le intestazioni non sono supportate per gli elementi della tabella intermedia. È possibile applicare intestazioni a più intestazioni di riga e colonna, purché siano supportate tutte queste righe e colonne insieme alla riga o alla colonna più in alto a sinistra della tabella.
   * `Rowspan`e `colspan`non è supportato da una posizione casuale all’interno della tabella.

   * Non è possibile aggiungere o rimuovere dinamicamente un&#39;istanza di righe che contengono elementi con valore di estensione di riga maggiore di 1.

1. Qual è l’ordine di lettura della descrizione comandi e della didascalia per gli assistenti vocali?

   Risposta:
   * Se sono presenti sia la didascalia che la descrizione comandi, viene letta l’unica didascalia. Se la didascalia non è disponibile, viene letta la descrizione comandi. È inoltre possibile specificare la precedenza per la lettura in un file XDP utilizzando il form designer
   * Quando passi il cursore su un elemento, viene visualizzata la descrizione comando. Se la descrizione comando non è disponibile, viene visualizzato il testo vocale. Se il testo vocale non è disponibile, viene visualizzato il nome del campo.

1. Quando passi il cursore del mouse su un campo, viene visualizzata una descrizione comandi. Come disattivarlo?

   Risposta: Per disattivare la descrizione comandi al passaggio del mouse, selezionarne una nel pannello di accesso facilitato di Designer.

1. In Designer, un utente può configurare proprietà di aspetto personalizzate dei pulsanti di scelta e delle caselle di controllo. Durante il rendering dei moduli, i moduli di HTML5 tengono conto di tali proprietà di aspetto personalizzate?

   Risposta: I moduli di HTML5 ignorano le proprietà di aspetto personalizzato dei pulsanti di scelta e delle caselle di controllo. I pulsanti di scelta e le caselle di controllo vengono visualizzati in base alle specifiche del browser sottostante.

1. Quando un modulo HTML5 viene aperto in un browser supportato, il bordo dei campi posizionati in modo adiacente non è allineato correttamente oppure i sottomoduli appaiono sovrapposti. Quando lo stesso modulo HTML5 viene visualizzato in anteprima in Forms Designer, i campi e il layout non vengono visualizzati correttamente e i sottomoduli vengono visualizzati nella posizione corretta. Come risolvere il problema?

   Risposta: Quando un sottomodulo è impostato per far fluire il contenuto e il sottomodulo ha un elemento di bordo nascosto, il bordo dei campi posizionati in modo adiacente non è allineato correttamente oppure i sottomoduli appaiono sovrapposti. Per risolvere il problema, è possibile rimuovere o commentare il &lt;border> elementi dell&#39;XDP corrispondente. Ad esempio: &lt;border> è contrassegnato come commento:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. Perché gli assistenti vocali non funzionano correttamente con l’oggetto Campo data/ora?

   Risposta: Gli assistenti vocali non supportano i campi data/ora. Tuttavia, è possibile immettere manualmente data/ora nel campo per consentire all’assistente vocale di leggerlo. Utilizzare il testo della descrizione comando o dell’assistente vocale per istruire l’utente sulla selezione manuale di data/ora per il campo.

1. I moduli di HTML5 supportano i pattern di visualizzazione per i campi mobili?

   Risposta: I moduli di HTML5 non supportano i pattern di visualizzazione per i campi mobili.

1. Qual è il formato del campo Data in HTML5 Forms?

Risposta: Il campo Data accetta il formato ISO AAAA-MM-GG. Se si specifica una data in un altro formato, il campo Data non accetta la formattazione finché l’utente non si sposta dal campo con il tasto di tabulazione.

### Scripting {#scripting}

1. Ci sono limitazioni nell&#39;implementazione JavaScript per HTML Forms?

   Risposta:

   * Il supporto per lo script xfa.connectionSet è limitato. Per connectionSet è supportata solo la chiamata del servizio Web lato server. Per informazioni dettagliate, consulta [Supporto per gli script](/help/forms/using/scripting-support.md).
   * Non è disponibile alcun supporto per $record e $data negli script lato client. Tuttavia, se gli script sono scritti in un blocco formReady e layoutReady, gli script continueranno a funzionare perché questi eventi vengono eseguiti sul lato server.
   * Gli script XFA Draw specifici dell’elemento, come la modifica del testo di disegno (o del testo della didascalia in caso di campi) non sono supportati.

1. L&#39;utilizzo di formCalc presenta limitazioni?

   Risposta: Attualmente è implementato solo un sottoinsieme degli script formCalc. Per informazioni dettagliate, consulta [Supporto per gli script](/help/forms/using/scripting-support.md).

1. Esiste una convenzione di denominazione consigliata e ci sono delle parole chiave riservate da evitare?

   Risposta:
   * In AEM Forms Designer, si consiglia di non iniziare il nome di un oggetto (ad esempio un sottomodulo o un campo di testo) con un carattere di sottolineatura (_). Per utilizzare il carattere di sottolineatura all&#39;inizio del nome, aggiungi un prefisso dopo il carattere di sottolineatura,_&lt;prefix>&lt;objectname>.
   * Tutte le API dei moduli di HTML5 sono parole chiave riservate. Per le API/funzioni personalizzate, utilizza un nome non identico a [API di HTML5 forms](/help/forms/using/scripting-support.md).

1. I moduli di HTML5 supportano i campi mobili?

   Risposta: Sì, HTML5 Forms supporta i campi mobili. Per abilitare i campi mobili, aggiungi la seguente proprietà al profilo di rendering:

   >[!NOTE]
   >
   >Per impostazione predefinita, i campi non sono abilitati per la funzione mobile. È possibile utilizzare Forms Designer per impostare la proprietà mobile dei campi.

   1. Apri CRXde lite e naviga fino al `/content/xfaforms/profiles/default` nodo.
   1. Aggiungi una proprietà `mfDataDependentFloatingField`di tipo String e imposta il valore della proprietà su `true`.
   1. Fai clic su **Salva tutto**. Ora i campi mobili sono abilitati per HTML Forms utilizzando il profilo di rendering aggiornato.

      >[!NOTE]
      >
      >Per abilitare i campi mobili per un modulo specifico senza aggiornare il profilo di rendering, passa la proprietà mfDataDependentFloatingField=true come parametro URL.

1. HTML5 forms esegue lo script di inizializzazione e l’evento form ready più volte?

   Risposta: Sì, gli script di inizializzazione e gli eventi form ready vengono eseguiti più volte, almeno una volta sul server e una volta sul lato client. È consigliabile creare script come eventi initialize o form:ready in base ad alcune logiche aziendali (dati modulo o campo) in modo che l&#39;azione venga eseguita in base allo stato dei dati e all&#39;idempotenti (se i dati sono uguali).

### Progettazione di XDP {#designing-xdp}

1. Esistono parole chiave riservate nei moduli HTML5?

   Risposta: Tutte le API dei moduli di HTML5 sono parole chiave riservate. Per le API/funzioni personalizzate, utilizza un nome non identico a [API di HTML5 forms](/help/forms/using/scripting-support.md). Oltre alle parole chiave riservate, se utilizzi nomi di oggetto che iniziano con un trattino basso (_), è consigliabile aggiungere un prefisso univoco dopo il trattino basso. L’aggiunta di un prefisso consente di evitare eventuali conflitti con le API interne di HTML5 forms. Esempio, `_fpField1`
