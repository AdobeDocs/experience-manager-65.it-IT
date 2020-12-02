---
title: Utilizzo della votazione
seo-title: Utilizzo della votazione
description: Aggiunta del componente Voto a una pagina
seo-description: Aggiunta del componente Voto a una pagina
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# Utilizzo del voto {#using-voting}

Il componente `Voting` è uno strumento utile che consente ai membri della comunità di valutare un particolare contenuto, ad esempio una risposta all&#39;interno di un componente QnA. Con il componente `Voting`, i membri selezionano frecce verso l&#39;alto o il basso per indicare la propria opinione.

## Aggiunta della votazione a una pagina {#adding-voting-to-a-page}

Per aggiungere un componente `Voting` a una pagina in modalità di creazione, usate il browser componenti per individuare `Communities / Voting` e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione su cui gli utenti possono votare.

Per le informazioni necessarie, visitare [Community Components Basics](basics.md).

Quando vengono incluse le [librerie lato client ](essentials-voting.md#essentials-for-client-side), viene visualizzato il componente `Voting`.

![componente di voto](assets/voting-component.png)

## Configurazione del voto {#configuring-voting}

Selezionare il componente `Voting` inserito a cui accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

Nella scheda **[!UICONTROL Testi e etichette]**, specificare le proprietà utilizzate per registrare i voti.

![etichetta di voto](assets/voting-label.png)

* **[!UICONTROL Etichetta risposta positiva]**

   (*Obbligatorio*) Il nome della proprietà interna per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

   (*Obbligatorio*) Il nome della proprietà interna per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

   (*Obbligatorio*) Il nome di proprietà interno identificabile per questa istanza di un componente di voto.

## Esperienza visitatori del sito {#site-visitor-experience}

### Membri {#members}

I deputati possono votare una sola volta, ma possono modificare il loro voto in qualsiasi momento.

### Anonimo {#anonymous}

Il voto anonimo non è supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l&#39;accesso per partecipare alle votazioni una volta.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Voting Essentials](essentials-voting.md) dedicata agli sviluppatori.
