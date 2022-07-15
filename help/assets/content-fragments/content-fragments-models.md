---
title: Modelli per frammenti di contenuto
description: Scopri come i modelli per frammenti di contenuto fungono da base per i contenuti headless in AEM e come creare frammenti di contenuto con contenuto strutturato.
feature: Content Fragments
role: User
exl-id: 6fd1fdb2-d1d3-4f97-b119-ecfddcccec9e
source-git-commit: 9b3e30f7523ff86fd1ed1b5fc55ce22b8e9f3429
workflow-type: tm+mt
source-wordcount: '2338'
ht-degree: 8%

---

# Modelli per frammenti di contenuto {#content-fragment-models}

I modelli per frammenti di contenuto in AEM definiscono la struttura del contenuto per il [frammenti di contenuto,](/help/assets/content-fragments/content-fragments.md) funge da base per i contenuti headless.

Per utilizzare i modelli di frammento di contenuto:

1. [Abilita la funzionalità del modello di frammento di contenuto per la tua istanza](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [Crea](#creating-a-content-fragment-model)e [configurare](#defining-your-content-fragment-model), i modelli per frammenti di contenuto
1. [Abilitare i modelli di frammenti di contenuto](#enabling-disabling-a-content-fragment-model) da utilizzare durante la creazione di frammenti di contenuto per la creazione di frammenti di contenuto
1. [Consenti modelli di frammenti di contenuto nelle cartelle Risorse richieste](#allowing-content-fragment-models-assets-folder) configurando **Criteri**.

## Creazione di un modello di frammento di contenuto {#creating-a-content-fragment-model}

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli per frammenti di contenuto**.
1. Passa alla cartella appropriata [configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md).
1. Utilizzo **Crea** per aprire la procedura guidata.

   >[!CAUTION]
   >
   >Se l’[utilizzo di modelli per frammenti di contenuto non è stato abilitato](/help/assets/content-fragments/content-fragments-configuration-browser.md), l’opzione **Crea** non sarà disponibile.

1. Specifica il **Titolo modello**. È inoltre possibile aggiungere **Tag**, **Descrizione**, quindi seleziona **Abilita modello** a [abilita il modello](#enabling-disabling-a-content-fragment-model) se necessario.

   ![titolo e descrizione](assets/cfm-models-02.png)

1. Utilizzo **Crea** per salvare il modello vuoto. Un messaggio indica il successo dell’azione, puoi selezionare **Apri** per modificare immediatamente il modello, oppure **Fine** per tornare alla console.

## Definizione del modello per frammenti di contenuto {#defining-your-content-fragment-model}

Il modello a frammento di contenuto definisce efficacemente la struttura dei frammenti di contenuto risultanti utilizzando una selezione di **[Tipi di dati](#data-types)**. Utilizzando l&#39;editor modelli è possibile aggiungere istanze dei tipi di dati, quindi configurarle per creare i campi richiesti:

>[!CAUTION]
>
>La modifica di un modello di frammento di contenuto esistente può avere un impatto sui frammenti dipendenti.

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello di frammento di contenuto.

1. Apri il modello richiesto per **Modifica**; utilizza l’azione rapida oppure seleziona il modello e quindi l’azione dalla barra degli strumenti.

   Una volta aperto l&#39;editor modelli mostra:

   * sinistra: campi già definiti
   * A destra: **Tipi di dati** disponibili per la creazione di campi, oltre alle **Proprietà** da utilizzare dopo la creazione.

   >[!NOTE]
   >
   >Quando un campo è **obbligatorio**, l’**Etichetta** indicata nel riquadro a sinistra sarà contrassegnata con un asterisco (**&#42;**).

   ![proprietà](assets/cfm-models-03.png)

1. **Aggiunta di un campo**

   * Trascina un tipo di dati obbligatorio nella posizione desiderata per un campo:

      ![tipo di dati a campo](assets/cfm-models-04.png)

   * Una volta aggiunto un campo al modello, il pannello di destra visualizza **Proprietà** che può essere definito per quel particolare tipo di dati. Qui puoi definire ciò che è necessario per quel campo.

      * Molte proprietà sono auto-esplicative, per ulteriori dettagli vedi [Proprietà](#properties).
      * Digitazione di un **Etichetta campo** completerà automaticamente il **Nome proprietà**  - se vuoto, e può essere aggiornato manualmente in seguito.

         >[!CAUTION]
         >
         >Quando si aggiorna manualmente la proprietà **Nome proprietà** per un tipo di dati, tenere presente che i nomi devono contenere solo i caratteri A-Z, a-z, 0-9 e il carattere di sottolineatura &quot;_&quot; come carattere speciale.
         >
         >Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.
      Esempio:

      ![proprietà del campo](assets/cfm-models-05.png)


1. **Rimozione di un campo**

   Seleziona il campo richiesto, quindi tocca o fai clic sull’icona del cestino. Viene richiesto di confermare l’operazione.

   ![rimuovere](assets/cfm-models-06.png)

1. Aggiungi tutti i campi obbligatori e definisci le relative proprietà in base alle esigenze. Esempio:

   ![save](assets/cfm-models-07.png)

1. Seleziona **Salva** per mantenere la definizione.

## Tipi di dati {#data-types}

Per definire il modello è disponibile una selezione di tipi di dati:

* **Testo su riga singola**
   * aggiungere uno o più campi di una singola riga di testo; la lunghezza massima può essere definita
* **Testo su più righe**
   * Area di testo che può essere RTF, testo normale o Markdown
* **Numero**
   * Aggiungi uno o più campi numerici
* **Booleano**
   * Aggiungi una casella di controllo booleana
* **Data e ora**
   * Aggiungere una data e/o un’ora
* **Enumerazione**
   * Aggiungere un set di caselle di controllo, pulsanti di scelta o campi a discesa
* **Tag**
   * Consente agli autori di frammenti di accedere alle aree dei tag e di selezionarle
* **Riferimento contenuto**
   * riferimenti ad altri contenuti di qualsiasi tipo; può essere utilizzato per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Se si fa riferimento a un&#39;immagine, è possibile scegliere di mostrare una miniatura
* **Riferimento frammento**
   * fa riferimento ad altri frammenti di contenuto; può essere utilizzato per [creare contenuto nidificato](#using-references-to-form-nested-content)
   * Il tipo di dati può essere configurato in modo da consentire agli autori di frammenti di:
      * Modificare direttamente il frammento a cui si fa riferimento.
      * Crea un nuovo frammento di contenuto basato sul modello appropriato
* **Oggetto JSON**
   * Consente all’autore del frammento di contenuto di immettere la sintassi JSON negli elementi corrispondenti di un frammento.
      * Per consentire AEM memorizzare JSON diretto che hai copiato/incollato da un altro servizio.
      * Il JSON verrà trasmesso e trasmesso come JSON in GraphQL.
      * Include l’evidenziazione della sintassi JSON, il completamento automatico e l’evidenziazione degli errori nell’editor dei frammenti di contenuto.
* **Segnaposto scheda**
   * Consente l’introduzione di schede da utilizzare per la modifica del contenuto dei frammenti di contenuto.
Questo verrà mostrato come divisore nell&#39;editor modelli, separando le sezioni dell&#39;elenco dei tipi di dati di contenuto. Ogni istanza rappresenta l’inizio di una nuova scheda.
Nell’editor frammenti ogni istanza viene visualizzata come una scheda .

      >[!NOTE]
      >
      >Questo tipo di dati viene utilizzato esclusivamente per la formattazione e viene ignorato dallo schema GraphQL AEM.

## Proprietà {#properties}

Molte proprietà sono auto-esplicative, per alcune proprietà ulteriori dettagli sono qui sotto:


* **Nome proprietà**

   Quando aggiorni manualmente questa proprietà per un tipo di dati, tieni presente che i nomi **deve** contain *only* A-Z, a-z, 0-9 e carattere di sottolineatura &quot;_&quot; come carattere speciale.

   >[!CAUTION]
   >
   >Se i modelli creati in versioni precedenti di AEM contengono caratteri non validi, rimuovi o aggiorna tali caratteri.

* **Rendering come**
Le varie opzioni per la realizzazione/il rendering del campo in un frammento. Spesso questo consente di definire se l’autore visualizza una singola istanza del campo o se può creare più istanze.

* **Etichetta campo**
Inserimento di un 
**Etichetta campo** genererà automaticamente un **Nome proprietà**, che può quindi essere aggiornato manualmente se necessario.

* **Convalida**
La convalida di base è disponibile tramite meccanismi quali **Obbligatorio** proprietà. Alcuni tipi di dati dispongono di campi di convalida aggiuntivi. Vedi [Convalida](#validation) per ulteriori dettagli.

* Per il tipo di dati **Testo su più righe** è possibile definire il **Tipo predefinito** come:

   * **Formato RTF**
   * **Markdown**
   * **Testo normale**

   Se non viene specificato, il valore predefinito **Rich Text** viene utilizzato per questo campo.

   La modifica del **Tipo predefinito** in un modello per frammenti di contenuto avrà effetto solo su un frammento esistente correlato, una volta che il frammento è stato aperto nell’editor e successivamente salvato.

* **Univoco**
Il contenuto (per il campo specifico) deve essere univoco in tutti i frammenti di contenuto creati dal modello corrente.

   Questo viene utilizzato per impedire agli autori di contenuti di ripetere contenuti già aggiunti in un altro frammento dello stesso modello.

   Ad esempio, un **Testo a riga singola** campo denominato `Country` nel modello frammento di contenuto non può essere presente il valore `Japan` in due frammenti di contenuto dipendenti. Viene visualizzato un avviso quando si tenta di eseguire la seconda istanza.

   >[!NOTE]
   >
   >L&#39;unicità è assicurata per radice linguistica.

   >[!NOTE]
   >
   >Le varianti possono avere lo stesso *unico* come varianti dello stesso frammento, ma non lo stesso valore utilizzato in qualsiasi variante di altri frammenti.

* Vedi **[Riferimento contenuto](#content-reference)** per ulteriori dettagli su quel tipo di dati specifico e sulle relative proprietà.

* Vedi **[Riferimento frammento (frammenti nidificati)](#fragment-reference-nested-fragments)** per ulteriori dettagli su quel tipo di dati specifico e sulle relative proprietà.

<!--
* **Translatable**
  Checking the **Translatable** checkbox on a field in the Content Fragment Model editor will:

  * Ensure the field's property name is added to the translation configuration, context `/content/dam/<sites-configuration>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.
-->

## Convalida {#validation}

Diversi tipi di dati includono ora la possibilità di definire requisiti di convalida per l’immissione di contenuto nel frammento risultante:

* **Testo su riga singola**
   * Confronta con un regex predefinito.
* **Numero**
   * Verifica la presenza di valori specifici.
* **Riferimento contenuto**
   * Test per tipi specifici di contenuto.
   * È possibile fare riferimento solo alle risorse di dimensioni file specificate o inferiori.
   * È possibile fare riferimento solo alle immagini entro un intervallo di larghezza e/o altezza predefinito (in pixel).
* **Riferimento frammento**
   * Test di un modello di frammento di contenuto specifico.

## Utilizzo di riferimenti per creare contenuti nidificati {#using-references-to-form-nested-content}

I frammenti di contenuto possono formare contenuto nidificato utilizzando uno dei seguenti tipi di dati:

* **[Riferimento contenuto](#content-reference)**
   * Fornisce un semplice riferimento ad altri contenuti; di qualsiasi tipo.
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

* **[Riferimento frammento](#fragment-reference-nested-fragments)** (Frammenti nidificati)
   * Fa riferimento ad altri frammenti, a seconda dei modelli specifici specificati.
   * Consente di includere/recuperare dati strutturati.

      >[!NOTE]
      >
      >Questo metodo ha un interesse particolare in relazione [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
   * Può essere configurato per uno o più riferimenti (nel frammento risultante).

>[!NOTE]
>
>AEM ha una protezione di ricorrenza per:
>
>* Riferimenti contenuto
   >  Questo impedisce all’utente di aggiungere un riferimento al frammento corrente. Questo può causare una finestra di dialogo vuota del selettore dei riferimenti ai frammenti.
>
>* Riferimenti a frammenti in GraphQL
   >  Se crei una query profonda che restituisce più frammenti di contenuto a cui fanno riferimento l’uno dall’altro, alla prima occorrenza restituirà null.


### Riferimento contenuto {#content-reference}

La funzione Riferimento contenuto consente di eseguire il rendering del contenuto da un’altra origine; ad esempio, frammento di immagine o di contenuto.

Oltre alle proprietà standard è possibile specificare:

* La **Percorso radice** per qualsiasi contenuto di riferimento
* Tipi di contenuto a cui è possibile fare riferimento
* Limitazioni per le dimensioni dei file
* Se si fa riferimento a un&#39;immagine:
   * Mostra miniatura
   * Restrizioni dell&#39;altezza e della larghezza dell&#39;immagine

![Riferimento contenuto](assets/cfm-content-reference.png)

### Riferimento frammento (frammenti nidificati) {#fragment-reference-nested-fragments}

Il riferimento al frammento fa riferimento a uno o più frammenti di contenuto. Questa funzione è particolarmente interessante per il recupero dei contenuti da utilizzare nell’app, in quanto consente di recuperare dati strutturati con più livelli.

Esempio:

* Un modello che definisce i dettagli di un dipendente; tra cui:
   * Un riferimento al modello che definisce il datore di lavoro (azienda)

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
>
>Ciò è di particolare interesse per [Distribuzione di contenuti headless tramite frammenti di contenuto con GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

Oltre alle proprietà standard puoi definire:

* **Rendering come**:

   * **multicampo** - l’autore del frammento può creare più riferimenti singoli o multipli

   * **fragmentreference** : consente all’autore del frammento di selezionare un singolo riferimento a un frammento

* **Tipo di modello**
È possibile selezionare più modelli. Durante la creazione del frammento di contenuto, tutti i frammenti a cui si fa riferimento devono essere stati creati utilizzando questi modelli.

* **Percorso radice**
Specifica un percorso principale per tutti i frammenti a cui viene fatto riferimento.

* **Consenti creazione di frammenti**

   In questo modo l’autore del frammento potrà creare un nuovo frammento basato sul modello appropriato.

   * **fragmentreferencecomposite** - consente all’autore del frammento di creare un composito selezionando più frammenti

   ![Riferimento frammento](assets/cfm-fragment-reference.png)

>[!NOTE]
>
>È in vigore un meccanismo di protezione contro la recidiva. Non consente all’utente di selezionare il frammento di contenuto corrente nel riferimento al frammento. Questo può causare una finestra di dialogo vuota del selettore dei riferimenti ai frammenti.
>
>In GraphQL è inoltre disponibile una protezione di ricorrenza per i riferimenti ai frammenti. Se crei una query approfondita tra due frammenti di contenuto che si riferiscono l’uno all’altro, restituirà null.

## Abilitazione o disabilitazione di un modello di frammento di contenuto {#enabling-disabling-a-content-fragment-model}

Per un controllo completo sull’utilizzo dei modelli di frammenti di contenuto, è possibile impostare uno stato .

### Abilitazione di un modello per frammenti di contenuto {#enabling-a-content-fragment-model}

Una volta creato un modello, questo deve essere abilitato in modo che:

* È disponibile per la selezione durante la creazione di un nuovo frammento di contenuto.
* È possibile fare riferimento a all’interno di un modello di frammento di contenuto.
* È disponibile per GraphQL; quindi lo schema viene generato.

Per abilitare un modello contrassegnato come:

* **Bozza** : mew (mai attivato).
* **Disabilitato** : è stato specificamente disabilitato.

Utilizzi le **Abilita** da:

* La barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Azione rapida corrispondente (passa il mouse sul modello richiesto).

![Abilita bozza o modello disabilitato](assets/cfm-status-enable.png)

### Disabilitazione di un modello di frammento di contenuto {#disabling-a-content-fragment-model}

Un modello può anche essere disabilitato in modo che:

* Il modello non è più disponibile come base per la creazione di *nuovo* Frammenti di contenuto.
* However:
   * Lo schema GraphQL continua a essere generato ed è ancora interrogabile (per evitare di influenzare l’API JSON).
   * È comunque possibile eseguire query su qualsiasi frammento di contenuto basato sul modello e restituirlo dall’endpoint GraphQL.
* Non è più possibile fare riferimento al modello, ma i riferimenti esistenti vengono mantenuti intatti e possono ancora essere interrogati e restituiti dall&#39;endpoint GraphQL.

Per disattivare un modello contrassegnato come **Abilitato** si utilizza **Disattiva** da:

* La barra degli strumenti superiore, quando è selezionato il modello richiesto.
* Azione rapida corrispondente (passa il mouse sul modello richiesto).

![Disattiva un modello abilitato](assets/cfm-status-disable.png)

## Consentire modelli di frammenti di contenuto nella cartella delle risorse {#allowing-content-fragment-models-assets-folder}

Per implementare la governance dei contenuti, puoi configurare **Criteri** nella cartella Risorse per controllare quali modelli di frammenti di contenuto sono consentiti per la creazione di frammenti in tale cartella.

>[!NOTE]
>
>Il meccanismo è simile a [consentire modelli di pagina](/help/sites-authoring/templates.md#allowing-a-template-author) per una pagina e i relativi elementi secondari, nelle proprietà avanzate di una pagina.

Per configurare le **Criteri** per **Modelli di frammenti di contenuto consentiti**:

1. Naviga e apri **Proprietà** per la cartella Risorse richiesta.

1. Apri **Criteri** , dove puoi configurare:

   * **Ereditato da`<folder>`**

      I criteri vengono ereditati automaticamente durante la creazione di nuove cartelle secondarie; il criterio può essere riconfigurato (e l’ereditarietà è interrotta) se le sottocartelle devono consentire modelli diversi dalla cartella principale.

   * **Modelli per frammenti di contenuto consentiti per percorso**

      Possono essere consentiti più modelli.

   * **Modelli di frammenti di contenuto consentiti per tag**

      Possono essere consentiti più modelli.
   ![Criterio modello frammento di contenuto](assets/cfm-model-policy-assets-folder.png)

1. **Salva** eventuali modifiche.

I modelli di frammento di contenuto consentiti per una cartella vengono risolti come segue:
* La **Criteri** per **Modelli di frammenti di contenuto consentiti**.
* Se vuoto, prova a determinare il criterio utilizzando le regole di ereditarietà.
* Se la catena di ereditarietà non fornisce un risultato, consulta la sezione **Cloud Services** configurazione per quella cartella (anche prima direttamente e poi tramite ereditarietà).
* Se nessuno dei risultati di cui sopra fornisce risultati, allora non ci sono modelli consentiti per quella cartella.

## Eliminazione di un modello di frammento di contenuto {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>L’eliminazione di un modello di frammento di contenuto può avere un impatto sui frammenti dipendenti.

Per eliminare un modello di frammento di contenuto:

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello di frammento di contenuto.
1. Seleziona il modello, seguito da **Elimina** dalla barra degli strumenti.

   >[!NOTE]
   >
   >Se si fa riferimento al modello, viene visualizzato un avviso. Agisci in modo appropriato.

## Pubblicazione di un modello di frammento di contenuto {#publishing-a-content-fragment-model}

I modelli di frammento di contenuto devono essere pubblicati quando/prima che vengano pubblicati eventuali frammenti di contenuto dipendenti.

Per pubblicare un modello di frammento di contenuto:

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello di frammento di contenuto.
1. Seleziona il modello, seguito da **Pubblica** dalla barra degli strumenti.
Lo stato di pubblicazione sarà indicato nella console.

   >[!NOTE]
   >
   >Se pubblichi un frammento di contenuto per il quale il modello non è ancora stato pubblicato, un elenco di selezione lo indicherà e il modello verrà pubblicato con il frammento.

## Annullamento della pubblicazione di un modello di frammento di contenuto {#unpublishing-a-content-fragment-model}

I modelli di frammento di contenuto possono essere inediti se non sono indicati da alcun frammento.

Per annullare la pubblicazione di un modello di frammento di contenuto:

1. Passa a **Strumenti**, **Risorse**, quindi apri **Modelli per frammenti di contenuto**.

1. Passa alla cartella contenente il modello di frammento di contenuto.
1. Seleziona il modello, seguito da **Annulla pubblicazione** dalla barra degli strumenti.
Lo stato di pubblicazione sarà indicato nella console.

## Modello frammento di contenuto - Proprietà {#content-fragment-model-properties}

È possibile modificare le **Proprietà** di un modello di frammento di contenuto:

* **Base**
   * **Titolo modello**
   * **Tag**
   * **Descrizione**
   * **Carica immagine**
