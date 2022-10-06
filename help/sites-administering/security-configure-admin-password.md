---
title: Configurare la password amministratore durante l’installazione
seo-title: Configure the Admin Password on Installation
description: Scopri come modificare la password dell’amministratore nell’installazione AEM.
seo-description: Learn how to change the Admin Password on AEM Installation.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Configurare la password amministratore durante l’installazione{#configure-the-admin-password-on-installation}

## Panoramica {#overview}

A partire dalla versione 6.3, AEM consente di impostare la password dell’amministratore utilizzando la riga di comando durante l’installazione di una nuova istanza.

Con le versioni precedenti di AEM, dopo l’installazione era necessario modificare la password dell’account amministratore, insieme alla password per diverse altre console.

Questa funzione aggiunge la possibilità di impostare una nuova password amministratore per l&#39;archivio e il Servlet Engine durante l&#39;installazione di un&#39;istanza AEM, eliminando così la necessità di farlo manualmente in seguito.

>[!CAUTION]
>
>Tieni presente che la funzione non copre la console Felix, per la quale la password deve essere modificata manualmente. Per ulteriori informazioni, consulta la sezione [Sezione Lista di controllo protezione](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## Come La Uso? {#how-do-i-use-it}

Questa funzione si attiva automaticamente se scegli di installare AEM tramite la riga di comando, invece di fare doppio clic sul JAR da un file system explorer.

La sintassi generale per l&#39;esecuzione di un&#39;istanza AEM dalla riga di comando è:

```shell
java -jar aem6.3.jar
```

Dopo aver eseguito l’istanza dalla riga di comando, ti verrà offerta l’opzione di cambiare la password dell’amministratore durante il processo di installazione:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>La richiesta di modifica della password dell&#39;amministratore verrà visualizzata solo durante l&#39;installazione di una nuova istanza AEM.

## Utilizzo del flag -nointerattivo {#using-the-nointeractive-flag}

Puoi anche scegliere di specificare la password da un file di proprietà. A tale scopo, utilizza le `-nointeractive` flag combinato con`-Dadmin.password.file` proprietà di sistema.

Di seguito è riportato un esempio:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

La password all&#39;interno della `passwordfile.properties` il file deve avere il formato seguente:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Se si utilizza semplicemente il `-nointeractive` senza `-Dadmin.password.file` proprietà di sistema, AEM utilizzerà la password amministratore predefinita senza chiedere di cambiarla, essenzialmente replicando il comportamento delle versioni precedenti. Questa modalità non interattiva può essere utilizzata per le installazioni automatizzate utilizzando la riga di comando in uno script di installazione.
