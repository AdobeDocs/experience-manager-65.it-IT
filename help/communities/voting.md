---
title: Utilizzo del voto
seo-title: Using Voting
description: Aggiunta del componente Voto a una pagina
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

# Utilizzo del voto {#using-voting}

La `Voting` Componente è uno strumento utile che consente ai membri della community di assegnare una valutazione a un particolare contenuto, ad esempio una risposta all’interno di un componente QnA. Con la `Voting` componenti, i membri selezionano frecce verso l’alto o verso il basso per indicare la propria opinione.

## Aggiunta di un voto a una pagina {#adding-voting-to-a-page}

Per aggiungere una `Voting` componente per una pagina in modalità di creazione, usate il browser componenti per individuare `Communities / Voting` e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione su cui gli utenti possono votare.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](essentials-voting.md#essentials-for-client-side) sono inclusi, è così che `Voting` apparirà .

![componente del voto](assets/voting-component.png)

## Configurazione del voto {#configuring-voting}

Seleziona il `Voting` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

Sotto la **[!UICONTROL Testi ed etichette]** specificare le proprietà utilizzate per registrare i voti.

![etichetta di voto](assets/voting-label.png)

* **[!UICONTROL Etichetta risposta positiva]**

   (*Obbligatorio*) Nome della proprietà interna per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

   (*Obbligatorio*) Nome della proprietà interna per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

   (*Obbligatorio*) Il nome della proprietà interna e identificabile per questa istanza di un componente di voto.

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Membri {#members}

I deputati possono votare una sola volta, ma possono modificare il loro voto in qualsiasi momento.

### Anonimo {#anonymous}

Il voto anonimo non è supportato. I visitatori del sito devono registrarsi (diventare membro) e accedere per partecipare al voto una volta.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Elementi essenziali del voto](essentials-voting.md) per sviluppatori.
