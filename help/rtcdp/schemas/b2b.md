---
title: Schemas in Real-time Customer Data Platform B2B Edition
description: Eine Übersicht über die Rolle von Experience-Datenmodell (XDM)-Schemas in Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 65afc75d89a4183d0ad03200f6c08c72dd104180
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 7%

---

# Schemata in Real-time Customer Data Platform B2B Edition (Beta)

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalität können sich ändern.

Real-time Customer Data Platform B2B Edition bietet mehrere standardmäßige [Experience-Datenmodell (XDM)-Klassen](../../xdm/schema/composition.md#class), die Details zu wesentlichen B2B-Datenentitäten wie Konten, Chancen, Kampagnen und mehr erfassen. Darüber hinaus können Sie mit der Echtzeit-Kundendatenplattform B2B Edition zwischen diesen Schemas eine Vielzahl von Beziehungen definieren, sodass sie an erweiterten Anwendungsfällen zur Segmentierung teilnehmen können.

Die folgenden Standardklassen werden in der Echtzeit-CDP B2B Edition bereitgestellt:

* [XDM-Geschäftskonto](../../xdm/classes/b2b/business-account.md)
* [Personenbeziehung zwischen XDM-Geschäftskonto](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign-Mitglieder](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM-Geschäftschancen](../../xdm/classes/b2b/business-opportunity.md)
* [XDM Business Opportunity-Personenbeziehung](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM Business Marketing List](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM Business Marketing List-Mitglieder](../../xdm/classes/b2b/business-marketing-list-members.md)

Anweisungen zum Erstellen einer n:1-Beziehung zwischen zwei Schemas finden Sie im Tutorial zum Definieren von B2B-Schemabeziehungen](../../xdm/tutorials/relationship-b2b.md).[

Wenn Sie eine B2B-Quellverbindung verwenden, können Sie ein Tool verwenden, um automatisch die erforderlichen Schemas und die Beziehungen zwischen ihnen zu generieren. Weitere Informationen finden Sie im Handbuch zu [B2B-Namespaces](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) in der Quelldokumentation.
