---
title: Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
source-git-commit: 0142b46d087d34707b09a1f172910c8b287b839d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 4%

---

# Impossibile utilizzare Experience Manager Forms con alcune versioni di Oracle JDK {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

Il problema si applica alle seguenti versioni:

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## Problema   {#issue}

L’utente riscontra la seguente eccezione:
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## Motivo {#reason}

L’eccezione si verifica quando si esegue Experience Manager Forms con la versione JDK (Java Development Kit) di Oracle maggiore o uguale alle seguenti versioni:

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

La versione di Java sopra e le versioni successive includono nuovi limiti di elaborazione XML nella JVM (Java Virtual Machine) che causano il mancato funzionamento di alcune operazioni specifiche di Forms.

## Soluzione alternativa {#workaround}

1. Arresta il server Experience Manager Forms.
1. Configura il seguente argomento JVM per il server applicazioni:

   `-Djdk.xml.xpathExprOpLimit=2000`

   Imposta la proprietà di sistema in JVM a un valore ragionevolmente alto in modo che il limite predefinito non venga raggiunto.

1. Avvia il server Experience Manager Forms.
