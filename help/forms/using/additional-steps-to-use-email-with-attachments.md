---
title: 'Passaggi aggiuntivi per ricevere e-mail con allegato '
description: 'Passaggi aggiuntivi per ricevere e-mail con allegato   '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Impossibile ottenere l&#39;e-mail con gli allegati per AEM Forms sulle piattaforme JEE{#unable-to-get-email-with-attachments}

Il problema si applica alla seguente versione:
* Experience Manager 6.5 Forms

## Problema   {#issue}

L’utente non è in grado di eseguire operazioni quali Invia PDF tramite e-mail o Includi allegati con configurazione di invio.

## Soluzione {#solution}

1. Scarica jar come [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) e decomprimi il file jar scaricato per ottenere il file manifest.

1. Utilizza il file manifesto di `java.mail-1.0.jar` recuperato dal passaggio 1 per creare un nuovo file jar personalizzato, ad esempio `java.mail-1.5.jar`.

1. Apri il file manifesto e sostituisci tutte le occorrenze di `1.5.0` con `1.5.6` e `Bundle-Version: 1.0` con `Bundle-Version:1.5`

1. Crea un nuovo jar personalizzato (`java.mail-1.5.jar`) utilizzando il seguente comando in `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` cartella come:
   `jar -cfm java.mail-1.5.jar manifest.mf`

   Nel comando precedente, *manifest.mf* è il nome del file manifesto e *java.mail-1.5.jar* è il nome del file che verrà creato dopo l&#39;esecuzione del comando precedente.

1. Scarica [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Passa a `http://<server name>:<port>/lc/system/console/bundles`ed elimina il bundle con un nome come `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Installa `java.mail-1.5.jar` ottenuto dalla fase 3.  Questo passaggio riavvia le proprietà sling della distribuzione JEE. Attendi i bundle installati a `http://<server name>:<port>/lc/system/console/bundles` per visualizzare lo stato come **Attivo**.

   >Nota: Nel caso in cui lo stato sia ancora **InActive**, riavviare   **JBoss** dal **Console Servizi**.


1. Installa `javax.mail-1.5.6.redhat-1.jar`file scaricato utilizzando il passaggio 5.

1. Interrompi **JBoss** dal **Console Servizi** e aggiungi le seguenti proprietà a **Sling.properties** file:
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Riavvia **JBoss**.