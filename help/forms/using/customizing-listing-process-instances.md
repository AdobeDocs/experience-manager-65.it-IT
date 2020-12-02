---
title: Personalizzazione dell'elenco delle istanze del processo
seo-title: Personalizzazione dell'elenco delle istanze del processo
description: Come personalizzare le proprietà visualizzate nell’istanza di processo ’area di lavoro di AEM Forms.
seo-description: Come personalizzare le proprietà visualizzate nell’istanza di processo ’area di lavoro di AEM Forms.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# Personalizzazione dell&#39;elenco delle istanze di processo {#customizing-the-listing-of-process-instances}

L&#39;elenco delle istanze di processo viene visualizzato nella scheda Tracciamento &#39;area di lavoro AEM Forms.

Nell’elenco delle istanze di processo, per ogni istanza di processo,  area di lavoro di AEM Forms mostra alcune proprietà di tale istanza. Le seguenti proprietà sono disponibili per ogni istanza di processo. Queste proprietà sono memorizzate come attributi nel modello di componenti dell’istanza di processo e sono disponibili per l’uso nella relativa vista e nel modello.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>descrizione</td>
   <td>Descrizione dell’istanza di processo.</td>
  </tr>
  <tr>
   <td>iniziatore</td>
   <td>Nome dell'iniziatore dell'istanza di processo.</td>
  </tr>
  <tr>
   <td>iniziatorId</td>
   <td>ID dell’iniziatore dell’istanza di processo.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Timestamp al completamento del processo.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID dell’istanza di processo.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Iniziato<br /> 1 = In esecuzione<br /> 2 = Completato<br /> 3 = Completato<br /> 4 = Terminato<br /> 5 = Terminante<br /> 6 = Sospeso<br /> 7 = Sospeso<br /> 8 = Non sospeso</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nome del processo.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Timestamp all'avvio del processo.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Array di oggetti di variabili di processo. Ogni oggetto variabile di processo contiene <strong>name</strong> (il nome della variabile di processo), <strong>value</strong> (valore della variabile di processo) e<strong> type</strong> (il tipo di variabile di processo).</td>
  </tr>
 </tbody>
</table>

**Esempio:**

Per visualizzare la proprietà `description` dell&#39;istanza di processo nella scheda dell&#39;istanza di processo, eseguire le operazioni seguenti.

1. Seguite i passaggi [Generici per  personalizzazione dell&#39;area di lavoro AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Effettua le seguenti operazioni:

   1. Copiate /libs/ws/js/runtime/templates/processinstance.htmlà/apps/ws/js/runtime/templates/, se non esiste. Fare clic su **Salva tutto**.
   1. Aggiungete div della descrizione del processo con classe = &#39;processDescription&#39; inprocessinstance.html.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Effettua le seguenti operazioni:

   1. Aprite /apps/ws/js/registry.js per la modifica.
   1. Cerca e sostituisci `text!/lc/libs/ws/js/runtime/templates/processinstance.html`con `text!/lc/`**app**/ws/js/runtime/templates/processinstance.html.

1. Le modifiche di cui sopra potrebbero richiedere un aggiornamento del file CSS aggiungendo una voce nel foglio di stile /apps/ws/css/newStyle.css nel modo seguente:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
