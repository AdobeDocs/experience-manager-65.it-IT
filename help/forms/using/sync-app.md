---
title: Sincronizzazione dell'app
seo-title: Sincronizzazione dell'app
description: Sincronizzate l'app AEM Forms  sul dispositivo mobile con il server AEM Forms .
seo-description: Sincronizzate l'app AEM Forms  sul dispositivo mobile con il server AEM Forms .
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Sincronizzazione dell&#39;app{#synchronizing-the-app}

## Sincronizzazione dell&#39;app {#synchronizing-the-app-1}

I moduli contenuti nell&#39;app vengono scaricati dal server AEM Forms . I moduli vengono scaricati nelle schede Attività e Forms. Le bozze create dai moduli vengono scaricate nella scheda delle bozze e le bozze create dalle attività vengono scaricate nella scheda delle attività. Per un modulo standalone sul server OSGi, i moduli e le bozze vengono scaricati nelle schede Forms e Bozza, rispettivamente.

Quando si completa e si invia un modulo, quest&#39;ultimo viene immediatamente caricato sul server AEM Forms  se l&#39;app è online. I moduli vengono recuperati dal server quando l&#39;app viene sincronizzata. Le bozze, tuttavia, vengono sincronizzate immediatamente con il server se l&#39;app è online.

Quando siete online con il server AEM Forms , per impostazione predefinita l&#39;app viene sincronizzata ogni 15 minuti. Tuttavia, potete modificare la frequenza di sincronizzazione. In alternativa, potete sincronizzare manualmente l&#39;app in qualsiasi momento.

**Per sincronizzare manualmente l&#39;app**

Toccate il pulsante Sincronizza ![app di sincronizzazione](assets/sync-app.png) nell&#39;angolo inferiore destro della schermata principale.

**Per modificare la frequenza di sincronizzazione**

1. Per passare alla schermata Impostazioni, toccate il pulsante del menu nell&#39;angolo superiore sinistro della schermata Home, quindi toccate **Impostazioni**.
1. Nella schermata Impostazioni, toccate la scheda Generale.

   ![Impostazione della frequenza di sincronizzazione nella finestra Impostazioni generali](assets/gen-settings-2.png)

1. Nell’opzione Frequenza sincronizzazione, toccate il valore a destra della frequenza di sincronizzazione.
1. Nell’elenco a discesa, selezionate la nuova frequenza di sincronizzazione.

### Specifiche tecniche {#technical-specifications}

* La logica principale dell&#39;invio dei dati dell&#39;app offline al server AEM Forms  è inclusa in runtime/offline/util/offline.js.
* In .js, la chiamata alla funzione processOfflineSubsentSavedTasks(...) invia al server le attività salvate/inviate. Vengono inoltre gestiti eventuali errori o conflitti nel processo di sincronizzazione. Se l&#39;invio di un&#39;attività non riesce, l&#39;attività nell&#39;app viene contrassegnata come non riuscita. Inoltre, l&#39;attività rimane nella casella in uscita.
* Le funzioni syncSubsentTask() e syncSavedTask() eseguono operazioni su singole attività.
* La chiamata alla funzione processOfflineSubsentSavedTasks() viene avviata dal componente Elenco attività dopo che l&#39;utente ha selezionato la sincronizzazione dello stato offline con il server o una sincronizzazione automatica dal thread in background.
