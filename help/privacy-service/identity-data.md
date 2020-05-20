---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identitätsdaten für Datenschutzanforderungen
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 3%

---


# Identitätsdaten für Datenschutzanforderungen

Damit der Adobe Experience Platform-Datenschutzdienst Kundenanforderungen für ihre privaten Daten verarbeiten kann (z. B. Anforderungen zum Zugriff, Löschen oder Ausschluss vom Verkauf), müssen eindeutige IDs für den Zugriff eines bestimmten Kunden auf die gespeicherten privaten Daten in den Anwendungen bereitgestellt werden, die mit Adobe Experience Cloud aktiviert wurden. Der Datenschutzdienst verwendet diese IDs dann, um alle unter der Identität des Kunden in Experience Cloud gespeicherten Daten zu sammeln und entsprechend der Anforderung des Kunden zu verarbeiten.

Dieses Dokument enthält allgemeine Anleitungen zum Konfigurieren Ihrer Datenvorgänge und zum Einsatz von Adobe-Technologien zum effektiven Abrufen der entsprechenden Identitätsdaten für Datenschutzanforderungen.

## Identitäten und Namensraum

Wenn ein Kunde mit Ihrer Marke über mehrere verschiedene Kanal interagieren kann, kann es schwierig sein, die unterschiedlichen Identifikatoren, die aus diesen vielen Interaktionen aufgezeichnet werden, miteinander in Einklang zu bringen. Dies wiederum kann die Feststellung erschweren, welche Daten zu einer bestimmten Person in Ihren Experience Cloud-Anwendungen gehören.

Bei der Bearbeitung von Kundendatenanforderungen im Datenschutzdienst kann eine Identität beispielsweise einen Cookie-Wert darstellen, der unter einer von Adobe kontrollierten Domäne eingestellt wird, einen Cookie-Wert unter einer Drittanbieterdomäne, der für Adobe freigegeben wird, oder einen benutzerdefinierten Bezeichner, den Sie in Ihrer IMS-Organisation explizit definieren.

Daher ist es erforderlich, dass jede an den Datenschutzdienst gesendete Identität mit einem **Namensraum** versehen wird, der einen Kontext bietet, indem der Identitätswert mit seinem System der Herkunft verknüpft wird. Ein Namensraum kann ein allgemeines Konzept wie eine E-Mail-Adresse (&quot;E-Mail&quot;) oder die Identität einer bestimmten Anwendung zuordnen, z. B. einer Adobe Advertising Cloud ID (&quot;AdCloud&quot;) oder einer Adobe-Zielgruppe-ID (&quot;TNTID&quot;).

Der Identitätsdienst für Adobe Experience Platform verwaltet einen Store von global definierten und benutzerdefinierten Identitäts-Namensräumen. Weitere Informationen zu Namensräumen finden Sie in der Übersicht über den [Identitäts-Namensraum](../identity-service/namespaces.md). Eine Liste der im Datenschutzdienst häufig verwendeten Namensraum und Namensraum-Qualifikatoren finden Sie im [Anhang](api/appendix.md) im Entwicklerhandbuch.

## ECID- und Einwahldienst

Der Adobe Experience Cloud-Identitätsdienst dient als gemeinsames Identifizierungsframework für Experience Cloud und weist jedem Site-Besucher eine eindeutige, beständige ID zu. Mit der Experience Cloud ID (ECID) wird die Aktivität eines Kunden durch die Verwendung eines Erstanbieter-Cookies verfolgt, ein Gerät kann für mehrere Anwendungen eindeutig identifiziert werden und Sie können denselben Site-Besucher und dessen Daten in verschiedenen Experience Cloud-Anwendungen identifizieren. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/de-DE/id-service/using/intro/overview.html) for more information.

Mit dem optionalen Dienst, einer Erweiterung des Experience Cloud-Identitätsdienstes, können Sie Protokolle für Ihre Anwendung einrichten, mit denen Besucher bestimmen können, ob ein Cookie auf dem Gerät oder Browser des Besuchers gesetzt werden kann. Ausführlichere Informationen zum Opt-in-Dienst, einschließlich der Einrichtung des Dienstes für Ihre Anwendung, finden Sie in der Dokumentation zum [Einstiegsdienst](https://docs.adobe.com/content/help/de-DE/id-service/using/implementation/opt-in-service/optin-overview.html).

Sobald Ihren Site-Besuchern ECIDs zugewiesen wurden, können Sie diese IDs mithilfe der Adobe Privacy JavaScript Library abrufen, um sie in Datenschutzanforderungen zu verwenden, wie im nächsten Abschnitt beschrieben.

## Datenschutz-JS-Bibliothek

Die Adobe Privacy JavaScript Library bietet mehrere Funktionen, mit denen Sie im Browser gespeicherte Kundenidentitäten abrufen und entfernen können. Die Bibliothek kann konfiguriert werden, um Identitätsinformationen aus verschiedenen Adobe-Anwendungen abzurufen, einschließlich ECID. Mithilfe von Rückrufen oder Versprechungen können Sie erfolgreich abgerufene IDs programmgesteuert verarbeiten und an die Datenschutzdienst-API senden.

Weitere Informationen zur Privacy JS Library, einschließlich Codebeispiele für verschiedene gängige Einsatzfälle, finden Sie in der Übersicht über die [Datenschutz-JS-Bibliothek](js-library.md).

## Nächste Schritte

Dieses Dokument vermittelte einen kurzen Überblick über die zentralen Konzepte, die beim Abrufen von Kundenidentitätsdaten für die Verwendung in Datenschutzanforderungen zum Einsatz kommen. Es wird empfohlen, die Links zur Dokumentation in den einzelnen Abschnitten zu lesen, um detaillierte Informationen zu diesen Konzepten und Diensten zu erhalten. Anweisungen zum Senden von abgerufenen IDs an den Datenschutzdienst zum Erstellen von Zugreifen, Löschen oder Ausschluss-von-Kauf-Anfragen finden Sie im Entwicklerhandbuch für den [Datenschutzdienst](api/getting-started.md).