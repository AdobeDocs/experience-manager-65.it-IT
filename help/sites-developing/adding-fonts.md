---
title: Aggiunta di font per il rendering grafico
description: L’AEM consente di generare elementi grafici che incorporano testo estratto in modo dinamico dal contenuto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 725c81d0-0258-4118-8b01-29fd7bcaf9b3
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Aggiunta di font per il rendering grafico{#adding-fonts-for-graphic-rendering}

L’AEM consente di generare elementi grafici che incorporano testo estratto in modo dinamico dal contenuto.

A questo scopo, puoi anche caricare e utilizzare i tuoi font.

Al momento sono supportate tutte le implementazioni della piattaforma Java [TrueType](https://en.wikipedia.org/wiki/Truetype) font.

1. Apri CRXDE Liti e passa alla cartella dell’applicazione del progetto:

   `/apps/<your-project>/`

1. Sotto `/apps/<your-project>/` creare un nodo:

   * **Nome**: `fonts`
   * **Tipo**: `sling:Folder`

   Salva tutte le modifiche.

1. Copiare i file dei caratteri in questa cartella, ad esempio utilizzando WebDAV.

   >[!NOTE]
   >
   >I file di font nel repository devono avere il suffisso `*.ttf` o `*.TTF`.

1. Aggiornare il [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) di [Supporto caratteri Day Commons GFX](/help/sites-deploying/osgi-configuration-settings.md). Aggiungere il percorso alla cartella dei caratteri, ovvero `/apps/<your-project>/fonts`.

1. Torna a CRXDE Liti. Ora dovresti vedere un `.fontlist` nella cartella contenente il nome dei caratteri importati.

   Questi font sono ora pronti per essere utilizzati nell’API Java.

Per informazioni dettagliate sull’utilizzo dei font con l’API Java, consulta la sezione [documentazione per la classe Font dell’API Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
