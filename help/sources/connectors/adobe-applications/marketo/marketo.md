---
keywords: Experience Platform;Startseite;beliebte Themen;Marketo Engage;Marketo Engage;Marketo
solution: Experience Platform
title: Marketo Engage-Connector
description: Dieses Dokument bietet einen Überblick über den Marketo Engage-Quell-Connector, einschließlich Informationen über seine Authentifizierung, Zuordnung und Datenlatenz.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 11%

---

# [!DNL Marketo Engage]-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) ist eine Komplettlösung für das Lead-Management. B2B-Marketer können damit Kundenerlebnisse transformieren, indem sie in allen Phasen komplexer Journey Interaktionen ermöglichen.

Mit dem [!DNL Marketo Engage]-Quell-Connector können Sie B2B-Daten aus [!DNL Marketo Engage] in Platform übertragen und mit Anwendungen, die mit Platform verbunden sind, auf dem neuesten Stand halten.

>[!IMPORTANT]
>
>Sie müssen Zugriff auf [Adobe Real-time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) haben, um alle Marketo-Datensätze für die Segmentierung mit dem [Echtzeit-Kundenprofil“ ](../../../../profile/home.md). Ohne Real-Time CDP B2B edition können Sie weiterhin die Marketo-Quelle verwenden, um Daten aus den Personen- und Aktivitätsdatensätzen zur Segmentierung in das Echtzeit-Kundenprofil zu übertragen.

Dieses Dokument bietet einen Überblick über den [!DNL Marketo Engage]-Quell-Connector, einschließlich Informationen zur Authentifizierung des Connectors, zur Zuordnung [!DNL Marketo Engage] Felder zum Experience-Datenmodell (XDM) und zur Datenlatenz des Connectors.

## Einrichten der Adobe-Organisationszuordnung

Bevor Sie Zuordnungssätze für [!DNL Marketo Engage] einrichten können, müssen Sie zunächst die Adobe-Organisationszuordnung einrichten. Ausführliche Anweisungen dazu finden Sie im Handbuch zum [ von Adobe-Organisationszuordnungen für  [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## [!DNL Marketo Engage]-Connector authentifizieren

Um [!DNL Marketo Engage] mit Platform zu verbinden, müssen Sie zunächst Werte für Ihre `munchkinId`, `clientId` und `clientSecret` abrufen.

Lesen Sie die Schritte, die im Dokument [Authentifizieren des Marketo-Quell-Connectors](./marketo-auth.md) zum Abrufen Ihrer Anmeldeinformationen beschrieben werden.

## Einrichten von B2B-Namespaces und des Dienstprogramms zur automatischen Schemaerstellung

Verwenden Sie anschließend das Dienstprogramm zur automatischen Generierung von B2B-Namespaces und -Schemas, um Ihre Platform Developer Console und Postman-Umgebung einzurichten. Auf diese Weise können Sie Ihre B2B-Namespaces und -Schemata automatisch ausfüllen. Detaillierte Anweisungen finden Sie im Handbuch unter [Einrichten der B2B-Namespaces und des Dienstprogramms zur automatischen Schemaerstellung](./marketo-namespaces.md)

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen bereitstellt, mit denen Sie Daten aus Drittanbieterquellen aufnehmen können, um sie in nachgelagerten Platform-Services zu verwenden.

Durch die Einhaltung von XDM-Standards können Daten einheitlich in das Platform-Ökosystem integriert werden, was die Bereitstellung von Daten und die Erfassung von Informationen erleichtert.

Weitere Informationen zu XDM und seiner Rolle in Platform finden Sie in der [XDM-Systemübersicht](../../../../xdm/home.md).

## Feldzuordnung von [!DNL Marketo Engage] zu XDM

Um eine Quellverbindung zwischen [!DNL Marketo Engage] und Platform herzustellen, müssen die Marketo-Quelldatenfelder ihren entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform aufgenommen werden können.

Siehe die folgenden Informationen zu den Feldzuordnungsregeln zwischen [!DNL Marketo Engage] Datensätzen und Platform:

* [Aktivitäten](../mapping/marketo.md#activities)
* [Programme](../mapping/marketo.md#programs)
* [Programmmitgliedschaften](../mapping/marketo.md#program-memberships)
* [Firmen](../mapping/marketo.md#companies)
* [Statische Listen](../mapping/marketo.md#static-lists)
* [Mitgliedschaften in statischen Listen](../mapping/marketo.md#static-list-memberships)
* [Benannte Konten](../mapping/marketo.md#named-accounts)
* [Opportunities](../mapping/marketo.md#opportunities)
* [Rollen von Kontakten bei Opportunities](../mapping/marketo.md#opportunity-contact-roles)
* [Personen](../mapping/marketo.md#persons)

## Erwartete Latenz von [!DNL Marketo Engage] auf Platform

In der folgenden Tabelle ist die erwartete Latenz für das Einbringen [!DNL Marketo Engage] Daten in Platform aufgeführt, basierend auf der Art der Aufnahme und dem gewünschten Ziel:

| Ziel | Erwartete Latenz |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 Minuten |
| Data Lake | &lt; 60 Minuten |

>[!NOTE]
>
>Die oben genannten Latenzzahlen stellen Erwartungen auf einem Konfidenzniveau von 95 % dar. Die tatsächlichen Latenzen variieren und können in seltenen Fällen um 50 % über diese Zahlen hinausgehen.

## Nächste Schritte und zusätzliche Ressourcen

Die folgende Dokumentation enthält weitere Informationen zum Erstellen einer [!DNL Marketo Engage]-Quellverbindung:

* Informationen zum Verbinden Ihrer [!DNL Marketo Engage] mit Platform finden Sie im Tutorial zum [Erstellen einer - [!DNL Marketo Engage]  in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Informationen zum Einrichten Ihrer Schemata und Aufnehmen benutzerdefinierter Aktivitätsdaten finden Sie im Tutorial zum [Erstellen einer Quellverbindung und eines Datenflusses für Daten  [!DNL Marketo Engage]  benutzerdefinierten Aktivität](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Informationen zum Migrieren Ihrer ECID-Zuordnung vom [!DNL Person]-Datensatz zum [!DNL Activity]-Datensatz finden Sie im [Migrationshandbuch für die ECID-Zuordnung](./migration.md).
* Informationen zum zugrunde liegenden Setup für die B2B-Namespaces und Schemata, die mit [!DNL Marketo Engage] verwendet werden, finden Sie in der Dokumentation für [B2B-Namespaces und -Schemata](./marketo-namespaces.md).
* Informationen zum Auffinden Ihrer [!DNL Marketo Engage] Munchkin-ID und zum Generieren Ihrer Anmeldeinformationen finden Sie im [[!DNL Marketo Engage] Authentifizierungshandbuch](./marketo-auth.md).
* Informationen zu den spezifischen Zuordnungsregeln, die für [!DNL Marketo Engage] Datensätze gelten, finden Sie in der Dokumentation unter [[!DNL Marketo Engage] Feldzuordnungen](../mapping/marketo.md).
* Allgemeine Informationen zu [!DNL Real-Time Customer Data Platform B2B Edition] und seinen Funktionen finden Sie in der Dokumentation zu [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
