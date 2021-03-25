---
title: Componente RemotePage
description: Il componente RemotePage è un componente di pagina personalizzato per la modifica del SPA React remoto in AEM.
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Componente RemotePage {#remote-page-component}

Quando si decide quale livello di integrazione si desidera avere tra il SPA esterno e il AEM, spesso è chiaro che è necessario essere in grado di visualizzare e modificare il SPA in AEM. Il componente RemotePage è un componente pagina personalizzato solo a questo scopo.

## Panoramica {#overview}

Il componente RemotePage recupera tutte le risorse necessarie dall&#39;elemento `asset-manifest.json` generato dall&#39;applicazione e lo utilizza per il rendering dell&#39;SPA all&#39;interno di AEM.

* RemotePage consente di inserire gli script e i fogli di stile di un SPA nel corpo di un componente Pagina AEM.
* I componenti Frontend virtuali consentono di contrassegnare le sezioni come modificabili in AEM editor di SPA.
* Insieme, un SPA ospitato su un dominio diverso può essere reso modificabile in AEM.

Per ulteriori informazioni sulle SPA modificabili esterne in AEM, consulta l’articolo [Modifica di un SPA esterno in AEM](spa-edit-external.md) .

## Requisiti {#requirements}

* Abilitare CORS nello sviluppo
* Configurare l’URL remoto nelle Proprietà pagina
* Esegui il rendering del SPA in AEM

## Limitazioni  {#limitations}

* L&#39;implementazione corrente del componente RemotePage supporta solo le applicazioni React remote.
* I CSS interni definiti nel file HTML principale dell’applicazione e i CSS in linea sul nodo DOM principale non saranno disponibili quando si esegue il rendering remoto in AEM.

## Dettagli tecnici {#technical-details}

Come il resto del progetto SPA AEM, il componente RemotePage è open source. Per informazioni tecniche complete sul componente RemotePage, [vedere l&#39;archivio GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
