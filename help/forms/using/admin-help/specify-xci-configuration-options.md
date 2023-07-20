---
title: Specificare le opzioni di configurazione XCI
description: Scopri come specificare le opzioni di configurazione XCI.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# Specificare le opzioni di configurazione XCI {#specify-xci-configuration-options}

L’output consente di specificare un file XCI personalizzato da utilizzare per il rendering. Consulta [Specificare i percorsi dei file per l&#39;output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

Per impostazione predefinita, Output sostituisce alcune delle opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puoi selezionare le opzioni che annullano l’override per le opzioni elencate qui sopra, nel qual caso Output utilizza i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fai clic su **Servizi** > output.
1. Selezionare o deselezionare la casella di controllo Usa opzioni XCI predefinite di sistema. Quando questa opzione è selezionata, l&#39;output utilizza i valori predefiniti per le impostazioni packets, creator, producer e compressObjectStream. Quando questa opzione è deselezionata, l’output utilizza i valori specificati nel file XCI personalizzato.
1. Fai clic su **Salva**.
