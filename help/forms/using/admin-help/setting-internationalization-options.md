---
title: Impostazione delle opzioni di internazionalizzazione
description: Scopri come specificare le impostazioni della lingua utilizzate per il rendering dei moduli e come specificare il set di caratteri utilizzato per codificare il flusso di output.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 100%
---
# Impostazione delle opzioni di internazionalizzazione{#setting-internationalization-options}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

## Specificare la lingua utilizzata per il rendering dei moduli {#specify-the-locale-used-to-render-forms}

Puoi specificare la lingua utilizzata per il rendering di un modulo di PDF. I campi di un modulo di PDF utilizzano la lingua specificata per la visualizzazione dei dati. Se, ad esempio, la lingua è confugurata sul tedesco, per i valori numerici verranno utilizzati i separatori decimali tedeschi. La lingua viene utilizzata anche per inviare messaggi di convalida ai dispositivi client, ad esempio i browser web, come parte delle trasformazioni HTML.

1. Nella console di amministrazione, fai clic su Servizi > Moduli.
1. Nell’elenco Lingua in Internazionalizzazione seleziona la lingua utilizzata per il rendering di un modulo. Il valore predefinito è Inglese (Stati Uniti).
1. Fai clic su Salva.

## Specificare il set di caratteri utilizzato per codificare il flusso di output {#specify-the-character-set-used-to-encode-the-output-stream}

1. Seleziona un set di caratteri sell’elenco Set di caratteri in Internazionalizzazione. Questa impostazione dipende dall’API utilizzata, renderHTMLForm o renderPDFForm. Per specificare un set di caratteri diverso da quelli elencati, seleziona Personalizzato e specifica un valore di codifica nella casella visualizzata.

   Per le trasformazioni HTML, AEM Forms supporta i valori di codifica dei caratteri definiti dal pacchetto `java.nio.charset`. Se sFormPreference è PDFForm, sono supportati solo set di caratteri specifici. Il set di caratteri deve essere un nome canonico valido. Il valore predefinito è ISO-8859-1.

1. Fai clic su Salva.
