---
title: Testo segnaposto in AEM Forms
description: Il testo segnaposto ha lo scopo di aiutare l'utente a immettere dati quando il controllo non contiene alcun valore. Potrebbe essere un valore di esempio o una breve descrizione del formato previsto.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 1%

---

# Testo segnaposto in AEM Forms {#placeholder-text-in-aem-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Il testo segnaposto rappresenta una parola o una breve frase. Lo scopo è quello di aiutare l&#39;utente a inserire dati quando il controllo non ha valore. Un testo segnaposto può essere un valore di esempio o una breve descrizione del formato previsto. Il testo segnaposto viene visualizzato prima che l’utente immetta un valore, viene rimosso quando l’utente immette o seleziona un valore.

>[!NOTE]
>
>Il testo segnaposto, se specificato, deve avere un valore che non contenga caratteri di riga nuovi.

![Componente data con e senza testo segnaposto](assets/dat-picker-place-holder-text.png)

**R.** Componente data con testo segnaposto **B.** Componente data senza testo segnaposto

AEM Forms supporta il testo segnaposto per i campi casella Password, selettore data, casella Numerica e casella di testo.\
I testi segnaposto non sono supportati per il widget data nativo di HTML5. Per specificare un testo segnaposto:

1. Fai clic con il pulsante destro del mouse su un componente che supporta il testo segnaposto e fai clic su **Modifica**. Viene visualizzata la finestra di dialogo Modifica componente.

1. Apri **Titolo e testo** scheda.
1. Specifica una parola o una breve frase nel **Casella di testo segnaposto**. Fai clic su **OK**.

>[!NOTE]
>
>Testo segnaposto non supportato in Microsoft Internet Explorer 9.
