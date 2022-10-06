---
title: Testo segnaposto in AEM Forms
seo-title: Placeholder text in AEM Forms
description: Il testo segnaposto ha lo scopo di aiutare l’utente a inserire dati quando il controllo non ha alcun valore. Può trattarsi di un valore di esempio o di una breve descrizione del formato previsto.
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Testo segnaposto in AEM Forms {#placeholder-text-in-aem-forms}

Il testo segnaposto rappresenta una parola o una frase breve. Ha lo scopo di aiutare l’utente a inserire dati quando il controllo non ha alcun valore. Un testo segnaposto può essere un valore di esempio o una breve descrizione del formato previsto. Il testo segnaposto viene visualizzato prima che l’utente immetta un valore e viene rimosso quando l’utente immette o seleziona un valore.

>[!NOTE]
>
>Il testo segnaposto, se specificato, deve avere un valore che non contenga nuovi caratteri di riga.

![Componente data con e senza testo segnaposto](assets/dat-picker-place-holder-text.png)

**A.** Componente data con testo segnaposto **B.** Componente data senza testo segnaposto

AEM Forms supporta il testo segnaposto per i campi Casella password, Selezione data, Casella numerica e Casella di testo.\
I testi segnaposto non sono supportati per il widget di data nativo di HTML5. Per specificare un testo segnaposto:

1. Fai clic con il pulsante destro del mouse su un componente che supporta il testo segnaposto e fai clic su **Modifica**. Viene visualizzata la finestra di dialogo Modifica componente.

1. Apri **Titolo e testo** scheda .
1. Specifica una parola o una frase breve nel **Casella di testo segnaposto**. Fai clic su **OK**.

>[!NOTE]
>
>Il testo segnaposto non è supportato in Microsoft Internet Explorer 9.
