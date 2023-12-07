---
title: Avvio e arresto del server WebLogic
description: Diverse procedure richiedono l'avvio o l'arresto dell'istanza del server WebLogic in cui si desidera distribuire i moduli AEM forms. Questo documento descrive come avviare e arrestare il server WebLogic.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# Avvio e arresto del server WebLogic {#starting-and-stopping-weblogic-server}

Diverse procedure richiedono l&#39;avvio o l&#39;arresto dell&#39;istanza del server WebLogic in cui si desidera distribuire i moduli AEM forms. Verificare che il server WebLogic sia arrestato o in esecuzione, a seconda dell&#39;attività che si sta eseguendo.

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
   <td><p>Aumento del numero di thread del server</p></td>
   <td><p>In esecuzione</p></td>
  </tr>
  <tr>
   <td><p>Distribuzione dei prodotti AEM forms</p></td>
   <td><p>In esecuzione</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se si esegue WebLogic Server su Red Hat® Enterprise Linux Advanced Server 4.0, impostare `LD_ASSUME_KERNEL` variabile di ambiente al 2.4.19 utilizzando `export LD_ASSUME_KERNEL=2.4.19` comando. Eseguire quindi WebLogic Server dalla stessa shell in cui si imposta la variabile di ambiente.

## Avvia server WebLogic {#start-weblogic-server}

1. Da un prompt dei comandi, passare a *[directory principale del server applicazioni]*/user_projects/domains/*[appserverdomain]*.
1. Immetti il comando seguente:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Arresta server WebLogic {#stop-weblogic-server}

1. Avviare la console di amministrazione del server WebLogic digitando `https://[host name]:7001/console` nella riga URL di un browser web.
1. Accedere digitando il nome utente e la password utilizzati durante la creazione della configurazione WebLogic e quindi fare clic su Accedi.
1. In Cambia centro fare clic su Blocca e modifica.
1. In Struttura dominio, fai clic su Ambiente > Server.
1. Fare clic su AdminServer e nel riquadro Impostazioni per AdminServer fare clic sulla scheda Controllo.
1. Verificare che AdminServer sia selezionato nella tabella Stato server e fare clic su Arresta.
1. Selezionare Quando il lavoro viene completato per arrestare il server in modo corretto oppure selezionare Forza arresto per arrestare immediatamente il server senza completare le attività in corso.
1. Nel riquadro Assistente ciclo di vita server fare clic su Sì per completare l&#39;arresto.

La console di amministrazione del server WebLogic non è più disponibile e il prompt dei comandi da cui è stato eseguito il comando start è disponibile.

## Avvia console di amministrazione WebLogic {#start-weblogic-administration-console}

1. Se WebLogic Admin Server non è già in esecuzione, da un prompt dei comandi passare alla *[directory principale del server applicazioni]\user_projects\domains\[domainname]* e immettere il comando seguente:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Accedere alla console di amministrazione del server WebLogic digitando `https://[host name]:[port]/console` nella riga URL di un browser web, dove *[porta]* è la porta di ascolto non sicura. Per impostazione predefinita, il valore della porta è 7001.
1. Nella schermata di accesso, digita il nome utente e la password dell’amministratore, quindi fai clic su Accedi.

## Avvia Node Manager {#start-node-manager}

1. Verificare che WebLogic Server sia in esecuzione.
1. Da un nuovo prompt dei comandi, vai a *[directory principale del server applicazioni]*/server/bin.
1. Immetti il comando seguente:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Interrompi gestione nodi {#stop-node-manager}

Dopo aver arrestato WebLogic Server, è possibile chiudere il prompt dei comandi dal quale è stato chiamato Node Manager.

## Avviare un server gestito WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Questa attività può essere eseguita solo dopo aver creato un dominio WebLogic e un server gestito.

1. Verificare che il server WebLogic e Node Manager siano in esecuzione.
1. Avviare la console di amministrazione del server WebLogic digitando `https://host name]:[port]/console` nella riga URL di un browser web.
1. In Struttura dominio, fai clic su Ambiente > Server.
1. Nel riquadro destro fare clic sulla scheda Controllo.
1. Selezionare il server gestito che si desidera avviare.
1. Fare clic sul pulsante Start sotto il server gestito che si desidera avviare.

## Arrestare un server gestito WebLogic {#stop-a-weblogic-managed-server}

1. Avviare la console di amministrazione del server WebLogic digitando `https://`*[nome host]:[porta ]*`/console` nella riga URL di un browser web.
1. In Struttura dominio, fai clic su Ambiente > Server.
1. Nel riquadro destro fare clic sulla scheda Controllo.
1. Selezionare il server gestito da arrestare.
1. Fare clic sul pulsante Chiudi sessione sotto il server gestito che si desidera arrestare.
1. Selezionare Quando il lavoro viene completato per arrestare il server in modo corretto oppure selezionare Forza arresto per arrestare immediatamente il server senza completare le attività in corso.
1. Nel riquadro Assistente ciclo di vita server fare clic su Sì per completare l&#39;arresto.

