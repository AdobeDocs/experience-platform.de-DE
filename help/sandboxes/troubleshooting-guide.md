---
keywords: Experience Platform;home;popular topics;sandbox troubleshooting
solution: Experience Platform
title: Handbuch zur Fehlerbehebung bei Sandboxes
topic-legacy: troubleshooting guide
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Sandboxes in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 2a7b2040c221ff039f17f78d9ca712032d9fc02c
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 44%

---

# Handbuch zur Fehlerbehebung bei Sandboxes

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Sandboxes in Adobe Experience Platform. Fragen und Fehlerbehebungen für andere Platform-Dienste finden Sie im [Handbuch zur Fehlerbehebung in Experience Platform](../landing/troubleshooting.md).

Sandboxes unterteilen eine einzelne Platform-Instanz in separate virtuelle Umgebungen, damit sich Programme für digitale Erlebnisse entwickeln und weiterentwickeln lassen. Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](home.md).

## Was ist eine Sandbox?

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Sandbox unterhält eine eigene, unabhängige Bibliothek mit Platform-Ressourcen (einschließlich Schemas, Datensätzen, Profilen usw.). Alle Inhalte und Aktionen, die innerhalb einer Sandbox ausgeführt werden, sind auf diese Sandbox beschränkt und wirken sich nicht auf andere Sandboxes aus. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](home.md).

## Welche Arten von Sandboxes gibt es und wie unterscheiden sie sich?

In Experience Platform gibt es zwei Arten von Sandboxes:

* **Production sandbox**: A production sandbox is meant to be used with profiles in your production environment. Platform ermöglicht es Ihnen, mehrere Produktions-Sandboxes zu erstellen, um die richtigen Funktionen für Daten bereitzustellen und gleichzeitig die betriebliche Isolierung beizubehalten. This feature allows you to dedicate specific production sandboxes to distinct lines of business, brands, projects, or regions. Produktions-Sandboxes unterstützen eine Vielzahl von Produktionsprofilen bis hin zu Ihren lizenzierten [!DNL Profile] Verpflichtung (kumulativ über alle Ihre autorisierten Produktions-Sandboxes gemessen). You are entitled to use licensed average profile per authorized [!DNL Profile] (measured cumulatively across all of your authorized production sandboxes).
* **Development sandbox**: A development sandbox is a sandbox that can be used exclusively for development and testing with non-production profiles. Entwicklungs-Sandboxes unterstützen eine Anzahl von Nicht-Produktions-Profilen mit bis zu 10 % Ihrer lizenzierten Profile. [!DNL Profile] Verpflichtung (kumulativ über alle autorisierten Entwicklungs-Sandboxes gemessen). Sie haben Anspruch auf:
   * Durchschnittliche Reichweite des Nicht-Produktionsprofils von 75 Kilobytes pro autorisiertem Nicht-Produktionsprofil (kumulativ gemessen in allen autorisierten Entwicklungs-Sandboxes);
   * One batch segmentation job per day, per development sandbox;
   * Ein Durchschnitt von 120 [!DNL Profile] API-Aufrufe pro [!DNL Profile], pro Jahr (kumulativ über alle Ihre autorisierten Entwicklungs-Sandboxes hinweg gemessen).

Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](./home.md).

## Kann ich von verschiedenen Sandboxes aus auf eine bestimmte Ressource zugreifen?

Sandboxes sind voneinander isolierte Partitionen einer einzelnen Platform-Instanz, wobei jede Sandbox eine eigene unabhängige Ressourcenbibliothek unterhält. Eine Ressource, die in einer Sandbox vorhanden ist, kann unabhängig vom Sandbox-Typ (Produktion oder Nicht-Produktion) nicht von einer anderen Sandbox aus aufgerufen werden.

## Was ist die standardmäßige Produktions-Sandbox?

Die standardmäßige Produktions-Sandbox ist die erste Produktions-Sandbox, die erstellt wird, wenn eine IMS-Organisation zum ersten Mal bereitgestellt wird. The default production sandbox allows you to ingest or consume data from Platform, as well as accept requests that do not include values for a sandbox name or a sandbox ID. The default production sandbox can be reset but not deleted.

## Wie viele Produktions-Sandboxes können wir nutzen?

Eine Experience Platform-Instanz unterstützt mehrere Produktions- und Entwicklungs-Sandboxes, wobei jede Sandbox eine eigene unabhängige Bibliothek mit Platform-Ressourcen (einschließlich Schemas, Datensätzen und Profilen) unterhält.

Mit einer Standardlizenz für Experience Platformen erhalten Sie insgesamt fünf Sandboxes, die Sie als  oder Entwicklung klassifizieren können. Sie können weitere Packs mit 10 Sandboxes bis zu insgesamt maximal 75 Sandboxes lizenzieren.

Produktions-Sandboxes können zurückgesetzt oder gelöscht werden, mit Ausnahme der Produktions-Sandboxes, die auch von Adobe Analytics für die [Geräteübergreifende Analyse (Cross Device Analytics, CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=de) oder wenn das innerhalb dieser Funktion gehostete Identitätsdiagramm auch von Adobe Audience Manager für die [Benutzerbasierte Ziele (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=de) Funktion.

You can update the title of a production sandbox. Eine Produktions-Sandbox kann jedoch nicht umbenannt werden.

>[!NOTE]
>
>Der Sandbox-Name wird für Suchzwecke in API-Aufrufen verwendet, während der Sandbox-Titel als Anzeigename verwendet wird.

## How many development sandboxes can I have?

In Experience Platform können derzeit maximal 75 Sandboxes (Produktion und Entwicklung) in einer IMS-Organisation aktiv sein.

Development sandboxes support both reset and delete functionalities.

## Ich habe gerade eine Sandbox eingerichtet. Wie lege ich Berechtigungen für Benutzer fest, die mit dieser Sandbox arbeiten sollen?

Adobe Admin Console verknüpft Benutzer über Profile mit Sandboxes und Berechtigungen. Nachdem Sie eine neue Sandbox erstellt haben, navigieren Sie zum Tab **Berechtigungen** des Produktprofils, dem Sie Zugriff gewähren möchten, und klicken Sie dann auf **Sandboxes**. Nun können Sie Zugriff auf die neue Sandbox genauso wie bei anderen Berechtigungen hinzufügen oder entfernen.

Wenn Sie Benutzern einer bestimmten Sandbox eindeutige Berechtigungen hinzufügen möchten, müssen Sie möglicherweise ein neues Produktprofil mit den jeweiligen Sandboxes und Berechtigungen erstellen und die gewünschten Benutzer diesem Profil zuordnen.

Weiterführende Informationen zum Verwalten von Sandboxes und Berechtigungen in der Admin Console finden Sie im [Benutzerhandbuch zur Zugriffskontrolle](../access-control/ui/overview.md).
