---
title: Configurazione dell’output del modulo
description: Scopri come configurare l’output del modulo. Per configurare l’output del modulo e abilitare questa funzione, utilizza gli script personalizzati prima dell’invio del modulo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '256'
ht-degree: 100%

---

# Configurazione dell’output del modulo{#configuring-form-output}

## Specificare il tipo di output HTML restituito al browser web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. Nella console di amministrazione, fai clic su Servizi > Moduli.
1. Nell’elenco Tipo di output, in Output del modulo, seleziona una delle opzioni seguenti:

   **HTML completo:** per eseguire il rendering del modulo in tag HTML completi (pagina HTML completa). Questo valore è predefinito.

   **Corpo del modulo:** per eseguire il rendering del modulo in tag `<BODY>` (non una pagina HTML completa).

1. Fai clic su Salva.

## Specificare la posizione in cui viene eseguito il rendering del contenuto PDF {#specify-the-location-where-pdf-content-is-rendered}

1. In Output del modulo, nell’elenco Rendering in, seleziona una delle seguenti opzioni:

   **Client:** per eseguire il rendering di moduli PDF in Adobe Acrobat o Adobe Reader. Il rendering lato client migliora le prestazioni dei moduli AEM e si applica solo alla trasformazione dei moduli PDF.

   **Server:** per eseguire il rendering di moduli PDF nel server applicazioni.

   **Auto:** per eseguire il rendering del modulo PDF nella posizione specificata dal valore di configurazione `dynamicRender` del file XDP. Questo valore è predefinito.

1. Fai clic su Salva.

## Configurazione della chiamata di script personalizzati prima dell’invio del modulo {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Per abilitare questa funzione, esegui i passaggi seguenti:

1. Accedi alla console di amministrazione.
1. Passa a **Servizi** > **moduli**.
1. Specifica il tipo di output come corpo del modulo.
1. Salva le impostazioni.
1. Dichiara una variabile JavaScript, __CUSTOM_SCRIPTS_VERSION, nella sezione head del codice HTML e impostane il valore su 1.

   >[!NOTE]
   >
   >*Per disabilitare questa funzione, puoi rimuovere la variabile JavaScript o impostarne il valore su 0.*
