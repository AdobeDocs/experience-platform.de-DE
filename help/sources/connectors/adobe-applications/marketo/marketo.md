---
keywords: Experience Platform; home; beliebte Themen; Marketo Engage; marketo engage; marketo
solution: Experience Platform
title: Marketo Engage-Connector
description: Dieses Dokument bietet einen Überblick über den Quell-Connector von Marketo Engage, einschließlich Informationen zur Authentifizierung, Zuordnung und Datenlatenz.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 11%

---

# [!DNL Marketo Engage]-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) ist eine Komplettlösung für das Lead-Management. B2B-Marketer können damit Kundenerlebnisse transformieren, indem sie in allen Phasen komplexer Journey Interaktionen ermöglichen.

Mit dem Quell-Connector [!DNL Marketo Engage] können Sie B2B-Daten von [!DNL Marketo Engage] an Platform übertragen und diese Daten mithilfe von Anwendungen, die mit Platform verbunden sind, auf dem neuesten Stand halten.

>[!IMPORTANT]
>
>Sie müssen Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) haben, um alle Marketo-Datensätze für die Segmentierung mit dem [Echtzeit-Kundenprofil](../../../../profile/home.md) verwenden zu können. Ohne Real-Time CDP B2B Edition können Sie die Marketo-Quelle weiterhin verwenden, um Daten aus den Personen- und Aktivitätsdatensätzen zur Segmentierung an das Echtzeit-Kundenprofil zu übertragen.

Dieses Dokument bietet einen Überblick über den Quell-Connector [!DNL Marketo Engage], einschließlich Informationen zur Authentifizierung des Connectors, zur Zuordnung von [!DNL Marketo Engage] -Feldern zum Experience-Datenmodell (XDM) und zur Datenlatenz des Connectors.

## Einrichten der Adobe-Organisationszuordnung

Bevor Sie Zuordnungssätze für [!DNL Marketo Engage] festlegen können, müssen Sie zunächst die Adobe-Organisationszuordnung einrichten. Ausführliche Anweisungen dazu finden Sie im Handbuch zum Einrichten der Adobe-Organisationszuordnung für  [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).[

## Authentifizieren des [!DNL Marketo Engage]-Connectors

Um [!DNL Marketo Engage] mit Platform zu verbinden, müssen Sie zunächst Werte für Ihre `munchkinId`, `clientId` und `clientSecret` abrufen.

Lesen Sie die im Dokument [Authentifizieren des Marketo-Quell-Connectors](./marketo-auth.md) beschriebenen Schritte, um Ihre Anmeldeinformationen abzurufen.

## Einrichten von B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung

Verwenden Sie als Nächstes den B2B-Namespace und das Dienstprogramm zur automatischen Schemaerstellung, um Ihre Platform-Entwicklerkonsole und Postman-Umgebung einzurichten. Auf diese Weise können Sie Ihre B2B-Namespaces und -Schemata automatisch ausfüllen lassen. Detaillierte Anweisungen finden Sie im Handbuch zum [Einrichten Ihrer B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung](./marketo-namespaces.md) .

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen bietet, mit denen Sie Daten aus Drittanbieterquellen erfassen und in nachgelagerten Platform-Diensten verwenden können.

Durch die Einhaltung von XDM-Standards können Daten einheitlich in das Platform-Ökosystem integriert werden, was die Bereitstellung von Daten und die Erfassung von Informationen erleichtert.

Weitere Informationen zu XDM und seiner Rolle in Platform finden Sie in der [XDM-Systemübersicht](../../../../xdm/home.md).

## Feldzuordnung von [!DNL Marketo Engage] zu XDM

Um eine Quellverbindung zwischen [!DNL Marketo Engage] und Platform herzustellen, müssen die Marketo-Quelldatenfelder den entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform erfasst werden.

Im Folgenden finden Sie detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Marketo Engage] Datensätzen und Platform:

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

## Erwartete Latenz von [!DNL Marketo Engage] Daten auf Platform

In der folgenden Tabelle wird die erwartete Latenz für das Einbringen von [!DNL Marketo Engage] -Daten in Platform basierend auf der Art der Aufnahme und des gewünschten Ziels beschrieben:

| Ziel | Erwartete Latenz |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 Minuten |
| Data Lake | &lt; 60 Minuten |

>[!NOTE]
>
>Die obigen Latenzzahlen stellen Erwartungen in einem Konfidenzniveau von 95 % dar. Die tatsächlichen Latenzen werden variieren und können in seltenen Fällen um 50 % über diese Zahlen hinausgehen.

## Nächste Schritte und zusätzliche Ressourcen

Die folgende Dokumentation enthält weitere Informationen zum Erstellen einer [!DNL Marketo Engage]-Quellverbindung:

* Informationen zum Verbinden Ihrer [!DNL Marketo Engage] -Daten mit Platform finden Sie im Tutorial zum Erstellen einer  [!DNL Marketo Engage]  -Quellverbindung in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).[
   * Informationen zum Einrichten Ihrer Schemas und Erfassen benutzerdefinierter Aktivitätsdaten finden Sie im Tutorial zum Erstellen einer Quellverbindung und eines Datenflusses für  [!DNL Marketo Engage] benutzerdefinierte Aktivitätsdaten](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md) .[
   * Informationen zum Migrieren Ihrer ECID-Zuordnung aus dem [!DNL Person] -Datensatz in den [!DNL Activity] -Datensatz finden Sie im Migrationshandbuch zur [ECID-Zuordnung](./migration.md).
* Informationen zur zugrunde liegenden Einrichtung für die mit [!DNL Marketo Engage] verwendeten B2B-Namespaces und Schemas finden Sie in der Dokumentation für [B2B-Namespaces und -Schemas](./marketo-namespaces.md).
* Informationen zum Auffinden Ihrer [!DNL Marketo Engage] -Munchkin-ID und zum Generieren Ihrer Anmeldeinformationen finden Sie im [[!DNL Marketo Engage] Authentifizierungshandbuch](./marketo-auth.md).
* Informationen zu den spezifischen Zuordnungsregeln, die für [!DNL Marketo Engage] -Datensätze gelten, finden Sie in der Dokumentation zu [[!DNL Marketo Engage] Feldzuordnungen](../mapping/marketo.md).
* Allgemeine Informationen zu [!DNL Real-Time Customer Data Platform B2B Edition] und seinen Funktionen finden Sie in der Dokumentation zu [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
