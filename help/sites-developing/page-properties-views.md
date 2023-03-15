---
title: Personalizzazione delle visualizzazioni delle proprietà pagina
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
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# Personalizzazione delle visualizzazioni delle proprietà pagina{#customizing-views-of-page-properties}

Ogni pagina ha un set di [proprietà](/help/sites-authoring/editing-page-properties.md) che possono essere visualizzate e modificate dagli utenti; alcune sono necessarie quando si crea la pagina (creazione di una visualizzazione), altre possono essere visualizzate e modificate (modifica visualizzazione) in un secondo momento. Queste proprietà della pagina vengono definite e rese disponibili dalla finestra di dialogo ( `cq:dialog`) del componente pagina appropriato.

>[!CAUTION]
>
>La personalizzazione della visualizzazione delle proprietà della pagina non è disponibile nell’interfaccia classica.

Lo stato predefinito per ogni proprietà di pagina è:

* nascosto nella vista di creazione (ad esempio **Crea pagina** procedura guidata)

* disponibile nella vista di modifica (ad esempio **Visualizza proprietà**)

Se è necessaria una modifica, i campi devono essere configurati in modo specifico. Questa operazione viene eseguita utilizzando le proprietà del nodo appropriate:

* Proprietà di pagina da rendere disponibile nella visualizzazione di creazione (ad esempio **Crea pagina** procedura guidata):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Proprietà di pagina da rendere disponibile nella visualizzazione di modifica (ad esempio **Visualizza**/**Modifica**) **Proprietà** opzione):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Ad esempio, vedere le impostazioni per i campi raggruppati sotto la **Altri titoli e descrizioni** sulla **Base** scheda per il componente Pagina di base. Sono visibili nella **Crea pagina** procedura guidata `cq:showOnCreate` è impostato su `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulta la sezione [Esercitazione sull’estensione delle proprietà pagina](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) per una guida alla personalizzazione delle proprietà della pagina.

## Configurazione delle proprietà di pagina {#configuring-your-page-properties}

Puoi anche configurare i campi disponibili configurando la finestra di dialogo del componente pagina e applicando le proprietà nodo appropriate.

Ad esempio, per impostazione predefinita il [**Crea pagina** procedura guidata](/help/sites-authoring/managing-pages.md#creating-a-new-page) mostra i campi raggruppati sotto **Altri titoli e descrizioni**. Per nascondere questi elementi è necessario configurare:

1. Crea il componente pagina in `/apps`.
1. Crea un override (utilizzando *dialogo diff* di cui [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) per `basic` sezione del componente page; ad esempio:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Come riferimento, vedi:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   Tuttavia, ***deve*** non modificare nulla nel `/libs` percorso.
   Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).
   Il metodo consigliato per la configurazione e altre modifiche è:
   1. Ricrea l&#39;elemento richiesto (ovvero così come esiste in `/libs`) `/apps`
   1. Apporta modifiche a `/apps`


1. Imposta la `path` proprietà su `basic` per puntare alla sostituzione della scheda di base (vedi anche il passaggio successivo). Esempio:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Crea una sostituzione del `basic` - `moretitles` sezione nel percorso corrispondente; ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Applica la proprietà nodo appropriata:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valore**: `false`

   La **Altri titoli e descrizioni** la sezione non verrà più visualizzata nella sezione **Crea pagina** procedura guidata.

>[!NOTE]
Durante la configurazione delle proprietà della pagina da utilizzare con le Live Copy vedi [Configurazione dei blocchi MSM nelle proprietà di pagina](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) per ulteriori dettagli.

## Configurazione di esempio delle proprietà di pagina {#sample-configuration-of-page-properties}

Questo esempio illustra la tecnica di dialogo delle differenze tra [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md); compreso l&#39;uso di [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Illustra inoltre l&#39;uso di entrambi `cq:showOnCreate` e `cq:hideOnEdit`.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-authoring-extension-page-dialog su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
