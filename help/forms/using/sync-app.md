---
title: Sincronizzazione dell’app
seo-title: Synchronizing the app
description: Sincronizza l’app AEM Forms sul tuo dispositivo mobile con il server AEM Forms.
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Sincronizzazione dell’app{#synchronizing-the-app}

## Sincronizzazione dell’app {#synchronizing-the-app-1}

I moduli nell’app vengono scaricati dal server AEM Forms. I moduli vengono scaricati nelle schede Attività e Forms. Le bozze create dai moduli vengono scaricate nella scheda bozze e le bozze create dalle attività vengono scaricate nella scheda attività. Per un modulo indipendente sul server OSGi, i moduli e le bozze vengono scaricati rispettivamente nelle schede Forms e Bozza.

Quando si completa e si invia un modulo, questo viene immediatamente caricato sul server AEM Forms se l’app è online. I moduli vengono recuperati dal server quando l’app viene sincronizzata. Le bozze, tuttavia, vengono sincronizzate istantaneamente con il server se l’app è online.

Quando sei online con il server AEM Forms, per impostazione predefinita l’app viene sincronizzata ogni 15 minuti. Tuttavia, è possibile modificare la frequenza di sincronizzazione. In alternativa, puoi sincronizzare manualmente l’app in qualsiasi momento.

**Per sincronizzare manualmente l’app**

Tocca il pulsante Sincronizza ![sync-app](assets/sync-app.png) nell&#39;angolo in basso a destra della schermata iniziale.

**Per modificare la frequenza di sincronizzazione**

1. Per passare alla schermata di impostazione, tocca il pulsante del menu nell’angolo in alto a sinistra della schermata iniziale, quindi tocca **Impostazioni**.
1. Nella schermata Impostazioni , tocca la scheda Generale .

   ![Impostazione della frequenza di sincronizzazione nella finestra Impostazioni generali](assets/gen-settings-2.png)

1. Nell’opzione Frequenza di sincronizzazione, toccare il valore a destra della frequenza di sincronizzazione.
1. Nell’elenco a discesa , seleziona la nuova frequenza di sincronizzazione.

### Specifiche tecniche {#technical-specifications}

* La logica principale dell’invio dei dati dell’app offline al server AEM Forms è inclusa in runtime/offline/util/offline.js.
* In .js, la chiamata alla funzione processOfflineSubmittedSavedTasks(...) invia al server le attività salvate/inviate. Inoltre, gestisce eventuali errori o conflitti nel processo di sincronizzazione. Se l’invio di un’attività non riesce, l’attività nell’app viene contrassegnata come non riuscita. Inoltre, l&#39;attività rimane nella Posta in uscita.
* La funzione syncSubmittedTask() e syncSavedTask() eseguono operazioni su singole attività.
* La chiamata alla funzione processOfflineSubmittedSavedTasks() viene avviata dal componente dell&#39;elenco delle attività dopo che un utente seleziona di sincronizzare lo stato offline al server o una sincronizzazione automatica dal thread in background.
