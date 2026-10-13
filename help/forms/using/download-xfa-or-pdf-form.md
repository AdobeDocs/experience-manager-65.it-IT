---
title: Scaricare un modello di modulo XFA o PDF
description: È possibile esportare i moduli dal repository al sistema locale e migrare i moduli scaricati nel nuovo repository.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: aa28c6c8-3ede-445b-a351-eeb0c9f9aec4
    internal-label: Interactive Communication
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 5%
---
# Scaricare un modello di modulo XFA o PDF {#download-an-xfa-or-a-pdf-form-template}

L&#39;operazione di download, come indica il nome, consente di esportare i moduli dal repository al sistema locale. In combinazione con l’operazione di caricamento, questa operazione consente di migrare i moduli da un archivio all’altro.

In AEM Forms, l’operazione di download è supportata per i seguenti tipi di risorse:

* Modelli di modulo (XFA Forms)
* PDF forms
* Documenti (file flat PDF)

AEM Forms supporta il download di questi tipi di moduli singolarmente o in una cartella contenente uno o più moduli supportati.

Oltre a queste risorse, puoi scaricare il tipo di risorsa `Resource` se è presente in una cartella. Questa funzionalità consente di scaricare la risorsa a cui fa riferimento un modulo XFA insieme al modulo.

## Scarica uno o più moduli {#download-one-or-more-forms}

1. Accedere all&#39;interfaccia utente di AEM Forms all&#39;indirizzo `https://<server>:<port>/aem/forms.html`.

1. Passa alla posizione della risorsa da scaricare.

1. Seleziona la risorsa. Fai clic sull&#39;icona **[!UICONTROL Scarica]** ![aem6forms_download](assets/aem6forms_download.png) nella barra degli strumenti.

   >[!NOTE]
   >
   >È possibile selezionare un solo modulo per il download. Se si desidera scaricare più moduli, è necessario scaricarli come cartella.

1. Nella finestra di dialogo visualizzata, fai clic su **[!UICONTROL Scarica]**.

   AEM Forms genera un file ZIP contenente il file selezionato o la cartella selezionata.

   Se stai scaricando una cartella, le risorse supportate all’interno della cartella vengono scaricate nella gerarchia esistente.

   Il file ZIP viene salvato nella cartella `Downloads` del sistema.

## Considerazioni correlate per l’operazione di caricamento {#related-considerations-for-the-upload-operation}

* Puoi caricare il file ZIP in qualsiasi altra posizione nello stesso archivio o in un altro archivio
* La gerarchia delle risorse in una cartella viene mantenuta durante l’operazione di caricamento
* Eventuali modifiche apportate ai metadati delle risorse scaricate prima del download vengono applicate al caricamento
