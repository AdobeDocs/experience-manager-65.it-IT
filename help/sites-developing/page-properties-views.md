---
title: Personalizzazione delle visualizzazioni delle proprietà di pagina
seo-title: Customizing Views of Page Properties
description: Ogni pagina dispone di un set di proprietà che è possibile modificare in base alle esigenze
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Personalizzazione delle visualizzazioni delle proprietà di pagina{#customizing-views-of-page-properties}

Ogni pagina ha un set di [proprietà](/help/sites-authoring/editing-page-properties.md) che possono essere visualizzate e modificate dagli utenti; alcune sono necessarie quando si crea la pagina (crea vista), altre possono essere visualizzate e modificate (modifica vista) in una fase successiva. Queste proprietà di pagina vengono definite e rese disponibili dalla finestra di dialogo ( `cq:dialog`) del componente pagina appropriato.

>[!CAUTION]
>
>La personalizzazione della visualizzazione delle proprietà di pagina non è disponibile nell’interfaccia classica.

Lo stato predefinito per ogni proprietà di pagina è:

* nascosta nella vista di creazione (ad esempio, **Crea pagina** procedura guidata)

* disponibile nella vista di modifica (ad esempio, **Visualizza proprietà**)

I campi devono essere configurati in modo specifico se è necessaria una modifica. Questa operazione viene eseguita utilizzando le proprietà del nodo appropriate:

* Proprietà di pagina da rendere disponibile nella visualizzazione di creazione (ad esempio, **Crea pagina** procedura guidata):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Proprietà di pagina da rendere disponibile nella vista di modifica (ad esempio, **Visualizza**/**Modifica**) **Proprietà** opzionale):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Ad esempio, consulta le impostazioni per i campi raggruppati sotto **Altri titoli e descrizioni** il **Base** per il componente Pagina di base. Questi sono visibili nel **Crea pagina** creazione guidata come `cq:showOnCreate` è stato impostato su `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulta la [Tutorial sull’estensione delle proprietà di pagina](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) guida alla personalizzazione delle proprietà di pagina.

## Configurazione delle proprietà della pagina {#configuring-your-page-properties}

Puoi anche configurare i campi disponibili configurando la finestra di dialogo del componente Pagina e applicando le proprietà del nodo appropriate.

Ad esempio, per impostazione predefinita [**Crea pagina** procedura guidata](/help/sites-authoring/managing-pages.md#creating-a-new-page) mostra i campi raggruppati in **Altri titoli e descrizioni**. Per nasconderli, configura:

1. Creare il componente Pagina in `/apps`.
1. Creare una sostituzione (tramite *finestra di dialogo* fornite da [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) per `basic` del componente Pagina, ad esempio:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Come riferimento, vedere:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   Tuttavia, ***deve*** non modificare nulla in `/libs` percorso.
   >
   Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe benissimo essere sovrascritto quando applichi un hotfix o un feature pack).
   >
   Il metodo consigliato per la configurazione e altre modifiche è:
   >
   1. Ricrea l&#39;elemento richiesto, ovvero come esiste in `/libs`) in `/apps`
   1. Apporta le modifiche in `/apps`

1. Imposta il `path` proprietà su `basic` per puntare alla sostituzione della scheda di base (vedi anche il passaggio successivo). Ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Creare un override di `basic` - `moretitles` nel percorso corrispondente; ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Applica la proprietà del nodo appropriata:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valore**: `false`

   Il **Altri titoli e descrizioni** non verrà più visualizzata nella sezione **Crea pagina** procedura guidata.

>[!NOTE]
>
Quando configuri le proprietà della pagina da utilizzare con le Live Copy, consulta [Configurazione dei blocchi MSM nelle proprietà della pagina](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) per ulteriori dettagli.

## Configurazione di esempio delle proprietà di pagina {#sample-configuration-of-page-properties}

In questo esempio viene illustrata la tecnica della finestra di dialogo [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md), compreso l&#39;uso di [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Illustra inoltre l’utilizzo di entrambi `cq:showOnCreate` e `cq:hideOnEdit`.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri il progetto aem-authoring-extension-page-dialog su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
