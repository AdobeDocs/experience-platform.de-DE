---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für Customer Profil-API in Echtzeit
topic: guide
translation-type: tm+mt
source-git-commit: 8449681a7fd0fc5dccf4837a1e8e512f1e2f2601
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---


# Entwicklerhandbuch für Customer Profil-API in Echtzeit

Mit dem Echtzeit-Profil können Sie eine ganzheitliche Ansicht Ihrer einzelnen Kunden in Adobe Experience Platform anzeigen. Mit Profil können Sie unterschiedliche Kundendaten aus mehreren Kanälen, z. B. Online-, Offline-, CRM- und Drittanbieter-Daten, in einer einheitlichen Ansicht zusammenfassen, die eine umsetzbare Zeitstempel-Übersicht über jede Kundeninteraktion bietet.

## Erste Schritte {#getting-started}

Mithilfe der Echtzeit-Client-Profil-API können Sie grundlegende CRUD-Vorgänge für Profil-Ressourcen durchführen, z. B. die Konfiguration berechneter Attribute, den Zugriff auf Entitäten, den Export von Profil-Daten und das Löschen nicht benötigter Datensätze oder Stapel.

Die Verwendung dieses Entwicklerhandbuchs erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die mit der Arbeit mit Profil-Daten verbunden sind. Bevor Sie mit der Echtzeit-Client-Profil-API arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [Echtzeit-Profil](../home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Erhalten Sie eine bessere Ansicht Ihres Kundenverhaltens, indem Sie Identitäten zwischen verschiedenen Geräten und Systemen überbrücken.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
* [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um Profil-API-Endpunkte erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

Die Dokumentation zur Echtzeit-Client-Profil-API enthält Beispiele für API-Aufrufe, die zeigen, wie Anforderungen korrekt formatiert werden. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Erforderliche Kopfzeilen

Die API-Dokumentation erfordert auch, dass Sie das [Authentifizierungstraining](../../tutorials/authentication.md) abgeschlossen haben, um Platform-Endpunkte erfolgreich aufrufen zu können. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Header in Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Anforderungen an Plattform-APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang stattfindet:

* x-sandbox-name: `{SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Alle Anforderungen mit einer Nutzlast im Anforderungstext (wie POST-, PUT- und PATCH-Aufrufe) müssen einen `Content-Type` Header enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern bereitgestellt.

## (Alpha) Berechnete Attribute

>[!IMPORTANT]
>Die Funktion für berechnete Attribute ist alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können geändert werden.

Berechnete Attribute ermöglichen es Ihnen, den Feldwert anhand anderer Werte, Berechnungen und Ausdruck automatisch zu berechnen. Berechnete Attribute werden auf Profil-Ebene ausgeführt, d. h., Sie können Werte über alle Datensätze und Ereignis hinweg Aggregat haben.

Jedes berechnete Attribut enthält einen Ausdruck, oder &#39;Regel&#39;, der eingehende Daten auswertet und den sich ergebenden Wert in einem Profil-Attribut oder in einem Ereignis speichert. Diese Berechnungen helfen Ihnen, Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungen einfach zu beantworten, ohne dass Sie bei jeder erforderlichen Information manuell komplexe Berechnungen durchführen müssen.

Mithilfe der `config/computedAttributes` Endpunkte können Sie berechnete Attribute erstellen, Ansichten vornehmen, bearbeiten und löschen. Weitere Informationen zur Verwendung dieser Endpunkte finden Sie im Unterhandbuch zu [berechneten Attributen](computed-attributes.md).

## Edge-Prognosen

Die Adobe Experience Platform ermöglicht die Personalisierung von Kundenerlebnissen in Echtzeit, indem sie Daten auf strategisch wichtigen Servern, die &quot;Kanten&quot;genannt werden, leicht zugänglich macht. Die Echtzeit-Client-Profil-API bietet Endpunkte zum Arbeiten mit Kanten über Komponenten, die als &quot;Projektionen&quot;bezeichnet werden. Dazu gehören Projektionskonfigurationen, um zu bestimmen, welche Daten auf die einzelnen Kanten projiziert werden sollen, sowie Projektionsziele, um zu definieren, wo eine Projektion weitergeleitet werden soll.

Detaillierte Informationen zum Arbeiten mit Kehrprojektionen finden Sie im Unterleitfaden [für Kehrprojektionen](edge-projections.md).

## Entitäten

Über Adobe Experience Platform können Sie über RESTful-APIs oder die Benutzeroberfläche auf Echtzeit-Daten zum Profil von Kunden zugreifen. Um zu erfahren, wie Sie mithilfe der API auf Entitäten zugreifen können, die allgemein als &quot;Profil&quot;bezeichnet werden, führen Sie die Schritte aus, die im Unterhandbuch [für Entitäten beschrieben werden](entities.md).

## Zusammenführungsrichtlinien

Beim Zusammenführen von Daten aus mehreren Quellen in Experience Platform sind Zusammenführungsrichtlinien die Regeln, die Plattform verwendet, um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um individuelle Profil zu erstellen.

Mit der Echtzeit-Client-Profil-API können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im Unterleitfaden [Zusammenführungsrichtlinien](merge-policies.md).

Eine Anleitung zum Arbeiten mit Richtlinien zum Zusammenführen mithilfe der Plattform-Benutzeroberfläche finden Sie im Benutzerhandbuch [](../ui/merge-policies.md)Richtlinien zusammenführen.

## Profil-Systemaufträge

Daten, die in Platform aufgenommen werden, werden im Data Lake sowie im Echtzeit-Kundendatenspeicher gespeichert. Gelegentlich kann es erforderlich sein, einen Datensatz oder Stapel aus dem Profil-Store zu löschen, um Daten zu entfernen, die Sie nicht mehr benötigen oder die fälschlicherweise hinzugefügt wurden. Dies erfordert die Verwendung der API zum Erstellen eines Profil-Systemauftrags, der als &quot;Löschanforderung&quot;bezeichnet wird und bei Bedarf auch bearbeitet, überwacht oder gelöscht werden kann.

Um zu erfahren, wie Sie mit Löschanfragen mithilfe der `/system/jobs` Endpunkte in der Echtzeit-Client-Profil-API arbeiten, führen Sie die Schritte aus, die im Unterhandbuch [zu](profile-system-jobs.md)Profil-Systemaufträgen beschrieben sind.

## Nächste Schritte

Wenn Sie mit der Echtzeit-Client-Profil-API mit dem Aufrufen beginnen möchten, wählen Sie eine der Unterleitfäden aus, um zu erfahren, wie Sie bestimmte Profil-bezogene Endpunkte verwenden. Weitere Informationen zum Arbeiten mit Profil-Daten mithilfe der Plattform-Benutzeroberfläche finden Sie im Benutzerhandbuch [zum](../ui/user-guide.md)Echtzeit-Profil.