---
title: Configurare la password amministratore durante l'installazione
seo-title: Configurare la password amministratore durante l'installazione
description: Scoprite come modificare la password amministratore nell'installazione AEM.
seo-description: Scoprite come modificare la password amministratore nell'installazione AEM.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Configurare la password amministratore durante l&#39;installazione{#configure-the-admin-password-on-installation}

## Panoramica {#overview}

Dalla versione 6.3, AEM consente di impostare la password amministratore tramite la riga di comando al momento dell&#39;installazione di una nuova istanza.

Con le versioni precedenti di AEM, dopo l’installazione era necessario modificare la password dell’account amministratore, insieme alla password per diverse altre console.

Questa funzione consente di impostare una nuova password amministratore per l&#39;archivio e il Motore servlet durante l&#39;installazione di un&#39;istanza AEM, eliminando così la necessità di farlo manualmente in seguito.

>[!CAUTION]
>
>Nota: la funzione non copre la console Felix, per la quale la password deve essere modificata manualmente. Per ulteriori informazioni, vedere la sezione [Elenco di controllo della sicurezza ](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts) pertinente.

## Come Lo Uso? {#how-do-i-use-it}

Questa funzione si attiva automaticamente se si sceglie di installare AEM tramite la riga di comando, invece di fare doppio clic sul JAR da un file system Explorer.

La sintassi generale per l&#39;esecuzione di un&#39;istanza AEM dalla riga di comando è la seguente:

```shell
java -jar aem6.3.jar
```

Dopo aver eseguito l&#39;istanza dalla riga di comando, vi verrà presentata l&#39;opzione per cambiare la password amministratore durante il processo di installazione:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>La richiesta di modifica della password amministratore verrà visualizzata solo durante l&#39;installazione di una nuova istanza AEM.

## Utilizzo del flag -nointeractive {#using-the-nointeractive-flag}

Potete anche scegliere di specificare la password da un file delle proprietà. A tale scopo, è necessario utilizzare il flag `-nointeractive` combinato con la proprietà di sistema`-Dadmin.password.file`.

Di seguito è riportato un esempio:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

La password all&#39;interno del file `passwordfile.properties` deve avere il formato seguente:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Se si utilizza semplicemente il parametro `-nointeractive` senza la proprietà di sistema `-Dadmin.password.file`, AEM utilizzare la password amministratore predefinita senza chiedere di modificarla, in sostanza replicando il comportamento delle versioni precedenti. Questa modalità non interattiva può essere utilizzata per le installazioni automatizzate utilizzando la riga di comando in uno script di installazione.

