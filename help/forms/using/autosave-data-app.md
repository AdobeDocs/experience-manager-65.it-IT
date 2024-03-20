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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
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

1. Accedi all’app e passa a **Impostazioni > Generale**.
1. Nella schermata Generale, utilizza **Frequenza salvataggio automatico** per selezionare gli intervalli in corrispondenza dei quali l’app deve salvare i dati immessi.
   [![Impostazione della frequenza di salvataggio automatico](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. Quando riavvii l’app e accedi con lo stesso utente, ti viene richiesto di ripristinare l’attività tramite la finestra di dialogo Recupera attività non salvata. Clic **OK** nella finestra di dialogo Recupera attività non salvata per riprendere a lavorare con l’attività salvata. Puoi fare clic su **Annulla** per eliminare i dati salvati corrispondenti all’ultimo salvataggio automatico attivato e iniziare a lavorare con una nuova attività.

   Quando fai clic su **OK**, l’attività viene ripristinata con i dati corrispondenti all’ultimo salvataggio automatico attivato prima dell’arresto anomalo dell’app. Include i dati del modulo e tutti gli allegati associati all&#39;attività.
   [![Recupero di un’attività&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**R.** Modulo work-in-progress **B.** App chiusa con forza **C.** App riavviata con la finestra di dialogo Recupera attività non salvata **D.** Modulo ripristinato con i dati originali
