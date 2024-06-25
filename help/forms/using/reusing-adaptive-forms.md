---
title: Riutilizzo dei moduli adattivi
description: Puoi riutilizzare un modulo adattivo esistente per creare nuovi moduli adattivi.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms,Foundation Components
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# Riutilizzo dei moduli adattivi {#reusing-adaptive-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/reusing-adaptive-forms.html) |
| AEM 6.5 | Questo articolo |

## Introduzione {#introduction}

Se desideri utilizzare alcune delle proprietà di un modulo adattivo esistente per generarne uno nuovo, puoi semplicemente utilizzare la funzionalità di copia e incolla. Inoltre, puoi incollare il nuovo modulo adattivo nel percorso di cartella desiderato. Tutte le proprietà dei metadati vengono replicate e vengono copiati anche gli XFA e gli XSD per i moduli adattivi basati su XFA e XSD.

>[!NOTE]
>
>Lo stato e i dettagli della revisione non vengono copiati. Ad esempio, se il modulo adattivo è pubblicato e quindi lo copi, il modulo adattivo incollato si trova nello stato non pubblicato. Analogamente, se una risorsa copiata è in revisione, la risorsa incollata non è in revisione.

### Copiare un modulo adattivo {#copy-an-adaptive-form}

Copiare un modulo adattivo utilizzando uno dei seguenti approcci:

1. Fai clic su Copia ![aem6forms_copy](assets/aem6forms_copy.png) da Azioni rapide.

   >[!NOTE]
   >
   >Le azioni rapide sono le azioni che vengono visualizzate su una miniatura al passaggio del mouse.

1. Seleziona il modulo adattivo. Il processo di selezione è diverso per le diverse viste.

   Se ti trovi nella vista a schede, passa alla modalità di selezione facendo clic sulla selezione ![aem6forms_check-circle](assets/aem6forms_check-circle.png) e fai clic su tutti i moduli adattivi da copiare.

   Se ti trovi nella vista a elenco, fai clic sulle caselle di controllo di tutti i moduli adattivi per selezionarli.

   >[!NOTE]
   >
   >Tutte le risorse selezionate devono essere moduli adattivi perché la funzionalità di copia e incolla è supportata solo per i moduli adattivi e tutte le risorse selezionate devono essere presenti nella stessa cartella.

   Dopo aver selezionato le risorse, fai clic sulla copia ![aem6forms_copy](assets/aem6forms_copy.png) presente nella barra degli strumenti per copiare il modulo adattivo selezionato.

### Incollare un modulo adattivo {#paste-an-adaptive-form}

Facendo clic sull&#39;azione di copia, si esce automaticamente dalla modalità di selezione e si esegue l&#39;operazione Incolla ![aem6forms_incolla](assets/aem6forms_paste.png) visibile. Ora vai al percorso della cartella desiderato e fai clic sul pulsante Incolla ![aem6forms_incolla](assets/aem6forms_paste.png) per incollare il modulo adattivo copiato.

Se si incolla nella stessa cartella o in questa cartella di destinazione esiste un altro file con lo stesso nome di nodo (con il quale è memorizzato nell&#39;archivio CRX), al suffisso viene aggiunto 1 (ad esempio, myaf diventa myaf1 e, se myaf1 esiste nella stessa posizione, myaf diventa myaf2. Tutte le altre proprietà rimangono invariate rispetto al modulo adattivo originale.

Dopo aver fatto clic sull’icona Incolla ![aem6forms_incolla](assets/aem6forms_paste.png) icona, sarà di nuovo nascosto. È possibile incollare una sola volta. Per creare di nuovo una copia della stessa risorsa, copiala nuovamente.

### Modificare il contenuto di un nuovo modulo adattivo {#change-contents-of-new-adaptive-form}

Il contenuto di un modulo adattivo incollato può essere modificato utilizzando i seguenti approcci per renderlo diverso dal modulo copiato:

1. **Modifica proprietà metadati:**

   Puoi modificare le proprietà dei metadati del modulo adattivo, ad esempio titolo e descrizione. Per ulteriori dettagli sulle proprietà dei metadati e su come modificarle, consulta [Gestione dei metadati del modulo](/help/forms/using/manage-form-metadata.md)

1. **Modifica XFA/XSD per Forms adattivo basato su XFA/XSD:**

   Puoi modificare l’XFA/XSD utilizzato nei moduli adattivi. Per scoprire come è possibile modificare questi moduli adattivi, consulta [Gestione dei metadati del modulo](/help/forms/using/manage-form-metadata.md)

1. **Ripubblica:**

   La risorsa incollata è diversa da quella copiata. Puoi pubblicarla come nuova risorsa per renderla disponibile agli utenti finali. Per informazioni su come pubblicare una risorsa, consulta [Pubblicazione e annullamento della pubblicazione dei moduli](/help/forms/using/publishing-unpublishing-forms.md)
