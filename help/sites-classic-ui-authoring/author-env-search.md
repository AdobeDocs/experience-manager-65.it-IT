---
title: Ricerca
description: L’ambiente di authoring di AEM offre vari metodi per la ricerca dei contenuti, a seconda del tipo di risorsa.
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 10%

---

# Ricerca{#searching}

L’ambiente di authoring di AEM offre vari metodi per la ricerca dei contenuti, a seconda del tipo di risorsa.

>[!NOTE]
>
>Al di fuori dell’ambiente di authoring sono disponibili anche altri meccanismi per la ricerca, come [Query Builder](/help/sites-developing/querybuilder-api.md) e [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Informazioni di base sulla ricerca {#search-basics}

Per accedere al pannello di ricerca, fai clic sul pulsante **Ricerca** nella parte superiore del riquadro a sinistra della console appropriata.

![chlimage_1-101](assets/chlimage_1-101.png)

Il pannello di ricerca consente di effettuare ricerche in tutte le pagine del sito web. Contiene campi e widget per i seguenti elementi:

* **Testo completo**: Cerca il testo specificato
* **Modificato dopo/prima**: Cerca solo nelle pagine modificate tra date specifiche
* **Modello**: Cerca solo le pagine basate sul modello specificato
* **Tag**: Cerca solo nelle pagine con i tag specificati

>[!NOTE]
>
>Quando l’istanza è configurata per [Ricerca Lucene](/help/sites-deploying/queries-and-indexing.md) puoi utilizzare quanto segue in **Testo completo**:
>
>* [Caratteri jolly](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [Operatori booleani](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [Espressioni regolari](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [Raggruppamento campi](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [Incremento](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>


Esegui la ricerca facendo clic su **Ricerca** nella parte inferiore del riquadro. Fai clic su **Reimposta** per cancellare i criteri di ricerca.

## Filtro {#filter}

In varie posizioni è possibile impostare (e cancellare) un filtro per approfondire e perfezionare la visualizzazione:

![chlimage_1-102](assets/chlimage_1-102.png)

## Trova e sostituisci {#find-and-replace}

In **Siti Web** console a **Trova e sostituisci** l’opzione di menu consente di cercare e sostituire più istanze di una stringa all’interno di una sezione del sito web.

1. Selezionare la pagina o la cartella principale in cui si desidera eseguire l’azione Trova e sostituisci.
1. Seleziona **Strumenti** then **Trova e sostituisci**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. La **Trova e sostituisci** la finestra di dialogo effettua le seguenti operazioni:

   * conferma il percorso principale in cui deve iniziare l&#39;azione di ricerca
   * definisce il termine da trovare
   * definisce il termine che deve sostituirlo
   * indica se la ricerca deve fare distinzione tra maiuscole e minuscole
   * indica se devono essere trovate solo parole intere (in caso contrario vengono trovate anche le sottostringhe)

   Clic **Anteprima** elenchi in cui è stato trovato il termine. È possibile selezionare o deselezionare istanze specifiche da sostituire:

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. Fai clic su **Sostituisci** per sostituire effettivamente tutte le istanze. Viene richiesto di confermare l’operazione.

L’ambito predefinito del servlet di ricerca e sostituzione include le seguenti proprietà:

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

L’ambito può essere modificato utilizzando la console di gestione web Apache Felix (ad esempio, in `https://localhost:4502/system/console/configMgr`). Seleziona `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` e configura l&#39;ambito come necessario.

>[!NOTE]
>
>In un’installazione standard AEM Trova e sostituisci utilizza Lucene per la funzionalità di ricerca.
>
>Lucene indicizza le proprietà delle stringhe con lunghezza fino a 16 k. Per le stringhe di lunghezza superiore a tale valore la ricerca non viene eseguita.
