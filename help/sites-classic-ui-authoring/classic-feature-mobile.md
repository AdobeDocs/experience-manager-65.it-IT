---
title: Authoring di una pagina per dispositivi mobili
seo-title: Authoring di una pagina per dispositivi mobili
description: Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.
seo-description: Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 84%

---


# Authoring di una pagina per dispositivi mobili {#authoring-a-page-for-mobile-devices}

Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.

I dispositivi sono raggruppati nelle categorie feature, smart e touch, a seconda delle funzionalità dei dispositivi di riprodurre una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al gruppo di dispositivi a cui appartiene.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. (Vedere [Creazione di una Live Copy per diversi canali](/help/sites-administering/msm-livecopy.md).)
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. (Vedere [Creazione di filtri per gruppi di dispositivi.](/help/sites-developing/groupfilters.md))

Segui la procedura seguente per creare una pagina mobile:

1. Nel browser, passate alla console **Site Admin** (Amministrazione sito).
1. Aprite la pagina **Products** sotto **Websites** >> **Geometrixx Demo mobile Site** >> **English**.

1. Passa a un altro emulatore effettuando una delle seguenti operazioni:

   * Fate clic sull’icona del dispositivo nella parte superiore della pagina.
   * Fate clic sul pulsante **Modifica** nella **barra laterale** e selezionate il dispositivo dal menu a discesa.

1. Trascinare il componente **Testo e immagine** dalla scheda Mobile della barra laterale alla pagina.
1. Modificate il componente e aggiungete del testo. Fate clic su **OK** per salvare le modifiche.

La pagina si presenta come illustrato di seguito:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile. L’authoring può essere eseguito utilizzando l’interfaccia touch.

