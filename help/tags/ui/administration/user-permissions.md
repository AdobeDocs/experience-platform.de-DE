---
title: Benutzerberechtigungen für Tags
description: Hier erfahren Sie mehr über die verschiedenen Arten von Berechtigungen, die für Tags verfügbar sind, und über einige grundlegende Implementierungsstrategien für verschiedene geschäftliche Anwendungsfälle.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 91%

---

# Benutzerberechtigungen für Tags

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Benutzerberechtigungen für Tags in Adobe Experience Platform werden Benutzern über Adobe Admin Console zugewiesen. Anstatt einzelnen Benutzern zugewiesen zu werden, werden unterschiedliche Berechtigungssätze separat als Produktprofile konfiguriert. Benutzer werden dann diesen Produktprofilen zugewiesen, um die Berechtigungen zu erhalten, für die sie konfiguriert wurden.

Dieses Handbuch bietet einen Überblick über die verschiedenen Arten von Berechtigungen, die für Tags verfügbar sind, die Funktionen, auf die sie Zugriff gewähren, und einige grundlegende Implementierungsstrategien für verschiedene geschäftliche Anwendungsfälle.

>[!NOTE]
>
>Anweisungen zum Konfigurieren von Berechtigungen für Benutzer mithilfe von Admin Console finden Sie im Tutorial zu [Verwalten von Berechtigungen für die Datenerfassung](../../../collection/permissions.md).

## Berechtigungstypen

Innerhalb eines Produktprofils sind die Berechtigungen für Tags in vier Kategorien unterteilt:

1. Plattformen
1. Eigenschaften
1. Eigenschaftsrechte
1. Unternehmensrechte

### Plattformen

Jede Tag-Eigenschaft verfügt über eine Plattform. Derzeit gibt es zwei Plattformen, die Sie für Tags verwenden können: Web und Mobile. Mit diesem Berechtigungstyp können Sie den Zugriff auf einen bestimmten Eigenschaftstyp einschränken oder gewähren. Dies kann nützlich sein, wenn sich das Team, das Ihre Mobile Apps verwaltet, von dem für die Verwaltung Ihrer Websites unterscheidet.

### Eigenschaften

Standardmäßig gewähren Produktprofile Zugriff auf alle Eigenschaften, die in Ihrem Unternehmen vorhanden sind, sowohl derzeit als auch in Zukunft. Mit diesem Berechtigungstyp können Sie den Zugriff auf bestimmte vorhandene Eigenschaften anhand des Namens einschränken oder gewähren.

### Eigenschaftsrechte {#property-rights}

Jede Tag-Eigenschaft, die Sie in der Benutzeroberfläche erstellen, steht in Admin Console zur Verfügung, sodass Sie die Eigenschaft mit bestimmten Eigenschaftsrechten im selben Produktprofil gruppieren können.

Wenn ein Produktprofil nicht auf Eigenschaft A1 zugreifen kann, können Benutzer, die zu diesem Profil gehören, keine Einstellungen innerhalb der Eigenschaft A1 anzeigen oder ändern.

Wenn ein Benutzer zu einem Profil gehört, das Zugriff auf Eigenschaft A1 hat, werden die Aktionen, die er in Eigenschaft A1 ausführen kann, durch die Rechte bestimmt, die ihm von diesem Profil gewährt wurden. Wenn ein Benutzer über Berechtigungen für Eigenschaft A1 verfügt, aber keine Rechte zugewiesen sind, hat er schreibgeschützten Zugriff für diese Eigenschaft.

In der folgenden Tabelle sind die verfügbaren Eigenschaftsrechte und die Funktionen aufgeführt, auf die sie Zugriff gewähren:

| Eigenschaftsrecht | Beschreibung |
| --- | --- |
| **Entwickeln** | Hiermit können Sie die folgenden Aktionen durchführen:<ul><li>Erstellen von Regeln und Datenelementen</li><li>Erstellen von Bibliotheken und Einbauen von Bibliotheken in bestehende Entwicklungsumgebungen </li><li>Eine Bibliothek zur Genehmigung einreichen</li></ul>Die meisten täglichen Aufgaben in der Benutzeroberfläche erfordern dieses Recht. |
| **Genehmigen** | Dies ermöglicht es Ihnen, eingereichte Bibliotheken in die Staging-Umgebung einzubauen. Sie können eine Bibliothek auch für die Veröffentlichung genehmigen, nachdem die nötigen Tests abgeschlossen wurden. |
| **Veröffentlichen** | Dies ermöglicht Ihnen die Veröffentlichung genehmigter Bibliotheken in der Produktionsumgebung. |
| **Erweiterungen verwalten** | Hiermit können Sie die folgenden Aktionen durchführen: <ul><li>Installieren neuer Erweiterungen für eine Eigenschaft</li><li>Ändern der Konfiguration für eine bereits installierte Erweiterung</li><li>Löschen einer Erweiterung</li></ul>In der Übersichtsdokumentation zu Erweiterungen finden Sie [weitere Informationen zu Erweiterungen](../managing-resources/extensions/overview.md). Diese Rolle gehört normalerweise zu IT oder Marketing, je nach Aufbau Ihrer Organisation. |
| **Umgebungen verwalten** | Hiermit können Sie Umgebungen erstellen und ändern. Konsultieren Sie die [Dokumentation zu Umgebungen](../publishing/environments.md) für weitere Informationen. Diese Rolle gehört normalerweise zur IT-Gruppe. |

{style="table-layout:auto"}

### Unternehmensrechte

Unternehmensrechte gelten für Berechtigungen, die mehrere Eigenschaften umfassen. Diese sind in der folgenden Tabelle aufgeführt:

| Unternehmensrecht | Beschreibung |
| --- | --- |
| **Eigenschaften verwalten** | Hiermit können Sie die folgenden Aktionen durchführen:<ul><li>Erstellen neuer Eigenschaften</li><li>Ändern von Metadaten und Einstellungen auf Eigenschaftsebene</li><li>Löschen von Eigenschaften</li></ul>In der Regel führen Administratoren diese Rolle aus. Weitere Informationen finden Sie in der [Dokumentation zu Eigenschaften](companies-and-properties.md). |
| **Entwickeln von Erweiterungen** | Ermöglicht die Erstellung und Änderung von Erweiterungspaketen, die dem Unternehmen gehören, einschließlich privater Versionen und Anfragen zur Veröffentlichung. |
| **Mobile-App-Konfigurationen verwalten** | Dies ist nur verfügbar, wenn Sie über eine Lizenz für Adobe Journey Optimizer oder eine andere Lösung verfügen, die Zugriff auf mobile In-App- und Push-Nachrichten gewährt.  Damit können Sie die Mobile Apps verwalten, die Experience Cloud bekannt sind, zusammen mit den notwendigen Push-Zugangsdaten, die für die Kommunikation mit dem Firebase Cloud Messaging-Service und dem Apple Push Notification Service benötigt werden. |

{style="table-layout:auto"}

## Gesamt-Benutzerberechtigungen

Die Gesamtberechtigungen eines einzelnen Benutzers werden durch seine Zugehörigkeit zu den verschiedenen Produktprofilen bestimmt. Wenn ein Benutzer mehreren Produktprofilen angehört, werden die Berechtigungen der einzelnen Profile zusammengerechnet und nicht multipliziert.

Beispiel: Produktprofil A gewährt Ihnen das Entwicklungsrecht für Eigenschaft 1. Produktprofil B gewährt Ihnen das Veröffentlichungsrecht für Eigenschaft 2. In dem Fall können Sie in Eigenschaft 1 entwickeln und in Eigenschaft 2 veröffentlichen, jedoch nicht in Eigenschaft 1 veröffentlichen oder in Eigenschaft 2 entwickeln, da Ihnen hierzu keine expliziten Rechte erteilt wurden.

## Rechteszenarien

Unternehmen haben beim Erstellen neuer Produktprofile unterschiedliche Anforderungen. Diese Anforderungen variieren je nach Unternehmensgröße, Organisationsstruktur, Anzahl der Sites, Anzahl der Personen, die an der Verwaltung von Tags beteiligt sind usw.

Im Folgenden finden Sie einige gängige Szenarien sowie den jeweiligen empfohlenen Ausgangspunkt zum Erstellen von Produktprofilen und Hinzufügen von Benutzern.

### One-Man-Show

Wenn Sie ein kleines Unternehmen leiten, in dem eine Person für alles verantwortlich ist, gewähren Sie dieser Person die Berechtigung für alle Eigenschaften und weisen Sie ihr alle oben aufgeführten Rechte zu.

### Aufgabentrennung

Stellen Sie sich jetzt eine Situation vor, in der viele Personen in Ihrer Organisation am Tagging beteiligt sind. Bei Ihnen erstellen mehrere Personen (etwa externe Berater) Regeln und Datenelemente. Sie wollen jedoch nicht, dass diese alle Zugriff auf die Produktionsumgebung erhalten. In diesem Fall möchten Sie sicherstellen, dass nur das IT-Team etwas für die Produktion bereitstellen kann.

Gehen Sie dazu folgendermaßen vor:

1. Erstellen Sie ein Konto für Ihre Berater und weisen Sie ihnen nur das Entwicklungsrecht zu.
1. So erstellen und testen Berater innerhalb der von Ihnen festgelegten Grenzen.
1. Wenn der Berater eine neue Erweiterung braucht oder für die Veröffentlichung bereit ist, führt ein Vertreter Ihrer Organisation (mit den entsprechenden Rechten) diese Aktionen durch.

### Großunternehmen

Großunternehmen betreiben häufig mehrere Sites geografisch verteilt, wobei verschiedene Teams für die jeweilige Region verantwortlich sind. Innerhalb dieser Teams entwickeln und veröffentlichen verschiedene Personen.

Dies ähnelt „Aufgabentrennung“, ist jedoch nach geografischen Bereichen organisiert. Sie können beispielsweise ein Profil „Entwickeln“ und ein Profil „Veröffentlichen“ für Nordamerika erstellen und separate Gruppen „Entwickeln“ und „Veröffentlichen“ für Europa erstellen.

## Beispielrollen

In der folgenden Tabelle finden Sie einige Beispiele für die Rollentypen, die Sie in Ihrem Unternehmen möglicherweise verwenden, und die Berechtigungen, die Sie ihnen zuweisen sollten:

| Rolle | Beschreibung | Eigenschaften | Eigenschaftsrechte | Unternehmensrechte |
| --- | --- | --- | --- | --- |
| Manager | Möchte sehen, was im System passiert, sollte jedoch keine Änderungen vornehmen können. | Automatisch einfügen | (Keine) | (Keine) |
| Vermarkter | Kann Erweiterungen installieren und neue Tags für vorhandene Eigenschaften einrichten, aber kann nicht in Staging- oder Produktionsumgebungen veröffentlichen. | Automatisch einfügen | <ul><li>Entwickeln</li><li>Erweiterungen verwalten</li></ul> | <ul><li>Eigenschaften verwalten</li></ul> |
| App-Entwickler | Ist für die Implementierung von Adobe- und Drittanbieterlösungen in nativen Mobile Apps verantwortlich. | Automatisch einfügen | <ul><li>Entwickeln</li><li>Erweiterungen verwalten</li></ul> | <li>Eigenschaften verwalten</li><li>Mobile-App-Konfigurationen verwalten</li> |
| IT-Team | Ändert zwar keine Tags, hat jedoch volle Kontrolle über die Staging- und die Produktionsumgebung und deren Inhalte. | Automatisch einfügen | (Keine) | <ul><li>Genehmigen</li><li>Veröffentlichen Sie</li><li>Umgebungen verwalten</li></ul> |
| Erweiterungsentwickler | Entwickelt Erweiterungen und kann sie zur Genehmigung einreichen, kann sie jedoch nicht veröffentlichen oder zu vorhandenen Eigenschaften hinzufügen. | Automatisch einfügen | <ul><li>Entwickeln</li></ul> | <ul><li>Eigenschaften verwalten</li><li>Entwickeln von Erweiterungen</li></ul> |
| Der Super-Anwender | Macht alles. | Automatisch einfügen | <ul><li>Entwickeln</li><li>Genehmigen</li><li>Veröffentlichen Sie</li><li>Erweiterungen verwalten</li><li>Umgebungen verwalten</li></ul> | <ul><li>Eigenschaften verwalten</li></ul> |

{style="table-layout:auto"}

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die verfügbaren Berechtigungen für Tags in Experience Platform. Anweisungen zum Konfigurieren von Produktprofilen für Tags in Adobe Admin Console finden Sie im Handbuch unter [Verwalten von Benutzerberechtigungen für die Datenerfassung](../../../collection/permissions.md).
