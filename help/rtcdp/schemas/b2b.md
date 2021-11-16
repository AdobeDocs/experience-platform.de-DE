---
title: Schemas in Real-time Customer Data Platform B2B Edition
description: Eine Übersicht über die Rolle von Experience-Datenmodell (XDM)-Schemas in Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 8%

---

# Schemata in Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition bietet mehrere Standardfunktionen [Experience-Datenmodell (XDM)-Klassen](../../xdm/schema/composition.md#class) , die Details zu wesentlichen B2B-Datenentitäten wie Konten, Chancen, Kampagnen und mehr erfassen. Darüber hinaus können Sie mit der Echtzeit-Kundendatenplattform B2B Edition zwischen diesen Schemas eine Vielzahl von Beziehungen definieren, sodass sie an erweiterten Anwendungsfällen zur Segmentierung teilnehmen können.

>[!IMPORTANT]
>
>Sie müssen Zugriff auf die B2B Edition in Echtzeit-Kundendatenplattform haben, damit B2B-Schemata teilnehmen können [Echtzeit-Kundenprofil](../../profile/home.md).

Die folgenden Standardklassen werden in der Echtzeit-CDP B2B Edition bereitgestellt:

* [XDM-Geschäftskonto](../../xdm/classes/b2b/business-account.md)
* [Personenbeziehung zwischen XDM-Geschäftskonto](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-Mitglieder](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM-Geschäftschancen](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity-Personenbeziehung](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List-Mitglieder](../../xdm/classes/b2b/business-marketing-list-members.md)

Anweisungen zum Erstellen einer n:1-Beziehung zwischen zwei Schemas finden Sie im Tutorial zu [Erstellen von B2B-Schemabeziehungen](../../xdm/tutorials/relationship-b2b.md).

Wenn Sie eine B2B-Quellverbindung verwenden, können Sie ein Tool verwenden, um automatisch die erforderlichen Schemas und die Beziehungen zwischen ihnen zu generieren. Siehe Handbuch unter [B2B-Namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in der Quelldokumentation für weitere Informationen.
