---
title: Configurazione dei messaggi di convalida
seo-title: Configuring validation messages
description: Scopri come specificare la modalità di visualizzazione dei messaggi di convalida e la relativa posizione rispetto al modulo restituito nel browser Web.
seo-description: Learn how to specify how validation messages are displayed and their location relative to the form returned in the web browser.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 2%

---

# Configurazione dei messaggi di convalida {#configuring-validation-messages}

Per i moduli sottoposti a rendering come HTML, l’utente visualizza gli errori di convalida dei moduli. È possibile personalizzare la visualizzazione dei messaggi di convalida. A seconda della posizione di visualizzazione dei messaggi di convalida, è inoltre possibile controllare la posizione del messaggio nel modulo e le dimensioni del bordo del frame.

## Specificare la modalità di visualizzazione dei messaggi di convalida {#specify-how-validation-messages-are-displayed}

1. Nella console di amministrazione, fai clic su Servizi > Moduli.
1. In Output convalida, nell&#39;elenco Reporting selezionare una delle opzioni seguenti:

   **Messaggio:** Visualizzazione dei messaggi di convalida in una finestra di dialogo separata

   **Frame:** Visualizzazione dei messaggi di convalida all&#39;interno di un frame della stessa finestra.

   **Nessun frame:** Visualizzazione dei messaggi di convalida nella stessa finestra. Questo è il valore predefinito.

   **Tramite API (con dati):** Per restituire i messaggi di convalida tramite l’API (con dati). I messaggi di convalida non vengono visualizzati sullo schermo.

   **Tramite API (con modulo):** Per restituire i messaggi di convalida tramite l’API (con il modulo). I messaggi di convalida non vengono visualizzati sullo schermo.

   **Nessuno:** Per non visualizzare i messaggi di convalida.

1. Fai clic su Salva.

## Specificare il percorso dei messaggi di convalida rispetto al modulo restituito nel browser Web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Quando Reporting è impostato su Frame o No Frame, è possibile specificare la posizione dei messaggi di convalida.

1. In Output convalida, nell&#39;elenco Posizione, selezionare una delle opzioni seguenti:

   **Sinistra:** Visualizzazione dei messaggi di convalida sul lato sinistro del browser Web

   **A destra:** Visualizzazione dei messaggi di convalida sul lato destro del browser Web

   **Top**: Visualizzazione dei messaggi di convalida nella parte superiore del browser Web Questo è il valore predefinito.

   **In basso**: Visualizzazione dei messaggi di convalida nella parte inferiore del browser Web

1. Fai clic su Salva.

## Specifica la dimensione del bordo del frame {#specify-the-frame-border-size}

Quando Reporting è impostato su Frame, è possibile specificare la dimensione del bordo del frame.

1. Nella casella Dimensione bordo della casella Output convalida digitare in pixel la dimensione del bordo del fotogramma.

   La dimensione del bordo deve essere uguale o maggiore di 0. Il valore predefinito è 1.

1. Fai clic su Salva.
