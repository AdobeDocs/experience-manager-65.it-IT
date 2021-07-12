---
title: Creazione di nuove cartelle per classificare i moduli
seo-title: Creazione di nuove cartelle per classificare i moduli
description: Utilizzare le cartelle per organizzare i modelli di modulo, i PDF, le risorse e i moduli adattivi.
seo-description: Utilizzare le cartelle per organizzare i modelli di modulo, i PDF, le risorse e i moduli adattivi.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Creazione di nuove cartelle per classificare i moduli {#create-new-folders-to-categorize-forms}

Puoi organizzare meglio le risorse utilizzando le cartelle. Poiché AEM Forms supporta diversi tipi di risorse (modelli di modulo, PDF, documenti, risorse e moduli adattivi con vari metadati), è possibile utilizzare le cartelle per suddividere i moduli in categorie in base ai criteri desiderati.

AEM Forms consente di modificare il titolo di una cartella. Il titolo non corrisponde al nome del nodo in cui la cartella è memorizzata nel repository. Il titolo viene invece mantenuto come metadati per la cartella. Se modifichi il titolo di una cartella, il percorso di qualsiasi risorsa presente all’interno della cartella non viene modificato.

## Crea una cartella . {#create-a-folder}

Puoi creare una cartella in AEM Forms in uno dei seguenti modi:

* Carica un file ZIP contenente risorse nella struttura di cartelle desiderata (consulta [Ottenere documenti XDP e PDF in AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Crea una nuova cartella vuota

1. Accedi all&#39;interfaccia utente di AEM Forms all&#39;indirizzo `https://<server>:<port>/aem/forms.html`.
1. Passa alla posizione in cui desideri creare una cartella.
1. Fai clic sull&#39;icona ![aem6forms_add](assets/aem6forms_add.png) nella barra degli strumenti, quindi seleziona **[!UICONTROL Crea cartella]**.

1. Immetti i seguenti dettagli:

   * **Titolo:** nome visualizzato per la cartella
   * **Nome:** *(obbligatorio)* il nome del nodo in cui si desidera memorizzare la cartella nel repository

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici oppure i trattini (-) e i caratteri speciali carattere di sottolineatura (_). Tutti gli altri caratteri speciali immessi nel titolo vengono automaticamente sostituiti con un trattino e viene richiesto di confermare il nuovo nome. Puoi scegliere di continuare con il nome suggerito o modificarlo ulteriormente.

1. Fare clic su **[!UICONTROL Invia].**

   Nella posizione corrente nell’elenco delle risorse viene visualizzata una nuova cartella con il titolo definito.

   Se esiste una cartella con il nome specificato, l’invio non riesce e viene visualizzato un errore. Per visualizzare il messaggio di errore, passa il puntatore del mouse sull&#39;icona di errore ![aem6forms_error_alert](assets/aem6forms_error_alert.png) visualizzata accanto al campo del nome.

### Modificare il titolo della cartella {#edit-the-folder-title-br}

1. Selezionare la cartella di cui si desidera modificare il titolo.
1. Fai clic sull&#39;icona Modifica ![aem6forms_edit](assets/aem6forms_edit.png) nella barra degli strumenti.
1. Inserisci il nuovo titolo. Il campo di testo viene precompilato con il valore corrente del titolo della cartella. È possibile modificarlo in un nuovo valore.
1. Fare clic su **[!UICONTROL Invia].**
