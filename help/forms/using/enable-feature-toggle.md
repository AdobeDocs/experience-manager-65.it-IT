---
title: Attiva l’interruttore delle funzioni per integrare le funzioni di adozione anticipata e prerelease
description: L’attivazione delle funzioni è una funzionalità di AEM che consente agli amministratori di abilitare le nuove funzioni in un ambiente di runtime.
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
exl-id: 08815c2b-23b3-4545-a3ab-ba47ba1c3c55
source-git-commit: 730f8cabd6825ed289238f9000037644a8139301
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 3%

---

# Attivazione/disattivazione delle funzioni in Adobe Experience Manager (AEM) 6.5{#enable-feature-toggle-aem-forms-65}

L’interruttore delle funzioni è una funzionalità di AEM che consente agli amministratori di abilitare o disabilitare in modo dinamico funzioni specifiche. Questa funzionalità è particolarmente utile per la gestione di **funzioni Early Adopter** e **funzioni prerelease** senza richiedere distribuzioni principali o modifiche alla base di codice. Garantisce flessibilità e controllo su quali funzioni sono accessibili in un ambiente AEM.

## Perché utilizzare gli interruttori delle funzioni in una configurazione di AEM 6.5?

Quando si lavora in una configurazione di AEM 6.5, la funzione attiva la guida in:

* Verifica sicura delle caratteristiche sperimentali.

* Rollout di nuovi componenti in fasi.

* Mantenimento di un&#39;unica base di codice in più ambienti.

* Riduzione dei rischi durante le installazioni e gli aggiornamenti.

## Considerazione

A partire da AEM 6.5 SP23, non è necessario installare il bundle [com.adobe.granite.toggle.impl.dev](http://com.adobe.granite.toggle.impl.dev/) in quanto è già installato con il componente aggiuntivo Forms.

## Prerequisiti

Prima di abilitare l’attivazione delle funzioni nella configurazione di AEM 6.5, verifica quanto segue:

* Utente membro del gruppo `forms-users`.

* Passa a `http://<author-instance-url>:portnumber/system/console/bundles` e controlla se il bundle **(com.adobe.granite.toggle.impl.dev-1.1.8.jar)** è presente o meno. Se non è presente, [scarica il bundle dal collegamento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fcom.adobe.granite.toggle.impl.dev-1.1.8.jar).

![Attiva/Disattiva funzionalità](/help/forms/using/assets/feature-toggle-1.1.8.png)

## Abilitare il pulsante di attivazione/disattivazione della funzione {#enable-feature-toggle-65}

È possibile configurare gli interruttori delle funzionalità per i primi utenti o le nuove funzionalità tramite la **console Web AEM** seguendo la procedura riportata di seguito:

1. Accedi all’istanza di AEM Forms.
2. Accedi a `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Cercare **Adobe Granite Dynamic Toggle Provider** in Configuration Manager.
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
3. Cercare **Adobe Granite Dynamic Toggle Provider** in Configuration Manager.
4. Fai clic sull&#39;icona ![icona-matita](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. Nella sezione [!UICONTROL Attivazione/disattivazione] fare clic su ![icona a forma di matita](assets/aem6forms_add.png).
6. Aggiungi il numero di attivazione/disattivazione della funzione.
   ![Rimuovi](assets/remove_toggle_feature_forms.png)
7. Fai clic su Salva.

## Considerazioni tecniche

Gli interruttori delle funzioni sono specifici dell’ambiente e vengono gestiti in fase di runtime, pertanto non richiedono il riavvio del server. Tuttavia, alcune funzioni potrebbero richiedere l’aggiornamento delle pagine rilevanti o la cancellazione della cache per riflettere le modifiche.
È possibile accedere all&#39;elenco delle funzionalità abilitate tramite l&#39;interruttore delle funzionalità per l&#39;ambiente tramite `http://<author-instance-url>:4502/etc.clientlibs/toggles.json`.
