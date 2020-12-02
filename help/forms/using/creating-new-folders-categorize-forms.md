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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Creare nuove cartelle per classificare i moduli {#create-new-folders-to-categorize-forms}

Potete organizzare meglio le risorse mediante le cartelle. Poiché  AEM Forms supporta diversi tipi di risorse (modelli di modulo, PDF, documenti, risorse e moduli adattivi, con vari metadati), è possibile utilizzare le cartelle per suddividere i moduli in categorie in base ai criteri desiderati.

 AEM Forms consente di modificare il titolo di una cartella. Il titolo non corrisponde al nome del nodo in cui è memorizzata la cartella nella directory archivio. Il titolo viene invece mantenuto come metadati per la cartella. Se modificate il titolo di una cartella, il percorso di qualsiasi risorsa presente nella cartella non viene modificato.

## Crea una cartella . {#create-a-folder}

Potete creare una cartella in  AEM Forms in uno dei seguenti modi:

* Caricate un file ZIP contenente le risorse nella struttura di cartelle desiderata (consultate [Ottenimento di XDP e documenti PDF in  AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Creare una nuova cartella vuota

1. Accedete all&#39;interfaccia utente  AEM Forms all&#39;indirizzo `https://<server>:<port>/aem/forms.html`.
1. Andate alla posizione in cui desiderate creare una cartella.
1. Fare clic sull&#39;icona ![aem6forms_add](assets/aem6forms_add.png) nella barra degli strumenti, quindi selezionare **[!UICONTROL Crea cartella]**.

1. Inserite i seguenti dettagli:

   * **Titolo:Nome** visualizzato per la cartella
   * **Nome:** *(obbligatorio)* Nome del nodo in cui si desidera memorizzare la cartella nell’archivio

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici, oppure caratteri speciali trattino (-) e carattere di sottolineatura (_). Eventuali altri caratteri speciali immessi nel titolo vengono sostituiti automaticamente con un trattino e viene richiesto di confermare il nuovo nome. Potete scegliere di continuare con il nome suggerito o di modificarlo ulteriormente.

1. Fare clic su **[!UICONTROL Invia].**

   Una nuova cartella con il titolo definito viene visualizzata nella posizione corrente nell’elenco delle risorse.

   Se esiste una cartella con il nome specificato, l&#39;invio non riesce con un errore. Per visualizzare il messaggio di errore, passare il puntatore del mouse sull&#39;icona di errore ![aem6forms_error_alert](assets/aem6forms_error_alert.png) visualizzata accanto al campo del nome.

### Modificare il titolo della cartella {#edit-the-folder-title-br}

1. Selezionate la cartella di cui desiderate modificare il titolo.
1. Fare clic sull&#39;icona Modifica ![aem6forms_edit](assets/aem6forms_edit.png) nella barra degli strumenti.
1. Inserite il nuovo titolo. Il campo di testo è precompilato con il valore corrente del titolo della cartella. È possibile modificarlo in un nuovo valore.
1. Fare clic su **[!UICONTROL Invia].**

