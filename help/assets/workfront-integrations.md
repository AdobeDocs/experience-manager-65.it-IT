---
title: '[!DNL Experience Manager Assets] integration with [!DNL Adobe Workfront]'
description: Introduzione all'integrazione tra [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
source-git-commit: 468a8d96153c67232524eea6f180c9ceb364d60a
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager Assets] integrazione con [!DNL Adobe Workfront] {#assets-integration-overview}

[!DNL Adobe Workfront] è un&#39;applicazione di gestione del lavoro che consente di gestire l&#39;intero ciclo di vita del lavoro in un&#39;unica posizione. Integrazione tra [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] consente alle organizzazioni di migliorare la velocità dei contenuti e il time-to-market collegando intrinsecamente il lavoro e la gestione delle risorse digitali. Nel contesto della gestione del lavoro in Workfront, gli utenti possono accedere ai documenti e alle immagini richiesti.

Adobe offre due connettori diversi per integrare entrambe le soluzioni. I connettori consentono l&#39;automazione, la configurazione e i flussi di lavoro estensibili complessi tra [!DNL Assets] e [!DNL Workfront]. Inoltre, [!DNL Assets Essentials] è disponibile come componente aggiuntivo per il nuovo [!DNL Workfront] i clienti possono acquistare separatamente. Per ulteriori informazioni, consulta [[!DNL Workfront] and [!DNL Assets Essentials] integrazione](https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/integration.html).

[!DNL Workfront for Experience Manage enhanced connector] consente alla tua organizzazione di:

* Collaborate facilmente. I team creativi possono preoccuparsi di una cosa in meno. Ora, al termine del lavoro, possono inviarlo ad AEM Assets con un clic
* Arricchisci le risorse in ogni passaggio. Raccogliere nuovi dati in ogni fase del ciclo di vita delle risorse. Da un’ideazione all’altra, la tua organizzazione può acquisire metriche chiave per prendere decisioni aziendali più informate sullo sviluppo futuro delle risorse.
* Fai riferimento alle risorse esistenti. È possibile trovare e riutilizzare facilmente le risorse esistenti in produzione e aggiungerle a nuovi progetti come elementi di riferimento.
* Sincronizza tutti i tuoi metadati. Migliora i metadati rendendoli il più semplice possibile da aggiungere. Con il connettore, i metadati vengono sincronizzati bidirezionalmente tra Workfront e AEM Assets
* Sfruttamento [!DNL Experience Manager Assets] funzionalità di gestione digitale. Accesso a tutte le risorse digitali direttamente all’interno dei tuoi preferiti [!DNL Creative Cloud] applicazioni. Assegnazione tag avanzati e ritaglio abilitati per l’intelligenza artificiale, strumenti di ricerca, distribuzione dinamica tramite [!DNL Dynamic Media]e molto di più.

Consulta il supporto per la piattaforma e altri [prerequisiti per il connettore avanzato](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>L&#39;Adobe richiede la distribuzione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rende tale connettore ridondante; in questo caso, potrebbe essere richiesto ai clienti di effettuare la transizione dall’utilizzo di questo connettore.

## Confrontare diverse integrazioni tra [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Di seguito sono riportati i dettagli delle funzionalità disponibili attraverso vari tipi di integrazioni tra [!DNL Assets] e [!DNL Workfront].

| Funzione obsoleta | Descrizione | [!DNL Workfront] e [!DNL Assets Essentials] | [!DNL Workfront] per [!DNL Experience Manager] connettore | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| Metodi di distribuzione | Adeguata per la quale [!DNL Assets] offerta. | Assets Essentials | Cloud Service, Adobe Managed Services, on-premise | Cloud Service, Adobe Managed Services, on-premise |
| Invia file digitali da [!DNL Workfront] a [!DNL Assets] | È possibile caricare in AEM Assets l’ultima versione di un documento WF, che verrà collegata come nuova versione del documento. | . | . | . |
| Collegamento manuale di cartelle AEM a oggetti Workfront | Le cartelle AEM esistenti possono essere collegate come cartella Workfront e le relative risorse secondarie sono collegate come nuovi documenti Workfront. | . | . | . |
| Collegamento [!DNL Assets] a oggetti Workfront | Le risorse esistenti in AEM possono essere collegate a un nuovo documento Workfront o a una nuova versione di un documento esistente. | . | . | . |
| Le risorse aggiunte alle cartelle collegate vengono inviate automaticamente a AEM | Se il documento viene aggiunto a una cartella collegata, la risorsa associata viene caricata automaticamente in AEM Assets come nuova risorsa. | . | . | . |
| Scarica AEM Assets collegato da Workfront | Quando una risorsa è collegata in Workfront, l&#39;utente può scaricare i byte della risorsa. | . | . | . |
| Ricerca di AEM Assets da Workfront | Il selettore AEM Assets in Workfront consente la ricerca full-text delle risorse. | . | . | . |
| Visualizza e naviga AEM gerarchia cartelle da Workfront | Il selettore AEM Assets in Workfront consente di esplorare la gerarchia AEM Assets limitata dai controlli di accesso e dalle autorizzazioni associate dell’utente impostate in AEM. | . | . | . |
| Scollegare risorse da AEM Assets in Workfront | Una risorsa collegata esistente da AEM può essere scollegata dal documento Workfront associato. La risorsa originale non viene eliminata all’interno di AEM. | . | . | . |
| Aggiungere una risorsa di nuova versione ad AEM Assets da Workfront | Quando in un documento di Workfront viene aggiunta una nuova versione, un utente può inviare la nuova versione per AEM per sostituire la versione esistente. | . | . | . |
| Risorse collegate in Workfront quando si fa clic su Utente diretto in AEM | Gli utenti vengono invitati a AEM di visualizzare in anteprima una risorsa collegata da Workfront. | . | . | Personalizzata |
| Crea automaticamente cartelle AEM collegate in Workfront | Crea automaticamente cartelle AEM collegate in Workfront utilizzando gli stati degli oggetti. Organizza automaticamente AEM cartelle in base a Portfoli, programmi e progetti Workfront. | No | No | . |
| Sincronizzazione dei commenti | Sincronizza automaticamente i commenti delle risorse da [!DNL Workfront] a [!DNL Assets] | No | . | . |
| Mappatura dei metadati delle risorse Workfront su AEM Assets | Le proprietà dell’oggetto Workfront e del modulo personalizzato possono essere mappate AEM proprietà dei metadati delle risorse. I valori verranno inviati al caricamento/collegamento iniziale. | . | . | . |
| Crea automaticamente un documento personalizzato Forms in Workfront | Allegare moduli personalizzati a documenti, attività e problemi di Workfront utilizzando i flussi di lavoro AEM. | No | Aggiungere manualmente il modulo personalizzato, quindi la sincronizzazione automatica funziona | . |
| Aggiornamento automatico bidirezionale dei metadati tra AEM Assets e Workfront | Aggiorna automaticamente i metadati tra AEM Assets e Workfront. | No | . | . |
| Mappare metadati Workfront nelle cartelle AEM Assets | Sincronizza i metadati del progetto Workfront con le cartelle AEM collegate. | No | No | . |
| Aggiornamenti AEM metadati con nuove versioni | È possibile effettuare una configurazione in AEM per determinare se una risorsa con nuove versioni in Workfront invia anche le modifiche apportate ai suoi metadati. | No | No | . |
| Aggiorna automaticamente i metadati AEM in caso di modifiche a Forms personalizzato in Workfront | Workfront è configurato in modo che le proprietà specifiche AEM metadati delle risorse siano mappate su un modulo personalizzato del documento. Quando una risorsa viene inizialmente collegata o quando una risorsa viene aggiornata, i valori di queste proprietà dei metadati vengono copiati nel corrispondente campo del modulo personalizzato del documento Workfront. È necessario prestare attenzione a evitare che la modifica AEM venga rimandata a AEM come se si trattasse di una modifica originata in Workfront. | No | . | . |
| Creare una nuova versione di prova sulle risorse collegate | Al collegamento di una risorsa in Workfront è possibile generare automaticamente una bozza. | No | . | Personalizzata |
| Imposta stato su oggetti Workfront | Impostare gli stati degli oggetti di Workfront in base a condizioni configurabili tramite flussi di lavoro AEM | No | No | . |
| Pubblicare risorse in AEM Publish Environment o Brand Portal | Consenti agli utenti di Workfront di pubblicare automaticamente le risorse collegate in un ambiente di pubblicazione AEM o Brand Portal. | No | No | . |
