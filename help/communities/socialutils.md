---
title: Refactoring di SocialUtils
seo-title: SocialUtils Refactoring
description: Il pacchetto com.adobe.cq.social.ugcbase.SocialUtils è stato dichiarato obsoleto in AEM 6.1
seo-description: The package com.adobe.cq.social.ugcbase.SocialUtils was deprecated in AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# Refactoring di SocialUtils {#socialutils-refactoring}

## Pacchetto SocialUtils obsoleto {#socialutils-package-deprecated}

Il pacchetto `com.adobe.cq.social.ugcbase.SocialUtils` è stato dichiarato obsoleto in AEM 6.1.

Nelle tabelle seguenti sono elencati i metodi da utilizzare al posto di `SocialUtils` metodi.

## Pacchetto SocialResourceUtilities  {#socialresourceutilities-package}

| Metodi in com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| CheckPermission booleano(ResourceResolver resolver, Percorso stringa, azione stringa) |  |
| SocialResourceProvider getSocialResourceProvider(risorsa risorsa) |  |
| SocialResourceConfiguration getStorageConfig(risorsa risorsa risorsa) |  |
| Risorsa getUGCResource(ResourceUserResource) |  |
| Risorsa getUGCResource(Resource userResource, ResourceResolverFactory rf) | nuovo |
| Risorsa getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | nuovo |
| Risorsa getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booleano hasModeratePermissions(risorsa Resource) |  |
| String resourceToACLPath(Risorsa di risorsa) |  |
| String resourceToUGCStoragePath(Resource resource) | sostituisce String resourceToUGCPath(Resource resource) |
| Stringa UGCToResourcePath(Risorsa di risorsa) |  |
| Stringa UGCToResourcePath(String ugcPath) | firma del metodo cambiata |
| Stringa UGCToResourcePath(String ugcPath, ResourceResolver) | nuovo |

| Metodi in `com.adobe.cq.social.`utility.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(risorsa risorsa) | sostituisce SocialResourceProvider getConfiguratedProvider(Risorsa) |

## Pacchetto SCFUtilities {#scfutilities-package}

| Metodi in `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| Stringa getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String AbsoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String AbsoluteDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Page getContainPage(Risorsa di risorsa) |
| Stringa getSocialProfileURL(nome utente stringa, risolutore ResourceResolver, pagina) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## Solo per uso interno {#for-internal-use-only}

| booleano canAddNode(Session session, String path) |
|---|
| Stringa createUniqueNameHint(Messaggio stringa) |
| Stringa createUniqueNameHint(Messaggio stringa, int numRandomChars) |
| Stringa generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(Percorso stringa, risolutore ResourceResolver) |
| Stringa getPagePath(Risorsa) |
| String getPagePath(Percorso stringa) |
| Stringa getResourceTypeForIncludedResource(Resource component, String defaultResourceType, String designPropertyName) |
| Stringa getResourceTypeFromDesign(Risorsa, String styleProperty, String defaultValue) |
| isResourceOwner(Resource resource) booleano |
| Stringa mapUGCPath(Risorsa di risorsa) |
| String mapUGCPath(String ugcPath, ResourceResolver) |
| booleano mayPost(ResourceResolver resolver, risorsa Resource) |
| String PrepareUserGeneratedContent(ResourceResolver resolver, Percorso stringa) |

## Metodi non più disponibili {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, Percorso stringa, Tipo nodo stringa) |
|---|
| Resource getResourceAtPath(ResourceResolver resolver, Percorso stringa) |
| Resource getResourceAtPath(ResourceResolver resolver, percorso stringa, String resourceType) |
| Configurazione getStorageCloudServiceConfig(risorsa risorsa risorsa) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booleano mayAccessUGC(ResourceResolver resolver) |
