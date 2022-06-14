---
keywords: Experience Platform; Startseite; beliebte Themen; Marketo Engage; Marketo Interaction; Marketo
solution: Experience Platform
title: Marketo Engage-Connector
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Marketo Engage-Quell-Connector, einschließlich Informationen zur Authentifizierung, Zuordnung und Datenlatenz.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 1ecdd5f058a5996b4a3d12ba62c5f352633cd75a
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 14%

---

# [!DNL Marketo Engage]-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (nachstehend &quot;genannt)[!DNL Marketo]&quot;) ist eine Komplettlösung für das Lead-Management. B2B-Marketer können damit Kundenerlebnisse transformieren, indem sie in allen Phasen komplexer Journey Interaktionen ermöglichen.

Mit dem [!DNL Marketo] Quell-Connector: Sie können B2B-Daten von [!DNL Marketo] zu Platform hinzufügen und diese Daten mithilfe von Anwendungen, die mit Platform verbunden sind, auf dem neuesten Stand zu halten.

Dieses Dokument bietet einen Überblick über die [!DNL Marketo] Quell-Connector, einschließlich Informationen zur Authentifizierung des Connectors, zur Zuordnung [!DNL Marketo] -Felder auf das Experience-Datenmodell (XDM) und die Datenlatenz des Connectors hinzu.

## Authentifizieren Sie Ihre [!DNL Marketo] Connector

Um eine Verbindung herzustellen [!DNL Marketo] in Platform müssen Sie zunächst Werte für Ihre `munchkinId`, `clientId`und `clientSecret`.

Siehe die Schritte, die im Abschnitt [Authentifizieren des Marketo-Quell-Connectors](./marketo-auth.md) Dokument zum Abrufen Ihrer Anmeldedaten.

## Einrichten der Adobe-Organisationszuordnung

Bevor Sie Zuordnungssätze für [!DNL Marketo]müssen Sie zunächst die Adobe-Organisationszuordnung einrichten. Ausführliche Anweisungen finden Sie im Handbuch unter [Einrichten der Adobe-Organisationszuordnung für [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Einrichten von B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung

Verwenden Sie als Nächstes den B2B-Namespace und das Dienstprogramm zur automatischen Schemaerstellung, um Ihre Platform-Entwicklerkonsole und Postman-Umgebung einzurichten. Auf diese Weise können Sie Ihre B2B-Namespaces und -Schemata automatisch ausfüllen lassen. Detaillierte Anweisungen finden Sie im Handbuch unter [Einrichten Ihrer B2B-Namespaces und des Dienstprogramm zur automatischen Schemaerstellung](./marketo-namespaces.md)

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen bietet, mit denen Sie Daten aus Drittanbieterquellen erfassen und in nachgelagerten Platform-Diensten verwenden können.

Durch die Einhaltung von XDM-Standards können Daten einheitlich in das Platform-Ökosystem integriert werden, was die Bereitstellung von Daten und die Erfassung von Informationen erleichtert.

Weitere Informationen zu XDM und seiner Rolle in Platform finden Sie unter [XDM-System - Übersicht](../../../../xdm/home.md).

## Feldzuordnung aus [!DNL Marketo] in XDM

So richten Sie eine Quellverbindung zwischen [!DNL Marketo] und Platform, müssen die Marketo-Quelldatenfelder ihren entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform erfasst werden.

Detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Marketo] Datensätze und Plattform:

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

## Erwartete Latenz von [!DNL Marketo] Daten in Platform

In der folgenden Tabelle wird die erwartete Latenz für die [!DNL Marketo] Daten in Platform, basierend auf der Art der Aufnahme und dem gewünschten Ziel:

| Ziel | Erwartete Latenz |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Nächste Schritte und zusätzliche Ressourcen

Die folgende Dokumentation enthält weitere Informationen zum Erstellen eines [!DNL Marketo] Quellverbindung:

* Informationen zum Verbinden Ihrer [!DNL Marketo] Daten an Platform weiterleiten, siehe Tutorial zu [Erstellen eines Quell-Connectors für Marketo über die Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Informationen zur zugrunde liegenden Einrichtung für die B2B-Namespaces und -Schemata, die mit [!DNL Marketo]finden Sie in der Dokumentation für [B2B-Namespaces und -Schemata](./marketo-namespaces.md).
* Informationen zum Auffinden Ihrer [!DNL Marketo] Munchkin-ID und Generieren Ihrer Anmeldeinformationen finden Sie im Abschnitt [[!DNL Marketo] Authentifizierungshandbuch](./marketo-auth.md).
* Informationen zu den spezifischen Zuordnungsregeln für [!DNL Marketo] Datensätze finden Sie in der Dokumentation unter [[!DNL Marketo] Feldzuordnungen](../mapping/marketo.md).
* Allgemeine Informationen [!DNL Real-time Customer Data Platform B2B Edition] und deren Funktionen finden Sie in der Dokumentation unter [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
