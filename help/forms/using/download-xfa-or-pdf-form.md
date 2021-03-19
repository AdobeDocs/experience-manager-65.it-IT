---
title: Scaricare un modello di modulo XFA o PDF
seo-title: Scaricare un modello di modulo XFA o PDF
description: È possibile esportare i moduli dall’archivio al sistema locale ed eseguire la migrazione dei moduli scaricati nel nuovo archivio.
seo-description: È possibile esportare i moduli dall’archivio al sistema locale ed eseguire la migrazione dei moduli scaricati nel nuovo archivio.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# Scaricare un XFA o un modello di modulo PDF {#download-an-xfa-or-a-pdf-form-template}

L’operazione di download, come suggerisce il nome, consente di esportare i moduli dall’archivio al sistema locale. In combinazione con l’operazione di caricamento, questa operazione consente di migrare i moduli da un archivio all’altro.

In AEM Forms, l’operazione di download è supportata per i seguenti tipi di risorse:

* Modelli di modulo (XFA Forms)
* PDF forms
* Documenti (file PDF semplici)

AEM Forms supporta il download di questi tipi di moduli singolarmente o in una cartella contenente uno o più moduli supportati.

Oltre a queste risorse, puoi scaricare il tipo di risorsa `Resource` se presente in una cartella. Questa funzionalità consente di scaricare insieme al modulo la risorsa a cui fa riferimento un modulo XFA.

## Scaricare uno o più moduli {#download-one-or-more-forms}

1. Accedi all&#39;interfaccia utente di AEM Forms all&#39;indirizzo `https://<server>:<port>/aem/forms.html`.

1. Andate alla posizione della risorsa da scaricare.

1. Seleziona la risorsa. Fai clic sull&#39;icona **[!UICONTROL Scarica]** ![aem6forms_download](assets/aem6forms_download.png) nella barra degli strumenti.

   >[!NOTE]
   >
   >È possibile selezionare un solo modulo da scaricare. Se si desidera scaricare più moduli, è necessario scaricarli come cartella.

1. Nella finestra di dialogo visualizzata, fai clic su **[!UICONTROL Scarica]**.

   AEM Forms genera un file ZIP contenente il file selezionato o la cartella selezionata.

   Se scarichi una cartella, le risorse supportate all’interno della cartella vengono scaricate nella gerarchia esistente.

   Il file ZIP viene salvato nella cartella `Downloads` del sistema.

## Considerazioni correlate all’operazione di caricamento {#related-considerations-for-the-upload-operation}

* Puoi caricare il file ZIP in qualsiasi altra posizione nello stesso archivio o in un altro archivio
* La gerarchia delle risorse in una cartella viene mantenuta durante l’operazione di caricamento
* Tutte le modifiche ai metadati apportate alle risorse scaricate prima del download vengono applicate al momento del caricamento

