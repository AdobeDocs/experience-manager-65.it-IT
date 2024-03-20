---
title: Forms Portal | Gestione dei dati utente
description: Scopri come gestire i dati utente, ad esempio l’accesso, l’eliminazione e l’archivio dati su AEM Forms Portal.
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Forms Portal | Gestione dei dati utente {#forms-portal-handling-user-data}

[!DNL AEM Forms] Portal fornisce componenti che è possibile utilizzare per elencare i moduli adattivi, i moduli HTML5 e altre risorse Forms sulla [!DNL AEM Sites] pagina. Inoltre, puoi configurarlo per visualizzare le bozze e i moduli adattivi inviati e i moduli HTML5 per un utente connesso. Per ulteriori informazioni su Forms Portal, consulta [Introduzione alla pubblicazione di moduli su un portale](/help/forms/using/introduction-publishing-forms.md).

Quando un utente connesso salva un modulo adattivo come bozza o lo invia, questo viene visualizzato nelle schede Bozze e Invii del portale Forms. I dati per le bozze di moduli o i moduli inviati vengono memorizzati nell’archivio dati configurato per la distribuzione AEM. Le bozze e gli invii di utenti anonimi non vengono visualizzati nella pagina del portale Forms; tuttavia, i dati vengono memorizzati nell&#39;archivio dati configurato. Consulta [Configurazione dei servizi di archiviazione per le bozze e gli invii](/help/forms/using/configuring-draft-submission-storage.md).

## Dati utente e archivi dati {#user-data-and-data-stores}

Forms Portal memorizza i dati per le bozze e i moduli inviati nei seguenti scenari:

* L’azione di invio configurata nel modulo adattivo è **Azione di invio Forms Portal**.
* Per azioni di invio diverse da **Azione di invio Forms Portal**, il **[!UICONTROL Archivia dati in Forms Portal]** è abilitata nella **[!UICONTROL Invio]** proprietà del contenitore di moduli adattivi.

Per ogni bozza e modulo inviato per utenti connessi e anonimi, il portale Forms memorizza i dati seguenti:

* Metadati del modulo come nome del modulo, percorso del modulo, ID bozza o invio, percorso allegati e ID dati utente
* Allegato modulo come byte di dati
* Dati modulo come byte di dati

A seconda della persistenza dell’archivio dati configurato, i dati delle bozze e dei moduli inviati vengono memorizzati nei seguenti percorsi.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo di persistenza</strong></p> </td>
   <td><p><strong>Archivio dati</strong></p> </td>
   <td><p><strong>Dove si trova</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predefiniti</p> </td>
   <td><p>Archivio AEM delle istanze Author e Publish</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Archivio AEM delle istanze dell’AEM Autore e remote</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Database</p> </td>
   <td><p>Archivio AEM dell’istanza Autore e delle tabelle di database</p> </td>
   <td>Tabelle di database <code>data</code>, <code>metadata</code>, e <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

Puoi accedere ai dati delle bozze e dei moduli inviati per gli utenti connessi e anonimi negli archivi dati configurati e, se necessario, eliminarli.

### Istanze AEM {#aem-instances}

Tutte le bozze e i dati dei moduli inviati nelle istanze AEM (di authoring, pubblicazione o in remoto) per gli utenti connessi e anonimi vengono memorizzati nel file `/content/forms/fp/` nodo dell’archivio AEM applicabile. Ogni volta che un utente connesso o anonimo salva una bozza o invia un modulo, viene visualizzata una `draft ID` o `submission ID`, a `user data ID`e casuale `ID` per ogni allegato (se applicabile). È associata alla rispettiva bozza o presentazione.

#### Accedere ai dati utente {#access-user-data}

Quando un utente connesso salva una bozza o invia un modulo, viene creato un nodo figlio con il relativo ID utente. Ad esempio, bozza e invia dati per Sarah Rose il cui ID utente è `srose` sono archiviati in `/content/forms/fp/srose/` nell’archivio AEM. Nel nodo ID utente, i dati sono organizzati in una struttura gerarchica.

Nella tabella seguente viene illustrato il modo in cui i dati di tutte le bozze vengono `srose` è memorizzato nell’archivio AEM.

>[!NOTE]
>
>Una struttura esatta come `drafts` viene replicato per i moduli inviati per `srose` sotto `/content/forms/fp/srose/submit/` nodo.
>
>Tutte le bozze e le richieste di `anonymous` Gli utenti vengono memorizzati sotto `/content/forms/fp/anonymous/` , che organizza le bozze e gli invii per tutti gli utenti anonimi sotto `draft` e `submit` nodi.

| Nodo | Descrizione |
|---|---|
| `/content/forms/fp/srose/drafts` | Contenitore dati nodo per tutte le bozze dell&#39;utente |
| `/content/forms/fp/srose/drafts/attachments/` | Organizza tutti gli allegati per l’utente in base all’ID bozza |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contiene un allegato per l’ID selezionato in formato binario |
| `/content/forms/fp/srose/drafts/metadata/` | Organizza i metadati del modulo per l’utente in base all’ID bozza |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contiene i metadati del modulo per l’ID bozza selezionato |
| `/content/forms/fp/srose/drafts/data/` | Organizza i dati dei moduli per l’utente in base all’ID dati utente |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contiene dati modulo per l&#39;ID dati utente selezionato in formato binario |

#### Elimina dati utente {#delete-user-data}

Per eliminare completamente i dati utente dalle bozze e dagli invii di un utente connesso dai sistemi AEM, è necessario eliminare `user ID` per un utente specifico dal nodo di authoring. Elimina manualmente i dati da tutte le istanze AEM applicabili.

Le bozze e i dati di invio per tutti gli utenti anonimi sono memorizzati nel comune `drafts` e `submit` nodi in `/content/forms/fp/anonymous`. Non esiste un metodo per trovare i dati per un particolare utente anonimo a meno che non siano note alcune informazioni identificabili. In questo caso, puoi cercare informazioni che identificano l’utente anonimo nell’archivio AEM ed eliminare manualmente il nodo che lo contiene da tutte le istanze AEM applicabili per rimuovere i dati dal sistema AEM. Tuttavia, per eliminare i dati di tutti gli utenti anonimi, puoi eliminare `anonymous` per rimuovere bozze e dati di invio per tutti gli utenti anonimi.

### Database {#database}

Quando l’AEM è configurato per memorizzare i dati in un database, i dati bozza e di invio di Forms Portal vengono memorizzati nelle seguenti tabelle di database sia per gli utenti connessi che per quelli anonimi:

* dati
* metadati
* metadati aggiuntivi

#### Accedere ai dati utente {#access-user-data-1}

Per accedere ai dati delle bozze e degli invii per un utente connesso e anonimo nelle tabelle del database, eseguire il comando seguente. Nella query, sostituisci `logged-in user` con l’ID utente di cui desideri accedere ai dati o con `anonymous` per utenti anonimi.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Elimina dati utente {#delete-user-data-1}

Per eliminare i dati relativi alle bozze e agli invii per un utente connesso dalle tabelle del database, eseguire il comando seguente. Nella query, sostituisci `logged-in user` con l’ID utente di cui desideri eliminare i dati o con `anonymous` per utenti anonimi. Per eliminare i dati di un utente anonimo specifico dal database, è necessario trovarli utilizzando alcune informazioni identificabili ed eliminarli dalle tabelle del database contenenti le informazioni.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
