---
title: Schemata in Real-time Customer Data Platform B2B Edition
description: Eine Übersicht über die Rolle von Experience-Datenmodell-Schemas (XDM) in Adobe Real-time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 52%

---

# Schemata in Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B edition bietet mehrere standardmäßige [Experience-Datenmodell (XDM)-Klassen](../../xdm/schema/composition.md#class) die Details zu wesentlichen B2B-Datenentitäten wie Konten, Opportunitys, Kampagnen und mehr erfassen. Darüber hinaus können Sie mit Real-Time CDP B2B edition zwischen diesen Schemata Viele-zu-Eins-Beziehungen definieren, damit diese für erweiterte Segmentierungs-Anwendungsfälle verwendet werden können.

>[!IMPORTANT]
>
>Sie müssen Zugriff auf Real-Time CDP B2B edition haben, damit B2B-Schemata am [Echtzeit-Kundenprofil) teilnehmen ](../../profile/home.md).

Die folgenden Standardklassen werden in Real-Time CDP B2B edition bereitgestellt:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign Members](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List Members](../../xdm/classes/b2b/business-marketing-list-members.md)

Informationen dazu, wie Schemata in Ihren B2B-Workflow passen, finden Sie im [End-to-End-Tutorial](../b2b-tutorial.md).

Anweisungen zum Erstellen einer n:1-Beziehung zwischen zwei Schemata finden Sie im Tutorial zum [Erstellen von B2B-Schemabeziehungen](../../xdm/tutorials/relationship-b2b.md).

Wenn Sie eine B2B-Quellverbindung nutzen, können Sie ein Tool verwenden, um automatisch die erforderlichen Schemata und die Beziehungen zwischen ihnen zu generieren. Weitere Informationen finden Sie im Handbuch [B2B-Namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in der Quellen-Dokumentation.
