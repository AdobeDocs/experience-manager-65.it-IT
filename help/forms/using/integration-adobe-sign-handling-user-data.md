---
title: Integrazione con Adobe Sign| Gestione dei dati utente
seo-title: Integrazione con Adobe Sign| Gestione dei dati utente
description: 'null'
seo-description: 'null'
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Integrazione con Adobe Sign| Gestione dei dati utente {#integration-with-adobe-sign-handling-user-data}

AEM Forms si integra con Adobe Sign per abilitare i flussi di lavoro di firma elettronica nei moduli adattivi al fine di elaborare moduli o accordi per flussi di lavoro legali, di vendita, di retribuzione e di gestione delle risorse umane. Consente la firma single e multiutente, flussi di lavoro di firma sequenziali e simultanei, la firma dei moduli come utente anonimo o connesso e diversi modi per l&#39;autenticazione degli utenti.

Quando uno o più firmatari firmano e inviano un modulo adattivo, viene generato un accordo Adobe Sign che include informazioni sui firmatari.

Per ulteriori informazioni sull&#39;integrazione di AEM Forms con Adobe Sign, vedere [Utilizzo di Adobe Sign in un modulo](/help/forms/using/working-with-adobe-sign.md)adattivo.

## Archivio dati utente e data {#data}

Il modulo adattivo abilitato per Adobe Sign include informazioni sui firmatari e può includere altri dati utente raccolti dal modulo adattivo. Il servizio Adobe Sign salva i dati utente con la firma all’interno dell’accordo. L&#39;accordo viene salvato sul server Adobe Sign configurato nei servizi cloud AEM Forms. Inoltre, se il modulo adattivo è configurato per l&#39;utilizzo dell&#39;azione di invio di Forms Portal, i dati del contratto vengono salvati nell&#39;archivio dei dati del portale moduli insieme ai dati del modulo.

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

I dati utente vengono raccolti all&#39;interno del contratto ma non salvati in nessuna delle tabelle dei servizi. Adobe Sign consente agli amministratori di effettuare le proprie scelte sulla gestione dei dati che controllano nel servizio. Gli amministratori della privacy nel servizio Adobe Sign possono elencare o rimuovere gli accordi in base all&#39;indirizzo e-mail di un richiedente.

Adobe Sign offre un’applicazione Web che consente di cercare gli accordi in base ai partecipanti e, se necessario, di eliminarli. Per ulteriori informazioni, vedere [Adobe Sign - Feature: Elimina informazioni](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)utente.

I dati degli accordi per i moduli adattivi configurati per l&#39;utilizzo dell&#39;azione di invio di Forms Portal vengono salvati anche nell&#39;archivio dati del portale moduli. Per accedere ed eliminare dati dall&#39;archivio dati del portale moduli, vedere Portale [Forms| Gestione dei dati](/help/forms/using/forms-portal-handling-user-data.md)utente.
