---
title: AEM Forms su gruppi OSGi e privilegi
seo-title: AEM Forms su gruppi OSGi e privilegi
description: Assegnazione di utenti ai gruppi per gestire AEM Forms su OSGi
seo-description: Assegnazione di utenti ai gruppi per gestire AEM Forms su OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# AEM Forms su gruppi OSGi e privilegi{#aem-forms-on-osgi-groups-and-privileges}

Potete [creare gruppi](/help/sites-administering/user-group-ac-admin.md#group-administration) e assegnare criteri e [utenti](/help/sites-administering/user-group-ac-admin.md#user-administration) ai gruppi in AEM. Tali criteri controllano i privilegi degli utenti che fanno parte del gruppo.

Dopo aver installato il pacchetto [aggiuntivo](../../forms/using/installing-configuring-aem-forms-osgi.md)AEM Forms, i gruppi menzionati in questo articolo, quali form-user e form-power-user, sono automaticamente disponibili per l&#39;assegnazione. Nella tabella seguente sono elencate le attività che un utente può eseguire per AEM Forms su OSGi in base alle assegnazioni dei gruppi:

<table>
 <tbody>
  <tr>
   <td>Gruppo</td> 
   <td>Attività</td> 
  </tr>
  <tr>
   <td>forms-user <sup><a href="#main-pars-text">[1]</a></sup></td> 
   <td>
    <ul> 
     <li>Creare, visualizzare in anteprima, pubblicare e inviare moduli adattivi</li> 
     <li>Creazione, anteprima e pubblicazione di comunicazioni interattive e frammenti di documento</li> 
     <li>Caricare le risorse in un’istanza di AEM</li> 
     <li>Creare temi</li> 
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
     <li>Creare temi</li> 
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
   <td>template-authors <sup><a href="#main-pars-text">[2]</a></sup></td> 
   <td>
    <ul> 
     <li>Creazione e anteprima di moduli adattivi o modelli di comunicazione interattiva</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-power-user</td> 
   <td>
    <ul> 
     <li>Creazione e anteprima di moduli adattivi o modelli di comunicazione interattiva</li> 
     <li>Creazione di script per moduli adattivi o modelli di comunicazione interattiva tramite l'editor di codice</li> 
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
     <li>Utilizzare le applicazioni<br /> inbox AEM <strong>Nota: Per accedere all’interfaccia utente di Interactive Communications Agent nella inbox di AEM, </strong>dovete disporre di un’assegnazione per i gruppi agente-utenti e utenti del flusso di lavoro.</li> 
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

1. L&#39;utente con privilegi di gruppo di moduli non può scrivere script per moduli adattivi.
1. L&#39;utente con privilegi di gruppo di autori di modelli non può scrivere script per i modelli.

