---
title: Integrazione con i componenti di Adobe Campaign
description: Quando si esegue l’integrazione con Adobe Campaign, sono disponibili componenti per l’utilizzo di newsletter e moduli.
uuid: a858d5ca-aa6e-4bde-92db-a6dcd8b48ae6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9da34dab-7e89-4127-ab26-532687746b2a
docset: aem65
exl-id: d1132fcd-e6a0-44a2-8753-d250f68fbd78
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2836'
ht-degree: 5%

---

# Componenti di Adobe Campaign{#adobe-campaign-components}

Quando si esegue l’integrazione con Adobe Campaign, sono disponibili componenti per l’utilizzo di newsletter e moduli. Entrambi sono descritti in questo documento.

>[!CAUTION]
>
>I componenti e-mail dell’AEM sono stati dichiarati obsoleti. A causa della natura dell’e-mail, che unisce contenuti e stile, i componenti e-mail forniti come predefiniti dall’AEM vengono riutilizzati in modo limitato per i clienti, a causa della necessità di implementare stili personalizzati in tutti i componenti necessari per i progetti.
>
>I componenti e-mail possono essere implementati a livello di progetto, e i componenti e-mail AEM obsoleti illustrano come ciò possa essere ottenuto. Tuttavia, questi componenti obsoleti non devono essere utilizzati nei progetti.

## Componenti della newsletter di Adobe Campaign {#adobe-campaign-newsletter-components}

Tutti i componenti di Campaign seguono le best practice descritte in [Best practice per i modelli e-mail](/help/sites-administering/best-practices-for-email-templates.md) e si basano sul linguaggio di markup Adobe [HTL](https://helpx.adobe.com/it/experience-manager/htl/using/overview.html).

Quando apri una newsletter/e-mail configurata per l’integrazione con Adobe Campaign, dovresti vedere i seguenti componenti in **Newsletter Adobe Campaign** sezione:

* Intestazione (Campaign)
* Immagine (Campaign)
* Collegamento (Campagna)
* Modello immagini di Scene7 (Campaign)
* Riferimento di destinazione (Campaign)
* Testo e immagine (Campaign)
* Testo e personalizzazione (Campaign)

La descrizione di questi componenti è riportata nella sezione seguente.

I componenti vengono visualizzati come segue:

![chlimage_1-43](assets/chlimage_1-43.png)

### Intestazione (Campaign) {#heading-campaign}

Il componente intestazione può:

* Visualizza il nome della pagina corrente lasciando il **Titolo** campo vuoto.
* Visualizzare un testo specificato in **Titolo** campo.

È possibile modificare **Intestazione (Campaign)** direttamente. Lascia vuoto per usare il titolo della pagina.

![chlimage_1-44](assets/chlimage_1-44.png)

Puoi configurare quanto segue:

* **Titolo**
Se si desidera utilizzare un nome diverso dal titolo della pagina, immetterlo qui.

* **Livello di intestazione (1, 2, 3, 4)**
Livello di intestazione in base alle dimensioni di intestazione HTML da 1 a 4.

L’esempio seguente mostra un componente Titolo (Campagna) visualizzato.

![chlimage_1-45](assets/chlimage_1-45.png)

### Immagine (Campaign) {#image-campaign}

Il componente Immagine (campagna) visualizza un’immagine e il testo che la accompagna in base ai parametri specificati.

Puoi caricare un’immagine, quindi modificarla e manipolarla (ad esempio ritagliarla, ruotarla, aggiungere un collegamento/titolo/testo).

È possibile trascinare un&#39;immagine dalla [Browser risorse](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui) direttamente sul componente o sui relativi [Finestra di dialogo per configurazione](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui). Puoi anche caricare un’immagine dalla finestra di dialogo Configura, che controlla anche tutte le definizioni e le manipolazioni dell’immagine:

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>È necessario immettere le informazioni nel **Testo alternativo** o non è possibile salvare l&#39;immagine.

Dopo che l’immagine è stata caricata (e non prima) puoi utilizzare [modifica diretta](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) per ritagliare/ruotare l&#39;immagine come richiesto:

![Barra degli strumenti di modifica diretta](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>L’editor locale utilizza le dimensioni e le proporzioni originali dell’immagine durante la modifica. È inoltre possibile specificare le proprietà relative all&#39;altezza e alla larghezza. Tutte le restrizioni relative a dimensioni e proporzioni definite nelle proprietà vengono applicate quando si salvano le modifiche.
>
>A seconda dell’istanza, è possibile che anche il numero minimo e massimo di [progettazione della pagina](/help/sites-developing/designer.md); questi vengono sviluppati durante l’implementazione del progetto.

Nella modalità di modifica a schermo intero sono disponibili diverse opzioni aggiuntive, ad esempio mappa e zoom:

![Modalità di modifica a schermo intero](do-not-localize/chlimage_1-11.png)

Quando viene caricata un’immagine, puoi configurare quanto segue:

* **Mappa**
Per mappare un&#39;immagine, selezionare Mappa. È possibile specificare la modalità di creazione della mappa immagine (rettangolo, poligono e così via) e il punto a cui deve puntare l&#39;area.

* **Ritaglio**
Seleziona Ritaglia per ritagliare un’immagine. Utilizzare il mouse per ritagliare l&#39;immagine.

* **Ruota**
Per ruotare un&#39;immagine, selezionare Ruota. Usare ripetutamente fino a quando l&#39;immagine non viene ruotata nel modo desiderato.

* **Cancella**
Rimuove l&#39;immagine corrente.

* Barra di zoom (solo classica) Per ingrandire e ridurre l&#39;immagine, utilizzare la barra sotto l&#39;immagine (sopra i pulsanti OK e Annulla)
* **Titolo**
Titolo dell&#39;immagine.

* **Testo alternativo**
Testo alternativo da utilizzare per la creazione di contenuto accessibile.

* **Collega a**
Crea un collegamento alle risorse o ad altre pagine del tuo sito web.

* **Descrizione**
Descrizione dell&#39;immagine.

* **Dimensione**
Imposta l&#39;altezza e la larghezza dell&#39;immagine.

>[!NOTE]
>
>È necessario immettere le informazioni nel **Testo alternativo** campo in **Avanzate** o l’immagine non può essere salvata e viene visualizzato il seguente messaggio di errore:
>
>`Validation failed. Verify the values of the marked fields.`
>

L’esempio seguente mostra un componente Immagine (Campaign) visualizzato.

![chlimage_1-47](assets/chlimage_1-47.png)

### Collegamento (Campagna) {#link-campaign}

Il componente Collegamento (Campagna) consente di aggiungere un collegamento alla newsletter.

Puoi configurare quanto segue nella sezione **Visualizzazione**, **Informazioni URL**, o **Avanzate** schede:

* **Didascalia collegamento**
Didascalia del collegamento. Questo è il testo visualizzato dagli utenti.

* **Descrizione comando collegamento**
Aggiunge ulteriori informazioni sull&#39;utilizzo del collegamento.

* **TipoCollegamento**
Nell’elenco a discesa, seleziona tra **URL personalizzato** e un **Documento adattivo**. Questo campo è obbligatorio. Se selezioni URL personalizzato, puoi fornire l’URL del collegamento. Se selezioni Documento adattivo, puoi fornire il percorso del documento.

* **Parametro URL aggiuntivo**
Aggiungi eventuali parametri URL aggiuntivi. Fai clic su Aggiungi elemento per aggiungere più elementi.

>[!NOTE]
>
>È necessario immettere le informazioni nel **Tipo di collegamento** campo in **Informazioni URL** oppure il componente non può essere salvato e viene visualizzato il seguente messaggio di errore:
>
>`Validation failed. Verify the values of the marked fields.`
>

L’esempio seguente mostra un componente Collega (Campagna) visualizzato.

![chlimage_1-48](assets/chlimage_1-48.png)

### Modello immagini Dynamic Media Classic (Scene7) (Campaign) {#scene-image-template-campaign}

I modelli di immagine Dynamic Media Classic (Scene7) sono a più livelli e sono file di immagine a più livelli, in cui il contenuto e le proprietà possono essere parametrizzati per variabilità. Il **[!UICONTROL Modello immagine]** Questo componente consente di utilizzare i modelli di Scene7 nelle newsletter e di modificare i valori dei parametri dei modelli. Inoltre, puoi utilizzare le variabili di metadati di Adobe Campaign all’interno dei parametri, in modo che ogni utente possa percepire l’immagine in modo personalizzato.

![chlimage_1-49](assets/chlimage_1-49.png)

Clic **Modifica** per configurare il componente. È possibile configurare le impostazioni descritte in questa sezione. Questo modello di immagine Scene7 è descritto in dettaglio in [Componente modello immagine Scene7](/help/assets/scene7.md#image-template).

Inoltre, il pannello dei parametri elenca tutti i parametri di modello definiti per il modello in Scene7. Per ciascuno di questi parametri, puoi adattare il valore, inserire variabili o reimpostarle sul valore predefinito.

![chlimage_1-50](assets/chlimage_1-50.png)

### Riferimento di destinazione (Campaign) {#targeted-reference-campaign}

Il componente Riferimento di destinazione (Campaign) consente di creare un riferimento a un paragrafo di destinazione.

In questo componente, passa al paragrafo di destinazione per selezionarlo.

Fai clic sull’icona della cartella per passare al paragrafo a cui desideri fare riferimento. Al termine, fare clic sul segno di spunta.

### Testo e immagine (Campaign) {#text-image-campaign}

Il componente Testo e immagine (Campaign) aggiunge un blocco di testo e un’immagine.

Quando fai clic su per configurare il componente, selezioni Testo o Immagine.

![chlimage_1-51](assets/chlimage_1-51.png)

Selezione **Testo** visualizza un editor in linea:

![Barra degli strumenti Testo](do-not-localize/chlimage_1-12.png)

Selezione **Immagine** visualizza l&#39;editor locale per le immagini:

![Barra degli strumenti Immagine](do-not-localize/chlimage_1-13.png)

Consulta [Componente Immagine (Campaign)](#image-campaign) per ulteriori informazioni sull&#39;utilizzo delle immagini. Consulta [Componente Testo e personalizzazione (Campaign)](#text-personalization-campaign) per ulteriori informazioni sull&#39;utilizzo del testo.

Come per i componenti Testo e personalizzazione (Campaign) e Immagine (Campaign), puoi configurare:

* **Testo**
Immettere il testo. Utilizza la barra degli strumenti per modificare la formattazione, creare elenchi e aggiungere collegamenti.

* **Immagine**
Trascina un&#39;immagine dal Finder dei contenuti o fai clic per passare a un&#39;immagine. Ritagliare o ruotare in base alle esigenze.

* **Proprietà immagine** (**Proprietà immagine avanzate**) Consente di specificare quanto segue:

   * **Titolo**
Il titolo del blocco; verrà visualizzato al passaggio del mouse.

   * **Testo alternativo**
Testo alternativo da visualizzare se l’immagine non può essere visualizzata.

   * **Collega a**
Crea un collegamento alle risorse o ad altre pagine del tuo sito web.

   * **Descrizione**
Descrizione dell&#39;immagine.

   * **Dimensione**
Imposta l&#39;altezza e la larghezza dell&#39;immagine.

>[!NOTE]
>
>Il **Testo alternativo** campo in **Avanzate** è richiesta una scheda oppure il componente non può essere salvato e viene visualizzato il seguente messaggio di errore:
>
>`Validation failed. Verify the values of the marked fields.`
>

L’esempio seguente mostra un componente Testo e immagine (Campaign) visualizzato.

![chlimage_1-52](assets/chlimage_1-52.png)

### Testo e personalizzazione (Campaign) {#text-personalization-campaign}

Il componente Testo e personalizzazione (Campaign) consente di inserire un blocco di testo utilizzando un editor WYSIWYG, con la funzionalità fornita da [Editor Rich Text](/help/sites-authoring/rich-text-editor.md). Inoltre, questo componente consente di utilizzare i campi di contesto e i blocchi di personalizzazione disponibili da Adobe Campaign; vedi anche [Inserimento della personalizzazione](/help/sites-authoring/campaign.md#inserting-personalization).

La selezione delle icone consente di formattare il testo, incluse le caratteristiche dei caratteri, l&#39;allineamento, i collegamenti, gli elenchi e i rientri. La funzionalità è sostanzialmente la stessa in [entrambe le interfacce](/help/sites-authoring/editing-content.md), anche se il look-and-feel è diverso:

![chlimage_1-53](assets/chlimage_1-53.png)

Nell’editor locale puoi aggiungere testo, modificare la giustificazione, aggiungere e rimuovere collegamenti, aggiungere campi di contesto o blocchi di personalizzazione e attivare la modalità a schermo intero. Al termine dell’aggiunta di testo/personalizzazione, seleziona il segno di spunta per salvare le modifiche (o x per annullare). Consulta [Modifica diretta](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) per ulteriori informazioni.

>[!NOTE]
>
>* I campi di personalizzazione disponibili dipendono dal modello Adobe Campaign a cui è collegata la newsletter.
>* Dopo aver selezionato un utente tipo da ContextHub, i campi di personalizzazione vengono sostituiti automaticamente dai dati del profilo selezionato.
>
>Consulta [Inserimento della personalizzazione](/help/sites-authoring/campaign.md#inserting-personalization).

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>Solo i campi definiti nella **nms:seedingMember** viene preso in considerazione lo schema o una delle sue estensioni. Attributi delle tabelle collegate a **nms:seedingMember** non sono disponibili.

## Componenti di Adobe Campaign Form {#adobe-campaign-form-components}

I componenti Adobe Campaign vengono utilizzati per creare un modulo che gli utenti compilano per abbonarsi a una newsletter, annullare l’abbonamento a una newsletter o aggiornare i propri profili utente. Consulta [Creazione di Adobe Campaign Forms](/help/sites-authoring/adobe-campaign-forms.md) per ulteriori informazioni.

Ogni campo componente può essere collegato a un campo del database di Adobe Campaign. I campi disponibili dipendono dal tipo di dati in essi contenuti, come descritto nella sezione [Componenti e tipo di dati](#components-and-data-type). Se estendi lo schema dei destinatari in Adobe Campaign, i nuovi campi saranno disponibili nei componenti i cui tipi di dati corrispondono.

Quando apri un modulo configurato per l’integrazione con Adobe Campaign, vengono visualizzati i seguenti componenti nel **Adobe Campaign** sezione:

* Casella di selezione (Campaign)
* Campo data (Campaign) e Campo data/HTML5 (Campaign)
* Chiave principale crittografata (Campaign)
* Visualizzazione errori (Campaign)
* Chiave riconciliazione nascosta (Campaign)
* Campo numerico (Campaign)
* Campo opzione (Campaign)
* Lista di controllo delle iscrizioni (Campaign)
* Campo testo (Campaign)

I componenti vengono visualizzati come segue:

![chlimage_1-55](assets/chlimage_1-55.png)

Questa sezione descrive in dettaglio ogni componente.

### Componenti e tipo di dati {#components-and-data-type}

La tabella seguente descrive i componenti disponibili per visualizzare e modificare i dati del profilo di Adobe Campaign. Ogni componente può essere mappato su un campo del profilo Adobe Campaign per visualizzarne il valore e aggiornare il campo quando il modulo viene inviato. I diversi componenti possono essere associati solo a campi di un tipo di dati appropriato.

<table>
 <tbody>
  <tr>
   <td><p><strong>Componente</strong></p> </td>
   <td><p><strong>Tipo di dati del campo Adobe Campaign</strong></p> </td>
   <td><p><strong>Campo di esempio</strong></p> </td>
  </tr>
  <tr>
   <td><p>Casella di selezione (Campaign)</p> </td>
   <td><p>booleano</p> </td>
   <td><p>No contatto più lungo (tramite qualsiasi canale)</p> </td>
  </tr>
  <tr>
   <td><p>Campo data (Campaign)</p> <p>Campo data/HTML 5 (Campaign)</p> </td>
   <td><p>data</p> </td>
   <td><p>Data di nascita</p> </td>
  </tr>
  <tr>
   <td><p>Campo numerico (Campaign)</p> </td>
   <td><p>numerico (byte, breve, lungo, doppio)</p> </td>
   <td><p>Età</p> </td>
  </tr>
  <tr>
   <td><p>Campo opzione (Campaign)</p> </td>
   <td><p>byte con valori associati</p> </td>
   <td><p>Genere</p> </td>
  </tr>
  <tr>
   <td><p>Campo testo (Campaign)</p> </td>
   <td><p>stringa</p> </td>
   <td><p>E-mail</p> </td>
  </tr>
 </tbody>
</table>

### Impostazioni comuni alla maggior parte dei componenti {#settings-common-to-most-components}

I componenti di Adobe Campaign hanno impostazioni comuni a tutti i componenti (ad eccezione dei componenti Crittografia chiave primaria e Riconciliazione nascosta).

Nella maggior parte dei componenti, puoi configurare i seguenti elementi:

#### Titolo e testo {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **Titolo**
Se desideri utilizzare un nome diverso da quello dell’elemento, inseriscilo qui.

* **Nascondi titolo**
Selezionare questa casella di controllo se non si desidera visualizzare il titolo.

* **Descrizione**
Aggiungi una descrizione al campo per fornire ulteriori informazioni agli utenti.

* **Mostra solo valore**
Mostra solo il valore, se presente

#### Adobe Campaign {#adobe-campaign}

Puoi configurare quanto segue:

* **Mappatura**
Se necessario, seleziona un campo di personalizzazione Adobe Campaign.

* **Chiave riconciliazione**
Seleziona questa casella di controllo se questo campo fa parte della chiave di riconciliazione.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Vincoli {#constraints}

* **Obbligatorio** Selezionare questa casella di controllo per rendere obbligatorio il componente, ovvero gli utenti devono immettere un valore.
* **Messaggio richiesto** Facoltativamente, aggiungi un messaggio che indichi che il campo è obbligatorio.

![chlimage_1-58](assets/chlimage_1-58.png)

#### Attribuzione stile {#styling}

* **CSS**
Immetti le classi CSS da utilizzare per questo componente.

![chlimage_1-59](assets/chlimage_1-59.png)

### Casella di selezione (Campaign) {#checkbox-campaign}

Il componente Casella di controllo (Campaign) consente all’utente di modificare i campi del profilo Adobe Campaign di tipo dati booleano. Ad esempio, puoi avere un componente Casella di controllo (Campagna) che consente al destinatario di specificare che non desidera essere contattato tramite alcun canale.

È possibile [configurare le impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components) nel componente Casella di controllo (Campagna).

L’esempio seguente mostra un componente Casella di controllo (Campaign) visualizzato.

![chlimage_1-60](assets/chlimage_1-60.png)

### Campo data (Campaign) e Campo data/HTML 5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Utilizza il campo data per consentire ai destinatari di specificare una data, ad esempio per specificare la data di nascita. Il formato della data corrisponde al formato utilizzato nell’istanza Adobe Campaign.

Oltre a [impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components), puoi configurare quanto segue:

* **Vincoli - Vincolo** a discesa È possibile selezionare - **Nessuno** o **Data -** per aggiungere il vincolo di una data o nessun vincolo. Se selezioni data, la risposta che gli utenti immettono nel campo deve essere in un formato data.

* **Messaggio vincolo** Inoltre, puoi aggiungere un messaggio di vincolo per consentire agli utenti di formattare correttamente le risposte.
* **Stile - Larghezza** Regola la larghezza del campo toccando o facendo clic sul pulsante **+** e **-** o immettere un numero.

L’esempio seguente mostra un componente Campo data (Campaign) con la larghezza regolata.

![chlimage_1-61](assets/chlimage_1-61.png)

### Chiave principale crittografata (Campaign) {#encrypted-primary-key-campaign}

Questo componente definisce il nome del parametro URL che conterrà l’identificatore di un profilo Adobe Campaign (**Identificatore risorsa principale** o **Chiave primaria crittografata** rispettivamente in Adobe Campaign Standard e 6.1).

Ogni modulo visualizza e modifica i dati del profilo di Adobe Campaign **deve** include un componente chiave primaria crittografata.

Nel componente Chiave primaria crittografata (Campaign) puoi configurare quanto segue:

* **Titolo e testo - Nome elemento** Impostazione predefinita: encryptedPK. È necessario modificare il nome dell&#39;elemento solo quando è in conflitto con il nome di un altro elemento nel modulo. Non ci sono due campi modulo che possono avere lo stesso nome elemento.
* **Adobe Campaign - Parametro URL** Aggiungi il parametro URL per EPK. Ad esempio, puoi utilizzare il valore **epk**.

L’esempio seguente mostra un componente Chiave primaria crittografata (Campaign) visualizzato.

![chlimage_1-62](assets/chlimage_1-62.png)

### Visualizzazione errori (Campaign) {#error-display-campaign}

Questo componente consente di visualizzare gli errori di back-end. Per il corretto funzionamento del componente, la gestione degli errori del modulo deve essere impostata su Inoltra.

L’esempio seguente mostra un componente Visualizzazione errori (Campaign) visualizzato.

![chlimage_1-63](assets/chlimage_1-63.png)

### Chiave riconciliazione nascosta (Campaign) {#hidden-reconciliation-key-campaign}

Il componente Chiave riconciliazione nascosta (Campaign) consente di aggiungere campi nascosti come parte della chiave di riconciliazione a un modulo.

Nel componente Chiave riconciliazione nascosta (Campaign) puoi configurare quanto segue:

* **Titolo e testo - Nome elemento** Impostazione predefinita: reconcilKey. È necessario modificare il nome dell&#39;elemento solo quando è in conflitto con il nome di un altro elemento nel modulo. Non ci sono due campi modulo che possono avere lo stesso nome elemento.
* **Adobe Campaign - Mappatura** Mappa su un campo di personalizzazione Adobe Campaign.

L’esempio seguente mostra un componente Chiave di riconciliazione nascosta (Campaign) visualizzato.

![chlimage_1-64](assets/chlimage_1-64.png)

### Campo numerico (Campaign) {#numeric-field-campaign}

Utilizza il campo numerico per consentire ai destinatari di immettere numeri, ad esempio la loro età.

Oltre a [impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components), puoi configurare quanto segue:

* **Vincoli - Vincolo** a discesa È possibile selezionare - **Nessuno** o **Numerico -** per aggiungere il vincolo di un numero o di nessun vincolo. Se si seleziona numero, la risposta che gli utenti immettono nel campo deve essere numerica.

* **Messaggio vincolo** Inoltre, puoi aggiungere un messaggio di vincolo per consentire agli utenti di formattare correttamente le risposte.
* **Stile - Larghezza** Regola la larghezza del campo toccando o facendo clic sul pulsante **+** e **-** o immettere un numero.

L’esempio seguente mostra un componente Campo numerico (Campaign) con la larghezza configurata.

![chlimage_1-65](assets/chlimage_1-65.png)

### Campo opzione (Campaign) {#option-field-campaign}

Questo elenco a discesa consente di selezionare un’opzione, ad esempio il genere o lo stato di un destinatario.

È possibile [configurare le impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components) nel componente Campo opzione (Campaign). Per popolare l’elenco a discesa, seleziona il campo appropriato nei campi di personalizzazione di Adobe Campaign toccando o facendo clic sul simbolo Adobe Campaign e navigando fino al campo.

![chlimage_1-66](assets/chlimage_1-66.png)

L’esempio seguente mostra un componente Campo opzione (Campaign) visualizzato.

![chlimage_1-67](assets/chlimage_1-67.png)

### Lista di controllo delle iscrizioni (Campaign) {#subscriptions-checklist-campaign}

Utilizza il **Elenco di controllo delle iscrizioni (Campaign)** per modificare le sottoscrizioni associate a un profilo Adobe Campaign.

Quando viene aggiunto a un modulo, questo componente visualizza tutte le sottoscrizioni disponibili come caselle di controllo e consente all’utente di selezionare le sottoscrizioni desiderate. Quando gli utenti inviano il modulo, questo componente sottoscrive o annulla l’abbonamento dell’utente ai servizi selezionati a seconda del tipo di azione modulo (**Adobe Campaign: abbonati ai servizi** o **Adobe Campaign: Annulla iscrizione a servizi**).

>[!NOTE]
>
>Il componente non controlla i servizi a cui l’utente è già abbonato/da cui ha annullato l’abbonamento.

È possibile [configurare le impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components) nel componente Elenco di controllo delle sottoscrizioni (Campaign). Non sono disponibili configurazioni di Adobe Campaign per questo componente.

L’esempio seguente mostra un componente Elenco di controllo iscrizioni (Campaign) visualizzato.

![chlimage_1-68](assets/chlimage_1-68.png)

### Campo testo (Campaign) {#text-field-campaign}

Il componente Campo di testo (Campaign) che consente di immettere dati di tipo stringa, ad esempio un nome, un cognome, un indirizzo, un indirizzo e-mail e così via.

Oltre a [impostazioni comuni alla maggior parte dei componenti di Adobe Campaign](#settings-common-to-most-components), puoi configurare quanto segue:

* **Vincoli - Vincolo** a discesa È possibile selezionare - **Nessuna,** **E-mail**, o **Nome** (nessun umlaut): per aggiungere il vincolo di un indirizzo e-mail, un nome o nessun vincolo. Se selezioni e-mail, la risposta che gli utenti immettono nel campo deve essere un indirizzo e-mail. Se selezioni nome, deve essere un nome (gli umlaut non sono consentiti).

* **Messaggio vincolo** Inoltre, puoi aggiungere un messaggio di vincolo per consentire agli utenti di formattare correttamente le risposte.
* **Stile - Larghezza** Regola la larghezza del campo toccando o facendo clic sul pulsante **+** e **-** o immettere un numero.

L’esempio seguente mostra un componente Campo di testo (Campaign) visualizzato.

![chlimage_1-69](assets/chlimage_1-69.png)
