---
title: Componente RemotePage
description: Il componente RemotePage è un componente di pagina personalizzato per la modifica del SPA React remoto in AEM.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
source-git-commit: 41aac3b4ea3b100e9d927bef161929477d667a95
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# Componente RemotePage {#remote-page-component}

Quando si decide quale livello di integrazione si desidera avere tra il SPA esterno e il AEM, spesso è chiaro che è necessario essere in grado di visualizzare e modificare il SPA in AEM. Il componente RemotePage è un componente pagina personalizzato solo a questo scopo.

## Panoramica {#overview}

Il componente RemotePage recupera tutte le risorse necessarie dall&#39;applicazione generata `asset-manifest.json` e lo utilizza per il rendering del SPA all&#39;interno di AEM.

* RemotePage consente di inserire gli script e i fogli di stile di un SPA nel corpo di un componente Pagina AEM.
* I componenti Frontend virtuali consentono di contrassegnare le sezioni come modificabili in AEM editor di SPA.
* Insieme, un SPA ospitato su un dominio diverso può essere reso modificabile in AEM.

Vedi l&#39;articolo [Modifica di un SPA esterno in AEM](spa-edit-external.md) per ulteriori dettagli sulle SPA modificabili esterne in AEM.

## Requisiti {#requirements}

* Abilitare CORS nello sviluppo
* Configurare l’URL remoto nelle Proprietà pagina
* Esegui il rendering del SPA in AEM
* L&#39;applicazione web deve utilizzare un manifesto di risorse del bundler come uno dei seguenti ed esporre un file asset-manifest.json nella directory principale del dominio che elenca in una proprietà entrypoints tutti i file CSS e JS da caricare:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![Punti di entrata](assets/asset-manifest-entrypoints.png)

* L&#39;applicazione deve essere in grado di inizializzare in un `<div id="root"></div>` sotto l&#39;elemento body. Se è previsto un markup diverso per l’istanza dell’app, questo deve essere regolato di conseguenza negli script HTL del componente proxy che ha un `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitazioni {#limitations}

* Il componente RemotePage prevede che l&#39;implementazione fornisca un manifesto di risorse come quello [Ho trovato qui.](https://github.com/shellscape/webpack-manifest-plugin) Il componente RemotePage, tuttavia, è stato testato solo per funzionare con il framework React (e Next.js tramite il componente Remote-page-next) e quindi non supporta il caricamento in remoto di applicazioni da altri framework, come ad Angular.
* I CSS interni definiti nel file HTML principale dell’applicazione e i CSS in linea sul nodo DOM principale non saranno disponibili quando si esegue il rendering remoto in AEM.

## Dettagli tecnici {#technical-details}

Come il resto del progetto SPA AEM, il componente RemotePage è open source. Per tutti i dettagli tecnici del componente RemotePage, [consulta l’archivio GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
