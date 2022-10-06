---
title: Emulatori
seo-title: Emulators
description: AEM consente agli autori di visualizzare una pagina in un emulatore che simula l’ambiente in cui un utente finale visualizza la pagina
seo-description: AEM enables authors to view a page in an emulator that simulates the environment in which an end-user will view the page
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Emulatori{#emulators}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Adobe Experience Manager (AEM) consente agli autori di visualizzare una pagina in un emulatore che simula l’ambiente in cui l’utente finale visualizzerà la pagina, ad esempio su un dispositivo mobile o in un client di posta elettronica.

Il framework emulatore AEM:

* Fornisce l’authoring dei contenuti all’interno di un’interfaccia utente simulata, ad esempio un dispositivo mobile o un client e-mail (utilizzato per creare newsletter).
* Adatta il contenuto della pagina in base all’interfaccia utente simulata.
* Consente la creazione di emulatori personalizzati.

>[!CAUTION]
>
>Questa funzione è supportata solo nell’interfaccia classica.

## Caratteristiche degli emulatori {#emulators-characteristics}

Un emulatore:

* Si basa su ExtJS.
* Funziona sul DOM della pagina.
* Il suo aspetto è regolato tramite CSS.
* Supporta i plug-in (ad esempio il plugin per la rotazione dei dispositivi mobili).
* È attivo solo sull&#39;autore.
* La sua componente base è `/libs/wcm/emulator/components/base`.

### Come l’emulatore trasforma il contenuto {#how-the-emulator-transforms-the-content}

L’emulatore funziona racchiudendo il contenuto del corpo di HTML in DIV emulatori. Ad esempio, il seguente codice HTML:

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

* div con id `cq-emulator` tenendo in mano l&#39;emulatore nel suo insieme e

* div con id `cq-emulator-content` rappresenta l’area viewport/screen/content del dispositivo in cui si trova il contenuto della pagina.

Le nuove classi CSS vengono assegnate anche ai nuovi video emulatori: rappresentano il nome dell&#39;emulatore corrente.

I plug-in di un emulatore possono estendere ulteriormente l&#39;elenco delle classi CSS assegnate, come nell&#39;esempio del plugin di rotazione, inserendo una classe &quot;verticale&quot; o &quot;orizzontale&quot; a seconda della rotazione corrente del dispositivo.

In questo modo, l’aspetto completo dell’emulatore può essere controllato avendo classi CSS corrispondenti agli ID e alle classi CSS dell’emulatore subs.

>[!NOTE]
>
>È consigliabile che il contenuto del corpo del progetto HTML sia racchiuso in un singolo div, come nell’esempio precedente. Se il contenuto del corpo contiene più tag, i risultati potrebbero essere imprevedibili.

### Emulatori per dispositivi mobili {#mobile-emulators}

Gli emulatori mobili esistenti:

* Sono sotto /libs/wcm/mobile/components/emulators.
* Sono disponibili tramite il servlet JSON all’indirizzo:

   http://localhost:4502/bin/wcm/mobile/emulators.json

Quando il componente pagina si basa sul componente pagina mobile ( `/libs/wcm/mobile/components/page`), la funzionalità emulatore viene integrata automaticamente nella pagina attraverso il seguente meccanismo:

* Componente pagina mobile `head.jsp` include il componente di init dell’emulatore associato del gruppo di dispositivi (solo in modalità di authoring) e il rendering CSS del gruppo di dispositivi tramite:

   `deviceGroup.drawHead(pageContext);`

* Il metodo `DeviceGroup.drawHead(pageContext)` include il componente init dell’emulatore, ovvero chiama il `init.html.jsp` del componente emulatore. Se il componente emulatore non ha un proprio `init.html.jsp` e si basa sull’emulatore di base mobile ( `wcm/mobile/components/emulators/base)`, viene chiamato lo script init dell’emulatore mobile base ( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* Lo script init dell’emulatore di base mobile definisce tramite Javascript:

   * Configurazione per tutti gli emulatori definiti per la pagina (emulatorConfigs)
   * Il gestore di emulatori che integra le funzionalità dell&#39;emulatore nella pagina attraverso:

      `emulatorMgr.launch(config)`;

      Il gestore emulatori è definito da:

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### Creazione di un emulatore mobile personalizzato {#creating-a-custom-mobile-emulator}

Per creare un emulatore mobile personalizzato:

1. Sotto `/apps/myapp/components/emulators` creare il componente `myemulator` (tipo di nodo: `cq:Component`).

1. Imposta la proprietà `sling:resourceSuperType` su `/libs/wcm/mobile/components/emulators/base`

1. Definire una libreria client CSS con una categoria `cq.wcm.mobile.emulator` per l&#39;aspetto dell&#39;emulatore: name = `css`, tipo di nodo = `cq:ClientLibrary`

   Ad esempio, puoi fare riferimento al nodo `/libs/wcm/mobile/components/emulators/iPhone/css`

1. Se necessario, definisci una libreria client JS, ad esempio per definire un plug-in specifico: name = js, tipo di nodo = cq:ClientLibrary

   Ad esempio, puoi fare riferimento al nodo `/libs/wcm/mobile/components/emulators/base/js`

1. Se l’emulatore supporta funzionalità specifiche definite dai plug-in (come lo scorrimento touch), crea un nodo di configurazione sotto l’emulatore: name = `cq:emulatorConfig`, tipo di nodo = `nt:unstructured` e aggiungi la proprietà che definisce il plug-in:

   * Nome = `canRotate`, Tipo = `Boolean`, Valore = `true`: per includere la funzionalità di rotazione.

   * Nome = `touchScrolling`, Tipo = `Boolean`, Valore = `true`: per includere la funzionalità di scorrimento touch.
   Puoi aggiungere altre funzionalità definendo i tuoi plug-in.
