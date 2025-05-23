---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffskontrolle;attributbasierte Zugriffskontrolle;
title: Attributbasierte Zugriffssteuerung – Übersicht
description: Dieses Dokument enthält Informationen zur attributbasierten Zugriffssteuerung in Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 70%

---

# Attributbasierte Zugriffssteuerung – Übersicht {#attribute-based-access-control-overview}

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administrierende den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Verwenden Sie diese Funktion, um Schemafelder des Experience-Datenmodells (XDM) mit Bezeichnungen zu versehen, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Admins die Benutzeroberfläche zur Verwaltung von Benutzenden und Rollen verwenden, um Zugriffsrichtlinien zu definieren, die XDM-Schemafelder abdecken, und den Zugriff, der Benutzenden oder Gruppen von Benutzenden (internen, externen oder Dritten) gewährt wird, besser verwalten. Darüber hinaus ermöglicht die attributbasierte Zugriffskontrolle Admins die Verwaltung des Zugriffs auf bestimmte Segmente.

>[!IMPORTANT]
>
>Die attributbasierte Zugriffssteuerung ist nicht zu verwechseln mit den Data Governance-Funktionen von Experience Platform, mit denen Sie mithilfe von Kennzeichnungen und Richtlinien steuern können, wie Daten in Experience Platform verwendet werden, und nicht damit, welche Benutzenden in Ihrem Unternehmen Zugriff darauf haben. Weitere Informationen finden Sie [ „Übersicht ](../../data-governance/home.md) Data Governance“.

Durch attributbasierte Zugriffssteuerung können Admins Ihres Unternehmens den Zugriff der Benutzenden auf sensible persönliche Daten (SPD), persönlich identifizierbare Informationen (PII) und benutzerdefinierte Datentypen in allen Workflows und Ressourcen von Experience Platform steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

Das folgende Video soll Ihnen dabei helfen, die attributbasierte Zugriffssteuerung zu verstehen, und beschreibt, wie Sie Rollen, Ressourcen und Richtlinien konfigurieren.

>[!VIDEO](https://video.tv.adobe.com/v/3451847?learn=on&captions=ger)

## Attributbasierte Zugriffssteuerung – Terminologie

Die attributbasierte Zugriffssteuerung umfasst die folgenden Komponenten:

| Terminologie | Definition |
| --- | --- |
| Attribute | Attribute sind die Bezeichner, die die Korrelation zwischen einem Benutzer und den Experience Platform-Ressourcen angeben, auf die er Zugriff hat. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten. |
| Beschriftungen | Mit Beschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in Experience Platform oder ab dem Zeitpunkt ihrer Nutzbarkeit in Experience Platform mit einer Beschriftung zu versehen. |
| Berechtigungen | Zu den Berechtigungen gehört die Möglichkeit, Experience Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen. |
| Berechtigungssätze | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Admin auf eine Rolle anwenden kann. Ein Admin kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| Richtlinien | Richtlinien sind Anweisungen, die Attribute zusammenbringen, um zulässige und unzulässige Aktionen festzustellen. Richtlinien können lokal oder global sein und andere Richtlinien überschreiben. |
| Ressource | Eine Ressource ist das Asset oder Objekt, auf das ein Subjekt zugreifen kann oder nicht. Ressourcen können Segmente oder Schemafelder sein. |
| Rollen | Rollen sind Möglichkeiten, die Typen von Benutzenden zu kategorisieren, die mit Ihrer Experience Platform-Instanz interagieren, und sind Bausteine von Richtlinien zur Zugriffssteuerung. In einer rollenbasierten Zugriffssteuerungsumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen, wobei Mitglieder Ihrer Organisation je nach dem Umfang des Lese- oder Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden können. |
| Betreff | Ein Subjekt ist der Benutzer, der Zugriff auf eine Ressource anfordert, um eine Aktion durchzuführen. |
| Benutzergruppen | Benutzergruppen sind mehrere Benutzer, die gruppiert wurden und Zugriff haben, um dieselben Funktionen auszuführen. |

## Berechtigungen

>[!IMPORTANT]
>
>Sobald für Ihr Unternehmen die attributbasierte Zugriffssteuerung aktiviert wurde, können Sie mit der Verwendung von Berechtigungen für Adobe Experience Cloud anstelle von Rollen in der Adobe Admin Console beginnen, um Berechtigungen für Benutzende, Funktionen, Beschriftungen und andere Ressourcen in Ihrem Unternehmen zu verwalten.

Berechtigungen sind der Bereich von Experience Cloud, in dem Admins Benutzerrollen und Zugriffsrichtlinien definieren können, um Zugriffsberechtigungen für Funktionen und Objekte in einem Produktprogramm zu verwalten.

Über Berechtigungen können Sie Rollen erstellen und verwalten sowie die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen. Mit Berechtigungen können Sie auch die Bezeichnungen, Sandboxes und Benutzende verwalten, die einer bestimmten Rolle zugeordnet sind. Weitere Informationen finden Sie im [Handbuch zu Berechtigungen](ui/browse.md).

## Attributbasierte Zugriffssteuerung – API

Mit der attributbasierten Zugriffssteuerungs-API können Sie Rollen, Richtlinien und Produkte innerhalb von Experience Platform mithilfe von APIs programmgesteuert verwalten. Weitere Informationen finden Sie im Handbuch zum [Verwenden der API zum Verwalten attributbasierter Zugriffssteuerungskonfigurationen](api/overview.md).

## Attributbasierte Zugriffssteuerung in Adobe Experience Platform

Die folgenden Abschnitte enthalten Informationen dazu, wie die attributbasierte Zugriffssteuerung in andere Komponenten von Experience Platform integriert wird:

### Zugangssteuerung

Experience Platform nutzt [Adobe Admin Console](https://adminconsole.adobe.com)-Rollen, um Benutzende mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf eine Vielzahl von Experience Platform-Funktionen, einschließlich Datenmodellierung, Profilverwaltung und Sandbox-Administration. Sobald für Ihr Unternehmen die attributbasierte Zugriffssteuerung aktiviert wurde, können Sie mit der Verwendung von Berechtigungen für Adobe Experience Cloud anstelle von Rollen in der Adobe Admin Console beginnen, um Berechtigungen für Benutzende, Funktionen, Beschriftungen und andere Ressourcen in Ihrem Unternehmen zu verwalten.

Es gibt nur eine begrenzte Verfügbarkeit der attributbasierten Zugriffssteuerung für Kunden, die Healthcare und/oder Privacy Shields erwerben. Zu den Features dieser Funktion gehören:

* Benutzeroberfläche „Berechtigungen“: Bietet eine Oberfläche für Sie, um Benutzerrollen, Berechtigungen und Richtlinien für die attributbasierte Zugriffssteuerung festzulegen.

* Beschriftungen: Fügen Sie Benutzerrollen, Schemafeldern, Segmenten und anderen unterstützten Objekten Beschriftungen hinzu, um Zugriffssteuerungsrichtlinien zu nutzen oder bearbeiten oder entfernen Sie diese. **Hinweis:** Jedes Segment, das ein gekennzeichnetes Attribut verwendet, muss ebenfalls gekennzeichnet werden, wenn dieselben Zugriffsbeschränkungen für es gelten sollen.

Die Verwaltungs-Workflows für alle Experience Platform-gestützten Anwendungen, von der Admin Console bis zur neuen Benutzeroberfläche „Berechtigungen“, werden derzeit umgestellt.

>[!IMPORTANT]
>
>Ihre Rollen werden automatisch in die Benutzeroberfläche „Berechtigungen“ migriert, wenn Ihre Organisation aktiviert ist. Die Rollen in Admin Console bleiben bis auf Weiteres unverändert. Bitte **nicht** ändern Sie Ihre Rollen, nachdem dies für Ihre Organisation aktiviert wurde.

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../home.md).

### Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

Als Admin können Sie attributbasierte Zugriffssteuerungsfunktionen für Folgendes verwenden:

* Konfigurieren Sie den Benutzerzugriff, um basierend auf Rollen, Berechtigungen und Beschriftungen bestimmte Segmente im Aktivierungsprozess anzuzeigen.
   * Während des Aktivierungsprozesses müssen Benutzende möglicherweise Segmente auswählen, die sie für ein Ziel aktivieren möchten. Als Admin können Sie für Benutzende in Ihrer Organisation festlegen, dass sie nur Segmente anzeigen können, die mit Beschriftungen versehen sind, auf die Benutzende Zugriff haben, sowie Segmente, die keine Beschriftungen enthalten.
* Konfigurieren Sie den Benutzerzugriff so, dass basierend auf Rollen, Berechtigungen und Beschriftungen bestimmte Felder im Aktivierungsprozess angezeigt werden können.
   * Während des Aktivierungsprozesses müssen Benutzende möglicherweise Felder auswählen, die sie für ein Ziel aktivieren möchten. Als Admin können Sie für Benutzende in Ihrer Organisation festlegen, dass sie nur Felder anzeigen können, die mit Beschriftungen versehen sind, auf die Benutzende Zugriff haben, sowie Felder, die keine Beschriftungen enthalten.

>[!IMPORTANT]
>
>Beachten Sie daher bei der Arbeit mit Zielen und attributbasierter Zugriffssteuerung die folgenden Auswirkungen:
>
>* Sie können nur Zielgruppen aktivieren, für die Sie über die Berechtigung zum Zugriff und zur Anzeige im [Zielgruppenportal](/help/segmentation/ui/audience-portal.md#browse) und [Segmentschritt auswählen](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) des Aktivierungs-Workflows verfügen.
>* Im [Zuordnungsschritt des Aktivierungs-Workflows](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) können Sie nur die Felder anzeigen und zur Aktivierung auswählen, für die Sie über Zugriffsberechtigungen verfügen.
>* Wenn Sie zusätzliche Segmente für ein vorhandenes Ziel aktivieren möchten, bei dem Sie nicht auf alle Felder zugreifen können, die für den Export zugeordnet sind, wird der Aktivierungs-Workflow für Sie blockiert.

Weitere Informationen zu [!DNL Destinations] finden Sie in der [[!DNL Destinations] Übersicht](../../destinations/home.md).

### Identity Service

Mit dem [!DNL Identity Service] von Adobe Experience Platform erhalten Sie einen besseren Überblick über Ihre Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend zusammenführen und so wirkungsvolle, persönliche digitale Erlebnisse in Echtzeit bereitstellen können.

Im Rahmen der attributbasierten Zugriffssteuerung können Sie mit der Berechtigung `view-identity-graph` festlegen, welche Benutzenden in Ihrer Organisation über die Benutzeroberfläche oder APIs auf das Identitätsdiagramm zugreifen können. Weitere Informationen finden Sie im Handbuch zum [Verwenden des Identitätsdiagramm-Viewers](../../identity-service/features/identity-graph-viewer.md).

Weitere Informationen zu [!DNL Identity Service] finden Sie in der [[!DNL Identity Service] Übersicht](../../identity-service/home.md).

### Echtzeit-Kundenprofil

Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Sicht zusammenführen, die eine aussagekräftige, im Zeitverlauf gezeichnete Darstellung jeder Kundeninteraktion bietet.

Als Admin können Sie attributbasierte Zugriffssteuerungsfunktionen für Folgendes verwenden:

* Konfigurieren Sie den Benutzerzugriff auf bestimmte Profilattribute basierend auf Rollen, Berechtigungen und Beschriftungen.
   * Als Admin können Sie für Benutzende in Ihrer Organisation festlegen, dass sie nur Profilattribute anzeigen können, die mit Beschriftungen versehen sind, auf die Benutzende Zugriff haben, sowie Profilattribute, die keine Beschriftungen enthalten.
   * Als Admin können Sie für Benutzende in Ihrer Organisation festlegen, dass sie beim Erstellen von Segmenten nur Profilattribute anzeigen können, die mit Beschriftungen versehen sind, auf die Benutzende Zugriff haben.
* Konfigurieren Sie den Benutzerzugriff auf die Datenvorschau, indem Sie bestimmte Datenfelder beschriften, die im XDM-Schema des Datenmodells verwendet werden.

Weiterführende Informationen zum Profil finden Sie in der [Profilübersicht](../../profile/home.md).

### Segmentierungs-Service

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

Als Admin können Sie attributbasierte Zugriffssteuerungsfunktionen für Folgendes verwenden:

* Konfigurieren Sie den Benutzerzugriff, um bestimmte Segmente basierend auf Rollen, Berechtigungen und Beschriftungen anzuzeigen und zu verwalten.
   * Als Admin können Sie für Benutzende in Ihrer Organisation festlegen, dass sie bei der Verwendung der Segmentierungsbenutzeroberfläche nur Segmente anzeigen können, die mit Beschriftungen versehen sind, auf die Benutzende Zugriff haben, sowie Segmente, die keine Beschriftungen enthalten.

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [[!DNL Segmentation Service] Übersicht](../../segmentation/home.md).

### XDM

Das Experience-Datenmodell (XDM) ist eine Open-Source-Spezifikation, die dazu dient, die Leistung digitaler Erlebnisse zu verbessern. Es bietet allgemeine Strukturen und Definitionen für Anwendungen, die mit Services auf Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

Mit der attributbasierten Zugriffssteuerung können Sie Folgendes durchführen:

* [Wenden Sie Datennutzungskennzeichnungen auf Feldergruppen und -klassen an](../../xdm/tutorials/labels.md). Dadurch wird es ermöglicht, dass mehrere Schemata mit denselben Feldergruppen oder -klassen Felder aufweisen können, die mit denselben Attributen versehen sind, je nach den Konfigurationen auf Feldergruppen- oder Klassenebene.
* Konfigurieren Sie den Benutzerzugriff auf bestimmte XDM-Schemafelder abhängig von den Berechtigungssätzen, die auf die Rollen der Benutzenden angewendet werden.

Weitere Informationen zu XDM finden Sie in der [XDM-Übersicht](../../xdm/home.md).