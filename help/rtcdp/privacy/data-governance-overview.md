---
keywords: Data Governance RTCDP;RTCDP Data Governance;Data Governance für Echtzeit-Kundenprofil
title: Data Governance – Übersicht
description: Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 30%

---

# Data Governance in Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) führt Daten aus verschiedenen Unternehmenssystemen zusammen, sodass Marketing-Experten Kundinnen und Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher müssen Sie bei der Verarbeitung Ihrer Daten sicherstellen, dass Real-Time CDP Nutzungsrichtlinien einhält.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Die Funktion spielt eine wichtige Rolle in Real-Time CDP, denn sie ermöglicht es Ihnen, Nutzungsrichtlinien zu definieren, Ihre Daten basierend auf diesen Richtlinien zu kategorisieren und bei der Durchführung bestimmter Marketing-Aktionen zu überprüfen, ob Richtlinien verletzt werden.

Real-Time CDP basiert auf Adobe Experience Platform. Daher werden die meisten Data Governance-Funktionen in der [!DNL Experience Platform]-Dokumentation behandelt. Dieses Dokument soll die [Übersicht zu Data Governance](../../data-governance/home.md) für [!DNL Experience Platform] ergänzen und beschreibt die in Real-Time CDP verfügbaren Governance-Funktionen. Folgende Themen werden behandelt:

* [Nutzungsbezeichnungen auf Daten anwenden &#x200B;](#labels)
* [Richtlinien zur Datennutzung verwalten](#policies)
* [Einhaltung von Datennutzungsrichtlinien durchsetzen](#enforce)

## Nutzungsbezeichnungen auf Daten anwenden {#labels}

Mit Data Governance können Sie Nutzungsbezeichnungen auf Ihre Daten anwenden, entweder auf der Datensatz- oder der Datensatzfeldebene. Mit Datennutzungsbezeichnungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren.

Genauere Informationen zum Arbeiten mit Datennutzungsbezeichnungen finden Sie im [Benutzerhandbuch für Datennutzungsbezeichnungen](../../data-governance/labels/overview.md) für Adobe Experience Platform.

## Konfigurieren von Marketing-Aktionen für Ziele {#destinations}

Sie können Datennutzungsbeschränkungen für ein Ziel festlegen, indem Sie Marketing-Aktionen (auch als Marketing-Anwendungsfälle bezeichnet) für dieses Ziel definieren. Eine Marketing-Aktion für ein Ziel gibt die Absicht der Daten an, die an dieses Ziel exportiert werden.

>[!NOTE]
>
>Weitere Informationen zu Marketing-Aktionen und deren Verwendung in Datennutzungsrichtlinien finden Sie unter [Datennutzungsrichtlinien - Übersicht](../../data-governance/policies/overview.md) in der [!DNL Experience Platform].

Durch das Definieren von Marketing-Aktionen für Ziele können Sie sicherstellen, dass alle Profile oder Zielgruppen, die an diese Ziele gesendet werden, mit Datennutzungsrichtlinien konform sind. Sie sollten daher Ihren Zielen geeignete Marketing-Aktionen hinzufügen, je nach den Anforderungen Ihres Unternehmens, um Richtlinienbeschränkungen für die Aktivierung durchzusetzen.

Marketing-Aktionen können nur ausgewählt werden, wenn ein Ziel zum ersten Mal eingerichtet wird. Je nach dem Zieltyp, mit dem Sie arbeiten, wird die Möglichkeit zur Konfiguration von Marketing-Aktionen an verschiedenen Stellen im Einrichtungs-Workflow angezeigt. Anweisungen zum Konfigurieren [&#x200B; bestimmten Ziels finden &#x200B;](../destinations/overview.md) in der Dokumentation zu Zielen .

## Richtlinien zur Datennutzung verwalten {#policies}

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in Real-Time CDP ausführen bzw. nicht ausführen dürfen. Weitere Informationen finden Sie im Abschnitt „Datennutzungsrichtlinien“ in der [!DNL Experience Platform] [Übersicht zu Data &#x200B;](../../data-governance/home.md).

Adobe Experience Platform bietet mehrere Kernrichtlinien für gängige Anwendungsfälle von Kundenerlebnissen. Diese Richtlinien können in der Benutzeroberfläche angezeigt werden, indem Sie zum Arbeitsbereich **[!UICONTROL Richtlinien]** navigieren und die Registerkarte **[!UICONTROL Durchsuchen]** auswählen. Ausführlichere Anweisungen zum Arbeiten mit Richtlinien in der Benutzeroberfläche, einschließlich [, wie Sie Ihre eigenen benutzerdefinierten Richtlinien erstellen, finden Sie &#x200B;](../../data-governance/policies/user-guide.md) der [!DNL Experience Platform]-Dokumentation im Benutzerhandbuch für Richtlinien .

## Einhaltung von Datennutzungsrichtlinien durchsetzen {#enforce}

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Beim Aktivieren von Zielgruppen für Ziele in Real-Time CDP erzwingt Data Governance automatisch Nutzungsrichtlinien, falls Verstöße auftreten sollten.

Weitere Informationen finden Sie im Dokument [Automatische Richtliniendurchsetzung](../../data-governance/enforcement/auto-enforcement.md) .

## Nächste Schritte

Nachdem Sie nun mit den wichtigsten Data Governance-Funktionen in Real-Time CDP vertraut sind und erfahren haben, wie [!DNL Experience Platform] diese aktiviert, lesen Sie bitte die [Dokumentation zu Data Governance in Adobe Experience Platform](../../data-governance/home.md). Die Dokumentation bietet einen Überblick über wesentliche Data Governance-Konzepte sowie schrittweise Workflows zum Verwalten von Datennutzungsbezeichnungen und -richtlinien.

Das folgende Video bietet einen Überblick über Data Governance in Real-Time CDP, einschließlich der Verwendung von Marketing-Anwendungsfällen für Ziele und Beispiel-Workflows für verschiedene Szenarien:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
