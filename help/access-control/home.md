---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Zugriffskontrolle
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 3%

---


# Übersicht über die Zugriffskontrolle

Zugriffskontrolle für Experience Platform wird über die [Adobe Admin-Konsole](https://adminconsole.adobe.com)bereitgestellt. Diese Funktion nutzt die Profil der Produkte in der Admin-Konsole, die Benutzer mit Berechtigungen und Sandboxen verknüpfen.

## Hierarchie und Arbeitsablauf der Zugriffskontrolle

Zum Konfigurieren der Zugriffskontrolle für Experience Platform müssen Sie über Administratorrechte für ein Unternehmen verfügen, das über eine Experience Platform-Produktintegration verfügt. Die Mindestrolle, die Berechtigungen erteilt oder entzieht, ist ein **Produktadministrator**. Andere Administratorrollen, die Berechtigungen verwalten können, sind **Produktadministratoren** (alle Profil innerhalb eines Produkts verwalten können) und **Systemadministratoren** (keine Einschränkungen). Weitere Informationen zu [Verwaltungsrollen](https://helpx.adobe.com/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE] Ab diesem Zeitpunkt beziehen sich alle Erwähnungen von &quot;administrator&quot;in diesem Dokument auf einen Produktadministrator oder höher (wie oben beschrieben).

Ein Arbeitsablauf auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach dem Abonnement für Adobe Experience Platform wird eine E-Mail an den Administrator gesendet, der im Registrierungsformular angegeben ist.
- Der Administrator meldet sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählt **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite.
- Der Administrator kann die standardmäßigen [Profil](#product-profiles) des Produkts Ansicht vornehmen oder bei Bedarf neue Profil für das Kundenprodukt erstellen.
- Der Administrator kann die Berechtigungen und Benutzer für alle vorhandenen Profil bearbeiten.
- Beim Erstellen oder Bearbeiten eines Profils fügt der Administrator dem Profil über die Registerkarte &quot; **** &quot;Benutzer hinzu und gewährt diesen Benutzern (z. B. &quot;Datensätze lesen&quot;oder &quot;Schema verwalten&quot;) Berechtigungen, indem sie auf die Registerkarte &quot; **Berechtigungen** &quot;zugreifen. Ebenso kann der Administrator über die gleiche Registerkarte &quot;Berechtigungen&quot;Zugriff auf Sandboxen zuweisen.
- Wenn sich Benutzer bei der Benutzeroberfläche von Experience Platform anmelden, wird ihr Zugriff auf Plattformfunktionen durch die Berechtigungen gesteuert, die ihnen in Schritt 2 erteilt wurden. Wenn ein Benutzer beispielsweise nicht über die Berechtigung &quot;Ansicht-Datasets&quot;verfügt, ist die Registerkarte &quot; *Datenblätter* &quot;im Seitenmenü für diesen Benutzer nicht sichtbar.

Detailliertere Anweisungen zum Verwalten der Zugriffskontrolle in Experience Platform finden Sie im [Zugriffskontrolle-Benutzerhandbuch](./ui/overview.md).

Alle Aufrufe von Experience Platform-APIs werden auf Berechtigungen überprüft und geben Fehler zurück, wenn die entsprechenden Berechtigungen im aktuellen Benutzerkontext nicht gefunden wurden. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Adobe Admin Console

Die Adobe Admin-Konsole bietet einen zentralen Speicherort für die Verwaltung der Adobe-Produktberechtigungen und den Zugriff für Ihr Unternehmen. Über die Konsole können Sie Benutzergruppen Zugriffsberechtigungen für verschiedene Plattformfunktionen erteilen, z. B. &quot;Ansichten verwalten&quot;, &quot;Datasets&quot;oder &quot;Profil verwalten&quot;.

### Produktprofile

In der Admin-Konsole werden Benutzern Berechtigungen über die Verwendung von **Produkt-Profilen** zugewiesen. Mit den Profilen des Produkts können Sie einem oder mehreren Benutzern Berechtigungen erteilen und auch deren Zugriff auf den Umfang der Sandboxen einschließen, die ihnen über Produkt-Profil zugewiesen werden. Benutzer können einem oder mehreren Profilen Ihres Unternehmens zugewiesen werden.

### Standardprodukt-Profil

Experience Platform verfügt über zwei vorkonfigurierte Standard-Profil. Die folgende Tabelle zeigt, was in den einzelnen Standardeinstellungen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Produkt-Profil | Sandbox-Zugriff | Zugriffsberechtigung |
| --- | --- | --- |
| Standardproduktion - Zugriff auf alle | Produktion | Alle für Experience Platform geltenden Berechtigungen mit Ausnahme der Sandbox-Administratorberechtigungen. |
| Standard-Sandbox-Administration | K. A. | Bietet nur Zugriff auf Sandbox-Administratorberechtigungen. |

## Sandboxen und Berechtigungen

Experience Platform bietet Zugriff auf eine Produktions-Sandbox und ermöglicht Ihnen das Erstellen von Nicht-Produktion- **Sandboxen**. Nicht-Produktion-Sandboxen sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxen isolieren können und die üblicherweise für Entwicklungsversuche, Tests oder Tests verwendet werden. Die **Berechtigungen** eines Profils geben den Benutzern des Profils Zugriff auf Plattformfunktionen innerhalb der Sandbox-Umgebung, auf die sie Zugriff haben.

Weitere Informationen zu Sandboxen in Experience Platform finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

### Zugriff auf Sandboxen

Der Zugriff auf Sandboxen wird über Produkt-Profil verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für ein Profil finden Sie im Benutzerhandbuch für die [Zugriffskontrolle](./ui/overview.md).

Benutzer können Zugriff auf eine oder mehrere Sandboxen innerhalb eines Profils erhalten. Wenn ein Benutzer in zwei oder mehr Profilen enthalten ist, hat er Zugriff auf alle in diesen Profilen enthaltenen Sandboxen.

Die Berechtigung &quot;Sandbox-Verwaltung&quot;ermöglicht Benutzern das Verwalten, Ansichten oder Zurücksetzen von Sandboxen.

### Zugriffsberechtigung

Auf der Registerkarte &quot; **Berechtigungen** &quot;in einem Profil werden die Sandboxen und Berechtigungen angezeigt, die für dieses Profil aktiv sind:

![](./images/permissions-overview.png)

Berechtigungen, die über die Admin-Konsole erteilt werden, werden nach Kategorie sortiert. Einige Berechtigungen gewähren Zugriff auf verschiedene Funktionen auf niedriger Ebene.

In der folgenden Tabelle sind die für Experience Platform in der Admin-Konsole verfügbaren Berechtigungen mit Beschreibungen der spezifischen Plattformfunktionen, auf die sie Zugriff gewähren, aufgeführt. Detaillierte Anweisungen zum Hinzufügen von Berechtigungen zu einem Profil finden Sie im Benutzerhandbuch zur [Zugriffskontrolle](./ui/overview.md).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| Datenmodellierung | Schemas verwalten | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schemas und zugehörigen Ressourcen. |
| Datenmodellierung | Ansicht Schema | Schreibgeschützter Zugriff auf Schema und zugehörige Ressourcen. |
| Data Management | Datenbestände verwalten | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen. Schreibgeschützter Zugriff für Schema. |
| Data Management | Ansichten-Datensätze | Schreibgeschützter Zugriff für Datensätze und Schema. |
| Data Management | Datenüberwachung | Schreibgeschützter Zugriff auf Überwachungsdatensätze und -ströme. |
| Profil-Management | Verwalten von Profilen | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen, die für Kundendaten verwendet werden. Schreibgeschützter Zugriff auf verfügbare Profil. |
| Profil-Management | Ansicht Profil | Schreibgeschützter Zugriff auf verfügbare Profil. |
| Profil-Management | Audience für Segment exportieren | Möglichkeit zum Exportieren eines ausgewerteten Segments für Audiencen in einen Datensatz. |
| Identitäten | Identitäts-Namensraum verwalten | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitäts-Namensräumen. |
| Identitäten | Ansicht Identitäts-Namensraum | Schreibgeschützter Zugriff für Identitäts-Namensraum. |
| Sandbox-Administration | Sandboxen verwalten | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Sandboxen. |
| Sandbox-Administration | Ansicht-Sandboxen | Schreibgeschützter Zugriff für Sandboxen Ihrer Organisation. |
| Sandbox-Administration | Sandbox zurücksetzen | Möglichkeit zum Zurücksetzen einer Sandbox. |
| Ziele | Ziele verwalten | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen.* |
| Ziele | Ansichten-Ziele | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte &quot; *Katalog* &quot;und authentifizierte Ziele auf der Registerkarte &quot; *Durchsuchen* &quot;.* |
| Ziele | Ziele aktivieren | Möglichkeit zur Aktivierung von Daten an aktiven Zielen, die erstellt wurden. Für diese Berechtigung ist es erforderlich, dass dem Benutzer, der Ziele aktivieren soll, entweder &quot;Zielorte der Ansicht&quot;oder &quot;Ziele verwalten&quot;erteilt wird.* |
| Dateneinbindung | Quellen verwalten | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| Dateneinbindung | Ansichten-Quellen | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte &quot; *Katalog* &quot;und authentifizierte Quellen auf der Registerkarte &quot; *Durchsuchen* &quot;. |
| Data Science-Arbeitsbereich | Data Science Workspace | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen im Data Science Workspace. |

_(*) Diese Berechtigung erfordert Bestimmungen für die Echtzeit-Kundendatenplattform. Für weitere Informationen zu Echtzeit-CDP lesen Sie bitte zunächst die[Echtzeit-CDP-Übersicht](https://docs.adobe.com/content/help/de-DE/experience-platform/rtcdp/overview.html)._

## Nächste Schritte

Durch Lesen dieses Handbuchs wurden Sie den Hauptgrundsätzen der Zugriffskontrolle in Experience Platform vorgestellt. Im Benutzerhandbuch [für die](./ui/overview.md) Zugriffskontrolle erfahren Sie ausführlich, wie Sie mit der Admin-Konsole Produktberechtigungen erstellen und Plattformberechtigungen zuweisen können.