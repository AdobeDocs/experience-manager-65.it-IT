---
title: Authoring di una pagina per dispositivi mobili
seo-title: Authoring a Page for Mobile Devices
description: Quando si effettua l’authoring per i dispositivi mobili, è possibile alternare tra diversi emulatori per capire che cosa vedrà l’utente finale
seo-description: When authoring for mobile, you can switch between several emulators to see what the end-user sees
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 88%

---

# Authoring di una pagina per dispositivi mobili {#authoring-a-page-for-mobile-devices}

Quando crei una pagina mobile, questa viene visualizzata in modo da emulare il dispositivo mobile. Quando crei la pagina, puoi scegliere tra diversi emulatori per verificare come la pagina verrà effettivamente vista dal visitatore.

I dispositivi sono raggruppati nelle categorie feature, smart e touch, a seconda delle funzionalità dei dispositivi di riprodurre una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione che corrisponde al gruppo di dispositivi a cui appartiene.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. (Vedi [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm-livecopy.md).)
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. (Vedi [Creazione di filtri per i gruppi di dispositivi](/help/sites-developing/groupfilters.md).)

Segui la procedura seguente per creare una pagina mobile:

1. Dalla navigazione globale apri la console **Sites**.
1. Apri la pagina **We.Retail** -> **Stati Uniti** -> **Inglese**.

1. Passa a **Anteprima** modalità.
1. Passa all&#39;emulatore desiderato facendo clic sull&#39;icona del dispositivo nella parte superiore della pagina.
1. Trascina e rilascia i componenti dal browser componente alla pagina.

La pagina avrà un aspetto simile al seguente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile.
