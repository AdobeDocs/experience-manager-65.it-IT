---
title: Specifica delle opzioni di configurazione XCI
seo-title: Specifica delle opzioni di configurazione XCI
description: Scoprite come specificare le opzioni di configurazione XCI.
seo-description: Scoprite come specificare le opzioni di configurazione XCI.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Specifica delle opzioni di configurazione XCI {#specifying-xci-configuration-options}

Forms consente di specificare un file XCI personalizzato da utilizzare per il rendering. (Vedere [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Per impostazione predefinita, Forms sostituisce alcune delle opzioni specificate nel file XCI, tra cui:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

È possibile selezionare opzioni che annullano l&#39;override delle opzioni elencate sopra. In tal caso Forms utilizzerà i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fare clic su Servizi > Moduli.
1. Selezionare o deselezionare la casella di controllo Usa opzioni XCI predefinite del sistema. Quando questa opzione è selezionata, Forms utilizza i valori predefiniti per le impostazioni di pacchetti, creatore, produttore e compressObjectStream. Quando questa opzione è deselezionata, Forms utilizza i valori specificati nel file XCI personalizzato.
1. Fate clic su Salva.

