---
title: Come si riavvia l’SDK per AEM?
description: Best practice per riavviare l’SDK per AEM
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# Riavvio dell’SDK dell’AEM

Se riavvii l’SDK dell’AEM interrompendo i processi Java™, potrebbero verificarsi incoerenze nell’ambiente di sviluppo dell’AEM, come segue:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Riavvia-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## Soluzione

Per riavviare l&#39;SDK per AEM, passare alla finestra di comando attiva e premere il comando `Ctrl + C` per riavviare l&#39;SDK.

Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java™, può causare incongruenze nell’ambiente di sviluppo dell’AEM.
