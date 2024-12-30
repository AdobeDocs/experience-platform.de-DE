---
keywords: Experience Platform;Startseite;beliebte Themen;ECID;ecid
solution: Experience Platform
title: Identitätsdaten für Datenschutzanfragen
description: In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 40%

---

# Identitätsdaten für Datenschutzanfragen

Damit Adobe Experience Platform [!DNL Privacy Service] Kundenanfragen für ihre privaten Daten (einschließlich Zugriffs-, Lösch- oder Opt-out-Anfragen) verarbeiten kann, müssen ihr eindeutige Kennungen bereitgestellt werden, die eine bestimmte Kundin oder einen bestimmten Kunden mit ihren gespeicherten privaten Daten in Ihren für Adobe Experience Cloud aktivierten Anwendungen verknüpfen. [!DNL Privacy Service] verwendet diese Kennungen dann, um alle Daten zu erfassen, die unter der Identität des Kunden in [!DNL Experience Cloud] gespeichert sind, und sie entsprechend der Anfrage des Kunden zu verarbeiten.

In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

## Identitäten und Namespaces

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanäle interagieren kann, kann es schwierig sein, die unterschiedlichen Kennungen, die aus diesen vielen Interaktionen erfasst werden, miteinander abzustimmen. Dadurch lässt sich wiederum nur schwer feststellen, welche Daten zu einer bestimmten Person in Ihren [!DNL Experience Cloud] gehören.

Bei der Verarbeitung von Kundendatenanfragen in [!DNL Privacy Service] kann eine Identität beispielsweise einen Cookie-Wert darstellen, der unter einer von Adobe kontrollierten Domain festgelegt wurde, einen Cookie-Wert unter einer Domain eines Drittanbieters, der für Adobe freigegeben wurde, oder eine benutzerdefinierte Kennung, die Sie in Ihrem Unternehmen explizit definieren.

Daher muss jede an [!DNL Privacy Service] gesendete Identität von einem Namespace begleitet sein, der Kontext bietet, indem der Identitätswert mit dem System seiner Herkunft verknüpft wird. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Adobe Experience Platform Identity Service verwaltet einen Speicher mit global definierten und benutzerdefinierten Identitäts-Namespaces. Weitere Informationen zu Namespaces finden Sie in [Identitäts-Namespace – Übersicht](../identity-service/features/namespaces.md). Eine Liste der Standard-Namespaces und Namespace-Qualifizierer, die häufig in [!DNL Privacy Service] verwendet werden, finden Sie im [Anhang](api/appendix.md) im API-Handbuch.

## ECID- und Opt-in-Service

Adobe Experience Cloud [!DNL Identity Service] dient als gemeinsames Identifizierungs-Framework für [!DNL Experience Cloud] und weist jedem Site-Besucher eine eindeutige, beständige ID zu. Die [!DNL Experience Cloud]-ID (ECID) verfolgt die Aktivität eines Kunden mithilfe eines Erstanbieter-Cookies. Sie kann ein Gerät über mehrere Anwendungen hinweg eindeutig identifizieren und ermöglicht es Ihnen, denselben Site-Besucher und dessen Daten in verschiedenen [!DNL Experience Cloud]-Anwendungen zu identifizieren. Weitere Informationen finden Sie in [Experience Cloud Identity Service – Übersicht](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Mit dem Opt-in-Dienst, einer Erweiterung von [!DNL Experience Cloud Identity Service], können Sie Protokolle in Ihrer Anwendung einrichten, damit Besuchende bestimmen können, ob Sie ein Cookie auf dem Gerät oder Browser des Besuchers setzen können. Ausführlichere Informationen zu Opt-in Service, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der [Opt-in Service-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=de).

Sobald Ihren Site-Besuchern ECIDs zugewiesen wurden, können Sie die Adobe-[!DNL Privacy JavaScript Library] verwenden, um diese IDs zur Verwendung in Datenschutzanfragen abzurufen, wie im nächsten Abschnitt beschrieben.

## [!DNL Privacy JS Library]

Die [!DNL Adobe Privacy JavaScript Library] bietet mehrere Funktionen, mit denen Sie im Browser gespeicherte Kundenidentitäten abrufen und entfernen können. Die Bibliothek kann so konfiguriert werden, dass Identitätsinformationen aus verschiedenen Adobe-Anwendungen, einschließlich ECID, abgerufen werden können. Durch die Verwendung von Callbacks oder Promises können Sie erfolgreich abgerufene IDs programmgesteuert verarbeiten und an die [!DNL Privacy Service]-API senden.

Weitere Informationen zu [!DNL Privacy JS Library], einschließlich Code-Beispielen für verschiedene gängige Anwendungsfälle, finden Sie unter [Übersicht über die Privacy JS Library](js-library.md).

## Nächste Schritte

Dieses Dokument bietet einen kurzen Überblick über die zentralen Konzepte zum Abrufen von Kundenidentitätsdaten zur Verwendung in Datenschutzanfragen. Es wird empfohlen, über die Dokumentations-Links in den einzelnen Abschnitten auf detailliertere Informationen über diese Konzepte und Dienste zuzugreifen. Anweisungen zum Senden abgerufener IDs an [!DNL Privacy Service] zum Erstellen von Zugriffs-, Lösch- oder Opt-out-Verkaufsanfragen finden Sie im [Privacy Service-API-Handbuch](api/overview.md).
