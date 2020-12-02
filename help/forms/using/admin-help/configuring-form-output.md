---
title: Configurazione dell'output del modulo
seo-title: Configurazione dell'output del modulo
description: Scoprite come configurare l'output del modulo.
seo-description: Scoprite come configurare l'output del modulo.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# Configurazione dell&#39;output del modulo{#configuring-form-output}

## Specificare il tipo di output HTML restituito al browser Web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Nella console di amministrazione, fare clic su Servizi > moduli.
1. In Output modulo, nell&#39;elenco Tipo di output, selezionare una delle opzioni seguenti:

   **HTML completo:** per eseguire il rendering del modulo all&#39;interno di tag HTML completi (una pagina HTML completa). Questo è il valore predefinito.

   **corpo del modulo:** Per eseguire il rendering del modulo all&#39;interno di  `<BODY>` tag (non una pagina HTML completa).

1. Fate clic su Salva.

## Specificare il percorso in cui viene eseguito il rendering del contenuto PDF {#specify-the-location-where-pdf-content-is-rendered}

1. In Output modulo, nell&#39;elenco Rendering in, selezionare una delle opzioni seguenti:

   **Client:** Per eseguire il rendering dei PDF forms all&#39;interno  Adobe Acrobat o  Adobe Reader. Il rendering sul lato client migliora le prestazioni dei moduli AEM e si applica solo alla trasformazione PDFForm.

   **Server:** per eseguire il rendering dei PDF forms sul server dell&#39;applicazione.

   **Automatico:** Per eseguire il rendering del modulo PDF nella posizione specificata dal valore di  `dynamicRender` configurazione del file XDP. Questo è il valore predefinito.

1. Fate clic su Salva.

## Configurazione della chiamata di script personalizzati prima dell&#39;invio del modulo {#configuring-invocation-of-custom-scripts-before-form-submit}

Per attivare la funzione, effettuate le seguenti operazioni:

1. Accedete alla console di amministrazione.
1. Accedere a **Services** > **forms**.
1. Specificare il tipo di output come corpo del modulo.
1. Salvate le impostazioni.
1. Dichiarate una variabile JavaScript, __CUSTOM_SCRIPTS_VERSION, nella sezione head del codice HTML e impostatene il valore su 1.

   >[!NOTE]
   >
   >*Per disattivare la funzione, è possibile rimuovere la variabile JavaScript o impostarne il valore su 0.*

