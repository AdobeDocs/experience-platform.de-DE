---
keywords: Experience Platform;Startseite;beliebte Themen;Sandbox;Sandbox;Test;Test
solution: Experience Platform
title: Übersicht über Sandboxen
topic: Übersicht
description: Sandboxes sind virtuelle Partitionen innerhalb einer Instanz von Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglichen.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 78%

---


# Sandbox-Übersicht

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

Darum stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Dieses Dokument bietet einen Überblick über Sandboxes in Experience Platform.

## Sandboxes

>[!NOTE]
>
>Die Funktion &quot;Mehrere Produktions-Sandboxen&quot;befindet sich in der Betaphase.

Sandboxes sind virtuelle Partitionen innerhalb einer Instanz von Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglichen. Eine Experience Platform-Instanz unterstützt mehrere Produktions- und Nicht-Produktions-Sandboxen, wobei jede Sandbox eine eigene, unabhängige Bibliothek mit Plattformressourcen (einschließlich Schemas, Datensätzen, Profilen usw.) unterhält. Alle Inhalte und Aktionen, die innerhalb einer Sandbox ausgeführt werden, sind auf diese Sandbox beschränkt und wirken sich nicht auf andere Sandboxes aus.

Mit Nicht-Produktions-Sandboxes können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktions-Sandbox zu beeinträchtigen. Darüber hinaus verfügen sowohl Produktions- als auch Nicht-Produktions-Sandboxen über eine Reset-Funktion, mit der alle vom Kunden erstellten Ressourcen aus der Sandbox entfernt werden. Nicht-Produktions-Sandboxes können nicht in Produktions-Sandboxes umgewandelt werden. Mit einer Standardlizenz für Experience Platformen erhalten Sie fünf Sandboxen (eine Produktion und vier Nicht-Produktion). Sie können Pakete von zehn Sandboxen bis zu maximal 75 Sandboxen hinzufügen. Mit diesen zusätzlichen Sandboxen können sowohl Produktions- als auch Nicht-Produktionssandboxes erstellt werden. Für weitere Informationen wenden Sie sich bitte an Ihren IMS-Organisationsadministrator oder Ihren Vertriebsmitarbeiter für Adoben.

>[!NOTE]
>
> Direkt nach der Erstellung einer Sandbox enthält diese noch keine Daten. Da jede Sandbox einen eigenen isolierten Datenspeicher unterhält, müssen sie auch ihre Daten unabhängig erfassen.

Zusammenfassend kann man sagen, dass Sandboxes folgende Vorteile bieten:

* **Application Lifecycle Management**: Richten Sie separate virtuelle Umgebungen ein, um Programme für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.
* **Projekt- und Markenverwaltung**: Lassen Sie es zu, dass in derselben IMS-Organisation verschiedene Projekte parallel ausgeführt werden, während Isolation und Zugriffskontrolle gewährleistet bleiben. Zukünftige Versionen werden Unterstützung zur Bereitstellung in verschiedenen Regionen bieten.
* **Flexibles Entwicklungsökosystem**: Stellen Sie Sandboxes auf nahtlose, skalierbare und kostengünstige Weise für Erkundungs-, Unterstützungs- und Demonstrationszwecke bereit.

## Zugriffskontrolle für Sandboxes

Standardmäßig haben alle Benutzer einer Organisation Zugriff auf eine Produktions-Sandbox. Der Zugriff auf Nicht-Produktions-Sandboxes muss über die [Adobe Admin Console](https://adminconsole.adobe.com) von einem Systemadministrator, Produktadministrator oder Produktprofiladministrator gewährt werden.

Um Produktions- und Nicht-Produktions-Sandboxen Ansicht, zu erstellen, zu aktualisieren oder zu löschen, müssen den Benutzern außerdem Sandbox-Administratorberechtigungen gewährt werden.

Weiterführende Informationen zum Verwalten von Rollen und Berechtigungen für Sandboxes finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Sandboxes in der Benutzeroberfläche von Experience Platform

In der [Benutzeroberfläche von Experience Platform](https://platform.adobe.com) können Benutzer mit dem Steuerelement **Sandbox-Umschalter** oben links auf dem Bildschirm zwischen den Sandboxes wechseln, auf die sie Zugriff haben.  Benutzer mit Sandbox-Administratorberechtigungen haben außerdem Zugriff auf den Tab **[!UICONTROL Sandboxes]** im linken Navigationsbereich, wo sie Sandboxes für ihre Organisation anzeigen und verwalten können. Weiterführende Informationen zum Arbeiten mit Sandboxes in der Benutzeroberfläche finden Sie im [Sandbox-Benutzerhandbuch](ui/overview.md).

## Sandboxes in Experience Platform-APIs

Beim Aufrufen von Experience Platform-APIs muss unter der Kopfzeile `x-sandbox-name` ein Sandbox-Name angegeben werden. Wenn Sie beispielsweise den Befehl [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) aufrufen, um alle Datensätze in der Produktions-Sandbox Ansicht, wird der Name der Sandbox (&quot;prod&quot;) als Kopfzeile in der API-Anforderung bereitgestellt:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Wenn `x-sandbox-name` in einem API-Aufruf nicht enthalten ist, verwendet das System stattdessen eine Standard-Sandbox. Es empfiehlt sich jedoch, diese Kopfzeile stets in alle API-Aufrufe aufzunehmen (selbst wenn die Standard-Sandbox verwendet wird). Aus diesem Grund wird `x-sandbox-name` in der API-Dokumentation für Experience Platform als erforderliche Kopfzeile behandelt.

### Sandbox-API

Mit der Sandbox-API können Sie Sandboxes unter Verwendung von RESTful-API-Operationen verwalten. Genaue Informationen zur Verwendung der API, einschließlich ordnungsgemäß formatierter Anfragen und Beispielantworten, finden Sie im [Sandbox-Entwicklerhandbuch](api/getting-started.md).

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie sich mit den grundlegenden Konzepten von Sandboxes in Experience Platform vertraut gemacht. Ausführliche Anweisungen zum Verwalten von Sandboxes finden Sie im [Benutzerhandbuch](ui/overview.md) zur Benutzeroberfläche oder im [Entwicklerhandbuch](./api/getting-started.md) zur API.

Sandboxes dienen Ihrem Entwicklungs-Team als nützliches Tool zum Isolieren von Platform-Umgebungen; über die Adobe Admin Console Sie können aber auch eine granularere Zugriffskontrolle nutzen. Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).