---
keywords: Experience Platform; Homepage; beliebte Themen; ECID; ecid
solution: Experience Platform
title: Identitätsdaten für Datenschutzanfragen
topic-legacy: overview
description: In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: d316c199c7e2d87d175015c1828af6fd0d57f32a
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 43%

---

# Identitätsdaten für Datenschutzanfragen

Damit Adobe Experience Platform [!DNL Privacy Service] Kundenanfragen für ihre privaten Daten verarbeiten kann (einschließlich Zugriffs-, Lösch- oder Verkaufs-Opt-out-Anfragen), müssen eindeutige Kennungen bereitgestellt werden, die einen bestimmten Kunden mit seinen gespeicherten privaten Daten in Ihren Adobe Experience Cloud-fähigen Anwendungen verknüpfen. [!DNL Privacy Service] verwendet diese Kennungen dann, um alle unter der Kundenidentität in gespeicherten Daten zu erfassen und gemäß der Kundenanfrage zu verarbeiten.[!DNL Experience Cloud]

In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

## Identitäten und Namespaces

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanal interagieren kann, kann es schwierig sein, die unterschiedlichen Kennungen, die aus diesen vielen Interaktionen erfasst werden, miteinander in Einklang zu bringen. Dies wiederum kann es schwierig machen, in Ihren [!DNL Experience Cloud] -Anwendungen zu bestimmen, welche Daten zu einer bestimmten Person gehören.

Bei der Verarbeitung von Kundendatenanfragen in [!DNL Privacy Service] kann eine Identität beispielsweise einen Cookie-Wert darstellen, der unter einer von der Adobe gesteuerten Domäne gesetzt wird, einen Cookie-Wert unter einer Drittanbieterdomäne, der für Adobe freigegeben ist, oder eine benutzerdefinierte ID, die Sie explizit in Ihrer IMS-Organisation definieren.

Daher ist es erforderlich, dass jede an [!DNL Privacy Service] gesendete Identität mit einem Namespace versehen wird, der einen Kontext bietet, indem der Identitätswert mit seinem Ursprungssystem in Beziehung gesetzt wird. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Adobe Experience Platform Identity Service verwaltet einen Speicher mit global definierten und benutzerdefinierten Identitäts-Namespaces. Weitere Informationen zu Namespaces finden Sie in [Identitäts-Namespace – Übersicht](../identity-service/namespaces.md). Eine Liste der Standard-Namespaces und Namespace-Kennzeichnungen, die häufig in [!DNL Privacy Service] verwendet werden, finden Sie im Abschnitt [Anhang](api/appendix.md) im Entwicklerhandbuch.

## ECID- und Opt-in-Service

Adobe Experience Cloud [!DNL Identity Service] dient als gemeinsames Identifizierungs-Framework für [!DNL Experience Cloud] und weist jedem Site-Besucher eine eindeutige, beständige ID zu. Die [!DNL Experience Cloud]-ID (ECID) verfolgt die Aktivität eines Kunden durch Verwendung eines Erstanbieter-Cookies, kann ein Gerät über mehrere Anwendungen hinweg eindeutig identifizieren und ermöglicht es Ihnen, denselben Site-Besucher und dessen Daten in verschiedenen [!DNL Experience Cloud]-Anwendungen zu identifizieren. Weitere Informationen finden Sie in [Experience Cloud Identity Service – Übersicht](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Mit Opt-in Service, einer Erweiterung von [!DNL Experience Cloud Identity Service], können Sie Protokolle in Ihrer Anwendung einrichten, mit denen Besucher bestimmen können, ob Sie ein Cookie auf dem Gerät oder Browser des Besuchers setzen können. Ausführlichere Informationen zu Opt-in Service, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der [Opt-in Service-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de).

Nachdem Ihren Site-Besuchern ECIDs zugewiesen wurden, können Sie die Adobe [!DNL Privacy JavaScript Library] verwenden, um diese IDs zur Verwendung in Datenschutzanfragen abzurufen, wie im nächsten Abschnitt beschrieben.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library] bietet mehrere Funktionen, mit denen Sie im Browser gespeicherte Kundenidentitäten abrufen und entfernen können. Die Bibliothek kann so konfiguriert werden, dass Identitätsinformationen aus verschiedenen Adobe-Anwendungen, einschließlich ECID, abgerufen werden können. Durch die Verwendung von Rückrufen oder Zusagen können Sie erfolgreich abgerufene IDs programmgesteuert verarbeiten und an die [!DNL Privacy Service]-API senden.

Weitere Informationen zu [!DNL Privacy JS Library], einschließlich Codebeispielen für verschiedene gängige Anwendungsfälle, finden Sie in der [Übersicht über die Privacy JS Library](js-library.md).

## Nächste Schritte

Dieses Dokument bietet einen kurzen Überblick über die zentralen Konzepte zum Abrufen von Kundenidentitätsdaten zur Verwendung in Datenschutzanfragen. Es wird empfohlen, über die Dokumentations-Links in den einzelnen Abschnitten auf detailliertere Informationen über diese Konzepte und Dienste zuzugreifen. Anweisungen zum Senden abgerufener IDs an [!DNL Privacy Service] zum Erstellen von Zugriffs-, Lösch- oder Verkaufs-Opt-out-Anfragen finden Sie im [Privacy Service-Entwicklerhandbuch](api/getting-started.md).
