---
title: Controllo collegamenti esterni
seo-title: Controllo collegamenti esterni
description: Ulteriori informazioni sul controllo dei collegamenti esterni in AEM.
seo-description: Ulteriori informazioni sul controllo dei collegamenti esterni in AEM.
uuid: 09160594-e45f-4604-8b36-f14b148b9f63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d1ccd194-8549-4188-8932-7136be1e88a2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# Controllo collegamenti esterni{#the-external-link-checker}

In AEM è disponibile un controllo esterno dei collegamenti. Controllo collegamenti:

* esegue la scansione di tutte le pagine di contenuto
* genera un elenco di tutti i collegamenti validi e non validi
* contrassegna i collegamenti non validi come interrotti in situ sulle singole pagine di contenuto

## Come convalidare collegamenti esterni {#how-to-validate-external-links}

Per utilizzare il controllo dei collegamenti esterni:

1. Utilizzando **Navigazione**, selezionare **Strumenti**, quindi **Siti**.
1. Selezionare **Controllo collegamenti esterni**. Viene generato un elenco di tutti i collegamenti esterni.
1. Convalida di un collegamento specifico selezionandolo nell&#39;elenco, quindi facendo clic su **Check**:

   ![](assets/telc-01.png)

   Vengono visualizzate le informazioni:

   * **Stato** del collegamento
   * **URL**
   * **Referrer**
   * tempo trascorso il quale il collegamento è stato **Ultimo controllo** (convalidato)
   * restituito il **Last Status**

   * tempo trascorso il quale il collegamento era **Ultimo disponibile**
   * tempo trascorso l&#39;accesso **Ultimo accesso**

1. Nelle singole pagine di contenuto, i collegamenti non validi vengono visualizzati come interrotti:

   ![](assets/chlimage_1-143.png)