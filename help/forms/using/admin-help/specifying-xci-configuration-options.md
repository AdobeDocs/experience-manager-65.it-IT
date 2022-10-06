---
title: Specifica delle opzioni di configurazione XCI
seo-title: Specifying XCI configuration options
description: Scopri come specificare le opzioni di configurazione XCI.
seo-description: Learn how to specify XCI configuration options.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# Specifica delle opzioni di configurazione XCI {#specifying-xci-configuration-options}

Forms consente di specificare un file XCI personalizzato che verrà utilizzato per il rendering. (Vedi [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Per impostazione predefinita, Forms sostituisce alcune delle opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

È possibile selezionare le opzioni che annullano l’override per le opzioni elencate sopra, nel qual caso Forms utilizzerà i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. Selezionare o deselezionare la casella di controllo Usa opzioni XCI predefinite del sistema. Quando questa opzione è selezionata, Forms utilizza i valori predefiniti per le impostazioni pacchetti, creatore, produttore e compressObjectStream. Quando questa opzione è deselezionata, Forms utilizza i valori specificati nel file XCI personalizzato.
1. Fai clic su Salva.
