---
keywords: Experience Platform;Startseite;beliebte Themen;Marketo Engage;Markieren
solution: Experience Platform
title: Marketo Engage-Anschluss
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Marketo Engage-Quellanschluss, einschließlich Informationen über Authentifizierung, Zuordnung und Datenlatenz.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: a36a4775c14e97df51f218cea3a083d29c7b69dc
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 13%

---

# (Beta) [!DNL Marketo Engage] Anschluss

>[!IMPORTANT]
>
>Die [!DNL Marketo Engage] Quelle in Adobe Experience Platform befindet sich derzeit in der Beta-Version. Dokumentation und Funktionalität können sich ändern.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (nachstehend &quot;nachstehend &quot;nachstehend&quot; genannt[!DNL Marketo]&quot;) ist eine Komplettlösung für Lead-Management- und B2B-Marketingexperten, die Kundenerlebnisse verändern möchten, indem sie in alle Phasen komplexer Journey-Kaufprozesse eingebunden werden.

Mit [!DNL Marketo] Quellanschluss, von dem Sie B2B-Daten abrufen können [!DNL Marketo] , um diese Daten mit Anwendungen mit Plattformverbindung zu plattformübergreifend auf dem Laufenden zu halten.

Dieses Dokument bietet einen Überblick über die [!DNL Marketo] Quellanschluss, einschließlich Informationen zur Authentifizierung des Connectors und zur Zuordnung [!DNL Marketo] Felder für Erlebnisdatenmodell (XDM) und die Datenlatenz des Connectors.

## Authentifizieren Sie Ihren [!DNL Marketo] Anschluss

Zur Verbindung [!DNL Marketo] auf Platform setzen, müssen Sie zunächst Werte für `munchkinId`, `clientId`und `clientSecret`.

Weitere Informationen finden Sie in den Schritten unter [Authentifizieren Sie Ihren Marketo-Quellanschluss.](./marketo-auth.md) Dokument zum Abrufen Ihrer Anmeldedaten.

## Freigabe von Adobe Experience Cloud-Audiencen einrichten

Zuordnungssätze müssen erstellt werden für [!DNL Marketo], müssen Sie zuerst Adobe Experience Cloud Audience Sharing einrichten. Detaillierte Anweisungen dazu finden Sie im Handbuch zu [zur Einrichtung der Adobe Experience Cloud Audience Sharing für [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-experience-cloud-audience-sharing.html?lang=en).

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die gemeinsame Strukturen und Definitionen bietet, mit denen Sie Daten von Drittanbieterquellen für die Verwendung in nachgeschalteten Plattformdiensten erfassen können.

Durch die Einhaltung der XDM-Standards können Daten einheitlich in das Platform-Ökosystem integriert werden, was die Bereitstellung von Daten und die Erfassung von Informationen erleichtert.

Weitere Informationen zu XDM und seiner Rolle in der Plattform finden Sie im [XDM-Systemübersicht](../../../../xdm/home.md).

## Feldzuordnung aus [!DNL Marketo] nach XDM

So erstellen Sie eine Quellverbindung zwischen [!DNL Marketo] und Platform, müssen die Marketo-Quelldatenfelder den entsprechenden XDM-Feldern der Zielgruppe zugeordnet werden, bevor sie in Platform integriert werden können.

Im Folgenden finden Sie detaillierte Informationen zu den Regeln für die Feldzuordnung zwischen [!DNL Marketo] Datensätze und Plattform:

* [Aktivitäten](../mapping/marketo.md#activities)
* [Programme](../mapping/marketo.md#programs)
* [Mitgliedschaft im Programm](../mapping/marketo.md#program-memberships)
* [Firmen](../mapping/marketo.md#companies)
* [Statische Listen](../mapping/marketo.md#static-lists)
* [Mitgliedschaft in statischen Listen](../mapping/marketo.md#static-list-memberships)
* [Benannte Konten](../mapping/marketo.md#named-accounts)
* [Gelegenheiten](../mapping/marketo.md#opportunities)
* [Gelegenheits-Kontaktrollen](../mapping/marketo.md#opportunity-contact-roles)
* [Personen](../mapping/marketo.md#persons)

## Erwartete Latenz von [!DNL Marketo] Daten auf Plattform

In der folgenden Tabelle wird die zu erwartende Wartezeit bei der Einführung von [!DNL Marketo] Daten in Plattform, basierend auf der Art der Aufnahme und dem gewünschten Ziel:

| Ziel | Erwartete Latenz |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 Minute |
| Data Lake | &lt; 60 Minuten |

## Nächste Schritte und zusätzliche Ressourcen

Die folgende Dokumentation enthält weitere Informationen zum Erstellen eines [!DNL Marketo] Quellverbindung:

* Weitere Informationen zum Herstellen einer Verbindung [!DNL Marketo] Daten zur Plattform finden Sie im Tutorial zu [Erstellen eines Marketo-Quellsteckers in der Benutzeroberfläche](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Informationen über die zugrunde liegende Einrichtung für die B2B-Namensraum und -Schema [!DNL Marketo], lesen Sie die Dokumentation für [B2B-Namensraum und -Schema](./marketo-namespaces.md).
* Informationen zum Auffinden Ihrer [!DNL Marketo] munchkin-ID und Generierung Ihrer Anmeldedaten finden Sie in der [[!DNL Marketo] Authentifizierungsleitfaden](./marketo-auth.md).
* Informationen zu den spezifischen Zuordnungsregeln für [!DNL Marketo] Datensätze finden Sie in der Dokumentation zu [[!DNL Marketo] Feldzuordnungen](../mapping/marketo.md).
* Allgemeine Informationen über [!DNL Real-time Customer Data Platform B2B Edition] und die zugehörigen Funktionen finden Sie in der Dokumentation auf [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
