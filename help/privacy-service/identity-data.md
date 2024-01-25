---
keywords: Experience Platform;Startseite;beliebte Themen;ECID;ecid
solution: Experience Platform
title: Identitätsdaten für Datenschutzanforderungen
description: In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 40%

---

# Identitätsdaten für Datenschutzanfragen

In Adobe Experience Platform [!DNL Privacy Service] Um Kundenanfragen für ihre privaten Daten zu verarbeiten (einschließlich Zugriffs-, Lösch- oder Verkaufs-Opt-out-Anfragen), müssen eindeutige Kennungen bereitgestellt werden, die einen bestimmten Kunden mit seinen gespeicherten privaten Daten in Ihren Adobe Experience Cloud-fähigen Anwendungen verknüpfen. [!DNL Privacy Service] verwendet diese IDs dann, um alle Daten zu erfassen, die unter der Kundenidentität in [!DNL Experience Cloud]und verarbeiten Sie sie entsprechend der Kundenanfrage.

In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

## Identitäten und Namespaces

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanäle interagieren kann, kann es schwierig sein, die unterschiedlichen Kennungen, die aus diesen vielen Interaktionen erfasst werden, miteinander abzustimmen. Dies wiederum kann es schwierig machen, zu bestimmen, welche Daten zu einer bestimmten Person in Ihrer [!DNL Experience Cloud] Anwendungen.

Beispielsweise bei der Verarbeitung von Kundendatenanfragen in [!DNL Privacy Service]kann eine Identität einen Cookie-Wert darstellen, der unter einer von Adobe gesteuerten Domäne gesetzt wird, einen Cookie-Wert unter einer Drittanbieterdomäne, der für Adobe freigegeben ist, oder eine benutzerdefinierte Kennung, die Sie explizit in Ihrem Unternehmen definieren.

Daher ist es erforderlich, dass jede Identität an [!DNL Privacy Service] wird von einem Namespace begleitet, der Kontext bietet, indem der Identitätswert mit seinem Ursprungssystem in Beziehung gesetzt wird. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Adobe Experience Platform Identity Service verwaltet einen Speicher mit global definierten und benutzerdefinierten Identitäts-Namespaces. Weitere Informationen zu Namespaces finden Sie in [Identitäts-Namespace – Übersicht](../identity-service/features/namespaces.md). Für eine Liste von Standard-Namespaces und Namespace-Kennzeichnungen, die häufig in [!DNL Privacy Service], siehe [Anhang](api/appendix.md) im API-Handbuch.

## ECID- und Opt-in-Service

Adobe Experience Cloud [!DNL Identity Service] dient als gemeinsamer Identifizierungsrahmen für [!DNL Experience Cloud]und weist jedem Site-Besucher eine eindeutige, beständige ID zu. Die [!DNL Experience Cloud] Die ID (ECID) verfolgt die Aktivität eines Kunden mithilfe eines Erstanbieter-Cookies, kann ein Gerät über mehrere Anwendungen hinweg eindeutig identifizieren und ermöglicht es Ihnen, denselben Site-Besucher und dessen Daten in verschiedenen [!DNL Experience Cloud] Anwendungen. Weitere Informationen finden Sie in [Experience Cloud Identity Service – Übersicht](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Opt-in-Dienst, eine Erweiterung von [!DNL Experience Cloud Identity Service]können Sie Protokolle in Ihrer Anwendung einrichten, damit Besucher feststellen können, ob Sie ein Cookie auf dem Gerät oder Browser des Besuchers setzen können. Ausführlichere Informationen zu Opt-in Service, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der [Opt-in Service-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de).

Sobald Ihren Site-Besuchern ECIDs zugewiesen wurden, können Sie die Adobe [!DNL Privacy JavaScript Library] , um diese IDs zur Verwendung in Datenschutzanfragen abzurufen, wie im nächsten Abschnitt beschrieben.

## [!DNL Privacy JS Library]

Die [!DNL Adobe Privacy JavaScript Library] bietet mehrere Funktionen, mit denen Sie Kundenidentitäten abrufen und entfernen können, die im Browser gespeichert sind. Die Bibliothek kann so konfiguriert werden, dass Identitätsinformationen aus verschiedenen Adobe-Anwendungen, einschließlich ECID, abgerufen werden können. Durch die Verwendung von Rückrufen oder Zusagen können Sie erfolgreich abgerufene IDs programmgesteuert verarbeiten und an die [!DNL Privacy Service] API.

Weitere Informationen finden Sie unter [!DNL Privacy JS Library], einschließlich Codebeispielen für verschiedene gängige Anwendungsfälle, siehe [Übersicht zur Privacy JS Library](js-library.md).

## Nächste Schritte

Dieses Dokument bietet einen kurzen Überblick über die zentralen Konzepte zum Abrufen von Kundenidentitätsdaten zur Verwendung in Datenschutzanfragen. Es wird empfohlen, über die Dokumentations-Links in den einzelnen Abschnitten auf detailliertere Informationen über diese Konzepte und Dienste zuzugreifen. Anweisungen zum Senden abgerufener IDs an [!DNL Privacy Service] Informationen zum Erstellen von Zugriffs-, Lösch- oder Verkaufs-Opt-out-Anfragen finden Sie in der [Handbuch zur Privacy Service-API](api/overview.md).
