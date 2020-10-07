---
title: Introduzione alla creazione di moduli adattivi
seo-title: Introduzione alla creazione di moduli adattivi
description: ' AEM Forms offre un''interfaccia semplice ma potente per la creazione di moduli adattivi. Contiene una serie di componenti e strumenti che è possibile utilizzare per creare moduli.'
seo-description: ' AEM Forms offre un''interfaccia semplice ma potente per la creazione di moduli adattivi. Contiene una serie di componenti e strumenti che è possibile utilizzare per creare moduli.'
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction, author
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
translation-type: tm+mt
source-git-commit: a69e0354b5599ab555df650858f8f3200e21d2b8
workflow-type: tm+mt
source-wordcount: '3145'
ht-degree: 3%

---


# Introduction to authoring adaptive forms {#introduction-to-authoring-adaptive-forms}

## Panoramica {#overview}

I moduli adattivi consentono di creare moduli coinvolgenti, reattivi, dinamici e adattivi.  AEM Forms offre un&#39;interfaccia utente intuitiva e componenti forniti con i prodotti per la creazione e l&#39;utilizzo di moduli adattivi. È possibile scegliere di creare un modulo adattivo basato su un modello di modulo o uno schema oppure senza un modello di modulo. È importante scegliere con attenzione il modello di modulo che non solo si adatta alle proprie esigenze ma che amplia gli investimenti infrastrutturali e le risorse esistenti. Per creare un modulo adattivo è possibile scegliere tra le seguenti opzioni:

* **Uso di un modello dati modulo**
   [L&#39;integrazione](../../forms/using/data-integration.md) dei dati consente di integrare entità e servizi da origini dati diverse in un modello di dati del modulo che è possibile utilizzare per creare moduli adattivi. Scegliere il modello dati del modulo se il modulo adattivo creato prevede il recupero e la scrittura di dati da e verso più origini dati.

* **Utilizzando un modello** di modulo XDP Si tratta di un modello di modulo ideale se si dispone di investimenti in moduli XFA o XDP. Fornisce un modo diretto per convertire i moduli basati su XFA in moduli adattivi. Eventuali regole XFA esistenti vengono conservate nei moduli adattivi associati. I moduli adattivi risultanti supportano i costrutti XFA, ad esempio convalide, eventi, proprietà e pattern.

* **L&#39;utilizzo di uno schema XML Definition (XSD) o di uno schema** XML e JSON rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile associare lo schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema saranno disponibili per l&#39;uso nella scheda Oggetti modello dati del browser Contenuto durante la creazione di moduli adattivi.

* **Se si utilizza uno o più moduli** adattivi per modelli di modulo creati con questa opzione, non viene utilizzato alcun modello di modulo. I dati XML generati da tali moduli hanno una struttura semplice con campi e valori corrispondenti.

Per ulteriori informazioni sulla creazione di un modulo adattivo, vedere [Creazione di un modulo](../../forms/using/creating-adaptive-form.md)adattivo.

## Interfaccia utente per la creazione di moduli adattivi {#adaptive-form-authoring-ui}

L’interfaccia touch per la creazione di moduli adattivi è intuitiva e fornisce:

* Funzionalità di trascinamento
* Componenti per moduli standard
* Archivio integrato per le risorse

Quando si crea un nuovo modulo o si modifica un modulo adattivo esistente, si utilizzano i seguenti elementi dell&#39;interfaccia utente:

* [Barra laterale](#sidebar)
* [Barra degli strumenti della pagina](#page-toolbar)
* [Barra degli strumenti del componente](#component-toolbar)
* [Pagina modulo adattivo](#af-page)

![Interfaccia utente per la creazione di moduli adattivi](assets/formeditor.png)

**A.** Barra laterale **B.** Pagina della barra degli strumenti **C.** Pagina del modulo adattivo

### Barra laterale {#sidebar}

La barra laterale consente di:

* Vedere il contenuto del modulo, ad esempio pannelli, componenti, campi e layout.
* Modificare le proprietà del componente.
* Cercare, visualizzare e utilizzare le risorse nell&#39;archivio AEM Digital Asset Management (DAM).
* Aggiungere componenti al modulo.

![Barra laterale](assets/sidebar-comps.png)

**A.** Browser dei contenuti **B.** Browser delle proprietà **C.** Browser delle risorse **D.** Browser componenti

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

La barra laterale comprende i seguenti browser:

* **Browser** Contenuto Nel browser del contenuto potete visualizzare

   * **Oggetti** modulo Mostra la gerarchia degli oggetti del modulo. L’autore può passare a un componente modulo specifico toccando tale elemento nella struttura ad albero oggetto modulo. L&#39;autore può cercare gli oggetti e riorganizzarli da questa struttura ad albero.

   * **Oggetti**modello dati Consente di visualizzare la gerarchia del modello di modulo.
Consente di trascinare gli elementi del modello di modulo nel modulo adattivo. Gli elementi aggiunti vengono automaticamente convertiti in componenti modulo, mantenendo le proprietà originali. È possibile visualizzare gli oggetti del modello dati quando il modulo utilizza lo schema XML, lo schema JSON o il modello XDP.

* **Browser proprietà**

   Consente di modificare le proprietà di un componente. Le proprietà cambiano in base a un componente. Per visualizzare le proprietà del contenitore di moduli adattivi:

   Selezionate un componente, quindi toccate il livello ![del](assets/field-level.png) campo > Contenitore **[!UICONTROL modulo]** adattivo, quindi toccate ![cmppr](assets/cmppr.png).

* **Browser risorse**

   Segrega contenuti di tipi diversi, come immagini, documenti, pagine, filmati e così via.

* **Browser componenti**

   Include componenti utilizzabili per creare un modulo adattivo. È possibile trascinare i componenti dal modulo adattivo per aggiungere elementi al modulo e configurare gli elementi aggiunti in base ai requisiti. La tabella seguente descrive i componenti elencati nel browser Componenti.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funzionalità</strong></th>
  </tr>
  <tr>
   <td>Blocco Adobe Sign</td>
   <td>Aggiunge un blocco di testo con segnaposto per i campi da compilare durante la firma tramite  Adobe Sign.</td>
  </tr>
  <tr>
   <td>Pulsante</td>
   <td>Aggiunge un pulsante che può essere configurato per eseguire azioni, ad esempio salvare, ripristinare, andare avanti, andare avanti e così via.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Aggiunge la convalida CAPTCHA utilizzando il servizio Google reCAPTCHA. Per informazioni dettagliate, vedere <a href="../../forms/using/captcha-adaptive-forms.md" target="_blank">Uso di CAPTCHA nei moduli</a>adattivi.</td>
  </tr>
  <tr>
   <td>Grafico</td>
   <td>Aggiunge un grafico che può essere utilizzato in moduli adattivi e documenti per la rappresentazione visiva di dati bidimensionali in pannelli e righe di tabella ripetibili.</td>
  </tr>
  <tr>
   <td>Casella di selezione</td>
   <td>Aggiunge una casella di controllo.</td>
  </tr>
  <tr>
   <td>Campo immissione data</td>
   <td>Utilizzare il componente Campo immissione data nel modulo per consentire ai clienti di compilare separatamente il giorno, il mese e l'anno in tre caselle. Potete personalizzare l’aspetto del componente e modificare il formato della data. Ad esempio, puoi consentire ai clienti di inserire le date in formato MM/GG/AAAA o GG/MM/AAAA.</td>
  </tr>
  <tr>
   <td>Selettore data</td>
   <td>Aggiunge un campo calendario per selezionare una data.</td>
  </tr>
  <tr>
   <td>Frammento di documento</td>
   <td>Consente di aggiungere componenti riutilizzabili di una corrispondenza.</td>
  </tr>
  <tr>
   <td>Gruppo di frammenti di documenti</td>
   <td>Consente di aggiungere un gruppo di frammenti di documento correlati che è possibile utilizzare in un modello di lettera come singola unità.</td>
  </tr>
  <tr>
   <td>Elenco a discesa</td>
   <td>Aggiunge un elenco a discesa: selezione singola o multipla</td>
  </tr>
  <tr>
   <td>E-mail</td>
   <td><p>Aggiunge un campo per acquisire l’indirizzo e-mail. Per impostazione predefinita, il componente E-mail convalida gli indirizzi e-mail utilizzando la seguente espressione regolare.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Allegato file</td>
   <td><p>Aggiunge un pulsante che consente agli utenti di sfogliare e allegare i documenti di supporto a un modulo. È possibile allegare più file a un componente Allegato file.</p> <p><strong> Nota: </strong><ul> <li> Il componente non supporta l'associazione di file con nomi di file che iniziano con caratteri (.), contenenti caratteri \ / : * ? " &lt; &gt; | ; % $, o contenente nomi file speciali riservati al sistema operativo Windows come nul, prn, con, lpt o com. </li> <li> Per allegare più file a un componente allegato aperto nel browser Apple Safari, selezionate e allegate i file uno alla volta. Non è possibile selezionare e allegare più file contemporaneamente.</li> <li>Il componente File allegato supporta un set predefinito di formati di file nei moduli adattivi abilitati per  Adobe Sign. Per ulteriori informazioni, vedere Formati <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">di file</a>supportati. </li> </ul></p> </td>
  </tr>
  <tr>
   <td>Elenco allegati file</td>
   <td>Aggiunge un campo in cui sono elencati tutti gli allegati caricati utilizzando il componente File allegato.</td>
  </tr>
  <tr>
   <td>Piè di pagina<br /> </td>
   <td>Aggiunge l’intestazione della pagina che in genere include il logo di una società, il titolo del modulo e il riepilogo.<br /> </td>
  </tr>
  <tr>
   <td>Intestazione</td>
   <td>Aggiunge il piè di pagina di pagina che in genere include informazioni sul copyright e collegamenti ad altre pagine. </td>
  </tr>
  <tr>
   <td>Immagine</td>
   <td>Consente di inserire un’immagine.</td>
  </tr>
  <tr>
   <td>Scelta immagine</td>
   <td>Consente ai clienti di selezionare un’immagine per fornire informazioni. Potete utilizzare le informazioni per fornire servizi personalizzati ai vostri clienti.</td>
  </tr>
  <tr>
   <td>Pulsante Successivo</td>
   <td>Aggiunge un pulsante per passare al pannello successivo di un modulo.</td>
  </tr>
  <tr>
   <td>Casella numerica</td>
   <td>Aggiunge un campo per l'acquisizione dei valori numerici</td>
  </tr>
  <tr>
   <td>Stepper numerico</td>
   <td>Nel modulo è possibile utilizzare la funzione Numeric Stepper per consentire ai clienti di inserire un valore numerico che può aumentare o diminuire in base a un passaggio predefinito.</td>
  </tr>
  <tr>
   <td>Pannello</td>
   <td><p>Aggiunge un pannello o un sottopannello.</p> <p>Potete anche aggiungere un componente pannello dalla barra degli strumenti del pannello principale mediante il pulsante <span class="uicontrol">Aggiungi pannello</code> secondario. Analogamente, potete aggiungere una barra degli strumenti specifica per il pannello utilizzando il pulsante <span class="uicontrol">Aggiungi barra degli strumenti</code> del pannello. Per configurare la posizione della barra degli strumenti del pannello, usate la finestra di dialogo Pannello di modifica.</code></code></p> </td>
  </tr>
  <tr>
   <td>Casella password</td>
   <td>Aggiunge un campo per l’acquisizione di una password.</td>
  </tr>
  <tr>
   <td>Pulsante Precedente</td>
   <td>Aggiunge un pulsante che gli utenti devono usare per tornare alla pagina o al pannello precedente.</td>
  </tr>
  <tr>
   <td>Pulsante di scelta</td>
   <td>Aggiunge pulsanti di scelta.</td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Aggiunge un pulsante per ripristinare i campi del modulo.</td>
  </tr>
  <tr>
   <td>Pulsante di salvataggio</td>
   <td>Aggiunge un pulsante per salvare i dati del modulo.</td>
  </tr>
  <tr>
   <td>Firma scarabocchio</td>
   <td>Aggiunge un campo per l'acquisizione delle firme a script.</td>
  </tr>
  <tr>
   <td>Separatore</td>
   <td>Abilita la separazione visiva dei pannelli nel modulo.</td>
  </tr>
  <tr>
   <td>Passaggio di firma</td>
   <td>Visualizza le informazioni fornite nel modulo e i campi firma che consentono all'utente di verificare e firmare il modulo.</td>
  </tr>
  <tr>
   <td>Testo</td>
   <td>Consente di specificare testo statico.</td>
  </tr>
  <tr>
   <td>Pulsante Invia</td>
   <td>Aggiunge un pulsante di invio per inviare il modulo all'azione di invio configurata.</td>
  </tr>
  <tr>
   <td>Passaggio di riepilogo</td>
   <td>Invia il modulo e visualizza il testo di riepilogo specificato dagli autori dopo l'invio del modulo. </td>
  </tr>
  <tr>
   <td>Scambia</td>
   <td>Aggiunge un interruttore che esegue un'azione di attivazione o disattivazione. Non è possibile aggiungere più di due opzioni nel componente Switch. Poiché un interruttore può avere solo due valori: Attivato o Disattivato, l'opzione obbligatoria non è applicabile. Almeno un valore viene salvato indipendentemente dall'input dell'utente. <br /> </td>
  </tr>
  <tr>
   <td>Tabella</td>
   <td>Aggiunge una tabella che consente di organizzare i dati in righe e colonne. </td>
  </tr>
  <tr>
   <td>Telefono</td>
   <td><p>Aggiunge un campo per acquisire il numero di telefono. Il componente Telefono consente agli autori di configurare uno dei seguenti tipi di numeri di telefono. Ciascun tipo è associato a un'espressione regolare predefinita per la convalida.</p>
    <ul>
     <li>Type International è convalidato da <code>^[+][0-9]{0,14}$</code>.</li>
     <li>Il tipo USPhoneNumber viene convalidato da <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>Il tipo UKPhoneNumber viene convalidato da <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Il tipo Personalizzato non fornisce un pattern di convalida predefinito. Prende il valore dell'ultimo tipo di numero di telefono selezionato. È inoltre possibile specificare un pattern di convalida personalizzato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Condizioni d’uso<br /> </td>
   <td>Aggiunge un campo che gli autori possono utilizzare per specificare i termini e le condizioni che gli utenti possono rivedere prima di compilare il modulo.</td>
  </tr>
  <tr>
   <td>Casella di testo </td>
   <td><p>Aggiunge una casella di testo in cui l'utente può specificare le informazioni richieste. </p> <p>Per impostazione predefinita, il componente Casella di testo accetta solo testo normale. È possibile abilitare un componente Casella di testo per accettare il testo RTF. Un componente Testo RTF offre opzioni per aggiungere intestazioni, modificare gli stili di carattere (grassetto, corsivo, sottolineare i caratteri), creare elenchi ordinati e non ordinati, modificare lo sfondo del testo e il colore del testo e aggiungere collegamenti ipertestuali. Per abilitare il testo RTF per una casella di testo, abilitare l'opzione<strong> Consenti testo</strong> RTF nelle proprietà del componente.</p> </td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Specifica un titolo per il modulo adattivo.</td>
  </tr>
  <tr>
   <td>Passaggio verifica</td>
   <td><p>Aggiunge un segnaposto per visualizzare il modulo compilato per la verifica da parte dell'utente.</p> <p><strong>Nota</strong>: Il modulo adattivo contenente il componente Verifica non supporta gli utenti anonimi. Inoltre, non è consigliabile utilizzare il componente Verifica in un frammento di modulo adattivo.</p> </td>
  </tr>
 </tbody>
</table>

#### Procedure ottimali per l’utilizzo dei componenti {#best-practices}

Di seguito sono riportati alcuni punti chiave e procedure ottimali da tenere presenti quando si utilizzano i componenti per moduli adattivi:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, toccate il componente e toccate ![cmppr](assets/cmppr.png) per aprire le proprietà del componente nel browser Proprietà.
* Un componente è identificato con il nome del relativo elemento. Toccando ![cmppr](assets/cmppr.png), potete modificare il nome del componente modificando il valore del campo Nome **** elemento nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e caratteri di sottolineatura (_). Non sono consentiti altri caratteri speciali e il nome dell&#39;elemento deve iniziare con una lettera.

* È possibile modificare la proprietà Titolo di un componente modulo adattivo in linea nell’editor modulo senza aprire il browser Proprietà finché il titolo è visibile sul modulo. A questo scopo:

   1. Toccate per selezionare un componente con una proprietà **[!UICONTROL Titolo]** e la cui proprietà **[!UICONTROL Nascondi titolo]** è disabilitata.

   1. Toccate ![aem_6_3_edit](assets/aem_6_3_edit.png) per rendere modificabile il titolo.

   1. Modificate il titolo e toccate il tasto Invio oppure toccate un punto qualsiasi all’esterno del componente per salvare le modifiche. Toccate il tasto Esc per annullare le modifiche.

* Alcuni componenti per moduli adattivi come E-mail e Telefono includono pattern di convalida out-of-the-box. Tuttavia, è possibile specificare la convalida personalizzata aggiornando il campo Pattern **** convalida nella scheda Pattern, all&#39;interno delle proprietà del componente. Per ulteriori informazioni sulle convalide predefinite, vedere le descrizioni dei componenti nella tabella precedente.

* I campi modulo adattivi, ad esempio Casella numerica e E-mail, possono essere configurati per includere tipi di input HTML5 specifici. Quando questi campi sono attivi su dispositivi mobili e tablet, la tastiera visualizza in primo piano un alfabeto, numeri e caratteri specifici, comunemente utilizzati per inserire informazioni nei campi. Consente agli utenti di immettere informazioni rapidamente senza dover alternare tra set di caratteri sul tastierino numerico. Per consentire l’input specializzato per un componente, abilitare la casella di controllo **[!UICONTROL Usa numero]** tipo HTML nelle proprietà del componente.

* È possibile abilitare un componente Casella di testo per accettare il testo RTF. Per abilitare il testo RTF per una casella di testo, abilitare la casella di controllo **[!UICONTROL Consenti RTF]** nelle proprietà del componente.

* È possibile abilitare i componenti Casella di testo, E-mail e Telefono per la compilazione automatica dei valori per campi quali nome, indirizzo, carta di credito, telefono ed e-mail dalle informazioni memorizzate nelle impostazioni di compilazione automatica del browser. Per attivare questa funzione, selezionate **[!UICONTROL Abilita riempimento automatico]** nelle proprietà del componente, quindi selezionate un attributo **[!UICONTROL di]** riempimento automatico. Quando un utente compila un modulo adattivo, i valori sono suggeriti dal profilo di compilazione automatica nel browser o in base ai valori precedentemente compilati dall&#39;utente. La compilazione automatica funziona se sono attivate le impostazioni di riempimento automatico nel browser dell&#39;utente.

* Specificare i valori per gli elementi Pulsante di scelta e Casella di controllo nel `{value}={text}` formato nelle proprietà del componente.
* Per impostazione predefinita, il componente File allegato consente a un utente di allegare un solo file. Tuttavia, è possibile configurare le proprietà del componente per supportare più allegati. Inoltre, se un utente allega più file con lo stesso nome file, gli allegati possono causare alcuni problemi. Si consiglia pertanto di associare un identificatore univoco per ciascun allegato inviato all&#39;invio del modulo. A questo scopo:

   1. Nel server AEM Forms , accedete a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web.
   1. Individuate e toccate **[!UICONTROL Adattivo Forms Configuration Service]**.
   1. Nella finestra di dialogo Servizio di configurazione Forms adattivo, abilita **[!UICONTROL Rendi univoci]** i nomi dei file. Per impostazione predefinita, è disattivata.

* Per consentire agli utenti di allegare un PDF utilizzando il browser Safari, assicurarsi che **application/pdf** venga aggiunto alla proprietà Tipi di file supportati del componente Allegato file. I moduli adattivi creati con  versione precedente di AEM Forms possono contenere **.pdf** invece di **application/pdf** nella proprietà Tipi di file supportati.

Per ulteriori procedure ottimali sui moduli adattivi, vedere Procedure [consigliate per l&#39;utilizzo dei moduli](/help/forms/using/adaptive-forms-best-practices.md)adattivi.

>[!NOTE]
>
>I componenti per moduli adattivi non supportano i linguaggi RTL (Right to Left). Ad esempio, ebraico.

### Barra degli strumenti della pagina {#page-toolbar}

La barra degli strumenti della pagina nella parte superiore contiene opzioni che consentono di visualizzare l&#39;anteprima del modulo, modificare le proprietà del modulo e il layout del modulo. È possibile visualizzare l&#39;anteprima del modulo al momento della creazione e apportare le modifiche necessarie. Nella barra degli strumenti della pagina sono disponibili:

* **Attiva/disattiva pannello** laterale ![o pannello](assets/toggle-side-panel.png)laterale: Consente di mostrare o nascondere la barra laterale.

* **Informazioni** pagina ![tema-opzioni](assets/theme-options.png): Consente di visualizzare le proprietà della pagina, pubblicare/annullare la pubblicazione di un modulo, avviare un flusso di lavoro del modulo e aprire il modulo nell’interfaccia classica.

* **Emulatore** ![righello](assets/ruler.png): Consente di emulare l&#39;aspetto del modulo per dimensioni di visualizzazione diverse, ad esempio tablet e telefoni.

* **Modifica**: Consente di selezionare altre modalità, ad esempio: **[!UICONTROL Modifica]**, **[!UICONTROL Stile]**, **[!UICONTROL Sviluppatore]** e **[!UICONTROL Progettazione]**.

   * **Modifica**: Consente di modificare le proprietà del modulo e dei suoi componenti. Ad esempio, aggiungere un componente, rilasciare un’immagine e specificare campi obbligatori.
   * **Stile**: Consente di formattare l&#39;aspetto dei componenti del modulo. Ad esempio, in modalità stile, potete selezionare un pannello e specificarne il colore di sfondo.

   * **Sviluppatore**: Consente a uno sviluppatore di:

      * Scopri di quali moduli sono composti.
      * Eseguire il debug di ciò che sta accadendo dove e quando, che a sua volta aiuta a risolvere i problemi.
   * **Progettazione**. Consente di abilitare o disabilitare componenti personalizzati, o componenti out-of-the-box non elencati nella barra laterale.


* **Anteprima**: Consente di visualizzare un&#39;anteprima dell&#39;aspetto del modulo al momento della pubblicazione.

### Component toolbar {#component-toolbar}

![Barra degli strumenti del componente nell’interfaccia touch](assets/component-toolbar.png)

Quando selezionate un componente, compare una barra degli strumenti che consente di utilizzarlo. Sono disponibili opzioni per tagliare, incollare, spostare e specificare le proprietà dei componenti. Le opzioni disponibili sono:

A.**Configure**: Toccando **[!UICONTROL Configura]**, le proprietà del componente sono visibili nella barra laterale. La configurazione di queste proprietà consente di personalizzare l&#39;esperienza di acquisizione dei dati. Potete modificare il nome dell’elemento del componente, specificare il testo dell’etichetta nel campo Titolo del componente. Il nome dell’elemento consente di acquisire i valori immessi dall’utente mediante il componente. Nelle proprietà del componente, potete specificare il comportamento del componente e gestire l’input dell’utente. Configurare le proprietà nella barra laterale per acquisire i dati utente e utilizzarli per un’ulteriore elaborazione. Le proprietà per il contenitore di moduli adattivi consentono di specificare librerie client, layout, temi, impostazioni del documento di registrazione, impostazioni di salvataggio, impostazioni di invio e impostazioni di metadati.

B.**Copia**: È possibile utilizzare l&#39;opzione Copia per copiare un componente e incollarlo in altre aree del modulo. Quando incollate un componente, il componente incollato riceve un nuovo nome di elemento ma mantiene le proprietà del componente copiato.

C.**Taglia**: È possibile utilizzare l’opzione Taglia per spostare un componente da una posizione all’altra nel modulo adattivo.

D. **Elimina**: Consente di eliminare il componente dal modulo.

E. **Inserisci**: Consente di inserire un componente sopra il componente selezionato.

F. **Incolla**: Consente di incollare il componente tagliato o copiato utilizzando le opzioni descritte sopra.

G. **Modifica regole**: Consente di aprire l&#39;editor delle regole. Per ulteriori informazioni, vedere Editor [](../../forms/using/rule-editor.md)regole.

H. **Gruppo**: Consente di selezionare più componenti per tagliare, copiare o incollare più componenti contemporaneamente.

I. **Elemento padre**: Consente di selezionare l’elemento padre di un componente. Ad esempio, un campo di testo si trova all&#39;interno di una sottosezione, che risiede in una sezione. La sezione si trova nel pannello principale della guida e il contenitore di modulo adattivo è l&#39;elemento principale di un pannello principale della guida. Per un componente, è possibile visualizzare tutte le opzioni con i bordi inferiori ordinati della gerarchia.

Ad esempio, toccando **[!UICONTROL Elemento padre]** per una casella di testo, è possibile visualizzare:

* Sottosezione
* Sezione
* guideRootPanel
* Contenitore di moduli adattivi

J. **Altri**: Offre ulteriori opzioni per l’utilizzo del componente selezionato.

* Visualizza espressione SOM
* Salvare un pannello come frammento (solo per i pannelli)
* Aggiungere un pannello secondario (solo per i pannelli)
* Barra degli strumenti del pannello Aggiungi (solo per i pannelli)
* Sostituisci (non per i pannelli)

### Adaptive form page {#af-page}

La pagina del modulo adattivo è il modulo effettivo. È come qualsiasi altra pagina WCM modellata come il componente WCM `cq:Page` . L&#39;immagine seguente mostra la struttura del contenuto di un tipico modulo adattivo.

![Struttura del contenuto di una pagina WCM modulo adattivo](assets/afstructure.png)

La struttura del contenuto contiene in genere i seguenti componenti primari:

* **guideContainer**: Livello principale di un modulo adattivo, contrassegnato come **[!UICONTROL Inizio del modulo]** adattivo nell’interfaccia utente del modulo adattivo. In questo componente potete specificare:

   * *Layout mobile del modulo* adattivo: Definisce l’aspetto del modulo sui dispositivi mobili.
   * *Pagina* di ringraziamento: Definisce la pagina in cui l&#39;utente viene reindirizzato dopo l&#39;invio del modulo.
   * *Invia azione*: Definisce la modalità di elaborazione del modulo sul server dopo l&#39;invio del modulo da parte dell&#39;utente.
   * *Attribuzione stile*: Specifica il percorso del file CSS utilizzato per personalizzare l&#39;aspetto del modulo.

* **rootPanel:** Pannello principale di un modulo adattivo. Può contenere sottopannelli sotto il nodo degli elementi. A ciascun pannello, incluso il pannello principale, può essere associato un layout. Il layout del pannello determina il layout del modulo. Ad esempio, nel layout Accordion, i relativi elementi sono disposti come passi Accordion.

* **barra degli strumenti:** A un contenitore di moduli adattivi è associata una barra degli strumenti globale, globale per il modulo. Questa barra degli strumenti può essere aggiunta utilizzando l’azione **[!UICONTROL Aggiungi barra degli strumenti]** nella barra di modifica, che consente agli autori di aggiungere azioni quali Invia, Salva, Ripristina e così via.

* **assets:** Questo nodo contiene informazioni aggiuntive utilizzate per la creazione di moduli. Ad esempio, dettagli relativi al modello di modulo, alla localizzazione e così via).

