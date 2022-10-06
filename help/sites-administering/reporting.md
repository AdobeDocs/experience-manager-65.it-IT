---
title: Generazione rapporti
seo-title: Reporting
description: Scopri come utilizzare i rapporti in AEM.
seo-description: Learn how to work with Reporting in AEM.
uuid: eee4befd-5fa9-4ebc-8eea-56e1534a6b9b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 7e2b30a3-75ff-4735-8038-5c5391ac36f3
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
source-git-commit: 429f3ee859477fb38938fd6b9706c8006623eb03
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 5%

---

# Generazione rapporti {#reporting}

Per facilitare il monitoraggio e l’analisi dello stato dell’istanza, AEM fornisce una selezione di rapporti predefiniti, che possono essere configurati per le singole esigenze:

* [Report componente](#component-report)
* [Utilizzo disco](#disk-usage)
* [Verifica stato](#health-check)
* [Report attività pagina](#page-activity-report)
* [Report per contenuti generati dall&#39;utente](#user-generated-content-report)
* [Report utente](#user-report)
* [Report di istanze flusso di lavoro](#workflow-instance-report)
* [Rapporto sul flusso di lavoro](#workflow-report)

>[!NOTE]
>
>Questi rapporti sono disponibili solo nell’interfaccia classica. Per il monitoraggio e il reporting del sistema nell’interfaccia utente moderna, consulta [Dashboard delle operazioni.](/help/sites-administering/operations-dashboard.md)

È possibile accedere a tutti i report dal **Strumenti** console. Seleziona **Rapporti** nel riquadro a sinistra, fai doppio clic sul rapporto desiderato nel riquadro a destra per aprirlo in modalità di visualizzazione e/o configurazione.

È inoltre possibile creare nuove istanze di un rapporto da **Strumenti** console. Seleziona **Rapporti** nel riquadro a sinistra, quindi **Nuovo...** dalla barra degli strumenti. Definire un **Titolo** e **Nome**, seleziona il tipo di rapporto desiderato, quindi fai clic su **Crea**. La nuova istanza di report verrà visualizzata nell&#39;elenco. Fai doppio clic su questo per aprire, quindi trascina un componente dalla barra laterale per creare la prima colonna e avviare la definizione del rapporto.

>[!NOTE]
>
>Oltre ai report AEM standard disponibili, puoi [sviluppare report personalizzati (completamente nuovi)](/help/sites-developing/dev-reports.md).

## Nozioni di base sulla personalizzazione dei report {#the-basics-of-report-customization}

Sono disponibili diversi formati di rapporti. Nei rapporti seguenti vengono utilizzate tutte le colonne personalizzabili come descritto nelle sezioni seguenti:

* [Report componente](#component-report)
* [Report attività pagina](#page-activity-report)
* [Report per contenuti generati dall&#39;utente](#user-generated-content-report)
* [Report utente](#user-report)
* [Report di istanze flusso di lavoro](#workflow-instance-report)

>[!NOTE]
>
>I seguenti rapporti hanno ciascuno un proprio formato e personalizzazione:
>
>
>* [Verifica stato](#health-check) utilizza i campi di selezione per specificare i dati sui quali si desidera creare un rapporto.
>* [Utilizzo del disco](#disk-usage) utilizza i collegamenti per approfondire la struttura del repository.
>* [Rapporto sul flusso di lavoro](/help/sites-administering/reporting.md#workflow-report) offre una panoramica dei flussi di lavoro in esecuzione sull’istanza.
>
>Pertanto, le seguenti procedure per la configurazione delle colonne non sono appropriate. Per i dettagli, vedere le descrizioni dei singoli rapporti.

### Selezione e posizionamento delle colonne di dati {#selecting-and-positioning-the-data-columns}

Le colonne possono essere aggiunte, riposizionate o rimosse da uno qualsiasi dei rapporti, sia standard che personalizzati.

La **Componenti** scheda della barra laterale (disponibile nella pagina del rapporto) elenca tutte le categorie di dati che possono essere selezionate come colonne.

Per modificare la selezione dei dati:

* per aggiungere una nuova colonna, trascinate il componente richiesto dalla barra laterale e rilasciatelo nella posizione desiderata

   * un segno di spunta verde indica quando la posizione è valida e una coppia di frecce indica esattamente dove sarà posizionata
   * se la posizione non è valida, viene visualizzato un simbolo rosso di rinuncia

* per spostare una colonna, fai clic sull’intestazione, tieni premuto e trascina nella nuova posizione
* per rimuovere una colonna, fai clic sul titolo della colonna, tieni premuto e trascina verso l’alto nell’area di intestazione del rapporto (un simbolo meno rosso indica che la posizione non è valida); rilascia il pulsante del mouse e la finestra di dialogo Elimina componenti per richiedere la conferma dell’eliminazione effettiva della colonna.

### Menu a discesa Colonna {#column-drop-down-menu}

Ogni colonna del rapporto dispone di un menu a discesa. Questo diventa visibile quando il cursore del mouse si sposta sulla cella del titolo della colonna.

All&#39;estrema destra della cella del titolo viene visualizzata una freccia (da non confondere con la freccia rivolta a destra del testo del titolo che indica la [meccanismo di ordinamento corrente](#sorting-the-data)).

![reportcolumnsort](assets/reportcolumnsort.png)

Le opzioni disponibili nel menu dipendono dalla configurazione della colonna (come apportata durante lo sviluppo del progetto), tutte le opzioni non valide saranno disattivate.

### Ordinamento dei dati {#sorting-the-data}

I dati possono essere ordinati in base a una colonna specifica in base a:

* facendo clic sull’intestazione della colonna appropriata; l’ordinamento viene alternato tra ascendente e decrescente, indicato da una freccia accanto al testo del titolo
* utilizza [menu a discesa della colonna](#column-drop-down-menu) per selezionare **Ordinamento crescente** o **Ordinamento decrescente**; di nuovo, questo viene indicato da una freccia accanto al testo del titolo

### Gruppi e Grafico dati corrente {#groups-and-the-current-data-chart}

Sulle colonne appropriate è possibile selezionare **Raggruppa per questa colonna** dal [menu a discesa della colonna](#column-drop-down-menu). In questo modo i dati verranno raggruppati in base a ciascun valore distinto all’interno di tale colonna. È possibile selezionare più colonne da raggruppare. L’opzione sarà disattivata quando i dati nella colonna non sono appropriati; Ad esempio, ogni voce è distinta e univoca per cui non è possibile formare alcun gruppo, ad esempio la colonna ID utente del rapporto utente.

Dopo che almeno una colonna è stata raggruppata in un grafico a torta **Dati correnti** verrà generato in base a questo raggruppamento. Se sono raggruppate più colonne, questo sarà indicato anche nel grafico.

![giornalista](assets/reportuser.png)

Spostando il cursore sul grafico a torta, viene visualizzato il valore aggregato per il segmento appropriato. Questo utilizza l’aggregato attualmente definito per la colonna; ad esempio, conteggio, minimo, media, tra gli altri.

### Filtri e aggregati {#filters-and-aggregates}

Nelle colonne appropriate è inoltre possibile configurare **Impostazioni filtro** e/o **Aggregati** dal [menu a discesa della colonna](#column-drop-down-menu).

#### Filtri {#filters}

Le impostazioni filtro consentono di specificare i criteri per le voci da visualizzare. Gli operatori disponibili sono:

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

Per impostare un filtro:

1. Seleziona l’operatore desiderato dall’elenco a discesa.
1. Immettere il testo su cui filtrare.
1. Fai clic su **Applica**.

Per disattivare il filtro:

1. Rimuovi il testo del filtro.
1. Fai clic su **Applica**.

#### Aggregati {#aggregates}

Puoi anche selezionare un metodo di aggregazione (che può variare a seconda della colonna selezionata):

![reportaggregato](assets/reportaggregate.png)

### Proprietà colonna {#column-properties}

Questa opzione è disponibile solo quando [Colonna generica](#generic-column) è stato utilizzato nella [Report utente](#user-report).

### Dati storici {#historic-data}

Un grafico della modifica dei dati nel tempo può essere visualizzato in **Dati storici**. Questo è derivato da istantanee effettuate a intervalli regolari.

I dati sono:

* Raccolte dalla prima colonna ordinata, se disponibile, oppure dalla prima colonna (non raggruppata)
* Raggruppato per la colonna appropriata

Il rapporto può essere generato:

1. Imposta **Raggruppamento** nella colonna richiesta.
1. **Modifica** la configurazione per definire la frequenza con cui devono essere effettuate le istantanee; ogni ora o ogni giorno.
1. **Fine...** la definizione per avviare la raccolta di istantanee.

   Il pulsante di scorrimento rosso/verde in alto a sinistra indica quando vengono raccolte le istantanee.

Il grafico risultante viene visualizzato in basso a destra:

![reportistica](assets/reporttrends.png)

Una volta avviata la raccolta dei dati, puoi selezionare:

* **Periodo**

   Puoi selezionare le date di inizio e fine per i dati del rapporto da visualizzare.

* **Intervallo**

   È possibile selezionare Mese, Settimana, Giorno, Ora per la scala e l’aggregazione del rapporto.

   Ad esempio, se per febbraio 2011 sono disponibili istantanee giornaliere:

   * Se l&#39;intervallo è impostato su `Day`, ogni istantanea viene visualizzata come un singolo valore nel grafico.
   * Se l&#39;intervallo è impostato su `Month`, tutte le istantanee di febbraio sono aggregate in un singolo valore (visualizzato come un singolo &quot;punto&quot; nel grafico).

Seleziona i requisiti e fai clic su **Vai** per applicarli al rapporto. Per aggiornare la visualizzazione dopo ulteriori istantanee, fare clic su **Vai** di nuovo.

![chlimage_1-43](assets/chlimage_1-43.png)

Quando vengono raccolte le istantanee, puoi:

* Utilizzo **Fine...** per reinizializzare la raccolta.

   **Fine** Consente di &quot;congelare&quot; la struttura del report (ovvero le colonne assegnate al report e raggruppate, ordinate, filtrate, ecc.) e inizia a scattare istantanee.

* Apri **Modifica** finestra di dialogo da selezionare **Nessuna istantanea dati** per terminare la raccolta fino a quando richiesto.

   **Modifica** attiva o disattiva solo l&#39;acquisizione delle istantanee. Se si riattiva l&#39;acquisizione delle istantanee, lo stato del rapporto dell&#39;ultima volta che è stato terminato per l&#39;esecuzione di ulteriori istantanee.

>[!NOTE]
>
>Le istantanee sono memorizzate in `/var/reports/...` dove il resto del percorso riflette il percorso del rispettivo rapporto e ID creato al termine del rapporto.
>
>
>Le vecchie istantanee possono essere eliminate manualmente, se sei completamente sicuro di non richiedere più tali istanze.

>[!NOTE]
>
>I rapporti preconfigurati non richiedono un&#39;elevata intensità di prestazioni, ma si consiglia comunque di utilizzare istantanee giornaliere in un ambiente di produzione. Se possibile, esegui queste istantanee giornaliere in un momento in cui non c&#39;è molta attività sul tuo sito web; può essere definito con `Daily snapshots (repconf.hourofday)` parametro per **Configurazione della generazione di rapporti CQ Day**; vedere [Configurazione OSGI](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli su come configurare questa funzionalità.

#### Limiti di visualizzazione {#display-limits}

Anche il rapporto sui dati storici può subire lievi variazioni di aspetto a causa dei limiti che possono essere impostati, in base al numero di risultati per il periodo selezionato.

Ogni linea orizzontale è nota come serie (e corrisponde a una voce nella legenda del grafico), ogni colonna verticale di punti rappresenta le istantanee aggregate.

![chlimage_1-44](assets/chlimage_1-44.png)

Per mantenere il grafico pulito per periodi di tempo più lunghi, è possibile impostare dei limiti. Per i rapporti standard, questi sono:

* serie orizzontale - sia il valore predefinito che il valore massimo del sistema è `9`

* istantanee aggregate verticali - il valore predefinito è `35` (per serie orizzontali)

Pertanto, quando i limiti (appropriati) vengono superati, i seguenti:

* i punti non verranno visualizzati
* la legenda del grafico dati storico potrebbe mostrare un numero di voci diverso da quello del grafico dati corrente

![chlimage_1-45](assets/chlimage_1-45.png)

I rapporti personalizzati possono anche mostrare **Totale** per tutte le serie. Viene visualizzata come una serie (linea orizzontale e voce nella legenda).

>[!NOTE]
>
>Per i rapporti personalizzati i limiti possono essere impostati in modo diverso.

### Modifica (rapporto) {#edit-report}

La **Modifica** apre **Modifica rapporto** Dialogo.

Si tratta di una posizione in cui il periodo di raccolta delle istantanee per [Dati storici](#historic-data) , ma è possibile definire anche diverse altre impostazioni:

![reportedit](assets/reportedit.png)

* **Titolo**

   Puoi definire un titolo personalizzato.

* **Descrizione**

   Puoi definire la tua descrizione.

* **Percorso radice** (*attivo solo per alcuni rapporti*)

   Utilizza questo per limitare il report a una sezione (sub) dell&#39;archivio.

* **Elaborazione dei rapporti**

   * **aggiorna i dati automaticamente**

      I dati del rapporto vengono aggiornati ogni volta che aggiorni la definizione del rapporto.

   * **aggiorna i dati manualmente**

      Questa opzione può essere utilizzata per evitare i ritardi causati dalle operazioni di aggiornamento automatico in presenza di un grande volume di dati.

      Selezionando questa opzione, i dati del rapporto devono essere aggiornati manualmente quando viene modificato un qualsiasi aspetto della configurazione del rapporto. Ciò significa anche che, non appena modifichi qualsiasi aspetto della configurazione, la tabella del rapporto sarà vuota.

      Quando questa opzione è selezionata, la **[Caricare dati](#load-data)** viene visualizzato il pulsante (accanto a **Modifica** sulla relazione). **Caricare dati** caricherà i dati e aggiornerà i dati del rapporto visualizzati.

* **Istantanee**
È possibile definire la frequenza con cui devono essere effettuate le istantanee; quotidianamente, ogni ora o per niente.

### Carica dati {#load-data}

La **Caricare dati** pulsante visibile solo quando **aggiornare manualmente i dati** è stato selezionato da **[Modifica](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

Clic su **Caricare dati** ricaricherà i dati e aggiornerà il rapporto visualizzato.

Se si seleziona per aggiornare manualmente i dati, è possibile:

1. Non appena modifichi la configurazione del rapporto, i dati della tabella del rapporto saranno disattivati.

   Ad esempio, se modifichi il meccanismo di ordinamento di una colonna, i dati non verranno visualizzati.

1. Se desideri che i dati del rapporto vengano visualizzati di nuovo, fai clic su **Caricare dati** per ricaricare i dati.

### Fine (rapporto) {#finish-report}

Quando **Fine** la relazione:

* Definizione del report *a decorrere da tale momento* viene utilizzato per acquisire le istantanee (in seguito puoi continuare a lavorare alla definizione di un report in quanto è poi separato dagli snapshot).
* Le eventuali istantanee esistenti verranno rimosse.
* Vengono raccolte nuove istantanee per [Dati storici](#historic-data).

Questa finestra di dialogo consente di definire o aggiornare il proprio titolo e descrizione per il rapporto risultante.

![rapporto](assets/reportfinish.png)

## Tipi di rapporti {#report-types}

### Report componente {#component-report}

Il rapporto sui componenti fornisce informazioni sull’utilizzo dei componenti da parte del sito web.

[Colonne delle informazioni](#selecting-and-positioning-the-data-columns) informazioni:

* Autore
* Percorso componente
* Tipo componente
* Ultima modifica
* Pagina

Significato visibile, ad esempio:

* Quali componenti vengono utilizzati quando.

   Utile, ad esempio, per i test.

* Distribuzione delle istanze di un componente specifico.

   Questo può essere interessante se si tratta di pagine specifiche (ad es. &quot;pagine pesanti&quot;) riscontrano problemi di prestazioni.

* Identificare parti del sito con modifiche frequenti/meno frequenti.
* Scopri come si sviluppa il contenuto delle pagine nel tempo.

Sono inclusi tutti i componenti, standard di prodotto e specifici per i progetti. Utilizzo della **Modifica** l&#39;utente può anche impostare un **Percorso radice** che definisce il punto di partenza del report: per il report vengono considerati tutti i componenti che si trovano sotto tale radice.

![reportcomponente](assets/reportcomponent.png) ![reportcompental](assets/reportcompentall.png)

### Utilizzo disco {#disk-usage}

Il rapporto sull&#39;utilizzo del disco mostra informazioni sui dati memorizzati nel repository.

Il rapporto inizia nella directory principale ( / ) dell&#39;archivio; facendo clic su un particolare ramo è possibile espandere il percorso all&#39;interno dell&#39;archivio (il percorso corrente verrà riportato nel titolo del rapporto).

![reportdiskusage](assets/reportdiskusage.png)

### Verifica stato {#health-check}

Questo report analizza il registro delle richieste correnti:

`<cq-installation-dir>/crx-quickstart/logs/request.log`
per identificare le richieste più costose in un dato periodo di tempo.

Per generare il rapporto puoi specificare:

* **Periodo (ore)**

   Numero di ore (passate) da analizzare.

   Predefiniti: `24`

* **max. Risultati**

   Numero massimo di linee di output.

   Predefiniti: `50`

* **max Richieste**

   Numero massimo di richieste da analizzare.

   Predefinito: `-1` (tutti)

* **Indirizzo e-mail**

   Invia i risultati a un indirizzo e-mail.

   Facoltativo; Predefinito: vuoto

* **Esegui ogni giorno alle (hh: mm)**

   Specifica l’ora in cui il rapporto deve essere eseguito automaticamente su base giornaliera.

   Facoltativo; Predefinito: vuoto

![reportive](assets/reporthealth.png)

### Report attività pagina {#page-activity-report}

Il rapporto di attività della pagina elenca le pagine e le azioni effettuate su di esse.

[Colonne delle informazioni](#selecting-and-positioning-the-data-columns) informazioni:

* Pagina
* stimato
* Tipo
* User

Consente di monitorare:

* Le ultime modifiche.
* Autori che lavorano su pagine specifiche.
* Pagine che non sono state modificate di recente, pertanto potrebbe essere necessario intervenire.
* Pagine modificate più o meno frequentemente.
* La maggior parte o meno degli utenti attivi.

Il rapporto di attività della pagina prende tutte le informazioni dal registro di controllo. Per impostazione predefinita, il percorso principale è configurato nel registro di controllo in `/var/audit/com.day.cq.wcm.core.page`.

![reportpageactivity](assets/reportpageactivity.png)

### Report per contenuti generati dall&#39;utente {#user-generated-content-report}

Questo rapporto fornisce informazioni sul contenuto generato dall’utente; siano commenti, valutazioni o forum.

[Colonne delle informazioni](#selecting-and-positioning-the-data-columns) su:

* Data
* Indirizzo IP
* Pagina
* Referrer
* Tipo
* Identificatore utente

Consente di:

* Vedi quali pagine ricevono più commenti.
* Ottieni una panoramica di tutti i commenti che specifici visitatori del sito lasciano, forse i problemi sono correlati.
* Giudica se il nuovo contenuto sta provocando commenti monitorando quando vengono effettuati commenti su una pagina.

![reportusercontent](assets/reportusercontent.png)

### Report utente {#user-report}

Questo rapporto fornisce informazioni su tutti gli utenti che hanno registrato un account e/o un profilo; può includere sia autori all’interno dell’organizzazione che visitatori esterni.

[Colonne delle informazioni](#selecting-and-positioning-the-data-columns) (se disponibile) informazioni su:

* Età
* Paese
* Dominio
* E-mail
* Cognome
* Genere
* [Generico](#generic-column)
* Nome assegnato
* Info
* Interesse
* Lingua
* Hashcode NTLM
* ID utente

Consente di:

* Scopri la diffusione demografica dei tuoi utenti.
* Report sui campi personalizzati aggiunti ai profili.

![reportusercanned](assets/reportusercanned.png)

#### Colonna generica {#generic-column}

La **Generico** La colonna è disponibile nel rapporto utente in modo da poter accedere a informazioni personalizzate, in genere dal [profili utente](/help/sites-administering/identity-management.md#profiles-and-user-accounts); ad esempio, [Colore preferito come descritto in Aggiunta di campi alla definizione del profilo](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

La finestra di dialogo della colonna Generico si aprirà quando:

* Trascina il componente Generico dalla barra laterale al rapporto.
* Selezionare Proprietà colonna per una colonna generica esistente.

![reportusrgenericola](assets/reportusrgenericcolm.png)

Da **Definizioni** è possibile definire:

* **Titolo**

   Titolo personalizzato per la colonna generica.

* **Proprietà**

   Il nome della proprietà memorizzato nell’archivio, in genere all’interno del profilo dell’utente.

* **Percorso**

   Di solito la proprietà viene prelevata dal `profile`.

* **Tipo**

   Seleziona il tipo di campo da `String`, `Number`, `Integer`, `Date`.

* **Aggregato predefinito**

   Definisce l’aggregato utilizzato per impostazione predefinita se la colonna è separata in un rapporto con almeno una colonna raggruppata. Seleziona l’aggregato richiesto da `Count`, `Minimum`, `Average`, `Maximum`, `Sum`.

   Ad esempio: *Conteggio* per `String` il numero di `String` vengono visualizzati i valori per la colonna nello stato aggregato.

In **Esteso** è inoltre possibile definire gli aggregati e i filtri disponibili:

![reportusrgenericcolmext](assets/reportusrgenericcolmextented.png)

### Report di istanze flusso di lavoro {#workflow-instance-report}

Questo offre una panoramica concisa che fornisce informazioni sulle singole istanze dei flussi di lavoro, sia in esecuzione che completati.

[Colonne delle informazioni](#selecting-and-positioning-the-data-columns) informazioni:

* Completato
* Durata
* Iniziatore
* Modello
* Payload
* Avviato
* Stato

Ciò significa che puoi:

* monitorare la durata media dei flussi di lavoro; se questo accade regolarmente, può evidenziare i problemi con il flusso di lavoro.

![reportworkflowintance](assets/reportworkflowintance.png)

### Rapporto sul flusso di lavoro {#workflow-report}

Questo fornisce statistiche chiave sui flussi di lavoro in esecuzione nell’istanza.

![reportworkflow](assets/reportworkflow.png)

## Utilizzo dei rapporti in un ambiente di pubblicazione {#using-reports-in-a-publish-environment}

Una volta configurati i rapporti in base a requisiti specifici, puoi attivarli per trasferire la configurazione nell’ambiente di pubblicazione.

>[!CAUTION]
>
>Se vuoi **Dati storici** per l’ambiente di pubblicazione, quindi **Fine** il rapporto sull’ambiente di authoring prima di attivare la pagina.

La relazione appropriata sarà quindi accessibile in

`/etc/reports`

Ad esempio, il rapporto Contenuto generato dall’utente si trova in:

`http://localhost:4503/etc/reports/ugcreport.html`

Questo ora genera rapporti sui dati raccolti dall’ambiente di pubblicazione.

Poiché nell’ambiente di pubblicazione non è consentita alcuna configurazione di report, la funzione **Modifica** e **Fine** i pulsanti non sono disponibili. Tuttavia, puoi selezionare la **Punto** e **Intervallo** per **Dati storici** segnala se vengono raccolte istantanee.

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>L&#39;accesso a tali relazioni può costituire una questione di sicurezza; pertanto, ti consigliamo di configurare il Dispatcher in modo che `/etc/reports` non è disponibile per i visitatori esterni. Consulta la sezione [Lista di controllo sicurezza](security-checklist.md) per ulteriori dettagli.

## Autorizzazioni necessarie per l’esecuzione dei rapporti {#permissions-needed-for-running-reports}

Le autorizzazioni necessarie dipendono dall’azione :

* I dati dei rapporti vengono fondamentalmente raccolti utilizzando i privilegi dell’utente corrente.
* I dati storici vengono raccolti utilizzando i privilegi dell’utente che ha completato il rapporto.

In un’installazione standard di AEM sono preimpostate le seguenti autorizzazioni per i rapporti:

* **Report utente**

   `user administrators` - lettura e scrittura

* **Report attività pagina**

   `contributors` - lettura e scrittura

* **Report componente**

   `contributors` - lettura e scrittura

* **Report per contenuti generati dall&#39;utente**

   `contributors` - lettura e scrittura

* **Report di istanze flusso di lavoro**

   `workflow-users` - lettura e scrittura

Tutti i membri `administrators` il gruppo dispone dei diritti necessari per creare nuovi rapporti.
