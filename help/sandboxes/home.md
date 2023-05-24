---
keywords: Experience Platform;Startseite;beliebte Themen;sandbox;Sandbox;Test;Testen
solution: Experience Platform
title: Sandbox-Übersicht
description: Sandboxes sind virtuelle Partitionen innerhalb einer Instanz von Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglichen.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 100%

---

# Sandbox-Übersicht

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

Darum stellt Experience Platform Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Dieses Dokument bietet einen Überblick über Sandboxes in Experience Platform.

## Sandboxes

Sandboxes sind virtuelle Partitionen innerhalb einer Instanz von Experience Platform, die eine nahtlose Integration in den Entwicklungsprozess Ihrer Programme für digitale Erlebnisse ermöglichen. Alle Inhalte und Aktionen, die innerhalb einer Sandbox ausgeführt werden, sind auf diese Sandbox beschränkt und wirken sich nicht auf andere Sandboxes aus. Es werden zwei Arten von Sandboxes für Experience Platform unterstützt:

* **Produktions-Sandbox**: Eine Produktions-Sandbox ist für die Verwendung mit Profilen in Ihrer Produktionsumgebung vorgesehen. Platform ermöglicht es Ihnen, mehrere Produktions-Sandboxes zu erstellen, um die richtigen Funktionen für Daten zu bieten und gleichzeitig die Isolierung beim Betreiben beizubehalten. Mit dieser Funktion können Sie bestimmte Produktions-Sandboxes unterschiedlichen Geschäftsbereichen, Marken, Projekten oder Regionen zuweisen. Produktions-Sandboxes unterstützen eine Vielzahl von Produktionsprofilen bis hin zu Ihrer lizenzierten [!DNL Profile]-Verpflichtung (kumulativ über alle Ihre autorisierten Produktions-Sandboxes gemessen). Sie sind berechtigt, ein lizenziertes durchschnittliches Profil pro autorisiertem [!DNL Profile] zu verwenden (kumulativ über alle Ihre zulässigen Produktions-Sandboxes gemessen).
* **Entwicklungs-Sandbox**: Eine Entwicklungs-Sandbox ist eine Sandbox, die ausschließlich für die Entwicklung und Tests mit Nicht-Produktionsprofilen verwendet werden kann. Entwicklungs-Sandboxes unterstützen eine Anzahl von Nicht-Produktions-Profilen mit bis zu 10 % Ihrer lizenzierten [!DNL Profile]-Verpflichtung (kumulativ über alle autorisierten Entwicklungs-Sandboxes gemessen). Sie haben maximal Anspruch auf Folgendes:
   * Durchschnittlicher Umfang des Nicht-Produktionsprofils von 75 Kilobyte pro autorisiertem Nicht-Produktionsprofil (kumulativ gemessen in allen autorisierten Entwicklungs-Sandboxes);
   * Ein Batch-Segmentierungsauftrag pro Tag und pro Entwicklungs-Sandbox;
   * Ein Durchschnitt von 120 [!DNL Profile]-API-Aufrufen pro [!DNL Profile] pro Jahr (kumulativ über alle Ihre autorisierten Entwicklungs-Sandboxes hinweg gemessen).

Eine Experience Platform-Instanz unterstützt mehrere Produktions- sowie Entwicklungs-Sandboxes, wobei jede eine eigene unabhängige Bibliothek mit Platform-Ressourcen (einschließlich Schemata, Datensätzen, Profilen usw.) unterhält. Darüber hinaus verfügen Produktions- und Entwicklungs-Sandboxes über eine Funktion zum Zurücksetzen, mit der sich alle kundenseitig erstellten Ressourcen aus der Sandbox entfernen lassen. Entwicklungs-Sandboxes können nicht in Produktions-Sandboxes umgewandelt werden.

Mit einer Standardlizenz für Experience Platform erhalten Sie insgesamt fünf Sandboxes, die Sie jeweils als Produktion oder Entwicklung klassifizieren können. Sie können Zusatzpakete von jeweils zehn Sandboxes bis zu einem Maximum von insgesamt 75 Sandboxes hinzufügen. Diese zusätzlichen Sandboxes können zum Erstellen von Produktions- und Entwicklungs-Sandboxes verwendet werden. Wenden Sie sich an die Admins Ihrer Organisation oder das Adobe-Vertriebspersonal, um weitere Informationen zu erhalten.

Die standardmäßige Produktions-Sandbox ist letztendlich die erste Produktions-Sandbox, die bei der Ersterstellung einer Organisation erstellt wird. Mit der standardmäßigen Produktions-Sandbox können Sie Daten aus Platform aufnehmen oder nutzen sowie Anfragen akzeptieren, die keine Werte für einen Sandbox-Namen oder eine Sandbox-ID enthalten.

>[!NOTE]
>
>Direkt nach der Erstellung einer Sandbox enthält diese noch keine Daten. Da jede Sandbox einen eigenen isolierten Datenspeicher unterhält, müssen sie auch ihre Daten unabhängig erfassen.

Zusammenfassend kann man sagen, dass Sandboxes folgende Vorteile bieten:

* **Application Lifecycle Management**: Richten Sie separate virtuelle Umgebungen ein, um Programme für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.
* **Projekt- und Markenverwaltung**: Lassen Sie es zu, dass in derselben Organisation verschiedene Projekte parallel ausgeführt werden, während Isolation und Zugriffskontrolle sichergestellt werden. Zukünftige Versionen werden Unterstützung zur Bereitstellung in verschiedenen Regionen bieten.
* **Flexibles Entwicklungsökosystem**: Stellen Sie Sandboxes auf nahtlose, skalierbare und kostengünstige Weise für Erkundungs-, Unterstützungs- und Demonstrationszwecke bereit.

## Zugriffskontrolle für Sandboxes

Standardmäßig haben alle Benutzer einer Organisation Zugriff auf eine Produktions-Sandbox. Der Zugriff auf Nicht-Produktions-Sandboxes muss über die [Adobe Admin Console](https://adminconsole.adobe.com) von einem Systemadministrator, Produktadministrator oder Produktprofiladministrator gewährt werden.

Um Nicht-Produktions-Sandboxes anzuzeigen, zu erstellen, zu aktualisieren oder zu löschen, müssen Benutzer außerdem Sandbox-Administratorberechtigungen erhalten.

Weiterführende Informationen zum Verwalten von Rollen und Berechtigungen für Sandboxes finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Sandboxes in der Benutzeroberfläche von Experience Platform

In der [Benutzeroberfläche von Experience Platform](https://platform.adobe.com) können Benutzer mit dem Steuerelement **Sandbox-Umschalter** oben links auf dem Bildschirm zwischen den Sandboxes wechseln, auf die sie Zugriff haben.  Benutzer mit Sandbox-Administratorberechtigungen haben außerdem Zugriff auf den Tab **[!UICONTROL Sandboxes]** im linken Navigationsbereich, wo sie Sandboxes für ihre Organisation anzeigen und verwalten können. Weiterführende Informationen zum Arbeiten mit Sandboxes in der Benutzeroberfläche finden Sie im [Sandbox-Benutzerhandbuch](ui/overview.md).

## Sandboxes in Experience Platform-APIs

Beim Aufrufen von Experience Platform-APIs muss unter der Kopfzeile `x-sandbox-name` ein Sandbox-Name angegeben werden. Wenn Sie beispielsweise die [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) aufrufen, um alle Datensätze in der Produktions-Sandbox anzuzeigen, wird der Name der Sandbox („prod“) in der API-Anfrage als Kopfzeile angegeben:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Wenn `x-sandbox-name` in einem API-Aufruf nicht enthalten ist, verwendet das System stattdessen eine Standard-Sandbox. Es empfiehlt sich jedoch, diese Kopfzeile stets in alle API-Aufrufe aufzunehmen (selbst wenn die Standard-Sandbox verwendet wird). Aus diesem Grund wird `x-sandbox-name` in der API-Dokumentation für Experience Platform als erforderliche Kopfzeile behandelt.

### Sandbox-API

Mit der Sandbox-API können Sie Sandboxes unter Verwendung von RESTful-API-Operationen verwalten. Genaue Informationen zur Verwendung der API, einschließlich ordnungsgemäß formatierter Anfragen und Beispielantworten, finden Sie im [Sandbox-Entwicklerhandbuch](api/overview.md).

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie sich mit den grundlegenden Konzepten von Sandboxes in Experience Platform vertraut gemacht. Ausführliche Anweisungen zum Verwalten von Sandboxes finden Sie im [Benutzerhandbuch](ui/overview.md) zur Benutzeroberfläche oder im [Entwicklerhandbuch](./api/getting-started.md) zur API.

Sandboxes dienen Ihrem Entwicklungs-Team als nützliches Tool zum Isolieren von Platform-Umgebungen; über die Adobe Admin Console Sie können aber auch eine granularere Zugriffskontrolle nutzen. Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).
