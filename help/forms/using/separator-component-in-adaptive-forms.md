---
title: Componente separatore nei moduli adattivi
description: È possibile utilizzare il componente Separatore per separare visivamente le sezioni di un modulo.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 5%
---
# Componente separatore nei moduli adattivi{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

È possibile utilizzare il componente Separatore per separare visivamente i pannelli di un modulo. È possibile definire l&#39;aspetto e lo stile generali di un componente separatore specificando le seguenti proprietà del componente separatore:

* **Nome elemento:** Specifica il nome del componente. Le espressioni SOM indirizzano il componente con un valore specificato nel campo Nome elemento.
* **Spessore:** Specifica lo spessore in pixel del componente separatore.

* **Classe CSS:** Specifica la classe CSS personalizzata per il componente separatore

* **Stili in linea:** Con AEM Forms, ora puoi applicare stili CSS in linea ai singoli componenti dei moduli adattivi e visualizzare in anteprima le modifiche in tempo reale.

Puoi utilizzare la modalità Layout per definire il numero di colonne su cui si estende il componente Separatore. Per ulteriori informazioni, vedere [Utilizzare la modalità Layout per ridimensionare i componenti](../../forms/using/resize-using-layout-mode.md).

Per specificare le proprietà di un componente separatore:

1. Selezionare un componente separatore e selezionare ![cmppr](assets/cmppr.png). Le proprietà si aprono nella barra laterale.
1. Fai clic su una scheda nella sezione Proprietà CSS in linea per specificare le proprietà CSS. Ad esempio: a. Nella scheda Campo fare clic su **Aggiungi elemento**. Viene aggiunta una riga con due campi.
1. Nel primo campo da sinistra, specifica una proprietà CSS3 da applicare. Ad esempio, **border**. Puoi anche selezionare una proprietà facendo clic sul pulsante freccia giù. L’elenco a discesa non è esaustivo ed è possibile specificare qualsiasi nome di proprietà CSS3 supportato in questo campo.
1. Nel campo adiacente, specifica un valore valido per la proprietà CSS3 specificata. Ad esempio, **3 px nero solido**.
1. Fare clic su **Aggiungi elemento** per specificare un&#39;altra proprietà e il relativo valore.
1. Fai clic su **Anteprima** per visualizzare in anteprima le modifiche nel modulo.
1. Fare clic su **OK** se si desidera confermare le modifiche oppure su **Annulla** per uscire dalla finestra di dialogo senza apportare modifiche.
