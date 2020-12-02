---
title: Specificare le opzioni di configurazione XCI
seo-title: Specificare le opzioni di configurazione XCI
description: Scoprite come specificare le opzioni di configurazione XCI.
seo-description: Scoprite come specificare le opzioni di configurazione XCI.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 1%

---


# Specificare le opzioni di configurazione XCI {#specify-xci-configuration-options}

Output consente di specificare un file XCI personalizzato utilizzato per il rendering. (Vedere [Specificare i percorsi dei file per Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) Per impostazione predefinita, Output sostituisce alcune delle opzioni specificate nel file XCI, tra cui:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

È possibile selezionare opzioni che annullano l&#39;override per le opzioni elencate sopra, nel qual caso Output utilizza i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fate clic su Servizi > output.
1. Selezionare o deselezionare la casella di controllo Usa opzioni XCI predefinite del sistema. Quando questa opzione è selezionata, Output utilizza i valori predefiniti per le impostazioni pacchetti, creatore, produttore e compressObjectStream. Quando questa opzione è deselezionata, Output utilizza i valori specificati nel file XCI personalizzato.
1. Fate clic su Salva.

