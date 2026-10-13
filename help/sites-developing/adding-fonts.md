---
title: Aggiunta di font per il rendering grafico
description: AEM consente di generare elementi grafici che incorporano testo estratto in modo dinamico dal contenuto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 5%
---
# Aggiunta di font per il rendering grafico{#adding-fonts-for-graphic-rendering}

AEM consente di generare elementi grafici che incorporano testo estratto in modo dinamico dal contenuto.

A questo scopo, puoi anche caricare e utilizzare i tuoi font.

Attualmente tutte le implementazioni della piattaforma Java supportano [caratteri TrueType](https://en.wikipedia.org/wiki/Truetype).

1. Apri CRXDE Lite e passa alla cartella dell’applicazione del progetto:

   `/apps/<your-project>/`

1. In `/apps/<your-project>/` creare un nodo:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`

   Salva tutte le modifiche.

1. Copiare i file dei caratteri in questa cartella, ad esempio utilizzando WebDAV.

   >[!NOTE]
   >
   >I file di font nel repository devono avere il suffisso `*.ttf` o `*.TTF`.

1. Aggiorna la [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) di [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Aggiungere il percorso alla cartella dei caratteri, ovvero `/apps/<your-project>/fonts`.

1. Torna a CRXDE Lite. Nella cartella dovrebbe essere presente un nodo `.fontlist` contenente il nome dei caratteri importati.

   Questi font sono ora pronti per essere utilizzati nell’API Java.

Per informazioni dettagliate su come utilizzare i font con l&#39;API Java, consulta la [documentazione per la classe Font dell&#39;API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
