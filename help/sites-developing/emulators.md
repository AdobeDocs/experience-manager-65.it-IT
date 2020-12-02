---
title: Emulatori
seo-title: Emulatori
description: AEM consente agli autori di visualizzare una pagina in un emulatore che simula l’ambiente in cui l’utente finale visualizzerà la pagina
seo-description: AEM consente agli autori di visualizzare una pagina in un emulatore che simula l’ambiente in cui l’utente finale visualizzerà la pagina
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Emulatori{#emulators}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) consente agli autori di visualizzare una pagina in un emulatore che simula l’ambiente in cui l’utente finale visualizzerà la pagina, ad esempio su un dispositivo mobile o in un client di posta elettronica.

Framework emulatore AEM:

* Fornisce la creazione di contenuti all’interno di un’interfaccia utente simulata, ad esempio un dispositivo mobile o un client e-mail (utilizzato per creare newsletter).
* Adatta il contenuto della pagina in base all’interfaccia utente simulata.
* Consente la creazione di emulatori personalizzati.

>[!CAUTION]
>
>Questa funzione è supportata solo nell’interfaccia classica.

## Caratteristiche degli emulatori {#emulators-characteristics}

Un emulatore:

* È basato su ExtJS.
* Funziona sul DOM della pagina.
* Il suo aspetto è regolato tramite CSS.
* Supporta i plug-in (ad es. il plug-in di rotazione del dispositivo mobile).
* È attivo solo per l’autore.
* Il suo componente base è in `/libs/wcm/emulator/components/base`.

### Come l&#39;emulatore trasforma il contenuto {#how-the-emulator-transforms-the-content}

L&#39;emulatore funziona racchiudendo il contenuto HTML del corpo in DIV emulatori. Ad esempio, il seguente codice HTML:

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

viene trasformato nel seguente codice HTML dopo l’inizio dell’emulatore:

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

Sono stati aggiunti due tag div:

* il div con id `cq-emulator` che contiene l&#39;emulatore nel suo insieme e

* il div con id `cq-emulator-content` che rappresenta l&#39;area di visualizzazione/schermo/contenuto del dispositivo in cui risiede il contenuto della pagina.

Le nuove classi CSS sono inoltre assegnate ai nuovi div emulatore: rappresentano il nome dell&#39;emulatore corrente.

I plug-in di un emulatore possono estendere ulteriormente l&#39;elenco delle classi CSS assegnate, come nell&#39;esempio del plugin di rotazione, inserendo una classe &quot;verticale&quot; o &quot;orizzontale&quot; a seconda della rotazione corrente del dispositivo.

In questo modo, l&#39;aspetto completo dell&#39;emulatore può essere controllato facendo sì che le classi CSS corrispondenti agli ID e alle classi CSS dell&#39;emulatore subs.

>[!NOTE]
>
>È consigliabile che il progetto HTML racchiuda il contenuto del corpo in un singolo div, come nell&#39;esempio precedente. Se il contenuto del corpo contiene più tag, potrebbero verificarsi risultati imprevedibili.

### Emulatori per dispositivi mobili {#mobile-emulators}

Gli emulatori mobili esistenti:

* Sono sotto /libs/wcm/mobile/components/emulators.
* Sono disponibili tramite il servlet JSON all&#39;indirizzo:

   http://localhost:4502/bin/wcm/mobile/emulators.json

Quando il componente pagina si basa sul componente pagina mobile ( `/libs/wcm/mobile/components/page`), la funzionalità emulatore viene automaticamente integrata nella pagina tramite il seguente meccanismo:

* Il componente pagina mobile `head.jsp` include il componente init dell&#39;emulatore associato al gruppo di dispositivi (solo in modalità di creazione) e il rendering CSS del gruppo di dispositivi attraverso:

   `deviceGroup.drawHead(pageContext);`

* Il metodo `DeviceGroup.drawHead(pageContext)` include il componente init dell&#39;emulatore, ovvero chiama il componente `init.html.jsp` dell&#39;emulatore. Se il componente emulatore non ha un proprio `init.html.jsp` e si basa sull&#39;emulatore di base mobile ( `wcm/mobile/components/emulators/base)`, viene chiamato lo script init dell&#39;emulatore di base mobile ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Lo script init dell&#39;emulatore di base mobile definisce tramite Javascript:

   * Configurazione per tutti gli emulatori definiti per la pagina (emulatorConfigs)
   * Gestione emulatore che integra la funzionalità dell&#39;emulatore nella pagina attraverso:

      `emulatorMgr.launch(config)`;

      Il manager emulatore è definito da:

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Creazione di un emulatore mobile personalizzato {#creating-a-custom-mobile-emulator}

Per creare un emulatore mobile personalizzato:

1. Sotto `/apps/myapp/components/emulators` creare il componente `myemulator` (tipo di nodo: `cq:Component`).

1. Impostare la proprietà `sling:resourceSuperType` su `/libs/wcm/mobile/components/emulators/base`

1. Definite una libreria client CSS con la categoria `cq.wcm.mobile.emulator` per l&#39;aspetto dell&#39;emulatore: name = `css`, tipo di nodo = `cq:ClientLibrary`

   Ad esempio, è possibile fare riferimento al nodo `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Se necessario, definite una libreria client JS, ad esempio per definire un plug-in specifico: name = js, tipo di nodo = cq:ClientLibrary

   Ad esempio, è possibile fare riferimento al nodo `/libs/wcm/mobile/components/emulators/base/js`

1. Se l&#39;emulatore supporta funzionalità specifiche definite dai plug-in (come lo scorrimento touch), create un nodo di configurazione sotto l&#39;emulatore: name = `cq:emulatorConfig`, node type = `nt:unstructured` e aggiungere la proprietà che definisce il plug-in:

   * Nome = `canRotate`, Tipo = `Boolean`, Valore = `true`: per includere la funzionalità di rotazione.

   * Nome = `touchScrolling`, Tipo = `Boolean`, Valore = `true`: per includere la funzionalità di scorrimento touch.

   È possibile aggiungere ulteriori funzionalità definendo i propri plug-in.

