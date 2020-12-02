---
title: Impostazione delle opzioni di internazionalizzazione
seo-title: Impostazione delle opzioni di internazionalizzazione
description: Come specificare le impostazioni internazionali utilizzate per il rendering dei moduli e come specificare il set di caratteri utilizzato per codificare il flusso di output.
seo-description: Come specificare le impostazioni internazionali utilizzate per il rendering dei moduli e come specificare il set di caratteri utilizzato per codificare il flusso di output.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# Impostazione delle opzioni di internazionalizzazione{#setting-internationalization-options}

## Specificare le impostazioni internazionali utilizzate per il rendering dei moduli {#specify-the-locale-used-to-render-forms}

È possibile specificare le impostazioni internazionali utilizzate per il rendering di un modulo PDF. I campi di un modulo PDF utilizzano le impostazioni internazionali specificate per visualizzare i dati. Ad esempio, se le impostazioni internazionali sono impostate su Tedesco, per i valori numerici il modulo utilizza i separatori decimali tedeschi. Le impostazioni internazionali vengono inoltre utilizzate per inviare messaggi di convalida ai dispositivi client, come i browser Web, nell&#39;ambito delle trasformazioni HTML.

1. Nella console di amministrazione, fate clic su Servizi > Forms.
1. In Internazionalizzazione, nell&#39;elenco Lingua, selezionare le impostazioni internazionali utilizzate per eseguire il rendering di un modulo. Il valore predefinito è Inglese (Stati Uniti).
1. Fate clic su Salva.

## Specificare il set di caratteri utilizzato per codificare il flusso di output {#specify-the-character-set-used-to-encode-the-output-stream}

1. In Internazionalizzazione, nell&#39;elenco Set di caratteri, selezionare un set di caratteri. Questa impostazione dipende dall’API utilizzata, ossia renderingHTMLForm o renderingPDFForm. Per specificare un set di caratteri diverso da quelli elencati, selezionare Personalizzato e specificare un valore di codifica nella casella visualizzata.

   Per le trasformazioni HTML, i moduli AEM supportano i valori di codifica dei caratteri definiti dal pacchetto `java.nio.charset`. Se sFormPreference è PDFForm, sono supportati solo set di caratteri specifici. Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fate clic su Salva.

