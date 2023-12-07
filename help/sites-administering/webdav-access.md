---
title: Accesso WebDAV
description: Scopri come accedere a Adobe Experience Manager utilizzando WebDAV.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 1%

---

# Accesso WebDAV{#webdav-access}

Per connettersi all’AEM tramite WebDAV con KDE:

AEM offre il supporto WebDAV che consente di visualizzare e modificare il contenuto dell&#39;archivio. La connessione tramite WebDAV consente l&#39;accesso diretto all&#39;archivio dei contenuti attraverso il desktop. I file di testo e PDF aggiunti al repository tramite la connessione WebDAV vengono automaticamente indicizzati in formato full-text e possono essere cercati con le interfacce di ricerca standard e tramite le API Java™ standard.

## Generale {#general}

[Istruzioni dettagliate per sistema operativo](/help/sites-administering/webdav-access.md#connecting-via-webdav) sono inclusi in questo documento, ma essenzialmente per connettersi all&#39;archivio utilizzando il protocollo WebDAV, il client WebDAV viene indirizzato alla seguente posizione:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Questo URL, se connesso dal livello del sistema operativo, fornisce accesso WebDAV all&#39;area di lavoro predefinita ( `crx.default`). Pur essendo più semplice per l’utente, non offre la flessibilità aggiuntiva di specificare i nomi delle aree di lavoro, che può essere ottenuta utilizzando [URL WebDAV](/help/sites-administering/webdav-access.md#webdav-urls).

AEM visualizza il contenuto dell’archivio come segue:

* Un nodo del tipo `nt:folder` viene visualizzato come cartella. Nodi sotto il `nt:folder` come contenuto della cartella.

* Un nodo del tipo `nt:file` viene visualizzato come file. Nodi sotto il `nt:file` non viene visualizzato, ma costituisce il contenuto del file.

Quando si utilizza WebDAV per creare e modificare cartelle e file, l&#39;AEM crea e modifica i dati necessari `nt:folder` e `nt:file` nodi. Se si intende utilizzare WebDAV per importare ed esportare contenuti, provare a utilizzare `nt:file` e `nt:folder` tipi di nodo il più possibile.

>[!NOTE]
>
>Prima di configurare WebDAV, controllare [Requisiti tecnici](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URL WebDAV {#webdav-urls}

L&#39;URL del server WebDAV ha la seguente struttura:

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
   <td>Host e porta su cui viene eseguito AEM</td>
   <td>Percorso per l’app web dell’archivio AEM</td>
   <td>Percorso a cui è mappato il servlet WebDAV</td>
   <td>Nome dell’area di lavoro</td>
  </tr>
 </tbody>
</table>

Modificando l’elemento del workspace nel percorso, puoi mappare aree di lavoro diverse da quelle predefinite ( `crx.default`). Ad esempio, per mappare un’area di lavoro denominata `staging`, utilizza il seguente URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Connessione tramite WebDAV {#connecting-via-webdav}

[Come indicato sopra](/help/sites-administering/webdav-access.md#general), per connettersi al repository utilizzando il protocollo WebDAV, puntare il client WebDAV alla posizione del repository. Tuttavia, a seconda del sistema operativo in uso, i passaggi necessari per la connessione del client sono diversi e potrebbe essere necessaria una configurazione del sistema operativo.

Vengono fornite istruzioni su come collegare i seguenti sistemi operativi:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Per connettere correttamente un sistema Microsoft® Windows 7 (e versioni successive) a un&#39;istanza AEM non protetta con SSL, l&#39;opzione per stabilire l&#39;autenticazione di base su una rete non protetta deve essere abilitata in modo esplicito in Windows. Questa funzionalità richiede una modifica nel Registro di sistema di Windows di WebClient.

Una volta aggiornato il Registro di sistema, è possibile mappare l&#39;istanza AEM come un&#39;unità.

#### Configurazione Windows 7 e versioni successive {#windows-and-greater-configuration}

Per aggiornare il Registro di sistema in modo da consentire l&#39;autenticazione di base su una rete non protetta:

1. Individuare la seguente sottochiave del Registro di sistema:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Imposta il `BasicAuthLevel` sottochiave della voce del Registro di sistema per un valore di `2` o superiore.

   Se non è presente, aggiungi la sottochiave.

1. Riavviare il sistema per rendere effettiva la modifica del Registro di sistema.

>[!NOTE]
>
>In questo Adobe si consiglia di creare un utente Windows con le stesse credenziali dell&#39;utente del repository, in caso contrario potrebbero verificarsi conflitti di autorizzazioni.

#### Configurazione Windows 8 {#windows-configuration}

Per Windows 8, modificare la voce del Registro di sistema [come descritto per Windows 7 e versioni successive](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Tuttavia, prima di eseguire questa operazione, è necessario abilitare Esperienza desktop per visualizzare la voce del Registro di sistema.

Per abilitare Esperienza desktop, apri **Server Manager**, quindi **Funzioni**, quindi **Aggiungi funzionalità**, quindi **Esperienza desktop**.

Dopo il riavvio, è disponibile la voce del Registro di sistema descritta per Windows 7 e versioni successive. Modificarlo come descritto per Windows 7 e versioni successive.

#### Connessione in Windows {#connecting-in-windows}

Per connettersi all&#39;AEM tramite WebDAV in un ambiente Windows:

1. Apri **Esplora risorse** o **Esplora file** e fai clic su **Computer** o **Questo PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Per avviare la procedura guidata, fare clic su **Mappare l&#39;unità di rete**.
1. Immetti i dettagli della mappatura:

   * **Unità**: scegli una lettera qualsiasi
   * **Cartella**: `http://localhost:4502`
   * Verifica **Connetti utilizzando credenziali diverse**

   Fai clic su Fine

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Se l&#39;AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP.

1. Inserisci il nome utente `admin` e password `admin`. L’Adobe consiglia di utilizzare l’account admin preconfigurato per il test.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. La procedura guidata si chiude e l&#39;unità appena mappata viene aperta in una finestra Esplora risorse o Esplora file.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows ha ora mappato l&#39;AEM come unità tramite WebDAV e può essere utilizzato come qualsiasi altra unità.

### macOS {#macos}

Non sono necessari passaggi di configurazione per la connessione tramite WebDAV su macOS. È possibile connettersi al server WebDAV.

1. Passa a qualsiasi **Finder** e fai clic su **Vai** e **Connetti al server** o premere **Comando+k**.
1. In **Connetti al server** immettere l&#39;ubicazione AEM:

   * `http://localhost:4502`

   >[!NOTE]
   >
   >Se l&#39;AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP.

1. Quando viene richiesta l&#39;autenticazione, immettere il nome utente `admin` e password `admin`. L’Adobe consiglia di utilizzare l’account admin preconfigurato per il test.

macOS è ora connesso all&#39;AEM tramite WebDAV e può essere utilizzato come qualsiasi altra cartella sul Mac.

### Linux® {#linux}

La connessione tramite WebDAV su Linux® non richiede alcuna configurazione, ma richiede alcuni passaggi per effettuare la connessione, che variano a seconda dell&#39;ambiente desktop.

#### GNOME {#gnome}

Per connettersi all&#39;AEM tramite WebDAV con GNOME:

1. In Nautilus (Esplora file), seleziona **Places** e seleziona **Connetti al server**.
1. In **Connetti al server** selezionare WebDAV (HTTP) in Tipo di servizio.

1. In entrata **Server**, immetti `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se l&#39;AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP.

1. In entrata **Cartella**, immetti `/dav`
1. Inserisci il nome utente `admin`. L’Adobe consiglia di utilizzare l’account admin preconfigurato per il test.
1. Lascia vuota la porta e immetti un nome per la connessione.
1. Clic **Connetti**. L&#39;AEM richiede la password.
1. Immetti la password `admin` e fai clic su **Connetti**.

GNOME ha ora montato AEM come volume e puoi usarlo come qualsiasi altro volume.

#### KDE {#kde}

1. Aprire la Creazione guidata cartella di rete.
1. Seleziona **CartellaWeb**(webdav) e fai clic su Avanti.
1. In entrata **Nome**, digitare un nome di connessione.
1. In entrata **Utente**, immetti `admin.` L’Adobe consiglia di utilizzare l’account amministratore preconfigurato.
1. In entrata **Server**, immetti `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se l&#39;AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP

1. In entrata **Cartella**, immetti `dav`

1. Clic **Salva e connetti**.
1. Quando viene richiesta la password, immetterla `admin` e fai clic su **Connetti**.

KDE ha ora montato AEM come volume e puoi utilizzarlo come qualsiasi altro volume.
