---
title: Gestione della corrispondenza| Gestione dei dati utente
seo-title: Gestione della corrispondenza| Gestione dei dati utente
description: 'null'
seo-description: 'null'
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gestione della corrispondenza| Gestione dei dati utente {#correspondence-management-handling-user-data}

AEM Forms Correspondence Management consente di creare, gestire e semplificare le corrispondenze dei clienti sicure e personalizzate. Offre agli utenti aziendali un&#39;interfaccia utente intuitiva per creare le corrispondenze utilizzando blocchi di contenuto e elementi multimediali già approvati. Per ulteriori informazioni sulla creazione delle corrispondenze, consultate [Creare corrispondenza](/help/forms/using/create-correspondence.md).

Quando un utente aziendale o un agente salva una corrispondenza come bozza o la invia, viene salvata un’istanza di lettera nell’archivio di AEM. L’istanza letter include i dati e i metadati della corrispondenza.

>[!NOTE]
>
>In AEM 6.5 Forms, la gestione della corrispondenza non è disponibile. Se state effettuando l&#39;aggiornamento da una versione precedente di AEM Forms, installate il pacchetto di compatibilità ed effettuate la migrazione delle risorse per la gestione della corrispondenza per continuare a utilizzarle in AEM 6.5 Forms. Per ulteriori informazioni, consultate [Pacchetto](/help/forms/using/compatibility-package.md)Compatibilità.

## Archivio dati utente e data {#data}

La gestione della corrispondenza memorizza i dati per le bozze e le lettere inviate nell’archivio AEM solo se l’istanza di pubblicazione è configurata per gestire le istanze di lettere. Per ulteriori informazioni sulla configurazione, consultate Proprietà [di configurazione di](/help/forms/using/cm-configuration-properties.md)Correspondence Management.

A seconda della persistenza dell’archivio dati configurata per la distribuzione AEM, le bozze e i dati di corrispondenza inviati vengono memorizzati nelle seguenti posizioni.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo di persistenza</strong></p> </td>
   <td><p><strong>Archivio dati</strong></p> </td>
   <td><p><strong>Dove si trova</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predefiniti</p> </td>
   <td><p>Archivio AEM delle istanze di pubblicazione e di creazione specificate nella configurazione di replica inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Archivio AEM dell’istanza di creazione dell’elaborazione remota</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

Nel percorso dell’archivio AEM sopra specificato:

* `[yyyy]/[mm]/[dd]` è la struttura del nodo in base alla data di creazione dell&#39;istanza della lettera
* `[node-id]` è l’ID assegnato alla cartella contenente la lettera
* `[letter-instance-name]` è il nome specificato al momento del salvataggio o dell&#39;invio di una lettera

Sotto il nodo [letter-instance-name] , viene creata la seguente struttura di nodi e i dati per ogni istanza letter vengono memorizzati nell’archivio AEM:

| Node | Descrizione |
|---|---|
| `extendedProperties` | Memorizza le proprietà dei metadati dell&#39;istanza della lettera. |
| `dataXML` | Memorizza un file dataXML scaricabile contenente i dati di corrispondenza in formato binario. |
| `processedXDP` | Include i dettagli del modello XDP utilizzato per creare la lettera inviata. Questo nodo viene creato solo per le corrispondenze inviate. |
| `submittedLetter` | Memorizza i dati della lettera inviati in formato binario scaricabile. Questo nodo viene creato solo per le corrispondenze inviate. |

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

È possibile accedere ai dati della corrispondenza bozza e inviata negli archivi dati configurati e, se necessario, eliminarli.

### Accesso ai dati utente {#access-user-data}

La gestione della corrispondenza fornisce API che potete utilizzare per trovare e accedere alle istanze di bozza e lettera inviata. Utilizzando le API, potete trovare e aprire le istanze di lettere utilizzando l&#39;ID istanza lettera o l&#39;utente che ha salvato o inviato la corrispondenza. Per ulteriori informazioni, consultate [API per accedere alle istanze](/help/forms/using/cm-apis-to-access-letter-instances.md)di lettere.

In alternativa, puoi passare all’istanza della lettera nell’archivio AEM utilizzando CRX DELite. Per informazioni sui dati archiviati e sulla posizione dell&#39;archivio, vedere Archivio [](/help/forms/using/correspondence-management-handling-user-data.md#data) dati e archivi dati.

### Eliminare i dati utente {#delete-user-data}

Per trovare un&#39;istanza della lettera contenente i dati di un utente specifico, è possibile:

* Utilizzare le API di gestione della corrispondenza se il nome dell&#39;istanza della lettera o l&#39;utente che ha salvato la bozza o ha inviato la corrispondenza è noto
* Utilizza la ricerca nell’archivio AEM utilizzando informazioni personali come l’ID e-mail o il nome per trovare il nodo in cui sono memorizzate le informazioni

Per eliminare completamente i dati utente dalle corrispondenze bozza e inviate dai sistemi AEM, devi eliminare manualmente il nodo dell’istanza della lettera da tutte le istanze AEM applicabili.
