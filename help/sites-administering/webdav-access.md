---
title: Accesso WebDAV
seo-title: WebDAV Access
description: Informazioni sull'accesso WebDAV in AEM.
seo-description: Learn about WebDAV access in AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# Accesso WebDAV{#webdav-access}

Per connettersi a AEM tramite WebDAV con KDE:

AEM offre il supporto WebDAV che consente di visualizzare e modificare il contenuto del repository. La connessione tramite WebDAV consente di accedere direttamente all’archivio dei contenuti tramite il desktop. I file di testo e PDF che vengono aggiunti all&#39;archivio tramite la connessione WebDAV vengono indicizzati automaticamente in formato full-text e possono essere cercati nelle interfacce di ricerca standard e tramite le API Java standard.

## Generale {#general}

[Istruzioni dettagliate per sistema operativo](/help/sites-administering/webdav-access.md#connecting-via-webdav) sono inclusi in questo documento, ma essenzialmente per connettersi al repository utilizzando il protocollo WebDAV, è necessario indirizzare il client WebDAV al seguente percorso:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Questo URL, se connesso dal livello del sistema operativo, fornisce l&#39;accesso WebDAV all&#39;area di lavoro predefinita ( `crx.default`). Pur essendo più semplice per l’utente, non offre loro la flessibilità aggiuntiva di specificare i nomi dell’area di lavoro, che può essere realizzata utilizzando [URL WebDAV](/help/sites-administering/webdav-access.md#webdav-urls).

AEM visualizza il contenuto del repository come segue:

* Un nodo del tipo `nt:folder` viene visualizzato come cartella. Nodi sotto il nodo `nt:folder` vengono visualizzati come contenuto della cartella.

* Un nodo del tipo `nt:file` viene visualizzato come file. Nodi sotto il nodo `nt:file` il nodo non viene visualizzato, ma forma il contenuto del file.

Quando si utilizza WebDAV per creare e modificare cartelle e file, AEM crea e modifica le modifiche necessarie `nt:folder` e `nt:file` nodi. Se si prevede di utilizzare WebDAV per importare ed esportare contenuti, provare a utilizzare `nt:file` e `nt:folder` tipi di nodo il più possibile.

>[!NOTE]
>
>Prima di configurare WebDAV, controlla il [Requisiti tecnici](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URL WebDAV {#webdav-urls}

L&#39;URL del server WebDAV presenta la struttura seguente:

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
   <td>Percorso dell’app Web dell’archivio AEM</td>
   <td>Percorso a cui è mappato il servlet WebDAV</td>
   <td>Nome dell’area di lavoro</td>
  </tr>
 </tbody>
</table>

Modificando l&#39;elemento workspace nel percorso, è possibile mappare aree di lavoro diverse da quelle predefinite ( `crx.default`). Ad esempio, per mappare un’area di lavoro denominata `staging`, utilizza il seguente URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Connessione tramite WebDAV {#connecting-via-webdav}

[Come indicato sopra](/help/sites-administering/webdav-access.md#general), per connettersi al repository utilizzando il protocollo WebDAV, posizionare il client WebDAV nel percorso del repository. Tuttavia, a seconda del sistema operativo, i passaggi necessari per la connessione al client sono diversi e potrebbe essere necessaria la configurazione del sistema operativo.

Vengono fornite istruzioni su come collegare i seguenti sistemi operativi:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Per connettere correttamente un sistema Microsoft Windows 7 (e versioni successive) a un&#39;istanza AEM non protetta con SSL, l&#39;opzione per stabilire l&#39;autenticazione di base su una rete non protetta deve essere abilitata esplicitamente in Windows. Ciò richiede una modifica nel Registro di sistema di Windows del WebClient.

Una volta aggiornato il registro, l&#39;istanza AEM può essere mappata come unità.

#### Configurazione di Windows 7 e versioni successive {#windows-and-greater-configuration}

Per aggiornare il Registro di sistema per consentire l&#39;autenticazione di base su una rete non protetta:

1. Individua la seguente sottochiave del Registro di sistema:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Imposta la `BasicAuthLevel` sottochiave della voce del Registro di sistema a un valore di `2` o superiore.

   Se non è presente, aggiungi la sottochiave.

1. Per rendere effettiva la modifica del Registro di sistema, è necessario riavviare il sistema.

Vedi [Supporto Microsoft KB 841215](https://support.microsoft.com/default.aspx/kb/841215) per ulteriori informazioni su questa modifica del Registro di sistema.

Vedi [Supporto Microsoft KB 2445570](https://support.microsoft.com/kb/2445570) per informazioni su come migliorare la reattività del client WebDav in Windows.

>[!NOTE]
>
>L&#39;Adobe consiglia di creare un utente Windows con le stesse credenziali dell&#39;utente del repository, altrimenti si potrebbero verificare conflitti di autorizzazione.

#### Configurazione di Windows 8 {#windows-configuration}

Per Windows 8 è inoltre necessario modificare la voce del Registro di sistema [come descritto per Windows 7 e versioni successive](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). Tuttavia, prima di eseguire questa operazione, per visualizzare la voce del Registro di sistema è necessario abilitare l’esperienza desktop.

Per abilitare l’esperienza desktop, apri **Server Manager**, quindi **Funzioni**, quindi **Aggiungi funzionalità**, quindi **Esperienza desktop**.

Dopo il riavvio è disponibile la voce del Registro di sistema descritta per Windows 7 e versioni successive. Modificarlo come descritto per Windows 7 e versioni successive.

#### Connessione a Windows {#connecting-in-windows}

Per connettersi a AEM tramite WebDAV in un ambiente Windows:

1. Apri **Esplora risorse** o **Esplora file** e fai clic su **Computer** o **Questo PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Fai clic su **Mappa unità di rete** per avviare la procedura guidata.
1. Immetti i dettagli di mappatura:

   * **Unità**: Scegli qualsiasi lettera disponibile
   * **Cartella**: `http://localhost:4502`
   * Controlla **Connessione tramite credenziali diverse**

   Fare clic su Fine

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Se AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP.

1. Immetti nome utente `admin` e password `admin`. Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato per il test.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. La procedura guidata viene chiusa e l&#39;unità appena mappata viene aperta in una finestra Esplora risorse o Esplora file di Windows.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows ha ora mappato AEM come unità tramite WebDAV e può essere utilizzato come qualsiasi altra unità.

### macOS {#macos}

Non sono necessari passaggi di configurazione per la connessione tramite WebDAV su macOS. È sufficiente connettersi al server WebDAV.

1. Passa a qualsiasi **Finder** finestra e fai clic su **Vai** e **Connetti al server** o premere **Comando+k**.
1. In **Connetti al server** nella finestra immetti la posizione AEM:

   * `http://localhost:4502`
   >[!NOTE]
   >
   >Se AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP.

1. Quando ti viene richiesto di eseguire l&#39;autenticazione, immetti il nome utente `admin` e password `admin`. Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato per il test.

macOS è ora connesso a AEM tramite WebDAV e può essere utilizzato come qualsiasi altra cartella sul Mac.

### Linux {#linux}

La connessione tramite WebDAV su Linux non richiede alcuna configurazione, ma richiede alcuni passaggi per effettuare la connessione che variano a seconda dell&#39;ambiente desktop.

#### GNOME {#gnome}

Per connettersi a AEM tramite WebDAV con GNOME:

1. In Nautilus (file explorer), seleziona **Luoghi** e seleziona **Connetti al server**.
1. In **Connetti al server** in Tipo di servizio, selezionare WebDAV (HTTP).

1. In **Server**, inserisci `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP.

1. In **Cartella**, inserisci `/dav`
1. Immetti il nome utente `admin`. Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato per il test.
1. Lasciate vuota la porta e immettete un nome per la connessione.
1. Fai clic su **Connetti**. AEM richiesto la password.
1. Immetti la password `admin` e fai clic su **Connetti**.

GNOME è ora montato AEM come volume e può essere utilizzato come qualsiasi altro volume.

#### KDE {#kde}

1. Apri la procedura guidata Cartella di rete .
1. Seleziona **WebFolder**(webdav) e fai clic su Avanti.
1. In **Nome**, digita un nome per la connessione.
1. In **Utente**, inserisci `admin.` Adobe consiglia di utilizzare l&#39;account amministratore preconfigurato.
1. In **Server**, inserisci `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM si trova su un&#39;altra porta, utilizzare il numero di porta anziché 4502. Inoltre, se non esegui l’archivio dei contenuti sul computer locale, sostituisci `localhost` con il rispettivo nome server o indirizzo IP

1. In **Cartella**, inserisci `dav`

1. Fai clic su **Salva e connetti**.
1. Quando viene richiesta la password, immetti la password `admin` e fai clic su **Connetti**.

KDE è ora montato AEM come volume e può essere utilizzato come qualsiasi altro volume.
