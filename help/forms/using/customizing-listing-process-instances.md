---
title: Personalizzazione dell’elenco delle istanze del processo
seo-title: Customizing the listing of process instances
description: Come personalizzare le proprietà visualizzate nell’istanza di processo nell’area di lavoro di AEM Forms.
seo-description: How-to customize the properties displayed in process instance in AEM Forms workspace.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# Personalizzazione dell’elenco delle istanze del processo {#customizing-the-listing-of-process-instances}

L’elenco delle istanze del processo viene visualizzato nella scheda Tracking dell’area di lavoro di AEM Forms.

Nell’elenco delle istanze di processo, per ogni istanza di processo, l’area di lavoro di AEM Forms mostra alcune proprietà di tale istanza. Le seguenti proprietà sono disponibili per ogni istanza di processo. Queste proprietà sono memorizzate come attributi nel modello di componente dell&#39;istanza di processo e sono disponibili per l&#39;uso nella relativa visualizzazione e nel relativo modello.

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
   <td>Nome dell'iniziatore dell'istanza del processo.</td>
  </tr>
  <tr>
   <td>iniziatorId</td>
   <td>ID dell'iniziatore dell'istanza del processo.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Timestamp al completamento del processo.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID dell'istanza del processo.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Iniziato<br /> 1 = In esecuzione<br /> 2 = Completa<br /> 3 = Completamento<br /> 4 = Terminato<br /> 5 = Terminazione<br /> 6 = Sospeso<br /> 7 = Sospensione<br /> 8 = Annulla sospensione</td>
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
   <td>Array di oggetti di variabili di processo. Ciascun oggetto variabile di processo contiene <strong>name</strong> (il nome della variabile di processo), <strong>value</strong> (valore della variabile di processo), e<strong> type</strong> (il tipo di variabile del processo).</td>
  </tr>
 </tbody>
</table>

**Esempio:**

Per visualizzare il `description` dell&#39;istanza di processo nella scheda dell&#39;istanza di processo, esegui i seguenti passaggi.

1. Segui [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Effettua le seguenti operazioni:

   1. Copia /libs/ws/js/runtime/templates/processinstance.html in/apps/ws/js/runtime/templates/, se non esiste. Fai clic su **Salva tutto**.
   1. Aggiungi div della descrizione del processo con classe = &#39;processDescription&#39; inprocessinstance.html.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Effettua le seguenti operazioni:

   1. Apri /apps/ws/js/registry.js per la modifica.
   1. Ricerca e sostituzione `text!/lc/libs/ws/js/runtime/templates/processinstance.html`con `text!/lc/`**app**/ws/js/runtime/templates/processinstance.html.

1. Le modifiche di cui sopra potrebbero richiedere un aggiornamento del file CSS aggiungendo una voce nel foglio di stile /apps/ws/css/newStyle.css nel modo seguente:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
