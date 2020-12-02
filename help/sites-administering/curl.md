---
title: Utilizzo di cURL con AEM
seo-title: Utilizzo di cURL con AEM
description: Scopri come utilizzare cURL con AEM.
seo-description: Scopri come utilizzare cURL con AEM.
uuid: 771b9acc-ff3a-41c9-9fee-7e5d2183f311
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d4ceb82e-2889-4507-af22-b051af83be38
translation-type: tm+mt
source-git-commit: 4eb5f1c4aa6631d2570279eb1d4bf17a928e3b9f
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---


# Utilizzo di cURL con AEM{#using-curl-with-aem}

Gli amministratori devono spesso automatizzare o semplificare le attività più comuni all&#39;interno di qualsiasi sistema. In AEM, ad esempio, la gestione di utenti, l&#39;installazione di pacchetti e la gestione di pacchetti OSGi sono attività che devono essere eseguite normalmente.

A causa della natura RESTful del framework Sling su cui AEM è costruito, la maggior parte delle attività può essere ridotta a una chiamata URL. cURL può essere utilizzato per eseguire tali chiamate URL e può essere uno strumento utile per AEM amministratori.

## Cos&#39;è cURL {#what-is-curl}

cURL è uno strumento della riga di comando open-source utilizzato per eseguire manipolazioni URL. Supporta un&#39;ampia gamma di protocolli Internet tra cui HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, DAP, DICT, TELNET, FILE, IMAP, POP3, SMTP e RTSP.

cURL è uno strumento noto e ampiamente utilizzato per ottenere o inviare dati utilizzando la sintassi URL ed è stato originariamente rilasciato nel 1997. Il nome cURL in origine significava &quot;see URL&quot;.

A causa della natura RESTful del framework Sling su cui AEM è creato, la maggior parte delle attività può essere ridotta a una chiamata URL, che può essere eseguita con cURL. [Le ](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) attività di manipolazione dei contenuti, come l’attivazione delle pagine e l’avvio dei flussi di lavoro, nonché  [le attività ](/help/sites-administering/curl.md#common-operational-aem-curl-commands) operative come la gestione dei pacchetti e la gestione degli utenti possono essere automatizzate tramite cURL. È inoltre possibile [creare comandi cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) personalizzati per la maggior parte delle attività in AEM.

>[!NOTE]
>
>Qualsiasi comando AEM eseguito tramite cURL deve essere autorizzato come qualsiasi utente a AEM. Tutti gli ACL e i diritti di accesso vengono rispettati quando si utilizza cURL per eseguire un comando AEM.

## Download di cURL {#downloading-curl}

cURL è una parte standard di macOS e alcune distanze Linux. Tuttavia è disponibile per la maggior parte di tutti i sistemi operativi. Gli ultimi download sono disponibili all&#39;indirizzo [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

L&#39;archivio di origine di cURL è disponibile anche su GitHub.

## Creazione di un comando di AEM cURL-Ready {#building-a-curl-ready-aem-command}

I comandi cURL possono essere creati per la maggior parte delle operazioni in AEM quali attivazione di flussi di lavoro, verifica delle configurazioni OSGi, attivazione di comandi JMX, creazione di agenti di replica e molto altro.

Per trovare il comando esatto necessario per la vostra particolare operazione, è necessario utilizzare gli strumenti di sviluppo nel browser per catturare la chiamata POST al server quando eseguite il comando AEM.

Nei passaggi seguenti viene descritto come eseguire questa operazione utilizzando come esempio la creazione di una nuova pagina nel browser Chrome.

1. Preparate l’azione da richiamare all’interno di AEM. In questo caso, alla fine della procedura guidata **Crea pagina**, non è stato ancora fatto clic su **Crea**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. Avviate gli strumenti di sviluppo e selezionate la scheda **Rete**. Fare clic sull&#39;opzione **Mantieni registro** prima di cancellare la console.

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. Fare clic su **Crea** nella procedura guidata **Crea pagina** per creare effettivamente il flusso di lavoro.
1. Fare clic con il pulsante destro del mouse sull&#39;azione POST risultante e selezionare **Copia** -> **Copia come cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. Copiate il comando cURL in un editor di testo e rimuovete tutte le intestazioni dal comando, che inizia con `-H` (evidenziato in blu nell&#39;immagine sottostante) e aggiungete il parametro di autenticazione corretto, ad esempio `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Eseguite il comando cURL dalla riga di comando e visualizzate la risposta.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## Comandi comuni AEM cURL operativi {#common-operational-aem-curl-commands}

Elenco di comandi cURL AEM per le comuni attività amministrative e operative.

>[!NOTE]
>
>Gli esempi seguenti presumono che AEM in esecuzione su `localhost` sulla porta `4502` e utilizza l&#39;utente `admin` con password `admin`. I segnaposto dei comandi aggiuntivi sono impostati tra parentesi angolari.

### Gestione pacchetti {#package-management}

#### Elenca tutti i pacchetti installati

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### Creare un pacchetto {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### Anteprima di un pacchetto {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### Contenuto pacchetto elenco {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### Creare un pacchetto {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### Riavvolgere un pacchetto {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### Rinominare un pacchetto {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### Caricare un pacchetto {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### Installare un pacchetto {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Disinstallare un pacchetto {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Eliminare un pacchetto {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Download di un pacchetto {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

### User Management {#user-management}

#### Crea nuovo utente {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### Creare un nuovo gruppo {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### Aggiunta di una proprietà a un utente esistente {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### Creazione di un utente con un profilo {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### Crea un nuovo utente come membro di un gruppo {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### Aggiunta di un utente a un gruppo {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Rimozione di un utente da un gruppo {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Imposta appartenenza a un gruppo di utenti {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### Eliminare un utente {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser 
```

#### Eliminare un gruppo {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### Backup {#backup}

Per ulteriori informazioni, vedere [Backup e ripristino](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup).

### OSGi {#osgi}

#### Avvio di un pacchetto {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### Arresto di un pacchetto {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### Annulla validità cache {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### Rimuovere la cache {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### Agente replica {#replication-agent}

#### Controllare lo stato di un agente {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:conten t.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on?agent=publish
```

#### Eliminare un agente {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### Creare un agente {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### Sospendi agente {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on
```

#### Cancellare la coda di un agente {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on
```

### Communities {#communities}

#### Assegnazione e revoca dei simboli {#assign-and-revoke-badges}

Per ulteriori informazioni, vedere [Punteggio delle community e Badge](/help/communities/implementing-scoring.md#assign-and-revoke-badges).

Per ulteriori informazioni, vedere [Punteggio e Badges Essentials](/help/communities/configure-scoring.md#example-setup).

#### Reindicizzazione MSRP {#msrp-reindexing}

Per ulteriori informazioni, vedere [MSRP - Provider risorse di storage MongoDB](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command).

### Sicurezza {#security}

#### Abilitazione e disabilitazione di CRX DE Lite {#enabling-and-disabling-crx-de-lite}

Per ulteriori informazioni, vedere [Abilitazione del CRXDE Lite in AEM](/help/sites-administering/enabling-crxde-lite.md).

### Archivio dati raccolta oggetti inattivi {#data-store-garbage-collection}

Per ulteriori informazioni, vedere [Raccolta di oggetti inattivi nell&#39;archivio dati](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection).

### Integrazione di Analytics e Target {#analytics-and-target-integration}

Per informazioni, vedere [Scelta  Adobe Analytics e  Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script).

### Single Sign On {#single-sign-on}

#### Invia intestazione test {#send-test-header}

Per ulteriori informazioni, vedere [Single Sign On](/help/sites-deploying/single-sign-on.md).

## Comandi comuni di gestione dei contenuti AEM cURL {#common-content-manipulation-aem-curl-commands}

Elenco dei comandi cURL AEM per la manipolazione del contenuto.

>[!NOTE]
>
>Gli esempi seguenti presumono che AEM in esecuzione su `localhost` sulla porta `4502` e utilizza l&#39;utente `admin` con password `admin`. I segnaposto dei comandi aggiuntivi sono impostati tra parentesi angolari.

### Gestione pagine {#page-management}

#### Attivazione pagina {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### Disattivazione pagina {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### Attivazione albero {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### Blocca pagina {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Sblocca pagina {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Copia pagina {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### Flussi di lavoro {#workflows}

Per informazioni dettagliate, vedere [Interazione con i flussi di lavoro a livello di programmazione](/help/sites-developing/workflows-program-interaction.md).

### Contenuto Sling {#sling-content}

#### Creare una cartella {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### Eliminare un nodo {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### Spostare un nodo {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Copiare un nodo {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Caricare i file utilizzando Sling PostServlet {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### Caricare i file utilizzando Sling PostServlet e specificando il nome del nodo {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### Carica file che specificano un tipo di contenuto {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### Gestione risorse {#asset-manipulation}

Per informazioni, consultate [Assets HTTP API](/help/assets/mac-api-assets.md).
