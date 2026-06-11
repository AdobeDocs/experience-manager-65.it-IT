---
title: Aggiornamento EAP JBoss da 7.4.10 a 7.4.23 per AEM Forms su JEE
description: Passaggi per aggiornare JBoss EAP dall’7.4.10 al 7.4.23 per AEM Forms in ambienti JEE autonomi.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: cb190feb41152d40c36ea2f152ee04cc8c8eba1d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# Aggiornamento EAP JBoss da 7.4.10 a 7.4.23 per AEM Forms su JEE {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## Panoramica {#overview}

Aggiornamento di JBoss EAP dalla versione 7.4.10 alla versione 7.4.23 in un ambiente autonomo AEM Forms su JEE. L’aggiornamento richiede la migrazione dei file di configurazione, delle credenziali del database e del repository di CRX alla nuova installazione JBoss e l’esecuzione di Configuration Manager per completare l’installazione.

## Applicabile a {#applies-to}

Il presente articolo si applica a:

* AEM Forms su JEE in esecuzione su JBoss EAP 7.4.10 in un ambiente autonomo
* Modalità di installazione chiavi in mano e chiavi in mano parziali su Windows e Linux

## Prerequisiti {#prerequisites}

Prima di iniziare:

* Scarica il pacchetto JBoss 7.4.23 dal [portale di distribuzione software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fjboss-eap-7.4.23-1.0.17.zip).
* Assicurati di disporre dell’accesso amministrativo all’ambiente di destinazione.
* Esegui un backup completo dell’installazione JBoss esistente.

## Passaggi {#steps}

Per aggiornare JBoss EAP dall’7.4.10 al 7.4.23, effettua le seguenti operazioni:

### Scarica ed estrai JBoss {#download-and-extract-jboss}

1. Scarica il pacchetto ZIP JBoss 7.4.23 dal portale di distribuzione software Adobe.
1. Estrarre il file ZIP in una directory locale.
1. Rinomina la cartella JBoss estratta in modo che corrisponda esattamente al nome della directory di installazione JBoss esistente.

### Backup dell&#39;installazione esistente {#back-up-the-existing-installation}

1. Crea un backup completo della directory di installazione JBoss corrente.
1. Verificare che il backup includa tutti i file di configurazione e le personalizzazioni.

### Configurare i file di database {#configure-database-files}

1. Passa alla directory di configurazione:

   * Windows: `<JBoss_Home>\standalone\configuration`
   * Linux: `<JBoss_Home>/standalone/configuration`

1. Configurare i file di database in base alla modalità di installazione:

   **Modalità chiavi in mano:**

   1. Rinomina `lc_mysql.xml` in `lc_turnkey.xml`.
   1. Eliminare i seguenti file:

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **Modalità chiavi in mano parziale:**

   1. Mantieni solo il file `lc_db.xml` che corrisponde al motore di database.
   1. Eliminare gli altri due file di configurazione `lc_db.xml`.

### Aggiorna credenziali database {#update-database-credentials}

1. Aprire il file `lc_turnkey.xml` dall&#39;installazione JBoss di cui è stato eseguito il backup.
1. Copia i seguenti valori:

   * URL origine dati
   * Nome utente database
   * Password del database

1. Aggiornare le voci corrispondenti nel nuovo file `lc_turnkey.xml`.

### Eseguire la migrazione dell’archivio CRX {#migrate-crx-repository}

1. Passa alla seguente directory nella vecchia installazione JBoss:

   `<old_jboss>\bin\`

1. Copia la cartella `crx-quickstart`.
1. Incolla la cartella in:

   `<new_jboss>\bin\`

### Esegui Configuration Manager {#run-configuration-manager}

1. Avvia l’ambiente JBoss aggiornato.
1. Avvia Gestione configurazione LiveCycle (LCM).
1. Eseguire il flusso di lavoro completo di Configuration Manager.
1. Verificare che tutte le attività di configurazione siano state completate correttamente.

### Convalida post-aggiornamento {#post-upgrade-validation}

Dopo l’aggiornamento, conferma quanto segue:

* Tutti i servizi sono stati avviati correttamente.
* Verifica della connettività del database.
* La funzionalità dell’applicazione viene convalidata.
