---
keywords: Experience Platform;Home;beliebte Themen;ECID;ecid
solution: Experience Platform
title: Identitätsdaten für Datenschutzanfragen
topic-legacy: overview
description: In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 44%

---

# Identitätsdaten für Datenschutzanfragen

Damit Adobe Experience Platform [!DNL Privacy Service] Kundenanforderungen für ihre privaten Daten verarbeiten kann (einschließlich Zugriffsanfragen, Löschanfragen oder Ausschlussanfragen), müssen eindeutige IDs bereitgestellt werden, die einen bestimmten Kunden mit den gespeicherten privaten Daten in Ihren Adobe Experience Cloud-fähigen Anwendungen verknüpfen. [!DNL Privacy Service] verwendet diese Kennungen dann, um alle unter der Kundenidentität in gespeicherten Daten zu erfassen und gemäß der Kundenanfrage zu verarbeiten.[!DNL Experience Cloud]

In diesem Dokument finden Sie allgemeine Anweisungen zur Konfiguration Ihrer Datenvorgänge und zur Nutzung der Adobe-Technologien, um die entsprechenden Identitätsinformationen für Datenschutzanfragen von Kunden effektiv abzurufen.

## Identitäten und Namespaces

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanal interagieren kann, kann es schwierig sein, die unterschiedlichen Kennungen, die aus diesen vielen Interaktionen erfasst werden, miteinander in Einklang zu bringen. Dies wiederum kann die Feststellung erschweren, welche Daten zu einer bestimmten Person in Ihren [!DNL Experience Cloud]-Anwendungen gehören.

Bei der Bearbeitung von Kundendatenanforderungen in [!DNL Privacy Service] kann eine Adobe beispielsweise einen Cookie-Wert darstellen, der unter einer von der  gesteuerten Domäne, einem Cookie-Wert unter einer Drittanbieterdomäne und der für die Adobe freigegeben wurde, oder einen benutzerdefinierten Bezeichner, den Sie in Ihrer IMS-Organisation explizit definieren.

Daher ist es erforderlich, dass jede an [!DNL Privacy Service] gesendete Identität mit einem Namensraum verknüpft wird, der Kontext bereitstellt, indem der Identitätswert mit dem zugehörigen Herkunft-System verknüpft wird. Ein Namespace kann ein allgemeines Konzept wie eine E-Mail-Adresse („E-Mail“) darstellen oder die Identität einer bestimmten Anwendung zuordnen, z. B. eine Adobe Advertising Cloud-ID („AdCloud“) oder eine Adobe Target-ID („TNTID“).

Adobe Experience Platform Identity Service verwaltet einen Speicher mit global definierten und benutzerdefinierten Identitäts-Namespaces. Weitere Informationen zu Namespaces finden Sie in [Identitäts-Namespace – Übersicht](../identity-service/namespaces.md). Eine Liste der in [!DNL Privacy Service] gebräuchlichen Namensraum und Namensraum-Qualifikatoren finden Sie im Abschnitt [Anhang](api/appendix.md) im Entwicklerhandbuch.

## ECID- und Opt-in-Service

Adobe Experience Cloud [!DNL Identity Service] dient als gemeinsames Identifizierungsframework für [!DNL Experience Cloud] und weist jedem Site-Besucher eine eindeutige, beständige ID zu. Die [!DNL Experience Cloud]-ID (ECID) verfolgt die Aktivität eines Kunden durch Verwendung eines Erstanbieter-Cookies, kann ein Gerät über mehrere Anwendungen hinweg eindeutig identifizieren und ermöglicht es Ihnen, denselben Site-Besucher und dessen Daten in verschiedenen [!DNL Experience Cloud]-Anwendungen zu identifizieren. Weitere Informationen finden Sie in [Experience Cloud Identity Service – Übersicht](https://docs.adobe.com/content/help/de-DE/id-service/using/intro/overview.html).

Mit dem optionalen Dienst, einer Erweiterung von [!DNL Experience Cloud Identity Service], können Sie Protokolle für Ihre Anwendung einrichten, damit Besucher bestimmen können, ob ein Cookie auf dem Gerät oder Browser des Besuchers gesetzt werden kann. Ausführlichere Informationen zu Opt-in Service, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der [Opt-in Service-Dokumentation](https://docs.adobe.com/content/help/de-DE/id-service/using/implementation/opt-in-service/optin-overview.html).

Sobald Ihren Site-Besuchern ECIDs zugewiesen wurden, können Sie diese IDs mit der Adobe [!DNL Privacy JavaScript Library] abrufen, um sie in Datenschutzanforderungen zu verwenden, wie im nächsten Abschnitt beschrieben.

## [!DNL Privacy JS Library]

Das [!DNL Adobe Privacy JavaScript Library] bietet mehrere Funktionen, mit denen Sie im Browser gespeicherte Kundenidentitäten abrufen und entfernen können. Die Bibliothek kann so konfiguriert werden, dass Identitätsinformationen aus verschiedenen Adobe-Anwendungen, einschließlich ECID, abgerufen werden können. Mithilfe von Rückrufen oder Versprechungen können Sie erfolgreich abgerufene IDs programmgesteuert verarbeiten und an die [!DNL Privacy Service]-API senden.

Weitere Informationen zu [!DNL Privacy JS Library], einschließlich Codebeispiele für verschiedene gängige Einsatzfälle, finden Sie in der [Übersicht über die JS-Bibliothek zum Datenschutz](js-library.md).

## Nächste Schritte

Dieses Dokument bietet einen kurzen Überblick über die zentralen Konzepte zum Abrufen von Kundenidentitätsdaten zur Verwendung in Datenschutzanfragen. Es wird empfohlen, über die Dokumentations-Links in den einzelnen Abschnitten auf detailliertere Informationen über diese Konzepte und Dienste zuzugreifen. Anweisungen zum Senden abgerufener IDs an [!DNL Privacy Service] zum Erstellen von Zugriffs-, Löschungs- oder Ausschluss-of-Sale-Anforderungen finden Sie im [Privacy Service-Entwicklerhandbuch](api/getting-started.md).
