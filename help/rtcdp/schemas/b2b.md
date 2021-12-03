---
title: Schemas in Real-time Customer Data Platform B2B Edition
description: Eine Übersicht über die Rolle von Experience-Datenmodell-Schemas (XDM) in Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: ht
source-wordcount: '220'
ht-degree: 100%

---

# Schemas in Real-time Customer Data Platform B2B Edition

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

Anweisungen zum Erstellen einer n:1-Beziehung zwischen zwei Schemas finden Sie im Tutorial zum [Erstellen von B2B-Schemabeziehungen](../../xdm/tutorials/relationship-b2b.md).

Wenn Sie eine B2B-Quellverbindung nutzen, können Sie ein Tool verwenden, um automatisch die erforderlichen Schemas und die Beziehungen zwischen ihnen zu generieren. Weitere Informationen finden Sie im Handbuch [B2B-Namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in der Quellen-Dokumentation.
