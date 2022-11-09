---
title: Creazione e modifica di app tramite la console App
seo-title: Creating and Editing Apps Using the Apps Console
description: Segui questa pagina per scoprire come creare e modificare le app utilizzando la console delle app.
seo-description: Follow this page to learn about creating and editing apps using apps console.
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
exl-id: 49e0b3f6-7ac7-4417-9c31-cc3d3c2305f3
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2615'
ht-degree: 1%

---

# Creazione e modifica di app tramite la console App{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Il processo di sviluppo delle applicazioni mobili AEM riconosce che gli utenti con competenze diverse contribuiscono allo sviluppo delle applicazioni mobili. La seguente mappa del processo illustra l’ordine generale in cui autori di contenuti e sviluppatori di applicazioni eseguono le attività.

![chlimage_1-10](assets/chlimage_1-10.gif)

In questa pagina vengono visualizzate informazioni su come eseguire le attività di marketing. Per informazioni sulle attività per sviluppatori, vedere Creazione di applicazioni PhoneGap.

## La struttura delle applicazioni mobili {#the-structure-of-mobile-applications}

AEM Mobile fornisce la blueprint dell’app Phonegap per la creazione di applicazioni mobili. La blueprint definisce la struttura delle applicazioni create. Le domande sono costituite dai seguenti elementi:

* La pagina principale.
* Variazioni linguistiche della domanda.
* Pagina principale della variante della lingua.

### La radice di un’app PhoneGap {#the-root-of-a-phonegap-app}

La pagina principale delle applicazioni mobili create in AEM viene visualizzata nella console App.

La pagina principale viene memorizzata sotto la proprietà Percorso di Destinazione dell&#39;applicazione specificata al momento della creazione dell&#39;applicazione (il percorso predefinito è /content/phonegap/apps). Il nome della pagina è la proprietà Name dell&#39;applicazione. Ad esempio, l’URL predefinito della pagina principale del sito denominato `myphonegapapp` è `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### Variazione di lingua di un’app PhoneGap {#the-language-variation-of-a-phonegap-app}

Le prime pagine figlie della pagina principale sono le varianti di lingua dell’applicazione. Il nome di ogni pagina è la lingua per la quale viene creata l’applicazione. Ad esempio, Inglese è il nome della variante inglese dell’applicazione.

**Nota:** La blueprint predefinita di PhoneGap crea solo un&#39;applicazione inglese. Lo sviluppatore può modificare la blueprint in modo da creare più varianti di lingua.

![chlimage_1-147](assets/chlimage_1-147.png)

La pagina relativa alla lingua ha due finalità:

* Il contenuto della pagina è la pagina spash per la variante di lingua dell&#39;applicazione.
* Le proprietà della pagina controllano diversi aspetti di progettazione dell’applicazione, ad esempio l’URL da utilizzare per la richiesta di aggiornamenti di contenuto, e informazioni sulla connessione alla build cloud e all’integrazione con Adobe Analytics Services.

![chlimage_1-148](assets/chlimage_1-148.png)

### Home page {#the-home-page}

All&#39;apertura dell&#39;applicazione viene visualizzata la home page o index.html di una variante di lingua di un&#39;applicazione.La home page fornisce agli utenti un menu di collegamenti a varie pagine dell&#39;applicazione. Il sistema paragrafo consente di aggiungere componenti alla pagina per la creazione di contenuti.

## Creazione di un&#39;applicazione mobile {#creating-a-mobile-application}

Le applicazioni mobili si basano su un modello che definisce una struttura e proprietà della pagina. Puoi configurare le seguenti proprietà dell&#39;applicazione:

* **Titolo:** Titolo dell&#39;applicazione.
* **Percorso di destinazione:** La posizione nel repository in cui è memorizzata l&#39;applicazione. Lascia l’impostazione predefinita per creare un percorso basato sul nome dell’app.

* **Nome:** Il valore predefinito è il valore della proprietà Titolo a cui sono stati rimossi gli spazi. Il nome viene utilizzato in CQ per fare riferimento all&#39;applicazione, ad esempio per il nodo del repository che rappresenta l&#39;applicazione.
* **Descrizione:** Descrizione della domanda.
* **URL server:** L’URL che fornisce contenuti OTA (Over-the-Air) viene aggiornato all’applicazione. Il valore predefinito è l&#39;URL del server di pubblicazione dell&#39;istanza utilizzata per creare un&#39;applicazione (prelevata dal servizio esternalizer). Nota: questa deve essere un&#39;istanza del server di pubblicazione anziché un autore, che richiede l&#39;autenticazione.

Puoi anche fornire un file immagine da utilizzare come miniatura dell’applicazione, selezionare la configurazione della PhoneGap Build da utilizzare e selezionare la configurazione di analisi dell’app mobile da utilizzare. Questa immagine viene utilizzata solo come miniatura per rappresentare la tua app mobile all’interno della console app mobili di Experience Manager.

Sono presenti schede aggiuntive (e facoltative) per creare il servizio cloud e integrare il plug-in Adobe Mobile Services SDK nella tua app.

* Build: Fai clic su gestisci configurazioni e configura il servizio build build build build build.phonegap.com qui. Dal menu a discesa potrai quindi selezionare il servizio cloud di build PhoneGap appena creato.
* Analytics: Fai clic su gestisci configurazioni e configura il tuo [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/using/home.html) servizio cloud. Quindi, dal menu a discesa potrai selezionare il nuovo Mobile Service da integrare nell’app mobile.

>[!NOTE]
>
>Gli sviluppatori possono utilizzare il kit di avvio PhoneGap AEM per creare app e aggiungerle alla console.

La procedura seguente utilizza l’interfaccia utente touch per creare un’app mobile.

1. Nella barra, fai clic su App.
1. Tocca o fai clic sull’icona Crea .

   ![](do-not-localize/chlimage_1-7.png)

1. (Facoltativo) Nella scheda Avanzate , fornisci una descrizione dell’applicazione e, se necessario, modifica l’URL del server.
1. (Facoltativo) Se si utilizza PhoneGap Build per compilare l&#39;applicazione, nella scheda Build selezionare la configurazione da utilizzare.

   Per creare una configurazione di build PhoneGap, fai clic su Gestisci configurazioni.

1. (Facoltativo) Se utilizzi SiteCatalyst per monitorare l’attività dell’applicazione, seleziona la configurazione da utilizzare nella scheda Analytics.

   Per creare una configurazione di app mobile, fai clic su Gestione configurazioni.

1. (Facoltativo) Per fornire un&#39;icona dell&#39;applicazione, fare clic sul pulsante Sfoglia, selezionare il file immagine dal file system e fare clic su Apri.
1. Fai clic su Crea.

### Modifica delle proprietà di un&#39;applicazione mobile {#changing-the-properties-of-a-mobile-application}

Dopo aver creato un’app mobile, puoi modificare le proprietà.

#### Modificare il titolo, la descrizione e l’icona {#change-the-title-description-and-icon}

1. Nella barra, tocca o fai clic su App.
1. Seleziona l’applicazione da configurare e fai clic sull’icona Visualizza proprietà pagina .

   ![](do-not-localize/chlimage_1-8.png)

1. Per modificare i valori delle proprietà, tocca o fai clic sull’icona Modifica .

   ![](do-not-localize/chlimage_1-9.png)

1. Configura le proprietà Base e Avanzate , quindi tocca o fai clic sull’icona Fine .

   ![](do-not-localize/chlimage_1-10.png)

#### Configurare una variante della lingua dell’applicazione {#configure-a-language-variation-of-the-application}

1. Nella barra, tocca o fai clic su App.
1. Fai clic su per approfondire l&#39;app mobile da modificare nella console di amministrazione delle app. Selezionare la versione della lingua dell&#39;applicazione da configurare e fare clic sull&#39;icona Visualizza proprietà applicazione.

   ![](do-not-localize/chlimage_1-11.png)

1. Per modificare i valori delle proprietà, tocca o fai clic sull’icona Modifica .

   ![](do-not-localize/chlimage_1-12.png)

1. Configura le proprietà nelle schede Base, Avanzate, Genera e Analytics , quindi tocca o fai clic sull’icona Fine .

   ![](do-not-localize/chlimage_1-13.png)

### Creazione del contenuto di un’applicazione mobile {#authoring-the-content-of-a-mobile-application}

Dopo aver creato l’app mobile, aggiungi il contenuto utilizzato come interfaccia utente dell’applicazione.

1. Nella barra, tocca o fai clic su App.
1. Tocca o fai clic sull’applicazione, quindi tocca o fai clic su Inglese.
1. Modificare la home page o aggiungere pagine figlie come necessario.

### Spostamento dei contenuti nelle applicazioni mobili {#moving-content-to-mobile-applications}

La cache di sincronizzazione dei contenuti nell’istanza di pubblicazione AEM viene utilizzata come archivio di contenuti per le applicazioni mobili:

* Il contenuto nella cache Content Sync viene incluso nell’applicazione quando gli sviluppatori compilano l’applicazione.
* Il contenuto nella cache è disponibile per le applicazioni mobili installate per l’aggiornamento del contenuto dell’applicazione.

Le applicazioni mobili includono un comando Aggiornamenti che scarica e installa il contenuto aggiornato dell&#39;applicazione. Quando un&#39;istanza di un&#39;applicazione invia una richiesta di aggiornamento, Content Sync determina quale contenuto è stato modificato dall&#39;ultima volta che l&#39;applicazione è stata aggiornata o installata e fornisce il nuovo contenuto.

![chlimage_1-149](assets/chlimage_1-149.png)

Per rendere disponibile contenuto aggiornato alle applicazioni, devi aggiornare la cache di sincronizzazione dei contenuti. Al primo aggiornamento della cache, viene aggiunto tutto il contenuto pubblicato. Gli aggiornamenti successivi aggiungono solo il contenuto pubblicato che è cambiato dall’aggiornamento precedente.

La sincronizzazione dei contenuti tiene traccia anche di quando si verificano gli aggiornamenti. Con queste informazioni, Content Sync può determinare quale aggiornamento della cache inviare a un’app mobile.

Esegui la seguente procedura sull’istanza in cui desideri aggiornare la cache. Ad esempio, se l’applicazione richiede aggiornamenti dall’istanza di pubblicazione, esegui la procedura sull’istanza di pubblicazione.

1. Nella barra, tocca o fai clic su App, quindi tocca o fai clic sull’applicazione.
1. Seleziona la pagina iniziale, quindi tocca o fai clic sull’icona Aggiorna cache .

   ![](do-not-localize/chlimage_1-14.png)

### Utilizzo dei modelli di app {#using-app-templates}

Si tratta di una funzione disponibile con App 6.1 Feature Pack 2 e fornisce un modo semplice per sfruttare i modelli di app esistenti per la creazione di nuove app in AEM.

Che cos&#39;è un modello di app? Consideralo come una raccolta di modelli di pagina e componenti che rappresentano una linea di base o una base di un’app.
Quando crei una nuova app basata sul modello di un’altra app, riceverai un’app con un punto di partenza rappresentativo dell’app da cui è stata creata.

Per utilizzare questa funzione, devi disporre di un modello di app mobile esistente (o di un’app installata con un modello di app).

L&#39;ultimo pacchetto di esempi AEM Apps 6.1 include una versione aggiornata dell&#39;app Geometrixx con un modello di app. In alternativa, è possibile installare StarterKit che fornisce anche un modello.

Passaggi per creare una nuova app basata su un modello di app:

1. Assicurati di avere installato il pacchetto di funzioni e i pacchetti di riferimento più recenti AEM Apps 6.1 .
1. Fai clic su App dalla barra a sinistra.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Fai clic sul pulsante + Crea in alto e seleziona Crea app.
1. Una volta visualizzato l’elenco dei modelli di app, selezionane uno:

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Fai clic su Avanti.
1. Immetti un ID app e un titolo, tuttavia potresti voler includere anche un Nome e una Descrizione.

   1. Inoltre, puoi fornire un PNG (formato icona PhoneGap supportato) come icona sfogliando AEM risorse.
   1. Ricorda che puoi modificare tutti questi campi dopo la creazione dell’app nel riquadro Gestione app . Ad eccezione dell’ID app, una volta impostato l’ID app non puoi modificarlo.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Fai clic sul pulsante crea , ti verranno presentate 2 opzioni, Fine (torna alla vista del catalogo App) o Gestione app (apre il dashboard dell’app).
1. Una volta creata, la nuova app dovrebbe essere elencata nel catalogo delle app:

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Fai clic sull’app per aprirla. La nuova app è stata creata correttamente in base al modello di un’app esistente.

>[!NOTE]
>
>Se disinstalli il pacchetto dell&#39;app di riferimento dei Geometrixx Outdoors da AEM e hai creato un&#39;app basata sul suo modello, allora quell&#39;app non funzionerà più. L’app Geometrixx Outdoors può essere rimossa, ma il modello di app deve rimanere se utilizzato da altre applicazioni mobili.

## Esplorazione dell’app Geometrixx Outdoors di esempio {#exploring-the-sample-geometrixx-outdoors-app}

L’app Geometrixx Outdoors è un’applicazione PhoneGap di esempio che illustra le funzioni del progetto predefinito dell’applicazione PhoneGap e dei componenti mobili di esempio.

Per aprire l&#39;applicazione, dalla barra laterale fai clic su Applicazioni mobili e quindi seleziona Geometrixx Outdoors app .

### Funzionalità comuni della pagina - App mobile Geometrixx {#common-page-features-geometrixx-mobile-app}

Ogni pagina dell’app mobile include le seguenti funzionalità:

* Pulsante Indietro per tornare alla pagina padre. Il pulsante Indietro non viene visualizzato nella home page.
* Una barra espandibile che offre un menu di comandi e collegamenti:

   * Apri la pagina Posizioni .
   * Apri il Carrello.
   * Accedi.
   * Aggiorna l&#39;applicazione.

* Il sistema paragrafo, per aggiungere componenti e creare contenuti.

### Home Page - Geometrixx Mobile App {#the-home-page-geometrixx-mobile-app}

Il contenuto della home page è costituito dai seguenti strumenti di navigazione:

* Componente Elenco menu che fornisce collegamenti alle pagine figlie Ingranaggio, Recensioni, Notizie e Informazioni su di noi.
* Un componente Carosello rapido che mostra le pagine figlie.

### Pagina degli ingranaggi - App mobile Geometrixx {#the-gear-page-geometrixx-mobile-app}

La pagina Gear consente agli utenti di accedere alle pagine dei prodotti. Un componente Elenco menu consente di accedere alle pagine figlie della pagina corrispondente. Le pagine figlie sono categorie di prodotti disponibili nel sito web.

* Stagione
* Abbigliamento
* Genere
* Attività

Ogni pagina di categoria utilizza la stessa struttura di contenuto della pagina Ingranaggio. Il carosello consente di accedere alle pagine figlie che sono sottocategorie di prodotti. Le pagine delle sottocategorie contengono elenchi di prodotti che forniscono collegamenti alle pagine di prodotto.

### Pagina Prodotti - App mobile Geometrixx {#the-products-page-geometrixx-mobile-app}

La pagina Prodotti e la sua gerarchia di pagine figlie implementano un sistema di classificazione per le pagine dei prodotti. Le pagine più basse di ogni ramo dell’gerarchia sono una pagina di prodotto contenente un componente Product .

La pagina Prodotti non è disponibile per gli utenti dell’applicazione. La pagina Gear consente di accedere a ogni pagina di prodotto.

### Pagina delle recensioni - Geometrixx Mobile App {#the-reviews-page-geometrixx-mobile-app}

Contiene un pulsante Indietro. Il sistema paragrafo consente di aggiungere componenti.

Quando utilizzi l’applicazione, la pagina Recensioni è disponibile dal carosello nella pagina inglese.

### Pagina News - App mobile Geometrixx {#the-news-page-geometrixx-mobile-app}

Contiene un pulsante Indietro. Il sistema paragrafo consente di aggiungere componenti.

Quando si utilizza l&#39;applicazione, la pagina News è disponibile dal carosello nella pagina inglese.

### Pagina Informazioni su di noi - Geometrixx Mobile App {#the-about-us-page-geometrixx-mobile-app}

La pagina Informazioni su di noi contiene diversi componenti per riga a due colonne . Ogni colonna contiene un componente Immagine o Testo . I componenti sono modificabili e il sistema paragrafo consente di aggiungere componenti.

Quando utilizzi l’applicazione, la pagina Informazioni su di noi è disponibile dal carosello nella pagina Inglese.

### Pagina Posizioni - Geometrixx App mobile {#the-locations-page-geometrixx-mobile-app}

La pagina Posizioni contiene un componente Posizioni .

Quando si utilizza l’applicazione, la pagina Posizioni è disponibile dall’elenco dei menu nella pagina Inglese.

## Componenti mobili di esempio {#sample-mobile-components}

Nella barra laterale sono immediatamente disponibili diversi componenti per la creazione delle pagine di un’app mobile. I componenti appartengono al gruppo di componenti PhoneGap.

### Carosello scorrevole {#swipe-carousel}

Il componente Carosello rapido è uno strumento per visualizzare e navigare nelle pagine del sito. Il componente include un carosello che scorre le immagini per le pagine elencate sopra un elenco di collegamenti di pagina. Modifica il componente per specificare le pagine da esporre e il comportamento del carosello.

Le immagini vengono visualizzate nel carosello per le pagine associate a un’immagine in un modo specifico. Quando le pagine non sono associate alle immagini, viene visualizzato solo l’elenco dei collegamenti.

![chlimage_1-151](assets/chlimage_1-151.png)

**Scheda delle proprietà del carosello**

Configura il comportamento del carosello:

* Velocità di riproduzione: Tempo in millisecondi impiegato per la visualizzazione di ogni immagine prima della visualizzazione dell&#39;immagine successiva.
* Tempo di transizione: Durata in millisecondi dell&#39;animazione per le transizioni di immagini.
* Stile comandi: Il tipo di controlli che vengono forniti per lo spostamento tra le immagini.

**Scheda Proprietà elenco**

Specifica come viene generato l’elenco di pagine:

* Crea elenco utilizzando: Metodo da utilizzare per specificare le pagine da includere nel carosello. Vedere Creazione dell’elenco di pagine .
* Ordina per: Selezionare una proprietà di pagina da utilizzare per ordinare l’elenco di pagine. Ad esempio, seleziona jcr:title per ordinare le pagine in ordine alfabetico per titolo.
* Limite: Il numero massimo di pagine da includere. Questa proprietà è appropriata per i metodi basati su ricerca per creare l&#39;elenco di pagine.

#### Creazione dell’elenco di pagine {#building-the-page-list}

Il componente Carosello rapido fornisce i seguenti valori per la proprietà Elenco build utilizzando . La finestra di dialogo di modifica cambia in base al valore selezionato:

**Pagine figlie**

Il componente elenca tutte le pagine figlie di una pagina specifica. Dopo aver selezionato questo valore, selezionare la pagina nella scheda Pagine figlie o specificare un valore per non elencare le pagine figlie della pagina corrente.

**Elenco fisso**

Specifica un elenco di pagine di inclusione. Dopo aver selezionato questo valore, configurare l&#39;elenco nella scheda Elenco fisso visualizzata quando si seleziona Elenco fisso:

* Per aggiungere una pagina, fare clic su Aggiungi elemento, quindi cercare la pagina.
* Utilizza le icone a forma di freccia su e freccia giù per spostare la pagina all’interno dell’elenco.
* Fare clic sul pulsante di rimozione per rimuovere una pagina dall’elenco.

La proprietà Order By non influisce sull&#39;ordine degli elenchi fissi.

**Ricerca**

Compilare l’elenco utilizzando i risultati di una ricerca per parola chiave. La ricerca viene eseguita negli elementi secondari di una pagina specificata:

1. Per specificare la pagina principale della ricerca, utilizzare la proprietà Start In per selezionare il percorso della pagina. Non specificare alcun percorso da cercare sotto la pagina corrente.
1. Nella proprietà Query di ricerca, immetti le parole chiave di ricerca.

**Ricerca avanzata**

Compilare l’elenco utilizzando un’ [Querybuilder](/help/sites-developing/querybuilder-api.md) query.

### Immagine {#image}

Aggiungi un&#39;immagine al contenuto dell&#39;applicazione.

### Testo {#text}

Aggiungi testo RTF al contenuto dell&#39;applicazione.

### Località negozio {#store-locations}

Il componente Store Locations (Posizioni store) fornisce agli utenti gli strumenti per trovare punti vendita:

* Ricerca
* Elenca le posizioni vicine o distanti dalle coordinate GPS del dispositivo.

Il componente richiede che l’archivio contenga informazioni sulla posizione per ogni archivio. Le posizioni di esempio sono installate nel nodo /etc/commerce/locations/adobe . ![chlimage_1-152](assets/chlimage_1-152.png)

### Riga a due colonne {#two-column-row}

Consente di aggiungere componenti affiancati a una pagina.

![chlimage_1-153](assets/chlimage_1-153.png)
