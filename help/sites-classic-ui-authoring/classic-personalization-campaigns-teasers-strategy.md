---
title: Teaser e strategie
seo-title: Teasers and Strategies
description: Per le campagne vengono spesso utilizzati i teaser per veicolare uno specifico segmento di visitatori verso contenuti che corrispondono ai loro interessi. Per una specifica campagna è possibile definire uno o più teaser.
seo-description: Campaigns often use teasers as a mechanism to entice a specific segment of the visitor population through to content focused on their interests. One or more teasers are defined for a specific campaign.
uuid: c78ec858-4b0a-48d5-99b2-5ddd9e15183d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7f378b94-5233-4358-8d93-a7b3386df00b
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 89%

---

# Teaser e strategie{#teasers-and-strategies}

Per le campagne vengono spesso utilizzati i teaser per veicolare uno specifico segmento di visitatori verso contenuti che corrispondono ai loro interessi. Per una specifica campagna è possibile definire uno o più teaser.

>[!NOTE]
>
>Il componente Teaser è diventato obsoleto in AEM 6.2. Al suo posto, utilizza il [componente Target](/help/sites-authoring/content-targeting-touch.md).

* **Pagine dei marchi** sono memorizzate nella sezione Campagne del sito web. Un marchio contiene le singole campagne.
* **Pagine di Campaign** sono memorizzate nella sezione Campagne del sito web. Ciascuna campagna ha una singola pagina, nella quale vengono memorizzate le definizioni dei teaser. La pagina contenitore, o di panoramica, contiene alcune informazioni e dati statistici sulle singole pagine teaser.

I teaser in AEM sono composti di diverse parti:

* **Pagine teaser** sono memorizzati nella pagina della campagna appropriata e contengono le definizioni dei paragrafi teaser disponibili per ogni campagna specifica. Tali definizioni sono usate per visualizzare i paragrafi teaser, comprese le varianti dei contenuti, il segmento che determina la selezione di una variante e il fattore di incremento.
* Il **componente Teaser** è fornito con il prodotto e permette di creare un’istanza del paragrafo teaser in una pagina di contenuto. Per creare un paragrafo teaser, trascina il componente teaser dalla barra laterale, quindi specifica la definizione. **Nota:** Il componente Teaser è stato dichiarato obsoleto in AEM 6.2. Utilizza il [Componente Target](/help/sites-authoring/content-targeting-touch.md) invece.
* I **paragrafi teaser** sono istanze effettive del teaser in una pagina di contenuto. Hanno il ruolo di invitare un segmento di utenti a visitare contenuti particolari, in base ai loro interessi.
* Pagine con il contenuto della campagna per un particolare segmento di visitatori. I paragrafi teaser invitano gli utenti a visitare queste pagine.

## Strategie {#strategies}

Quando si aggiunge un paragrafo teaser a una pagina, è necessario definire la **Strategia**.

Questo parametro serve qualora siano disponibili per la selezione più teaser in seguito alla risoluzione di tutti i segmenti ad essi associati. Con la **Strategia** viene quindi specificato un ulteriore criterio per selezionare il teaser da mostrare:

* **Punteggio clickstream**: si basa sui tag e sugli hit di tag correlati presenti nel ClientContext del visitatore (mostra la frequenza con cui il visitatore ha fatto clic su pagine contenenti il relativo tag). Vengono confrontate le frequenze dei tag definiti nella pagina teaser.
* **Casuale**, per una selezione &quot;casuale&quot;; utilizza il fattore casuale generato per una pagina, visibile con [contesto client](/help/sites-administering/client-context.md).
* **Primo** nell’elenco dei segmenti risolti. L’ordine corrisponde a quello dei teaser nella pagina contenitore della campagna.

La [Fattore di incremento](/help/sites-administering/campaign-segmentation.md#boost-factor) del segmento ha anche un impatto sulla selezione. Si tratta di un fattore di rilevanza aggiunto a una definizione di segmento per aumentare o ridurre la probabilità che venga selezionato.

È più facile illustrare il processo e le interrelazioni dei vari criteri di selezione tramite un esempio (utile anche per verificare che i teaser creati vengano visualizzati dal pubblico richiesto).

Considerate i seguenti segmenti, già creati e a cui sia già stato assegnato un fattore di incremento:

| Segmento | Fattore di incremento |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

Considerate inoltre le seguenti definizioni di teaser:

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
   <td>Business, Marketing</td>
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

Se si applica questo a un visitatore con le seguenti caratteristiche:

* **S1**, **S2** e **S6** risolvere

* Il tag **marketing** ha 3 hit
* Il tag **business** ha 6 hit

Risultato:

* corrispondenza positiva: alcuni dei segmenti assegnati al teaser vengono risolti per il visitatore corrente?
* fattore di incremento: fattore di incremento maggiore tra tutti i segmenti applicabili
* punteggio clickstream: totale cumulativo per tutti gli hit di tag applicabili

calcolati prima di applicare la strategia appropriata:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Segmenti assegnati</td>
   <td>Tag </td>
   <td>Corrispondenza positiva?</td>
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
   <td>Business</td>
   <td>Sì</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

Questi valori vengono usati per determinare i teaser che verranno mostrati al visitatore, a seconda della **Strategia** applicata al paragrafo teaser:

<table>
 <tbody>
  <tr>
   <td>Strategia</td>
   <td>Teaser risultante</td>
   <td>Commenti</td>
  </tr>
  <tr>
   <td>Primo</td>
   <td>T5</td>
   <td>Vengono considerati solo T5 e T6 perché tutti i loro segmenti vengono risolti <i>e inoltre</i> hanno il fattore di incremento maggiore. L’elenco restituito è nell’ordine T5, T6; quindi T5 viene selezionato e mostrato al visitatore.</td>
  </tr>
  <tr>
   <td>Casuale</td>
   <td>T5 o T6</td>
   <td>Entrambi i teaser hanno segmenti che vengono risolti e lo stesso fattore di incremento. Vengono quindi mostrati in ugual proporzione.</td>
  </tr>
  <tr>
   <td>Punteggio clickstream</td>
   <td>T6</td>
   <td><p>Per il visitatore vengono risolti i segmenti T1, T4, T5 e T6. I fattori di incremento maggiori di T5 e T6 escludono pertanto T1 e T4. Infine, a causa del suo punteggio clickstream maggiore, viene selezionato T6.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se, dopo le tecniche di risoluzione di cui sopra, restano disponibili per la selezione più teaser, mediante una selezione casuale interna verrà selezionato per la visualizzazione un singolo teaser.
>
>Ad esempio, se la strategia prevista è Punteggio clickstream e T5 ha lo stesso punteggio di T6 (ossia 6, anziché 3 dell’esempio qui sopra), viene utilizzata la selezione casuale interna per selezionare uno dei due.

Le pagine o i paragrafi teaser vengono utilizzati per indirizzare alcuni segmenti di visitatori verso contenuti pertinenti in base ai loro interessi. Possono presentare al visitatore una serie di opzioni oppure un solo paragrafo teaser, a seconda del segmento di visitatori (ad esempio, in base all’età del visitatore).

In genere, una pagina teaser è impostata come azione temporanea con una specifica durata di tempo, dopodiché viene sostituita da una successiva pagina teaser.

Dopo aver creato un marchio e una campagna, puoi creare e impostare un’esperienza teaser.

### Creazione di un punto di contatto per il teaser {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>Il componente Teaser è diventato obsoleto in AEM 6.2. Al suo posto, utilizza il [componente Target](/help/sites-authoring/content-targeting-touch.md).

1. Passa alla pagina del contenuto in cui desideri inserire il paragrafo teaser che indirizzerà l’utente alla pagina della campagna.
1. Aggiungi un componente **Teaser** (dalla sezione **Personalizzazione** della barra laterale) nella posizione desiderata. Inizialmente il percorso della campagna non sarà ancora configurato:

   ![chlimage_1](assets/chlimage_1.png)

1. Modifica il componente teaser e aggiungi i seguenti parametri:

   * **Percorso campagna** Percorso della pagina della campagna contenente la singola pagina teaser; i segmenti determinano esattamente quale teaser viene visualizzato.

   * **[Strategia](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)** Metodo utilizzato per la selezione quando più segmenti vengono risolti con successo.
   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Fai clic su **OK** per salvare. Il contenuto visualizzato dipende dai segmenti impostati per il teaser e dal profilo utente con cui è stato effettuato l’accesso:

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Passa il mouse sul paragrafo teaser per visualizzare l’icona del punto interrogativo (nell’angolo in basso a destra del componente). Fai clic su tale icona per visualizzare i segmenti applicati e verificare se vengono attualmente risolti.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Panoramica sui teaser {#teaser-overview}

Come nella vista della campagna in MCM, anche la pagina della campagna offre informazioni sui teaser associati:

1. Dalla console **Siti Web**, aprite la pagina della campagna, ad esempio:

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   Viene visualizzata una panoramica delle definizioni del teaser e delle statistiche di visualizzazione:

   ![chlimage_1-4](assets/chlimage_1-4.png)
