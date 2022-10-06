---
title: Authoring di una pagina per dispositivi mobili
seo-title: Authoring a Page for Mobile Devices
description: Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.
seo-description: When authoring a mobile page, the page is displayed in a way that emulates the mobile device. When authoring the page, you can switch between several emulators to see what the end-user sees when accessing the page.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 82%

---

# Authoring di una pagina per dispositivi mobili{#authoring-a-page-for-mobile-devices}

Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.

I dispositivi sono raggruppati nelle categorie feature, smart e touch, a seconda delle funzionalità dei dispositivi di riprodurre una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al gruppo di dispositivi a cui appartiene.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. (Vedi [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm-livecopy.md).)
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. (Vedi [Creazione di filtri per i gruppi di dispositivi.](/help/sites-developing/groupfilters.md))

Segui la procedura seguente per creare una pagina mobile:

1. Nel browser, passate alla console **Site Admin** (Amministrazione sito).
1. Apri **Prodotti** pagina sottostante **Siti Web** >> **Sito Demo Di Geometrixx Mobile** >> **Inglese**.

1. Passa a un altro emulatore effettuando una delle seguenti operazioni:

   * Fate clic sull’icona del dispositivo nella parte superiore della pagina.
   * Fate clic sul pulsante **Modifica** nella **barra laterale** e selezionate il dispositivo dal menu a discesa.

1. Trascina e rilascia la **Testo e immagine** Dalla scheda Mobile della barra laterale alla pagina.
1. Modificate il componente e aggiungete del testo. Fate clic su **OK** per salvare le modifiche.

La pagina si presenta come illustrato di seguito:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile. L’authoring può quindi essere eseguito utilizzando l’interfaccia touch.
