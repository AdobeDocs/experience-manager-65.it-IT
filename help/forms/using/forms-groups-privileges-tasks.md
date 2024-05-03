---
title: AEM Forms su gruppi e privilegi OSGi
description: Assegnare utenti a gruppi per gestire Adobe Experience Manager (AEM) Forms su OSGi
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 6%

---

# AEM Forms su gruppi e privilegi OSGi{#aem-forms-on-osgi-groups-and-privileges}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html) |
| AEM 6.5 | Questo articolo |

È possibile [creare gruppi](/help/sites-administering/user-group-ac-admin.md#group-administration) e assegnare criteri e [utenti](/help/sites-administering/user-group-ac-admin.md#user-administration) ai gruppi in Adobe Experience Manager (AEM). Questi criteri controllano i privilegi degli utenti che fanno parte del gruppo.

Dopo aver installato [Pacchetto del componente aggiuntivo AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), i gruppi menzionati in questo articolo, ad esempio utenti di forms e utenti avanzati di forms, sono automaticamente disponibili per l&#39;assegnazione. Nella tabella seguente sono elencate le attività che un utente può eseguire per AEM Forms su OSGi in base alle assegnazioni del gruppo:

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
     <li>Creare, visualizzare in anteprima e pubblicare comunicazioni interattive e frammenti di documenti</li> 
     <li>Caricare risorse in un’istanza AEM</li> 
     <li>Creare temi</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>Creare, visualizzare in anteprima, pubblicare e inviare moduli adattivi</li> 
     <li>Creare, visualizzare in anteprima e pubblicare comunicazioni interattive e frammenti di documenti</li> 
     <li>Creare script per i moduli adattivi utilizzando un editor di codice</li> 
     <li>Caricare risorse, inclusi script</li> 
     <li>Creare temi</li> 
     <li>Importare pacchetti contenenti XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submit-reviewers</td> 
   <td>
    <ul> 
     <li>Rivedi gli invii</li> 
     <li>Approvare o rifiutare gli invii</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
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
     <li>Accedere a lettere o comunicazioni interattive di Gestione corrispondenza tramite l'interfaccia utente agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editor</p> </td> 
   <td>
    <ul> 
     <li>Creare un’applicazione casella in entrata</li> 
     <li>Creare un modello di flusso di lavoro</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>Utilizzare le applicazioni casella in entrata AEM<br /> <strong>Nota: </strong>Per accedere all’interfaccia utente di Interactive Communications Agent nella casella in entrata AEM, è necessario disporre delle assegnazioni di gruppi cm-agent-users e workflow-users.</li> 
     <li>Gestire le istanze del flusso di lavoro</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>amministratori fd</td> 
   <td>
    <ul> 
     <li>Configura PDF Generator</li> 
     <li>Configurare la cartella controllata</li> 
     <li>Gestire le applicazioni del flusso di lavoro</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. L’utente con privilegi di gruppo forms-users non può scrivere script per i moduli adattivi.
1. L’utente con privilegi di gruppo per autori di modelli non può scrivere script per i modelli.
