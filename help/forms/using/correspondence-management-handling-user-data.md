---
title: Gestione della corrispondenza | Gestione dei dati utente
seo-title: Correspondence Management | Handling user data
description: Gestione della corrispondenza | Gestione dei dati utente
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Gestione della corrispondenza | Gestione dei dati utente {#correspondence-management-handling-user-data}

Gestione della corrispondenza di AEM Forms consente di creare, gestire e semplificare corrispondenze cliente sicure e personalizzate. Offre agli utenti aziendali un’interfaccia utente intuitiva per creare corrispondenze utilizzando blocchi di contenuto e elementi multimediali pre-approvati. Per ulteriori informazioni sulla creazione delle corrispondenze, vedi [Crea corrispondenza](/help/forms/using/create-correspondence.md).

Quando un utente aziendale o un agente salva una corrispondenza come bozza o la invia, un&#39;istanza di lettera viene salvata nell&#39;archivio AEM. L&#39;istanza della lettera include i dati e i metadati della corrispondenza.

>[!NOTE]
>
>AEM 6.5 Forms, la gestione della corrispondenza non è disponibile. Se stai effettuando l’aggiornamento da una versione precedente di AEM Forms, installa il pacchetto di compatibilità ed esegui la migrazione delle risorse di gestione della corrispondenza per continuare a utilizzarle in Forms 6.5 AEM. Per ulteriori informazioni, consulta [Pacchetto di compatibilità](/help/forms/using/compatibility-package.md).

## Archiviazione dati e dati utente {#data}

La gestione della corrispondenza memorizza i dati per le bozze e le lettere inviate AEM archivio solo se l’istanza di pubblicazione è configurata per gestire le istanze di lettere. Per ulteriori informazioni sulla configurazione, vedi [Proprietà di configurazione della gestione della corrispondenza](/help/forms/using/cm-configuration-properties.md).

A seconda della persistenza dell’archivio dati configurata per la distribuzione AEM, le bozze e i dati di corrispondenza inviati vengono memorizzati nelle posizioni seguenti.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo di persistenza</strong></p> </td>
   <td><p><strong>Archiviazione dati</strong></p> </td>
   <td><p><strong>Dove si trova</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predefiniti</p> </td>
   <td><p>AEM archivio dell'istanza di pubblicazione e delle istanze di authoring specificate nella configurazione di replica inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Archivio AEM dell’istanza dell’autore dell’elaborazione remota</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

Nel percorso AEM repository specificato sopra:

* `[yyyy]/[mm]/[dd]` è la struttura del nodo in base alla data di creazione dell&#39;istanza della lettera
* `[node-id]` è l&#39;ID assegnato alla cartella contenente la lettera
* `[letter-instance-name]` è il nome specificato al momento del salvataggio o dell&#39;invio di una lettera

Sotto la [letter-instance-name] nodo, viene creata la seguente struttura del nodo e i dati per ogni istanza di lettera vengono memorizzati nell&#39;archivio AEM:

| Nodo | Descrizione |
|---|---|
| `extendedProperties` | Memorizza le proprietà dei metadati dell&#39;istanza della lettera. |
| `dataXML` | Memorizza un file dataXML scaricabile contenente i dati di corrispondenza in formato binario. |
| `processedXDP` | Include i dettagli del modello XDP utilizzato per creare la lettera inviata. Questo nodo viene creato solo per le corrispondenze inviate. |
| `submittedLetter` | Memorizza i dati della lettera inviati in formato binario scaricabile. Questo nodo viene creato solo per le corrispondenze inviate. |

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

È possibile accedere ai dati della bozza e della corrispondenza inviati negli archivi dati configurati e, se necessario, eliminarli.

### Accedere ai dati utente {#access-user-data}

La gestione della corrispondenza fornisce API che è possibile utilizzare per trovare e accedere alle istanze di lettere bozze e inviate. Utilizzando le API, puoi trovare e aprire le istanze di lettere utilizzando l’ID istanza lettera o l’utente che ha salvato o inviato la corrispondenza. Per ulteriori informazioni, consulta [API per accedere alle istanze di lettere](/help/forms/using/cm-apis-to-access-letter-instances.md).

In alternativa, puoi passare all&#39;istanza della lettera in AEM archivio utilizzando CRX DELite. Vedi [Archiviazione dati e dati utente](/help/forms/using/correspondence-management-handling-user-data.md#data) per informazioni sui dati archiviati e sulla posizione del repository.

### Eliminare i dati utente {#delete-user-data}

Per trovare un&#39;istanza di lettera contenente i dati di un utente specifico, puoi:

* Utilizza le API di gestione della corrispondenza se è noto il nome dell&#39;istanza di lettera o l&#39;utente che ha salvato la bozza o ha inviato la corrispondenza
* Utilizza AEM ricerca archivio utilizzando informazioni personali identificabili come l’ID e-mail o il nome per trovare il nodo in cui sono memorizzate le informazioni

Per eliminare completamente i dati utente dalla bozza e dalle corrispondenze inviate dai sistemi AEM, è necessario eliminare manualmente il nodo di istanza della lettera da tutte le istanze AEM applicabili.
