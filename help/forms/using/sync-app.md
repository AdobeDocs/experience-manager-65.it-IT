---
title: Sincronizzazione dell’app
description: Sincronizza l’app AEM Forms sul tuo dispositivo mobile con il server AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%
---
# Sincronizzazione dell’app{#synchronizing-the-app}

>[!NOTE]
>
>L’app AEM Forms è attualmente obsoleta. Per domande o assistenza, contattare [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

## Sincronizzazione dell’app {#synchronizing-the-app-1}

I moduli nell’app vengono scaricati dal server AEM Forms. I moduli vengono scaricati nelle schede Attività e Forms. Le bozze create da moduli vengono scaricate nella scheda bozze e le bozze create da attività vengono scaricate nella scheda attività. Per un modulo indipendente sul server OSGi, i moduli e le bozze vengono scaricati rispettivamente nelle schede Forms e Bozza.

Quando completi e invii un modulo, questo viene caricato nuovamente sul server di AEM Forms immediatamente se l’app è online. I moduli vengono recuperati dal server quando l’app viene sincronizzata. Le bozze, tuttavia, vengono sincronizzate con il server immediatamente se l’app è online.

Quando sei online con il server AEM Forms, per impostazione predefinita, l’app viene sincronizzata ogni 15 minuti. Tuttavia, è possibile modificare la frequenza di sincronizzazione. In alternativa, puoi sincronizzare manualmente l’app in qualsiasi momento.

**Per sincronizzare l&#39;app manualmente**

Selezionare il pulsante Sincronizza ![sync-app](assets/sync-app.png) nell&#39;angolo inferiore destro della schermata iniziale.

**Per modificare la frequenza di sincronizzazione**

1. Per passare alla schermata Impostazioni, selezionare il pulsante del menu nell&#39;angolo superiore sinistro della schermata iniziale, quindi selezionare **Impostazioni**.
1. Nella schermata Settings, selezionare la scheda General.

   ![Impostazione della frequenza di sincronizzazione nella finestra Impostazioni generali](assets/gen-settings-2.png)

1. Nell&#39;opzione Frequenza di sincronizzazione selezionare il valore a destra di Frequenza di sincronizzazione.
1. Nell&#39;elenco a discesa selezionare la nuova frequenza di sincronizzazione.

### Specifiche tecniche {#technical-specifications}

* La logica principale per l’invio dei dati dell’app offline al server AEM Forms è inclusa in runtime/offline/util/offline.js.
* In .js, la chiamata a processOfflineSubmittedSavedTasks(...) , invia le attività salvate/inviate al server. Gestisce inoltre eventuali errori o conflitti nel processo di sincronizzazione. Se l’invio di un’attività non riesce, l’attività nell’app viene contrassegnata come non riuscita. Inoltre, l’attività rimane nella cartella Posta in uscita.
* Le funzioni syncSubmittedTask() e syncSavedTask() eseguono operazioni su singole attività.
* La chiamata alla funzione processOfflineSubmittedSavedTasks() viene avviata dal componente Elenco attività dopo che un utente ha scelto di sincronizzare lo stato offline con il server o una sincronizzazione automatica da parte del thread in background.
