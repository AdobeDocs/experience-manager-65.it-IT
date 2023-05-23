---
title: Utilizzo della votazione
seo-title: Using Voting
description: Aggiunta del componente Votazione a una pagina
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# Utilizzo della votazione {#using-voting}

Il `Voting` Il componente è uno strumento utile che consente ai membri della community di assegnare una valutazione a un particolare contenuto, ad esempio una risposta all’interno di un componente Controllo qualità. Con il `Voting` componente, i membri selezionano frecce verso l&#39;alto o verso il basso per indicare la propria opinione.

## Aggiunta di voti a una pagina {#adding-voting-to-a-page}

Per aggiungere una `Voting` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare `Communities / Voting` e trascinarlo in una pagina, ad esempio una posizione relativa alla funzione su cui gli utenti possono votare.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](essentials-voting.md#essentials-for-client-side) sono inclusi, è così che `Voting` verrà visualizzato.

![componente voto](assets/voting-component.png)

## Configurazione della votazione {#configuring-voting}

Seleziona la inserita `Voting` per accedere e selezionare il `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Sotto **[!UICONTROL Testi ed etichette]** , specificare le proprietà utilizzate per registrare i voti.

![voting-label](assets/voting-label.png)

* **[!UICONTROL Etichetta risposta positiva]**

   (*Obbligatorio*) Nome della proprietà interna per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

   (*Obbligatorio*) Nome della proprietà interna per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

   (*Obbligatorio*) Nome di proprietà interno e identificabile per questa istanza di un componente voting.

## Esperienza visitatore del sito {#site-visitor-experience}

### Membri {#members}

I deputati possono votare una sola volta, ma possono cambiare il loro voto in qualsiasi momento.

### Anonimo {#anonymous}

Voto anonimo non supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l&#39;accesso per partecipare una volta sola alle votazioni.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Elementi di base per la votazione](essentials-voting.md) pagina per sviluppatori.
