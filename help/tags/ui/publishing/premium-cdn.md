---
title: Premium CDN support for tags
description: Learn about the premium CDN feature for tags and how it can be used to deliver your content in multiple geographic regions.
source-git-commit: 530fc1ad3f389ffb5d77ddf6aa0b0b3208f1d532
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Premium CDN support for tags (Beta)

>[!IMPORTANT]
>
>The premium CDN feature for tags is currently in beta and your organization may not have access to it yet. This documentation is subject to change.

[](./hosts/managed-by-adobe-host.md) However, there are certain regions that require all website assets to be replicated and hosted on a server within that region.

To account for this, tags in Experience Platform provides a premium CDN feature which allows you to deliver content to these special regions.

Premium CDN support is a paid feature, and must be purchased by your organization in order to enable and use it. This guide covers how to configure and use this feature in the Data Collection UI after it has been purchased.

## Enable premium CDN for a company

Premium CDN is enabled at the company level, meaning that you must have company edit permissions to enable the feature.

******** ****

![](../../images/ui/publishing/premium-cdn/configure-property.png)

********

![](../../images/ui/publishing/premium-cdn/enable-premium-cdn.png)

## Rebuild and install tag libraries with updated embed codes

Enabling the premium CDN feature does not mean that your tag assets are immediately replicated and ready to use within the new regions. It only means that you can now choose when to opt in to this functionality.

>[!IMPORTANT]
>
>Libraries built before enabling premium CDN will continue to operate as-is exactly as they do today. [](./environments.md#archive) Please note that after you have enabled premium CDN, any library you build that is not managed by Adobe will behave as if the premium CDN feature is not enabled.

Once you have enabled premium CDN and rebuilt any libraries that you wish to use from the new hosting regions, you can retrieve the new hosting region embed codes to add to your websites.

>[!NOTE]
>
>

****  `.cn`

![](../../images/ui/publishing/premium-cdn/embed-codes.png)

`<head>` [](./environments.md#installation)

## Nächste Schritte

This guide covered how to enable and install the premium CDN feature for your tags implementation. [](./overview.md)
