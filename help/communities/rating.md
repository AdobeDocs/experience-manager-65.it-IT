---
title: Utilizzo delle valutazioni
seo-title: Utilizzo delle valutazioni
description: Aggiunta di un componente Valutazione a una pagina
seo-description: Aggiunta di un componente Valutazione a una pagina
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 0051791da06d15a48b82cf93164a89b4ea42ce98
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---


# Utilizzo delle valutazioni {#using-ratings}

Il componente `Rating` viene utilizzato autonomamente o insieme ad altre funzioni di Communities. Questo componente permette ai membri della community che hanno effettuato l’accesso di esprimere le proprie opinioni in base al punteggio contenuto.

## Aggiunta di una valutazione a una pagina {#adding-a-rating-to-a-page}

Per aggiungere un componente `Rating` a una pagina in modalità di creazione, individuate il componente `Communities / Rating` e trascinatelo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione per i membri da classificare.

Per le informazioni necessarie, visitare [Community Components Basics](basics.md).

Quando vengono incluse le [librerie lato client ](rating-basics.md#essentials-for-client-side), viene visualizzato il componente `Rating`.

![valutazione](assets/rating.png)

## Configurazione della classificazione {#configuring-rating}

Selezionare il componente `Rating` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

Nella scheda **[!UICONTROL Testi e etichette]** è possibile specificare l&#39;identificatore interno per la valutazione.

![tallyname](assets/tallyname.png)

**[!UICONTROL Tally Name]**
(*Obbligatorio*) Un nome semplice per il  `Rating` quale identifica l&#39;istanza in modo univoco. Deve essere un nome di nodo valido per il repository.

## Esperienza visitatori del sito {#site-visitor-experience}

### Membri {#members}

È consentita una sola valutazione per membro. Il membro può cambiare la propria valutazione in qualsiasi momento.

### Anonimo {#anonymous}

L&#39;invio anonimo di una valutazione non è supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l’accesso per partecipare.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Classificazione di Essentials](rating-basics.md) per gli sviluppatori.
