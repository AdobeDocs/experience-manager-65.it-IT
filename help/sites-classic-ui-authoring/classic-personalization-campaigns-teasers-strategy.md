---
title: Teaser e strategie
description: Le campagne utilizzano spesso i teaser come meccanismo per attrarre un segmento specifico della popolazione di visitatori, fino a contenuti incentrati sui loro interessi. Uno o più teaser sono definiti per una campagna specifica.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 3%

---

# Teaser e strategie{#teasers-and-strategies}

Le campagne utilizzano spesso i teaser come meccanismo per attrarre un segmento specifico della popolazione di visitatori, fino a contenuti incentrati sui loro interessi. Uno o più teaser sono definiti per una campagna specifica.

>[!NOTE]
>
>Il componente Teaser è ora obsoleto nell’AEM 6.2. Utilizzare invece il [componente Target](/help/sites-authoring/content-targeting-touch.md).

* **Le pagine del marchio** sono archiviate nella sezione Campagne del sito Web. Un brand contiene le singole campagne.
* **Le pagine della campagna** sono archiviate nella sezione Campagne del sito Web. Ogni campagna ha una singola pagina, in cui sono conservate le definizioni del teaser. La pagina contenitore, o panoramica, contiene anche determinate informazioni e statistiche relative alle singole pagine teaser.

I teaser all’interno dell’AEM sono composti da diverse parti:

* Le **pagine teaser** sono memorizzate nella pagina della campagna appropriata e contengono le definizioni dei paragrafi teaser disponibili per ogni campagna specifica. Queste definizioni vengono utilizzate quando vengono visualizzati i paragrafi del teaser, incluse le varianti di contenuto, il segmento da utilizzare per selezionare una variante e un fattore di incremento.
* Il componente **Teaser** è disponibile come strumento predefinito e consente di creare un&#39;istanza del paragrafo del teaser specifico in una pagina di contenuto. Puoi trascinare il componente teaser dalla barra laterale, quindi specificare la definizione del teaser per creare un paragrafo teaser personalizzato. **Nota:** il componente Teaser è ora obsoleto in AEM 6.2. Utilizzare invece il [componente Target](/help/sites-authoring/content-targeting-touch.md).
* **I paragrafi teaser** sono istanze effettive del teaser all&#39;interno di una pagina di contenuto. Questi attirano un segmento di visitatori fino a contenuti incentrati sui loro interessi.
* Le pagine che contengono il contenuto della campagna si concentrano su un segmento di visitatori specifico. Di solito, i paragrafi teaser portano il visitatore a tali pagine.

## Strategie {#strategies}

Quando si aggiunge un paragrafo teaser a una pagina, è necessario definire la **strategia**.

In questo caso, poiché i segmenti assegnati si risolvono tutti correttamente, sono disponibili diversi teaser da selezionare. La **Strategia** specifica quindi un criterio aggiuntivo utilizzato per selezionare il teaser mostrato:

* **Il punteggio clickstream** è basato sui tag e sugli hit di tag correlati presenti nel contesto client del visitatore (mostra la frequenza con cui un visitatore ha fatto clic su pagine che contengono il rispettivo tag). Vengono confrontate le percentuali di hit per i tag definiti nella pagina teaser.
* **Casuale**, per la selezione &quot;casuale&quot;; utilizza il fattore casuale generato per una pagina, visibile con il [contesto client](/help/sites-administering/client-context.md).
* **Primo** nell&#39;elenco dei segmenti risolti. L’ordine è quello dei teaser all’interno della pagina del contenitore della campagna.

Anche il [fattore di incremento](/help/sites-administering/campaign-segmentation.md#boost-factor) del segmento ha un impatto sulla selezione. Questo è un fattore di ponderazione aggiunto a una definizione di segmento per aumentare/diminuire la probabilità relativa che venga selezionata.

Il processo e le interrelazioni dei vari criteri di selezione sono meglio illustrati con un esempio (un metodo che può essere utilizzato anche per garantire che i teaser raggiungano il pubblico richiesto).

Se i seguenti segmenti sono già stati creati e assegnati al rispettivo Fattore di incremento:

| Segmento | Fattore di incremento |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

Utilizziamo inoltre le seguenti definizioni di teaser:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Segmenti assegnati</td>
   <td>Tag assegnati </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Business, marketing</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Business<br /> </td>
  </tr>
 </tbody>
</table>

Quindi, se applichiamo questo a un visitatore in cui:

* Risoluzione di **S1**, **S2 e &#x200B;** S6** completata

* il tag **marketing** ha tre hit
* il tag **business** ha sei hit

Possiamo vedere il risultato:

* corrispondenza riuscita: nessuno dei segmenti assegnati al teaser viene risolto correttamente per il visitatore corrente?
* fattore di incremento: il fattore di incremento più elevato di tutti i segmenti applicabili
* punteggio di clickstream: il totale cumulativo per tutti gli hit tag applicabili

calcolati prima di applicare la strategia appropriata:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Segmenti assegnati</td>
   <td>Tag </td>
   <td>Corrispondenza riuscita?</td>
   <td>Fattore di incremento risultante</td>
   <td>Punteggio clickstream risultante </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Business, marketing</td>
   <td>Sì</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>Sì</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
   <td>No</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
   <td>Sì<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
   <td>Sì</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Economia</td>
   <td>Sì</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

Questi valori vengono utilizzati per determinare i teaser che il visitatore vedrà, a seconda della **Strategia** applicata al paragrafo teaser:

<table>
 <tbody>
  <tr>
   <td>Strategia</td>
   <td>Teaser risultante</td>
   <td>Commenti</td>
  </tr>
  <tr>
   <td>Primo/a</td>
   <td>T5</td>
   <td>Solo T5 e T6 sono considerati come i loro segmenti tutti risolvono <i>e</i> hanno il fattore di incremento più alto. L'elenco restituito è nell'ordine T5, T6; quindi T5 viene selezionato e mostrato.</td>
  </tr>
  <tr>
   <td>Casuale</td>
   <td>T5 o T6</td>
   <td>Entrambi i teaser hanno segmenti che si risolvono tutti e lo stesso fattore di incremento. Pertanto, i due teaser vengono visualizzati in proporzione uguale.</td>
  </tr>
  <tr>
   <td>Punteggio clickstream</td>
   <td>T6</td>
   <td><p>I segmenti per T1, T4, T5 e T6 si risolvono tutti per il visitatore. I fattori di incremento più elevati di T5 e T6 escludono quindi T1 e T4. Infine, il punteggio Clickstream più alto di T6 fa sì che questo venga selezionato.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se, dopo le tecniche di risoluzione di cui sopra, sono disponibili più teaser per la selezione, una selezione interna (casuale) selezionerà un singolo teaser per la visualizzazione.
>
>Ad esempio, se la strategia era Punteggio di clickstream e T5 aveva lo stesso Punteggio di clickstream di T6 (ovvero sei invece di tre), la selezione interna (casuale) sarebbe stata utilizzata per selezionare uno di questi due.

Le pagine/paragrafi teaser vengono utilizzate per indirizzare specifici segmenti di visitatori a contenuti incentrati sui loro interessi. Possono presentare una serie di opzioni tra cui scegliere il visitatore o mostrare un solo paragrafo teaser basato sul segmento specifico del visitatore. Ad esempio, il paragrafo del teaser mostrato può dipendere dall’età del visitatore.

In genere, una pagina teaser è un’azione temporanea che dura per un periodo di tempo specifico, fino a quando non viene sostituita dalla pagina teaser successiva.

Dopo aver creato il brand e la campagna, puoi creare e configurare l’esperienza teaser.

### Creazione di un punto di contatto per il teaser {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>Il componente Teaser è ora obsoleto nell’AEM 6.2. Utilizzare invece il [componente Target](/help/sites-authoring/content-targeting-touch.md).

1. Passa alla pagina del contenuto in cui desideri inserire il paragrafo del teaser che porterà alla pagina della campagna.
1. Aggiungi un componente **Teaser** (disponibile nella sezione **Personalization** della barra laterale) nella posizione desiderata. La prima volta che viene creato, mostra che il percorso della campagna non è ancora configurato:

   ![chlimage_1](assets/chlimage_1.png)

1. Modifica il componente teaser per aggiungere:

   * **Percorso campagna**
Percorso della pagina della campagna che contiene la pagina del singolo teaser; i segmenti determinano esattamente quale teaser viene visualizzato.

   * **[Strategia](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
Metodo utilizzato per la selezione quando più segmenti vengono risolti correttamente.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Fare clic su **OK** per salvare. A seconda dei segmenti impostati sul teaser e del profilo dell’utente attualmente connesso come, verrà visualizzato il contenuto appropriato:

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Passa il puntatore del mouse sul paragrafo teaser per visualizzare l’icona del punto interrogativo (angolo in basso a destra del componente). Fai clic su questo pulsante per visualizzare i segmenti applicati e se sono attualmente risolti.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Panoramica del teaser {#teaser-overview}

Oltre alla visualizzazione della campagna in MCM, la pagina della campagna fornisce anche informazioni sui teaser collegati:

1. Dalla console **Siti Web**, apri la pagina della campagna, ad esempio:

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   Qui viene mostrata una panoramica delle definizioni dei teaser e delle statistiche di visualizzazione:

   ![chlimage_1-4](assets/chlimage_1-4.png)
