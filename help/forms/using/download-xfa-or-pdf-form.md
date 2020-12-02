---
title: Download di un modello di modulo XFA o PDF
seo-title: Download di un modello di modulo XFA o PDF
description: È possibile esportare i moduli dall'archivio nel sistema locale ed eseguire la migrazione dei moduli scaricati in un nuovo archivio.
seo-description: È possibile esportare i moduli dall'archivio nel sistema locale ed eseguire la migrazione dei moduli scaricati in un nuovo archivio.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Download di un modello di modulo XFA o PDF {#download-an-xfa-or-a-pdf-form-template}

L&#39;operazione di download, come suggerisce il nome, consente di esportare i moduli dall&#39;archivio nel sistema locale. In combinazione con l&#39;operazione di caricamento, questa operazione consente di migrare i moduli da un archivio all&#39;altro.

In  AEM Forms, l’operazione di download è supportata per i seguenti tipi di risorse:

* Modelli di modulo (XFA Forms)
* PDF forms
* Documenti (file PDF semplici)

 AEM Forms supporta il download di questi tipi di moduli singolarmente o in una cartella contenente uno o più moduli supportati.

A parte queste risorse, potete scaricare il tipo di risorsa `Resource` se presente in una cartella. Questa funzionalità consente di scaricare la risorsa a cui fa riferimento un modulo XFA insieme al modulo.

## Download di uno o più moduli {#download-one-or-more-forms}

1. Accedete all&#39;interfaccia utente  AEM Forms all&#39;indirizzo `https://<server>:<port>/aem/forms.html`.

1. Andate alla posizione della risorsa da scaricare.

1. Selezionate la risorsa. Fare clic sull&#39;icona **[!UICONTROL Download]** ![aem6forms_download](assets/aem6forms_download.png) nella barra degli strumenti.

   >[!NOTE]
   >
   >È possibile selezionare un solo modulo da scaricare. Se si desidera scaricare più moduli, è necessario scaricarli come cartella.

1. Nella finestra di dialogo visualizzata, fate clic su **[!UICONTROL Scarica]**.

    AEM Forms genera un file ZIP contenente il file selezionato o la cartella selezionata.

   Se scaricate una cartella, le risorse supportate all’interno della cartella vengono scaricate nella gerarchia esistente.

   Il file ZIP viene salvato nella cartella `Downloads` del sistema.

## Considerazioni correlate all&#39;operazione di caricamento {#related-considerations-for-the-upload-operation}

* Potete caricare il file ZIP in qualsiasi altra posizione nello stesso repository o in un altro repository
* La gerarchia delle risorse in una cartella viene mantenuta durante l’operazione di caricamento
* Eventuali modifiche ai metadati apportate alle risorse scaricate prima del download vengono riportate al momento del caricamento

