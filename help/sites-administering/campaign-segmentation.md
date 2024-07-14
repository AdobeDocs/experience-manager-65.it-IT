---
title: Configurazione della segmentazione
description: Scopri come configurare la segmentazione per AEM Campaign.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 7%

---


# Configurazione della segmentazione {#configuring-segmentation}

>[!NOTE]
>
>Questo documento descrive la configurazione della segmentazione utilizzata con ClientContext. Per configurare i segmenti con ContextHub utilizzando l&#39;interfaccia utente touch, vedi [Configurazione della segmentazione con ContextHub](/help/sites-administering/segmentation.md).

La segmentazione è un concetto chiave per la creazione di una campagna. Per informazioni sul funzionamento della segmentazione e sui termini chiave, consulta il [glossario sulla segmentazione](/help/sites-authoring/segmentation-overview.md).

A seconda delle informazioni già raccolte sui visitatori del sito e degli obiettivi che desideri raggiungere, devi definire i segmenti e le strategie necessarie per i contenuti di destinazione.

Questi segmenti verranno poi utilizzati per fornire al visitatore i contenuti di destinazione più pertinenti. Questo contenuto viene mantenuto nella sezione [Campagne](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) del sito Web. Le pagine teaser definite qui possono essere incluse come paragrafi teaser in qualsiasi pagina e definiscono a quale segmento di visitatore è applicabile il contenuto specializzato.

AEM consente di creare e aggiornare facilmente segmenti, teaser e campagne. Consente inoltre di verificare i risultati delle definizioni.

L&#39;**Editor segmenti** ti consente di definire facilmente un segmento:

![Finestra dell&#39;Editor segmenti](assets/segmenteditor.png)

È possibile **Modificare** ogni segmento per specificare un fattore **Titolo**, **Descrizione** e **Incremento**. Utilizzando la barra laterale puoi aggiungere i contenitori **AND** e **OR** per definire la **Logica segmento**, quindi aggiungere le **Caratteristiche segmento** richieste per definire i criteri di selezione.

## Fattore di incremento {#boost-factor}

Ogni segmento ha un parametro **Incrementa** utilizzato come fattore di ponderazione; un numero più alto indica che il segmento verrà selezionato al posto di un segmento con un numero più basso.

* Valore minimo: `0`
* Valore massimo: `1000000`

## Logica del segmento {#segment-logic}

I seguenti contenitori logici sono disponibili come predefiniti e ti consentono di creare la logica della selezione dei segmenti. Possono essere trascinati dalla barra laterale all’editor:

<table>
 <tbody>
  <tr>
   <td> Contenitore AND<br /> </td>
   <td> Operatore AND booleano.<br /> </td>
  </tr>
  <tr>
   <td> Contenitore OR<br /> </td>
   <td> Operatore OR booleano.</td>
  </tr>
 </tbody>
</table>

## Caratteristiche segmento {#segment-traits}

Le seguenti caratteristiche del segmento sono disponibili come predefinite e possono essere trascinate dalla barra laterale all’editor:

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
   <td>Riferimento a un'altra definizione di segmento.<br /> </td>
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

Puoi combinare queste caratteristiche utilizzando gli operatori booleani OR e AND (vedi [Creazione di un nuovo segmento](#creating-a-new-segment)) per definire lo scenario esatto per la selezione di questo segmento.

Quando l’intera istruzione restituisce true, questo segmento è stato risolto. Se sono presenti più segmenti applicabili, viene utilizzato anche il fattore **[Incrementa](/help/sites-administering/campaign-segmentation.md#boost-factor)**.

>[!CAUTION]
>
>L’editor segmento non verifica la presenza di riferimenti circolari. Ad esempio, il segmento A fa riferimento a un altro segmento B, che a sua volta fa riferimento al segmento A. Assicurati che i segmenti non contengano riferimenti circolari.

>[!NOTE]
>
>Le proprietà con il suffisso **_i18n** sono impostate da uno script che fa parte di clientlib dell&#39;interfaccia utente di personalizzazione. Tutte le clientlibs relative all’interfaccia utente vengono caricate sull’autore solo perché l’interfaccia utente non è necessaria al momento della pubblicazione.
>
>Pertanto, durante la creazione di un segmento con tali proprietà è in genere necessario fare affidamento su **browserFamily** per l&#39;istanza invece di **browserFamily_i18n**.

### Creazione di un nuovo segmento {#creating-a-new-segment}

Per definire il nuovo segmento:

1. Nella barra scegliere **Strumenti > Operazioni > Configurazione**.
1. Fai clic sulla pagina **Segmentazione** nel riquadro a sinistra e passa alla posizione desiderata.
1. Crea una [nuova pagina](/help/sites-authoring/editing-content.md#creatinganewpage) utilizzando il modello **Segmento**.
1. Apri la nuova pagina per visualizzare l’editor di segmenti:

   ![Primo passaggio della creazione di un segmento nell&#39;Editor segmenti](assets/screen_shot_2012-02-02at101726am.png)

1. Utilizza la barra laterale o il menu di scelta rapida (in genere facendo clic con il pulsante destro del mouse e selezionando **Nuovo...** per aprire la finestra Inserisci nuovo componente) per trovare la caratteristica del segmento necessaria. Trascinarlo quindi nell&#39;**Editor segmenti** per visualizzarlo nel contenitore predefinito **AND**.
1. Fare doppio clic sulla nuova caratteristica per modificare i parametri specifici, ad esempio la posizione del mouse:

   ![Modifica di un componente nell&#39;Editor segmenti](assets/screen_shot_2012-02-02at103135am.png)

1. Fai clic su **OK** per salvare la definizione:
1. Puoi **modificare** la definizione del segmento per assegnargli un fattore **Titolo**, **Descrizione** e **[Incremento](#boost-factor)**:

   ![Modifica delle impostazioni del segmento nell&#39;Editor segmenti](assets/screen_shot_2012-02-02at103547am.png)

1. Se necessario, aggiungi altre caratteristiche. È possibile formulare espressioni booleane utilizzando i componenti **AND Container** e **OR Container** trovati in **Segment Logic**. Con l’editor segmento è possibile eliminare caratteristiche o contenitori non più necessari o trascinarli in nuove posizioni all’interno dell’istruzione.

### Utilizzo dei contenitori AND e OR {#using-and-and-or-containers}

Puoi costruire segmenti complessi in AEM. È utile tenere presenti alcuni punti di base:

* Il livello superiore della definizione è sempre il contenitore AND creato inizialmente; questo non può essere modificato, ma non ha alcun effetto sul resto della definizione del segmento.
* Assicurati che la nidificazione del contenitore abbia una logica. I contenitori possono essere visualizzati come parentesi dell’espressione boolean.

L’esempio seguente viene utilizzato per selezionare i visitatori che sono:

Maschio e età compresa tra 16 e 65 anni

OR

Femmina e di età compresa tra 16 e 62 anni

Poiché l&#39;operatore principale è OR, è necessario iniziare con un contenitore **OR**. All&#39;interno di questo si hanno 2 istruzioni AND, per ognuna di queste è necessario un **contenitore AND**, in cui è possibile aggiungere le singole caratteristiche.

![Esempio di operatori AND e OR nell&#39;Editor segmenti](assets/screen_shot_2012-02-02at105145am.png)

## Test dell’applicazione di un segmento {#testing-the-application-of-a-segment}

Una volta definito il segmento, è possibile testare i risultati potenziali con l&#39;aiuto di **[ClientContext](/help/sites-administering/client-context.md)**:

1. Seleziona il segmento da testare.
1. Premere **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** per aprire **[ClientContext](/help/sites-administering/client-context.md)**, che mostra i dati raccolti. A scopo di test puoi **Modificare** determinati valori o **Caricare** un altro profilo per vederne l&#39;impatto.

1. A seconda delle caratteristiche definite, i dati disponibili per la pagina corrente possono corrispondere o meno alla definizione del segmento. Lo stato della corrispondenza viene visualizzato sotto la definizione.

Ad esempio, una semplice definizione del segmento può essere basata sull’età e sul sesso dell’utente. Il caricamento di un profilo specifico mostra che il segmento è stato risolto correttamente:

![Utilizzo della finestra ClientContext per testare un&#39;operazione di segmentazione AND](assets/screen_shot_2012-02-02at105926am.png)

Oppure no:

![Utilizzo della finestra ClientContext per testare un&#39;operazione NOT segmentation](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>Tutte le caratteristiche vengono risolte immediatamente, anche se la maggior parte si modifica solo al ricaricamento della pagina. Le modifiche apportate alla posizione del mouse sono immediatamente visibili e risultano quindi utili a scopo di test.

Tali test possono essere eseguiti anche sulle pagine di contenuto e in combinazione con i componenti **Teaser**.

Passando il puntatore del mouse su un paragrafo teaser verranno visualizzati i segmenti applicati, indipendentemente dal fatto che siano attualmente risolti e quindi il motivo per cui è stata selezionata l’istanza teaser corrente:

![Un esempio di passaggio del mouse su un segmento](assets/chlimage_1-47.png)

### Utilizzo del segmento {#using-your-segment}

I segmenti sono attualmente utilizzati in [Campagne](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). Vengono utilizzati per gestire il contenuto effettivo visualizzato da un pubblico specifico. Per ulteriori informazioni, consulta [Informazioni sui segmenti](/help/sites-authoring/segmentation-overview.md).
