---
keywords: Experience Platform;Home;beliebte Themen;Zugriffskontrolle;adobe Admin Console
solution: Experience Platform
topic-legacy: overview
title: Zugriffskontrolle – Übersicht
description: Die Zugriffskontrolle für Adobe Experience Platform erfolgt über die Adobe Admin Console. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 53%

---

# Zugriffskontrolle – Übersicht

Die Zugriffskontrolle für [!DNL Experience Platform] wird über [Adobe Admin Console](https://adminconsole.adobe.com) bereitgestellt. Diese Funktion nutzt die Profil von Produkten in [!DNL Admin Console], die Benutzer mit Berechtigungen und Sandboxen verknüpfen.

## Zugriffskontrolle auf Hierarchie und Workflow

Um die Zugriffskontrolle für [!DNL Experience Platform] zu konfigurieren, müssen Sie über Administratorrechte für ein Unternehmen verfügen, das über eine [!DNL Experience Platform]-Produktintegration verfügt. Die Mindestrolle, die Berechtigungen erteilt oder entzieht, ist ein Produktprofil-Administrator. Andere Administratorrollen, die Berechtigungen verwalten können, sind Produktadministratoren (kann alle Profile innerhalb eines Produkts verwalten) und Systemadministratoren (keine Einschränkungen). Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

>[!NOTE]
>
>Ab diesem Zeitpunkt beziehen sich alle Erwähnungen von „Administrator“ in diesem Dokument auf einen Produktadministrator oder höher (wie oben beschrieben).

Ein Workflow auf hoher Ebene zum Abrufen und Zuweisen von Zugriffsberechtigungen kann wie folgt zusammengefasst werden:

- Nach der Lizenzierung von Adobe Experience Platform oder einem Anwendungs-/App-Dienst, der Experience Platform verwendet, wird eine E-Mail an den Administrator gesendet, der während der Lizenzierung angegeben wurde.
- Der Administrator meldet sich bei der [Adobe Admin Console](#adobe-admin-console) an und wählt **Adobe Experience Platform** aus der Liste der Produkte auf der Übersichtsseite aus.
- Der Administrator kann die standardmäßigen [Produktprofile](#product-profiles) anzeigen oder bei Bedarf neue Kundenproduktprofile erstellen.
- Der Administrator kann die Berechtigungen und Benutzer für alle vorhandenen Profile bearbeiten.
- Beim Erstellen oder Bearbeiten eines Profils fügt der Administrator dem Profil Benutzer über die Registerkarte **[!UICONTROL users]** hinzu und erteilt diesen Benutzern Berechtigungen (z. B. &quot;[!UICONTROL Read DataSets]&quot;oder &quot;[!UICONTROL Schema verwalten]&quot;), indem er auf die Registerkarte **[!UICONTROL permissions]** zugreift. Ebenso kann der Administrator über die gleiche Registerkarte „ „Berechtigungen“ Zugriff auf Sandboxes zuweisen.
- Wenn sich Benutzer bei der [!DNL Experience Platform]-Benutzeroberfläche anmelden, wird ihr Zugriff auf [!DNL Platform]-Funktionen von den Berechtigungen gesteuert, die ihnen aus Schritt 2 erteilt wurden. Wenn ein Benutzer beispielsweise nicht über die Berechtigung &quot;[!UICONTROL Ansicht-Datensätze]&quot;verfügt, ist die Registerkarte **[!UICONTROL Datensätze]** im Seitenmenü für diesen Benutzer nicht sichtbar.

Detailliertere Anweisungen zum Verwalten der Zugriffskontrolle in [!DNL Experience Platform] finden Sie im [Zugriffskontrolle-Benutzerhandbuch](./ui/overview.md).

Alle Aufrufe von [!DNL Experience Platform]-APIs werden auf Berechtigungen überprüft und geben Fehler zurück, wenn die entsprechenden Berechtigungen im aktuellen Benutzerkontext nicht gefunden wurden. In der Benutzeroberfläche werden Elemente je nach den dem aktuellen Benutzer zugewiesenen Berechtigungen ausgeblendet oder geändert.

## Adobe Admin Console

Die Adobe Admin Console bietet einen zentralen Speicherort für die Verwaltung der Adobe-Produktberechtigungen und den Zugriff für Ihr Unternehmen. Über die Konsole können Sie Benutzergruppen Zugriffsberechtigungen für verschiedene Funktionen von [!DNL Platform] erteilen, z. B. &quot;[!UICONTROL Datenbestände verwalten]&quot;, &quot;[!UICONTROL Ansichten-Datensätze]&quot;oder &quot;[!UICONTROL Profil verwalten]&quot;.

### Produktprofile

In [!DNL Admin Console] werden Benutzern Berechtigungen durch die Verwendung von Produkt-Profilen zugewiesen. Mit den Produktprofilen können Sie einem oder mehreren Benutzern Berechtigungen erteilen und auch deren Zugriff auf den Umfang der Sandboxes einschließen, die ihnen über Produktprofile zugewiesen werden. Benutzer können einem oder mehreren Produktprofilen Ihres Unternehmens zugewiesen werden.

### Standard-Produktprofile

[!DNL Experience Platform] enthält zwei vorkonfigurierte Standard-Profil. Die folgende Tabelle zeigt, was in den einzelnen Standardprofilen bereitgestellt wird, einschließlich der Sandbox, auf die sie Zugriff gewähren, sowie der Berechtigungen, die sie im Rahmen dieser Sandbox gewähren.

| Produktprofile | Sandbox-Zugriff | Berechtigungen |
| --- | --- | --- |
| Standardproduktion mit Zugriff | Produktion | Alle Berechtigungen, die auf [!DNL Experience Platform] anwendbar sind, mit Ausnahme der Sandbox-Administratorberechtigungen. |
| Sandbox-Administratoren | K. A. | Bietet nur Zugriff auf Sandbox-Administratorberechtigungen. |

## Sandboxes und Berechtigungen

Nicht-Produktion-Sandboxes sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxes isolieren können und die üblicherweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Die Berechtigungen eines Profils geben den Benutzern des Profils Zugriff auf [!DNL Platform]-Funktionen innerhalb der Sandbox-Umgebung, auf die sie Zugriff haben. Mit einer Standardlizenz für Experience Platformen erhalten Sie fünf Sandboxen (eine Produktion und vier Nicht-Produktion). Sie können Pakete von zehn Nicht-Produktions-Sandboxen bis zu maximal 75 Sandboxen hinzufügen. Für weitere Informationen wenden Sie sich bitte an Ihren IMS-Organisationsadministrator oder Ihren Vertriebsmitarbeiter für Adoben.

Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Übersicht über Sandboxen](../sandboxes/home.md).

### Zugriff auf Sandboxes

Der Zugriff auf Sandboxes wird über Produktprofile verwaltet. Ausführliche Anweisungen zum Aktivieren des Zugriffs auf eine Sandbox für ein Produktprofil finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

Benutzern kann Zugriff auf eine oder mehrere Sandboxes innerhalb eines Profils gewährt werden. Wenn ein Benutzer in zwei oder mehr Produktprofilen enthalten ist, hat er Zugriff auf alle in diesen Profilen enthaltenen Sandboxes.

Die Berechtigung „Sandbox-Verwaltung“ ermöglicht Benutzern das Verwalten, Anzeigen oder Zurücksetzen von Sandboxes.

### Berechtigungen

Auf der Registerkarte Berechtigungen in einem Produktprofil werden die Sandboxes und Berechtigungen angezeigt, die für dieses Profil aktiv sind:

![permissions-overview](./images/permissions-overview.png)

Berechtigungen, die über das [!DNL Admin Console] erteilt werden, werden nach Kategorie sortiert, wobei einige Berechtigungen Zugriff auf mehrere Funktionen auf niedriger Ebene gewähren.

In der folgenden Tabelle sind die verfügbaren Berechtigungen für [!DNL Experience Platform] in [!DNL Admin Console] mit Beschreibungen der spezifischen [!DNL Platform]-Funktionen, auf die sie Zugriff gewähren, aufgeführt. Detaillierte Anweisungen zum Hinzufügen von Berechtigungen zu einem Produktprofil finden Sie im [Benutzerhandbuch für die Zugriffskontrolle](./ui/overview.md).

| Kategorie | Berechtigung | Beschreibung |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Verwalten von Schemas] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schemas und zugehörigen Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL Anzeigen von Schemas] | Schreibgeschützter Zugriff auf Schemas und zugehörige Ressourcen. |
| [!DNL Data Modeling] | [!UICONTROL Beziehungen verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Schema-Beziehungen. |
| [!DNL Data Modeling] | [!UICONTROL Identitätsmetadaten verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitätsmetadaten für Schema. |
| [!DNL Data Management] | [!UICONTROL Datensätze verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen. Schreibgeschützter Zugriff auf Schemas. |
| [!DNL Data Management] | [!UICONTROL Anzeigen von Datensätzen] | Schreibgeschützter Zugriff auf Datensätze und Schemas. |
| [!DNL Data Management] | [!UICONTROL Datenüberwachung] | Schreibgeschützter Zugriff auf das Monitoring von Datensätzen und Streams. |
| [!DNL Profile Management] | [!UICONTROL Verwalten von Profilen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datensätzen, die für Kundenprofile verwendet werden. Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Anzeigen von Profilen] | Schreibgeschützter Zugriff auf verfügbare Profile. |
| [!DNL Profile Management] | [!UICONTROL Segmente verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Segmenten. |
| [!DNL Profile Management] | [!UICONTROL Ansichten-Segmente] | Schreibgeschützter Zugriff auf verfügbare Segmente. |
| [!DNL Profile Management] | [!UICONTROL Richtlinien zusammenführen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Zusammenführungsrichtlinien. |
| [!DNL Profile Management] | [!UICONTROL Richtlinien zum Zusammenführen von Ansichten] | Schreibgeschützter Zugriff auf verfügbare Zusammenführungsrichtlinien. |
| [!DNL Profile Management] | [!UICONTROL Exportieren der Zielgruppe für das Segment] | Fähigkeit, eine ausgewertetes Zielgruppensegment in einen Datensatz zu exportieren. |
| [!DNL Profile Management] | [!UICONTROL Segmentauswertung für eine Audience] | Möglichkeit, Profil für eine Audience zu generieren, indem eine Segmentdefinition ausgewertet wird. |
| [!DNL Identities] | [!UICONTROL Verwalten von Identitäts-Namensräumen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Identitäts-Namensräumen. |
| [!DNL Identities] | [!UICONTROL Anzeigen von Identitäts-Namensräumen] | Schreibgeschützter Zugriff für Identitäts-Namensräume. |
| [!DNL Sandbox Administration] | [!UICONTROL Verwalten von Sandboxes] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen von Sandboxes. |
| [!DNL Sandbox Administration] | [!UICONTROL Anzeigen von Sandboxes] | Schreibgeschützter Zugriff für Sandboxes Ihrer Organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Zurücksetzen einer Sandbox] | Fähigkeit, eine Sandbox zurückzusetzen. |
| [!DNL Destinations] | [!UICONTROL Verwalten von Zielen] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen. |
| [!DNL Destinations] | [!UICONTROL Anzeigen von Zielen] | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Ziele auf der Registerkarte **[!UICONTROL Durchsuchen.]** |
| [!DNL Destinations] | [!UICONTROL Aktivieren von Zielen] | Fähigkeit zur Aktivierung von Daten an aktiven Zielen, die erstellt wurden. Für diese Berechtigung ist es erforderlich, dass dem Benutzer, der Ziele aktivieren soll, entweder &quot;Ansichten-Ziele&quot;oder &quot;Ziele verwalten [!UICONTROL &quot;erteilt wird.] |
| [!DNL Data Ingestion] | [!UICONTROL Verwalten von Quellen] | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| [!DNL Data Ingestion] | [!UICONTROL Anzeigen von Quellen] | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Durchsuchen]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Verwalten des Data Science Workspace] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen in [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Bezeichnungen für die Datenverwendung anwenden] | Zugriff zum Lesen, Erstellen und Löschen von Beschriftungen für die Verwendung. |
| [!DNL Data Governance] | [!UICONTROL Richtlinien zur Datenverwendung verwalten] | Zugriff zum Lesen, Erstellen, Bearbeiten und Löschen von Datenverwendungsrichtlinien. |
| [!DNL Data Governance] | [!UICONTROL Richtlinien zur Ansicht von Daten] | Schreibgeschützter Zugriff für Datenverwendungsrichtlinien Ihres Unternehmens. |
| [!DNL Query Service] | [!UICONTROL Abfragen verwalten] | Zugriff auf das Lesen, Erstellen, Bearbeiten und Löschen strukturierter SQL-Abfragen für Plattformdaten. |

## Nächste Schritte

Durch Lesen dieses Handbuchs wurden Sie den Hauptgrundsätzen der Zugriffskontrolle in [!DNL Experience Platform] hinzugefügt. Sie können nun im [Zugriffskontrolle-Benutzerhandbuch](./ui/overview.md) detaillierte Anweisungen zur Verwendung von [!DNL Admin Console] zum Erstellen von Profilen und Zuweisen von Berechtigungen für [!DNL Platform] finden.
