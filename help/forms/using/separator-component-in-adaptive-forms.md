---
title: Componente separatore nei moduli adattivi
seo-title: Componente separatore nei moduli adattivi
description: È possibile utilizzare il componente separatore per separare visivamente sezioni di un modulo.
seo-description: È possibile utilizzare il componente separatore per separare visivamente sezioni di un modulo.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Componente separatore nei moduli adattivi{#separator-component-in-adaptive-forms}

È possibile utilizzare il componente separatore per separare visivamente i pannelli di un modulo. È possibile definire l’aspetto e lo stile generali di un componente separatore specificando le seguenti proprietà del componente separatore:

* **Nome elemento:** specifica il nome del componente. Le espressioni SOM si rivolgono al componente con il valore specificato nel campo Nome elemento .
* **Spessore:** specifica lo spessore in pixel del componente separatore.

* **Classe CSS:** specifica la classe CSS personalizzata per il componente separatore

* **Stili in linea:** con AEM Forms, ora puoi applicare gli stili CSS in linea ai singoli componenti dei moduli adattivi e visualizzare in anteprima le modifiche in tempo reale.

È possibile utilizzare la modalità Layout per definire il numero di colonne su cui si estende il componente separatore. Per ulteriori informazioni, consulta [Utilizzare la modalità Layout per ridimensionare i componenti](../../forms/using/resize-using-layout-mode.md).

Per specificare le proprietà di un componente separatore:

1. Seleziona un componente separatore e tocca ![cmppr](assets/cmppr.png). Le proprietà si aprono nella barra laterale.
1. Fai clic su una scheda nella sezione Proprietà CSS in linea per specificare le proprietà CSS. Ad esempio: a) Nella scheda Campo, fai clic su **Aggiungi elemento**. Viene aggiunta una riga con due campi.
1. Nel primo campo da sinistra, specifica una proprietà CSS3 da applicare. Ad esempio, **border**. È inoltre possibile selezionare una proprietà facendo clic sul pulsante freccia giù. L’elenco a discesa non è esaustivo e puoi specificare qualsiasi nome di proprietà CSS3 supportato in questo campo.
1. Nel campo adiacente, specifica un valore valido per la proprietà CSS3 specificata. Ad esempio, **3px solid black**.
1. Fare clic su **Aggiungi elemento** per specificare un&#39;altra proprietà e il relativo valore.
1. Fare clic su **Anteprima** per visualizzare in anteprima le modifiche apportate al modulo.
1. Fai clic su **OK** per confermare le modifiche o su **Annulla** per uscire dalla finestra di dialogo senza apportare alcuna modifica.

