---
title: Authoring di una pagina per dispositivi mobili
description: Quando si effettua l’authoring di una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 52%

---

# Authoring di una pagina per dispositivi mobili{#authoring-a-page-for-mobile-devices}

Quando si effettua l’authoring di una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.

I dispositivi sono raggruppati nelle categorie funzione, smart e touch in base alle funzionalità dei dispositivi per il rendering di una pagina. Quando l’utente finale accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al suo gruppo di dispositivi.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. (Vedi [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm-livecopy.md).)
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. (Vedi [Creazione di filtri per gruppi di dispositivi.](/help/sites-developing/groupfilters.md))

Segui la procedura seguente per creare una pagina mobile:

1. Nel browser, accedi alla console **Siteadmin**.
1. Apri la pagina **Prodotti** sotto **Siti Web** >> **Geometrixx sito demo mobile** >> **Inglese**.

1. Passa a un emulatore diverso. A tale scopo, puoi effettuare le seguenti operazioni:

   * Fai clic sull’icona del dispositivo nella parte superiore della pagina.
   * Fai clic sul pulsante **Modifica** nel **Sidekick** e seleziona il dispositivo nel menu a discesa.

1. Trascina e rilascia il componente **Testo e immagine** dalla scheda Mobile del Sidekick alla pagina.
1. Modifica il componente e aggiungi del testo. Fare clic su **OK** per salvare le modifiche.

L&#39;aspetto della pagina è lo stesso del seguente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile. L’authoring può quindi essere eseguito utilizzando l’interfaccia touch.
