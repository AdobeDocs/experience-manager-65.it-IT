---
title: Creazione di una pagina di contenuto per dispositivi mobili
description: Quando si effettua l’authoring per i dispositivi mobili, è possibile alternare tra diversi emulatori per capire che cosa vedrà l’utente finale.
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 27%

---

# Authoring di una pagina per dispositivi mobili{#authoring-a-page-for-mobile-devices}

Quando crei una pagina mobile, questa viene visualizzata in modo da simulare il dispositivo mobile. Durante l’authoring della pagina, puoi passare da un emulatore all’altro per vedere cosa vedrà l’utente finale quando accede alla pagina.

I dispositivi sono raggruppati nelle categorie feature, smart e touch in base alle capacità dei dispositivi di rendering di una pagina. Quando l’utente accede a una pagina mobile, AEM rileva il dispositivo e invia la rappresentazione corrispondente al gruppo di dispositivi.

>[!NOTE]
>
>Per creare un sito mobile basato su un sito standard esistente, crea una Live Copy del sito standard. (Vedi [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm-livecopy.md).)
>
>Gli sviluppatori AEM possono creare nuovi gruppi di dispositivi. (Vedi [Creazione di filtri per i gruppi di dispositivi](/help/sites-developing/groupfilters.md).)

Segui la procedura seguente per creare una pagina mobile:

1. Dalla navigazione globale apri la console **Sites**.
1. Apri la pagina **We.Retail** -> **Stati Uniti** -> **Inglese**.

1. Passa a **Anteprima** modalità.
1. Passa all’emulatore desiderato facendo clic sull’icona del dispositivo nella parte superiore della pagina.
1. Trascina i componenti dal browser Componenti alla pagina.

La pagina ha un aspetto simile al seguente:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Gli emulatori vengono disattivati quando una pagina nell’istanza di authoring viene richiesta da un dispositivo mobile.
