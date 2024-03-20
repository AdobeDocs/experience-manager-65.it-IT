---
title: Configurazione della pagina per la modifica in blocco delle proprietà di pagina
description: La modifica in blocco delle proprietà di pagina consente di modificare le proprietà di più pagine contemporaneamente
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Configurazione della pagina per la modifica in blocco delle proprietà di pagina {#configuring-your-page-for-bulk-editing-of-page-properties}

[Modifica in serie delle proprietà di pagina](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) consente di modificare le proprietà di più pagine contemporaneamente.

A causa della possibilità di valori diversi, le proprietà della pagina non sono abilitate per la modifica in serie come impostazione predefinita. Devono essere esplicitamente consentiti (abilitati). Quando definisci le proprietà della pagina da rendere disponibili per la modifica in blocco, devi tenere in considerazione alcune implicazioni, ad esempio:

* Alcuni campi sono in genere univoci, ad esempio il titolo di una pagina. Decidi se è utile abilitare questi campi per la modifica in blocco, quando verrà applicato un valore.
* Alcuni campi possono avere più valori, che devono essere rappresentati in modo significativo durante il rendering.

  Ad esempio, la casella di controllo &quot;Pronto per la pubblicazione&quot;. Questo potrebbe avere diversi valori prima della modifica in blocco (ad esempio, pronto, in revisione, in corso).

>[!CAUTION]
>
>La modifica in blocco delle proprietà di pagina è:
>
>* Non disponibile nell’interfaccia classica.
>* Non disponibile per le pagine all’interno di una Live Copy.
>* Disponibile solo per le pagine con lo stesso tipo di risorsa.
>

>[!NOTE]
>
>La modifica in blocco è disponibile anche per Assets. È molto simile, ma differisce in alcuni punti. Consulta [Modifica delle proprietà di più risorse](/help/assets/metadata.md) per informazioni complete. Puoi personalizzare i campi nell’editor di metadati in blocco per le risorse utilizzando [Editor schema](/help/assets/metadata-schemas.md).

## Abilitazione di un campo {#enabling-a-field}

>[!NOTE]
>
>Alcuni campi possono avere più valori, che devono essere rappresentati in modo significativo durante il rendering. Per questo motivo è necessario abilitare solo i seguenti tipi di campo:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>

I campi sono abilitati nel componente Pagina (*non* sul modello):

1. Utilizzando CRXDE Liti (o un metodo equivalente) apri il componente Pagina.

   Esempio: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Questo esempio presuppone che i Componenti core siano stati installati nell&#39;istanza, il che avviene se l&#39;istanza è in esecuzione con il contenuto di esempio We.Retail. Consulta la [Documentazione dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) per ulteriori informazioni.

1. Passa al campo richiesto all’interno di `cq:dialog` definizione.
1. Definisci la seguente proprietà sul nodo del campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

   Ad esempio, per la pagina standard [componente di base](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   La proprietà viene definita il:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Tu ***deve*** non modificare nulla in `/libs` percorso.
   >
   >Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe benissimo essere sovrascritto quando applichi un hotfix o un feature pack).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >    1. Ricrea l&#39;elemento richiesto, ovvero come esiste in `/libs`) in `/apps`
   >    1. Apporta le modifiche in `/apps`

1. Seleziona **Salva tutto** per mantenere gli aggiornamenti.
