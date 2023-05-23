---
title: Impostazione del filtro Referrer su Allow Empty
seo-title: Setting Your Referrer Filter to Allow Empty
description: Segui questa pagina per scoprire di più sul filtro Referrer. Per consentire al Visualizzatore applicazioni di AEM Mobile di visualizzare le app nell’istanza Autore, imposta il filtro del referente HTML su "Consenti vuoto".
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 3%

---

# Impostazione del filtro Referrer su Allow Empty{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Per consentire al Visualizzatore applicazioni di AEM Mobile di visualizzare le app nell’istanza Autore, imposta il filtro del referente HTML su &quot;Consenti vuoto&quot;.

Se non si intende utilizzare il Visualizzatore applicazioni per esaminare le applicazioni all&#39;interno degli stati di sviluppo e staging, non è necessario modificare l&#39;impostazione predefinita del filtro referente.

Nell’istanza di authoring in esecuzione dell’AEM, accedi a: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) e cerca &quot;Apache Sling Referrer Filter&quot;. Fai clic su per modificare il filtro del referente e seleziona la casella di controllo &quot;Consenti vuoto&quot; (vedi immagine seguente). Quindi premi il pulsante Salva e chiudi la pagina del browser.

![Impostazioni filtro referrer](assets/chlimage_1-106.png)
