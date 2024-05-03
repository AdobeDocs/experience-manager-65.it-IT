---
title: Personalizzazione dell'elenco delle istanze di processo
description: Come personalizzare le proprietà visualizzate nell’istanza del processo nell’area di lavoro di AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b27ffe92-8491-43a0-bf42-613eb39a606e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 3%

---

# Personalizzazione dell&#39;elenco delle istanze di processo {#customizing-the-listing-of-process-instances}

L’elenco delle istanze di processo viene visualizzato nella scheda Tracciamento dell’area di lavoro di AEM Forms.

Nell&#39;elenco delle istanze di processo, per ogni istanza di processo, l&#39;area di lavoro di AEM Forms mostra alcune proprietà dell&#39;istanza. Per ogni istanza di processo sono disponibili le seguenti proprietà. Queste proprietà vengono memorizzate come attributi nel modello di componente dell&#39;istanza di processo e sono disponibili per l&#39;uso nella vista e nella maschera.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>descrizione</td>
   <td>Descrizione dell'istanza del processo.</td>
  </tr>
  <tr>
   <td>iniziatore</td>
   <td>Nome dell'iniziatore dell'istanza del processo.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>ID dell'iniziatore dell'istanza del processo.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Timestamp del completamento del processo.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>ID dell’istanza del processo.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Avviato<br /> 1 = In esecuzione<br /> 2 = Completo<br /> 3 = Completamento<br /> 4 = Terminato<br /> 5 = Terminazione<br /> 6 = Sospeso<br /> 7 = Sospensione<br /> 8 = Annullamento sospensione</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nome del processo.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Timestamp dell’avvio del processo.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Array di oggetti delle variabili di processo. Ogni oggetto variabile di processo contiene <strong>nome</strong> (il nome della variabile di processo), <strong>valore</strong> (valore della variabile di processo), e<strong> tipo</strong> (il tipo di variabile di processo).</td>
  </tr>
 </tbody>
</table>

**Esempio:**

Per visualizzare `description` dell&#39;istanza del processo nella scheda dell&#39;istanza del processo, effettuare le seguenti operazioni.

1. Segui le [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Effettua le seguenti operazioni:

   1. Se non esiste, copia /libs/ws/js/runtime/templates/processinstance.html in/apps/ws/js/runtime/templates/. Clic **Salva tutto**.
   1. Aggiungi div descrizione processo con classe = &#39;processDescription&#39; inprocessinstance.html.

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Effettua le seguenti operazioni:

   1. Apri /apps/ws/js/registry.js per la modifica.
   1. Cerca e sostituisci `text!/lc/libs/ws/js/runtime/templates/processinstance.html`con `text!/lc/`**app**/ws/js/runtime/templates/processinstance.html.

1. Le modifiche di cui sopra possono richiedere un aggiornamento del file CSS aggiungendo una voce nel foglio di stile /apps/ws/css/newStyle.css nel modo seguente:

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement and user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
