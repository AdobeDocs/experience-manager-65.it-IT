---
title: Domande frequenti per i moduli di HTML5
description: Domande frequenti sul layout, sul supporto degli script e sull’ambito dei moduli HTML5.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 85c9315e-1bc8-44a9-937e-af6fc7cf54d1
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 0%

---


# Domande frequenti per i moduli di HTML5{#frequently-asked-questions-faq-for-html-forms}

Sono presenti alcune domande frequenti sul layout, sul supporto degli script e sull’ambito dei moduli HTML5.

## Layout {#layout}

1. Perché i codici a barre e il campo firma non vengono visualizzati nel modulo?

   Risposta: i campi dei codici a barre e delle firme non sono rilevanti in scenari HTML o mobili. Questi campi vengono visualizzati come area non interattiva. Tuttavia, AEM Forms Designer fornisce un nuovo campo a mano che può essere utilizzato al posto del campo firma. È inoltre possibile aggiungere una [widget personalizzato](../../forms/using/custom-widgets.md) per i codici a barre e integrarlo.

1. Rich Text è supportato per il campo di testo XFA?

   Risposta: il campo XFA, che consente contenuti avanzati in AEM Forms Designer, non è supportato e viene riprodotto come testo normale senza il supporto per la formattazione del testo dall’interfaccia utente. Inoltre, i campi XFA con proprietà comb vengono visualizzati come un campo normale, anche se esistono ancora restrizioni sul numero di caratteri consentiti in base al valore delle cifre comb.

1. Esistono limitazioni relative all&#39;utilizzo di sottomaschere ripetibili?

   Risposta: le sottomaschere ripetibili devono avere un conteggio iniziale pari a 1 o più. Le sottomaschere ripetibili con un conteggio iniziale pari a zero non sono supportate. È inoltre possibile scegliere di utilizzare una sottomaschera ripetibile e di non visualizzarla al caricamento della maschera. Per ottenere il caso d’uso:

   1. Impostare il conteggio iniziale della sottomaschera ripetibile su 1.

      ![primo conteggio](assets/intial-count.png)

   1. Utilizzare l&#39;evento di inizializzazione del modulo per nascondere l&#39;istanza principale del sottomodulo. Ad esempio, il codice seguente nasconde l&#39;istanza principale del sottomodulo all&#39;inizializzazione del modulo. Verifica anche il tipo di app per garantire che lo script venga eseguito solo sul lato client:

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Aprire lo script per l&#39;aggiunta di un&#39;istanza del sottomodulo per la modifica. Aggiungi il codice seguente per aggiungere un’istanza dello script Subform.

      Il codice seguente controlla l’istanza nascosta del sottomodulo. Se viene trovata l&#39;istanza nascosta del sottomodulo, eliminare l&#39;istanza nascosta del sottomodulo e inserire una nuova istanza del sottomodulo. Se l&#39;istanza nascosta del sottomodulo non viene trovata, è sufficiente inserire una nuova istanza del sottomodulo.

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

   1. Aprire lo script per rimuovere un&#39;istanza del sottomodulo per la modifica. Per rimuovere un&#39;istanza dello script Subform, aggiungere il codice nel modo seguente.

      Il codice verifica il numero di sottomaschere. Se il conteggio del sottomodulo ha raggiunto 1, il codice nasconde il sottomodulo invece di eliminarlo.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Apri l’evento di pre-invio del modulo per la modifica. Aggiungi lo script seguente all’evento per rimuovere l’istanza nascosta dello script prima della modifica. Impedisce l’invio di dati del sottomodulo nascosto al momento dell’invio.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. Esistono limitazioni relative all’utilizzo delle sottomaschere nascoste?

   Risposta: una sottomaschera nascosta con gerarchia complessa divisa in più pagine causa problemi di layout. Una soluzione consiste nel contrassegnare il sottomodulo inizialmente visibile e quindi nasconderlo in uno script di inizializzazione in base a una logica o a dati specifici.

1. Perché alcuni testi vengono troncati o non vengono visualizzati correttamente in HTML5?

   Risposta: se a un elemento di testo Disegno o Didascalia non è stato assegnato spazio sufficiente per visualizzare il contenuto, il testo viene troncato nella rappresentazione mobile. Questo troncamento è visibile anche nella vista Progettazione di AEM Forms Designer. Anche se questo troncamento può essere gestito nei PDF, non può essere gestito nei moduli HTML5. Per evitare il problema, fornisci spazio sufficiente per disegnare o sottotitolare il testo in modo che non venga troncato nella modalità progettazione di AEM Forms Designer.

1. Sto osservando problemi di layout relativi a contenuti mancanti o sovrapposti. Qual è il motivo?

   Risposta: se nella stessa posizione è presente un elemento Disegna testo o Disegna immagine insieme a un altro elemento sovrapposto (ad esempio un rettangolo), il contenuto Disegna testo non è visibile se viene visualizzato successivamente nell&#39;ordine del documento (nella visualizzazione Gerarchia di AEM Forms Designer). PDF supporta la creazione di livelli trasparenti, ma HTML/browser non la supportano.

1. Perché alcuni tipi di carattere visualizzati nel modulo HTML sono diversi da quelli utilizzati durante la progettazione del modulo?

   Risposta: HTML5 Forms non consente l&#39;incorporamento di tipi di carattere, a differenza dei PDF forms in cui i tipi di carattere sono incorporati all&#39;interno del modulo. Affinché la versione HTML di un modulo possa essere riprodotta come previsto, assicurati che i font siano disponibili nel repository CRX (AEM Content Repository) del server AEM Forms e nel computer in cui è installato AEM Designer. Quando i font non sono disponibili nel repository CRX del server AEM Forms o nel percorso in cui è installato AEM Designer, il form viene sottoposto a rendering con i font di fallback.

1. Gli attributi vAlign e hAlign sono supportati nei moduli HTML?

   Risposta: Sì, sono supportati gli attributi vAlign e hAlign. L&#39;attributo vAlign non è supportato in Internet Explorer e nel campo multiriga.

1. I moduli di HTML5 supportano i caratteri ebraici?

   Risposta: i moduli di HTML5 supportano caratteri ebraici in tutti i browser eccetto Microsoft Internet Explorer.

1. I moduli HTML5 presentano limitazioni per i campi numerici?

   Risposta: Sì, i moduli HTML5 presentano alcune limitazioni. Se il numero di cifre è maggiore del numero specificato nella clausola picture, i numeri non verranno localizzati e verranno visualizzati nelle impostazioni internazionali della lingua inglese.

1. Perché i moduli HTML sono più grandi dei PDF forms?

   Risposta: per eseguire il rendering di un XDP in un modulo HTML sono necessari numerosi oggetti e strutture di dati intermedie, ad esempio dom del modulo, dom dei dati e dom del layout.

   Per i PDF forms, Adobe Acrobat dispone di un motore XTG integrato per la creazione di strutture di dati e oggetti intermedi. Acrobat si occupa anche di layout e script.

   Per i moduli HTML5, i browser non dispongono di un motore XTG integrato per la creazione di strutture di dati intermedie e di oggetti da byte XDP non elaborati. Pertanto, per i moduli HTML5, sul server vengono generate strutture intermedie che vengono inviate al client. Nel client, il motore di script e layout basato su JavaScript utilizza queste strutture intermedie.

   Le dimensioni della struttura intermedia dipendono dalle dimensioni dell’XDP originale e dai dati uniti a quest’ultimo.

1. Esistono limitazioni relative all’utilizzo delle tabelle nel mio xdp?

   Risposta: le tabelle complesse causano problemi nel rendering.

   * Sezione (SubformSet) all&#39;interno di una tabella non supportata.
   * Le righe di intestazione o piè di pagina in alcune tabelle sono contrassegnate per la ripetizione. La suddivisione di tali tabelle in più pagine può causare alcuni problemi.

1. Le tabelle accessibili hanno limitazioni?

   Risposta: Sì, le tabelle accessibili presentano le seguenti limitazioni:

   * Le tabelle nidificate e le sottomaschere all&#39;interno di una tabella non sono supportate.
   * Le intestazioni sono supportate solo per la riga superiore o le colonne sinistre della tabella. Le intestazioni non sono supportate per gli elementi della tabella intermedia. È possibile applicare intestazioni a più intestazioni di riga e colonna, purché tutte queste righe e colonne siano associate alla riga o alla colonna più a sinistra della tabella.
   * `Rowspan`e `colspan`da una posizione casuale all’interno della tabella non è supportato.

   * Non è possibile aggiungere o rimuovere in modo dinamico un&#39;istanza di righe contenenti elementi con valore rowspan maggiore di 1.

1. Qual è l’ordine di lettura della descrizione comando e della didascalia per gli assistenti vocali?

   Risposta:
   * Se sono presenti sia la didascalia che la descrizione, l&#39;unica didascalia viene letta. Se la didascalia non è disponibile, la descrizione viene letta. È inoltre possibile specificare la precedenza per la lettura in un XDP utilizzando Progettazione moduli
   * Quando passi il cursore su un elemento, viene visualizzata la descrizione comando. Se la descrizione non è disponibile, viene visualizzato il testo vocale. Se il testo del riconoscimento vocale non è disponibile, viene visualizzato il nome del campo.

1. Quando passi il cursore su un campo, viene visualizzata una descrizione comando. Come si disattiva?

   Risposta: per disattivare la descrizione comando al passaggio del mouse, selezionare nessuno nel pannello Accesso facilitato della finestra di progettazione.

1. In Designer, l&#39;utente può configurare le proprietà di aspetto personalizzate dei pulsanti di scelta e delle caselle di controllo. Durante il rendering dei moduli, i moduli HTML5 tengono conto di tali proprietà di aspetto personalizzate?

   Risposta: i moduli di HTML5 ignorano le proprietà di aspetto personalizzate dei pulsanti di scelta e delle caselle di controllo. I pulsanti di scelta e le caselle di controllo vengono visualizzati in base alle specifiche del browser sottostante.

1. Quando un modulo HTML5 viene aperto in un browser supportato, il bordo dei campi adiacenti non è allineato correttamente o le sottomaschere appaiono sovrapposte. Quando lo stesso modulo HTML5 viene visualizzato in anteprima in Forms Designer, i campi e il layout non vengono visualizzati disallineati e le sottomaschere vengono visualizzate nella posizione corretta. Come risolvere il problema?

   Risposta: quando una sottomaschera è impostata sul contenuto di flusso e la sottomaschera ha un elemento di bordo nascosto, il bordo dei campi posizionati adiacenti non è allineato correttamente o le sottomaschere appaiono sovrapposte. Per risolvere il problema, puoi rimuovere o aggiungere un commento al &lt;border> elementi dall&#39;XDP corrispondente. Ad esempio, i seguenti &lt;border> L&#39;elemento è contrassegnato come commento:

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. Perché gli assistenti vocali non funzionano correttamente con l’oggetto campo Data/ora?

   Risposta: gli assistenti vocali non supportano i campi data/ora. Tuttavia, è possibile immettere manualmente data/ora nel campo per consentire allo screen reader di leggerlo. Utilizza il testo della descrizione comando o dell’assistente vocale per istruire l’utente a selezionare manualmente data/ora per il campo.

1. I moduli HTML5 supportano i modelli di visualizzazione per i campi mobili?

   Risposta: i moduli HTML5 non supportano modelli di visualizzazione per campi mobili.

1. Qual è il formato del campo Data in HTML 5 Forms?

Risposta: il campo Data accetta il formato ISO AAAA-MM-GG. Se si specifica una data in un altro formato, il campo Data non accetta la formattazione fino a quando l&#39;utente non esce dal campo.

### Scripting {#scripting}

1. Esistono limitazioni nell’implementazione JavaScript per HTML Forms?

   Risposta:

   * Il supporto per lo script xfa.connectionSet è limitato. Per connectionSet è supportata solo la chiamata lato server del servizio Web. Per informazioni dettagliate, consulta [Supporto script](/help/forms/using/scripting-support.md).
   * Negli script lato client non sono supportati $record e $data. Tuttavia, se gli script vengono scritti in un blocco formReady, layoutReady, gli script funzioneranno comunque perché questi eventi vengono eseguiti sul lato server.
   * Gli script XFA Draw specifici dell’elemento, come la modifica del testo Draw (o del testo della didascalia se sono presenti campi), non sono supportati.

1. Esistono limitazioni nell&#39;utilizzo di formCalc?

   Risposta: è attualmente implementato solo un sottoinsieme degli script formCalc. Per informazioni dettagliate, consulta [Supporto script](/help/forms/using/scripting-support.md).

1. Esiste una convenzione di denominazione consigliata e ci sono parole chiave riservate da evitare?

   Risposta:
   * In AEM Forms Designer, si consiglia di non iniziare il nome di un oggetto (ad esempio una sottomaschera o un campo di testo) con un carattere di sottolineatura (_). Per utilizzare il carattere di sottolineatura all&#39;inizio del nome, aggiungere un prefisso dopo il carattere di sottolineatura,_&lt;prefix>&lt;objectname>.
   * Tutte le API di HTML5 Forms sono parole chiave riservate. Per le API/funzioni personalizzate, utilizza un nome non identico a [API di HTML5 Forms](/help/forms/using/scripting-support.md).

1. I moduli HTML5 supportano i campi mobili?

   Risposta: Sì, HTML5 Forms supporta i campi mobili. Per abilitare i campi mobili, aggiungi la seguente proprietà al profilo di rendering:

   >[!NOTE]
   >
   >Per impostazione predefinita, i campi non sono attivati per la modalità mobile. È possibile utilizzare Forms Designer per impostare la proprietà mobile dei campi.

   1. Apri CRXde lite e naviga su `/content/xfaforms/profiles/default` nodo.
   1. Aggiungi una proprietà `mfDataDependentFloatingField`di tipo String e impostare il valore della proprietà su `true`.
   1. Clic **Salva tutto**. Ora i campi mobili sono abilitati per HTML Forms utilizzando il profilo di rendering aggiornato.

      >[!NOTE]
      >
      >Per abilitare i campi mobili per un modulo specifico senza aggiornare il profilo di rendering, passa la proprietà mfDataDependentFloatingField=true come parametro URL.

1. I moduli HTML5 eseguono più volte lo script di inizializzazione e l’evento di preparazione al modulo?

   Risposta: sì, gli script di inizializzazione e gli eventi di preparazione al modulo vengono eseguiti più volte, almeno una volta sul server e una volta sul lato client. Si consiglia di scrivere script come initialize o form:ready, in base ad alcune regole di business (dati di form o campi), in modo che l&#39;azione venga eseguita in base allo stato dei dati e all&#39;idempotente (se i dati sono uguali).

### Progettazione di XDP {#designing-xdp}

1. Esistono parole chiave riservate nei moduli di HTML5?

   Risposta: tutte le API di HTML5 Forms sono parole chiave riservate. Per le API/funzioni personalizzate, utilizza un nome non identico a [API di HTML5 Forms](/help/forms/using/scripting-support.md). Oltre alle parole chiave riservate, se si utilizzano nomi di oggetto che iniziano con un carattere di sottolineatura (_), si consiglia di aggiungere un prefisso univoco dopo il carattere di sottolineatura. L’aggiunta di un prefisso consente di evitare possibili conflitti con le API interne di HTML5 Forms. Ad esempio `_fpField1`
