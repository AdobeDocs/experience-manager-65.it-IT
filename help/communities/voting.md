---
title: Utilizzo della votazione
description: Scopri come aggiungere il componente Votazione a una pagina che consente ai membri della community con accesso effettuato di valutare un particolare contenuto, ad esempio una risposta.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# Utilizzo della votazione {#using-voting}

Il componente `Voting` è uno strumento utile che consente ai membri della community di valutare un particolare contenuto, ad esempio una risposta all&#39;interno di un componente di controllo qualità. Con il componente `Voting`, i membri selezionano frecce verso l&#39;alto o verso il basso per indicare la propria opinione.

## Aggiunta di voti a una pagina {#adding-voting-to-a-page}

Per aggiungere un componente `Voting` a una pagina in modalità Creazione, utilizzare il browser Componenti. Individuare `Communities / Voting` e trascinarlo in una pagina, ad esempio una posizione relativa alla funzione su cui gli utenti possono votare.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando sono incluse le [librerie lato client richieste](essentials-voting.md#essentials-for-client-side), il componente `Voting` viene visualizzato in questo modo.

![componente voto](assets/voting-component.png)

## Configurazione della votazione {#configuring-voting}

Selezionare il componente `Voting` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Nella scheda **[!UICONTROL Testi ed etichette]**, specifica le proprietà utilizzate per registrare i voti.

![voting-label](assets/voting-label.png)

* **[!UICONTROL Etichetta risposta positiva]**

  (*Obbligatorio*) Nome della proprietà interna per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

  (*Obbligatorio*) Nome della proprietà interna per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

  (*Obbligatorio*) Il nome della proprietà interna identificabile per questa istanza di un componente voting.

## Esperienza visitatore del sito {#site-visitor-experience}

### Membri {#members}

I deputati possono votare una sola volta, ma possono cambiare il loro voto in qualsiasi momento.

### Anonimo {#anonymous}

Voto anonimo non supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l&#39;accesso per partecipare una volta sola alle votazioni.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Voting Essentials](essentials-voting.md) per sviluppatori.
