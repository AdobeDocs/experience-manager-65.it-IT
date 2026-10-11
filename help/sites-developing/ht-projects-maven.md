---
title: Creare progetti AEM con Apache Maven
description: Questo documento descrive come impostare un progetto AEM basato su Apache Maven
exl-id: 451913bf-bb1e-4444-aee5-968ac30b5c9d
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 24%
---
# Creare progetti AEM con Apache Maven {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5 aderisce alle best practice più recenti per la gestione dei pacchetti e la struttura del progetto, implementate dall’archetipo del progetto AEM più recente per le implementazioni locali e AMS.

>[!TIP]
>
>Per maggiori dettagli, cfr.:
>
>* L&#39;articolo [Struttura del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) nella documentazione di AEM as a Cloud Service per la struttura dei progetti AEM moderni.
>* Documentazione di [Archetipo progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview) su come avviare un nuovo progetto AEM utilizzando l&#39;archetipo.
>* L&#39;articolo [Plug-in Maven per pacchetto di contenuti Adobe](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=it#developer-tools) nella documentazione di AEM as a Cloud Service per informazioni su come distribuire le applicazioni AEM.
>
>I tre documenti sono applicabili ad AEM 6.5.
