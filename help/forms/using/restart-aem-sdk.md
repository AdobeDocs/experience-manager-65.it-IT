---
title: Come si riavvia l’SDK per AEM?
description: Best practice per riavviare l’SDK per AEM
role: Admin, Developer, User
feature: Adaptive Forms, Troubleshooting
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# Riavvio dell’SDK dell’AEM

Se riavvii l’SDK dell’AEM interrompendo i processi Java™, potrebbero verificarsi incoerenze nell’ambiente di sviluppo dell’AEM, come segue:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## Soluzione

Per riavviare l&#39;SDK dell&#39;AEM, passare alla finestra di comando attiva e premere `Ctrl + C` per riavviare l&#39;SDK.

Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java™, può causare incongruenze nell’ambiente di sviluppo dell’AEM.
