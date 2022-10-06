---
title: Avvio e interruzione da riga di comando
seo-title: Command Line Start and Stop
description: Scopri come avviare e arrestare AEM dalla riga di comando.
seo-description: Learn how to start and stop AEM from the command line.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# Avvio e interruzione da riga di comando{#command-line-start-and-stop}

## Avvio di Adobe Experience Manager dalla riga di comando {#starting-adobe-experience-manager-from-the-command-line}

La `start` lo script è disponibile in *la &lt;cq-installation>/bin* directory. Vengono fornite sia le versioni Unix che Windows. Lo script avvia l&#39;istanza installata in *&lt;cq-installation>* directory.

Queste due versioni supportano un elenco di variabili di ambiente che possono essere utilizzate per avviare e ottimizzare l&#39;istanza AEM.

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
   <td>Nome del file jarfile<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>Uso di JAAS (se true)<br /> </td>
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
>Tieni presente che alcune modalità di esecuzione, tra cui l’authoring e la pubblicazione, devono essere impostate prima del primo AEM di avvio e non possono essere modificate successivamente. Prima di configurare un&#39;istanza AEM che dovrebbe essere utilizzata in produzione, consulta la [documentazione sulle modalità di esecuzione](/help/sites-deploying/configure-runmodes.md) per i dettagli.

### Esempio di script start.bat di Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Esempio di script di avvio della piattaforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>Lo script di avvio avvia il AEM Quickstart installato in *la &lt;cq-installation>/app* cartella.

## Arresto di Adobe Experience Manager {#stopping-adobe-experience-manager}

Per interrompere AEM, eseguire una delle operazioni seguenti:

* A seconda della piattaforma che utilizzi:

   * Se è stato avviato AEM da uno script o dalla riga di comando, premere **Ctrl+C** per arrestare il server.
   * Se è stato utilizzato lo script di avvio su UNIX, è necessario utilizzare lo script di arresto per arrestare AEM.

* Se hai iniziato AEM facendo doppio clic sul file jar, fai clic sul pulsante **On** pulsante nella finestra di avvio (il pulsante cambia in **Disattivato**) per arrestare il server.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Arresto di Adobe Experience Manager dalla riga di comando {#stopping-adobe-experience-manager-from-the-command-line}

La `stop` lo script è disponibile in *la &lt;cq-installation>/bin* directory. Vengono fornite sia le versioni Unix che Windows. Lo script interrompe l&#39;istanza in esecuzione installata in *&lt;cq-installation>* directory.

### Esempio di script di arresto della piattaforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Esempio di script stop.bat di Windows platform {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Se desideri semplicemente preconfigurare l’archivio (senza rimuoverlo), devi solo:

* estrarre `repository.xml` alla posizione richiesta

* update `repository.xml` come richiesto

* creare `bootstrap.properties` e definire `repository.config`

Di nuovo, prima di avviare l&#39;installazione effettiva.
