---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sandbox-Übersicht
topic: overview
translation-type: tm+mt
source-git-commit: 564940f37b66159c84ca7402bd3648010232182b
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 4%

---


# Sandbox-Übersicht

Die Adobe Experience Platform wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene zu erweitern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

In order to address this need, Experience Platform provides **sandboxes** which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

Dieses Dokument bietet einen Überblick über Sandboxen in Experience Platform auf hoher Ebene.

## Sandboxes

Sandboxes sind virtuelle Partitionen innerhalb einer Instanz von Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer digitalen Erlebnisanwendungen ermöglichen. Eine Experience Platform-Instanz unterstützt eine Produktions-Sandbox und mehrere Nicht-Produktions-Sandboxes, wobei jede Sandbox eine eigene, unabhängige Bibliothek mit Plattformressourcen (einschließlich Schemas, Datensätzen, Profilen usw.) unterhält.  Alle Inhalte und Aktionen, die innerhalb einer Sandbox durchgeführt werden, sind auf diese Sandbox beschränkt und wirken sich nicht auf andere Sandboxen aus.

Mit Sandboxen ohne Produktionsumfang können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktionssandbox zu beeinträchtigen. Darüber hinaus verfügen Sandboxen, die keine Produktion sind, über eine Reset-Funktion, mit der alle vom Kunden erstellten Ressourcen aus der Sandbox entfernt werden. Nicht-produzierende Sandboxen können nicht in Produktions-Sandboxen konvertiert werden.

>[!NOTE] Wenn eine Sandbox zum ersten Mal erstellt wird, enthält sie keine Daten. Da jede Sandbox ihren eigenen isolierten Datenspeicher unterhält, müssen sie auch ihre Daten unabhängig erfassen.

Zusammenfassend lässt sich sagen, dass Sandboxen die folgenden Vorteile bieten:

* **Anwendungs-Lebenszyklusmanagement**: Erstellen Sie separate virtuelle Umgebung, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.
* **Projekt- und Markenmanagement**: Mehrere Projekte können parallel im selben IMS-Org ausgeführt werden, während Isolation und Zugriffskontrolle gewährleistet sind. Zukünftige Versionen bieten Unterstützung für die Bereitstellung in mehreren Regionen.
* **Flexibles Entwicklungs-Ökosystem**: Bieten Sie Sandboxen auf nahtlose, skalierbare und kostengünstige Weise für Exploration, Aktivierung und Demonstration an.

## Zugriffskontrolle für Sandboxen

Standardmäßig haben alle Benutzer eines Unternehmens Zugriff auf eine Produktions-Sandbox. Der Zugriff auf Nicht-Produktions-Sandboxen muss von einem Systemadministrator, Produktadministrator oder Produktadministrator über die [Adobe Admin Console](https://adminconsole.adobe.com)gewährt werden.

Um Sandbox-Sandboxen, die keine Produktionsumgebung sind, Ansicht, zu erstellen, zu aktualisieren oder zu löschen, müssen den Benutzern außerdem Sandbox-Administratorrechte gewährt werden.

Weitere Informationen zum Verwalten von Rollen und Berechtigungen für Sandboxen finden Sie in der Übersicht über die [Zugriffskontrolle](../access-control/home.md).

## Sandboxes in der Benutzeroberfläche der Experience Platform

In der Benutzeroberfläche [der](https://platform.adobe.com)Experience Platform können Benutzer mithilfe des **Sandbox-Umschalters** oben links auf dem Bildschirm zwischen den Sandboxen wechseln, auf die sie Zugriff haben.  Benutzer mit Sandbox-Administratorberechtigungen haben auch Zugriff auf die Registerkarte &quot; **Sandboxen** &quot;in der linken Navigation, auf der sie Sandboxen für ihre Organisation Ansicht und verwalten können. Weitere Informationen zum Arbeiten mit Sandboxen in der Benutzeroberfläche finden Sie im [Sandbox-Benutzerhandbuch](ui/overview.md).

## Sandboxes in Experience Platform-APIs

Beim Aufrufen von Experience Platform-APIs muss unter der Kopfzeile ein Sandbox-Name angegeben werden `x-sandbox-name`. Wenn Sie beispielsweise die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) aufrufen, um alle Datensätze in der Produktions-Sandbox Ansicht, wird der Name der Sandbox (&quot;prod&quot;) als Kopfzeile in der API-Anforderung bereitgestellt:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Wenn `x-sandbox-name` kein API-Aufruf enthalten ist, verwendet das System stattdessen eine Standard-Sandbox. Es empfiehlt sich jedoch, diesen Header immer in alle API-Aufrufe aufzunehmen, auch wenn die Standard-Sandbox verwendet wird. Aus diesem Grund wird in der API-Dokumentation für Experience Platform `x-sandbox-name` als erforderlicher Header behandelt.

### Sandbox-API

Die Sandbox-API ermöglicht Ihnen die Verwaltung von Sandboxen mithilfe von RESTful-API-Operationen. Detaillierte Informationen zur Verwendung der API, einschließlich ordnungsgemäß formatierter Anforderungen und Beispielantworten, finden Sie im [Sandbox-Entwicklerhandbuch](api/getting-started.md) .

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie mit den wesentlichen Konzepten zu Sandboxen in Experience Platform vertraut gemacht. Ausführliche Anweisungen zum Verwalten von Sandboxen finden Sie im [Benutzerhandbuch](ui/overview.md) für die Benutzeroberfläche oder im [Entwicklerhandbuch](./api/getting-started.md) für die API.

Sandboxen dienen zwar als nützliches Tool zum Isolieren von Plattformfunktionen für Ihr Entwicklungsteam, aber Sie können auch eine granularere Zugriffskontrolle über die Adobe Admin-Konsole verwalten. See the [access control overview](../access-control/home.md) for more information.