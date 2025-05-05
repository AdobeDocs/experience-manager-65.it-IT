---
title: Personalizzazione delle visualizzazioni delle proprietà di pagina
description: Ogni pagina dispone di un set di proprietà che è possibile modificare in base alle esigenze
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Personalizzazione delle visualizzazioni delle proprietà di pagina{#customizing-views-of-page-properties}

Ogni pagina dispone di un set di [proprietà](/help/sites-authoring/editing-page-properties.md) che possono essere visualizzate e modificate dagli utenti; alcune sono necessarie durante la creazione della pagina (crea visualizzazione), altre possono essere visualizzate e modificate (modifica visualizzazione) in una fase successiva. Queste proprietà di pagina sono definite e rese disponibili dalla finestra di dialogo ( `cq:dialog`) del componente pagina appropriato.

>[!CAUTION]
>
>La personalizzazione della visualizzazione delle proprietà di pagina non è disponibile nell’interfaccia classica.

Lo stato predefinito per ogni proprietà di pagina è:

* nascosto nella visualizzazione di creazione (ad esempio, **Creazione guidata pagina**)

* disponibile nella visualizzazione di modifica (ad esempio, **Visualizza proprietà**)

I campi devono essere configurati in modo specifico se è necessaria una modifica. Questa operazione viene eseguita utilizzando le proprietà del nodo appropriate:

* Proprietà di pagina da rendere disponibile nella visualizzazione di creazione (ad esempio, **Creazione guidata pagina**):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Proprietà di pagina da rendere disponibile nella visualizzazione di modifica (ad esempio, **Visualizza**/**Modifica**) **Proprietà**):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Ad esempio, vedi le impostazioni per i campi raggruppati sotto **Altri titoli e descrizioni** nella scheda **Base** del componente Pagina di base. Sono visibili nella procedura guidata **Crea pagina** poiché `cq:showOnCreate` è stato impostato su `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Per una guida alla personalizzazione delle proprietà di pagina, consulta il [tutorial Estensione delle proprietà di pagina](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=it).

## Configurazione delle proprietà della pagina {#configuring-your-page-properties}

Puoi anche configurare i campi disponibili configurando la finestra di dialogo del componente Pagina e applicando le proprietà del nodo appropriate.

Per impostazione predefinita, ad esempio, la procedura guidata [**Crea pagina**](/help/sites-authoring/managing-pages.md#creating-a-new-page) mostra i campi raggruppati in **Altri titoli e descrizioni**. Per nasconderli, configura:

1. Crea il componente Pagina in `/apps`.
1. Crea una sostituzione (utilizzando *dialog diff* fornito da [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) per la sezione `basic` del componente pagina, ad esempio:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Come riferimento, vedere:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   >Tuttavia, ***devi*** non modificare nulla nel percorso `/libs`.
   >
   >Il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >1. Ricrea l&#39;elemento richiesto (ovvero, poiché esiste in `/libs`) in `/apps`
   >1. Apporta le modifiche in `/apps`

1. Impostare la proprietà `path` su `basic` per puntare all&#39;override della scheda di base (vedere anche il passaggio successivo). Ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Creare una sostituzione della sezione `basic` - `moretitles` nel percorso corrispondente, ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Applica la proprietà del nodo appropriata:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valore**: `false`

   La sezione **Altri titoli e descrizioni** non verrà più visualizzata nella procedura guidata **Crea pagina**.

>[!NOTE]
>
>Durante la configurazione delle proprietà di pagina da utilizzare con le Live Copy, vedi [Configurazione dei blocchi MSM nelle proprietà di pagina](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) per ulteriori dettagli.

## Configurazione di esempio delle proprietà di pagina {#sample-configuration-of-page-properties}

In questo esempio viene illustrata la tecnica di dialogo diff di [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md), incluso l&#39;utilizzo di [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Illustra inoltre l&#39;utilizzo di `cq:showOnCreate` e `cq:hideOnEdit`.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-authoring-extension-page-dialog su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
