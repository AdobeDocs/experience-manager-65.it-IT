---
title: Creazione e modifica di app tramite la console App
seo-title: Creazione e modifica di app tramite la console App
description: Seguite questa pagina per informazioni sulla creazione e la modifica di app tramite la console delle app.
seo-description: Seguite questa pagina per informazioni sulla creazione e la modifica di app tramite la console delle app.
uuid: 4f7db978-ae2b-4ca6-89f1-26e091d9140a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 9890d045-cead-4d70-b797-95319284e0d8
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '2638'
ht-degree: 1%

---


# Creazione e modifica di app tramite la console App{#creating-and-editing-apps-using-the-apps-console}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Il processo di sviluppo AEM applicazioni mobili riconosce che gli utenti con competenze diverse contribuiscono allo sviluppo di applicazioni mobili. La seguente mappa del processo illustra l’ordine generale in cui gli autori e gli sviluppatori di contenuti eseguono le attività.

![chlimage_1-10](assets/chlimage_1-10.gif)

In questa pagina vengono visualizzate informazioni su come eseguire le attività di marketing. Per informazioni sulle attività per gli sviluppatori, vedere Creazione di applicazioni PhoneGap.

## Struttura delle applicazioni mobili {#the-structure-of-mobile-applications}

 AEM Mobile fornisce il progetto App PhoneGap per la creazione di applicazioni mobili. Il modello definisce la struttura delle applicazioni create. Le applicazioni sono composte dai seguenti elementi:

* La pagina principale.
* Le varianti di lingua dell&#39;applicazione.
* Pagina principale della variante della lingua.

### Radice di un&#39;app PhoneGap {#the-root-of-a-phonegap-app}

La pagina principale delle applicazioni mobili create in AEM viene visualizzata nella console App.

La pagina principale è memorizzata sotto la proprietà Percorso di destinazione dell’applicazione specificata al momento della creazione dell’applicazione (il percorso predefinito è /content/phonegap/apps). Il nome pagina è la proprietà Name dell&#39;applicazione. Ad esempio, l&#39;URL predefinito della pagina principale del sito denominato `myphonegapapp` è `http://localhost:4502/content/phonegap/apps/myphonegapapp.html`.

![chlimage_1-146](assets/chlimage_1-146.png)

### La variante della lingua di un&#39;app PhoneGap {#the-language-variation-of-a-phonegap-app}

Le prime pagine figlie della pagina principale sono le varianti di lingua dell&#39;applicazione. Il nome di ogni pagina è la lingua per la quale viene creata l’applicazione. Ad esempio, Inglese è il nome della variante inglese dell&#39;applicazione.

**Nota:** il progetto predefinito PhoneGap crea solo un&#39;applicazione in lingua inglese. Lo sviluppatore può modificare il progetto in modo da creare più varianti di lingua.

![chlimage_1-147](assets/chlimage_1-147.png)

La pagina relativa alla lingua ha due scopi:

* Il contenuto della pagina è la pagina spash per la variante della lingua dell&#39;applicazione.
* Le proprietà della pagina controllano diversi aspetti di progettazione dell&#39;applicazione, ad esempio l&#39;URL da utilizzare per richiedere aggiornamenti di contenuto, nonché informazioni sulla connessione alla build cloud e &#39;integrazione dei servizi Adobe Analytics.

![chlimage_1-148](assets/chlimage_1-148.png)

### Pagina principale {#the-home-page}

Quando l&#39;applicazione viene aperta, viene visualizzata la pagina principale, o index.html di una variante della lingua di un&#39;applicazione. La pagina principale fornisce agli utenti un menu di collegamenti alle varie pagine dell&#39;applicazione. Il sistema paragrafo consente di aggiungere componenti alla pagina per la creazione di contenuti.

## Creazione di un&#39;applicazione mobile {#creating-a-mobile-application}

Le applicazioni mobili si basano su un modello che definisce una struttura e proprietà di pagina. Potete configurare le seguenti proprietà dell’applicazione:

* **Titolo:** Titolo dell’applicazione.
* **Percorso di destinazione:** percorso nella directory archivio in cui è memorizzata l&#39;applicazione. Lasciate l&#39;impostazione predefinita per creare un percorso basato sul nome dell&#39;app.

* **Nome:** il valore predefinito è il valore della proprietà Titolo a cui sono stati rimossi gli spazi. Il nome viene utilizzato in CQ per fare riferimento all’applicazione, ad esempio per il nodo del repository che rappresenta l’applicazione.
* **Descrizione:** Una descrizione dell’applicazione.
* **URL server:** l&#39;URL che fornisce aggiornamenti di contenuto Over-the-Air (OTA) all&#39;applicazione. Il valore predefinito è l’URL del server di pubblicazione dell’istanza utilizzata per creare un’applicazione (proveniente dal servizio esternalizzatore). Nota: questa deve essere un&#39;istanza del server di pubblicazione anziché un autore, che richiede l&#39;autenticazione.

Puoi anche fornire un file immagine da usare come miniatura dell’applicazione, selezionare la configurazione delle PhoneGap Build da utilizzare e selezionare la configurazione di analisi per app mobili da utilizzare. Questa immagine viene utilizzata solo come miniatura per rappresentare l’applicazione mobile all’interno della console delle app mobili  Experience Manager.

Sono presenti schede aggiuntive (e facoltative) per creare il servizio cloud e integrare il plug-in SDK di Mobile Services  Adobe nell&#39;app.

* Build: Fai clic su Gestione configurazioni e configura il servizio build build build build build build build build.phonegap.com qui. Dal menu a discesa potrete selezionare il nuovo servizio cloud PhoneGap build.
* Analytics: Fai clic su Gestione configurazioni e configura il servizio cloud [ Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/using/home.html). Dal menu a discesa potrete selezionare il nuovo Mobile Service da integrare nell&#39;app mobile.

>[!NOTE]
>
>Gli sviluppatori possono utilizzare il AEM PhoneGap Starter Kit per creare app e aggiungerle alla console.

La procedura seguente utilizza l’interfaccia utente touch per creare un’applicazione mobile.

1. Nella barra laterale, fate clic su App.
1. Tocca o fai clic sull’icona Crea.

   ![](do-not-localize/chlimage_1-7.png)

1. (Facoltativo) Nella scheda Avanzate, fornite una descrizione per l&#39;applicazione e modificate l&#39;URL del server, se necessario.
1. (Facoltativo) Se per compilare l&#39;applicazione utilizzate PhoneGap Build, nella scheda Build selezionate la Configurazione da utilizzare.

   Per creare una configurazione di build PhoneGap, fate clic su Gestisci configurazioni.

1. (Facoltativo) Se utilizzate SiteCatalyst per monitorare l&#39;attività dell&#39;applicazione, nella scheda Analytics selezionate la configurazione da utilizzare.

   Per creare una configurazione per app mobile, fai clic su Gestisci configurazioni.

1. (Facoltativo) Per fornire un&#39;icona dell&#39;applicazione, fare clic sul pulsante Sfoglia, selezionare il file immagine dal file system in uso e fare clic su Apri.
1. Fai clic su Crea.

### Modifica delle proprietà di un&#39;applicazione mobile {#changing-the-properties-of-a-mobile-application}

Dopo aver creato un’applicazione mobile, potete modificare le proprietà.

#### Modificare il titolo, la descrizione e l&#39;icona {#change-the-title-description-and-icon}

1. Nella barra laterale, fate clic o toccate App.
1. Selezionate l’applicazione da configurare e fate clic sull’icona Visualizza proprietà pagina.

   ![](do-not-localize/chlimage_1-8.png)

1. Per modificare i valori delle proprietà, fate clic o toccate l&#39;icona Modifica.

   ![](do-not-localize/chlimage_1-9.png)

1. Configurate le proprietà Base e Avanzate, quindi toccate o fate clic sull&#39;icona Fine.

   ![](do-not-localize/chlimage_1-10.png)

#### Configurare una variante della lingua dell&#39;applicazione {#configure-a-language-variation-of-the-application}

1. Nella barra laterale, fate clic o toccate App.
1. Fai clic per approfondire l&#39;applicazione mobile che desideri modificare nella console di amministrazione delle app. Selezionate la versione della lingua dell’applicazione da configurare e fate clic sull’icona Visualizza proprietà applicazione.

   ![](do-not-localize/chlimage_1-11.png)

1. Per modificare i valori delle proprietà, fate clic o toccate l&#39;icona Modifica.

   ![](do-not-localize/chlimage_1-12.png)

1. Configura le proprietà nelle schede Base, Avanzate, Genera e Analytics, quindi tocca o fai clic sull&#39;icona Fine.

   ![](do-not-localize/chlimage_1-13.png)

### Creazione di contenuti di un&#39;applicazione mobile {#authoring-the-content-of-a-mobile-application}

Dopo aver creato l’applicazione per dispositivi mobili, aggiungete il contenuto utilizzato come interfaccia utente dell’applicazione.

1. Nella barra laterale, fate clic o toccate App.
1. Tocca o fai clic sull’applicazione, quindi tocca o fai clic su Inglese.
1. Modificate la home page o aggiungete le pagine figlie come necessario.

### Spostamento del contenuto nelle applicazioni mobili {#moving-content-to-mobile-applications}

La cache di sincronizzazione dei contenuti nell’istanza di pubblicazione AEM viene utilizzata come archivio del contenuto per le applicazioni mobili:

* Il contenuto nella cache Content Sync è incluso nell&#39;applicazione quando gli sviluppatori compilano l&#39;applicazione.
* Il contenuto presente nella cache è disponibile per le applicazioni mobili installate per aggiornare il contenuto dell&#39;applicazione.

Le applicazioni mobili includono un comando Aggiornamenti che scarica e installa il contenuto aggiornato dell&#39;applicazione. Quando un&#39;istanza di applicazione invia una richiesta di aggiornamento, Content Sync determina quale contenuto è cambiato dall&#39;ultima volta che l&#39;applicazione è stata aggiornata o installata e fornisce il nuovo contenuto.

![chlimage_1-149](assets/chlimage_1-149.png)

Per rendere disponibile il contenuto aggiornato alle applicazioni, aggiornate la cache di sincronizzazione dei contenuti. La prima volta che aggiornate la cache, viene aggiunto tutto il contenuto pubblicato. Gli aggiornamenti successivi aggiungono solo il contenuto pubblicato che è cambiato dall&#39;aggiornamento precedente.

Content Sync tiene traccia anche quando si verificano gli aggiornamenti. Con queste informazioni, Content Sync può determinare quale aggiornamento della cache inviare a un&#39;applicazione mobile.

Effettuate la seguente procedura nell’istanza in cui desiderate aggiornare la cache. Ad esempio, se l’applicazione richiede aggiornamenti dall’istanza di pubblicazione, eseguite la procedura nell’istanza di pubblicazione.

1. Nella barra laterale, tocca o fai clic su App, quindi tocca o fai clic sull’applicazione.
1. Selezionate la pagina iniziale, quindi toccate o fate clic sull&#39;icona Aggiorna cache.

   ![](do-not-localize/chlimage_1-14.png)

### Utilizzo dei modelli di app {#using-app-templates}

Questa funzione è disponibile con App 6.1 Feature Pack 2 e fornisce un modo semplice per sfruttare i modelli di app esistenti per la creazione di nuove app all&#39;interno di AEM.

Che cos&#39;è un modello di app? Può essere considerato come una raccolta di modelli di pagina e componenti che rappresentano una linea di base o una base di un&#39;app.
Quando crei una nuova app basata sul modello di un&#39;altra app, riceverai un&#39;app con un punto di partenza rappresentativo dell&#39;app da cui è stata creata.

Per utilizzare questa funzione, è necessario disporre di un modello di app mobile esistente (o di un&#39;app installata con un modello di app).

L&#39;ultimo pacchetto di AEM App 6.1 include una versione aggiornata dell&#39;app Geometrixx con un modello di app. In alternativa, è possibile installare StarterKit che fornisce anche un modello.

Passaggi per creare una nuova app basata su un modello di app:

1. Verificare che siano installati i pacchetti di feature pack App 6.1 più recenti e di esempi di riferimento
1. Fate clic su App nella parte sinistra.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Fate clic sul pulsante + Crea nella parte superiore e selezionate Crea app.
1. Dopo aver visualizzato l&#39;elenco Modelli app, selezionane uno:

![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Fai clic su Avanti.
1. Immetti un ID app e un titolo, ma potresti voler includere anche un nome e una descrizione.

   1. Potete inoltre fornire un file PNG (formato di icona PhoneGap supportato) come icona sfogliando AEM risorse.
   1. Ricorda che puoi modificare tutti questi campi dopo che l&#39;app è stata creata nel riquadro Gestisci app. Ad eccezione dell&#39;ID app, una volta impostato l&#39;ID app non potrai modificarlo.

![chlimage_1-150](assets/chlimage_1-150.png)

1. Fate clic sul pulsante Crea, vi verranno presentate due opzioni: Fine (tornate alla vista del catalogo App) oppure Gestisci app (apre il dashboard dell&#39;app).
1. Una volta creata, la nuova app dovrebbe essere elencata nel catalogo delle app:

![chlimage_1-3](assets/chlimage_1-3.jpeg)

1. Fai clic sull&#39;app per aprirla. La nuova app è stata creata correttamente in base al modello di un&#39;app esistente.

>[!NOTE]
>
>Se disinstallate il pacchetto dell&#39;app di riferimento Geometrixx Outdoors da AEM e create un&#39;app basata sul suo modello, tale app non funzionerà più. L&#39;app Geometrixx Outdoors può essere rimossa, ma il modello di app deve rimanere se utilizzato da altre applicazioni mobili.

## Esplorazione dell&#39;app Geometrixx Outdoors di esempio {#exploring-the-sample-geometrixx-outdoors-app}

L&#39;app Geometrixx Outdoors è un&#39;applicazione PhoneGap di esempio che illustra le funzioni del modello di applicazione PhoneGap predefinito e dei componenti mobili di esempio.

Per aprire l&#39;applicazione, dalla barra laterale fate clic su Applicazioni mobili, quindi selezionate Geometrixx Outdoors App.

### Funzioni comuni delle pagine - App mobile Geometrixx {#common-page-features-geometrixx-mobile-app}

Ogni pagina dell&#39;app mobile include le seguenti funzionalità:

* Pulsante Indietro per tornare alla pagina padre. Il pulsante Indietro non viene visualizzato nella home page.
* Una barra laterale che offre un menu di comandi e collegamenti:

   * Aprite la pagina Posizioni.
   * Apri il Carrello.
   * Effettuate l&#39;accesso.
   * Aggiornare l&#39;applicazione.

* Il sistema paragrafo, per aggiungere componenti e creare contenuti.

### Pagina principale - App mobile Geometrixx {#the-home-page-geometrixx-mobile-app}

Il contenuto della home page è costituito dai seguenti strumenti di navigazione:

* Componente Elenco menu che fornisce collegamenti alle pagine figlie Ingranaggio, Recensioni, Novità e Informazioni su di noi.
* Un componente Carosello con scorrimento che mostra le pagine figlie.

### Pagina ingranaggio - App mobile Geometrixx {#the-gear-page-geometrixx-mobile-app}

La pagina Gear consente agli utenti di accedere alle pagine dei prodotti. Un componente Elenco menu consente di accedere alle pagine figlie della pagina Ingranaggio. Le pagine figlie sono categorie di prodotti disponibili nel sito Web.

* Stagione
* Abbigliamento
* Genere
* Attività

Ogni pagina di categoria utilizza la stessa struttura di contenuto della pagina Ingranaggio. Il carosello consente di accedere alle pagine figlie che sono sottocategorie di prodotti. Le pagine delle sottocategorie contengono elenchi di prodotti che contengono collegamenti alle pagine di prodotto.

### Pagina Prodotti - Geometrixx app mobile {#the-products-page-geometrixx-mobile-app}

La pagina Products (Prodotti) e la sua gerarchia di pagine figlie implementano un sistema di classificazione per le pagine di prodotto. Le pagine più basse di ciascun ramo dell’eredità sono una pagina di prodotto che contiene un componente Prodotto PNG.

La pagina Prodotti non è disponibile per gli utenti dell’applicazione. La pagina Gear consente di accedere a ogni pagina di prodotto.

### Pagina recensioni - App mobile Geometrixx {#the-reviews-page-geometrixx-mobile-app}

Contiene un pulsante Indietro. Il sistema paragrafo consente di aggiungere componenti.

Quando si utilizza l&#39;applicazione, la pagina Recensioni è disponibile dal carosello nella pagina inglese.

### Pagina delle notizie - App mobile Geometrixx {#the-news-page-geometrixx-mobile-app}

Contiene un pulsante Indietro. Il sistema paragrafo consente di aggiungere componenti.

Quando si utilizza l&#39;applicazione, la pagina News è disponibile dal carosello sulla pagina inglese.

### Pagina Informazioni su di noi - App mobile Geometrixx {#the-about-us-page-geometrixx-mobile-app}

La pagina Informazioni su di noi contiene diversi componenti Riga a due colonne. Ogni colonna contiene un componente Immagine o Testo. I componenti sono modificabili e il sistema di paragrafi consente di aggiungere componenti.

Quando si utilizza l’applicazione, la pagina Informazioni su di noi è disponibile dal carosello nella pagina inglese.

### Pagina Posizioni - App mobile Geometrixx {#the-locations-page-geometrixx-mobile-app}

La pagina Locations (Posizioni) contiene un componente Locations (Posizioni).

Quando si utilizza l&#39;applicazione, la pagina Locations (Posizioni) è disponibile dall&#39;elenco dei menu nella pagina in lingua inglese.

## Componenti mobili di esempio {#sample-mobile-components}

Diversi componenti sono immediatamente disponibili nella barra laterale quando si creano le pagine di un’applicazione mobile. I componenti appartengono al gruppo di componenti PhoneGap.

### Carosello scorrevole {#swipe-carousel}

Il componente Scorrimento carosello è uno strumento per mostrare e navigare nelle pagine del sito. Il componente include un carosello che passa in rassegna le immagini delle pagine al di sopra di un elenco di collegamenti di pagina. Modificate il componente per specificare le pagine da esporre e il comportamento del carosello.

Le immagini vengono visualizzate nel carosello per le pagine associate a un’immagine in un modo specifico. Quando le pagine non sono associate alle immagini, viene visualizzato solo l’elenco dei collegamenti.

![chlimage_1-151](assets/chlimage_1-151.png)

**scheda Proprietà carosello**

Configurare il comportamento del carosello:

* Velocità di riproduzione: Tempo, in millisecondi, entro il quale ogni immagine viene visualizzata prima della visualizzazione dell’immagine successiva.
* Tempo di transizione: La durata in millisecondi dell&#39;animazione per le transizioni di immagine.
* Stile comandi: Tipo di controlli per lo spostamento tra le immagini.

**scheda Proprietà elenco**

Specificate la modalità di generazione dell’elenco di pagine:

* Genera elenco con: Metodo da utilizzare per specificare le pagine da includere nel carosello. Vedere Creazione dell&#39;elenco di pagine.
* Ordina per: Selezionare una proprietà pagina da utilizzare per ordinare l&#39;elenco di pagine. Ad esempio, selezionate jcr:title per ordinare le pagine in ordine alfabetico per titolo.
* Limite: Il numero massimo di pagine da includere. Questa proprietà è appropriata per i metodi basati sulla ricerca per la creazione dell&#39;elenco di pagine.

#### Creazione dell&#39;elenco di pagine {#building-the-page-list}

Il componente Scorrimento del carosello contiene i seguenti valori per la proprietà Genera elenco tramite. La finestra di dialogo di modifica cambia in base al valore selezionato:

**Pagine figlie**

Il componente elenca tutte le pagine figlie di una pagina specifica. Dopo aver selezionato questo valore, selezionare la pagina nella scheda Pagine figlie o non specificare alcun valore per elencare gli elementi secondari della pagina corrente.

**Elenco fisso**

Specificate un elenco di pagine di inclusione. Dopo aver selezionato questo valore, configurare l&#39;elenco nella scheda Elenco fisso che viene visualizzata quando si seleziona Elenco fisso:

* Per aggiungere una pagina, fate clic su Aggiungi elemento, quindi individuate la pagina.
* Utilizzate le icone freccia su e freccia giù per spostare la pagina all&#39;interno dell&#39;elenco.
* Fate clic sul pulsante Rimuovi per rimuovere una pagina dall’elenco.

La proprietà Order By non influisce sull&#39;ordine degli elenchi fissi.

**Ricerca**

Compilare l’elenco utilizzando i risultati di una ricerca per parole chiave. La ricerca viene eseguita negli elementi secondari di una pagina specificata:

1. Per specificare la pagina principale della ricerca, utilizzare la proprietà Inizia in per selezionare il percorso della pagina. Non specificare alcun percorso di ricerca sotto la pagina corrente.
1. Nella proprietà Query di ricerca, immettere le parole chiave di ricerca.

**Ricerca avanzata**

Compilare l&#39;elenco utilizzando una query [Querybuilder](/help/sites-developing/querybuilder-api.md).

### Immagine {#image}

Aggiungete un&#39;immagine al contenuto dell&#39;applicazione.

### Testo {#text}

Aggiungere testo RTF al contenuto dell&#39;applicazione.

### Località negozio {#store-locations}

Il componente Store Locations (Posizioni nello store) offre agli utenti gli strumenti per trovare punti vendita:

* Ricerca
* Elenca le posizioni vicine o distanti dalle coordinate GPS del dispositivo.

Il componente richiede che il repository contenga informazioni sulla posizione per ogni store. Le posizioni di esempio sono installate nel nodo /etc/commerce/locations/adobe. ![chlimage_1-152](assets/chlimage_1-152.png)

### Riga a due colonne {#two-column-row}

Consente di aggiungere componenti affiancati a una pagina.

![chlimage_1-153](assets/chlimage_1-153.png)
