---
title: Accesso WebDAV
seo-title: Accesso WebDAV
description: Informazioni sull'accesso WebDAV in AEM.
seo-description: Informazioni sull'accesso WebDAV in AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# WebDAV Access{#webdav-access}

Per connettersi ad AEM tramite WebDAV con KDE:

AEM offre il supporto WebDAV che consente di visualizzare e modificare il contenuto del repository. La connessione tramite WebDAV consente di accedere direttamente all&#39;archivio dei contenuti tramite il desktop. I file di testo e PDF che vengono aggiunti all&#39;archivio tramite la connessione WebDAV vengono indicizzati automaticamente in full-text e possono essere ricercati con le interfacce di ricerca standard e tramite le API Java standard.

## Generale {#general}

[Istruzioni dettagliate per ogni sistema](/help/sites-administering/webdav-access.md#connecting-via-webdav) operativo sono incluse in questo documento, ma sostanzialmente per connettersi al repository utilizzando il protocollo WebDAV, è necessario puntare il client WebDAV al seguente percorso:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Questo URL, se collegato a livello di sistema operativo, fornisce l&#39;accesso WebDAV all&#39;area di lavoro predefinita ( `crx.default`). Semplificando l&#39;utente, l&#39;operazione non offre agli utenti la flessibilità di specificare i nomi degli spazi di lavoro, che possono essere eseguiti utilizzando URL [WebDAV aggiuntivi](/help/sites-administering/webdav-access.md#webdav-urls).

AEM visualizza il contenuto dell’archivio come segue:

* Un nodo del tipo `nt:folder` viene visualizzato come cartella. I nodi sotto il `nt:folder` nodo vengono visualizzati come contenuto della cartella.

* Un nodo del tipo `nt:file` viene visualizzato come file. I nodi sotto il `nt:file` nodo non vengono visualizzati, ma costituiscono il contenuto del file.

Quando utilizzate WebDAV per creare e modificare cartelle e file, AEM crea e modifica i nodi `nt:folder` e `nt:file` i nodi necessari. Se prevedete di utilizzare WebDAV per importare ed esportare contenuto, provate a utilizzare il più possibile i tipi `nt:file` e `nt:folder` nodo.

>[!NOTE]
>
>Prima di configurare WebDAV, verificare i requisiti [tecnici](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URL WebDAV {#webdav-urls}

L&#39;URL per il server WebDAV ha la struttura seguente:

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>Descrizione</strong></td>
   <td>Host e porta su cui AEM esegue</td>
   <td>Percorso dell'app Web dell'archivio AEM</td>
   <td>Percorso di mappatura del servlet WebDAV</td>
   <td>Nome dell’area di lavoro</td>
  </tr>
 </tbody>
</table>

Modificando l’elemento area di lavoro nel percorso, potete eseguire la mappatura di aree di lavoro diverse da quelle predefinite ( `crx.default`). Ad esempio, per mappare un’area di lavoro denominata `staging`, utilizzate il seguente URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Connessione tramite WebDAV {#connecting-via-webdav}

[Come già detto](/help/sites-administering/webdav-access.md#general), per connettersi al repository utilizzando il protocollo WebDAV, è necessario puntare il client WebDAV al percorso del repository. Tuttavia, a seconda del sistema operativo in uso, i passaggi necessari per collegare il client sono diversi e potrebbe essere necessaria una configurazione del sistema operativo.

Sono fornite istruzioni su come collegare i seguenti sistemi operativi:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Per collegare correttamente un sistema Microsoft Windows 7 (e versioni successive) a un’istanza di AEM non protetta con SSL, in Windows deve essere esplicitamente abilitata l’opzione per stabilire l’autenticazione di base su una rete non protetta. Ciò richiede una modifica nel Registro di sistema di Windows del WebClient.

Una volta aggiornato il Registro di sistema, l’istanza di AEM può essere mappata come un’unità.

#### Configurazione di Windows 7 e versioni successive {#windows-and-greater-configuration}

Per aggiornare il Registro di sistema per consentire l&#39;autenticazione di base su una rete non protetta:

1. Individuate la seguente sottochiave del Registro di sistema:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Impostate la sottochiave della voce di `BasicAuthLevel` registro su un valore `2` o maggiore.

   Se non è presente, aggiungete la sottochiave.

1. Per rendere effettiva la modifica del Registro di sistema, è necessario riavviare il sistema.

Per ulteriori informazioni su questa modifica del Registro di sistema, consultate [Microsoft Support KB 841215](https://support.microsoft.com/default.aspx/kb/841215) .

Per informazioni su come migliorare la reattività del client WebDav in Windows, consultate [Microsoft Support KB 2445570](https://support.microsoft.com/kb/2445570) .

>[!NOTE]
>
>Adobe consiglia di creare un utente Windows con le stesse credenziali dell&#39;utente del repository, in caso contrario si verifichino conflitti di autorizzazione.

#### Configurazione di Windows 8 {#windows-configuration}

Per Windows 8 è inoltre necessario modificare la voce del Registro di sistema [come descritto per Windows 7 e versioni successive](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Tuttavia, prima di eseguire questa operazione, per visualizzare la voce del Registro di sistema è necessario abilitare Esperienza desktop.

Per abilitare Desktop Experience, apri **Server Manager**, quindi **Funzioni**, quindi **Aggiungi funzionalità**, quindi Esperienza **** desktop.

Dopo il riavvio è disponibile la voce del Registro di sistema descritta per Windows 7 e versioni successive. Modificatelo come descritto per Windows 7 e versioni successive.

#### Connessione in Windows {#connecting-in-windows}

Per connettersi ad AEM tramite WebDAV in un ambiente Windows:

1. Aprire **Esplora** risorse o **Esplora** file e fare clic su **Computer** o **Questo PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Fare clic su **Mappa unità** di rete per avviare la procedura guidata.
1. Immettete i dettagli di mappatura:

   * **Unità**: Scegli una lettera disponibile
   * **Cartella**: `http://localhost:4502`
   * Verificare **Connect utilizzando credenziali diverse**
   Fare clic su Fine

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizzate tale numero invece di 4502. Inoltre, se non si esegue l&#39;archivio contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente.

1. Immettere nome utente `admin` e password `admin`. Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato per il test.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. La procedura guidata si chiude e l&#39;unità mappata di recente viene aperta in una finestra di Esplora risorse o Esplora file.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows ha mappato AEM come unità tramite WebDAV ed è possibile utilizzarlo come qualsiasi altra unità.

### macOS {#macos}

Non sono necessari passaggi di configurazione per la connessione tramite WebDAV su macOS. È sufficiente connettersi al server WebDAV.

1. Passate a una finestra del **Finder** e fate clic su **Vai** e **Connetti al server** oppure premete **Comando+k**.
1. Nella finestra **Connetti al server** , immettete il percorso AEM:

   * `http://localhost:4502`
   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizzate tale numero invece di 4502. Inoltre, se non si esegue l&#39;archivio contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente.

1. Quando viene richiesta l’autenticazione, immettete nome utente `admin` e password `admin`. Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato per il test.

macOS è ora connesso ad AEM tramite WebDAV e può essere utilizzato come qualsiasi altra cartella sul Mac.

### Linux {#linux}

La connessione tramite WebDAV su Linux non richiede alcuna configurazione, ma richiede alcuni passaggi per effettuare la connessione che varia a seconda dell&#39;ambiente desktop.

#### GNOME {#gnome}

Per connettersi ad AEM tramite WebDAV con GNOME:

1. In Nautilus (file Explorer), selezionate **Luoghi** e selezionate **Connetti al server**.
1. Nella finestra **Connetti al server** , selezionate WebDAV (HTTP) in Tipo di servizio.

1. Nel **server**, immettere `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizzate tale numero invece di 4502. Inoltre, se non si esegue l&#39;archivio contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente.

1. In **Cartella**, immettete `/dav`
1. Immettere il nome utente `admin`. Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato per il test.
1. Lasciate vuota la porta e immettete un nome per la connessione.
1. Fate clic su **Connect**. AEM richiede la password.
1. Immettete la password `admin` e fate clic su **Connect**.

GNOME ha ora montato AEM come volume ed è possibile utilizzarlo come qualsiasi altro volume.

#### KDE {#kde}

1. Aprire la procedura guidata Cartella di rete.
1. Selezionate **WebFolder**(webDAV) e fate clic su Avanti.
1. In **Nome**, digitate un nome di connessione.
1. In **Utente**, immettere `admin.` Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato.
1. Nel **server**, immettere `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM si trova su un’altra porta, utilizzate tale numero invece di 4502. Inoltre, se non si esegue l&#39;archivio contenuti nel computer locale, sostituire `localhost` con il nome del server o l&#39;indirizzo IP corrispondente

1. In **Cartella**, immettete `dav`

1. Fate clic su **Salva e collega**.
1. Quando viene richiesta la password, immettete la password `admin` e fate clic su **Connect**.

KDE ha ora montato AEM come volume e può essere utilizzato come qualsiasi altro volume.
