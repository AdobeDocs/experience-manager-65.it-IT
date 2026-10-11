---
title: Creare tabelle complesse accessibili nei moduli HTML5
description: Scopri come creare tabelle accessibili nei moduli di HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 5%
---
# Creare tabelle complesse accessibili nei moduli HTML5 {#create-accessible-complex-tables-in-html-forms}

L’implementazione predefinita delle tabelle in HTML5 Forms utilizza gli elementi DIV di HTML per eseguire il rendering di una tabella. Il rendering prevede l’utilizzo dei ruoli ARIA per soddisfare i requisiti di accessibilità.

Per evitare problemi di accessibilità con gli assistenti vocali che non supportano completamente i ruoli ARIA utilizzati con le tabelle dati, HTML5 Forms fornisce una rappresentazione alternativa per le tabelle. Queste tabelle si basano sul nuovo formato di tabella introdotto in Designer che supporta anche:

* Intestazioni di riga
* Estensione riga

Per utilizzare il nuovo formato in HTML5 Forms, contrassegna la tabella come complessa. Per contrassegnare la tabella come complessa, aggiungere il tag `extras` nell&#39;origine XML della sottomaschera di tabella nel modo seguente:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Le tabelle contrassegnate come *complexTable* seguono il rendering nativo di HTML e forniscono un migliore supporto per l&#39;accesso facilitato ad alcuni assistenti vocali.  Per creare un&#39;estensione di riga, selezionare celle consecutive di una tabella nella stessa colonna, fare clic con il pulsante destro del mouse sulla selezione e quindi scegliere **[!UICONTROL Unisci celle]**.

>[!NOTE]
>
>La creazione di un&#39;estensione di riga funziona solo per le celle più a sinistra.

Per contrassegnare una riga come intestazione di riga, selezionare tutte le celle nella riga, fare clic con il pulsante destro del mouse sulla selezione e quindi scegliere **[!UICONTROL Contrassegna intestazione]**.

Per contrassegnare una cella come intestazione di colonna, selezionare una cella qualsiasi nella colonna, fare clic con il pulsante destro del mouse sulla selezione e quindi scegliere **[!UICONTROL Contrassegna intestazione]**.

Limitazioni nel nuovo formato *AccessibleTable*:

* Mancanza di supporto per i campi espandibili se nella tabella viene utilizzato rowspan
* Tabelle nidificate (tabelle all’interno di celle di tabella) non supportate
* Il supporto per rowspan è limitato alle righe e alle celle di intestazione
* Il supporto è limitato alle tabelle regolari
* Nelle tabelle con rowspan > 1 non è supportato alcun tipo di precompilazione dei dati
