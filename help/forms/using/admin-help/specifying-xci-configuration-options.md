---
title: Specifica delle opzioni di configurazione XCI
description: Scopri come specificare le opzioni di configurazione XCI. Puoi specificare i valori di un file XCI personalizzato per Modulo adattivo, in modo che possa essere utilizzato durante il rendering del modulo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# Specifica delle opzioni di configurazione XCI {#specifying-xci-configuration-options}

Forms consente di specificare un file XCI personalizzato da utilizzare per il rendering. (Vedi [Configurazione delle posizioni per Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Per impostazione predefinita, Forms ignora alcune delle opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puoi selezionare le opzioni che annullano l’override per le opzioni elencate qui sopra, nel qual caso Forms utilizza i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fare clic su **Servizi** > **Forms**.
1. Selezionare o deselezionare la casella di controllo Usa opzioni XCI predefinite di sistema. Quando questa opzione è selezionata, Forms utilizza i valori predefiniti per le impostazioni packets, creator, producer e compressObjectStream. Quando questa opzione è deselezionata, Forms utilizza i valori specificati nel file XCI personalizzato.
1. Fai clic su **Salva**.
