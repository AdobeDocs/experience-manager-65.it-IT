---
title: Impostazione delle opzioni di internazionalizzazione
seo-title: Setting internationalization options
description: Scopri come specificare le impostazioni internazionali utilizzate per il rendering dei moduli e come specificare il set di caratteri utilizzato per codificare il flusso di output.
seo-description: Learn how to specify the locale used to render forms and how to specify the character set used to encode the output stream.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 1%

---

# Impostazione delle opzioni di internazionalizzazione{#setting-internationalization-options}

## Specificare le impostazioni internazionali utilizzate per il rendering dei moduli {#specify-the-locale-used-to-render-forms}

È possibile specificare le impostazioni internazionali utilizzate per il rendering di un modulo PDF. I campi di un modulo PDF utilizzano le impostazioni internazionali specificate per visualizzare i dati. Ad esempio, se le impostazioni internazionali sono impostate su Tedesco, per i valori numerici il modulo utilizza separatori decimali tedeschi. Le impostazioni internazionali vengono inoltre utilizzate per inviare messaggi di convalida ai dispositivi client, come i browser web, come parte delle trasformazioni di HTML.

1. Nella console di amministrazione, fai clic su Servizi > Forms.
1. In Internazionalizzazione, nell’elenco Lingua, selezionare le impostazioni internazionali utilizzate per eseguire il rendering di un modulo. Il valore predefinito è Inglese (Stati Uniti).
1. Fai clic su Salva.

## Specifica il set di caratteri utilizzato per codificare il flusso di output {#specify-the-character-set-used-to-encode-the-output-stream}

1. In Internazionalizzazione, selezionare un set di caratteri dall’elenco Set di caratteri. Questa impostazione dipende dall’API utilizzata, renderHTMLForm o renderPDFForm. Per specificare un set di caratteri diverso da quelli elencati, selezionare Personalizzato e specificare un valore di codifica nella casella visualizzata.

   Per le trasformazioni di HTML, i moduli AEM supportano i valori di codifica dei caratteri definiti dal `java.nio.charset` pacchetto. Se sFormPreference è PDFForm, sono supportati solo set di caratteri specifici. Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su Salva.
