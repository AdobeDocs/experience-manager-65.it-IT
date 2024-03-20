---
title: Prerequisiti per l’integrazione con Adobe Target
description: Scopri i prerequisiti per l’integrazione con Adobe Target.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 30813c44-51ac-4e6e-8ee6-4e8baacb1ff9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 7%

---

# Prerequisiti per l’integrazione con Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Nell&#39;ambito del [Integrazione di AEM e Adobe Target](/help/sites-administering/target.md), è necessario registrarsi ad Adobe Target, configurare l’agente di replica e proteggere le impostazioni delle attività sul nodo di pubblicazione.

## Registrazione ad Adobe Target {#registering-with-adobe-target}

Per integrare l’AEM con Adobe Target, devi disporre di un account Adobe Target valido. Questo account deve avere **approvatore** livello di autorizzazioni minimo. Quando ti registri a Adobe Target, ricevi un codice cliente. Per collegare l’AEM ad Adobe Target sono necessari il codice cliente e il nome di accesso e la password di Adobe Target.

Il codice client identifica l’account cliente Adobe Target quando si chiama il server Adobe Target.

>[!NOTE]
>
>Per utilizzare l’integrazione, il team di Target deve anche abilitare il tuo account.
>
>In caso contrario, contattare [Assistenza clienti Adobe](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html).

## Abilitazione dell’agente di replica di Target {#enabling-the-target-replication-agent}

Test e Target [agente di replica](/help/sites-deploying/replication.md) deve essere abilitato sull’istanza di authoring. Tieni presente che questo agente di replica non è abilitato per impostazione predefinita se hai utilizzato [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) modalità di esecuzione per l’installazione dell’AEM. Per ulteriori informazioni sulla protezione dell&#39;ambiente di produzione, vedi [Elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md).

1. Nella home page dell’AEM, fai clic su **Strumenti** > **Distribuzione** > **Replica**.
1. Clic **Agenti per creazione**.
1. Fai clic su **Test e Target (test e target)** agente di replica, quindi fare clic su **Modifica**.
1. Seleziona l’opzione Abilitato, quindi fai clic su **OK**.

   >[!NOTE]
   >
   >Quando configuri l’agente di replica di Test and Target, nel **Trasporto** , l&#39;URI è impostato per impostazione predefinita su **tnt:///**. Non sostituire questo URI con **https://admin.testandtarget.omniture.com**.
   >
   >Se tenti di verificare la connessione con **tnt:///**, genera un errore. Questo comportamento è previsto perché questo URI è solo per uso interno; non utilizzare con **Verifica connessione**.

## Protezione del nodo Impostazioni attività {#securing-the-activity-settings-node}

Proteggere il nodo delle impostazioni delle attività **cq:ActivitySettings** sull’istanza di pubblicazione, in modo che non sia accessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.

Il **cq:ActivitySettings** è disponibile in CRXDE lite sotto `/content/campaigns/*nameofbrand*`* *nel nodo attività jcr:content;* *ad esempio, `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Questo nodo viene creato solo dopo aver eseguito il targeting di un componente.

Il **cq:ActivitySettings** sotto il jcr:content dell’attività è protetto dai seguenti ACL:

* Nega tutto per tutti
* Consenti jcr:read,rep:write per &quot;target-activity-authors&quot; (l&#39;autore è un membro di questo gruppo preconfigurato)
* Consenti jcr:read,rep:write per &quot;targetservice&quot;

Queste impostazioni garantiscono che gli utenti normali non abbiano accesso alle proprietà del nodo. Utilizza gli stessi ACL per l’authoring e per la pubblicazione. Consulta [Amministrazione utenti e sicurezza](/help/sites-administering/security.md) per ulteriori informazioni.

## Configurazione di AEM Link Externalizer {#configuring-the-aem-link-externalizer}

Quando modifichi un’attività in Adobe Target, l’URL punta a **localhost** a meno che tu non modifichi l’URL nel nodo di authoring dell’AEM. Puoi configurare AEM Link Externalizer se desideri che il contenuto esportato punti a uno specifico *pubblicare* dominio.

>[!NOTE]
>
>Vedi anche [Aggiungere la configurazione cloud](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Per configurare l’esternalizzatore AEM:

>[!NOTE]
>
>Per ulteriori dettagli vedi [Esternalizzazione degli URL](/help/sites-developing/externalizer.md).

1. Passa alla console web OSGi all’indirizzo **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Trova **Day CQ Link Externalizer** e immetti il dominio per il nodo di authoring.

   ![Day CQ Link Externalizer](assets/aem-externalizer-01.png)
