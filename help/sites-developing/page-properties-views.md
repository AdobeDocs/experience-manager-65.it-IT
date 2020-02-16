---
title: Personalizzazione delle visualizzazioni delle proprietà pagina
seo-title: Personalizzazione delle visualizzazioni delle proprietà pagina
description: Ogni pagina dispone di un set di proprietà che è possibile modificare come necessario
seo-description: Ogni pagina dispone di un set di proprietà che è possibile modificare come necessario
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d

---


# Personalizzazione delle visualizzazioni delle proprietà pagina{#customizing-views-of-page-properties}

Ogni pagina dispone di un set di [proprietà](/help/sites-authoring/editing-page-properties.md) che possono essere visualizzate e modificate dagli utenti; alcuni sono necessari quando si crea la pagina (vista di creazione), altri possono essere visualizzati e modificati (vista di modifica) in un secondo momento. Queste proprietà di pagina sono definite e rese disponibili dalla finestra di dialogo ( `cq:dialog`) del componente pagina appropriato.

>[!CAUTION]
>
>La personalizzazione della visualizzazione delle proprietà della pagina non è disponibile nell’interfaccia classica.

Lo stato predefinito per ogni proprietà pagina è:

* nascosta nella visualizzazione di creazione (ad esempio, **Creazione guidata pagina** )

* disponibile nella visualizzazione di modifica (ad esempio, **Visualizza proprietà**)

Se è necessaria una modifica, i campi devono essere configurati in modo specifico. Questa operazione viene eseguita utilizzando le proprietà nodo appropriate:

* Proprietà di pagina da rendere disponibile nella vista di creazione (ad esempio, procedura guidata **Crea pagina** ):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Proprietà pagina per essere disponibile nella visualizzazione di modifica (ad esempio, opzione **Visualizza**/**Modifica**) **Proprietà** ):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Ad esempio, vedere le impostazioni per i campi raggruppati in **Altri titoli e Descrizione** nella scheda **Base** del componente Pagina di base. Questi sono visibili nella procedura guidata **Crea pagina** come `cq:showOnCreate` impostato su `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Per una guida alla personalizzazione delle proprietà di pagina, consultate l’esercitazione [](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) Estensione delle proprietà di pagina.

## Configurazione delle proprietà pagina {#configuring-your-page-properties}

È inoltre possibile configurare i campi disponibili configurando la finestra di dialogo del componente pagina e applicando le proprietà nodo appropriate.

Ad esempio, per impostazione predefinita, la procedura guidata [**Crea pagina **mostra i campi raggruppati in](/help/sites-authoring/managing-pages.md#creating-a-new-page)Altri titoli e Descrizione****. Per nascondere questi elementi è necessario configurare:

1. Create il componente della pagina in `/apps`.
1. Creare un override (utilizzando la *finestra di dialogo* fornita dalla fusione [risorse](/help/sites-developing/sling-resource-merger.md)Sling) per la `basic` sezione del componente della pagina; ad esempio:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Come riferimento, vedete:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   Tuttavia, non ***è necessario*** modificare nulla nel `/libs` percorso.
   Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
   Il metodo consigliato per la configurazione e altre modifiche è:
   1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
   1. Apportare modifiche all&#39;interno `/apps`


1. Impostate la `path` proprietà su `basic` per puntare all&#39;override della scheda di base (vedere anche il passaggio successivo). Esempio:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Creare una sostituzione della sezione `basic` - `moretitles` sul percorso corrispondente; ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Applicare la proprietà node appropriata:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valore**: `false`
   La sezione **Altri titoli e descrizioni** non verrà più visualizzata nella procedura guidata **Crea pagina** .

>[!NOTE]
Per ulteriori informazioni, vedere [Configurazione dei blocchi MSM sulle proprietà](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) di pagina per l&#39;utilizzo con copie dal vivo.

## Configurazione di esempio delle proprietà pagina {#sample-configuration-of-page-properties}

Questo esempio illustra la tecnica della finestra di dialogo delle differenze della fusione delle risorse [Sling](/help/sites-developing/sling-resource-merger.md); compreso l&#39;uso di [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Inoltre illustra l&#39;uso di `cq:showOnCreate` e `cq:hideOnEdit`.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto Aem-authoring-extension-page-dialog su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
