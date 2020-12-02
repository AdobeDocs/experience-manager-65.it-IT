---
title: Riutilizzo di moduli adattivi
seo-title: Riutilizzo di moduli adattivi
description: È possibile riutilizzare un modulo adattivo esistente per creare nuovi moduli adattivi.
seo-description: È possibile riutilizzare un modulo adattivo esistente per creare nuovi moduli adattivi.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Riutilizzo di moduli adattivi {#reusing-adaptive-forms}

## Introduzione {#introduction}

Se si desidera utilizzare alcune delle proprietà di un modulo adattivo esistente per generare un nuovo modulo, è sufficiente utilizzare la funzione di copia-incolla. Inoltre, è possibile incollare il nuovo modulo adattivo nel percorso della cartella desiderato. Vengono replicate tutte le proprietà dei metadati e vengono copiati anche XFA e XSD per i moduli adattivi basati su XFA e XSD.

>[!NOTE]
>
>Lo stato e i dettagli della revisione non vengono copiati. Ad esempio, se il modulo adattivo viene pubblicato e successivamente copiato, lo stato del modulo adattivo incollato non viene pubblicato. Analogamente, se una risorsa copiata è in fase di revisione, la risorsa incollata non si trova nella stessa revisione.

### Copiare un modulo adattivo {#copy-an-adaptive-form}

Copiate un modulo adattivo utilizzando uno dei seguenti approcci:

1. Fare clic sull&#39;icona Copia ![aem6forms_copy](assets/aem6forms_copy.png) dalle azioni rapide.

   >[!NOTE]
   >
   >Le azioni rapide sono gli elementi di azione visualizzati sopra una miniatura al passaggio del mouse.

1. Selezionare il modulo adattivo. Il processo di selezione è diverso per le diverse viste.

   Se vi trovate nella vista a schede, passate alla modalità di selezione facendo clic sull&#39;icona ![aem6forms_check-cerchio](assets/aem6forms_check-circle.png) e fate clic su tutti i moduli adattivi da copiare.

   Se si è nella vista a elenco, fare clic sulle caselle di controllo di tutti i moduli adattivi per selezionarli.

   >[!NOTE]
   >
   >Tutte le risorse selezionate devono essere moduli adattivi perché la funzione di copia e incolla è supportata solo per i moduli adattivi e tutte le risorse selezionate devono essere presenti nella stessa cartella.

   Dopo aver selezionato le risorse, fate clic sull&#39;icona Copia ![aem6forms_copy](assets/aem6forms_copy.png) presente nella barra degli strumenti per copiare il modulo adattivo selezionato.

### Incolla un modulo adattivo {#paste-an-adaptive-form}

Facendo clic sull&#39;azione di copia, la modalità di selezione viene chiusa automaticamente e l&#39;icona Incolla ![aem6forms_paste](assets/aem6forms_paste.png) diventa visibile. Passate ora al percorso della cartella desiderato e fate clic sull&#39;icona Incolla ![aem6forms_paste](assets/aem6forms_paste.png) per incollare il modulo adattivo copiato.

Se incollate nella stessa cartella o in un altro file con lo stesso nome di nodo (con il quale è memorizzato nell’archivio CRX) già presente nella cartella di destinazione, 1 viene aggiunto al suffisso (ad esempio, myaf diventa myaf1 e se myaf1 esiste nella stessa posizione, myaf diventa myaf2. Tutte le altre proprietà rimangono invariate rispetto al modulo adattivo originale.

Dopo aver fatto clic sull&#39;icona Incolla ![aem6forms_paste](assets/aem6forms_paste.png), il file verrà nuovamente nascosto. È possibile incollare una sola volta. Per creare nuovamente una copia della stessa risorsa, copiatela di nuovo.

### Modifica del contenuto del nuovo modulo adattivo {#change-contents-of-new-adaptive-form}

Il contenuto di un modulo adattivo incollato può essere modificato utilizzando i seguenti approcci per renderlo diverso dal modulo copiato:

1. **Cambiare le proprietà dei metadati:**

   È possibile modificare le proprietà dei metadati del modulo adattivo, ad esempio titolo e descrizione. Per ulteriori dettagli sulle proprietà dei metadati e sulle modalità di modifica, vedere [Gestione dei metadati dei moduli](/help/forms/using/manage-form-metadata.md)

1. **Modificare XFA/XSD per Forms adattivo basato su XFA/XSD:**

   È possibile modificare l&#39;XFA/XSD utilizzato nei moduli adattivi. Per sapere come è possibile modificare questi moduli adattivi, vedere [Gestione dei metadati dei moduli](/help/forms/using/manage-form-metadata.md)

1. **Ripubblica:**

   La risorsa incollata è diversa da quella copiata. Potete pubblicarlo come nuova risorsa per renderlo disponibile agli utenti finali. Per informazioni su come pubblicare una risorsa, vedere [Pubblicazione e annullamento della pubblicazione di moduli](/help/forms/using/publishing-unpublishing-forms.md)

