---
title: Configurazione dell’output del modulo
seo-title: Configuring form output
description: Scopri come configurare l’output del modulo.
seo-description: Learn how to configure form output.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---

# Configurazione dell’output del modulo{#configuring-form-output}

## Specificare il tipo di output HTML restituito al browser Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Nella console di amministrazione, fai clic su Servizi > Moduli.
1. Nell’elenco Tipo di output della casella di gruppo Output modulo selezionare una delle opzioni seguenti:

   **HTML completo:** Per eseguire il rendering del modulo all’interno di tag HTML completi (una pagina HTML completa). Questo è il valore predefinito.

   **Corpo del modulo:** Per eseguire il rendering del modulo all’interno di `<BODY>` tag (non una pagina HTML completa).

1. Fai clic su Salva.

## Specificare la posizione in cui viene eseguito il rendering del contenuto PDF {#specify-the-location-where-pdf-content-is-rendered}

1. Nell’elenco Rendering a, in Output modulo, selezionare una delle opzioni seguenti:

   **Client:** Per eseguire il rendering di PDF forms all’interno di Adobe Acrobat o Adobe Reader. Il rendering lato client migliora le prestazioni dei moduli AEM e si applica solo alla trasformazione PDFForm.

   **Server:** Per eseguire il rendering dei PDF forms sul server applicazioni.

   **Automatico:** Per eseguire il rendering del modulo PDF nella posizione specificata dal `dynamicRender` valore di configurazione del file XDP. Questo è il valore predefinito.

1. Fai clic su Salva.

## Configurazione della chiamata degli script personalizzati prima dell’invio del modulo {#configuring-invocation-of-custom-scripts-before-form-submit}

Esegui i seguenti passaggi per abilitare la funzione:

1. Accedi alla console di amministrazione.
1. Vai a **Servizi** > **forms**.
1. Specificare il tipo di output come corpo del modulo.
1. Salva le impostazioni.
1. Dichiarare una variabile JavaScript, __CUSTOM_SCRIPTS_VERSION, nella sezione head del codice HTML e impostarne il valore su 1.

   >[!NOTE]
   >
   >*Per disattivare la funzione, è possibile rimuovere la variabile JavaScript o impostarne il valore su 0.*
