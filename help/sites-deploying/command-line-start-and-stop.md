---
title: Avvio e interruzione da riga di comando
seo-title: Avvio e interruzione da riga di comando
description: Scopri come avviare e arrestare AEM dalla riga di comando.
seo-description: Scopri come avviare e arrestare AEM dalla riga di comando.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1

---


# Avvio e interruzione da riga di comando{#command-line-start-and-stop}

## Avvio di Adobe Experience Manager dalla riga di comando {#starting-adobe-experience-manager-from-the-command-line}

Lo `start` script è disponibile *nella directory &lt;cq-install>/bin* . Sono disponibili entrambe le versioni Unix e Windows. Lo script avvia l&#39;istanza installata nella directory *&lt;cq-install>* .

Queste due versioni supportano un elenco di variabili di ambiente che possono essere utilizzate per avviare e sintonizzare l’istanza di AEM.

<table>
 <tbody>
  <tr>
   <td><strong>Variabile di ambiente </strong></td>
   <td><strong>Descrizione </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Porta TCP utilizzata per gli script di arresto e stato<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>Nome host<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Interfaccia che il server deve ascoltare<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>Modalità di esecuzione separate da virgola<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nome del file Jarfile<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>Utilizzo di JAAS (se true)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>Percorso della configurazione JAAS<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>Opzioni JVM predefinite<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Alcune modalità di esecuzione, tra cui l’authoring e la pubblicazione, devono essere impostate prima di avviare AEM e non possono essere successivamente modificate. Prima di configurare un’istanza di AEM che dovrebbe essere utilizzata per la produzione, consulta la documentazione [sulle modalità di](/help/sites-deploying/configure-runmodes.md) esecuzione per ulteriori informazioni.

### Esempio di script start.bat della piattaforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Esempio di script di inizio piattaforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>Lo script di avvio avvia l&#39;avvio rapido di AEM installato *nella cartella &lt;cq-install>/app* .

## Stopping Adobe Experience Manager {#stopping-adobe-experience-manager}

Per arrestare AEM, effettuate una delle seguenti operazioni:

* A seconda della piattaforma in uso:

   * Se AEM è stato avviato da uno script o dalla riga di comando, premere **Ctrl+C** per arrestare il server.
   * Se avete utilizzato lo script start in UNIX, dovete utilizzare lo script stop per arrestare AEM.

* Se AEM è stato avviato facendo doppio clic sul file JAR, fate clic sul pulsante **Attivato** nella finestra di avvio (il pulsante diventa **Disattivato**) per arrestare il server.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Arresto di Adobe Experience Manager dalla riga di comando {#stopping-adobe-experience-manager-from-the-command-line}

Lo `stop` script è disponibile *nella directory &lt;cq-install>/bin* . Sono disponibili entrambe le versioni Unix e Windows. Lo script arresta l&#39;istanza in esecuzione installata nella directory *&lt;cq-install>* .

### Esempio di script di arresto piattaforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Esempio di script stop.bat della piattaforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Per preconfigurare la directory archivio (senza rimuoverla) è sufficiente:

* extract `repository.xml` to the required location

* aggiornamento `repository.xml` come richiesto

* creare `bootstrap.properties` e definire `repository.config`

Di nuovo, prima di avviare l&#39;installazione effettiva.

