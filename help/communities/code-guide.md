---
title: Linee guida sulla codifica
seo-title: Linee guida sulla codifica
description: Linee guida, suggerimenti e trucchi per gli sviluppatori di Communities
seo-description: Linee guida, suggerimenti e trucchi per gli sviluppatori di Communities
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Linee guida sulla codifica {#coding-guidelines}

## Linee guida, suggerimenti e trucchi {#guidelines-tips-and-tricks}

L&#39;utilizzo di AEM Communities si è evoluto passando dall&#39;essere fortemente dipendenti dalle pagine Java Server alla flessibilità nella scelta di modelli di linguaggi di script in cui logica aziendale, stile e contenuto delle pagine sono diversi l&#39;uno dall&#39;altro.

Un&#39;ulteriore flessibilità nell&#39;utilizzo dei contenuti generati dall&#39;utente (UGC) è garantita dall&#39;API SocialResourceProvider, che elimina la necessità di conoscere quale opzione [SRP](srp.md) è stata scelta per la distribuzione.

Di seguito sono riportate diverse linee guida e procedure ottimali per gli sviluppatori di AEM Communities:

### Codice {#code}

* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - come evitare la scrittura di un&#39;applicazione che funziona solo quando UGC viene memorizzato in JCR (JSRP).
* [Refactoring](socialutils.md) SocialUtils - metodi di utilità per SRP che sostituiscono SocialUtils.
* [Convenzioni](naming-conventions.md) di denominazione - convenzioni di denominazione per classi Java personalizzate.

### Script {#scripts}

* [Componenti](sideloading.md) di sideloading Communities: procedura per aggiungere dinamicamente un componente dopo il caricamento della pagina.
* [Editor Rich Text Essentials](rte.md) - Come personalizzare l&#39;interfaccia utente RTF fornita ai membri per la pubblicazione di contenuti.

### IDE {#ide}

* [Utilizzo di Maven for Communities](maven.md) - come includere l&#39;API Jar di Communities.
* [Refactoring](socialutils.md) SocialUtils - metodi di utilità per SRP che sostituiscono SocialUtils.

