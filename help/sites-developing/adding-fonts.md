---
title: Aggiunta di font per il rendering grafico
seo-title: Aggiunta di font per il rendering grafico
description: AEM consente di generare elementi grafici con testo ripreso in modo dinamico dai contenuti
seo-description: AEM consente di generare elementi grafici con testo ripreso in modo dinamico dai contenuti
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aggiunta di font per il rendering grafico{#adding-fonts-for-graphic-rendering}

AEM consente di generare elementi grafici con testo tratto dai contenuti in modo dinamico.

A questo scopo è anche possibile caricare e utilizzare i propri font.

Attualmente tutte le implementazioni della piattaforma Java supportano i font [TrueType](https://en.wikipedia.org/wiki/Truetype) .

1. Apri CRXDE Lite e passa alla cartella dell&#39;applicazione di progetto:

   `/apps/<your-project>/`

1. In `/apps/<your-project>/` Crea un nuovo nodo:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`
   Salvate tutte le modifiche.

1. Copiare i file dei font in questa cartella; ad esempio, utilizzando WebDAV.

   >[!NOTE]
   >
   >I file di font nell&#39;archivio devono avere il suffisso `*.ttf` o `*.TTF`.

1. Aggiornate la configurazione [](/help/sites-deploying/configuring-osgi.md) OSGi di [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Aggiungete il percorso alla cartella dei font; ovvero `/apps/<your-project>/fonts`.

1. Tornate a CRXDE Lite. È ora necessario visualizzare un `.fontlist` nodo nella cartella contenente il nome dei font importati.

   Questi font sono ora pronti per essere utilizzati nell&#39;API Java.

Per informazioni dettagliate sull&#39;utilizzo dei font con l&#39;API Java, consultate la [documentazione per la classe Font dell&#39;API](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html)Java.

