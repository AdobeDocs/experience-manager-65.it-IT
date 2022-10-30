---
title: Integrazione con Adobe Sign | Gestione dei dati utente
seo-title: Integration with Adobe Sign | Handling user data
description: Integrazione con Adobe Sign | Gestione dei dati utente
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Integrazione con Adobe Sign | Gestione dei dati utente {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] si integra con[!DNL  Adobe Sign] abilitare i flussi di lavoro di firma elettronica nei moduli adattivi per elaborare moduli o accordi per i flussi di lavoro legali, di vendita, di retribuzione, di gestione delle risorse umane. Consente la firma di utenti singoli e multipli, flussi di lavoro di firma sequenziali e simultanei, la firma di moduli come utente anonimo o connesso e diversi modi per autenticare gli utenti.

Quando un firmatario o più firmatari firmano e inviano un modulo adattivo, un [!DNL Adobe Sign] viene generato un accordo che include informazioni sui firmatari.

Per ulteriori informazioni [!DNL AEM Forms] integrazione con [!DNL Adobe Sign], vedi [Utilizzo di Adobe Sign in un modulo adattivo](/help/forms/using/working-with-adobe-sign.md).

## Archiviazione dati e dati utente {#data}

[!DNL Adobe Sign] il modulo adattivo abilitato include informazioni sui firmatari e può includere altri dati utente raccolti dal modulo adattivo. La [!DNL Adobe Sign] consente di salvare i dati utente con la firma all’interno del contratto. Il contratto viene salvato su [!DNL Adobe Sign] server configurato in [!DNL AEM Forms] servizi cloud. Inoltre, se il modulo adattivo è configurato per utilizzare l’azione di invio di Forms Portal, i dati del contratto vengono salvati nell’archivio dati del portale dei moduli insieme ai dati del modulo.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

I dati utente vengono raccolti all&#39;interno del contratto ma non vengono salvati in nessuna delle tabelle del servizio. [!DNL Adobe Sign] consente agli amministratori di effettuare le proprie scelte sulla gestione dei dati che controllano nel servizio. Amministratori della privacy su [!DNL Adobe Sign] Il servizio può elencare o rimuovere gli accordi in base all&#39;indirizzo e-mail di un richiedente.

[!DNL Adobe Sign] offre un&#39;applicazione web che consente la ricerca di accordi da parte dei partecipanti e, se necessario, l&#39;eliminazione. Per ulteriori informazioni, consulta [Adobe Sign - Funzionalità: Elimina informazioni utente](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

I dati dei contratti per i moduli adattivi configurati per utilizzare l’azione di invio del portale Forms vengono salvati anche nell’archivio dati del portale dei moduli. Per accedere ed eliminare dati dall’archivio dati del portale moduli, vedere [Portale Forms | Gestione dei dati utente](/help/forms/using/forms-portal-handling-user-data.md).
