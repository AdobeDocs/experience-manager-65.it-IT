---
title: Operazioni di elaborazione in blocco
description: Nullo
page-status-flag: never-activated
contentOwner: sarchiz
docset: aem65
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 1%

---


# Operazioni di elaborazione in blocco {#bulk-processing-operations}

## Introduzione {#introduction}

Con la versione più recente di Adobe Experience Manager (AEM), il pulsante Seleziona tutto è stato esteso a tutte le visualizzazioni: Elenco, Colonna e Scheda. Il pulsante Seleziona tutto ora seleziona tutto il contenuto di una determinata cartella o raccolta e non solo le risorse e le pagine caricate e visibili nel browser client.

Le azioni chiave sono state abilitate per l&#39;operazione in blocco: **Sposta**, **Elimina**, e **Copia**. Una nuova finestra di dialogo consente ai clienti di sapere per quali azioni l’elaborazione in blocco non è disponibile.

## Come Usare {#how-to-use}

Un nuovo pulsante denominato **Seleziona tutto** è stato aggiunto alle viste Scheda, Elenco o Colonna. Questo pulsante può essere utilizzato in una qualsiasi delle viste per selezionare tutti gli elementi del set di dati.

Nelle versioni precedenti di AEM, la selezione limitava ciò che veniva caricato nel browser client. Questa nuova modifica è stata introdotta per evitare confusione riguardo al numero di elementi su cui viene eseguita un’operazione in blocco.

Per il momento, sono state aggiunte tre operazioni all’elaborazione in blocco:

* Sposta
* Copia
* Eliminare

In futuro verrà aggiunto il supporto per ulteriori operazioni.
Per utilizzare questa funzione, accedi alla cartella o raccolta in cui desideri eseguire l’operazione collettiva su Pagine o Risorse.

Quindi, scegliete una delle viste, come illustrato di seguito:

### Vista a schede {#card-view}

![La vista a schede mostra le miniature di diverse risorse immagine.](assets/unu.png)

### Selezione di massa nella vista a schede {#bulk-selection-in-card-view}

È possibile selezionare risorse o pagine in blocco utilizzando **Seleziona tutto** pulsante in alto a destra:

![Seleziona Tutto, nell’angolo superiore destro della Vista a schede.](assets/doi.png) ![Tutte le miniature delle risorse immagini nella Vista a schede vengono visualizzate come selezionate con segni di spunta.](assets/trei.png)

### Vista a elenco  {#list-view}

Lo stesso vale per la vista a elenco:

![Viene evidenziata l&#39;opzione Seleziona tutto nell&#39;angolo superiore destro della Vista elenco.](assets/patru_modified.png)

### Selezione in blocco nella vista a elenco {#bulk-selection-in-list-view}

Nella Vista a elenco, utilizza **Seleziona tutto** oppure utilizzare la casella di controllo a sinistra per la selezione in serie.

![La Vista live mostra le miniature e le immagini delle risorse delle immagini e viene visualizzata in righe orizzontali.](assets/cinci.png) ![Casella di riepilogo che mostra le miniature e le immagini delle risorse immagine e una casella di controllo a sinistra di Nome.](assets/sase.png)

### Vista a colonne {#column-view}

![La Vista a colonne mostra le miniature delle risorse di immagini visualizzate in colonne verticali.](assets/sapte.png)

### Selezione in blocco nella vista a colonne {#bulk-selection-in-column-view}

![Tutte le miniature delle risorse immagini nella Vista a colonne vengono visualizzate come selezionate con segni di spunta.](assets/opt.png)

## Operazioni abilitate in blocco {#bulk-enabled-operations}

Dopo la selezione, è possibile eseguire una delle tre azioni abilitate in blocco: **Sposta**, **Copia** o **Elimina**.

Qui, **Sposta** L&#39;operazione viene eseguita sulle risorse selezionate sopra. In una qualsiasi delle visualizzazioni, questo determina lo spostamento di tutte le risorse nella posizione scelta e non solo di quelle caricate sullo schermo.

![Sposta le risorse mostrando una cartella selezionata nella Vista a colonne.](assets/noua.png)

Per altre operazioni che non sono abilitate in blocco, come **Download,** viene visualizzato un avviso che indica che nell’operazione sono inclusi solo gli elementi caricati nel browser.

![La vista Risorse mostra le risorse immagine selezionate e la finestra di dialogo a comparsa &quot;Azione di massa non supportata&quot;.](assets/zece.png)
