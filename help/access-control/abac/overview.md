---
keywords: Experience Platform; Startseite; beliebte Themen; Zugriffskontrolle; attributbasierte Zugriffskontrolle;
title: Attributbasierte Zugriffssteuerung - Übersicht
description: Dieses Dokument enthält Informationen zur attributbasierten Zugriffskontrolle in Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 32%

---

# Attributbasierte Zugriffskontrolle - Übersicht

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, mit der Administrierende den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen steuern können. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten.

Mit dieser Funktion können Sie Experience-Datenmodell (XDM)-Schemafelder mit Bezeichnungen beschriften, die Organisations- oder Datennutzungsbereiche definieren. Parallel dazu können Administratoren die Benutzeroberfläche zur Verwaltung von Benutzern und Rollen verwenden, um Zugriffsrichtlinien für XDM-Schemafelder zu definieren und den Zugriff, der Benutzern oder Benutzergruppen (internen, externen oder Drittanbieterbenutzern) gewährt wird, besser zu verwalten. Darüber hinaus ermöglicht die attributbasierte Zugriffskontrolle Administrierenden die Verwaltung des Zugriffs auf bestimmte Segmente.

Mithilfe der attributbasierten Zugriffskontrolle können Administratoren Ihres Unternehmens den Zugriff der Benutzer auf sensible personenbezogene Daten (EPPD), personenbezogene Daten (PII) und benutzerdefinierte Datentypen für alle Platform-Workflows und -Ressourcen steuern. Administrierende können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

## Terminologie der attributbasierten Zugriffskontrolle

Die attributbasierte Zugriffskontrolle umfasst die folgenden Komponenten:

| Terminologie | Definition |
| --- | --- |
| Attribute | Attribute sind die Bezeichner, die die Korrelation zwischen einem Benutzer und den Platform-Ressourcen angeben, auf die er Zugriff hat. Attribute können Metadaten sein, die einem Objekt hinzugefügt werden, z. B. eine Bezeichnung, die einem Schemafeld oder Segment hinzugefügt wird. Administrierende definieren Zugriffsrichtlinien, die Attribute zur Verwaltung von Benutzerzugriffsberechtigungen enthalten. |
| Beschriftungen | Mit Beschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in Platform oder ab dem Zeitpunkt ihrer Nutzbarkeit in Platform mit einer Beschriftung zu versehen. |
| Berechtigungen | Zu den Berechtigungen gehört die Möglichkeit, Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen. |
| Berechtigungssätze | Berechtigungssätze stellen eine Gruppe von Berechtigungen dar, die ein Administrator auf eine Rolle anwenden kann. Ein Administrator kann einer Rolle Berechtigungssätze zuweisen, anstatt einzelne Berechtigungen zuzuweisen. Auf diese Weise können Sie benutzerdefinierte Rollen aus einer vordefinierten Rolle erstellen, die eine Gruppe von Berechtigungen enthält. |
| Richtlinien | Richtlinien sind Aussagen, die Attribute zusammenbringen, um zulässige und unzulässige Handlungen festzustellen. Richtlinien können lokal oder global sein und andere Richtlinien überschreiben. |
| Ressource | Eine Ressource ist das Asset oder Objekt, auf das ein Betreff zugreifen kann oder nicht. Ressourcen können Segmente oder Schemafelder sein. |
| Rollen | Rollen sind Möglichkeiten, die Typen von Benutzern zu kategorisieren, die mit Ihrer Platform-Instanz interagieren und Bausteine von Richtlinien zur Zugriffssteuerung sind. In einer rollenbasierten Zugriffskontrollumgebung erfolgt die Bereitstellung des Benutzerzugriffs über gemeinsame Zuständigkeiten und Anforderungen. Eine Rolle verfügt über bestimmte Berechtigungen und Mitglieder Ihrer Organisation können je nach dem Umfang der Ansicht oder des Schreibzugriffs, den sie benötigen, einer oder mehreren Rollen zugewiesen werden. |
| Betreff | Ein Betreff ist der Benutzer, der Zugriff auf eine Ressource anfordert, um eine Aktion durchzuführen. |
| Benutzergruppen | Benutzergruppen sind mehrere Benutzer, die gruppiert wurden und Zugriff haben, um dieselben Funktionen auszuführen. |

## Berechtigungen

>[!IMPORTANT]
>
>Sobald Ihre Organisation für eine attributbasierte Zugriffskontrolle aktiviert wurde, können Sie mit der Verwendung von Berechtigungen für Adobe Experience Cloud anstelle von Produktprofilen in der Adobe Admin Console beginnen, um Berechtigungen für Benutzer, Funktionen, Beschriftungen und andere Ressourcen in Ihrer Organisation zu verwalten.

Berechtigungen sind der Bereich von Experience Cloud, in dem Administrierende Benutzerrollen und Zugriffsrichtlinien definieren können, um Zugriffsberechtigungen für Funktionen und Objekte in einem Produktprogramm zu verwalten.

Über Berechtigungen können Sie Rollen erstellen und verwalten sowie die gewünschten Ressourcenberechtigungen für diese Rollen zuweisen. Mit Berechtigungen können Sie auch die Bezeichnungen, Sandboxes und Benutzer*innen verwalten, die einer bestimmten Rolle zugeordnet sind. Weitere Informationen finden Sie unter [Berechtigungshandbuch](ui/browse.md).

## Attributbasierte Zugriffssteuerungs-API

Mit der attributbasierten Zugriffssteuerungs-API können Sie Rollen, Richtlinien und Produkte in Platform mithilfe von APIs programmgesteuert verwalten. Weitere Informationen finden Sie im Handbuch unter [Verwenden der API zum Verwalten attributbasierter Zugriffssteuerungskonfigurationen](api/overview.md).

## Attributbasierte Zugriffssteuerung in Adobe Experience Platform

Die folgenden Abschnitte enthalten Informationen dazu, wie die attributbasierte Zugriffskontrolle in andere Komponenten von Platform integriert wird:

### Zugangssteuerung

 Platform nutzt [Adobe Admin Console](https://adminconsole.adobe.com)-Produktprofile, um Benutzer mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf verschiedene Platform-Funktionen, einschließlich Datenmodellierung, Profil-Management und Sandbox-Verwaltung. Sobald Ihre Organisation für eine attributbasierte Zugriffskontrolle aktiviert wurde, können Sie mit der Verwendung von Berechtigungen für Adobe Experience Cloud anstelle von Produktprofilen in der Adobe Admin Console beginnen, um Berechtigungen für Benutzer, Funktionen, Beschriftungen und andere Ressourcen in Ihrer Organisation zu verwalten.

Weitere Informationen zur Zugriffskontrolle finden Sie unter [Zugriffskontrolle - Übersicht](../home.md).

### Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

Als Administrator können Sie attributbasierte Zugriffssteuerungsfunktionen verwenden, um:

* Konfigurieren Sie den Benutzerzugriff, um bestimmte Segmente im Aktivierungsprozess basierend auf Rollen, Berechtigungen und Beschriftungen anzuzeigen.
   * Während des Aktivierungsprozesses müssen Benutzer möglicherweise Segmente auswählen, die sie für ein Ziel aktivieren möchten. Als Administrator können Sie Benutzern in Ihrer Organisation ermöglichen, nur Segmente anzuzeigen, die mit Bezeichnungen beschriftet sind, auf die Benutzer Zugriff haben, und Segmente, die keine Bezeichnungen enthalten.
* Konfigurieren Sie den Benutzerzugriff, um bestimmte Felder im Aktivierungsprozess basierend auf Rollen, Berechtigungen und Beschriftungen anzuzeigen.
   * Während des Aktivierungsprozesses müssen Benutzer möglicherweise Felder auswählen, die sie für ein Ziel aktivieren möchten. Als Administrator können Sie Benutzern in Ihrer Organisation ermöglichen, nur Felder anzuzeigen, die mit Beschriftungen versehen sind, auf die Benutzer Zugriff haben, und Felder, die keine Beschriftungen enthalten.

>[!IMPORTANT]
>
>Beachten Sie daher bei der Arbeit mit Zielen und attributbasierter Zugriffskontrolle die folgenden Auswirkungen:
>
>* Sie können nur Segmente aktivieren, für die Sie Zugriff und Zugriff auf die Seite im [Ansicht zum Durchsuchen von Segmenten](/help/segmentation/ui/overview.md#browse) und [Segmentschritt auswählen](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) des Aktivierungs-Workflows.
>* Im [Zuordnungsschritt des Aktivierungs-Workflows](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)können Sie nur die Felder anzeigen und zur Aktivierung auswählen, auf die Sie Zugriff haben.
>* Wenn Sie zusätzliche Segmente für ein vorhandenes Ziel aktivieren möchten, für das Sie keinen Zugriff auf alle Felder haben, die für den Export zugeordnet sind, wird der Aktivierungs-Workflow für Sie blockiert.


Weitere Informationen finden Sie unter [!DNL Destinations], siehe [[!DNL Destinations] Übersicht](../../destinations/home.md).

### Identity Service

Mit dem [!DNL Identity Service] von Adobe Experience Platform erhalten Sie einen besseren Überblick über Ihre Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend zusammenführen und so wirkungsvolle, persönliche digitale Erlebnisse in Echtzeit bereitstellen können.

Im Rahmen der attributbasierten Zugriffskontrolle muss die `view-identity-graph` -Berechtigung können Sie festlegen, welche Benutzer in Ihrer Organisation über die Benutzeroberfläche oder APIs auf das Identitätsdiagramm zugreifen können. Weitere Informationen finden Sie im Handbuch unter [Verwenden des Identitätsdiagramm-Viewers](../../identity-service/ui/identity-graph-viewer.md).

Weitere Informationen finden Sie unter [!DNL Identity Service], siehe [[!DNL Identity Service] Übersicht](../../identity-service/home.md).

### Echtzeit-Kundenprofil

Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Kunden, unabhängig davon, wo und wann diese mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert. Mit dem Profil können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Sicht zusammenführen, die eine aussagekräftige, im Zeitverlauf gezeichnete Darstellung jeder Kundeninteraktion bietet.

Als Administrator können Sie attributbasierte Zugriffssteuerungsfunktionen verwenden, um:

* Konfigurieren des Benutzerzugriffs auf bestimmte Profilattribute basierend auf Rollen, Berechtigungen und Bezeichnungen;
   * Als Administrator können Sie Benutzern in Ihrer Organisation ermöglichen, nur Profilattribute anzuzeigen, die mit Bezeichnungen beschriftet sind, auf die Benutzer Zugriff haben, sowie Profilattribute, die keine Bezeichnungen enthalten.
   * Als Administrator können Sie Benutzern in Ihrer Organisation ermöglichen, beim Erstellen von Segmenten nur Profilattribute anzuzeigen, die mit Bezeichnungen beschriftet sind, auf die Benutzer Zugriff haben.
* Konfigurieren Sie den Benutzerzugriff auf die Datenvorschau, indem Sie bestimmte Datenfelder beschriften, die im XDM-Schema des Datenmodells verwendet werden.

Weiterführende Informationen zum Profil finden Sie im Abschnitt [Profilübersicht](../../profile/home.md).

### Segmentierungs-Service

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

Als Administrator können Sie attributbasierte Zugriffssteuerungsfunktionen verwenden, um:

* Konfigurieren Sie den Benutzerzugriff, um bestimmte Segmente basierend auf Rollen, Berechtigungen und Beschriftungen anzuzeigen und zu verwalten.
   * Als Administrator können Sie Benutzern in Ihrer Organisation bei der Verwendung der Segmentierungsbenutzeroberfläche nur Segmente anzeigen, die mit Bezeichnungen beschriftet sind, auf die Benutzer Zugriff haben, und Segmente, die keine Bezeichnungen enthalten.

Weitere Informationen finden Sie unter [!DNL Segmentation Service], siehe [[!DNL Segmentation Service] Übersicht](../../segmentation/home.md).

### XDM

Das Experience-Datenmodell (XDM) ist eine Open-Source-Spezifikation, die dazu dient, die Leistung digitaler Erlebnisse zu verbessern. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

Mit der attributbasierten Zugriffskontrolle können Sie:

* [Anwenden von Datennutzungsbezeichnungen auf Feldergruppen und Klassen](../../xdm/tutorials/labels.md). Dies ermöglicht es mehreren Schemas mit denselben Feldergruppen oder -klassen, Felder mit denselben Attributen zu versehen, je nach den Konfigurationen auf Feldergruppen- oder Klassenebene.
* Konfigurieren Sie den Benutzerzugriff auf bestimmte XDM-Schemafelder abhängig von den auf Benutzerrollen angewendeten Berechtigungssätzen.

Weitere Informationen zu XDM finden Sie im Abschnitt [XDM-Übersicht](../../xdm/home.md).