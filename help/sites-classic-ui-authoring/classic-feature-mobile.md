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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 58%
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
1. Apri la pagina **Prodotti** sotto **Siti Web** >> **Sito Geometrixx Mobile Demo** >> **Inglese**.

1. Passa a un emulatore diverso. A tale scopo, puoi effettuare le seguenti operazioni:

   * Fai clic sull’icona del dispositivo nella parte superiore della pagina.
   * Fai clic sul pulsante **Modifica** in **Sidekick** e seleziona il dispositivo nel menu a discesa.

1. Trascina e rilascia il componente **Testo e immagine** dalla scheda Mobile di Sidekick alla pagina.
1. Modifica il componente e aggiungi del testo. Fare clic su **OK** per salvare le modifiche.

L&#39;aspetto della pagina è lo stesso del seguente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile. L’authoring può quindi essere eseguito utilizzando l’interfaccia touch.
