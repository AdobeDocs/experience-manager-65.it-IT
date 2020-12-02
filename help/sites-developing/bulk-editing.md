---
title: Configurazione della pagina per la modifica collettiva delle proprietà pagina
seo-title: Configurazione della pagina per la modifica collettiva delle proprietà pagina
description: La modifica collettiva delle proprietà della pagina consente di modificare le proprietà di più pagine contemporaneamente
seo-description: La modifica collettiva delle proprietà della pagina consente di modificare le proprietà di più pagine contemporaneamente
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: b08149e00c418319ebacec71c56472ad4e8e1089
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---


# Configurazione della pagina per la modifica collettiva delle proprietà pagina {#configuring-your-page-for-bulk-editing-of-page-properties}

[La modifica collettiva delle ](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) proprietà della pagina consente di modificare le proprietà di più pagine alla volta.

A causa della possibilità di valori diversi, per impostazione predefinita le proprietà della pagina non sono abilitate per la modifica collettiva. Devono essere esplicitamente consentiti (abilitati). Per definire le proprietà della pagina in modo che siano disponibili per la modifica collettiva, è necessario considerare alcune implicazioni, ad esempio:

* Alcuni campi sono in genere univoci; ad esempio un titolo di pagina. È necessario stabilire se è utile abilitare tali campi per la modifica collettiva, quando verrà applicato un valore.
* Alcuni campi possono avere più valori; questo richiede una rappresentazione significativa durante il rendering.

   Ad esempio, una casella di controllo che indica &quot;Pronto per la pubblicazione&quot;. Potrebbero essere presenti diversi valori prima della modifica in blocco (ad esempio, pronta, in-revisione, in corso).

>[!CAUTION]
>
>La modifica collettiva delle proprietà della pagina è:
>
>* Non disponibile nell’interfaccia classica.
>* Non disponibile per le pagine all&#39;interno di una Live Copy.
>* Disponibile solo per le pagine con lo stesso tipo di risorsa.

>



>[!NOTE]
>
>La modifica collettiva è disponibile anche per le risorse. È molto simile, ma differisce in alcuni punti. Per ulteriori informazioni, vedere [Modifica delle proprietà di più risorse](/help/assets/metadata.md). Potete personalizzare i campi nell&#39;editor metadati di massa per le risorse utilizzando l&#39; [Editor schema](/help/assets/metadata-schemas.md).

## Abilitazione di un campo {#enabling-a-field}

>[!NOTE]
>
>Alcuni campi possono avere più valori; questo richiede una rappresentazione significativa durante il rendering. Per questo motivo, è consigliabile abilitare solo i seguenti tipi di campo:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`

>



I campi sono attivati sul componente pagina (*non* nel modello):

1. Utilizzando un CRXDE Lite (o un metodo equivalente) potete aprire il componente della pagina.

   Esempio: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Nell&#39;esempio si presuppone che nell&#39;istanza siano stati installati i componenti core, il che si verifica se l&#39;istanza è in esecuzione con contenuto di esempio We.Retail. Per ulteriori informazioni, consulta la [Documentazione sui componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html).

1. Andate al campo obbligatorio all&#39;interno della definizione `cq:dialog`.
1. Definire la seguente proprietà sul nodo campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valore**:  `true`

   Ad esempio, per la pagina standard [foundation component](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   La proprietà viene definita in:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >***non è necessario*** modificare nulla nel percorso `/libs`.
   >
   >Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >    1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
   >    1. Apportare modifiche all&#39;interno di `/apps`


1. Selezionare **Salva tutto** per mantenere gli aggiornamenti.

