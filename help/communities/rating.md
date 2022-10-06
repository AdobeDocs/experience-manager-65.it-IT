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

La `Rating` viene utilizzato separatamente o insieme ad altre funzioni di Communities. Questo componente permette ai membri della community che hanno effettuato l’accesso di esprimere le proprie opinioni in base al contenuto del punteggio.

## Aggiunta di una valutazione a una pagina {#adding-a-rating-to-a-page}

Per aggiungere una `Rating` in una pagina in modalità di authoring, individua il componente `Communities / Rating` e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione per la valutazione dei membri.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](rating-basics.md#essentials-for-client-side) sono inclusi, è così che `Rating` apparirà .

![valutazione](assets/rating.png)

## Configurazione della valutazione {#configuring-rating}

Seleziona il `Rating` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

Sotto la **[!UICONTROL Testi ed etichette]** Specifica l’identificatore interno per la valutazione.

![nome](assets/tallyname.png)

**[!UICONTROL Nome dell’alleanza]**
(*Obbligatorio*) Un nome semplice per `Rating` che identifica in modo univoco questa istanza. Deve essere un nome di nodo valido per il repository.

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Membri {#members}

È consentita una sola classificazione per membro. Il membro può modificare il proprio rating in qualsiasi momento.

### Anonimo {#anonymous}

Pubblicazione anonima di una classificazione non supportata. I visitatori del sito devono registrarsi (diventare membro) e accedere per partecipare.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sulla valutazione](rating-basics.md) per sviluppatori.
