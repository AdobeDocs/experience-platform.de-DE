---
keywords: Experience Platform;home;beliebte Themen;ECID;ecid
solution: Experience Platform
title: Identitätsdaten für Datenschutzanfragen
topic-legacy: overview
description: In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 43%

---

# Identitätsdaten für Datenschutzanfragen

In Adobe Experience Platform [!DNL Privacy Service] Um Kundenanfragen für ihre privaten Daten zu verarbeiten (z. B. für den Zugriff auf, das Löschen oder die Abwahl von Kaufanfragen), müssen eindeutige IDs bereitgestellt werden, die einen bestimmten Kunden mit den gespeicherten Daten in Ihren Adobe Experience Cloud-fähigen Anwendungen verknüpfen. [!DNL Privacy Service] verwendet diese Kennungen dann, um alle unter der Kundenidentität in gespeicherten Daten zu erfassen und gemäß der Kundenanfrage zu verarbeiten.[!DNL Experience Cloud]

In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

## Identitäten und Namespaces

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanal interagieren kann, kann es schwierig sein, die unterschiedlichen Kennungen, die aus diesen vielen Interaktionen erfasst werden, miteinander in Einklang zu bringen. Dies wiederum kann es schwierig machen festzustellen, welche Daten zu einer bestimmten Person in Ihrem [!DNL Experience Cloud] Anwendungen.

Beispielsweise bei der Verarbeitung von Kundendatenanforderungen in [!DNL Privacy Service], kann eine Identität einen Cookie-Wert darstellen, der unter einer von der Adobe kontrollierten Domäne eingestellt ist, einen Cookie-Wert unter einer Drittanbieter-Domäne, der mit der Adobe geteilt wird, oder einen benutzerdefinierten Bezeichner, den Sie explizit in Ihrer IMS-Organisation definieren.

Es ist daher erforderlich, dass jede Identität [!DNL Privacy Service] wird mit einem Namensraum begleitet, der den Kontext bereitstellt, indem er den Identitätswert mit seinem System der Herkunft verknüpft. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Adobe Experience Platform Identity Service verwaltet einen Speicher mit global definierten und benutzerdefinierten Identitäts-Namespaces. Weitere Informationen zu Namespaces finden Sie in [Identitäts-Namespace – Übersicht](../identity-service/namespaces.md). Für eine Liste von Standard-Namensräumen und Namensraum-Qualifikatoren, die häufig in [!DNL Privacy Service], siehe [Anhang](api/appendix.md) im API-Handbuch.

## ECID- und Opt-in-Service

Adobe Experience Cloud [!DNL Identity Service] dient als gemeinsamer Identifikationsrahmen für [!DNL Experience Cloud]und weist jedem Site-Besucher eine eindeutige, dauerhafte ID zu. Die [!DNL Experience Cloud] Die ID (ECID) verfolgt die Aktivität eines Kunden mithilfe eines Erstanbieter-Cookies, kann ein Gerät über mehrere Anwendungen hinweg eindeutig identifizieren und ermöglicht es Ihnen, denselben Site-Besucher und die Daten in verschiedenen Bereichen zu identifizieren. [!DNL Experience Cloud] Anwendungen. Weitere Informationen finden Sie in [Experience Cloud Identity Service – Übersicht](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Teilnahme am Dienst, eine Erweiterung von [!DNL Experience Cloud Identity Service], ermöglicht das Einrichten von Anwendungsprotokollen, damit Besucher bestimmen können, ob Sie ein Cookie auf dem Gerät oder im Browser des Besuchers setzen können. Ausführlichere Informationen zu Opt-in Service, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der [Opt-in Service-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de).

Sobald Ihren Site-Besuchern ECIDs zugewiesen wurden, können Sie die Adobe nutzen [!DNL Privacy JavaScript Library] um diese IDs für die Verwendung in Datenschutzanfragen abzurufen, wie im nächsten Abschnitt beschrieben.

## [!DNL Privacy JS Library]

Die [!DNL Adobe Privacy JavaScript Library] bietet mehrere Funktionen, mit denen Sie im Browser gespeicherte Kundenidentitäten abrufen und entfernen können. Die Bibliothek kann so konfiguriert werden, dass Identitätsinformationen aus verschiedenen Adobe-Anwendungen, einschließlich ECID, abgerufen werden können. Durch Rückrufe oder Versprechungen können Sie erfolgreich abgerufene IDs programmgesteuert verarbeiten und an die [!DNL Privacy Service] API.

Für weitere Informationen über [!DNL Privacy JS Library], einschließlich Codebeispielen für mehrere häufige Verwendungszwecke, finden Sie in den [Übersicht über JS-Datenschutzbibliothek](js-library.md).

## Nächste Schritte

Dieses Dokument bietet einen kurzen Überblick über die zentralen Konzepte zum Abrufen von Kundenidentitätsdaten zur Verwendung in Datenschutzanfragen. Es wird empfohlen, über die Dokumentations-Links in den einzelnen Abschnitten auf detailliertere Informationen über diese Konzepte und Dienste zuzugreifen. Schritte zum Senden der abgerufenen IDs an [!DNL Privacy Service] zum Erstellen von Zugriffs-, Löschen- oder Abmeldeanfragen siehe [Privacy Service-API-Handbuch](api/overview.md).
