---
title: Introduzione alla creazione di moduli adattivi
seo-title: Introduzione alla creazione di moduli adattivi
description: AEM Forms offre un’interfaccia facile da usare ma potente per la creazione di moduli adattivi. Fornisce una serie di componenti e strumenti che è possibile utilizzare per creare i moduli.
seo-description: AEM Forms offre un’interfaccia facile da usare ma potente per la creazione di moduli adattivi. Fornisce una serie di componenti e strumenti che è possibile utilizzare per creare i moduli.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction, author
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
feature: Moduli adattivi
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3171'
ht-degree: 3%

---


# Introduzione alla creazione di moduli adattivi {#introduction-to-authoring-adaptive-forms}

## Panoramica {#overview}

I moduli adattivi consentono di creare moduli coinvolgenti, reattivi, dinamici e adattivi. AEM Forms offre un’interfaccia utente intuitiva e componenti predefiniti per la creazione e l’utilizzo di moduli adattivi. È possibile scegliere di creare un modulo adattivo basato su un modello di modulo o schema o senza un modello di modulo. È importante scegliere con attenzione il modello di modulo che non solo si adatta alle proprie esigenze ma estende gli investimenti e le risorse infrastrutturali esistenti. Per creare un modulo adattivo è possibile scegliere tra le seguenti opzioni:

* **Uso di un modello dati modulo**
   [L’](../../forms/using/data-integration.md) integrazione dei dati consente di integrare entità e servizi da diverse origini dati in un modello di dati modulo che è possibile utilizzare per creare moduli adattivi. Scegli il modello dati del modulo se il modulo adattivo che stai creando prevede il recupero e la scrittura di dati da e verso più origini dati.

* **Utilizzo di un**
modello di modulo XDP È un modello di modulo ideale se si dispone di investimenti in moduli XFA o XDP. Fornisce un modo diretto per convertire i moduli basati su XFA in moduli adattivi. Eventuali regole XFA esistenti vengono mantenute nei moduli adattivi associati. I moduli adattivi risultanti supportano i costrutti XFA, ad esempio convalide, eventi, proprietà e pattern.

* **L’utilizzo di una definizione di schema XML (XSD) o di uno schema JSON**
SchemaXML e di schemi JSON rappresenta la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile associare lo schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema saranno disponibili per l’uso nella scheda Oggetti modello dati del browser Contenuto durante la creazione di moduli adattivi.

* **I moduli adattivi creati con questa opzione non utilizzano modelli di modulo, né sono privi di un**
modello di modulo. I dati XML generati da tali moduli hanno una struttura piatta con campi e valori corrispondenti.

Per ulteriori informazioni sulla creazione di un modulo adattivo, vedere [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).

## Interfaccia utente per la creazione di moduli adattivi {#adaptive-form-authoring-ui}

L’interfaccia touch per la creazione di moduli adattivi è intuitiva e fornisce:

* Funzionalità di trascinamento della selezione
* Componenti standard per moduli
* Archivio integrato per le risorse

Quando crei un nuovo modulo adattivo o ne modifichi uno esistente, puoi utilizzare i seguenti elementi dell’interfaccia utente:

* [Barra laterale](#sidebar)
* [Barra degli strumenti della pagina](#page-toolbar)
* [Barra degli strumenti del componente](#component-toolbar)
* [Pagina del modulo adattivo](#af-page)

![Interfaccia utente per la creazione di moduli adattivi](assets/formeditor.png)

**A.** Barra laterale  **B.** Barra degli strumenti della pagina  **C.** Pagina del modulo adattivo

### Barra laterale {#sidebar}

La barra laterale consente di:

* Vedere il contenuto del modulo, ad esempio pannelli, componenti, campi e layout.
* Modifica le proprietà del componente.
* Cerca, visualizza e utilizza le risorse nell’archivio AEM Digital Asset Management (DAM).
* Aggiungere componenti al modulo.

![Barra laterale](assets/sidebar-comps.png)

**A.** Browser del contenuto  **B.** Browser delle proprietà  **C.** Browser risorse  **D.** Browser componenti

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

La barra laterale comprende i seguenti browser:

* **Browser**
dei contenutiNel browser dei contenuti è possibile visualizzare

   * **Oggetti**
moduloMostra la gerarchia degli oggetti del modulo. L’autore può passare a un componente modulo specifico toccandolo nella struttura ad albero oggetto modulo. L&#39;autore può cercare gli oggetti e riorganizzarli da questo albero.

   * **Oggetti**
del modello datiConsente di visualizzare la gerarchia del modello di modulo.
Consente di trascinare e rilasciare gli elementi del modello di modulo sul modulo adattivo. Gli elementi aggiunti vengono automaticamente convertiti in componenti modulo mantenendo le proprietà originali. È possibile visualizzare gli oggetti del modello dati quando il modulo utilizza lo schema XML, lo schema JSON o il modello XDP.

* **Browser proprietà**

   Consente di modificare le proprietà di un componente. Le proprietà cambiano in base a un componente. Per visualizzare le proprietà del contenitore di moduli adattivi:

   Seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi tocca ![cmppr](assets/cmppr.png).

* **Browser risorse**

   Segrega contenuti di tipi diversi come immagini, documenti, pagine, filmati e così via.

* **Browser Componenti**

   Include i componenti che è possibile utilizzare per creare un modulo adattivo. Puoi trascinare i componenti da al modulo adattivo per aggiungere elementi al modulo e configurare gli elementi aggiunti in base ai requisiti. La tabella seguente descrive i componenti elencati nel browser Componenti.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funzionalità</strong></th>
  </tr>
  <tr>
   <td>Blocco Adobe Sign</td>
   <td>Aggiunge un blocco di testo con segnaposto per i campi da compilare durante la firma tramite Adobe Sign.</td>
  </tr>
  <tr>
   <td>Pulsante</td>
   <td>Aggiunge un pulsante che è possibile configurare per eseguire azioni quali salvataggio, ripristino, successivo, precedente e così via.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Aggiunge la convalida CAPTCHA utilizzando il servizio Google reCAPTCHA. Per informazioni dettagliate, consulta <a href="../../forms/using/captcha-adaptive-forms.md" target="_blank">Uso del CAPTCHA nei moduli adattivi</a>.</td>
  </tr>
  <tr>
   <td>Grafico</td>
   <td>Aggiunge un grafico che è possibile utilizzare nei moduli adattivi e nei documenti per la rappresentazione visiva di dati bidimensionali in pannelli e righe di tabella ripetibili.</td>
  </tr>
  <tr>
   <td>Casella di selezione</td>
   <td>Aggiunge una casella di controllo.</td>
  </tr>
  <tr>
   <td>Campo immissione data</td>
   <td>Utilizzare il componente Campo di immissione data nel modulo per consentire ai clienti di compilare separatamente in tre caselle il giorno, il mese e l’anno. Puoi personalizzare l’aspetto del componente e modificare il formato della data. Ad esempio, puoi lasciare che i tuoi clienti inseriscano le date in formato MM/GG/AAAA o GG/MM/AAAA .</td>
  </tr>
  <tr>
   <td>Selettore data</td>
   <td>Aggiunge un campo calendario per scegliere una data.</td>
  </tr>
  <tr>
   <td>Frammento di documento</td>
   <td>Consente di aggiungere componenti riutilizzabili di una corrispondenza.</td>
  </tr>
  <tr>
   <td>Gruppo di frammenti di documenti</td>
   <td>Consente di aggiungere un gruppo di frammenti di documento correlati che è possibile utilizzare in un modello di lettera come una singola unità.</td>
  </tr>
  <tr>
   <td>Elenco a discesa</td>
   <td>Aggiunge un elenco a discesa, a selezione singola o multipla</td>
  </tr>
  <tr>
   <td>E-mail</td>
   <td><p>Aggiunge un campo per acquisire l’indirizzo e-mail. Il componente E-mail, per impostazione predefinita, convalida gli indirizzi e-mail utilizzando la seguente espressione regolare.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Allegato file</td>
   <td><p>Aggiunge un pulsante che consente agli utenti di sfogliare e allegare documenti di supporto a un modulo. È possibile allegare più file a un componente File allegato. Puoi inoltre specificare i **[!UICONTROL Dimensione massima file]** e **[!UICONTROL Tipi di file supportati]** per gli allegati nel browser delle proprietà del componente. </p> <p><strong> Nota: </strong><ul> <li> Il componente non supporta l’associazione di file con nome del file che inizia con caratteri (.), contenenti caratteri \ / : * ? " &lt; &gt; | % $, o contenente nomi di file speciali riservati per sistemi operativi Windows come nul, prn, con, lpt o com. </li> <li> Per allegare più file a un componente file allegato aperto nel browser Apple Safari, selezionare e allegare i file uno alla volta. Non è possibile selezionare e allegare più file contemporaneamente.</li> <li>Il componente File allegato supporta un set predefinito di formati di file nei moduli adattivi abilitati per Adobe Sign. Per ulteriori informazioni, vedere <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formati di file supportati</a>. </li></ul></p> </td>
  </tr>
  <tr>
   <td>Elenco allegati file</td>
   <td>Aggiunge un campo che elenca tutti gli allegati caricati utilizzando il componente File allegato.</td>
  </tr>
  <tr>
   <td>Intestazione<br /> </td>
   <td>Aggiunge l'intestazione di pagina che in genere include il logo di una società, il titolo del modulo e il riepilogo.<br /> </td>
  </tr>
  <tr>
   <td>Piè di pagina</td>
   <td>Aggiunge il piè di pagina che in genere include informazioni sul copyright e collegamenti ad altre pagine. </td>
  </tr>
  <tr>
   <td>Immagine</td>
   <td>Consente di inserire un’immagine.</td>
  </tr>
  <tr>
   <td>Scelta immagine</td>
   <td>Consente ai clienti di selezionare un’immagine per fornire informazioni. Puoi utilizzare le informazioni per fornire servizi personalizzati ai tuoi clienti.</td>
  </tr>
  <tr>
   <td>Pulsante Successivo</td>
   <td>Aggiunge un pulsante per passare al pannello successivo di un modulo.</td>
  </tr>
  <tr>
   <td>Casella numerica</td>
   <td>Aggiunge un campo per l’acquisizione di valori numerici</td>
  </tr>
  <tr>
   <td>Stepper numerico</td>
   <td>Utilizzare l’opzione Incremento numerico nel modulo per consentire ai clienti di immettere un valore numerico che può aumentare o diminuire in base a un passaggio predefinito.</td>
  </tr>
  <tr>
   <td>Pannello</td>
   <td><p>Aggiunge un pannello o un sottopannello.</p> <p>Puoi anche aggiungere un componente pannello dalla barra degli strumenti del pannello principale utilizzando il pulsante <span class="uicontrol">Aggiungi pannello figlio</code> . Allo stesso modo, puoi aggiungere una barra degli strumenti specifica per il pannello utilizzando il pulsante <span class="uicontrol">Aggiungi barra degli strumenti del pannello</code> . È possibile configurare la posizione della barra degli strumenti del pannello utilizzando la finestra di dialogo Modifica pannello.</code></code></p> </td>
  </tr>
  <tr>
   <td>Casella password</td>
   <td>Aggiunge un campo per l’acquisizione di una password.</td>
  </tr>
  <tr>
   <td>Pulsante Precedente</td>
   <td>Aggiunge un pulsante necessario agli utenti per tornare alla pagina o al pannello precedente.</td>
  </tr>
  <tr>
   <td>Pulsante di scelta</td>
   <td>Aggiunge pulsanti di scelta.</td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Aggiunge un pulsante per reimpostare i campi del modulo.</td>
  </tr>
  <tr>
   <td>Pulsante di salvataggio</td>
   <td>Aggiunge un pulsante per salvare i dati del modulo.</td>
  </tr>
  <tr>
   <td>Firma scarabocchio</td>
   <td>Aggiunge un campo per l’acquisizione delle firme a forma di scarabocchio.</td>
  </tr>
  <tr>
   <td>Separatore</td>
   <td>Abilita la separazione visiva dei pannelli nel modulo.</td>
  </tr>
  <tr>
   <td>Passaggio di firma</td>
   <td>Visualizza le informazioni fornite nel modulo e i campi firma che consentono all’utente di verificare e firmare il modulo.</td>
  </tr>
  <tr>
   <td>Testo</td>
   <td>Consente di specificare il testo statico.</td>
  </tr>
  <tr>
   <td>Pulsante Invia</td>
   <td>Aggiunge un pulsante di invio per inviare il modulo all’azione di invio configurata.</td>
  </tr>
  <tr>
   <td>Passaggio di riepilogo</td>
   <td>Invia il modulo e visualizza il testo di riepilogo specificato dagli autori dopo l’invio del modulo. </td>
  </tr>
  <tr>
   <td>Scambia</td>
   <td>Aggiunge un interruttore che esegue un’azione di attivazione/disattivazione o attivazione/disattivazione. Non è possibile aggiungere più di due opzioni nel componente Cambia. Poiché un commutatore può avere solo due valori: On o Off, obbligatorio non applicabile. Almeno un valore viene salvato indipendentemente dall’input dell’utente. <br /> </td>
  </tr>
  <tr>
   <td>Tabella</td>
   <td>Aggiunge una tabella che consente di organizzare i dati in righe e colonne. </td>
  </tr>
  <tr>
   <td>Telefono</td>
   <td><p>Aggiunge un campo per acquisire il numero di telefono. Il componente Telefono permette agli autori di configurare uno dei seguenti tipi di numeri di telefono: Ciascun tipo è associato a un'espressione regolare predefinita per la convalida.</p>
    <ul>
     <li>Type International viene convalidato da <code>^[+][0-9]{0,14}$</code>.</li>
     <li>Il tipo USPhoneNumber viene convalidato da <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>Il tipo UKPhoneNumber viene convalidato da <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Il tipo personalizzato non fornisce un pattern di convalida predefinito. Prende il valore dell'ultimo tipo di numero di telefono selezionato. È inoltre possibile specificare un pattern di convalida personalizzato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Condizioni d’uso<br /> </td>
   <td>Aggiunge un campo che gli autori possono utilizzare per specificare i termini e le condizioni da esaminare prima di compilare il modulo.</td>
  </tr>
  <tr>
   <td>Casella di testo </td>
   <td><p>Aggiunge una casella di testo in cui l’utente può specificare le informazioni richieste. </p> <p>Per impostazione predefinita, il componente Casella di testo accetta solo testo normale. È possibile abilitare un componente Casella di testo per accettare il testo RTF. Un componente Testo avanzato fornisce opzioni per aggiungere intestazioni, modificare gli stili dei caratteri (grassetto, corsivo, sottolineato i caratteri), creare elenchi ordinati e non ordinati, modificare lo sfondo del testo e il colore del testo e aggiungere collegamenti ipertestuali. Per abilitare il testo RTF per una casella di testo, abilitare l'opzione<strong> Consenti testo RTF</strong> nelle proprietà del componente.</p> </td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Specifica un titolo per il modulo adattivo.</td>
  </tr>
  <tr>
   <td>Passaggio verifica</td>
   <td><p>Aggiunge un segnaposto per visualizzare il modulo compilato per la verifica da parte dell’utente.</p> <p><strong>Nota</strong>: Il modulo adattivo contenente il componente Verifica non supporta gli utenti anonimi. Inoltre, si sconsiglia di utilizzare il componente Verifica in un frammento di modulo adattivo.</p> </td>
  </tr>
 </tbody>
</table>

#### Best practice per l’utilizzo dei componenti {#best-practices}

Alcune best practice e punti chiave da tenere a mente quando si utilizzano i componenti per moduli adattivi sono i seguenti:

* A ciascun componente sono associate proprietà che ne controllano l’aspetto e la funzionalità. Per configurare le proprietà di un componente, tocca il componente e tocca ![cmppr](assets/cmppr.png) per aprire le proprietà del componente nel browser Proprietà.
* Un componente viene identificato con il suo nome elemento. Quando tocchi ![cmppr](assets/cmppr.png), puoi modificare il nome del componente modificando il valore del campo **[!UICONTROL Nome elemento]** nel browser delle proprietà. Il campo Nome elemento accetta solo lettere, numeri, trattini (-) e caratteri di sottolineatura (_). Altri caratteri speciali non sono consentiti e il nome dell’elemento deve iniziare con una lettera.

* È possibile modificare la proprietà Title di un componente modulo adattivo in linea nell’editor moduli senza aprire il browser Proprietà, purché il titolo sia visibile sul modulo. Per eseguire questa operazione:

   1. Tocca per selezionare un componente che ha una proprietà **[!UICONTROL Titolo]** e la cui proprietà **[!UICONTROL Nascondi titolo]** è disabilitata.

   1. Tocca ![aem_6_3_edit](assets/aem_6_3_edit.png) per rendere modificabile il titolo.

   1. Modifica il titolo e tocca il tasto Invio oppure tocca un punto qualsiasi all’esterno del componente per salvare le modifiche. Tocca il tasto Esc per eliminare le modifiche.

* Alcuni componenti per moduli adattivi come E-mail e telefono includono pattern di convalida predefiniti. Tuttavia, è possibile specificare una convalida personalizzata aggiornando il campo **[!UICONTROL Pattern convalida]** nel pannello Pattern delle proprietà del componente. Per ulteriori informazioni sulle convalide predefinite, consulta le descrizioni dei componenti nella tabella precedente.

* I campi dei moduli adattivi, ad esempio Casella numerica e E-mail, possono essere configurati per includere tipi di input HTML5 specifici. Quando questi campi sono concentrati su dispositivi mobili e tablet, il tastierino mostra in primo piano un alfabeto, numeri e caratteri specifici comunemente utilizzati per inserire informazioni nei campi. Consente agli utenti di immettere le informazioni rapidamente senza dover alternare tra i set di caratteri sul tastierino. Per consentire un input specializzato per un componente, abilita la casella di controllo **[!UICONTROL Use HTML Type Number]** nelle proprietà del relativo componente.

* È possibile abilitare un componente Casella di testo per accettare il testo RTF. Per abilitare il testo RTF per una casella di testo, abilitare la casella di controllo **[!UICONTROL Consenti testo RTF]** nelle proprietà del componente.

* È possibile abilitare i componenti Casella di testo, E-mail e Telefono per la compilazione automatica dei valori per campi quali nome, indirizzo, carta di credito, telefono ed e-mail dalle informazioni memorizzate nelle impostazioni di compilazione automatica del browser. Per abilitare questa funzione, seleziona **[!UICONTROL Abilita compilazione automatica]** nelle proprietà del componente e seleziona un **[!UICONTROL Attributo di compilazione automatica]**. Quando un utente compila un modulo adattivo, i valori vengono suggeriti dal profilo di compilazione automatica nel browser o in base ai valori precedentemente compilati dall’utente. La compilazione automatica funziona se le impostazioni di compilazione automatica nel browser dell’utente sono attivate.

* Specificare i valori per gli elementi Pulsante di scelta e Casella di controllo nel formato `{value}={text}` nelle proprietà dei componenti.
* Il componente File allegato, per impostazione predefinita, consente a un utente di allegare un solo file. Tuttavia, è possibile configurare le proprietà del componente per supportare più allegati. Inoltre, se un utente allega più file con lo stesso nome file, gli allegati possono causare alcuni problemi. Pertanto, è consigliabile associare un identificatore univoco per ciascun allegato inviato all’invio del modulo. Per eseguire questa operazione:

   1. Sul server AEM Forms, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
   1. Trova e tocca **[!UICONTROL Servizio di configurazione Forms adattiva]**.
   1. Nella finestra di dialogo Servizio di configurazione Forms adattivo, abilita **[!UICONTROL Rendi unici i nomi dei file]**. Per impostazione predefinita, è disabilitata.

* Per consentire agli utenti di allegare un PDF utilizzando il browser Safari, assicurarsi che **application/pdf** sia aggiunto alla proprietà Tipi di file supportati del componente File allegato. I moduli adattivi creati con la versione precedente di AEM Forms possono contenere **.pdf** invece di **application/pdf** nella proprietà Tipi di file supportati.

Per ulteriori best practice sui moduli adattivi, consulta [Best practice per l’utilizzo dei moduli adattivi](/help/forms/using/adaptive-forms-best-practices.md).

>[!NOTE]
>
>I componenti per moduli adattivi non supportano le lingue RTL (da destra a sinistra). Per esempio, l&#39;ebraico.

### Barra degli strumenti della pagina {#page-toolbar}

La barra degli strumenti della pagina in alto contiene opzioni che consentono di visualizzare l’anteprima del modulo, modificare le proprietà del modulo e il layout del modulo. È possibile visualizzare l’anteprima del modulo durante la creazione e apportare le modifiche necessarie. Nella barra degli strumenti della pagina sono disponibili le seguenti opzioni:

* **Attiva/Disattiva pannello laterale** ![di selezione](assets/toggle-side-panel.png): Consente di mostrare o nascondere Sidebar.

* **Informazioni pagina** ![theme-options](assets/theme-options.png): Consente di visualizzare le proprietà della pagina, pubblicare/annullare la pubblicazione di un modulo, avviare un flusso di lavoro del modulo e aprire il modulo nell’interfaccia classica.

* **** ![Emulatore](assets/ruler.png): Consente di emulare l’aspetto del modulo per diverse dimensioni di visualizzazione, ad esempio tablet e telefoni.

* **Modifica**: Consente di selezionare altre modalità, ad esempio:  **[!UICONTROL Modifica]**,  **[!UICONTROL Stile]**,  **[!UICONTROL Sviluppatore]** e  **[!UICONTROL Progettazione]**.

   * **Modifica**: Consente di modificare le proprietà del modulo e dei suoi componenti. Ad esempio, aggiungere un componente, rilasciare un’immagine e specificare campi obbligatori.
   * **Stile**: Consente di definire lo stile dei componenti del modulo. Ad esempio, in modalità stile è possibile selezionare un pannello e specificarne il colore di sfondo.

   * **Sviluppatore**: Consente a uno sviluppatore di:

      * Scopri di quali moduli sono composti.
      * Esegui il debug di ciò che sta accadendo dove e quando, che a sua volta aiuta a risolvere i problemi.
   * **Progettazione**. Consente di abilitare o disabilitare i componenti personalizzati o i componenti predefiniti non elencati nella barra laterale.


* **Anteprima**: Consente di visualizzare un’anteprima dell’aspetto del modulo quando viene pubblicato.

### Barra degli strumenti del componente {#component-toolbar}

![Barra degli strumenti del componente nell’interfaccia touch](assets/component-toolbar.png)

Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di utilizzarlo. Sono disponibili opzioni per tagliare, incollare, spostare e specificare le proprietà dei componenti. Le opzioni disponibili sono:

A.**Configura**: Quando tocchi **[!UICONTROL Configura]**, le proprietà dei componenti sono visibili nella barra laterale. La configurazione di queste proprietà ti consente di personalizzare l’esperienza di acquisizione dei dati. Puoi modificare il nome dell’elemento del componente, specificare il testo dell’etichetta nel campo Titolo del componente. Il nome dell’elemento consente di acquisire i valori immessi dall’utente utilizzando il componente. Nelle proprietà del componente, specifichi il comportamento del componente e gestisci l’input dell’utente. Configura le proprietà nella barra laterale per acquisire i dati utente e utilizzalo per un’ulteriore elaborazione. Le proprietà per il contenitore di moduli adattivi consentono di specificare le librerie client, i layout, i temi, le impostazioni del documento di record, salvare le impostazioni, le impostazioni di invio e le impostazioni dei metadati.

B.**Copia**: È possibile utilizzare l’opzione Copia per copiare un componente e incollarlo in altre posizioni del modulo. Quando incolla un componente, il componente incollato ottiene un nuovo nome di elemento ma mantiene le proprietà del componente copiato.

C.**Taglia**: È possibile utilizzare l’opzione Taglia per spostare un componente da una posizione all’altra nel modulo adattivo.

D. **Elimina**: Consente di eliminare il componente dal modulo.

E. **Inserisci**: Consente di inserire un componente sopra il componente selezionato.

F. **Incolla**: Consente di incollare il componente tagliato o copiato utilizzando le opzioni descritte in precedenza.

G. **Modifica regole**: Consente di aprire l’editor di regole. Per ulteriori informazioni, consulta [Editor regole](../../forms/using/rule-editor.md).

H. **Gruppo**: Consente di selezionare più componenti se si desidera tagliare, copiare o incollare più componenti contemporaneamente.

I. **Elemento padre**: Consente di selezionare l’elemento padre di un componente. Ad esempio, un campo di testo si trova all’interno di una sottosezione, che si trova in una sezione. La sezione si trova nel pannello principale della guida e il contenitore di moduli adattivi è l’elemento padre di un pannello principale della guida. Per un componente, è possibile visualizzare tutte le opzioni con la gerarchia ordinata in base ai bordi inferiori.

Ad esempio, se tocchi **[!UICONTROL Elemento padre]** per una casella di testo, puoi vedere:

* Sottosezione
* Sezione
* guideRootPanel
* Contenitore Modulo adattivo

J. **Altro**: Fornisce ulteriori opzioni per lavorare con il componente selezionato.

* Visualizza espressione SOM
* Salvare un pannello come frammento (solo per i pannelli)
* Aggiungi pannello figlio (solo per pannelli)
* Aggiungi barra degli strumenti del pannello (solo per i pannelli)
* Sostituisci (non per pannelli)

### Pagina del modulo adattivo {#af-page}

La pagina del modulo adattivo è il modulo effettivo. È come qualsiasi altra pagina WCM modellata come il componente WCM `cq:Page` . L’immagine seguente mostra la struttura del contenuto di un tipico modulo adattivo.

![Struttura del contenuto di una pagina WCM del modulo adattivo](assets/afstructure.png)

La struttura del contenuto contiene in genere i seguenti componenti principali:

* **guideContainer**: Livello principale di un modulo adattivo, contrassegnato come  **[!UICONTROL Inizio del]** modulo adattivo nell’interfaccia utente del modulo adattivo. In questo componente puoi specificare:

   * *Layout mobile del modulo* adattivo: Definisce l’aspetto del modulo su dispositivi mobili.
   * *Pagina* di ringraziamento: Definisce la pagina in cui l’utente viene reindirizzato dopo l’invio del modulo.
   * *Invia azione*: Definisce la modalità di elaborazione del modulo sul server dopo l’invio del modulo da parte dell’utente.
   * *Stile*: Specifica il percorso del file CSS utilizzato per personalizzare l’aspetto del modulo.

* **rootPanel:** il pannello principale di un modulo adattivo. Può contenere pannelli secondari sotto il nodo elementi. A ogni pannello, incluso il pannello principale, può essere associato un layout. Il layout del pannello determina il layout del modulo. Ad esempio, nel layout Pannello a soffietto, i relativi elementi vengono disposti come passi Pannello a soffietto.

* **barra degli strumenti:** a un contenitore di moduli adattivi è associata una barra degli strumenti globale, globale per il modulo. Questa barra degli strumenti può essere aggiunta utilizzando l’azione **[!UICONTROL Aggiungi barra degli strumenti]** nella barra di modifica, che consente agli autori di aggiungere azioni quali Invia, Salva, Ripristina e così via.

* **risorse:** questo nodo contiene informazioni aggiuntive utilizzate per la creazione dei moduli. Ad esempio, dettagli del modello di modulo, localizzazione e così via).

