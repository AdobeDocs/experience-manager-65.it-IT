---
title: '[!DNL Experience Manager Assets] integrazione con [!DNL Adobe Workfront]'
description: Introduzione all'integrazione tra [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] integrazione con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | Questo articolo |
| AEM 6.4 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en) |

[!DNL Adobe Workfront] è un’applicazione per la gestione dell’intero ciclo di vita del lavoro, tutto in un’unica posizione. Integrazione tra [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] consente alle organizzazioni di migliorare la velocità dei contenuti e il time-to-market collegando intrinsecamente il lavoro e la gestione delle risorse digitali. Nel contesto della gestione del lavoro in Workfront, gli utenti possono accedere ai documenti e alle immagini richiesti.

La [!DNL Workfront for Experience Manager enhanced connector] consente processi aziendali avanzati con flussi di lavoro end-to-end e offre esperienze cliente end-to-end personalizzate e archiviazione centrale. Adobe offre un connettore standard e un connettore avanzato per integrare le due soluzioni. Vedi le funzioni supportate di seguito per un confronto e vedi [novità in [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] consente alla tua organizzazione di:

* Crea automaticamente cartelle di Experienci Manager collegate in Workfront e organizza le cartelle in base a Portfoli, programmi e progetti Workfront.
* Sincronizza i metadati del progetto Workfront con le cartelle di Experience Manager collegate.
* Experience Manager di aggiornamenti dei metadati con nuove versioni.
* Impostare gli stati degli oggetti di Workfront in base a condizioni configurabili tramite i flussi di lavoro Experience Manager.
* Pubblicare risorse nell’ambiente di pubblicazione Experience Manager o in Brand Portal.

Consulta il supporto per la piattaforma e [prerequisiti per il connettore avanzato](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* L&#39;Adobe richiede la distribuzione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono tale connettore ridondante; in questo caso, potrebbe essere richiesto ai clienti di effettuare la transizione dall’utilizzo di questo connettore.
>
>* Adobe supporta le versioni di connettore avanzate 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per controllare la versione del connettore avanzato, passa alla `digital.hoodoo` gruppo disponibile nel riquadro a sinistra in [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it).
>
>* Vedi [Esame di certificazione dei partner per Workfront per il connettore avanzato Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedi [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## Confrontare diverse integrazioni tra [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Di seguito sono riportati i dettagli delle funzionalità disponibili attraverso vari tipi di integrazioni tra [!DNL Assets] e [!DNL Workfront].

| Funzione obsoleta | Descrizione | [!DNL Workfront] e [!DNL Assets Essentials] | [!DNL Workfront] per [!DNL Experience Manager] connettore | [!DNL Workfront for Experience Manager enhanced connector] |
|----|----|----|------|-----|
| Metodi di distribuzione | Adeguata per la quale [!DNL Assets] offerta. | Assets Essentials | Cloud Service, Adobe Managed Services, on-premise | Cloud Service, Adobe Managed Services, on-premise |
| Invia file digitali da [!DNL Workfront] a [!DNL Assets] | È possibile caricare in AEM Assets l’ultima versione di un documento WF, che verrà collegata come nuova versione del documento. | ✓ | ✓ | ✓ |
| Collegamento manuale di cartelle AEM a oggetti Workfront | Le cartelle AEM esistenti possono essere collegate come cartella Workfront e le relative risorse secondarie sono collegate come nuovi documenti Workfront. | ✓ | ✓ | ✓ |
| Collegamento [!DNL Assets] a oggetti Workfront | Le risorse esistenti in AEM possono essere collegate a un nuovo documento Workfront o a una nuova versione di un documento esistente. | ✓ | ✓ | ✓ |
| Le risorse aggiunte alle cartelle collegate vengono inviate automaticamente a AEM | Se il documento viene aggiunto a una cartella collegata, la risorsa associata viene caricata automaticamente in AEM Assets come nuova risorsa. | ✓ | ✓ | ✓ |
| Scarica AEM Assets collegato da Workfront | Quando una risorsa è collegata in Workfront, l&#39;utente può scaricare i byte della risorsa. | ✓ | ✓ | ✓ |
| Ricerca di AEM Assets da Workfront | Il selettore AEM Assets in Workfront consente la ricerca full-text delle risorse. | ✓ | ✓ | ✓ |
| Visualizza e naviga AEM gerarchia cartelle da Workfront | Il selettore AEM Assets in Workfront consente di esplorare la gerarchia AEM Assets limitata dai controlli di accesso e dalle autorizzazioni associate dell’utente impostate in AEM. | ✓ | ✓ | ✓ |
| Scollegare risorse da AEM Assets in Workfront | Una risorsa collegata esistente da AEM può essere scollegata dal documento Workfront associato. La risorsa originale non viene eliminata all’interno di AEM. | ✓ | ✓ | ✓ |
| Aggiungere una risorsa di nuova versione ad AEM Assets da Workfront | Quando in un documento di Workfront viene aggiunta una nuova versione, un utente può inviare la nuova versione per AEM per sostituire la versione esistente. | ✓ | ✓ | ✓ |
| Risorse collegate in Workfront quando si fa clic su Utente diretto in AEM | Gli utenti vengono invitati a AEM di visualizzare in anteprima una risorsa collegata da Workfront. | ✓ | ✓ | Personalizzati |
| Crea automaticamente cartelle AEM collegate in Workfront | Crea automaticamente cartelle AEM collegate in Workfront utilizzando gli stati degli oggetti. Organizza automaticamente AEM cartelle in base a Portfoli, programmi e progetti Workfront. | No | No | ✓ |
| Sincronizzazione dei commenti | Sincronizza automaticamente i commenti delle risorse da [!DNL Workfront] a [!DNL Assets] | No | ✓ | ✓ |
| Mappatura dei metadati delle risorse Workfront su AEM Assets | Le proprietà dell’oggetto Workfront e del modulo personalizzato possono essere mappate AEM proprietà dei metadati delle risorse. I valori verranno inviati al caricamento/collegamento iniziale. | ✓ | ✓ | ✓ |
| Crea automaticamente un documento personalizzato Forms in Workfront | Allegare moduli personalizzati a documenti, attività e problemi di Workfront utilizzando i flussi di lavoro AEM. | No | Aggiungere manualmente il modulo personalizzato, quindi la sincronizzazione automatica funziona | ✓ |
| Aggiornamento automatico bidirezionale dei metadati tra AEM Assets e Workfront | Aggiorna automaticamente i metadati tra AEM Assets e Workfront. | No | ✓ | ✓ |
| Mappare metadati Workfront nelle cartelle AEM Assets | Sincronizza i metadati del progetto Workfront con le cartelle AEM collegate. | No | No | ✓ |
| Aggiornamenti AEM metadati con nuove versioni | È possibile effettuare una configurazione in AEM per determinare se una risorsa con nuove versioni in Workfront invia anche le modifiche apportate ai suoi metadati. | No | No | ✓ |
| Aggiorna automaticamente i metadati AEM in caso di modifiche a Forms personalizzato in Workfront | Workfront è configurato in modo che le proprietà specifiche AEM metadati delle risorse siano mappate su un modulo personalizzato del documento. Quando una risorsa viene inizialmente collegata o quando una risorsa viene aggiornata, i valori di queste proprietà dei metadati vengono copiati nel corrispondente campo del modulo personalizzato del documento Workfront. È necessario prestare attenzione a evitare che la modifica AEM venga rimandata a AEM come se si trattasse di una modifica originata in Workfront. | No | ✓ | ✓ |
| Creare una nuova versione di prova sulle risorse collegate | Al collegamento di una risorsa in Workfront è possibile generare automaticamente una bozza. | No | ✓ | Personalizzati |
| Imposta stato su oggetti Workfront | Impostare gli stati degli oggetti di Workfront in base a condizioni configurabili tramite flussi di lavoro AEM | No | No | ✓ |
| Pubblicare risorse in AEM Publish Environment o Brand Portal | Consenti agli utenti di Workfront di pubblicare automaticamente le risorse collegate in un ambiente di pubblicazione AEM o Brand Portal. | No | No | ✓ |
