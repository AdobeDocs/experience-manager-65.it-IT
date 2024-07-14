---
title: Impostazione delle opzioni di internazionalizzazione
description: Scopri come specificare le impostazioni locali utilizzate per il rendering dei moduli e come specificare il set di caratteri utilizzato per codificare il flusso di output.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---

# Impostazione delle opzioni di internazionalizzazione{#setting-internationalization-options}

## Specificare le impostazioni locali utilizzate per il rendering dei moduli {#specify-the-locale-used-to-render-forms}

È possibile specificare le impostazioni locali utilizzate per il rendering di un modulo PDF. I campi di un modulo PDF utilizzano le impostazioni locali specificate per la visualizzazione dei dati. Se ad esempio la lingua è impostata sul tedesco, per i valori numerici verranno utilizzati i separatori decimali tedeschi. La lingua viene utilizzata anche per inviare messaggi di convalida ai dispositivi client, come i browser web, come parte delle trasformazioni di HTML.

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Internazionalizzazione selezionare le impostazioni locali utilizzate per il rendering di un modulo nell&#39;elenco Lingua. Il valore predefinito è Inglese (Stati Uniti).
1. Fai clic su Salva.

## Specifica il set di caratteri utilizzato per codificare il flusso di output {#specify-the-character-set-used-to-encode-the-output-stream}

1. In Internazionalizzazione selezionare un set di caratteri nell&#39;elenco Set di caratteri. Questa impostazione dipende dall’API utilizzata, renderHTMLForm o renderPDFForm. Per specificare un set di caratteri diverso da quelli elencati, selezionare Personalizzato e specificare un valore di codifica nella casella visualizzata.

   Per le trasformazioni HTML, i moduli AEM supportano i valori di codifica dei caratteri definiti dal pacchetto `java.nio.charset`. Se sFormPreference è PDFForm, sono supportati solo set di caratteri specifici. Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su Salva.
