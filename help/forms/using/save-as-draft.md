---
title: Salvataggio di un'attività o di un modulo come bozza
description: Passaggi per salvare una bozza di copia di un’attività o di un modulo nell’app AEM Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b4a23b2e-ab18-402c-8dfa-2533ee692912
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Salvataggio di un&#39;attività o di un modulo come bozza {#saving-a-task-or-form-as-a-draft}

L’opzione Salva come bozza consente di salvare un’istantanea di un’attività o di un modulo insieme ai dati inseriti nel modulo associato. Potete anche creare una bozza da un modello. Le bozze vengono salvate nel dispositivo mobile e sincronizzate con il server Adobe Experience Manager Forms per un recupero successivo.

È possibile [aggiornare il modulo](/help/forms/using/working-with-form.md), [annota](/help/forms/using/add-attachments.md) con fotografie e note a mano. Mentre si continua ad aggiornare un modulo, si consiglia di salvarlo come bozza. Nelle situazioni in cui si decide di inviare un modulo compilato in un momento successivo, è utile salvarlo come bozza.

Per abilitare la funzione Salva come bozza per i moduli salvati nel portale dei moduli, vedere [Salvataggio di un modulo HTML5 come bozza](/help/forms/using/saving-html5-form-draft.md).
Per configurare l’invio di moduli adattivi, consulta [Componente Bozze e invii](/help/forms/using/draft-submission-component.md). (Non valido per i moduli sincronizzati con il server AEM Forms JEE).

Per creare una bozza, aprite la maschera e selezionate **Salva come bozza** ![salva come bozza](assets/save-as-draft.png). Immettete il nome della bozza e selezionate **Salva**. La bozza viene salvata nella cartella Bozze e sincronizzata con il server. Se l’app non è in linea, viene salvata nella cartella Posta in uscita.

Se successivamente aggiorni il modulo corrispondente, le modifiche vengono applicate immediatamente. Quando l’app AEM Forms viene sincronizzata con il server AEM Forms, la bozza viene caricata sul server AEM Forms. Inoltre, la bozza viene spostata dalla cartella Posta in uscita alla cartella Attività o Bozze. Accanto a esso viene visualizzata un&#39;icona di modifica.

Mentre si continua a lavorare su più attività e punti iniziali e si salvano, le bozze vengono salvate. Ogni volta che l’app viene sincronizzata con il server AEM Forms, la bozza viene salvata nel server. In questo modo è possibile recuperare le bozze in qualsiasi momento in base alla data e all&#39;ora dell&#39;ultimo salvataggio. Ad esempio, se reinstalli l’app o modifichi il dispositivo mobile, puoi scaricare la bozza dal server.

## Eliminare una bozza {#delete-a-draft}

Nella cartella Bozze sono elencate tutte le bozze. È possibile utilizzare l’opzione Elimina bozza per eliminare definitivamente le bozze dal dispositivo mobile e dal server.

L’opzione per eliminare le bozze create da un’attività non è disponibile. Quando si elimina una bozza creata da un&#39;attività, l&#39;attività viene abbandonata.

È possibile eliminare le bozze sia in modalità offline che in modalità online. Quando si eliminano le bozze in modalità non in linea, le bozze vengono eliminate dal server solo quando viene ripristinata la connessione con il server.

Per eliminare una bozza, effettuate le seguenti operazioni:

1. Nell’app AEM Forms, passa a **Forms.**
1. Seleziona **Bozze** dal menu a discesa accanto a Cerca.
1. Un modulo con l’icona di modifica ![edit-draft-app](assets/edit-draft-app.png) indica una bozza. Selezionate i puntini di sospensione orizzontali accanto allo sformo.
1. Nelle opzioni visualizzate quando selezioni i puntini di sospensione orizzontali, seleziona **Elimina bozza**.
