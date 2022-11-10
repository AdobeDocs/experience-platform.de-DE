---
keywords: Experience Platform; Startseite; beliebte Themen; Sandbox-Fehlerbehebung
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Sandboxes
topic-legacy: troubleshooting guide
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Sandboxes in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 42%

---

# Handbuch zur Fehlerbehebung bei Sandboxes

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Sandboxes in Adobe Experience Platform. Fragen und Fehlerbehebungen für andere Platform-Dienste finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

Sandboxes unterteilen eine einzelne Platform-Instanz in separate virtuelle Umgebungen, damit sich Programme für digitale Erlebnisse entwickeln und weiterentwickeln lassen. Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](home.md).

## Was ist eine Sandbox?

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Sandbox unterhält eine eigene, unabhängige Bibliothek mit Platform-Ressourcen (einschließlich Schemas, Datensätzen, Profilen usw.). Alle Inhalte und Aktionen, die innerhalb einer Sandbox ausgeführt werden, sind auf diese Sandbox beschränkt und wirken sich nicht auf andere Sandboxes aus. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](home.md).

## Welche Arten von Sandboxes gibt es und wie unterscheiden sie sich? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Sandbox-Typ"
>abstract="Der Sandbox-Typ gibt an, ob es sich um eine Produktions- oder Entwicklungs-Sandbox handelt. Produktions-Sandboxes umfassen Live-Daten und Entwicklungs-Sandboxes, die zum Testen und Entwickeln verwendet werden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="Sandbox in der Benutzeroberfläche erstellen"

In Experience Platform gibt es zwei Arten von Sandboxes:

* **Produktions-Sandbox**: Eine Produktions-Sandbox ist für die Verwendung mit Profilen in Ihrer Produktionsumgebung vorgesehen. Platform ermöglicht es Ihnen, mehrere Produktions-Sandboxes zu erstellen, um die richtigen Funktionen für Daten bereitzustellen und gleichzeitig die betriebliche Isolierung beizubehalten. Mit dieser Funktion können Sie bestimmte Produktions-Sandboxes unterschiedlichen Geschäftsbereichen, Marken, Projekten oder Regionen zuweisen. Produktions-Sandboxes unterstützen eine Vielzahl von Produktionsprofilen bis hin zu Ihren lizenzierten [!DNL Profile] Verpflichtung (kumulativ über alle Ihre autorisierten Produktions-Sandboxes gemessen). Sie sind berechtigt, lizenziertes durchschnittliches Profil pro autorisiertem [!DNL Profile] (kumulativ über alle Ihre zulässigen Produktions-Sandboxes gemessen).
* **Entwicklungs-Sandbox**: Eine Entwicklungs-Sandbox ist eine Sandbox, die ausschließlich für Entwicklung und Tests mit Nicht-Produktionsprofilen verwendet werden kann. Entwicklungs-Sandboxes unterstützen eine Anzahl von Nicht-Produktions-Profilen mit bis zu 10 % Ihrer lizenzierten Profile. [!DNL Profile] Verpflichtung (kumulativ über alle autorisierten Entwicklungs-Sandboxes gemessen). Sie haben Anspruch auf:
   * Durchschnittliche Reichweite des Nicht-Produktionsprofils von 75 Kilobytes pro autorisiertem Nicht-Produktionsprofil (kumulativ gemessen in allen autorisierten Entwicklungs-Sandboxes);
   * Ein Batch-Segmentierungsauftrag pro Tag, pro Entwicklungs-Sandbox;
   * Ein Durchschnitt von 120 [!DNL Profile] API-Aufrufe pro [!DNL Profile], pro Jahr (kumulativ über alle Ihre autorisierten Entwicklungs-Sandboxes hinweg gemessen).

Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](./home.md).

## Kann ich von verschiedenen Sandboxes aus auf eine bestimmte Ressource zugreifen?

Sandboxes sind voneinander isolierte Partitionen einer einzelnen Platform-Instanz, wobei jede Sandbox eine eigene unabhängige Ressourcenbibliothek unterhält. Eine Ressource, die in einer Sandbox vorhanden ist, kann unabhängig vom Sandbox-Typ (Produktion oder Nicht-Produktion) nicht von einer anderen Sandbox aus aufgerufen werden.

## Was ist die standardmäßige Produktions-Sandbox?

Die standardmäßige Produktions-Sandbox ist die erste Produktions-Sandbox, die erstellt wird, wenn eine IMS-Organisation zum ersten Mal bereitgestellt wird. Mit der standardmäßigen Produktions-Sandbox können Sie Daten aus Platform erfassen oder nutzen sowie Anforderungen akzeptieren, die keine Werte für einen Sandbox-Namen oder eine Sandbox-ID enthalten. Die standardmäßige Produktions-Sandbox kann zurückgesetzt, aber nicht gelöscht werden.

## Wie viele Produktions-Sandboxes können wir nutzen?

Eine Experience Platform-Instanz unterstützt mehrere Produktions- und Entwicklungs-Sandboxes, wobei jede Sandbox eine eigene unabhängige Bibliothek mit Platform-Ressourcen (einschließlich Schemas, Datensätzen und Profilen) unterhält.

Mit einer Standardlizenz für Experience Platformen erhalten Sie insgesamt fünf Sandboxes, die Sie als  oder Entwicklung klassifizieren können. Sie können weitere Packs mit 10 Sandboxes bis zu insgesamt maximal 75 Sandboxes lizenzieren.

Produktions-Sandboxes können zurückgesetzt oder gelöscht werden, mit Ausnahme der Produktions-Sandboxes, die auch von Adobe Analytics für die [Geräteübergreifende Analyse (Cross Device Analytics, CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=de) oder wenn das innerhalb dieser Funktion gehostete Identitätsdiagramm auch von Adobe Audience Manager für die [Benutzerbasierte Ziele (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=de) Funktion.

Sie können den Titel einer Produktions-Sandbox aktualisieren. Eine Produktions-Sandbox kann jedoch nicht umbenannt werden.

>[!NOTE]
>
>Der Sandbox-Name wird für Suchzwecke in API-Aufrufen verwendet, während der Sandbox-Titel als Anzeigename verwendet wird.

## Wie viele Entwicklungs-Sandboxes kann ich haben?

In Experience Platform können derzeit maximal 75 Sandboxes (Produktion und Entwicklung) in einer IMS-Organisation aktiv sein.

Entwicklungs-Sandboxes unterstützen Funktionen zum Zurücksetzen und Löschen.

## Ich habe gerade eine Sandbox eingerichtet. Wie lege ich Berechtigungen für Benutzer fest, die mit dieser Sandbox arbeiten sollen?

Adobe Admin Console verknüpft Benutzer über Profile mit Sandboxes und Berechtigungen. Nachdem Sie eine neue Sandbox erstellt haben, navigieren Sie zum Tab **Berechtigungen** des Produktprofils, dem Sie Zugriff gewähren möchten, und klicken Sie dann auf **Sandboxes**. Nun können Sie Zugriff auf die neue Sandbox genauso wie bei anderen Berechtigungen hinzufügen oder entfernen.

Wenn Sie Benutzern einer bestimmten Sandbox eindeutige Berechtigungen hinzufügen möchten, müssen Sie möglicherweise ein neues Produktprofil mit den jeweiligen Sandboxes und Berechtigungen erstellen und die gewünschten Benutzer diesem Profil zuordnen.

Weiterführende Informationen zum Verwalten von Sandboxes und Berechtigungen in der Admin Console finden Sie im [Benutzerhandbuch zur Zugriffskontrolle](../access-control/ui/overview.md).
