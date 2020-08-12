---
title: Annullamento della validità della cache CDN tramite Dynamic Media
description: L’annullamento della validità della rete CDN (Content Delivery Network) nei contenuti memorizzati nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, anziché attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# Annullamento della validità della cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Le risorse per contenuti multimediali dinamici sono memorizzate nella cache dalla rete CDN (Content Delivery Network) per una distribuzione rapida dei contenuti ai clienti. Tuttavia, quando apportate gli aggiornamenti a tali risorse, potreste desiderare che le modifiche diventino attive immediatamente sul sito Web. Lo svuotamento o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse distribuite da Dynamic Media. Invece di aspettare che la cache scada utilizzando un valore TTL (Time To Live) (il valore predefinito è 10 ore), potete inviare una richiesta dall&#39;interno di Dynamic Media affinché la cache scada immediatamente.

>[!IMPORTANT]
>
>Questi passaggi si applicano solo alla modalità Dynamic Media - Scene7 in AEM 6.5, Service Pack 6 o successivo. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Consultate anche Panoramica sulla [memorizzazione nella cache in Contenuti multimediali](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)dinamici.

**Per annullare la validità del contenuto CDN memorizzato nella cache per le risorse Dynamic Media:**

1. In AEM 6.5.6 o versioni successive, toccate **[!UICONTROL Strumenti > Risorse > Annullamento validità CDN.]**

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Nella pagina Annullamento validità CDN, impostate le opzioni desiderate:

   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | Quando selezionate questa opzione, potete selezionare una o più risorse Contenuti multimediali dinamici, indipendentemente dal tipo MIME, e i relativi predefiniti immagine associati per l’annullamento della validità della cache.<br>Anche se potete selezionare una o più cartelle contenenti risorse,  Adobe non consiglia questo approccio. È invece necessario selezionare singoli file di risorse.<br>Procedete quindi con il passaggio successivo. |
   | **[!UICONTROL Annullamento della convalida in base al modello]** | Quando selezionate questa opzione, potete selezionare le risorse Contenuti multimediali dinamici e il modello di annullamento della validità precedentemente creato. Utilizzate questa opzione con |
   | **[!UICONTROL Aggiungi risorse]** | Blah |
   | **[!UICONTROL Aggiungi URL]** | Aggiungete manualmente i percorsi URL completi alle risorse Contenuti multimediali dinamici la cui cache desiderate annullare la validità. |

1. 
1. Toccate **[!UICONTROL Avanti.]**
1. 
