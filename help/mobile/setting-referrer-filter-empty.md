---
title: Impostazione del filtro Referrer su Allow Empty
description: Scopri il filtro Referrer. Per consentire al visualizzatore di applicazioni per dispositivi mobili Adobe Experience Manager (AEM) di visualizzare le app nell’istanza Autore, devi impostare il filtro del referente HTML su "Consenti vuoto".
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Impostazione del filtro Referrer su Allow Empty{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Per consentire al visualizzatore di applicazioni per dispositivi mobili Adobe Experience Manager (AEM) di visualizzare le app nell’istanza Autore, devi impostare il filtro del referente HTML su &quot;Consenti vuoto&quot;.

Se non si intende utilizzare il Visualizzatore applicazioni per esaminare le applicazioni all&#39;interno degli stati di sviluppo e di gestione temporanea, non è necessario modificare l&#39;impostazione predefinita del filtro referente.

Nell&#39;istanza di authoring in esecuzione di AEM, passa a: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e cerca &quot;Filtro referrer Apache Sling&quot;. Fai clic su per modificare il filtro del referente e seleziona la casella di controllo &quot;Consenti vuoto&quot; (vedi immagine seguente). Quindi premi il pulsante Salva e chiudi la pagina del browser.

![Impostazioni filtro referrer](assets/chlimage_1-106.png)
