---
title: Domande frequenti per moduli HTML5
seo-title: Domande frequenti per moduli HTML5
description: Domande frequenti sul layout, il supporto degli script e l'ambito dei moduli HTML5.
seo-description: Domande frequenti sul layout, il supporto degli script e l'ambito dei moduli HTML5.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1970'
ht-degree: 0%

---


# Domande frequenti per moduli HTML5{#frequently-asked-questions-faq-for-html-forms}

Sono presenti alcune domande frequenti sul layout, il supporto degli script e l&#39;ambito dei moduli HTML5.

## Layout {#layout}

1. Perché i codici a barre e i campi firma non vengono visualizzati nel modulo?

   Risposta: I campi per codici a barre e firme non sono pertinenti negli scenari HTML o mobili. Questi campi vengono visualizzati come area non interattiva. Tuttavia, in Designer AEM Forms è disponibile un nuovo campo di script firma che è possibile utilizzare al posto del campo firma. È inoltre possibile aggiungere un widget [](../../forms/using/custom-widgets.md) personalizzato per i codici a barre e integrarlo.

1. Il formato RTF è supportato per il campo di testo XFA?

   Risposta: Il campo XFA, che consente l&#39;uso di contenuti avanzati in AEM Forms Designer, non è supportato ed è rappresentato come testo normale senza il supporto per lo stile del testo dall&#39;interfaccia utente. Inoltre, i campi XFA con proprietà comb vengono visualizzati come un campo normale, anche se esistono ancora delle limitazioni per il numero di caratteri consentiti in base al valore delle cifre comb.

1. Esistono limitazioni per quanto riguarda l&#39;uso di sottomoduli ripetibili?

   Risposta: I sottomoduli ripetibili devono avere un conteggio iniziale pari a 1 o più. I sottomoduli ripetibili con un conteggio iniziale pari a zero non sono supportati. È inoltre possibile scegliere di utilizzare un sottomodulo ripetibile e non visualizzarlo al caricamento del modulo. Per ottenere il caso di utilizzo:

   1. Impostare il conteggio iniziale del sottomodulo ripetibile su 1.

      ![conteggio iniziale](assets/intial-count.png)

   1. Utilizzare l&#39;evento initialize del modulo per nascondere l&#39;istanza principale del sottomodulo. Ad esempio, il codice seguente nasconde l&#39;istanza principale del sottomodulo all&#39;inizializzazione del modulo. Controlla inoltre il tipo di app per garantire che lo script venga eseguito solo sul lato client:

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Aprire lo script per l&#39;aggiunta di un&#39;istanza del sottomodulo per la modifica. Aggiungere il codice come illustrato di seguito per aggiungere un&#39;istanza dello script Sottomodulo.

      Il codice seguente controlla l&#39;istanza nascosta del sottomodulo. Se l&#39;istanza nascosta del sottomodulo viene trovata, eliminare l&#39;istanza nascosta del sottomodulo e inserire una nuova istanza del sottomodulo. Se l&#39;istanza nascosta del sottomodulo non viene trovata, è sufficiente inserire una nuova istanza del sottomodulo.

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

   1. Aprire lo script per rimuovere un&#39;istanza del sottomodulo per la modifica. Aggiungere il codice come segue per rimuovere un&#39;istanza dello script Sottomodulo.

      Il codice verifica il conteggio dei sottomoduli. Se il conteggio del sottomodulo ha raggiunto 1, il codice nasconde il sottomodulo invece di eliminare il sottomodulo.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Aprire l&#39;evento presubmit del modulo per la modifica. Aggiungete lo script seguente all&#39;evento per rimuovere l&#39;istanza nascosta dello script prima di modificarla. Impedisce l&#39;invio dei dati del sottomodulo nascosto al momento dell&#39;invio.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. Esistono limitazioni per quanto riguarda l&#39;uso dei sottomoduli nascosti?

   Risposta: Un sottomodulo nascosto con una gerarchia complessa divisa tra le pagine causa problemi di layout. Una soluzione consiste nel contrassegnare il sottomodulo inizialmente visibile e nasconderlo in uno script di inizializzazione in base ad alcune logiche o dati.

1. Perché alcuni elementi di testo vengono troncati o visualizzati in modo non corretto in HTML5?

   Risposta: Se a un elemento di testo Disegno o Didascalia non è stato assegnato spazio sufficiente per visualizzare il contenuto, il testo appare troncato nella rappresentazione del modulo mobile. Questo troncamento è visibile anche nella vista Progettazione di AEM Forms Designer. Anche se questo troncamento può essere gestito nei PDF, non può essere gestito nei moduli HTML5. Per evitare il problema, lasciare spazio sufficiente a Disegno o Didascalia testo in modo che non venga troncato nella modalità di progettazione di Progettazione AEM Forms.

1. Osservo problemi di layout relativi a contenuti mancanti o sovrapposti. Qual è la ragione?

   Risposta: Se è presente un elemento Disegna testo o Disegna immagine insieme a un altro elemento sovrapposto nella stessa posizione (ad esempio un rettangolo), il contenuto Disegna testo non è visibile se compare successivamente nell’ordine del documento (nella visualizzazione Gerarchia di Progettazione AEM Forms). PDF supporta la creazione di livelli trasparenti, ma HTML/browser non supportano la sovrapposizione dei livelli trasparenti.

1. Perché alcuni font visualizzati nel modulo HTML sono diversi da quelli utilizzati per la progettazione del modulo?

   Risposta: I moduli HTML5 non incorporano i font (a differenza dei PDF forms in cui i font sono incorporati nel modulo). Affinché il rendering della versione HTML del modulo sia eseguito come previsto, assicurarsi che i font specificati in XDP siano disponibili sul server e sul computer client. Se i font richiesti non sono disponibili sul server, vengono utilizzati i font di fall-back. Inoltre, se si utilizzano font nel modello di modulo non disponibili sul dispositivo client, per il rendering del testo vengono utilizzati i font predefiniti del browser.

1. Gli attributi vAlign e hAlign sono supportati nei moduli HTML?

   Sì, gli attributi vAlign e hAlign sono supportati. L&#39;attributo vAlign non è supportato in Internet Explorer e nel campo su più righe.

1. I moduli HTML5 supportano i caratteri ebraici?

   I moduli HTML5 supportano i caratteri ebraici in tutti i browser, ad eccezione di Microsoft Internet Explorer.

1. I moduli HTML5 presentano limitazioni per i campi numerici?

   Risposta: Sì, i moduli HTML5 presentano alcune limitazioni. Se il numero di cifre è superiore al conteggio specificato nella clausola illustrazione, i numeri non sono localizzati e vengono visualizzati in lingua inglese.

1. Perché i moduli HTML hanno dimensioni maggiori rispetto ai PDF forms

   Per eseguire il rendering di un XDP in un modulo HTML, sono necessari numerosi oggetti e strutture di dati intermedi, ad esempio il DOM del modulo e il DOM dei dati.

   Per i PDF forms, Adobe Acrobat dispone di un motore XTG integrato per creare strutture e oggetti di dati intermedi. Acrobat si occupa anche di layout e script.

   Per i moduli HTML5, i browser non dispongono di un motore XTG integrato per creare strutture di dati intermedie e oggetti da byte XDP non elaborati. Pertanto, per i moduli HTML5, le strutture intermedie vengono generate sul server e inviate al client. Sul client, i motori di script e layout basati su JavaScript utilizzano queste strutture intermedie.

   Le dimensioni della struttura intermedia dipendono dalle dimensioni dell&#39;XDP originale e dai dati uniti all&#39;XDP.

1. Esistono limitazioni per quanto riguarda l&#39;utilizzo di tabelle nel mio xdp?

   Risposta: Tabelle complesse causano problemi durante il rendering.

   * La sezione (SubformSet) all&#39;interno di una tabella non è supportata.
   * Le righe di intestazione o piè di pagina di alcune tabelle sono contrassegnate per la ripetizione. La suddivisione di tali tabelle in più pagine può causare problemi.

1. Le tabelle con accesso facilitato presentano delle limitazioni?

   Risposta: Sì, le tabelle con accesso facilitato presentano le seguenti limitazioni:

   * Le tabelle e i sottomoduli nidificati all&#39;interno di una tabella non sono supportati.
   * Le intestazioni sono supportate solo per la riga superiore o per le colonne sinistre della tabella. Le intestazioni non sono supportate per gli elementi della tabella centrale. È possibile applicare intestazioni a più intestazioni di riga e colonna, purché siano supportate tutte queste righe e colonne insieme alla riga o alla colonna più a sinistra della tabella.
   * `Rowspan`e `colspan`da una posizione casuale all&#39;interno della tabella non è supportata.

   * Non è possibile aggiungere o rimuovere dinamicamente un&#39;istanza di righe contenenti elementi con un valore di estensione di riga maggiore di 1.

1. Qual è l&#39;ordine di lettura della descrizione comandi e della didascalia per gli assistenti vocali?

   * Se sono presenti sia didascalie che descrizioni comandi, viene letta l’unica didascalia. Se la didascalia non è disponibile, la descrizione viene letta. È inoltre possibile specificare la precedenza per la lettura in un file XDP utilizzando la finestra di progettazione dei moduli
   * Quando passate il puntatore del mouse su un elemento, viene visualizzata la descrizione comandi. Se la descrizione comandi non è disponibile, viene visualizzato del testo vocale. Se il testo vocale non è disponibile, viene visualizzato il nome del campo.

1. Quando si passa il puntatore del mouse su un campo, viene visualizzata una descrizione comandi. Come disattivarlo?

   Per disattivare la descrizione comandi al passaggio del mouse, selezionare Nessuna nel pannello di accessibilità di Designer.

1. In Designer, un utente può configurare le proprietà di aspetto personalizzate dei pulsanti di scelta e delle caselle di controllo. Durante il rendering dei moduli, i moduli HTML5 prendono in considerazione tali proprietà di aspetto personalizzate?

   Risposta: I moduli HTML5 ignorano le proprietà di aspetto personalizzate dei pulsanti di scelta e delle caselle di controllo. I pulsanti di scelta e le caselle di controllo vengono visualizzati in base alle specifiche del browser sottostante.

1. Quando un modulo HTML5 viene aperto in un browser supportato, il bordo dei campi inseriti in modo adiacente non viene allineato correttamente oppure i sottomoduli appaiono sovrapposti. Se in Forms Designer è disponibile l&#39;anteprima dello stesso modulo HTML5, i campi e il layout non vengono visualizzati correttamente e i sottomoduli vengono visualizzati nella posizione corretta. Come risolvere il problema?

   Quando un sottomodulo è impostato per far fluire il contenuto e il sottomodulo ha un elemento di bordo nascosto, il bordo dei campi posizionati in modo adiacente non è allineato correttamente oppure i sottomoduli appaiono sovrapposti. Per risolvere il problema, è possibile rimuovere o commentare gli elementi nascosti &lt;border> dall&#39;XDP corrispondente. Ad esempio, il seguente elemento &lt;border> è contrassegnato come commento:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. Perché gli assistenti vocali non funzionano correttamente con l&#39;oggetto campo Data/Ora?

   Gli assistenti vocali non supportano i campi data/ora. Tuttavia, è possibile inserire manualmente la data/ora nel campo per consentire all&#39;assistente vocale di leggerlo. Utilizzare il testo descrittivo o dell&#39;assistente vocale per indicare all&#39;utente di selezionare manualmente la data e l&#39;ora del campo.

1. I moduli HTML5 supportano pattern di visualizzazione per i campi mobili?

   Risposta: I moduli HTML5 non supportano i pattern di visualizzazione per i campi mobili.

### Scripting {#scripting}

1. Esistono limitazioni nell&#39;implementazione JavaScript per i moduli HTML?

   Risposta:

   * Il supporto per lo script xfa.connectionSet è limitato. Per connectionSet, è supportata solo la chiamata lato server del servizio Web. Per informazioni dettagliate, vedere [Supporto](/help/forms/using/scripting-support.md)script.
   * Non è supportato $record e $data negli script sul lato client. Tuttavia, se gli script sono scritti in un blocco formReady e layoutReady, gli script funzionano comunque perché questi eventi vengono eseguiti sul lato server.
   * Gli script XFA Draw specifici dell&#39;elemento, come la modifica del testo Disegno (o del testo della didascalia nel caso di campi) non sono supportati.

1. Esistono limitazioni nell&#39;uso di formCalc?

   Risposta: Attualmente è implementato solo un sottoinsieme degli script formCalc. Per informazioni dettagliate, vedere [Supporto](/help/forms/using/scripting-support.md)script.

1. Esistono convenzioni di denominazione consigliate e sono presenti parole chiave riservate da evitare?

   * In AEM Forms Designer, si consiglia di non iniziare il nome di un oggetto (ad esempio un sottomodulo o un campo di testo) con un carattere di sottolineatura (_). Per utilizzare il carattere di sottolineatura all&#39;inizio del nome, aggiungete un prefisso dopo il carattere di sottolineatura, _&lt;prefisso>&lt;nome oggetto>.
   * Tutte le API dei moduli HTML5 sono parole chiave riservate. Per le API/funzioni personalizzate, utilizzare un nome non identico alle API dei moduli [HTML5](/help/forms/using/scripting-support.md).

1. I moduli HTML5 supportano i campi mobili?

   Sì, i moduli HTML5 supportano i campi mobili. Per abilitare i campi mobili, aggiungi la seguente proprietà al profilo di rendering:

   >[!NOTE]
   >
   >Per impostazione predefinita, i campi non sono attivati per il mobile. È possibile utilizzare Forms Designer per impostare la proprietà mobile dei campi.

   1. Aprite CRXde lite e individuate il `/content/xfaforms/profiles/default` nodo.
   1. Aggiungere una proprietà `mfDataDependentFloatingField`di tipo String e impostare il valore della proprietà su `true`.
   1. Fate clic su **Salva tutto**. Ora i campi mobili sono abilitati per i moduli HTML utilizzando il profilo di rendering aggiornato.

      >[!NOTE]
      >
      >Per abilitare i campi mobili per un modulo specifico senza aggiornare il profilo di rendering, passare la proprietà mfDataDependentFloatingField=true come parametro URL.

1. I moduli HTML5 eseguono più volte lo script di inizializzazione e l’evento form ready?

   Sì, gli script di inizializzazione e gli eventi ready del modulo vengono eseguiti più volte, almeno una volta sul server e una volta sul lato client. È consigliabile scrivere script come eventi initialize o form:ready basati su una logica aziendale (dati modulo o campo) in modo che l&#39;azione venga eseguita in base allo stato dei dati e all&#39;importanza (se i dati sono identici).

### Progettazione di XDP {#designing-xdp}

1. Nei moduli HTML5 sono presenti parole chiave riservate?

   Risposta: Tutte le API dei moduli HTML5 sono parole chiave riservate. Per le API/funzioni personalizzate, utilizzare un nome non identico alle API dei moduli [HTML5](/help/forms/using/scripting-support.md). Oltre alle parole chiave riservate, se si utilizzano nomi di oggetti che iniziano con un carattere di sottolineatura (_), è consigliabile aggiungere un prefisso univoco dopo il carattere di sottolineatura. L&#39;aggiunta di un prefisso consente di evitare possibili conflitti con le API interne dei moduli HTML5. Esempio, `_fpField1`
