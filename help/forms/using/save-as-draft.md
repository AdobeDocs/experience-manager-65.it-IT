---
title: Salvataggio di un'attività o di un modulo come bozza
seo-title: Salvataggio di un'attività o di un modulo come bozza
description: 'Passaggi per salvare una bozza di copia di un''attività o di un modulo nell''app AEM Forms '
seo-description: 'Passaggi per salvare una bozza di copia di un''attività o di un modulo nell''app AEM Forms '
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Salvataggio di un&#39;attività o di un modulo come bozza {#saving-a-task-or-form-as-a-draft}

L&#39;opzione Salva come bozza consente di salvare un&#39;istantanea di un&#39;attività o di un modulo insieme ai dati compilati nel modulo associato. Potete anche creare una bozza da un modello. Le bozze vengono salvate nel dispositivo mobile e sincronizzate con  server Adobe Experience Manager Forms per un successivo recupero.

È possibile [aggiornare il modulo](/help/forms/using/working-with-form.md), [annotarlo](/help/forms/using/add-attachments.md) con fotografie e note di script. Durante l&#39;aggiornamento di un modulo, si consiglia di salvarlo come bozza. Per le situazioni in cui si decide di inviare un modulo compilato in un momento successivo, è utile salvarlo come bozza.

Per abilitare la funzione Salva come bozza per i moduli salvati nel portale dei moduli, vedere [Salvataggio di un modulo HTML5 come bozza](/help/forms/using/saving-html5-form-draft.md).
Per configurare l&#39;invio di moduli adattivi, vedere [Bozze e componenti di invio](/help/forms/using/draft-submission-component.md). (Non valido per i moduli sincronizzati con  server AEM Forms JEE).

Per creare una bozza, aprire il modulo e toccare **Salva come bozza** ![salva come bozza](assets/save-as-draft.png). Specificare il nome della bozza e toccare **Salva**. La bozza viene salvata nella cartella Bozze e sincronizzata con il server. Se l&#39;app è offline, viene salvata nella cartella Posta in uscita.

Se successivamente si aggiorna il modulo corrispondente, le modifiche verranno applicate immediatamente. Quando si sincronizza l&#39;app  AEM Forms con  server AEM Forms, la bozza viene caricata  server AEM Forms. Inoltre, la bozza viene spostata dalla casella in uscita alla cartella Attività o Bozze. Accanto ad essa viene visualizzata un’icona di modifica.

Se si continua a lavorare su più attività e punti di inizio e si salvano le bozze, queste vengono salvate. Ogni volta che l&#39;app viene sincronizzata con il server AEM Forms , la bozza viene salvata sul server. In qualsiasi momento è possibile recuperare le bozze in base all&#39;ultima data e ora salvate. Ad esempio, se reinstallate l&#39;app o modificate il dispositivo mobile, potete scaricare la bozza dal server.

## Eliminare una bozza {#delete-a-draft}

Nella cartella delle bozze sono elencate tutte le bozze. Potete utilizzare l&#39;opzione Elimina bozza per eliminare definitivamente le bozze dal dispositivo mobile e dal server.

L&#39;opzione per eliminare le bozze create da un&#39;attività non è disponibile. Quando si elimina una bozza creata da un&#39;attività, l&#39;attività viene abbandonata.

Potete eliminare le bozze sia in modalità offline che online. Se si scartano le bozze in modalità offline, le bozze vengono eliminate dal server solo quando viene ripristinata la connessione con il server.

Per eliminare una bozza, effettuate le seguenti operazioni:

1. Nell&#39;app AEM Forms , andate a **Forms.**
1. Selezionare **Bozze** dal menu a discesa accanto a Cerca.
1. Un modulo con l&#39;icona di modifica ![edit-draft-app](assets/edit-draft-app.png) indica una bozza. Toccate i puntini di sospensione orizzontali accanto alla bozza.
1. Nelle opzioni visualizzate quando toccate i puntini di sospensione orizzontali, toccate **Elimina bozza**.
