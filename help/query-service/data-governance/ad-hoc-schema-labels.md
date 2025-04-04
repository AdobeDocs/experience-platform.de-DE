---
title: Unterstützung der attributbasierten Zugriffssteuerung für Ad-hoc-Schemata
description: Eine Anleitung zum Beschränken des Zugriffs auf Datenfelder in Ad-hoc-Schemata, die über den Abfrage-Service von Adobe Experience Platform generiert wurden.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 7%

---

# Unterstützung der attributbasierten Zugriffskontrolle für ungeplante Schemata

Alle Daten, die in Adobe Experience Platform importiert werden, sind in Experience-Datenmodell (XDM)-Schemata gekapselt und können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Vorschriften definiert werden.

Durch das Ausführen einer CTAS-Abfrage über den Abfrage-Service, wenn kein Schema angegeben ist, wird automatisch ein Ad-hoc-Schema generiert. Häufig ist es erforderlich, die Verwendung bestimmter Felder oder Datensätze von Ad-hoc-Schemata einzuschränken, um den Zugriff auf sensible personenbezogene Daten und persönlich identifizierbare Informationen zu steuern. Adobe Experience Platform erleichtert diese Zugriffssteuerung, indem Sie Schemafelder über die Experience Platform-Benutzeroberfläche mithilfe der attributbasierten Zugriffssteuerungsfunktion beschriften können.

Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Es empfiehlt sich jedoch, Daten direkt bei ihrer Aufnahme in Experience Platform oder ab dem Zeitpunkt ihrer Nutzbarkeit in Experience Platform mit einer Beschriftung zu versehen.

Die schemabasierte Beschriftung ist eine wichtige Komponente der attributbasierten Zugriffssteuerung, um den Zugriff für Benutzende oder Benutzergruppen besser zu verwalten. Mit Adobe Experience Platform können Sie den Zugriff auf Felder eines Ad-hoc-Schemas einschränken, indem Sie Kennzeichnungen erstellen und anwenden.

Dieses Dokument enthält ein Tutorial zum Verwalten des Zugriffs auf vertrauliche Daten durch Anwenden von Kennzeichnungen auf Datenfelder von Ad-hoc-Schemas, die über den Abfrage-Service generiert wurden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [[!DNL Schema Editor]](../../xdm/ui/overview.md): Erfahren Sie, wie Sie Schemas und andere Ressourcen in der Experience Platform-Benutzeroberfläche erstellen und verwalten.
* [[!DNL Data Governance]](../../data-governance/home.md): Erfahren Sie, wie Sie mit [!DNL Data Governance] Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von relevanten Vorschriften, Einschränkungen und Richtlinien sicherstellen können.
* [Attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md): Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Admins den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Beschriftung, die einem Ad-hoc- oder regulären Schemafeld hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

## Erstellen eines Ad-hoc-Schemas

Nachdem Ihre Abfrage ausgeführt und Ergebnisse generiert wurden, wird automatisch ein Ad-hoc-Schema generiert und zum Schema-Inventar hinzugefügt.

Um eine Datenbeschriftung hinzuzufügen, navigieren Sie zur Registerkarte [!UICONTROL Schemata] Dashboard durchsuchen , indem Sie [!UICONTROL Schemata] in der linken Leiste der Experience Platform-Benutzeroberfläche auswählen. Das Schema-Inventar wird angezeigt.

>[!NOTE]
>
>Ad-hoc-Schemata werden standardmäßig nicht im Schema-Inventar angezeigt.

## Erkunden von Ad-hoc-Schemata im Schemabestand der Experience Platform-Benutzeroberfläche {#discover-ad-hoc-schemas}

Um die Anzeige von Ad-hoc-Schemata in der Experience Platform-Benutzeroberfläche zu aktivieren, wählen Sie das Filtersymbol (![.](/help/images/icons/filter.png)) links neben dem Suchfeld aus und wählen Sie dann in der ] Leiste, die angezeigt wird, die Option **[!UICONTROL Ad-hoc-Schemata anzeigen aus.

![Die Filteroptionen für das Schema-Dashboard in der linken Leiste mit aktiviertem Umschalter „Ad-hoc-Schema anzeigen“](../images/data-governance/adhoc-schema-toggle.png)

Wählen Sie den Namen des kürzlich erstellten Ad-hoc-Schemas aus der verfügbaren Liste aus. Eine Visualisierung der Ad-hoc-Schemastruktur wird angezeigt.

![Das Beispiel-Strukturdiagramm eines Ad-hoc-Schemas.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Governance-Kennzeichnungen bearbeiten

Um Datenbeschriftungen für Ihr Ad-hoc-Schema zu bearbeiten, wählen Sie die Registerkarte [!UICONTROL Beschriftungen] aus. Der Arbeitsbereich Kennzeichnungen ermöglicht es Ihnen, Kennzeichnungen auf Ihre Ad-hoc-Schemafelder anzuwenden, zu erstellen und zu bearbeiten und Zugriffsberechtigungen über die Benutzeroberfläche zu steuern. Alle Felder innerhalb des Ad-hoc-Schemas werden hier dargestellt.

## Bearbeiten von Kennzeichnungen für das Schema oder Feld

Um die Beschriftungen für das gesamte Schema zu bearbeiten, klicken Sie auf das Stiftsymbol (![Stiftsymbol).](/help/images/icons/edit.png)) neben dem Namen des Schemas auf der Registerkarte [!UICONTROL Kennzeichnungen] an.

![Die Beschriftungsansicht im Arbeitsbereich „Schemata“ mit hervorgehobenem Stiftsymbol.](../images/data-governance/edit-entire-schema-labels.png)

Um eine Kennzeichnung auf ein vorhandenes Feld anzuwenden, wählen Sie ein oder mehrere Felder aus der Liste aus und [!UICONTROL  Sie in ] rechten Seitenleiste „Governance-Kennzeichnungen bearbeiten“.

![Die Ansicht „Kennzeichnungen“ im Arbeitsbereich „Schemata“ mit hervorgehobener Option „Governance-Kennzeichnungen bearbeiten“ in der rechten Seitenleiste.](../images/data-governance/edit-governance-labels.png)

## Popover „Kennzeichnungen bearbeiten“

Das [!UICONTROL Beschriftungen bearbeiten] wird angezeigt. In dieser Ansicht können Sie vorhandene Governance-Kennzeichnungen über die Benutzeroberfläche erstellen oder bearbeiten.

![Das Popover „Beschriftungen bearbeiten“.](../images/data-governance/edit-labels-popover.png)

In der Dokumentation finden Sie Anleitungen zum [ (Erstellen oder Bearbeiten von Kennzeichnungen für das ausgewählte Schema oder Feld](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>Das Erstellen einer neuen Kennzeichnung oder das Bearbeiten einer vorhandenen Kennzeichnung erfordert Administratorberechtigungen für Ihre Organisation. Wenn Sie keine Administratorrechte haben, wenden Sie sich an Ihren Systemadministrator, um den Zugriff zu arrangieren.

Kennzeichnungen können auch mit dem Arbeitsbereich Berechtigungen erstellt werden. Anweisungen finden Sie [Handbuch zum Erstellen von Beschriftungen im ](../../access-control/abac/ui/labels.md) .

Sobald die entsprechende Ebene der attributbasierten Zugriffssteuerung angewendet wurde, gilt das folgende Systemverhalten für jede Abfrage, die über den Abfrage-Service ausgeführt wird, wenn ein Benutzer versucht, auf nicht zugängliche Daten zuzugreifen:

1. Wenn einem Benutzer der Zugriff auf eines der Felder innerhalb eines Schemas verweigert wird, kann der Benutzer das eingeschränkte Feld nicht lesen oder schreiben. Dies gilt für die folgenden gängigen Szenarien:

   * Wenn ein(e) Benutzende(r) versucht, eine Abfrage mit nur einer eingeschränkten Spalte auszuführen, gibt das System den Fehler aus, dass die Spalte nicht vorhanden ist.
   * Wenn ein(e) Benutzende(r) versucht, eine Abfrage mit mehreren Spalten auszuführen, die eine eingeschränkte Spalte enthalten, gibt das System nur die Ausgabe für alle nicht eingeschränkten Spalten zurück.

1. Wenn ein(e) Benutzende(r) Zugriff auf ein berechnetes Feld anfordert, muss er/sie Zugriff auf alle in der Komposition verwendeten Felder haben, oder das System verweigert den Zugriff auf das berechnete Feld.

Wenn eine Identität oder primäre Identität für ein Ad-hoc-Schema festgelegt ist, berücksichtigt das System automatisch alle zugehörigen Datenhygiene-Anfragen und bereinigt die Daten in diesen Datensätzen, die mit der Identitätsspalte verknüpft sind.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie besser, wie Sie Datennutzungsbeschriftungen zu Ad-hoc-Schemas hinzufügen, die durch Abfragen des Abfrage-Service-CTAS erstellt wurden. Wenn Sie dies noch nicht getan haben, sind die folgenden Dokumente nützlich, um Ihr Verständnis von Data Governance in Query Service zu verbessern:

* [Ad-hoc-Schemaidentitäten](./ad-hoc-schema-identities.md)
* [Data Governance](../../data-governance/home.md)
