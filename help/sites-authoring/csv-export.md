---
title: Esportazione in formato CSV
seo-title: Export to CSV
description: Esporta informazioni sulle pagine in un file CSV sul sistema locale
seo-description: Export information about your pages to a CSV file on your local system
uuid: 6eee607b-3510-4f6a-ba82-b27480a4fbe1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 7be506fb-f5c4-48dd-bec2-a3ea3ea19397
docset: aem65
exl-id: 18910143-f2f2-4cfe-88b9-651df90d9cb9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 85%

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
   * Analytics
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

La creazione **Rapporto CSV** è disponibile quando esplori la pagina **Sites** console (nella vista a elenco): è un&#39;opzione del **Crea** menu a discesa:

![etc-02](assets/etc-02.png)

Per creare un’esportazione CSV:

1. Apri la console **Sites** e passa alla posizione desiderata, se necessario.
1. Dalla barra degli strumenti, seleziona **Crea**, quindi **Rapporto CSV** per aprire la procedura guidata:

   ![etc-03](assets/etc-03.png)

1. Seleziona le proprietà da esportare.
1. Seleziona **Crea**.
