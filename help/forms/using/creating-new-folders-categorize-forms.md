---
title: Creare nuove cartelle per categorizzare i moduli
seo-title: Create new folders to categorize forms
description: Utilizza le cartelle per organizzare modelli di modulo, PDF, risorse e moduli adattivi.
seo-description: Use folders to organize your form templates, PDFs, resources, and adaptive forms.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# Creare nuove cartelle per categorizzare i moduli {#create-new-folders-to-categorize-forms}

Puoi organizzare meglio le risorse utilizzando le cartelle. Poiché AEM Forms supporta diversi tipi di risorse (modelli di modulo, PDF, documenti, risorse e moduli adattivi con vari metadati), è possibile utilizzare le cartelle per classificare i moduli in base ai criteri desiderati.

AEM Forms consente di modificare il titolo di una cartella. Il titolo non corrisponde al nome del nodo in cui è memorizzata la cartella nell&#39;archivio. Il titolo viene invece mantenuto come metadati per la cartella. Se modifichi il titolo di una cartella, il percorso di qualsiasi risorsa presente all’interno della cartella non viene modificato.

## Crea una cartella . {#create-a-folder}

Puoi creare una cartella in AEM Forms in uno dei seguenti modi:

* Carica un file ZIP contenente le risorse nella struttura di cartelle desiderata (vedi, [Recupero documenti XDP e PDF in AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Crea una cartella vuota

1. Accedi all’interfaccia utente di AEM Forms all’indirizzo `https://<server>:<port>/aem/forms.html`.
1. Passare alla posizione in cui si desidera creare una cartella.
1. Fai clic su ![aem6forms_add](assets/aem6forms_add.png) nella barra degli strumenti, quindi seleziona **[!UICONTROL Crea cartella]**.

1. Immetti i seguenti dettagli:

   * **Titolo:** Nome visualizzato per la cartella
   * **Nome:** *(Obbligatorio)* Nome del nodo in cui si desidera archiviare la cartella nell&#39;archivio

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici o trattini (-) e trattini bassi (_) caratteri speciali. Tutti gli altri caratteri speciali immessi nel titolo vengono automaticamente sostituiti da un trattino e viene richiesto di confermare il nuovo nome. Puoi scegliere di continuare con il nome suggerito o modificarlo ulteriormente.

1. Fai clic su **[!UICONTROL Invia].**

   Nell’elenco delle risorse, nella posizione corrente viene visualizzata una nuova cartella con il titolo definito.

   Se esiste una cartella con il nome specificato, l’invio non riesce e viene visualizzato un errore. Puoi visualizzare il messaggio di errore passando il cursore sopra l’errore ![aem6forms_error_alert](assets/aem6forms_error_alert.png) accanto al campo del nome.

### Modifica il titolo della cartella {#edit-the-folder-title-br}

1. Seleziona la cartella di cui desideri modificare il titolo.
1. Fai clic sul pulsante Modifica ![aem6forms_edit](assets/aem6forms_edit.png) nella barra degli strumenti.
1. Inserisci il nuovo titolo. Nel campo di testo viene inserito automaticamente il valore corrente del titolo della cartella. È possibile modificarlo in un nuovo valore.
1. Fai clic su **[!UICONTROL Invia].**
