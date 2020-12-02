---
title: Refactoring SocialUtils
seo-title: Refactoring SocialUtils
description: Il pacchetto com.adobe.cq.social.ugcbase.SocialUtils è stato dichiarato obsoleto in AEM 6.1
seo-description: Il pacchetto com.adobe.cq.social.ugcbase.SocialUtils è stato dichiarato obsoleto in AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Refactoring SocialUtils {#socialutils-refactoring}

## Pacchetto SocialUtils obsoleto {#socialutils-package-deprecated}

Il pacchetto `com.adobe.cq.social.ugcbase.SocialUtils` è stato dichiarato obsoleto in AEM 6.1.

Nelle tabelle seguenti sono elencati i metodi da utilizzare al posto dei metodi `SocialUtils`.

## Pacchetto SocialResourceUtilities {#socialresourceutilities-package}

| Metodi in com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| CheckPermissionBooleano(ResourceResolver resolver, percorso stringa, azione stringa) |  |
| SocialResourceProvider getSocialResourceProvider(risorsa risorsa risorsa) |  |
| SocialResourceConfiguration getStorageConfig(risorsa risorsa risorsa risorsa) |  |
| Resource getUGCResource(Resource userResource) |  |
| Resource getUGCResource(ResourceUserResource, ResourceResolverFactory rrf) | nuovo |
| Resource getUGCResource(ResourceUserResource, ResourceResolverFactory rrf, String resourceTypeHint) | nuovo |
| Resource getUGCResource(ResourceUserResource, String resourceTypeHint) |  |
| boolean hasModeratePermissions(Risorsa risorsa risorsa) |  |
| String resourceToACLPath(Resource Resource) |  |
| String resourceToUGCStoragePath(Resource Resource) | sostituisce String resourceToUGCPath(Resource Resource) |
| Stringa UGCToResourcePath(Risorsa risorsa) |  |
| Stringa UGCToResourcePath(String ugcPath) | firma del metodo modificata |
| String UGCToResourcePath(String ugcPath, ResourceResolver) | nuovo |

| Metodi in `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(risorsa risorsa risorsa) | sostituisce SocialResourceProvider getConfiguratedProvider(risorsa risorsa risorsa) |

## Pacchetto SCFUtilities {#scfutilities-package}

| Metodi in `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String AbsoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String AbsoluteDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Page getContainPage(Risorsa risorsa) |
| String getSocialProfileURL(nome utente stringa, risolutore risorse, pagina pagina) |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## Solo per uso interno {#for-internal-use-only}

| boolean canAddNode(Session session, String path) |
|---|
| String createUniqueNameHint(messaggio stringa) |
| String createUniqueNameHint(messaggio stringa, int numRandomChars) |
| String generateRandomString(lunghezza int) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(Percorso stringa, Risolutore risorse) |
| String getPagePath(Risorsa risorsa) |
| String getPagePath(percorso stringa) |
| String getResourceTypeForIndedResource(Componente risorsa, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource resource, String styleProperty, String defaultValue) |
| isResourceOwner(Risorsa risorsa risorsa) booleana |
| String mapUGCPath(Risorsa risorsa) |
| String mapUGCPath(String ugcPath, ResourceResolver) |
| canPostBooleano(ResourceResolver, Resource Resource) |
| String PrepareUserGeneratedContent(ResourceResolver, percorso stringa) |

## Metodi non più disponibili {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, percorso stringa, tipo nodoStringa) |
|---|
| Resource getResourceAtPath(ResourceResolver, percorso stringa) |
| Resource getResourceAtPath(ResourceResolver, percorso stringa, String resourceType) |
| Configurazione getStorageCloudServiceConfig(risorsa risorsa risorsa risorsa) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| canAccessUGC(ResourceResolver) booleano |

