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

Il `Liking` Il componente è uno strumento utile che consente agli utenti di esprimere un’opinione su un particolare contenuto, ad esempio un commento all’interno di un forum. Con il `Liking` componente, i membri selezionano l’icona del cuore per indicare un’opinione positiva.

## Aggiunta di un collegamento a una pagina {#adding-liking-to-a-page}

Per aggiungere una `Liking` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Liking`

Trascinalo in posizione su una pagina, ad esempio una posizione relativa alla funzione desiderata dagli utenti.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](basics.md).

Quando [librerie lato client richieste](essentials-liking.md#essentials-for-client-side) sono inclusi, è così che `Liking` viene visualizzato.

![componente-gradimento](assets/liking-component.png)

## Configurazione di Mi piace {#configuring-liking}

Seleziona la inserita `Liking` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configure-new](assets/configure-new.png)

Sotto **[!UICONTROL Testi ed etichette]** , specifica le proprietà utilizzate per registrare mi piace.

![tipo di configurazione](assets/configure-liking.png)

* **[!UICONTROL Etichetta risposta positiva]**

  (*Obbligatorio*) Nome della proprietà per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

  (*Obbligatorio*) Nome della proprietà per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

  (*Obbligatorio*) Nome di proprietà interno e identificabile per questa istanza di un componente voting.

## Esperienza visitatore del sito {#site-visitor-experience}

### Membri {#members}

I membri possono cambiare il proprio Mi piace in qualsiasi momento.

### Anonimo {#anonymous}

Il collegamento anonimo non è supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l&#39;accesso per partecipare al Mi piace.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base su Mi piace](essentials-liking.md) pagina per sviluppatori.
