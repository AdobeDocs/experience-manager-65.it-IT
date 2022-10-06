---
title: AEM Forms su gruppi e privilegi OSGi
seo-title: AEM Forms on OSGi Groups and Privileges
description: Assegnare gli utenti ai gruppi per gestire AEM Forms su OSGi
seo-description: Assign users to the groups to manage AEM Forms on OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
role: Admin
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# AEM Forms su gruppi e privilegi OSGi{#aem-forms-on-osgi-groups-and-privileges}

È possibile [creare gruppi](/help/sites-administering/user-group-ac-admin.md#group-administration) e assegna politiche e [utenti](/help/sites-administering/user-group-ac-admin.md#user-administration) ai gruppi in AEM. Questi criteri controllano i privilegi degli utenti che fanno parte del gruppo.

Una volta installata [Pacchetto aggiuntivo di AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), i gruppi menzionati in questo articolo, ad esempio gli utenti di moduli e gli utenti di moduli-power, sono automaticamente disponibili per l&#39;assegnazione. Nella tabella seguente sono elencate le attività che un utente può eseguire per AEM Forms su OSGi in base alle assegnazioni dei gruppi:

<table>
 <tbody>
  <tr>
   <td>Gruppo</td> 
   <td>Attività</td> 
  </tr>
  <tr>
   <td>utenti dei moduli <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Creare, visualizzare in anteprima, pubblicare e inviare moduli adattivi</li> 
     <li>Creazione, visualizzazione in anteprima e pubblicazione di comunicazioni interattive e frammenti di documento</li> 
     <li>Caricare le risorse in un’istanza AEM</li> 
     <li>Creare temi</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>utenti di moduli</td> 
   <td>
    <ul> 
     <li>Creare, visualizzare in anteprima, pubblicare e inviare moduli adattivi</li> 
     <li>Creazione, visualizzazione in anteprima e pubblicazione di comunicazioni interattive e frammenti di documento</li> 
     <li>Creazione di script per i moduli adattivi tramite l’editor di codice</li> 
     <li>Caricare le risorse inclusi gli script</li> 
     <li>Creare temi</li> 
     <li>Importa pacchetti contenenti XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>moduli-sottomissione-revisori</td> 
   <td>
    <ul> 
     <li>Recensione dei documenti</li> 
     <li>Approvare o rifiutare gli invii</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>autori di modelli <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Creare e visualizzare in anteprima moduli adattivi o modelli di comunicazione interattivi</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>Creare e modificare un modello di dati modulo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Accedere alle lettere di gestione della corrispondenza o alle comunicazioni interattive tramite l’interfaccia utente dell’agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>editor di workflow</p> </td> 
   <td>
    <ul> 
     <li>Creare un’applicazione inbox</li> 
     <li>Creare un modello di flusso di lavoro</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>utenti del flusso di lavoro</td> 
   <td>
    <ul> 
     <li>Utilizzare le applicazioni di posta in AEM<br /> <strong>Nota: </strong>Per accedere all’interfaccia utente di Interactive Communications Agent nella casella in entrata è necessario disporre di assegnazioni di gruppi di utenti e utenti di un agente cm-agent e di un gruppo di utenti del flusso di lavoro.</li> 
     <li>Gestire le istanze del flusso di lavoro</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>amministratori di file</td> 
   <td>
    <ul> 
     <li>Configura PDF Generator</li> 
     <li>Configura cartella di controllo</li> 
     <li>Gestione delle applicazioni del flusso di lavoro</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. L’utente con privilegi di gruppo per gli utenti di moduli non può scrivere script per i moduli adattivi.
1. L&#39;utente con privilegi di gruppo di autori modelli non può scrivere script per i modelli.
