---
title: ' AEM Forms su gruppi e privilegi OSGi'
seo-title: ' AEM Forms su gruppi e privilegi OSGi'
description: Assegnare gli utenti ai gruppi per gestire  AEM Forms su OSGi
seo-description: Assegnare gli utenti ai gruppi per gestire  AEM Forms su OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 494551d3d886c1ed70d252a28b03cfa9d8e82a6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


#  AEM Forms su OSGi Groups and Privileges{#aem-forms-on-osgi-groups-and-privileges}

È possibile [creare gruppi](/help/sites-administering/user-group-ac-admin.md#group-administration) e assegnare criteri e [utenti](/help/sites-administering/user-group-ac-admin.md#user-administration) ai gruppi in AEM. Tali criteri controllano i privilegi degli utenti che fanno parte del gruppo.

Dopo aver installato [ pacchetto aggiuntivo AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), i gruppi menzionati in questo articolo, quali form-users e form-power-user, sono automaticamente disponibili per l&#39;assegnazione. Nella tabella seguente sono elencate le attività che un utente può eseguire per  AEM Forms in OSGi in base alle assegnazioni del gruppo:

<table>
 <tbody>
  <tr>
   <td>Gruppo</td> 
   <td>Attività</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Creare, visualizzare in anteprima, pubblicare e inviare moduli adattivi</li> 
     <li>Creazione, anteprima e pubblicazione di comunicazioni interattive e frammenti di documento</li> 
     <li>Caricare le risorse in un’istanza AEM</li> 
     <li>Creazione di temi</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>form-power-user</td> 
   <td>
    <ul> 
     <li>Creare, visualizzare in anteprima, pubblicare e inviare moduli adattivi</li> 
     <li>Creazione, anteprima e pubblicazione di comunicazioni interattive e frammenti di documento</li> 
     <li>Creazione di script per i moduli adattivi tramite l'editor di codice</li> 
     <li>Caricare le risorse inclusi gli script</li> 
     <li>Creazione di temi</li> 
     <li>Importa pacchetti contenenti XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>form-submit-reviewers</td> 
   <td>
    <ul> 
     <li>Esaminare i contributi</li> 
     <li>Approvare o rifiutare gli invii</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Creazione e anteprima di moduli adattivi o modelli di comunicazione interattiva</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>Creazione e modifica di un modello dati modulo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Accedere a lettere di gestione della corrispondenza o a comunicazioni interattive mediante l'interfaccia utente dell'agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>editor di workflow</p> </td> 
   <td>
    <ul> 
     <li>Creare un’applicazione in entrata</li> 
     <li>Creare un modello di workflow</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>Utilizzate AEM applicazioni inbox<br /> <strong>Nota: </strong>Per accedere all'interfaccia utente di Interactive Communications Agent in AEM inbox, è necessario disporre di assegnazioni di gruppi di utenti e utenti con agente di gestione di cm-agent.</li> 
     <li>Gestione delle istanze del flusso di lavoro</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>Configura PDF Generator</li> 
     <li>Configura cartella esaminata</li> 
     <li>Gestione delle applicazioni di workflow</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. L&#39;utente con privilegi di gruppo di utenti modulo non è in grado di scrivere script per i moduli adattivi.
1. L&#39;utente con privilegi di gruppo di autori di modelli non può scrivere script per i modelli.

