---
title: Schemata in Real-time Customer Data Platform B2B Edition
description: Eine Übersicht über die Rolle von Experience-Datenmodell (XDM)-Schemas in Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 45%

---

# Schemata in Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B Edition bietet mehrere Standardfunktionen [Experience-Datenmodell (XDM)-Klassen](../../xdm/schema/composition.md#class) , die Details zu wesentlichen B2B-Datenentitäten wie Konten, Chancen, Kampagnen und mehr erfassen. Darüber hinaus können Sie mit der Real-Time CDP B2B Edition eine n:n-Beziehung zwischen diesen Schemas definieren, damit sie an erweiterten Anwendungsfällen für die Segmentierung teilnehmen können.

>[!IMPORTANT]
>
>Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit B2B-Schemata teilnehmen können [Echtzeit-Kundenprofil](../../profile/home.md).

Die folgenden Standardklassen werden in Real-Time CDP B2B Edition bereitgestellt:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign Members](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List Members](../../xdm/classes/b2b/business-marketing-list-members.md)

Informationen dazu, wie Schemata in Ihren B2B-Workflow passen, finden Sie im [End-to-End-Tutorial](../b2b-tutorial.md).

Anweisungen zum Erstellen einer n:1-Beziehung zwischen zwei Schemas finden Sie im Tutorial zum [Erstellen von B2B-Schemabeziehungen](../../xdm/tutorials/relationship-b2b.md).

Wenn Sie eine B2B-Quellverbindung nutzen, können Sie ein Tool verwenden, um automatisch die erforderlichen Schemas und die Beziehungen zwischen ihnen zu generieren. Weitere Informationen finden Sie im Handbuch [B2B-Namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in der Quellen-Dokumentation.
