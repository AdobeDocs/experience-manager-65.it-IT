---
title: Configurazione dei messaggi di convalida
seo-title: Configurazione dei messaggi di convalida
description: Scoprite come specificare la modalità di visualizzazione dei messaggi di convalida e la relativa posizione rispetto al modulo restituito nel browser Web.
seo-description: Scoprite come specificare la modalità di visualizzazione dei messaggi di convalida e la relativa posizione rispetto al modulo restituito nel browser Web.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---


# Configurazione dei messaggi di convalida {#configuring-validation-messages}

Per i moduli di cui viene eseguito il rendering in formato HTML, gli errori di convalida del modulo che si verificano vengono visualizzati dall&#39;utente. È possibile personalizzare la modalità di visualizzazione dei messaggi di convalida. A seconda di dove vengono visualizzati i messaggi di convalida, è inoltre possibile controllare la posizione del messaggio nel modulo e le dimensioni del bordo della cornice.

## Specificare la modalità di visualizzazione dei messaggi di convalida {#specify-how-validation-messages-are-displayed}

1. Nella console di amministrazione, fare clic su Servizi > moduli.
1. In Output convalida, nell&#39;elenco Rapporti, selezionare una delle opzioni seguenti:

   **Messaggio:** Per visualizzare i messaggi di convalida in una finestra di dialogo separata.

   **Frame:** Per visualizzare i messaggi di convalida all&#39;interno di un frame della stessa finestra.

   **Nessun fotogramma:** Per visualizzare i messaggi di convalida nella stessa finestra. Questo è il valore predefinito.

   **Tramite API (con i dati):** per restituire i messaggi di convalida tramite l&#39;API (con i dati). I messaggi di convalida non vengono visualizzati sullo schermo.

   **Tramite API (con modulo):** per restituire i messaggi di convalida tramite l&#39;API (con il modulo). I messaggi di convalida non vengono visualizzati sullo schermo.

   **Nessuno:** Per non visualizzare i messaggi di convalida.

1. Fate clic su Salva.

## Specificare il percorso dei messaggi di convalida relativi al modulo restituito nel browser Web {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

Se Reporting (Generazione rapporti) è impostato su Frame o No Frame, è possibile specificare la posizione dei messaggi di convalida.

1. In Output convalida, nell&#39;elenco Posizione, selezionare una delle opzioni seguenti:

   **Sinistra:** per visualizzare i messaggi di convalida sul lato sinistro del browser Web.

   **Destra:** Per visualizzare i messaggi di convalida sul lato destro del browser Web.

   **In alto**: Per visualizzare i messaggi di convalida nella parte superiore del browser Web. Questo è il valore predefinito.

   **In basso**: Per visualizzare i messaggi di convalida nella parte inferiore del browser Web.

1. Fate clic su Salva.

## Specificare la dimensione del bordo del fotogramma {#specify-the-frame-border-size}

Quando Reporting (Generazione rapporti) è impostato su Frame, potete specificare la dimensione del bordo della cornice.

1. In Output convalida, nella casella Dimensione bordo, digitare la dimensione del bordo della cornice, in pixel.

   La dimensione del bordo deve essere uguale o maggiore di 0. Il valore predefinito è 1.

1. Fate clic su Salva.

