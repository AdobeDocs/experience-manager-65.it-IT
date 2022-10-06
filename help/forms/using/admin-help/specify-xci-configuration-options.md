---
title: Specificare le opzioni di configurazione XCI
seo-title: Specify XCI configuration options
description: Scopri come specificare le opzioni di configurazione XCI.
seo-description: Learn how to specify XCI configuration options.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%

---

# Specificare le opzioni di configurazione XCI {#specify-xci-configuration-options}

L&#39;output consente di specificare un file XCI personalizzato utilizzato per il rendering. (Vedi [Specificare le posizioni dei file per l&#39;output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) Per impostazione predefinita, Output sostituisce alcune delle opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

È possibile selezionare le opzioni che annullano l&#39;override per le opzioni elencate sopra, nel qual caso Output utilizza i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fai clic su Servizi > output.
1. Selezionare o deselezionare la casella di controllo Usa opzioni XCI predefinite del sistema. Quando questa opzione è selezionata, Output utilizza i valori predefiniti per le impostazioni dei pacchetti, creatore, produttore e compressObjectStream. Quando questa opzione è deselezionata, Output utilizza i valori specificati nel file XCI personalizzato.
1. Fai clic su Salva.
