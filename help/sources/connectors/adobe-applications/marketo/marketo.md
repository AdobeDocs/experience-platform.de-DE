---
keywords: Experience Platform; Startseite; beliebte Themen; Marketo Engage; Marketo Interaction; Marketo
solution: Experience Platform
title: Marketo Engage-Connector
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Marketo Engage-Quell-Connector, einschließlich Informationen zur Authentifizierung, Zuordnung und Datenlatenz.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0661d124ffe520697a1fc8e2cae7b0b61ef4edfc
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 14%

---

# (Beta) [!DNL Marketo Engage] Connector

>[!IMPORTANT]
>
>Die Quelle [!DNL Marketo Engage] in Adobe Experience Platform befindet sich derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (im Folgenden &quot;[!DNL Marketo]&quot;) ist eine Komplettlösung für das Lead-Management und B2B-Marketer, die Kundenerlebnisse transformieren möchten, indem sie in allen Phasen komplexer Journey Interaktionen ermöglichen.

Mit dem Quell-Connector [!DNL Marketo] können Sie B2B-Daten von [!DNL Marketo] in Platform übertragen und diese Daten mithilfe von Anwendungen mit Plattformverbindung auf dem neuesten Stand halten.

Dieses Dokument bietet einen Überblick über den Quell-Connector [!DNL Marketo], einschließlich Informationen zur Authentifizierung des Connectors, zur Zuordnung von [!DNL Marketo]-Feldern zum Experience-Datenmodell (XDM) und zur Datenlatenz des Connectors.

## Authentifizieren Sie Ihren [!DNL Marketo]-Connector.

Um [!DNL Marketo] mit Platform zu verbinden, müssen Sie zunächst Werte für `munchkinId`, `clientId` und `clientSecret` abrufen.

Lesen Sie die im Dokument [Authentifizieren Sie Ihren Marketo-Quell-Connector](./marketo-auth.md) beschriebenen Schritte, um Ihre Anmeldeinformationen abzurufen.

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen bietet, mit denen Sie Daten aus Drittanbieterquellen erfassen und in nachgelagerten Platform-Diensten verwenden können.

Durch die Einhaltung von XDM-Standards können Daten einheitlich in das Platform-Ökosystem integriert werden, was die Bereitstellung von Daten und die Erfassung von Informationen erleichtert.

Weitere Informationen zu XDM und seiner Rolle in Platform finden Sie unter [XDM-Systemübersicht](../../../../xdm/home.md).

## Feldzuordnung von [!DNL Marketo] zu XDM

Um eine Quellverbindung zwischen [!DNL Marketo] und Platform herzustellen, müssen die Marketo-Quelldatenfelder den entsprechenden Ziel-XDM-Feldern zugeordnet werden, bevor sie in Platform erfasst werden.

Im Folgenden finden Sie detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Marketo] Datensätzen und Platform:

* [Aktivitäten](../mapping/marketo.md#activities)
* [Programme](../mapping/marketo.md#programs)
* [Programmmitgliedschaften](../mapping/marketo.md#program-memberships)
* [Firmen](../mapping/marketo.md#companies)
* [Statische Listen](../mapping/marketo.md#static-lists)
* [Mitgliedschaft in statischen Listen](../mapping/marketo.md#static-list-memberships)
* [Spezifische Konten](../mapping/marketo.md#named-accounts)
* [Chancen](../mapping/marketo.md#opportunities)
* [Kontaktrollen bei Chancen](../mapping/marketo.md#opportunity-contact-roles)
* [Personen](../mapping/marketo.md#persons)

## Erwartete Latenz von [!DNL Marketo] Daten auf Platform

In der folgenden Tabelle wird die erwartete Latenz für das Einbringen von [!DNL Marketo]-Daten in Platform basierend auf der Art der Aufnahme und des gewünschten Ziels beschrieben:

| Ziel | Erwartete Latenz |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Nächste Schritte und zusätzliche Ressourcen

Die folgende Dokumentation enthält weitere Informationen zum Erstellen einer [!DNL Marketo]-Quellverbindung:

* Informationen zum Verbinden Ihrer [!DNL Marketo]-Daten mit Platform finden Sie im Tutorial zum Erstellen eines Marketo-Quell-Connectors in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).[
* Informationen zur zugrunde liegenden Einrichtung für die B2B-Namespaces und -Schemas, die mit [!DNL Marketo] verwendet werden, finden Sie in der Dokumentation für [B2B-Namespaces und -Schemata](./marketo-namespaces.md).
* Informationen zum Suchen Ihrer [!DNL Marketo]-Munchkin-ID und zum Generieren Ihrer Anmeldeinformationen finden Sie im [[!DNL Marketo] Authentifizierungshandbuch](./marketo-auth.md).
* Informationen zu den spezifischen Zuordnungsregeln für [!DNL Marketo]-Datensätze finden Sie in der Dokumentation zu [[!DNL Marketo] Feldzuordnungen](../mapping/marketo.md).
* Allgemeine Informationen zu [!DNL Real-time Customer Data Platform B2B Edition] und seinen Funktionen finden Sie in der Dokumentation zu [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
