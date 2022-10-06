---
title: Avvio e arresto del server WebLogic
seo-title: Starting and stopping WebLogic Server
description: Diverse procedure richiedono l’avvio o l’arresto dell’istanza di WebLogic Server in cui si desidera distribuire moduli AEM. Questo documento descrive come avviare e arrestare il server WebLogic.
seo-description: Several procedures require you to start or stop the instance of WebLogic Server where you want to deploy AEM forms modules. This document describes how to start and stop the WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---


# Avvio e arresto del server WebLogic {#starting-and-stopping-weblogic-server}

Diverse procedure richiedono l’avvio o l’arresto dell’istanza di WebLogic Server in cui si desidera distribuire moduli AEM. Assicurati che il server WebLogic sia arrestato o in esecuzione, a seconda dell&#39;attività che stai eseguendo.

<table>
 <thead>
  <tr>
   <th><p>Attività</p></th>
   <th><p>Stato WebLogic richiesto</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Creazione di un dominio WebLogic</p></td>
   <td><p>Interrotto</p></td>
  </tr>
  <tr>
   <td><p>Creazione di un server gestito WebLogic</p></td>
   <td><p>In esecuzione</p></td>
  </tr>
  <tr>
   <td><p>Aumento del conteggio dei thread del server</p></td>
   <td><p>In esecuzione</p></td>
  </tr>
  <tr>
   <td><p>Distribuzione di prodotti AEM forms</p></td>
   <td><p>In esecuzione</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se esegui WebLogic Server su Red Hat® Enterprise Linux Advanced Server 4.0, imposta la `LD_ASSUME_KERNEL` variabile di ambiente a 2.4.19 utilizzando il `export LD_ASSUME_KERNEL=2.4.19` comando. Esegui quindi WebLogic Server dalla stessa shell in cui hai impostato questa variabile di ambiente.

## Avvia server WebLogic {#start-weblogic-server}

1. Da un prompt dei comandi, vai a *[root appserver]*/user_projects/domini/*[appserverdomain]*.
1. Immetti il seguente comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Arresta server WebLogic {#stop-weblogic-server}

1. Avvia la console di amministrazione del server WebLogic digitando `https://[host name]:7001/console` nella riga URL di un browser web.
1. Accedi digitando il nome utente e la password utilizzati durante la creazione della configurazione WebLogic, quindi fai clic su Accedi.
1. In Cambia centro fare clic su Blocca e modifica.
1. In Struttura del dominio, fai clic su Ambiente > Server.
1. Fare clic su AdminServer e, nel riquadro Impostazioni per AdminServer, fare clic sulla scheda Controllo.
1. Assicurarsi che AdminServer sia selezionato nella tabella Stato server e fare clic su Arresta.
1. Selezionare Quando il lavoro viene completato per arrestare correttamente il server o selezionare Forza arresto per arrestare immediatamente il server senza completare le attività in corso.
1. Nel riquadro Assistente ciclo di vita server fare clic su Sì per completare l&#39;arresto.

La console di amministrazione del server WebLogic non è più disponibile ed è disponibile il prompt dei comandi da cui è stato eseguito il comando start.

## Avvia la console di amministrazione di WebLogic {#start-weblogic-administration-console}

1. Se WebLogic Admin Server non è già in esecuzione, da un prompt dei comandi, passare a *[root appserver]\user_projects\domains\[nome dominio]* e immettere il comando seguente:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Accedere alla console di amministrazione del server WebLogic digitando `https://[host name]:[port]/console` nella riga URL di un browser web, dove *[porta]* è la porta di ascolto non sicura. Per impostazione predefinita, questo valore di porta è 7001.
1. Nella schermata di accesso, digitare il nome utente e la password dell&#39;amministratore e fare clic su Accesso.

## Avvia Node Manager {#start-node-manager}

1. Assicurati che il server WebLogic sia in esecuzione.
1. Da un nuovo prompt dei comandi, vai a *[root appserver]*/server/bin.
1. Immetti il seguente comando:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Arresta Node Manager {#stop-node-manager}

Dopo aver arrestato il server WebLogic, è possibile chiudere il prompt dei comandi da cui si è chiamato Node Manager.

## Avviare un server gestito WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Questa attività può essere eseguita solo dopo la creazione di un dominio WebLogic e di un server gestito.

1. Assicurati che WebLogic Server e Node Manager siano in esecuzione.
1. Avvia la console di amministrazione del server WebLogic digitando `https://host name]:[port]/console` nella riga URL di un browser web.
1. In Struttura del dominio, fai clic su Ambiente > Server.
1. Nel riquadro di destra, fare clic sulla scheda Controllo.
1. Selezionare il server gestito che si desidera avviare.
1. Fare clic sul pulsante Start sotto il server gestito che si desidera avviare.

## Arresta un server gestito WebLogic {#stop-a-weblogic-managed-server}

1. Avvia la console di amministrazione del server WebLogic digitando `https://`*[nome host]:[porta ]*`/console` nella riga URL di un browser web.
1. In Struttura del dominio, fai clic su Ambiente > Server.
1. Nel riquadro di destra, fare clic sulla scheda Controllo.
1. Selezionare il server gestito che si desidera arrestare.
1. Fare clic sul pulsante Arresto sotto il server gestito che si desidera arrestare.
1. Selezionare Quando il lavoro viene completato per arrestare correttamente il server o selezionare Forza arresto per arrestare immediatamente il server senza completare le attività in corso.
1. Nel riquadro Assistente ciclo di vita server fare clic su Sì per completare l&#39;arresto.

