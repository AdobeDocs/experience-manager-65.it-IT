---
title: Abilitare la registrazione per i moduli HTML5
seo-title: Abilitare la registrazione per i moduli HTML5
description: L'utilità logger abilita la registrazione di un modulo e consente di eseguire il debug dei problemi relativi al modulo.
seo-description: L'utilità logger abilita la registrazione di un modulo e consente di eseguire il debug dei problemi relativi al modulo.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
feature: Forms Mobile
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 6%

---

# Abilita la registrazione per i moduli HTML5{#enable-logging-for-html-forms}

È possibile configurare l&#39;utilità logger per iniziare a creare registri per i moduli HTML5. L&#39;utilità logger ha vari livelli, è possibile impostare un livello in base alle proprie esigenze. I moduli HTML5 hanno componenti server e client. Puoi configurare i registri per entrambi i componenti.

## Configurazione della registrazione lato server {#configuring-server-side-logging}

Esegui i seguenti passaggi per configurare i registri lato server:

1. Passa a `https://'[server]:[port]'/system/console/configMgr`. Individua e apri l&#39;opzione *Configurazione del logger di registrazione di Apache Sling* . Viene visualizzata una finestra di dialogo:

   ![ Finestra di dialogo delle opzioni di configurazione del logger di registrazione di Apache Sling](assets/logconfig.png)

   Opzione di configurazione del logger di registrazione di Apache Sling

1. Cambia il **Livello di log** in **Debug**.

1. Specificare il nome e il percorso del **File di log**.

   >[!NOTE]
   >
   >Per generare i registri nella directory di registro dei moduli HTML5, aggiungi ../logs/ prima del nome del file.

1. Cambia **Logger** in **HTMLFormsPerfLogger**. Fai clic su **Salva**.

## Configurazione della registrazione client {#configuring-client-logging}

Per abilitare la registrazione lato client nei moduli HTML5 è possibile utilizzare i seguenti metodi:

* Utilizzando il parametro della richiesta denominato `log`
* Utilizzo di CQ Configuration Manager

### Abilitazione della registrazione utilizzando il parametro di richiesta {#enabling-logging-using-request-parameter}

Utilizzando questo metodo, puoi generare registri per una particolare richiesta. Il nome del parametro della richiesta è `log`. L’URL del registro è il seguente:

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

La configurazione del registro è composta dal livello di registro e dalla categoria logger.

#### Destinazione log {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>Destinazione log</strong></th>
   <th><strong>Descrizione</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>I registri vengono indirizzati al browser <strong>Console</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>I registri vengono raccolti in un oggetto JavaScript sul lato client e possono essere inviati a <strong>Server</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>Entrambe le opzioni sopra riportate<br /> </td>
  </tr>
 </tbody>
</table>

#### Livelli di registro {#log-levels}

<table>
 <tbody>
  <tr>
   <th>Livello registro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>0</td>
   <td>DISATTIVATO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>1</td>
   <td>FATAL<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>ERRORE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>AVVISO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>INFO<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>DEBUG<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>TRACE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>ALL<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Categorie di logger {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>Categoria registro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>una sessione lavagna </td>
   <td>xfa (registri relativi al motore di script)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView (registri relativi al motore di layout)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf (registri relativi alle prestazioni)<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Configurazione del registro {#log-configuration}

Nell’URL del registro, il parametro della stringa di query per la configurazione del registro è definito come segue:

`{destination}-{a level}-{b level}-{c level}`

Esempio:

<table>
 <tbody>
  <tr>
   <th>Configurazione del registro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>Destinazione: Livello server<br /> xfa: Livello INFO<br /> xfaView: Livello DEBUG<br /> xfaPerf: TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Il livello di log predefinito per ogni categoria di log a (xfa), b (xfaView) e c (xfaPerf) è 2 (ERROR). Di conseguenza, per la configurazione del registro: 2-b6, i livelli di log per le diverse categorie sono:
>a (xfa): 2 (livello predefinito ERROR)
>b (xfaView): 6 (TRACE specificato dall&#39;utente)
>a (xfaPerf): 2 (livello predefinito ERROR)

### Abilitazione della registrazione tramite Configuration Manager {#enabling-logging-using-configuration-manager}

Se si utilizza Configuration Manager per abilitare la registrazione, vengono generati i registri per ogni richiesta di rendering fino a quando la registrazione non viene nuovamente disabilitata.

1. Accedi a CQ Configuration Manager all&#39;indirizzo `https://'[server]:[port]'/system/console/configMgr` e accedi con le credenziali di amministratore.
1. Cerca e fai clic su **Configurazioni Forms mobili**.
1. Nella casella di testo Opzioni di debug, immetti le configurazioni del registro come descritto nella sezione precedente, ad esempio **2-a4-b5-c6**

   ![Configurazione dei moduli](assets/forms_configuration.png)

   Configurazione dei moduli

## Caricamento dei registri {#uploading-logs}

Se la destinazione è impostata su 1, tutti i messaggi di log degli script client vengono indirizzati alla console. Se un amministratore richiede questi registri insieme ai registri del server, imposta il livello di destinazione su 2. A questo livello, tutti i registri vengono raccolti in un oggetto JS sul lato client e, se viene eseguito il rendering del modulo con il profilo predefinito, viene visualizzato un pulsante **Invia registri** a sinistra del pulsante **Evidenzia campi esistenti** nella barra degli strumenti. Quando l&#39;utente fa clic sul collegamento, tutti i registri raccolti vengono inviati al server e vengono registrati nel file di registro degli errori configurato sul server.

Per impostazione predefinita, tutte le informazioni vengono aggiunte al file error.log nella directory /crx-repository/logs/ .

Per modificare la posizione e il nome del file di log:

1. Accedi a Configuration Manager come amministratore. L’URL predefinito di Configuration Manager è `https://'[server]:[port]'/system/console/configMgr`.
1. Fai clic su **Configurazione logger di registrazione Sling Apache**. Viene visualizzata una finestra di dialogo.

   ![logconfig-1](assets/logconfig-1.png)

1. Cambia il **Livello di log** in Debug.

1. Specificare il percorso e il nome del **File di log**.

   >[!NOTE]
   >
   >Per creare i registri nella stessa directory in cui vengono conservati gli altri file di registro, specifica ../logs/&lt;filename> nella proprietà File di registro.

1. Cambia il **logger** in **HTMLFormsPerfLogger** e fai clic su **Salva**.
