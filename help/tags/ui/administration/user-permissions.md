---
title: Benutzerberechtigungen für Tags
description: Erfahren Sie mehr über die verschiedenen Arten von Berechtigungen, die für Tags verfügbar sind, und über einige grundlegende Implementierungsstrategien für verschiedene geschäftliche Anwendungsfälle.
source-git-commit: acef25fe46f0ac0c45c18d4590be4af95ad5e0ab
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 24%

---

# Benutzerberechtigungen für Tags

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Benutzerberechtigungen für Tags in Adobe Experience Platform werden Benutzern über Adobe Admin Console zugewiesen. Anstatt einzelnen Benutzern zugewiesen zu werden, werden unterschiedliche Berechtigungssätze separat als Produktprofile konfiguriert. Benutzer werden dann diesen Produktprofilen zugewiesen, um die Berechtigungen zu erhalten, für die sie konfiguriert wurden.

Dieses Handbuch bietet einen Überblick über die verschiedenen Arten von Berechtigungen, die für Tags verfügbar sind, die Funktionen, auf die sie Zugriff gewähren, und einige grundlegende Implementierungsstrategien für verschiedene geschäftliche Anwendungsfälle.

>[!NOTE]
>
>Anweisungen zum Konfigurieren von Berechtigungen für Benutzer, die Admin Console verwenden, finden Sie im Tutorial zum Verwalten von Berechtigungen für Tags](./manage-permissions.md).[

## Berechtigungstypen

In einem Produktprofil sind die Berechtigungen für Tags in vier Kategorien unterteilt:

1. Plattformen
1. Eigenschaften
1. Eigenschaftsrechte
1. Unternehmensrechte

### Plattformen

Jede Tag-Eigenschaft verfügt über eine Plattform. Derzeit gibt es zwei Plattformen, die Sie für Tags verwenden können: Web und Mobile. Mit diesem Berechtigungstyp können Sie den Zugriff auf einen bestimmten Eigenschaftstyp einschränken oder gewähren. Dies kann nützlich sein, wenn sich das Team, das Ihre mobilen Apps verwaltet, von dem unterscheidet, das Ihre Websites verwaltet.

### Eigenschaften

Standardmäßig gewähren Produktprofile Zugriff auf alle Eigenschaften, die in Ihrem Unternehmen vorhanden sind, sowohl derzeit als auch in Zukunft. Mit diesem Berechtigungstyp können Sie den Zugriff auf bestimmte vorhandene Eigenschaften anhand des Namens einschränken oder gewähren.

### Eigenschaftsrechte

Jede Eigenschaft, die Sie in der Datenerfassungs-Benutzeroberfläche erstellen, steht in Admin Console zur Verfügung, sodass Sie die Eigenschaft mit bestimmten Eigenschaftsrechten im selben Produktprofil gruppieren können.

Wenn beispielsweise ein bestimmtes Produktprofil keinen Zugriff auf Property A1 hat, können Benutzer, die zu diesem Profil gehören, keine Einstellungen in Property A1 anzeigen oder ändern.

Wenn ein Benutzer zu einem Profil gehört, das Zugriff auf Property A1 hat, werden die Aktionen, die er in Property A1 ausführen kann, durch die Rechte bestimmt, die ihm von diesem Profil gewährt wurden. Wenn ein Benutzer über Berechtigungen für Eigenschaft A1 verfügt, aber keine Rechte zugewiesen sind, hat er schreibgeschützten Zugriff für diese Eigenschaft.

In der folgenden Tabelle sind die verfügbaren Eigenschaftsrechte und die Funktionen aufgeführt, auf die sie Zugriff gewähren:

| Eigenschaftsrecht | Beschreibung |
| --- | --- |
| **Entwickeln** | Auf diese Weise können Sie die folgenden Aktionen durchführen:<ul><li>Erstellen von Regeln und Datenelementen</li><li>Erstellen Sie Bibliotheken und erstellen Sie sie in bestehenden Entwicklungsumgebungen</li><li>Bibliothek zur Genehmigung übermitteln</li></ul>Die meisten alltäglichen Aufgaben in der Datenerfassungs-Benutzeroberfläche erfordern diese Berechtigung. |
| **Genehmigen** | Dadurch können Sie eine gesendete Bibliothek in die Staging-Umgebung erstellen. Sie können eine Bibliothek auch für die Veröffentlichung genehmigen, nachdem die nötigen Tests abgeschlossen wurden. |
| **Veröffentlichen** | Dadurch können Sie genehmigte Bibliotheken in der Produktionsumgebung veröffentlichen. |
| **Erweiterungen verwalten** | Auf diese Weise können Sie die folgenden Aktionen durchführen: <ul><li>Installieren neuer Erweiterungen für eine Eigenschaft</li><li>Ändern der Konfiguration für eine bereits installierte Erweiterung</li><li>Löschen einer Erweiterung</li></ul>In der Übersichtsdokumentation zu Erweiterungen finden Sie [weitere Informationen zu Erweiterungen](../managing-resources/extensions/overview.md). Diese Rolle gehört normalerweise zu IT oder Marketing, je nach Aufbau Ihrer Organisation. |
| **Umgebungen verwalten** | Auf diese Weise können Sie Umgebungen erstellen und ändern. Konsultieren Sie die [Dokumentation zu Umgebungen](../publishing/environments.md) für weitere Informationen. Diese Rolle gehört normalerweise zur IT-Gruppe. |

{style=&quot;table-layout:auto&quot;}

### Unternehmensrechte

Unternehmensrechte gelten für Berechtigungen, die mehrere Eigenschaften umfassen. Diese sind in der folgenden Tabelle aufgeführt:

| Unternehmensrecht | Beschreibung |
| --- | --- |
| **Eigenschaften verwalten** | Auf diese Weise können Sie die folgenden Aktionen durchführen:<ul><li>Erstellen neuer Eigenschaften</li><li>Ändern von Metadaten und Einstellungen auf Eigenschaftsebene</li><li>Eigenschaften löschen</li></ul>In der Regel führen Administratoren diese Rolle aus. Weitere Informationen finden Sie in der [Eigenschaftendokumentation](companies-and-properties.md) . |
| **Entwickeln von Erweiterungen** | Ermöglicht das Erstellen und Ändern von Erweiterungspaketen, die dem Unternehmen gehören, einschließlich privater Versionen und Anfragen zur Veröffentlichung. |
| **Mobile-App-Konfigurationen verwalten** | Dies ist nur verfügbar, wenn Sie über eine Lizenz für Adobe Journey Optimizer oder eine andere Lösung verfügen, die Zugriff auf mobile In-App- und Push-Nachrichten gewährt.  Damit können Sie die Mobile Apps verwalten, die Experience Cloud bekannt sind, zusammen mit den notwendigen Push-Zugangsdaten, die für die Kommunikation mit dem Firebase Cloud Messaging-Service und dem Apple Push Notification Service benötigt werden. |

{style=&quot;table-layout:auto&quot;}

## Gesamt-Benutzerberechtigungen

Die Gesamtberechtigungen eines einzelnen Benutzers werden durch die Gesamtmitgliedschaft eines Benutzers in verschiedenen Produktprofilen bestimmt. Wenn ein Benutzer mehreren Produktprofilen angehört, werden die Berechtigungen der einzelnen Profile zusammen hinzugefügt anstatt multipliziert.

Beispielsweise gewährt Ihnen das Produktprofil A das Entwicklungsrecht für Property 1. Produktprofil B gewährt Ihnen das Veröffentlichungsrecht für Property 2. In diesem Fall können Sie in Property 1 entwickeln und in Property 2 veröffentlichen. Sie können jedoch nicht in Property 1 veröffentlichen oder in Property 2 entwickeln, da Ihnen hierfür keine expliziten Rechte erteilt wurden.

## Rechteszenarien

Verschiedene Unternehmen haben unterschiedliche Anforderungen bei der Erstellung neuer Produktprofile. Diese Anforderungen variieren je nach Unternehmensgröße, Organisationsstruktur, Anzahl der Sites, Anzahl der Personen, die an der Verwaltung von Tags beteiligt sind usw.

Im Folgenden finden Sie einige gängige Szenarien und einen empfohlenen Ausgangspunkt für die Erstellung von Produktprofilen und das Hinzufügen von Benutzern zu diesen Profilen.

### One-Man-Show

Wenn Sie ein kleines Unternehmen betreiben, für das eine Person für alles verantwortlich ist, gewähren Sie diesem Benutzer Berechtigungen für alle Eigenschaften und weisen Sie ihm alle oben aufgeführten Rechte zu.

### Aufgabentrennung

Stellen Sie sich eine Situation vor, in der viele Personen in Ihrer Organisation am Tagging beteiligt sind. Sie verfügen über eine Gruppe von Personen (z. B. einen externen Berater), die Regeln und Datenelemente erstellen, aber nicht möchten, dass sie Zugriff auf die Produktionsumgebung haben. In diesem Fall möchten Sie sicherstellen, dass außer dem IT-Team niemand für die Produktion bereitgestellt wird.

Gehen Sie dazu folgendermaßen vor:

1. Erstellen Sie ein Konto für Ihre Berater und gewähren Sie ihnen nur das Recht Entwickeln .
1. So erstellen und testen Berater innerhalb der von Ihnen festgelegten Grenzen.
1. Wenn der Berater eine neue Erweiterung wünscht oder bereit ist, live zu gehen, führt ein Mitarbeiter Ihrer Organisation (mit den entsprechenden Rechten) diese Aktionen durch.

### Großunternehmen

Großunternehmen betreiben häufig mehrere Sites geografisch verteilt, wobei verschiedene Teams für die jeweilige Region verantwortlich sind. Innerhalb dieser Teams entwickeln und veröffentlichen verschiedene Personen.

Dies ähnelt „Aufgabentrennung“, ist jedoch nach geografischen Bereichen organisiert. Sie können beispielsweise ein Profil &quot;Entwickeln&quot;und ein Profil &quot;Veröffentlichen&quot;für Nordamerika erstellen und separate Gruppen &quot;Entwickeln&quot;und &quot;Veröffentlichen&quot;für Europa erstellen.

## Beispielrollen

In der folgenden Tabelle finden Sie einige Beispiele für die Rollen, die Sie in Ihrem Unternehmen möglicherweise verwenden und die Sie ihnen zuweisen sollten:

| Rolle | Beschreibung | Eigenschaften | Eigenschaftsrechte | Unternehmensrechte |
| --- | --- | --- | --- | --- |
| Manager | Möchte sehen, was im System passiert, sollte jedoch keine Änderungen vornehmen können. | Automatisch einfügen | (Keine) | (Keine) |
| Vermarkter | Kann Erweiterungen installieren und neue Tags für vorhandene Eigenschaften einrichten, aber nicht in der Staging- oder Produktionsumgebung veröffentlichen. | Automatisch einfügen | <ul><li>Entwickeln</li><li>Erweiterungen verwalten</li></ul> | <ul><li>Eigenschaften verwalten</li></ul> |
| App-Entwickler | ist für die Implementierung von Adobe- und Drittanbieterlösungen in einer nativen mobilen App verantwortlich. | Automatisch einfügen | <ul><li>Entwickeln</li><li>Erweiterungen verwalten</li></ul> | <li>Eigenschaften verwalten</li><li>Mobile-App-Konfigurationen verwalten</li> |
| IT-Team | Ändert keine Tags, aber sie haben die volle Kontrolle über die Staging- und Produktionsumgebungen und deren Inhalt. | Automatisch einfügen | (Keine) | <ul><li>Genehmigen</li><li>Veröffentlichen Sie</li><li>Umgebungen verwalten</li></ul> |
| Erweiterungsentwickler | Entwickelt Erweiterungen und kann zur Genehmigung gesendet werden, sie können jedoch nicht veröffentlichen oder zu vorhandenen Eigenschaften hinzufügen. | Automatisch einfügen | <ul><li>Entwickeln</li></ul> | <ul><li>Eigenschaften verwalten</li><li>Entwickeln von Erweiterungen</li></ul> |
| Der Superuser | Macht alles. | Automatisch einfügen | <ul><li>Entwickeln</li><li>Genehmigen</li><li>Veröffentlichen Sie</li><li>Erweiterungen verwalten</li><li>Umgebungen verwalten</li></ul> | <ul><li>Eigenschaften verwalten</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die verfügbaren Berechtigungen für Tags in Experience Platform. Anweisungen zum Konfigurieren von Produktprofilen für Tags in Adobe Admin Console finden Sie im Handbuch [Verwalten von Benutzerberechtigungen](./manage-permissions.md).
