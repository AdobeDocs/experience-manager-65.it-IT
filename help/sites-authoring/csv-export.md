---
title: 'Esportazione in formato CSV  '
seo-title: 'Esportazione in formato CSV  '
description: Esporta informazioni sulle pagine in un file CSV sul sistema locale
seo-description: Esporta informazioni sulle pagine in un file CSV sul sistema locale
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
translation-type: tm+mt
source-git-commit: 317093bce043ff2aaa5b5ceb8499f057fa9fa24b
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 86%

---


# Esportazione in formato CSV  {#export-to-csv}

**Crea rapporto CSV** consente di esportare le informazioni contenute nelle pagine in un file CSV nel sistema locale.

* Il nome del file scaricato è `export.csv`
* Il contenuto dipende dalle proprietà selezionate.
* Puoi definire il percorso e il livello di profondità dell’esportazione.

>[!NOTE]
>
>Vengono utilizzate la funzione di download e la destinazione predefinita del browser in uso.

La procedura guidata **Crea esportazione CSV** permette di selezionare:

* Proprietà da esportare
   * Metadati
      * Nome
      * Modificato
      * Pubblicato
      * Modello
      * Flusso di lavoro
   * Traduzione
      * Tradotto
   * Analisi
      * Visualizzazioni pagina
      * Visitatori univoci
      * Tempo sulla pagina
* Profondità
   * Percorso principale
   * Solo elementi figlio diretti
   * Livelli aggiuntivi di elementi figlio
   * Livelli

Il file `export.csv` risultante può essere aperto in Excel o in un’altra applicazione compatibile.

![etc-01](assets/etc-01.png)

L&#39;opzione Crea rapporto CSV **è disponibile quando si sfoglia la console** Siti **(in vista Elenco): è un&#39;opzione del menu a discesa** Crea **:**

![etc-02](assets/etc-02.png)

Per creare un’esportazione CSV:

1. Apri la console **Sites** e passa alla posizione desiderata, se necessario.
1. Dalla barra degli strumenti, seleziona **Crea**, quindi **Rapporto CSV** per aprire la procedura guidata:

   ![etc-03](assets/etc-03.png)

1. Seleziona le proprietà da esportare.
1. Seleziona **Crea**.
