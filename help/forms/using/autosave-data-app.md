---
title: Utilizzo del salvataggio automatico nell’app AEM Forms
seo-title: Using autosave in AEM Forms app
description: Scopri come utilizzare la funzione di salvataggio automatico nell’app AEM Forms per evitare la perdita di dati.
seo-description: Learn how to use autosave feature in AEM Forms app that lets you avoid data loss.
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Utilizzo del salvataggio automatico nell’app AEM Forms{#using-autosave-in-aem-forms-app}

Quando un utente immette dei dati nell’app Adobe Experience Manager Forms, la funzione di salvataggio automatico li salva a intervalli regolari. La funzione di salvataggio automatico nell’app AEM Forms consente di evitare la perdita di dati in caso di chiusura accidentale dell’app.

L’app può chiudersi accidentalmente:

* Se il dispositivo si spegne a causa della batteria scarica
* Se l’utente uccide l’app
* Se si verifica un arresto anomalo imprevisto

Puoi specificare gli intervalli in cui l’app salva i dati immessi.

>[!NOTE]
>
>Selezionare la frequenza di salvataggio automatico in modo giudizioso. Le frequenti operazioni di salvataggio automatico possono avere un impatto notevole sulle prestazioni del dispositivo.

Esegui i seguenti passaggi per utilizzare la funzione di salvataggio automatico nell’app AEM Forms:

1. Accedi all’app e passa a **Impostazioni > Generale**.
1. Nella schermata Generale, utilizza il **Frequenza di salvataggio automatico** per selezionare gli intervalli in cui salvare i dati immessi dall’app.
   [ ![Impostazione della frequenza di salvataggio automatico](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Quando riavvii l&#39;app e accedi con lo stesso utente, ti viene richiesto di ripristinare l&#39;attività con la finestra di dialogo Ripristina attività non salvata. Fai clic su **OK** nella finestra di dialogo Ripristina attività non salvata per riprendere a lavorare con l&#39;attività salvata. Puoi fare clic su **Annulla** per eliminare i dati salvati corrispondenti all&#39;ultimo salvataggio automatico attivato e iniziare a lavorare con una nuova attività.

   Quando fai clic su **OK**, l’attività viene ripristinata con i dati corrispondenti all’ultimo salvataggio automatico attivato prima dell’arresto anomalo dell’app. Include i dati del modulo e tutti gli allegati associati all’attività.
   [ ![Recupero di un&#39;attività&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Modulo work-in-progress **B.** Applicazione chiusa con forza **C.** App riavviata con la finestra di dialogo Ripristina attività non salvata **D.** Modulo ripristinato con dati originali
