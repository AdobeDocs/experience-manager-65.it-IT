---
title: Attiva l’interruttore delle funzioni per integrare le funzioni di adozione anticipata e prerelease
description: L’attivazione delle funzioni è una funzionalità di AEM che consente agli amministratori di abilitare le nuove funzioni in un ambiente di runtime.
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
source-git-commit: 794d93d890ba752f9036a85831f7cbc8391fb545
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 2%

---

# Attivazione/disattivazione delle funzioni in Adobe Experience Manager (AEM) 6.5{#enable-feature-toggle-aem-forms-65}

La funzione di attivazione/disattivazione delle funzioni è una funzionalità di AEM che consente agli amministratori di abilitare o disabilitare in modo dinamico funzioni specifiche. Questa funzionalità è particolarmente utile per la gestione di **funzioni Early Adopter** e **funzioni prerelease** senza richiedere distribuzioni principali o modifiche alla base di codice. Garantisce flessibilità e controllo su quali funzioni sono accessibili in un ambiente AEM.

## Attiva/disattiva funzione {#enable-feature-toggle-65}

È possibile configurare gli interruttori delle funzionalità per i primi utenti o le nuove funzionalità tramite la **console Web AEM** seguendo la procedura seguente:

1. Accedi all’istanza di AEM Forms.
2. Accedi a `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Cerca **Provider di attivazione/disattivazione dinamica Adobe Granite** in Configuration Manager.
4. Fai clic sull&#39;icona ![icona-matita](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. Nella sezione [!UICONTROL Attivazione/disattivazione] fare clic su ![icona a forma di matita](assets/aem6forms_add.png).
6. Aggiungi l’ID di attivazione/disattivazione della funzione, come illustrato nell’immagine seguente.
   ![Aggiungi/nascondi](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >L’ID di attivazione/disattivazione della funzione è disponibile nel documento specifico per le funzioni utilizzate in precedenza.

7. Fai clic su Salva.

## Disabilita attivazione funzionalità {#disable-feature-toggle-65}

Per disattivare l&#39;attivazione/disattivazione delle funzionalità per le funzionalità attivate, procedere come segue:

1. Accedi all’istanza di AEM Forms.
2. Accedi a `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Cerca **Provider di attivazione/disattivazione dinamica Adobe Granite** in Configuration Manager.
4. Fai clic sull&#39;icona ![icona-matita](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. Nella sezione [!UICONTROL Attivazione/disattivazione] fare clic su ![icona a forma di matita](assets/aem6forms_add.png).
6. Aggiungi il numero di attivazione/disattivazione della funzione.
   ![Rimuovi](assets/remove_toggle_feature_forms.png)
7. Fai clic su Salva.

## Considerazioni tecniche

Gli interruttori delle funzioni sono specifici dell’ambiente e vengono gestiti in fase di runtime, pertanto non richiedono il riavvio del server. Tuttavia, alcune funzioni potrebbero richiedere l’aggiornamento delle pagine rilevanti o la cancellazione della cache per riflettere le modifiche.
È possibile accedere all&#39;elenco delle funzionalità abilitate tramite l&#39;interruttore delle funzionalità per l&#39;ambiente tramite `http://<author-instance-url>:4502/etc.clientlibs/toggles.json`.