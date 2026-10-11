---
title: Componente RemotePage
description: Il componente RemotePage è un componente pagina personalizzato per la modifica dell’applicazione a pagina singola React remota in AEM.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: a9f7d31e-bbe1-4475-966a-5f213546fcd9
    internal-label: SPA Editor
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%
---

# Componente RemotePage {#remote-page-component}

Quando decidi quale livello di integrazione desideri avere tra l’applicazione a pagina singola esterna e AEM, spesso è chiaro che devi essere in grado di visualizzare e modificare l’applicazione a pagina singola in AEM. Il componente RemotePage è un componente pagina personalizzato appositamente per questo scopo.

{{ue-over-spa}}

## Panoramica {#overview}

Il componente RemotePage recupera tutte le risorse necessarie da `asset-manifest.json` generato dall&#39;applicazione e lo utilizza per il rendering dell&#39;applicazione a pagina singola in AEM.

* RemotePage consente di inserire gli script e i fogli di stile di un’applicazione a pagina singola nel corpo di un componente AEM Page.
* I componenti front-end virtuali consentono di contrassegnare le sezioni come modificabili nell’editor SPA di AEM.
* Insieme, un’applicazione a pagina singola ospitata su un dominio diverso può essere resa modificabile in AEM.

Consulta l&#39;articolo [Modifica di un&#39;applicazione a pagina singola esterna all&#39;interno di AEM](spa-edit-external.md) per ulteriori dettagli sulle applicazioni a pagina singola esterne modificabili in AEM.

## Requisiti {#requirements}

* Abilitare CORS nello sviluppo
* Configurare l’URL remoto nelle Proprietà pagina
* Eseguire il rendering dell’applicazione a pagina singola in AEM
* L’applicazione web deve utilizzare un manifesto della risorsa bundler come uno dei seguenti ed esporre un file asset-manifest.json nella directory principale del dominio che elenca in una proprietà entrypoints tutti i file CSS e JS da caricare:
  * https://github.com/shellscape/webpack-manifest-plugin
  * https://github.com/webdeveric/webpack-assets-manifest
  * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

  ![Punti di ingresso](assets/asset-manifest-entrypoints.png)

* L&#39;applicazione deve essere in grado di inizializzare in un `<div id="root"></div>` sotto l&#39;elemento body. Se è previsto un markup diverso per la creazione dell&#39;istanza dell&#39;app, è necessario regolarlo di conseguenza negli script HTL del componente proxy con `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitazioni {#limitations}

* Il componente RemotePage prevede che l&#39;implementazione fornisca un manifesto di risorse come quello [trovato qui.](https://github.com/shellscape/webpack-manifest-plugin) Il componente RemotePage, tuttavia, è stato testato per funzionare solo con il framework React (e Next.js tramite il componente remote-page-next ) e pertanto non supporta il caricamento remoto di applicazioni da altri framework, come Angular.
* I CSS interni definiti nel file HTML principale dell’applicazione e i CSS in linea sul nodo DOM principale non saranno disponibili durante il rendering remoto in AEM.

## Dettagli tecnici {#technical-details}

Come il resto del progetto SPA di AEM, il componente RemotePage è open source. Per informazioni tecniche complete sul componente RemotePage, [consulta l&#39;archivio GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
