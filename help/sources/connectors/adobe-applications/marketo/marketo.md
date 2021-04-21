---
keywords: Experience Platform;Startseite;beliebte Themen;Marketo Engage;Markieren;Markieren
solution: Experience Platform
title: Marketo Engage-Anschluss
topic-legacy: overview
description: In diesem Dokument erhalten Sie einen Überblick über den Marketo Engage Source Connector, einschließlich Informationen zur Authentifizierung, Zuordnung und Datenlatenz.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 13%

---


# (Beta) [!DNL Marketo Engage] Connector

>[!IMPORTANT]
>
>Die [!DNL Marketo Engage]-Quelle befindet sich derzeit in der Betaphase. Seine Funktionen und die Dokumentation können sich ändern.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (im Folgenden &quot;[!DNL Marketo]&quot;) ist eine Komplettlösung für Interessentenmanagement und B2B-Vermarkter, die Kundenerlebnisse verändern möchten, indem sie sich über alle Phasen komplexer Journey einbringen.

Mit dem [!DNL Marketo]-Quellanschluss können Sie B2B-Daten von [!DNL Marketo] auf die Plattform übertragen und diese Daten mithilfe von Anwendungen mit Plattformverbindung auf dem neuesten Stand halten.

Dieses Dokument bietet einen Überblick über den [!DNL Marketo]-Quellanschluss, einschließlich Informationen zum Authentifizieren des Connectors, zum Zuordnen von [!DNL Marketo]-Feldern zum Experience Data Model (XDM) und zur Datenlatenz des Connectors.

## [!DNL Marketo]-Connector authentifizieren

Um [!DNL Marketo] mit Platform zu verbinden, müssen Sie zunächst Werte für `munchkinId`, `clientId` und `clientSecret` abrufen.

Gehen Sie wie im Dokument [Authentifizieren Sie Ihren Marketo-Quellanschluss](./marketo-auth.md) beschrieben vor, um Ihre Anmeldeinformationen abzurufen.

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen bietet, die es Ihnen ermöglichen, Daten von Drittanbieterquellen für die Verwendung in nachgeschalteten Plattformdiensten zu erfassen.

Durch die Einhaltung von XDM-Standards können Daten einheitlich in das Plattform-Ökosystem integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weitere Informationen zu XDM und seiner Rolle in der Plattform finden Sie unter [XDM-Systemübersicht](../../../../xdm/home.md).

## Feldzuordnung von [!DNL Marketo] zu XDM

Um eine Quellverbindung zwischen [!DNL Marketo] und Platform herzustellen, müssen die Marketo-Quelldatenfelder den entsprechenden XDM-Feldern der Zielgruppe zugeordnet werden, bevor sie in Platform aufgenommen werden.

Detaillierte Informationen zu den Feldzuordnungsregeln zwischen [!DNL Marketo]-Datensätzen und -Plattformen finden Sie in den folgenden Abschnitten:

* [Aktivitäten](../mapping/marketo.md#activities)
* [Programme](../mapping/marketo.md#programs)
* [Mitgliedschaft in Programmen](../mapping/marketo.md#program-memberships)
* [Unternehmen](../mapping/marketo.md#companies)
* [Statische Listen](../mapping/marketo.md#static-lists)
* [Mitgliedschaft in statischen Listen](../mapping/marketo.md#static-list-memberships)
* [Benannte Konten](../mapping/marketo.md#named-accounts)
* [Chancen](../mapping/marketo.md#opportunities)
* [Kontaktrollen bei Chancen](../mapping/marketo.md#opportunity-contact-roles)
* [Personen](../mapping/marketo.md#persons)

## Erwartete Latenz von [!DNL Marketo]-Daten auf der Plattform

In der folgenden Tabelle wird die erwartete Latenz für das Einfügen von [!DNL Marketo]-Daten in Plattform basierend auf der Art der Erfassung und dem gewünschten Ziel aufgeführt:

| Ziel | Erwartete Latenz |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Nächste Schritte und zusätzliche Ressourcen

Die folgende Dokumentation enthält weitere Informationen zum Erstellen einer [!DNL Marketo]-Quellverbindung:

* Weitere Informationen zum Verbinden Ihrer [!DNL Marketo]-Daten mit der Plattform finden Sie im Lernprogramm [Erstellen eines Marketo-Quellconnectors in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Informationen zum zugrunde liegenden Setup für die B2B-Namensraum und -Schema, die mit [!DNL Marketo] verwendet werden, finden Sie in der Dokumentation für [B2B-Namensraum und -Schema](./marketo-namespaces.md).
* Weitere Informationen zum Suchen der [!DNL Marketo]-munchkin-ID und zum Generieren Ihrer Anmeldeinformationen finden Sie im [[!DNL Marketo] Authentifizierungshandbuch](./marketo-auth.md).
* Informationen zu den spezifischen Zuordnungsregeln für [!DNL Marketo]-Datensätze finden Sie in der Dokumentation zu [[!DNL Marketo] Feldzuordnungen](../mapping/marketo.md).