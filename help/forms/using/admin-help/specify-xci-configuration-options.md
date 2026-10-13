---
title: Specificare le opzioni di configurazione XCI
description: Scopri come specificare le opzioni di configurazione XCI. Puoi specificare i valori di un file XCI personalizzato per il modulo adattivo, che verrà utilizzato per il rendering del modulo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 100%
---
# Specificare le opzioni di configurazione XCI {#specify-xci-configuration-options}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

L’output consente di specificare un file XCI personalizzato da utilizzare per il rendering. Consulta [Specificare i percorsi dei file per l’output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

Per impostazione predefinita, Output sostituisce alcune delle opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puoi selezionare le opzioni che annullano la sostituzione con le opzioni elencate qui sopra, nel qual caso Output utilizzerà i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fai clic su **Servizi** > Output.
1. Seleziona o deseleziona la casella di controllo Usa le opzioni XCI predefinite di sistema. Quando questa opzione è selezionata, Output utilizza i valori predefiniti per le impostazioni Pacchetti, Creatore, Produttore e compressObjectStream. Quando questa opzione è deselezionata, Output utilizza i valori specificati nel file XCI personalizzato.
1. Fai clic su **Salva**.
