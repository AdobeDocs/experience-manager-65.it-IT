---
title: Specificare le opzioni di configurazione XCI
description: Scopri come specificare le opzioni di configurazione XCI. Puoi specificare i valori di un file XCI personalizzato per Modulo adattivo, in modo che possa essere utilizzato durante il rendering del modulo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---

# Specificare le opzioni di configurazione XCI {#specify-xci-configuration-options}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

L’output consente di specificare un file XCI personalizzato da utilizzare per il rendering. Vedere [Specificare i percorsi dei file per l&#39;output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

Per impostazione predefinita, Output sostituisce alcune delle opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puoi selezionare le opzioni che annullano l’override per le opzioni elencate qui sopra, nel qual caso Output utilizza i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fare clic su **Servizi** > output.
1. Selezionare o deselezionare la casella di controllo Usa opzioni XCI predefinite di sistema. Quando questa opzione è selezionata, l&#39;output utilizza i valori predefiniti per le impostazioni packets, creator, producer e compressObjectStream. Quando questa opzione è deselezionata, l’output utilizza i valori specificati nel file XCI personalizzato.
1. Fai clic su **Salva**.
