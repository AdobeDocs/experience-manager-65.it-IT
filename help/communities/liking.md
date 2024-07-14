---
title: Utilizzo di Mi piace
description: Scopri come aggiungere e configurare il componente Mi piace in modo che gli utenti possano esprimere un’opinione su un particolare contenuto, ad esempio un commento.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Utilizzo di Mi piace {#using-liking}

Il componente `Liking` è uno strumento utile che consente agli utenti di esprimere un&#39;opinione su un particolare contenuto, ad esempio un commento all&#39;interno di un forum. Con il componente `Liking`, i membri selezionano l&#39;icona del cuore per indicare un&#39;opinione positiva.

## Aggiunta di un collegamento a una pagina {#adding-liking-to-a-page}

Per aggiungere un componente `Liking` a una pagina in modalità di creazione, utilizza il browser componenti per individuare

* `Communities / Liking`

Trascinalo in posizione su una pagina, ad esempio una posizione relativa alla funzione desiderata dagli utenti.

Per informazioni necessarie, visitare [Nozioni di base sui componenti delle community](basics.md).

Quando sono incluse le [librerie lato client richieste](essentials-liking.md#essentials-for-client-side), il componente `Liking` viene visualizzato in questo modo.

![componente-Mi piace](assets/liking-component.png)

## Configurazione di Mi piace {#configuring-liking}

Selezionare il componente `Liking` inserito in modo da poter accedere e selezionare l&#39;icona `Configure` che apre la finestra di dialogo per modifica.

![configura-nuovo](assets/configure-new.png)

Nella scheda **[!UICONTROL Testi ed etichette]**, specifica le proprietà utilizzate per registrare Mi piace.

![simulazione](assets/configure-liking.png)

* **[!UICONTROL Etichetta risposta positiva]**

  (*Obbligatorio*) Nome della proprietà per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

  (*Obbligatorio*) Nome della proprietà per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

  (*Obbligatorio*) Il nome della proprietà interna identificabile per questa istanza di un componente voting.

## Esperienza visitatore del sito {#site-visitor-experience}

### Membri {#members}

I membri possono cambiare il proprio Mi piace in qualsiasi momento.

### Anonimo {#anonymous}

Il collegamento anonimo non è supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l&#39;accesso per partecipare al Mi piace.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Preferenze di Essentials](essentials-liking.md) per sviluppatori.
