---
title: AEM Commercio - Preparazione GDPR
seo-title: AEM Commercio - Preparazione GDPR
description: 'null'
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# AEM Commerce - GDPR: prontezza{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>Il GDPR è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come GDPR, CCPA ecc.

Il regolamento generale dell&#39;Unione europea sulla protezione dei dati in materia di diritti sulla privacy ha effetto a maggio 2018. Per ulteriori informazioni, vedere la pagina [GDPR all&#39; Centro per la privacy del Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Per ulteriori informazioni, vedere [AEM GDPR Readiness](/help/managing/data-protection-and-privacy.md).

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Nelle integrazioni Commerce pronte all&#39;uso, AEM è il livello esperienza, i servizi di consumo e l&#39;invio di dati alla piattaforma di e-commerce del cliente che viene eseguita in modalità headless.

Per alcune piattaforme di e-commerce, vengono memorizzate le informazioni di profilo ( `/home/users`) e i token di e-commerce (per accedere alla piattaforma di e-commerce) in AEM. Per questi casi di utilizzo, leggere [Gestione delle richieste GDPR per la piattaforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Gestione delle richieste GDPR per AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Per l&#39;integrazione con l&#39;Commerce Cloud Salesforce, AEM Commerce non memorizza informazioni rilevanti per il GDPR. Inoltra la richiesta a [Salesforce Cloud](https://documentation.demandware.com/).

Per le integrazioni hybris e IBM WebSphere, ci sono alcuni dati in AEM. È necessario utilizzare le [AEM istruzioni GDPR della piattaforma](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e prendere in considerazione le seguenti domande:

1. **Dove vengono memorizzati o utilizzati i dati personali?** Le informazioni del profilo utente memorizzate nella cache, come nome, identificatore utente di e-commerce, token, password, dati dell&#39;indirizzo e così via, vengono visualizzate da AEM.
1. **Con chi condivido i dati GDPR coperti?** Qualsiasi aggiornamento dei dati GDPR rilevanti in AEM Commerce non viene memorizzato (ad eccezione delle informazioni di profilo pertinenti, come indicato sopra) ma viene proxy alla piattaforma di eCommerce.
1. **Come eliminare i dati** utente? Eliminate il profilo utente in AEM e richiamate l&#39;eliminazione dell&#39;utente sulla piattaforma di eCommerce.

>[!NOTE]
>
>Date un&#39;occhiata alla [hybris wiki](https://wiki.hybris.com/) o alla [Documentazione di WebCommerce](https://www-01.ibm.com/support/docview.wss?uid=swg27036450), se necessario.

