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

Damit Adobe Experience Platform [!DNL Privacy Service] Kundenanfragen für ihre privaten Daten verarbeiten kann (einschließlich Zugriffs-, Lösch- oder Verkaufs-Opt-out-Anfragen), müssen eindeutige Kennungen für die Zuordnung eines bestimmten Kunden zu seinen gespeicherten privaten Daten in Ihren Adobe Experience Cloud-aktivierten Anwendungen bereitgestellt werden. [!DNL Privacy Service] verwendet diese Kennungen dann, um alle unter der Kundenidentität in [!DNL Experience Cloud] gespeicherten Daten zu erfassen und gemäß der Anforderung des Kunden zu verarbeiten.

In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

## Identitäten und Namespaces

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanäle interagieren kann, kann es schwierig sein, die unterschiedlichen Kennungen, die aus diesen vielen Interaktionen erfasst werden, miteinander abzustimmen. Dies wiederum kann es schwierig machen, in Ihren [!DNL Experience Cloud] -Anwendungen zu bestimmen, welche Daten zu einer bestimmten Person gehören.

Bei der Verarbeitung von Kundendatenanfragen in [!DNL Privacy Service] kann eine Identität beispielsweise einen Cookie-Wert darstellen, der unter einer von Adobe gesteuerten Domäne gesetzt wird, einen Cookie-Wert unter einer Drittanbieterdomäne, der für Adobe freigegeben ist, oder eine benutzerdefinierte ID, die Sie explizit in Ihrem Unternehmen definieren.

Daher ist es erforderlich, dass jede an [!DNL Privacy Service] gesendete Identität mit einem Namespace versehen wird, der Kontext bietet, indem der Identitätswert mit seinem Ursprungssystem in Beziehung gesetzt wird. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Adobe Experience Platform Identity Service verwaltet einen Speicher mit global definierten und benutzerdefinierten Identitäts-Namespaces. Weitere Informationen zu Namespaces finden Sie in [Identitäts-Namespace – Übersicht](../identity-service/features/namespaces.md). Eine Liste der Standard-Namespaces und Namespace-Kennzeichnungen, die häufig in [!DNL Privacy Service] verwendet werden, finden Sie im Abschnitt [Anhang ](api/appendix.md) im API-Handbuch.

## ECID- und Opt-in-Service

Adobe Experience Cloud [!DNL Identity Service] dient als gemeinsames Identifizierungs-Framework für [!DNL Experience Cloud] und weist jedem Site-Besucher eine eindeutige, beständige ID zu. Die [!DNL Experience Cloud]-ID (ECID) verfolgt die Aktivität eines Kunden durch Verwendung eines Erstanbieter-Cookies, kann ein Gerät über mehrere Anwendungen hinweg eindeutig identifizieren und ermöglicht es Ihnen, denselben Site-Besucher und dessen Daten in verschiedenen [!DNL Experience Cloud]-Anwendungen zu identifizieren. Weitere Informationen finden Sie in [Experience Cloud Identity Service – Übersicht](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Mit dem Opt-in-Dienst, einer Erweiterung von [!DNL Experience Cloud Identity Service], können Sie Protokolle in Ihrer Anwendung einrichten, mit denen Besucher bestimmen können, ob Sie ein Cookie auf dem Gerät oder Browser des Besuchers setzen können. Ausführlichere Informationen zu Opt-in Service, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der [Opt-in Service-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de).

Nachdem Ihren Site-Besuchern ECIDs zugewiesen wurden, können Sie diese IDs mit der Adobe [!DNL Privacy JavaScript Library] abrufen, um sie in Datenschutzanfragen zu verwenden, wie im nächsten Abschnitt beschrieben.

## [!DNL Privacy JS Library]

Der [!DNL Adobe Privacy JavaScript Library] bietet mehrere Funktionen, mit denen Sie Kundenidentitäten abrufen und entfernen können, die im Browser gespeichert sind. Die Bibliothek kann so konfiguriert werden, dass Identitätsinformationen aus verschiedenen Adobe-Anwendungen, einschließlich ECID, abgerufen werden können. Durch die Verwendung von Rückrufen oder Zusagen können Sie erfolgreich abgerufene IDs programmgesteuert verarbeiten und an die [!DNL Privacy Service] -API senden.

Weitere Informationen zu [!DNL Privacy JS Library], einschließlich Codebeispielen für verschiedene gängige Anwendungsfälle, finden Sie in der [Übersicht zur Privacy JS Library](js-library.md) .

## Nächste Schritte

Dieses Dokument bietet einen kurzen Überblick über die zentralen Konzepte zum Abrufen von Kundenidentitätsdaten zur Verwendung in Datenschutzanfragen. Es wird empfohlen, über die Dokumentations-Links in den einzelnen Abschnitten auf detailliertere Informationen über diese Konzepte und Dienste zuzugreifen. Anweisungen zum Senden abgerufener IDs an [!DNL Privacy Service] zum Erstellen von Zugriffs-, Lösch- oder Verkaufs-Opt-out-Anfragen finden Sie im [Privacy Service API-Handbuch](api/overview.md).
