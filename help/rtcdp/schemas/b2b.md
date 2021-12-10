---
title: Schemas in Real-time Customer Data Platform B2B Edition
description: Eine Übersicht über die Rolle von Experience-Datenmodell-Schemas (XDM) in Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 1a104d26b920082ee73178dd0ad7234ad43dec1a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 93%

---

# Schemata in Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition bietet mehrere standardmäßige [Experience-Datenmodell-Klassen (XDM)](../../xdm/schema/composition.md#class), die Details zu wesentlichen B2B-Datenentitäten wie Konten, Chancen und Kampagnen erfassen. Darüber hinaus können Sie mit Real-time Customer Data Platform B2B Edition zwischen diesen Schemas Viele-zu-Eins-Beziehungen definieren, sodass diese für erweiterte Segmentierungs-Anwendungsfälle verwendet werden können.

>[!IMPORTANT]
>
>Sie müssen Zugriff auf Real-time Customer Data Platform B2B Edition haben, damit B2B-Schemas bei [Echtzeit-Kundenprofilen](../../profile/home.md) berücksichtigt werden können.

Die folgenden Standardklassen werden in Real-time Customer Data Platform B2B Edition bereitgestellt:

* [XDM Business Account](../../xdm/classes/b2b/business-account.md)
* [XDM Business Account Person Relation](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign Members](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity Person Relation](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List Members](../../xdm/classes/b2b/business-marketing-list-members.md)

Informationen dazu, wie Schemata in Ihren B2B-Workflow passen, finden Sie in der [End-to-End-Tutorial](../b2b-tutorial.md).

Anweisungen zum Erstellen einer n:1-Beziehung zwischen zwei Schemas finden Sie im Tutorial zum [Erstellen von B2B-Schemabeziehungen](../../xdm/tutorials/relationship-b2b.md).

Wenn Sie eine B2B-Quellverbindung nutzen, können Sie ein Tool verwenden, um automatisch die erforderlichen Schemas und die Beziehungen zwischen ihnen zu generieren. Weitere Informationen finden Sie im Handbuch [B2B-Namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in der Quellen-Dokumentation.
