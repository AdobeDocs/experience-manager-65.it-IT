---
title: Authoring di una pagina per dispositivi mobili
description: Quando crei una pagina mobile, questa viene visualizzata in modo da simulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.
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

Quando crei una pagina mobile, questa viene visualizzata in modo da simulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.

I dispositivi sono raggruppati nelle categorie feature, smart e touch in base alle capacità dei dispositivi di rendering di una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione corrispondente al gruppo di dispositivi.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. (Vedi [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm-livecopy.md).)
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. (Vedi [Creazione di filtri per i gruppi di dispositivi.](/help/sites-developing/groupfilters.md))

Segui la procedura seguente per creare una pagina mobile:

1. Nel browser, vai alla pagina **Siteadmin** console.
1. Apri **Prodotti** pagina sottostante **Siti Web** >> **Sito Demo Di Geometrixx Mobile** >> **Inglese**.

1. Passa a un emulatore diverso. A questo scopo, puoi effettuare le seguenti operazioni:

   * Fai clic sull’icona del dispositivo nella parte superiore della pagina.
   * Fai clic sul pulsante **Modifica** nel **Barra laterale** e seleziona il dispositivo nel menu a discesa.

1. Trascina e rilascia la **Testo e immagine** Dalla scheda Mobile della barra laterale alla pagina.
1. Modifica il componente e aggiungi del testo. Fai clic su **OK** per salvare le modifiche.

La pagina si presenta come segue:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile. L’authoring può quindi essere eseguito utilizzando l’interfaccia touch.
