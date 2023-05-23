---
title: Utilizzo delle valutazioni
seo-title: Using Ratings
description: Aggiunta di un componente Valutazione a una pagina
seo-description: Adding a Rating component to a page
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# Utilizzo delle valutazioni {#using-ratings}

Il `Rating` Il componente viene utilizzato da solo o insieme ad altre funzioni di Communities. Questo componente consente ai membri della community con accesso esterno di esprimere le proprie opinioni attraverso la valutazione del contenuto.

## Aggiunta di una valutazione a una pagina {#adding-a-rating-to-a-page}

Per aggiungere una `Rating` a una pagina in modalità di authoring, individua il componente `Communities / Rating` e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla caratteristica da assegnare ai membri.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](rating-basics.md#essentials-for-client-side) sono inclusi, è così che `Rating` verrà visualizzato.

![valutazione](assets/rating.png)

## Configurazione della valutazione {#configuring-rating}

Seleziona la inserita `Rating` per accedere e selezionare il `Configure` che apre la finestra di dialogo per modifica.

![configure-new](assets/configure-new.png)

Sotto **[!UICONTROL Testi ed etichette]** specifica l’identificatore interno per la valutazione.

![tallyname](assets/tallyname.png)

**[!UICONTROL Nome conteggio]**
(*Obbligatorio* a) Un nome semplice per il `Rating` che identifica in modo univoco questa istanza. Deve essere un nome di nodo valido per l’archivio.

## Esperienza visitatore del sito {#site-visitor-experience}

### Membri {#members}

È consentita una sola valutazione per membro. L&#39;iscritto può cambiare la propria valutazione in qualsiasi momento.

### Anonimo {#anonymous}

La pubblicazione anonima di una valutazione non è supportata. I visitatori del sito devono registrarsi (diventare membri) e accedere per partecipare.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sulla valutazione](rating-basics.md) pagina per sviluppatori.
