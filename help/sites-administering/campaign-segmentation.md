---
title: Configurazione della segmentazione
seo-title: Configurazione della segmentazione
description: Scopri come configurare la segmentazione per AEM Campaign.
seo-description: Scopri come configurare la segmentazione per AEM Campaign.
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 3%

---


# Configurazione della segmentazione {#configuring-segmentation}

>[!NOTE]
>
>Questo documento descrive la configurazione della segmentazione utilizzata con ClientContext. Per configurare i segmenti con ContextHub utilizzando l&#39;interfaccia utente touch, consultate [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md) (Configurazione della segmentazione con ContextHub).

La segmentazione è un concetto chiave per la creazione di una campagna. Per informazioni sul funzionamento della segmentazione e sui termini chiave, vedere [Glossario di segmentazione](/help/sites-authoring/segmentation-overview.md).

A seconda delle informazioni già raccolte sui visitatori del sito e degli obiettivi da raggiungere, dovrete definire i segmenti e le strategie necessari per il contenuto di destinazione.

Questi segmenti vengono quindi utilizzati per fornire a un visitatore contenuto con targeting specifico. Questo contenuto viene mantenuto nella sezione [Campagne](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) del sito Web. Le pagine teaser qui definite possono essere incluse come paragrafi teaser in qualsiasi pagina e definire per quale segmento di visitatori si applica il contenuto specializzato.

AEM consente di creare e aggiornare facilmente segmenti, teaser e campagne. Consente inoltre di verificare i risultati delle definizioni.

L&#39; **Editor segmento** consente di definire facilmente un segmento:

![](assets/segmenteditor.png)

È possibile **modificare** ogni segmento per specificare un fattore **Titolo**, **Descrizione** e **Incrementa**. Utilizzando la barra laterale potete aggiungere i contenitori **AND** e **OR** per definire la logica del segmento **e quindi aggiungere le** Caratteristiche del segmento **necessarie per definire i criteri di selezione.**

## Fattore di incremento {#boost-factor}

Ogni segmento ha un parametro **Boost** utilizzato come fattore di ponderazione; un numero più alto indica che il segmento verrà selezionato preferibilmente a un segmento con un numero inferiore.

* Valore minimo: `0`
* Valore massimo: `1000000`

## Logica segmento {#segment-logic}

I seguenti contenitori logici sono disponibili out-of-the-box e consentono di creare la logica della selezione dei segmenti. È possibile trascinarli dalla barra laterale all’editor:

<table>
 <tbody>
  <tr>
   <td> Contenitore E<br /> </td>
   <td> Operatore AND booleano.<br /> </td>
  </tr>
  <tr>
   <td> Contenitore O<br /> </td>
   <td> Operatore OR booleano.</td>
  </tr>
 </tbody>
</table>

## Caratteristiche del segmento {#segment-traits}

Sono disponibili le seguenti caratteristiche del segmento out-of-the-box; possono essere trascinati dalla barra laterale all’editor:

<table>
 <tbody>
  <tr>
   <td> Intervallo IP<br /> </td>
   <td>Definisce un intervallo di indirizzi IP che il visitatore può avere.<br /> </td>
  </tr>
  <tr>
   <td> Hit pagina<br /> </td>
   <td>Con quale frequenza è stata richiesta la pagina. <br /> </td>
  </tr>
  <tr>
   <td> Proprietà pagina<br /> </td>
   <td>Qualsiasi proprietà della pagina visitata.<br /> </td>
  </tr>
  <tr>
   <td> Parole chiave di riferimento<br /> </td>
   <td>Parole chiave da associare alle informazioni del sito Web di provenienza. <br /> </td>
  </tr>
  <tr>
   <td> Script</td>
   <td>Espressione JavaScript da valutare.<br /> </td>
  </tr>
  <tr>
   <td> Riferimento segmento <br /> </td>
   <td>Riferimento a un'altra definizione del segmento.<br /> </td>
  </tr>
  <tr>
   <td> Tag cloud<br /> </td>
   <td>Tag da associare a quelli delle pagine visitate.<br /> </td>
  </tr>
  <tr>
   <td> Età utente<br /> </td>
   <td>Come tratto dal profilo utente.<br /> </td>
  </tr>
  <tr>
   <td> Proprietà utente<br /> </td>
   <td>Qualsiasi altra informazione disponibile nel profilo utente. </td>
  </tr>
 </tbody>
</table>

È possibile combinare queste caratteristiche utilizzando gli operatori booleani OR e AND (vedere [Creazione di un nuovo segmento](#creating-a-new-segment)) per definire lo scenario esatto per la selezione di questo segmento.

Quando l&#39;intera istruzione restituisce true, il segmento è stato risolto. Se sono applicabili più segmenti, viene utilizzato anche il fattore **[Incrementa](/help/sites-administering/campaign-segmentation.md#boost-factor)**.

>[!CAUTION]
>
>L&#39;editor segmenti non verifica la presenza di riferimenti circolari. Ad esempio, il segmento A fa riferimento a un altro segmento B, che a sua volta fa riferimento al segmento A. Devi accertarti che i tuoi segmenti non contengano riferimenti circolari.

>[!NOTE]
>
>Le proprietà con il suffisso **_i18n** sono impostate da uno script che fa parte della clientlib dell&#39;interfaccia utente della personalizzazione. Tutti i clientlibs relativi all’interfaccia utente vengono caricati solo sull’autore, poiché l’interfaccia utente non è necessaria al momento della pubblicazione.
>
>Pertanto, quando si crea un segmento con tali proprietà è normalmente necessario fare affidamento su **browserFamily**, ad esempio invece di **browserFamily_i18n**.

### Creazione di un nuovo segmento {#creating-a-new-segment}

Per definire il nuovo segmento:

1. Nella barra laterale, scegliete **Strumenti > Operazioni > Configurazione**.
1. Fare clic sulla pagina **Segmentazione** nel riquadro a sinistra e passare alla posizione desiderata.
1. Create una nuova pagina [nuova](/help/sites-authoring/editing-content.md#creatinganewpage) utilizzando il modello **Segment**.
1. Apri la nuova pagina per visualizzare l’editor segmenti:

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. Utilizzate la barra laterale o il menu di scelta rapida (in genere fate clic con il pulsante destro del mouse, quindi selezionate **Nuovo...** per aprire la finestra Inserisci nuovo componente) per trovare la caratteristica del segmento desiderata. Trascinala quindi nell&#39; **Editor segmento** che verrà visualizzato nel contenitore **AND** predefinito.
1. Fare doppio clic sulla nuova caratteristica per modificare i parametri specifici; ad esempio la posizione del mouse:

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. Fare clic su **OK** per salvare la definizione:
1. È possibile **modificare** la definizione del segmento per assegnargli un fattore **Titolo**, **Descrizione** e **[Incrementa](#boost-factor)**:

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. Se necessario, aggiungete altre caratteristiche. È possibile formulare espressioni booleane utilizzando i componenti **AND Container** e **OR Container** presenti in **Segment Logic**. Con l&#39;editor segmenti è possibile eliminare caratteristiche o contenitori non più necessari, oppure trascinarli in nuove posizioni all&#39;interno dell&#39;istruzione.

### Utilizzo di AND e OR Containers {#using-and-and-or-containers}

Puoi creare segmenti complessi in AEM. È utile conoscere alcuni punti fondamentali:

* Il livello principale della definizione è sempre il contenitore AND creato inizialmente; questo non può essere modificato, ma non ha un effetto sul resto della definizione del segmento.
* Verificare che la nidificazione del contenitore abbia senso. I contenitori possono essere visualizzati come parentesi dell&#39;espressione booleana.

L&#39;esempio seguente viene utilizzato per selezionare i visitatori:

Maschio e tra i 16 e i 65 anni

OPPURE

Femmina e tra i 16 e i 62 anni

Poiché l&#39;operatore principale è OR è necessario iniziare con un **OR Container**. All&#39;interno di questo sono presenti 2 istruzioni AND, per ognuna di queste è necessario un **AND Container**, in cui è possibile aggiungere le singole caratteristiche.

![](assets/screen_shot_2012-02-02at105145am.png)

## Verifica dell&#39;applicazione di un segmento {#testing-the-application-of-a-segment}

Una volta definito il segmento, i potenziali risultati possono essere testati con l&#39;aiuto di **[Client Context](/help/sites-administering/client-context.md)**:

1. Selezionare il segmento da sottoporre a test.
1. Premere **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** per aprire il **[Client Context](/help/sites-administering/client-context.md)**, che mostra i dati raccolti. A scopo di test è possibile **modificare** alcuni valori, oppure **caricare** un altro profilo per vedere l&#39;impatto di tali valori.

1. A seconda delle caratteristiche definite, i dati disponibili per la pagina corrente potrebbero non corrispondere alla definizione del segmento. Lo stato della corrispondenza viene visualizzato sotto la definizione.

Ad esempio, una semplice definizione del segmento può essere basata sull’età e sul genere dell’utente. Il caricamento di un profilo specifico mostra che il segmento è stato risolto correttamente:

![](assets/screen_shot_2012-02-02at105926am.png)

Oppure no:

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>Tutte le caratteristiche vengono risolte immediatamente, anche se la maggior parte delle modifiche apportate al ricaricamento della pagina. Le modifiche alla posizione del mouse sono visibili immediatamente, e sono quindi utili a scopo di test.

Tali test possono essere eseguiti anche sulle pagine di contenuto e in combinazione con i componenti **Teaser**.

Quando si passa il mouse su un paragrafo teaser, vengono visualizzati i segmenti applicati, a prescindere dal fatto che siano attualmente risolti e quindi dal motivo per cui è stata selezionata l’istanza teaser corrente:

![](assets/chlimage_1-47.png)

### Utilizzo del segmento {#using-your-segment}

I segmenti sono attualmente utilizzati all&#39;interno di [Campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). Vengono utilizzati per indirizzare il contenuto effettivo visualizzato da audience target specifiche. Per ulteriori informazioni, vedere [Informazioni sui segmenti](/help/sites-authoring/segmentation-overview.md).
