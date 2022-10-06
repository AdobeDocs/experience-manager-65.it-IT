---
title: Portale Forms | Gestione dei dati utente
seo-title: Forms Portal | Handling user data
description: Portale Forms | Gestione dei dati utente
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Portale Forms | Gestione dei dati utente {#forms-portal-handling-user-data}

[!DNL AEM Forms] Portal fornisce componenti utilizzabili per elencare moduli adattivi, moduli HTML5 e altre risorse Forms su [!DNL AEM Sites] pagina. Inoltre, è possibile configurarlo per visualizzare bozze e moduli adattivi inviati e moduli HTML5 per un utente connesso. Per ulteriori informazioni sul portale dei moduli, vedere [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md).

Quando un utente connesso salva un modulo adattivo come bozza o lo invia, viene visualizzato nelle schede Bozze e Invii nel portale dei moduli. I dati per le bozze o i moduli inviati vengono memorizzati nell’archivio dati configurato per la distribuzione AEM. Le bozze e le comunicazioni degli utenti anonimi non vengono visualizzate nella pagina del portale dei moduli; tuttavia, i dati vengono memorizzati nell’archivio dati configurato. Per ulteriori informazioni, consulta [Configurazione dei servizi di archiviazione per bozze e invii](/help/forms/using/configuring-draft-submission-storage.md).

## Archiviazione dati e dati utente {#user-data-and-data-stores}

Il portale Forms memorizza i dati per la bozza e i moduli inviati nei seguenti scenari:

* L’azione di invio configurata nel modulo adattivo è **Azione di invio Forms Portal**.
* Per le azioni di invio diverse da **Azione di invio Forms Portal**, **[!UICONTROL Archiviare dati nel portale moduli]** è abilitata nella **[!UICONTROL Invio]** proprietà del contenitore di moduli adattivi.

Per ogni bozza e modulo inviato per utenti registrati e anonimi, il portale dei moduli memorizza i dati seguenti:

* Metadati del modulo come nome del modulo, percorso del modulo, ID bozza o invio, percorso allegato e ID dati utente
* Allegato modulo come byte di dati
* Dati modulo come byte di dati

A seconda della persistenza dell’archivio dati configurato, le bozze e i dati dei moduli inviati vengono memorizzati nelle posizioni seguenti.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo di persistenza</strong></p> </td>
   <td><p><strong>Archiviazione dati</strong></p> </td>
   <td><p><strong>Dove si trova</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predefiniti</p> </td>
   <td><p>AEM archivio delle istanze di authoring e pubblicazione</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>AEM archivio dell’autore e delle istanze AEM remote</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Database</p> </td>
   <td><p>AEM archivio dell'istanza autore e delle tabelle del database</p> </td>
   <td>Tabelle del database <code>data</code>, <code>metadata</code>e <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

È possibile accedere ai dati dei moduli bozza e inviati per gli utenti registrati e anonimi negli archivi dati configurati e, se necessario, eliminarli.

### Istanze AEM {#aem-instances}

Tutte le bozze e i dati dei moduli inviati nelle istanze AEM (autore, pubblicazione o remoto) per gli utenti registrati e anonimi sono memorizzati nella `/content/forms/fp/` nodo dell&#39;archivio AEM applicabile. Ogni volta che un utente connesso o anonimo salva una bozza o invia un modulo, un `draft ID` o `submission ID`, `user data ID`e un `ID` per ogni allegato (se del caso) è generato, che è associato alla relativa bozza o presentazione.

#### Accedere ai dati utente {#access-user-data}

Quando un utente connesso salva una bozza o invia un modulo, viene creato un nodo figlio con il relativo ID utente. Ad esempio, bozze e dati di invio per Sarah Rose il cui ID utente è `srose` sono memorizzati in `/content/forms/fp/srose/` nodo AEM repository. Nel nodo ID utente, i dati sono organizzati in una struttura gerarchica.

La tabella seguente spiega come i dati per tutte le bozze di `srose` è memorizzato AEM archivio.

>[!NOTE]
>
>Una struttura esatta come `drafts` viene replicato per i moduli inviati per `srose` in `/content/forms/fp/srose/submit/` nodo.
>
>Tutte le bozze e le comunicazioni di `anonymous` gli utenti sono memorizzati nella `/content/forms/fp/anonymous/` nodo, che organizza bozze e invii per tutti gli utenti anonimi sotto `draft` e `submit` nodi.

| Nodo | Descrizione |
|---|---|
| `/content/forms/fp/srose/drafts` | Dati dei nodi dei contenitori per tutte le bozze dell&#39;utente |
| `/content/forms/fp/srose/drafts/attachments/` | Organizza tutti gli allegati per l&#39;utente in base all&#39;ID bozza |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contiene l&#39;allegato per l&#39;ID selezionato in formato binario |
| `/content/forms/fp/srose/drafts/metadata/` | Organizza i metadati del modulo per l&#39;utente in base alla bozza di ID |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contiene i metadati del modulo per l&#39;ID bozza selezionato |
| `/content/forms/fp/srose/drafts/data/` | Organizza i dati dei moduli per l’utente in base all’ID dei dati utente |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contiene i dati del modulo per l’ID dati utente selezionato in formato binario |

#### Eliminare i dati utente {#delete-user-data}

Per eliminare completamente i dati utente dalle bozze e dagli invii di un utente connesso dai sistemi AEM, è necessario eliminare il `user ID` nodo per un utente specifico dal nodo autore. È necessario eliminare manualmente i dati da tutte le istanze AEM applicabili.

Le bozze e i dati di invio per tutti gli utenti anonimi sono memorizzati all&#39;interno della comune `drafts` e `submit` nodi sotto `/content/forms/fp/anonymous`. Non esiste un metodo per trovare i dati per un particolare utente anonimo a meno che non siano note alcune informazioni identificabili. In questo caso, è possibile cercare le informazioni che identificano l&#39;utente anonimo in AEM archivio ed eliminare manualmente il nodo che lo contiene da tutte le istanze AEM applicabili per rimuovere i dati dal sistema AEM. Tuttavia, per eliminare i dati per tutti gli utenti anonimi, puoi eliminare il `anonymous` nodo per rimuovere bozze e dati di invio per tutti gli utenti anonimi.

### Database {#database}

Quando AEM è configurato per memorizzare i dati in un database, le bozze e i dati di invio del portale dei moduli vengono memorizzati nelle seguenti tabelle di database per gli utenti connessi e anonimi:

* data
* metadati
* metadata aggiuntivi

#### Accedere ai dati utente {#access-user-data-1}

Per accedere alle bozze e ai dati di invio di utenti registrati e anonimi nelle tabelle del database, eseguire il seguente comando di database. Nella query, sostituisci `logged-in user` con l’ID utente a cui desideri accedere o con `anonymous` per utenti anonimi.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Eliminare i dati utente {#delete-user-data-1}

Per eliminare le bozze e i dati di invio per un utente connesso dalle tabelle del database, eseguire il seguente comando di database. Nella query, sostituisci `logged-in user` con l’ID utente di cui desideri eliminare i dati o con `anonymous` per utenti anonimi. Tieni presente che per eliminare dal database i dati di un utente anonimo specifico, devi trovarli utilizzando alcune informazioni identificabili ed eliminarli dalle tabelle del database contenenti le informazioni.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
