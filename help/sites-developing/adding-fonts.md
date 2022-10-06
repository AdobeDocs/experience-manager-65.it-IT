---
title: Aggiunta di font al rendering grafico
seo-title: Adding Fonts for Graphic-Rendering
description: AEM consente di generare elementi grafici che incorporano testo tratto dinamicamente dal contenuto
seo-description: AEM allows you to generate graphics incorporating text dynamically taken from your content
uuid: 67d9b10f-e986-4d29-bde2-10e08075fe17
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6af48ef5-75e6-4b66-bc0d-ecf254b1c4ef
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---

# Aggiunta di font al rendering grafico{#adding-fonts-for-graphic-rendering}

AEM consente di generare elementi grafici che incorporano testo tratto dinamicamente dal contenuto.

A questo scopo è anche possibile caricare e utilizzare i propri font.

Attualmente tutte le implementazioni del supporto della piattaforma Java [TrueType](https://en.wikipedia.org/wiki/Truetype) font.

1. Apri CRXDE Lite e passa alla cartella dell&#39;applicazione di progetto:

   `/apps/<your-project>/`

1. Sotto `/apps/<your-project>/` crea un nuovo nodo:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`

   Salva tutte le modifiche.

1. Copiare i file di font in questa cartella; ad esempio, utilizzando WebDAV.

   >[!NOTE]
   >
   >I file di font nell’archivio devono avere il suffisso `*.ttf` o `*.TTF`.

1. Aggiorna [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) di [Helper font GFX Day Commons](/help/sites-deploying/osgi-configuration-settings.md). Aggiungi il percorso alla cartella dei font; ovvero `/apps/<your-project>/fonts`.

1. Torna a CRXDE Lite. Ora dovresti visualizzare un `.fontlist` nella cartella contenente il nome dei font importati.

   Questi font sono ora pronti per essere utilizzati nell’API Java.

Per informazioni dettagliate su come utilizzare i font con l’API Java, consulta la sezione [documentazione per la classe Font dell&#39;API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
