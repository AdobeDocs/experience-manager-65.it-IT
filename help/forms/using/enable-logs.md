---
title: Abilitare la registrazione per i moduli HTML5
seo-title: Abilitare la registrazione per i moduli HTML5
description: L'utilità logger consente di registrare un modulo e consente di eseguire il debug dei problemi relativi al modulo.
seo-description: L'utilità logger consente di registrare un modulo e consente di eseguire il debug dei problemi relativi al modulo.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 6%

---


# Abilita registrazione per moduli HTML5{#enable-logging-for-html-forms}

È possibile configurare l&#39;utilità di registrazione per avviare la creazione di registri per i moduli HTML5. L&#39;utilità logger ha vari livelli, è possibile impostare un livello in base ai requisiti. I moduli HTML5 hanno componenti server e client. Potete configurare i registri per entrambi i componenti.

## Configurazione della registrazione lato server {#configuring-server-side-logging}

Per configurare i registri lato server, effettuate le seguenti operazioni:

1. Passa a `https://'[server]:[port]'/system/console/configMgr`. Individuate e aprite l&#39;opzione *Configurazione del logger di registrazione di Apple Sling*. Viene visualizzata una finestra di dialogo:

   ![ Apace Sling logging logger, finestra di dialogo di configurazione](assets/logconfig.png)

   Opzione di configurazione del logger di registrazione di Apace Sling

1. Modificare il **Livello di registro** in **Debug**.

1. Specificare il nome e il percorso del **file di registro**.

   >[!NOTE]
   >
   >Per generare i registri nella directory di registro dei moduli HTML5, aggiungere ../logs/ prima del nome del file.

1. Modificate **Logger** in **HTMLFormsPerfLogger**. Fai clic su **Salva**.

## Configurazione della registrazione client {#configuring-client-logging}

Per abilitare la registrazione lato client nei moduli HTML5 è possibile utilizzare i metodi seguenti:

* Utilizzo del parametro di richiesta denominato `log`
* Utilizzo di CQ Configuration Manager

### Abilitazione della registrazione mediante il parametro di richiesta {#enabling-logging-using-request-parameter}

Utilizzando questo metodo, potete generare file di registro per una particolare richiesta. Il nome del parametro di richiesta è `log. L’URL del registro è il seguente:

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

La configurazione del registro è composta dal livello di registro e dalla categoria logger.

#### Destinazione registro {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>Destinazione registro</strong></th>
   <th><strong>Descrizione</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>I registri sono indirizzati al browser <strong>Console</strong></td>
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
   <td>1</td>
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

#### Categorie di registri {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>Categoria registro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>una sessione lavagna </td>
   <td>xfa (registri relativi ai motori di script)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView (registri relativi ai motori di layout)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf (registri relativi alle prestazioni)<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Configurazione del registro {#log-configuration}

Nell’URL del registro, il parametro della stringa della query di configurazione del registro è definito come segue:

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
   <td>Destinazione: Livello server<br /> xfa: Livello INFO<br /> xfaView: DEBUG<br /> livello xfaPerf: TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Il livello di registro predefinito per ciascuna categoria di registro a (xfa), b (xfaView) e c (xfaPerf) è 2 (ERROR). Di conseguenza, per la configurazione del registro: 2-b6, i livelli di registro per le diverse categorie sono:
>a (xfa): 2 (ERRORE di livello predefinito)
>b (xfaView): 6 (TRACE specificato dall&#39;utente)
>a (xfaPerf): 2 (ERRORE di livello predefinito)

### Abilitazione dell&#39;accesso tramite Configuration Manager {#enabling-logging-using-configuration-manager}

Se utilizzate Configuration Manager per abilitare la registrazione, vengono generati dei registri per ogni richiesta di rendering finché la registrazione non viene nuovamente disattivata.

1. Accedete a CQ Configuration Manager all&#39;indirizzo `https://'[server]:[port]'/system/console/configMgr` ed effettuate l&#39;accesso con le credenziali di amministratore.
1. Cercare e fare clic su **Configurazioni Forms mobili**.
1. Nella casella di testo Opzioni debug, immettere le configurazioni del registro come descritto nella sezione precedente, ad esempio **2-a4-b5-c6**

   ![Configurazione dei moduli](assets/forms_configuration.png)

   Configurazione dei moduli

## Caricamento dei registri {#uploading-logs}

Se la destinazione è impostata su 1, tutti i messaggi del registro script client vengono indirizzati alla console. Se un amministratore richiede questi registri insieme ai registri del server, imposta il livello di destinazione su 2. A questo livello, tutti i registri vengono raccolti in un oggetto JS sul lato client e, se viene eseguito il rendering del modulo con il profilo predefinito, nella barra degli strumenti viene visualizzato un pulsante **Invia registri** a sinistra di **Evidenzia campi esistenti**. Quando l&#39;utente fa clic sul collegamento, tutti i registri raccolti vengono inviati al server e registrati nel file di registro degli errori configurato sul server.

Per impostazione predefinita, tutte le informazioni vengono aggiunte al file error.log nella directory /crx-repository/logs/.

Per modificare il percorso e il nome del file di registro:

1. Accedete a Configuration Manager come amministratore. L&#39;URL predefinito di Configuration Manager è `https://'[server]:[port]'/system/console/configMgr`.
1. Fare clic su **Configurazione del log di registrazione Apache Sling**. Viene visualizzata una finestra di dialogo.

   ![logconfig-1](assets/logconfig-1.png)

1. Modificate il **Livello di registro** in Debug.

1. Specificare percorso e nome del **file di registro**.

   >[!NOTE]
   >
   >Per creare file di registro nella stessa directory in cui sono conservati gli altri file di registro, specificare ../logs/&lt;nomefile> nella proprietà File di registro.

1. Modificate **Logger** in **HTMLFormsPerfLogger** e fate clic su **Salva**.
