---
title: Emulatori
seo-title: Emulators
description: AEM consente agli autori di visualizzare una pagina in un emulatore che simula l’ambiente in cui l’utente finale visualizzerà la pagina
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# Emulatori{#emulators}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) consente agli autori di visualizzare una pagina in un emulatore che simula l’ambiente in cui un utente finale visualizzerà la pagina, ad esempio su un dispositivo mobile o in un client e-mail.

Il framework dell’emulatore AEM:

* Fornisce l’authoring dei contenuti all’interno di un’interfaccia utente simulata, ad esempio un dispositivo mobile o un client e-mail (utilizzato per creare newsletter).
* Adatta il contenuto della pagina in base all’interfaccia utente simulata.
* Consente la creazione di emulatori personalizzati.

>[!CAUTION]
>
>Questa funzione è supportata solo nell’interfaccia classica.

## Caratteristiche degli emulatori {#emulators-characteristics}

Un emulatore:

* È basato su ExtJS.
* Funziona sulla pagina DOM.
* Il suo aspetto è regolato tramite CSS.
* Supporta i plug-in (ad esempio, il plug-in di rotazione per dispositivi mobili).
* È attivo solo sull’autore.
* Il suo componente base è in `/libs/wcm/emulator/components/base`.

### Come l’emulatore trasforma il contenuto {#how-the-emulator-transforms-the-content}

L’emulatore funziona racchiudendo il contenuto del corpo del HTML in div dell’emulatore. Ad esempio, il seguente codice html:

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

viene trasformato nel seguente codice html dopo l’avvio dell’emulatore:

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

* div con id `cq-emulator` tenendo l’emulatore nel suo insieme e

* div con id `cq-emulator-content` rappresenta il riquadro di visualizzazione/lo schermo/l’area di contenuto del dispositivo in cui si trova il contenuto della pagina.

Ai nuovi elementi div dell’emulatore vengono assegnate anche nuove classi CSS, che rappresentano il nome dell’emulatore corrente.

I plug-in di un emulatore possono estendere ulteriormente l’elenco delle classi CSS assegnate, come nell’esempio del plug-in di rotazione, inserendo una classe &quot;verticale&quot; o &quot;orizzontale&quot; a seconda della rotazione corrente del dispositivo.

In questo modo, l’aspetto completo dell’emulatore può essere controllato con classi CSS corrispondenti agli ID e alle classi CSS dell’emulatore div.

>[!NOTE]
>
>Si consiglia che il project HTML racchiuda il contenuto del corpo in un singolo div, proprio come nell’esempio precedente. Se il contenuto del corpo contiene più tag, potrebbero verificarsi risultati imprevedibili.

### Emulatori per dispositivi mobili {#mobile-emulators}

Gli emulatori mobili esistenti:

* Sono riportati di seguito /libs/wcm/mobile/components/emulators.
* Sono disponibili tramite il servlet JSON all’indirizzo:

  http://localhost:4502/bin/wcm/mobile/emulators.json

Quando il componente Pagina si basa sul componente Pagina mobile ( `/libs/wcm/mobile/components/page`), la funzionalità dell’emulatore viene integrata automaticamente nella pagina tramite il seguente meccanismo:

* Il componente Pagina mobile `head.jsp` include il componente iniziale dell’emulatore associato al gruppo di dispositivi (solo in modalità di authoring) e il CSS di rendering del gruppo di dispositivi tramite:

  `deviceGroup.drawHead(pageContext);`

* Il metodo `DeviceGroup.drawHead(pageContext)` include il componente init dell’emulatore, ovvero chiama il `init.html.jsp` del componente emulatore. Se il componente dell’emulatore non ha un proprio `init.html.jsp` e si basa sull&#39;emulatore di base mobile ( `wcm/mobile/components/emulators/base)`, lo script di inizializzazione dell’emulatore di base per dispositivi mobili è denominato ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Lo script di inizializzazione dell’emulatore di base mobile definisce tramite JavaScript:

   * Configurazione di tutti gli emulatori definiti per la pagina (emulatorConfigs)
   * Il gestore dell’emulatore che integra le funzionalità dell’emulatore nella pagina tramite:

     `emulatorMgr.launch(config)`;

     Il gestore degli emulatori è definito da:

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Creazione di un emulatore mobile personalizzato {#creating-a-custom-mobile-emulator}

Per creare un emulatore mobile personalizzato:

1. Sotto `/apps/myapp/components/emulators` creare il componente `myemulator` (tipo di nodo: `cq:Component`).

1. Imposta la proprietà `sling:resourceSuperType` su `/libs/wcm/mobile/components/emulators/base`

1. Definire una libreria client CSS con categoria `cq.wcm.mobile.emulator` per l&#39;aspetto dell&#39;emulatore: nome = `css`, tipo di nodo = `cq:ClientLibrary`

   Ad esempio, puoi fare riferimento al nodo `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Se necessario, definisci una libreria client JS, ad esempio per definire un plug-in specifico: name = js, node type = cq:ClientLibrary

   Ad esempio, puoi fare riferimento al nodo `/libs/wcm/mobile/components/emulators/base/js`

1. Se l’emulatore supporta funzionalità specifiche definite dai plug-in (come lo scorrimento touch), crea un nodo di configurazione sotto l’emulatore: name = `cq:emulatorConfig`, tipo di nodo = `nt:unstructured` e aggiungi la proprietà che definisce il plug-in:

   * Nome = `canRotate`, Tipo = `Boolean`, Valore = `true`: per includere la funzionalità di rotazione.

   * Nome = `touchScrolling`, Tipo = `Boolean`, Valore = `true`: per includere la funzionalità di scorrimento touch.

   Puoi aggiungere altre funzionalità definendo i tuoi plug-in.
