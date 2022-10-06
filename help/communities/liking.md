---
title: Utilizzo del collegamento
seo-title: Using Liking
description: Aggiunta e configurazione del componente Collegamento
seo-description: Adding and configuring the Liking component
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---

# Utilizzo del collegamento {#using-liking}

La `Liking` Componente è uno strumento utile che consente agli utenti di esprimere un’opinione su un particolare contenuto, ad esempio un commento all’interno di un forum. Con la `Liking` i membri selezionano l&#39;icona del cuore per indicare un&#39;opinione positiva.

## Aggiunta di collegamenti a una pagina {#adding-liking-to-a-page}

Per aggiungere una `Liking` componente per una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Liking`

e trascinarlo nella posizione desiderata su una pagina, ad esempio una posizione relativa alla funzione.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](basics.md).

Quando il [librerie lato client richieste](essentials-liking.md#essentials-for-client-side) sono inclusi, è così che `Liking` apparirà .

![componente di gradimento](assets/liking-component.png)

## Configurazione del collegamento {#configuring-liking}

Seleziona il `Liking` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configure-new](assets/configure-new.png)

Sotto la **[!UICONTROL Testi ed etichette]** specificare le proprietà utilizzate per registrare i like.

![configurare-like](assets/configure-liking.png)

* **[!UICONTROL Etichetta risposta positiva]**

   (*Obbligatorio*) Nome della proprietà per una risposta positiva.

* **[!UICONTROL Etichetta risposta negativa]**

   (*Obbligatorio*) Nome della proprietà per una risposta negativa.

* **[!UICONTROL Nome conteggio]**

   (*Obbligatorio*) Il nome della proprietà interna e identificabile per questa istanza di un componente di voto.

## Esperienza dei visitatori del sito {#site-visitor-experience}

### Membri {#members}

I membri possono cambiare il loro atteggiamento in qualsiasi momento.

### Anonimo {#anonymous}

Il collegamento anonimo non è supportato. I visitatori del sito devono registrarsi (diventare membro) e accedere per partecipare.

## Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base](essentials-liking.md) per sviluppatori.
