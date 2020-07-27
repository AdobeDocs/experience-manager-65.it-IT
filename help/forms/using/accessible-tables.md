---
title: Creazione di tabelle complesse con accesso facilitato nei moduli HTML5
seo-title: Creazione di tabelle complesse con accesso facilitato nei moduli HTML5
description: Scoprite come creare tabelle con accesso facilitato nei moduli HTML5.
seo-description: Scoprite come creare tabelle con accesso facilitato nei moduli HTML5.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# Creazione di tabelle complesse con accesso facilitato nei moduli HTML5 {#create-accessible-complex-tables-in-html-forms}

L&#39;implementazione predefinita delle tabelle in HTML5 Forms utilizza elementi DIV HTML per eseguire il rendering di una tabella. Il rendering richiede l&#39;uso dei ruoli ARIA per soddisfare i requisiti di accessibilità.

Per evitare problemi di accessibilità con gli assistenti vocali che non supportano completamente i ruoli ARIA utilizzati con le tabelle di dati, in HTML5 Forms è disponibile una rappresentazione alternativa per le tabelle. Queste tabelle si basano sul nuovo formato di tabella introdotto in Designer e supporta inoltre:

* Intestazioni riga
* Estensione riga

Per utilizzare il nuovo formato in HTML5 Forms, contrassegnare la tabella come complessa. Per contrassegnare la tabella come complessa, aggiungere `extras` tag nell&#39;origine XML del sottomodulo tabella come segue:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Le tabelle contrassegnate come *complesseTable* seguono la rappresentazione HTML nativa e forniscono un supporto di accessibilità migliore per alcuni assistenti vocali.  Per creare un intervallo di righe, selezionare celle consecutive di una tabella nella stessa colonna, fare clic con il pulsante destro del mouse sulla selezione, quindi fare clic su **[!UICONTROL Unisci celle]**.

>[!NOTE]
>
>La creazione di un intervallo di righe funziona solo per le celle più a sinistra.

Per contrassegnare una riga come intestazione di riga, selezionare tutte le celle della riga, fare clic con il pulsante destro del mouse sulla selezione, quindi fare clic su **[!UICONTROL Contrassegna intestazione]**.

Per contrassegnare una cella come intestazione di colonna, selezionare una cella nella colonna, fare clic con il pulsante destro del mouse sulla selezione, quindi fare clic su **[!UICONTROL Contrassegna intestazione]**.

Limitazioni nel nuovo formato *AccessibleTable* :

* Mancanza del supporto per i campi espandibili se nella tabella viene utilizzato l&#39;estensione di riga
* Nessun supporto per tabelle nidificate (tabelle all&#39;interno di celle di tabella)
* Il supporto per l&#39;estensione di riga è limitato alle righe di intestazione e alle celle di intestazione
* Il supporto è limitato alle tabelle regolari
* Nessun supporto delle precompilazioni dei dati nelle tabelle con estensione di riga > 1

