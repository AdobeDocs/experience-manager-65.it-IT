---
title: Utilizzo del salvataggio automatico nell’app AEM Forms
description: Scopri come utilizzare la funzione di salvataggio automatico nell’app AEM Forms per evitare la perdita di dati.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Utilizzo del salvataggio automatico nell’app AEM Forms{#using-autosave-in-aem-forms-app}

Quando un utente immette dati nell’app Adobe Experience Manager Forms, la funzione di salvataggio automatico li salva a intervalli regolari. La funzione di salvataggio automatico nell’app AEM Forms consente di evitare la perdita di dati in caso di chiusura accidentale dell’app.

L’app può chiudersi accidentalmente:

* Se il dispositivo si spegne a causa di batteria insufficiente
* Se l’utente uccide l’app
* Se si verifica un arresto anomalo imprevisto

Puoi specificare gli intervalli dopo i quali l’app salva i dati immessi.

>[!NOTE]
>
>Seleziona la frequenza di salvataggio automatico in modo giudizioso. Le operazioni di salvataggio automatico frequenti possono avere un impatto notevole sulle prestazioni del dispositivo.

Per utilizzare la funzione di salvataggio automatico nell’app AEM Forms, effettua le seguenti operazioni:

1. Accedi all&#39;app e passa a **Impostazioni > Generale**.
1. Nella schermata Generale, utilizza l&#39;opzione **Salvataggio automatico frequenza** per selezionare gli intervalli in cui desideri che l&#39;app salvi i dati immessi.
   [![Impostazione della frequenza di salvataggio automatico](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Quando riavvii l’app e accedi con lo stesso utente, ti viene richiesto di ripristinare l’attività tramite la finestra di dialogo Recupera attività non salvata. Fare clic su **OK** nella finestra di dialogo Recupera attività non salvata per riprendere a utilizzare l&#39;attività salvata. Puoi fare clic su **Annulla** per eliminare i dati salvati corrispondenti all&#39;ultimo salvataggio automatico attivato e iniziare a lavorare con una nuova attività.

   Quando fai clic su **OK**, l&#39;attività viene ripristinata con i dati corrispondenti all&#39;ultimo salvataggio automatico attivato prima dell&#39;arresto anomalo dell&#39;app. Include i dati del modulo e tutti gli allegati associati all&#39;attività.
   [![Recupero di un&#39;attività&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** Modulo in corso di lavorazione **B.** App chiusa forzatamente **C.** App riavviata con la finestra di dialogo Recupera attività non salvata **D.** Modulo ripristinato con i dati originali
