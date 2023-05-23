---
title: Authoring di una pagina per dispositivi mobili
description: Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 13%

---

# Authoring di una pagina per dispositivi mobili{#authoring-a-page-for-mobile-devices}

Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.

I dispositivi sono raggruppati in categorie, funzione, smart e touch in base alle funzionalità dei dispositivi per il rendering di una pagina. Quando l’utente finale accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al suo gruppo di dispositivi.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. (vedere [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm-livecopy.md).)
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. (vedere [Creazione di filtri per gruppi di dispositivi.](/help/sites-developing/groupfilters.md))

Segui la procedura seguente per creare una pagina mobile:

1. Nel browser, vai al **Siteadmin** console.
1. Apri **Prodotti** pagina sotto **Siti Web** >> **Geometrixx sito demo mobile** >> **Inglese**.

1. Passa a un emulatore diverso. A tale scopo, puoi effettuare le seguenti operazioni:

   * Fai clic sull’icona del dispositivo nella parte superiore della pagina.
   * Fai clic su **Modifica** pulsante in **Barra laterale** e selezionare il dispositivo nel menu a discesa.

1. Trascina la **Testo e immagine** dalla scheda Mobile della barra laterale alla pagina.
1. Modifica il componente e aggiungi del testo. Clic **OK** per salvare le modifiche.

L&#39;aspetto della pagina è lo stesso del seguente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile. L’authoring può quindi essere eseguito utilizzando l’interfaccia touch.
