---
title: Abilita registrazione per moduli HTML5
description: L'utilità logger consente di registrare un modulo e di eseguire il debug dei problemi correlati ai moduli.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---

# Abilita registrazione per moduli HTML5{#enable-logging-for-html-forms}

È possibile configurare l&#39;utilità logger per avviare la creazione di registri per i moduli HTML5. L&#39;utilità logger dispone di vari livelli, è possibile impostare un livello in base alle proprie esigenze. HTML5 Forms dispone di componenti server e client. Puoi configurare i registri per entrambi i componenti.

## Configurazione della registrazione lato server {#configuring-server-side-logging}

Per configurare i registri lato server, effettua le seguenti operazioni:

1. Vai a `https://'[server]:[port]'/system/console/configMgr`. Individua e apri l&#39;opzione *Configurazione logger di accesso Sling*. Viene visualizzata una finestra di dialogo:

   Finestra di dialogo dell&#39;opzione di configurazione del logger di registrazione di Sling ![ dell&#39;interfaccia](assets/logconfig.png)

   Opzione di configurazione del logger di registrazione di accesso Sling

1. Cambia il **livello di registro** in **debug**.

1. Specificare il nome e il percorso del **file di log**.

   >[!NOTE]
   >
   >Per generare i registri nella directory dei registri di HTML5 forms, aggiungere ../logs/ prima del nome del file.

1. Cambia **Logger** in **HTMLFormsPerfLogger**. Fai clic su **Salva**.

## Configurazione della registrazione client {#configuring-client-logging}

Per abilitare la registrazione lato client nei moduli HTML5, puoi utilizzare i seguenti metodi:

* Utilizzo del parametro della richiesta denominato `log`
* Utilizzo di CQ Configuration Manager

### Abilitazione della registrazione tramite il parametro di richiesta {#enabling-logging-using-request-parameter}

Utilizzando questo metodo, puoi generare i registri per una particolare richiesta. Il nome del parametro della richiesta è `log`. L’URL del registro è il seguente:

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

La configurazione del registro è costituita dal livello del registro e dalla categoria del logger.

#### Log Destination {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>Log Destination</strong></th>
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
   <td>Entrambe le opzioni precedenti<br /> </td>
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
   <td>FATALE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
   <td>ERRORE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>AVVERTENZA<br type="_moz" /> </td>
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
   <td>TUTTI<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### Categorie logger {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>Categoria registro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>a</td>
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

#### Configurazione registro {#log-configuration}

Nell’URL del registro, il parametro della stringa di query per la configurazione del registro è definito come segue:

`{destination}-{a level}-{b level}-{c level}`

Ad esempio:

<table>
 <tbody>
  <tr>
   <th>Configurazione registro</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>Destinazione: Server<br /> livello xfa: INFO<br /> livello xfaView: DEBUG<br /> livello xfaPerf: TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Il livello di registro predefinito per ogni categoria di registro a (xfa), b (xfaView) e c (xfaPerf) è 2 (ERROR). Di conseguenza, per la configurazione del registro: 2-b6, i livelli del registro per le diverse categorie sono:
>a (xfa): 2 (errore di livello predefinito)
>b (xfaView): 6 (TRACE specificato dall&#39;utente)
>a (xfaPerf): 2 (errore di livello predefinito)

### Abilitazione della registrazione tramite Configuration Manager {#enabling-logging-using-configuration-manager}

Se utilizzi Configuration Manager per abilitare la registrazione, i registri vengono generati per ogni richiesta di rendering fino a quando la registrazione non viene nuovamente disabilitata.

1. Accedi a CQ Configuration Manager all&#39;indirizzo `https://'[server]:[port]'/system/console/configMgr` e accedi con le credenziali di amministratore.
1. Cerca e fai clic su **Configurazioni Forms mobile**.
1. Nella casella di testo Opzioni debug, immettere le configurazioni del registro come descritto nella sezione precedente, ad esempio **2-a4-b5-c6**

   ![Configurazione Forms](assets/forms_configuration.png)

   Configurazione dei moduli

## Caricamento dei registri {#uploading-logs}

Se la destinazione è impostata su 1, tutti i messaggi di registro degli script client vengono indirizzati alla console. Se un amministratore richiede questi registri insieme ai registri del server, imposta il livello di destinazione su 2. A questo livello, tutti i registri vengono raccolti in un oggetto JS sul lato client e se il rendering del modulo viene eseguito con il profilo predefinito, a sinistra del pulsante **Evidenzia campi esistenti** nella barra degli strumenti viene visualizzato il pulsante **Invia registri**. Quando l’utente fa clic sul collegamento, tutti i registri raccolti vengono pubblicati sul server e registrati nel file di registro degli errori configurato.

Per impostazione predefinita, tutte le informazioni vengono aggiunte al file error.log nella directory /crx-repository/logs/.

Per modificare la posizione e il nome del file di registro:

1. Accedere a Configuration Manager come amministratore. L&#39;URL predefinito di Configuration Manager è `https://'[server]:[port]'/system/console/configMgr`.
1. Fai clic su **Configurazione logger registrazione Sling Apache**. Viene visualizzata una finestra di dialogo.

   ![logconfig-1](assets/logconfig-1.png)

1. Cambia il **livello di registro** in Debug.

1. Specificare il percorso e il nome del **file di log**.

   >[!NOTE]
   >
   >Per creare i registri nella stessa directory in cui sono conservati altri file di registro, specificare ../logs/&lt;nomefile> nella proprietà File di registro.

1. Cambia il **Logger** in **HTMLFormsPerfLogger** e fai clic su **Salva**.
