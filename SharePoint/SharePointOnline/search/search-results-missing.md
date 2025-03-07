---
title: Search results missing in SharePoint Online
description: This article describes how to resolve an issue where search results are missing in SharePoint Online
author: helenclu
manager: dcscontentpm
localization_priority: Normal
search.appverid: 
- MET150
audience: ITPro
ms.prod: sharepoint-server-itpro
ms.topic: article
ms.author: luche
ms.custom: CSSTroubleshoot
appliesto:
- SharePoint Online
---

# Search results missing in SharePoint Online

## Problem

When a user tries to search a site in SharePoint Online, items may be missing from the search results. For example, the following items may be missing:

- Content
- Pages
- ASPX pages

This issue may occur even though the site was crawled and indexed by the Search service, and the user has permissions to access the resource by using a search query.

## Cause

There are various reasons why expected results maybe be missing that are related to crawl latency or settings in SharePoint Online.

## Solution

1. Make sure that **Allow this site to appear in Search results** is set to **Yes**.
        
     1. As an admin, locate the site that's missing results.
    
     1. Click the gear icon in the upper-right corner.
    
     1. Select **Site Settings**.
    
     1. Under **Search**, select **Search and offline availability**.
    
     1. Make sure that **Allow this site to appear in Search results** is set to **Yes**. 
    
         After the setting is set to **Yes**, the site should be indexed during the next scheduled crawl.
    
         > [!NOTE]
         > From the same location, admins can also select **Reindex Site** to enable the site to be picked up during the next scheduled search crawl.
    
         See the [More Information](#more-information) section for a detailed explanation and walk-through of site-level search configuration settings.

1. Make sure that **Allow items from this document library to appear in search results?** is set to **Yes**.

    1. As an admin, locate the library that's missing from search results.
    
    1. Click the gear icon in the upper-right corner.
    
    1. Select **Library Settings**.
    
    1. Select **Advanced Settings**.
    
    1. Make sure that **Allow items from this document library to appear in search results?** is set to **Yes**.
    
         After the setting is set to **Yes**, the library should be indexed during the next scheduled crawl.
    
         > [!NOTE]
         > From the same location, admins can also select **Reindex Document Library** to make sure that all content in the document library is indexed during the next scheduled crawl.

1. Verify that the version of the document that's missing from search results is a major version of the document. If the version is a minor version, it won't be displayed in the search results until it's checked in and published as a major version.

    1. As an admin, locate the document that's missing from search results.
    
    1. Select the three dots next to the document to see more settings.
    
    1. Check **Version History** to see whether there are any minor versions of the document. If there are, the document is available as a minor version but won't be found when the user searches for it.
    
    1. To make the document available in search results, select the three dots () next to the document to see more settings.
    
    1. This time, select the **Advanced** option, and then select **Publish a Major Version**. The admin can go back to **Version History** and see that the document is published as a major version, typically a later version than 1.0.
    
    1. Try to search for the document again. The document will be displayed (after it's crawled and indexed) because it's published as a major version.
    
    To have draft items crawled, see [Draft items are not crawled in SharePoint](https://support.microsoft.com/office/draft-items-are-not-crawled-in-sharepoint-9198c307-13d6-425c-a174-542a60e410e4).

1. Verify the site's search visibility options at the following location: 

     **<site_name>/_layouts/srchvis.aspx**

     Make sure that the **Allow this site to appear in Search results** option is selected.

### Parent site and sub site-specific search issues

The default setting for search visibility is one of the following options:

- **Do not index Web Parts if this site contains fine-grained permissions**
- **Always index all Web Parts on this site**
- **Never index any Web Parts on this site**

If a subsite on the site collection doesn't inherit permissions, .aspx pages won't appear in the search results. To resolve this issue, set the search visibility option in Srchvis.aspx to **Always index all Web Parts on this site**. Additionally, you may set the subsite to inherit permissions from the parent site.

## More information

For more information about search, see the following Microsoft webpages: 

- [Enable content on a site to be searchable](/sharepoint/make-site-content-searchable)
- [Not getting the search results you're looking for in SharePoint?](https://support.office.com/article/not-getting-the-search-results-you-re-looking-for-in-sharepoint-d80687f7-1010-4e6d-add9-584b423289d9)
- [Specify search settings for a site collection or a site](/sharepoint/override-default-search-center)

Still need help? Go to [SharePoint Community](https://techcommunity.microsoft.com/t5/sharepoint/ct-p/SharePoint).
