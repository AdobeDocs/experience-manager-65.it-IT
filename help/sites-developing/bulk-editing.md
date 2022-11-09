---
title: Configurazione della pagina per la modifica in serie delle proprietà di pagina
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: La modifica collettiva delle proprietà di pagina consente di modificare le proprietà di più pagine alla volta
seo-description: Bulk editing of page properties allows you to edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 2%

---

# Configurazione della pagina per la modifica in serie delle proprietà di pagina {#configuring-your-page-for-bulk-editing-of-page-properties}

[Modifica in serie delle proprietà di pagina](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) consente di modificare le proprietà di più pagine alla volta.

A causa della possibilità di valori diversi, le proprietà della pagina non sono abilitate per la modifica collettiva come impostazione predefinita. Devono essere esplicitamente consentiti (abilitati). Quando definisci le proprietà di pagina da rendere disponibili per la modifica collettiva, devi considerare alcune implicazioni, come:

* Taluni campi sono in genere unici; ad esempio un titolo della pagina. È necessario stabilire se è utile abilitare tali campi per la modifica collettiva, quando verrà applicato un valore.
* Alcuni campi possono avere più valori; questo richiede una rappresentazione significativa durante il rendering.

   Ad esempio, una casella di controllo che indica &quot;Pronto per la pubblicazione&quot;. Potrebbero essere presenti diversi valori prima della modifica in serie (ad esempio pronti, in revisione o in corso).

>[!CAUTION]
>
>Modifica in serie delle proprietà di pagina:
>
>* Non disponibile nell’interfaccia classica.
>* Non disponibile per le pagine all’interno di una Live Copy.
>* Disponibile solo per le pagine con lo stesso tipo di risorsa.
>


>[!NOTE]
>
>La modifica in serie è disponibile anche per Assets. È molto simile, ma differisce in alcuni punti. Vedi [Modifica delle proprietà di più risorse](/help/assets/metadata.md) per informazioni complete. Puoi personalizzare i campi nell’editor metadati in blocco per Assets utilizzando [Editor di schema](/help/assets/metadata-schemas.md).

## Abilitazione di un campo {#enabling-a-field}

>[!NOTE]
>
>Alcuni campi possono avere più valori; questo richiede una rappresentazione significativa durante il rendering. Per questo motivo è consigliabile abilitare solo i seguenti tipi di campi:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>


I campi sono abilitati nel componente pagina (*not* sul modello):

1. Utilizzando CRXDE Lite (o un metodo equivalente) apri il componente pagina.

   Esempio: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Questo esempio presuppone che i componenti core siano stati installati nell&#39;istanza, il che si verifica se l&#39;istanza è in esecuzione con contenuto di esempio di We.Retail. Consulta la sezione [Documentazione sui componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) per ulteriori informazioni.

1. Passa al campo richiesto all’interno della `cq:dialog` definizione.
1. Definire la seguente proprietà sul nodo del campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

   Ad esempio, per la pagina standard [componente base](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   La proprietà viene definita in:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >You ***deve*** non modificare nulla nel `/libs` percorso.
   >
   >Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >    1. Ricrea l&#39;elemento richiesto (ovvero così come esiste in `/libs`) `/apps`
   >    1. Apporta modifiche a `/apps`


1. Seleziona **Salva tutto** per mantenere gli aggiornamenti.
