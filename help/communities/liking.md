---
title: Utilizzo del collegamento
seo-title: Utilizzo del collegamento
description: Aggiunta e configurazione del componente Collegamento
seo-description: Aggiunta e configurazione del componente Collegamento
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: e7268e43620860b7a1f7aa0a1f1a54199dadcf17
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 6%

---


# Utilizzo del collegamento {#using-liking}

Il `Liking` componente è uno strumento utile che consente agli utenti di esprimere un’opinione su un particolare contenuto, ad esempio un commento all’interno di un forum. Con il `Liking` componente, i membri selezionano l&#39;icona del cuore per indicare un&#39;opinione positiva.

## Aggiunta di collegamenti a una pagina {#adding-liking-to-a-page}

Per aggiungere un `Liking` componente a una pagina in modalità di creazione, usate il browser Componenti per individuare

* `Communities / Liking`

e trascinarlo nella posizione desiderata sulla pagina, ad esempio una posizione relativa alla funzione che gli utenti possano apprezzare.

Per le informazioni necessarie, consulta [Community Components Basics](basics.md).

Quando vengono incluse le librerie [lato client](essentials-liking.md#essentials-for-client-side) richieste, viene visualizzato così il `Liking` componente.

![chlimage_1-93](assets/chlimage_1-93.png)

## Configurazione del collegamento {#configuring-liking}

Selezionate il `Liking` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![chlimage_1-94](assets/chlimage_1-94.png)

Nella scheda **[!UICONTROL Testo ed etichette]** , specificare le proprietà utilizzate per registrare i like.

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL Etichetta risposta positiva]**

   (*Obbligatorio*) Nome della proprietà per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

   (*Obbligatorio*) Il nome della proprietà per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

   (*Obbligatorio*) Il nome della proprietà interna e identificabile per questa istanza di un componente con diritto di voto.

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Membri {#members}

I membri possono cambiare il proprio stile in qualsiasi momento.

### Anonimo {#anonymous}

Il collegamento anonimo non è supportato. I visitatori del sito devono registrarsi (diventare membri) ed effettuare l’accesso per partecipare al loro collegamento.

## Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Liking Essentials](essentials-liking.md) (Collegamenti essenziali) per gli sviluppatori.
