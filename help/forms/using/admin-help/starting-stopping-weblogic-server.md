---
title: Avvio e arresto del server WebLogic
seo-title: Avvio e arresto del server WebLogic
description: Diverse procedure richiedono l'avvio o l'arresto dell'istanza di WebLogic Server in cui si desidera distribuire moduli AEM. Questo documento descrive come avviare e arrestare il server WebLogic.
seo-description: Diverse procedure richiedono l'avvio o l'arresto dell'istanza di WebLogic Server in cui si desidera distribuire moduli AEM. Questo documento descrive come avviare e arrestare il server WebLogic.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---


# Avvio e arresto del server WebLogic {#starting-and-stopping-weblogic-server}

Diverse procedure richiedono l&#39;avvio o l&#39;arresto dell&#39;istanza di WebLogic Server in cui si desidera distribuire moduli AEM. Verificare che WebLogic Server sia arrestato o in esecuzione, a seconda dell&#39;attività in esecuzione.

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
   <td><p>Distribuzione di prodotti AEM moduli</p></td>
   <td><p>In esecuzione</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Se si esegue WebLogic Server su Red Hat® Enterprise Linux Advanced Server 4.0, impostare la variabile di ambiente `LD_ASSUME_KERNEL` su 2.4.19 utilizzando il comando `export LD_ASSUME_KERNEL=2.4.19`. Quindi, eseguire WebLogic Server dalla stessa shell in cui si imposta la variabile di ambiente.

## Avvia server WebLogic {#start-weblogic-server}

1. Da un prompt dei comandi, andate a *[host dell&#39;appserver]*/user_projects/domain/*[appserverdomain]*.
1. Digitate il comando seguente:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Arrestare il server WebLogic {#stop-weblogic-server}

1. Avviate la console di amministrazione del server WebLogic digitando `https://[host name]:7001/console` nella riga URL di un browser Web.
1. Effettuate l&#39;accesso digitando il nome utente e la password utilizzati per creare la configurazione WebLogic, quindi fate clic su Accesso.
1. In Centro modifiche, fate clic su Blocca e modifica.
1. In Struttura dominio, fare clic su Ambiente > Server.
1. Fare clic su AdminServer e, nel riquadro Impostazioni per AdminServer, fare clic sulla scheda Controllo.
1. Assicurarsi che AdminServer sia selezionato nella tabella Stato server e fare clic su Arresto.
1. Selezionare Al completamento del lavoro per arrestare correttamente il server o selezionare Forza arresto per arrestare immediatamente il server senza completare le attività in corso.
1. Nel riquadro Assistente ciclo di vita server fare clic su Sì per completare l&#39;arresto.

La console di amministrazione del server WebLogic non è più disponibile ed è disponibile il prompt dei comandi da cui è stato eseguito il comando start.

## Avvia console di amministrazione WebLogic {#start-weblogic-administration-console}

1. Se WebLogic Admin Server non è già in esecuzione, dal prompt dei comandi andare alla directory *[appserver principale]\user_projects\domains\[domainname]* e immettere il comando seguente:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Accedete alla console di amministrazione del server WebLogic digitando `https://[host name]:[port]/console` nella riga URL di un browser Web, dove *[port]* è la porta di ascolto non sicura. Per impostazione predefinita, questo valore della porta è 7001.
1. Nella schermata di accesso, digitate il nome utente e la password dell’amministratore e fate clic su Accedi.

## Avvia Node Manager {#start-node-manager}

1. Verificare che WebLogic Server sia in esecuzione.
1. Da un nuovo prompt dei comandi, andare a *[host dell&#39;appserver]*/server/bin.
1. Digitate il comando seguente:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Arresta Node Manager {#stop-node-manager}

Dopo aver chiuso WebLogic Server, è possibile chiudere il prompt dei comandi da cui si è chiamato Node Manager.

## Avviare un server gestito WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Questa attività può essere eseguita solo dopo la creazione di un dominio WebLogic e di un server gestito.

1. Verificare che WebLogic Server e Node Manager siano in esecuzione.
1. Avviate la console di amministrazione del server WebLogic digitando `https://host name]:[port]`/console` nella riga URL di un browser Web.
1. In Struttura dominio, fare clic su Ambiente > Server.
1. Nel riquadro a destra, fare clic sulla scheda Controllo.
1. Selezionare il server gestito da avviare.
1. Fare clic sul pulsante Start sotto il server gestito che si desidera avviare.

## Arrestare un server gestito WebLogic {#stop-a-weblogic-managed-server}

1. Avviate la console di amministrazione del server WebLogic digitando `https://`*[nome host]:[porta ]*`/console` nella riga URL di un browser Web.
1. In Struttura dominio, fare clic su Ambiente > Server.
1. Nel riquadro a destra, fare clic sulla scheda Controllo.
1. Selezionare il server gestito che si desidera arrestare.
1. Fare clic sul pulsante Arresto sotto il server gestito che si desidera arrestare.
1. Selezionare Al completamento del lavoro per arrestare correttamente il server o selezionare Forza arresto per arrestare immediatamente il server senza completare le attività in corso.
1. Nel riquadro Assistente ciclo di vita server fare clic su Sì per completare l&#39;arresto.

