---
title: Avvio e arresto riga di comando
seo-title: Command Line Start and Stop
description: Scopri come avviare e arrestare l’AEM dalla riga di comando.
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
ht-degree: 0%

---

# Avvio e arresto riga di comando{#command-line-start-and-stop}

## Avvio di Adobe Experience Manager dalla riga di comando {#starting-adobe-experience-manager-from-the-command-line}

Il `start` script disponibile in *il &lt;cq-installation>/bin* directory. Vengono fornite sia le versioni Unix che Windows. Lo script avvia l’istanza installata in *&lt;cq-installation>* directory.

Queste due versioni supportano un elenco di variabili di ambiente che possono essere utilizzate per avviare e regolare l’istanza dell’AEM.

<table>
 <tbody>
  <tr>
   <td><strong>Variabile di ambiente </strong></td>
   <td><strong>Descrizione </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>Porta TCP utilizzata per gli script di stato e di arresto<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>Nome host<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>Interfaccia a cui il server deve essere in ascolto<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>Modalità di esecuzione separate da virgola<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Nome del file jar<br /> </td>
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
>Tieni presente che alcune modalità di esecuzione, tra cui authoring e pubblicazione, devono essere impostate prima di iniziare l’AEM e non possono essere modificate in seguito. Prima di configurare un’istanza AEM da utilizzare nella produzione, consulta la sezione [documentazione sulle modalità di esecuzione](/help/sites-deploying/configure-runmodes.md) per i dettagli.

### Esempio di script start.bat per piattaforma Windows {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Esempio di script di avvio della piattaforma Unix {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>Lo script di avvio avvia Quickstart per AEM installato in *il &lt;cq-installation>/app* cartella.

## Interruzione di Adobe Experience Manager {#stopping-adobe-experience-manager}

Per interrompere l&#39;AEM, effettuare una delle seguenti operazioni:

* A seconda della piattaforma in uso:

   * Se l&#39;AEM è stato avviato da uno script o dalla riga di comando, premere **CTRL+C** per arrestare il server.
   * Se è stato utilizzato lo script di avvio in UNIX, è necessario utilizzare lo script di arresto per arrestare l&#39;AEM.

* Se hai avviato AEM facendo doppio clic sul file jar, fai clic sul pulsante **On** nella finestra di avvio (il pulsante diventa quindi **Disattivato**) per arrestare il server.

   ![chlimage_1-63](assets/chlimage_1-63.png)

## Interruzione di Adobe Experience Manager dalla riga di comando {#stopping-adobe-experience-manager-from-the-command-line}

Il `stop` script disponibile in *il &lt;cq-installation>/bin* directory. Vengono fornite sia le versioni Unix che Windows. Lo script arresta l&#39;istanza in esecuzione installata in *&lt;cq-installation>* directory.

### Esempio di script di arresto della piattaforma Unix {#unix-platform-stop-script-example}

```shell
./stop
```

### Esempio di script stop.bat della piattaforma Windows {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

Se desideri semplicemente preconfigurare l’archivio (senza riposizionarlo), devi solo:

* estrarre `repository.xml` nella posizione desiderata

* aggiorna `repository.xml` come richiesto

* creare `bootstrap.properties` e definire `repository.config`

Di nuovo, prima di avviare l&#39;installazione effettiva.
