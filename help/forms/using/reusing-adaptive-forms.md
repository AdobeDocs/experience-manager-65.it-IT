---
title: Riutilizzo dei moduli adattivi
seo-title: Reusing adaptive forms
description: È possibile riutilizzare un modulo adattivo esistente per creare nuovi moduli adattivi.
seo-description: You can reuse an existing adaptive form to create new adaptive forms.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Riutilizzo dei moduli adattivi {#reusing-adaptive-forms}

## Introduzione {#introduction}

Se si desidera utilizzare alcune delle proprietà di un modulo adattivo esistente per generarne una nuova, è sufficiente utilizzare la funzionalità di copia e incolla. Inoltre, puoi incollare il nuovo modulo adattivo nel percorso della cartella desiderato. Vengono replicate tutte le proprietà dei metadati e vengono copiati anche XFA e XSD per i moduli adattivi basati su XFA e XSD.

>[!NOTE]
>
>Lo stato e i dettagli della revisione non vengono copiati. Ad esempio, se il modulo adattivo viene pubblicato e quindi lo si copia, lo stato del modulo adattivo incollato non viene pubblicato. Analogamente, se una risorsa copiata è in fase di revisione, la risorsa incollata non è sotto la stessa revisione.

### Copiare un modulo adattivo {#copy-an-adaptive-form}

Copia un modulo adattivo utilizzando uno dei seguenti approcci:

1. Fai clic su Copia ![aem6forms_copy](assets/aem6forms_copy.png) da Azioni rapide.

   >[!NOTE]
   >
   >Le azioni rapide sono gli elementi che vengono visualizzati su una miniatura al passaggio del mouse.

1. Seleziona il modulo adattivo. Il processo di selezione è diverso per le diverse viste.

   Se siete nella vista a schede, passate alla modalità di selezione facendo clic sulla selezione ![aem6forms_check-cerchio](assets/aem6forms_check-circle.png) e fai clic su tutti i moduli adattivi da copiare.

   Se ti trovi nella vista a elenco, fai clic sulle caselle di controllo di tutti i moduli adattivi per selezionarli.

   >[!NOTE]
   >
   >Tutte le risorse selezionate devono essere moduli adattivi perché la funzionalità di copia e incolla è supportata solo per i moduli adattivi e tutte le risorse selezionate devono essere presenti nella stessa cartella.

   Dopo aver selezionato le risorse, fai clic sulla copia ![aem6forms_copy](assets/aem6forms_copy.png) presente nella barra degli strumenti per copiare il modulo adattivo selezionato.

### Incolla un modulo adattivo {#paste-an-adaptive-form}

Quando si fa clic sull’azione di copia, la modalità di selezione viene automaticamente chiusa e l’opzione incolla ![aem6forms_paste](assets/aem6forms_paste.png) icona visibile. Ora vai al percorso della cartella desiderato e fai clic su incolla ![aem6forms_paste](assets/aem6forms_paste.png) per incollare il modulo adattivo copiato.

Se si incolla nella stessa cartella o in un altro file con lo stesso nome di nodo (con il quale è memorizzato nell&#39;archivio CRX) esiste in questa cartella di destinazione, viene aggiunto 1 al suffisso (ad esempio, myaf diventa myaf1 e se myaf1 esiste nella stessa posizione, myaf diventa myaf2. Tutte le altre proprietà rimangono invariate rispetto al modulo adattivo originale.

Dopo aver fatto clic sul pulsante Incolla ![aem6forms_paste](assets/aem6forms_paste.png) icona, si nasconderà di nuovo. È possibile incollare una sola volta. Per creare nuovamente una copia della stessa risorsa, copiala nuovamente.

### Modificare il contenuto del nuovo modulo adattivo {#change-contents-of-new-adaptive-form}

Il contenuto di un modulo adattivo incollato può essere modificato utilizzando i seguenti approcci per renderlo diverso dal modulo copiato:

1. **Modificare le proprietà dei metadati:**

   È possibile modificare le proprietà dei metadati del modulo adattivo, ad esempio titolo e descrizione. Per ulteriori dettagli sulle proprietà dei metadati e su come modificarle, consulta [Gestione dei metadati dei moduli](/help/forms/using/manage-form-metadata.md)

1. **Modificare XFA/XSD per Forms adattivo basato su XFA/XSD:**

   È possibile modificare XFA/XSD utilizzato nei moduli adattivi. Per informazioni sulle modalità di modifica di questi moduli adattivi, consulta [Gestione dei metadati dei moduli](/help/forms/using/manage-form-metadata.md)

1. **Ripubblica:**

   La risorsa incollata è diversa da quella copiata. Puoi pubblicarlo come nuova risorsa per renderlo disponibile agli utenti finali. Per informazioni su come pubblicare una risorsa, consulta [Pubblicazione e annullamento della pubblicazione dei moduli](/help/forms/using/publishing-unpublishing-forms.md)
