---
title: Specificare le opzioni di configurazione XCI
description: Scopri come specificare le opzioni di configurazione XCI. Puoi specificare i valori di un file XCI personalizzato per il modulo adattivo, che verrà utilizzato per il rendering del modulo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '161'
ht-degree: 100%

---

# Specificare le opzioni di configurazione XCI {#specifying-xci-configuration-options}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I moduli ti consentono di specificare un file XCI personalizzato da utilizzare per il rendering. Consulta [Configurare i percorsi per i moduli](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms). Per impostazione predefinita, i moduli ignorano alcune opzioni specificate nel file XCI, tra cui le seguenti:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puoi selezionare opzioni che annullano la sostituzione delle opzioni elencate qui sopra, nel qual caso i moduli utilizzano i valori specificati nel file XCI personalizzato.

1. Nella console di amministrazione, fai clic su **Servizi** > **Moduli**.
1. Seleziona o deseleziona la casella di controllo Usa le opzioni XCI predefinite di sistema. Quando questa opzione è selezionata, i moduli utilizzano valori predefiniti per le impostazioni packets, creator, producer e compressObjectStream. Quando questa opzione è deselezionata, i moduli utilizzano i valori specificati nel file XCI personalizzato.
1. Fai clic su **Salva**.
