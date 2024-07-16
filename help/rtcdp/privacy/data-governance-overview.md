---
keywords: Data Governance rtcdp;rtcdp Data Governance;Echtzeit-Data Profil Data Governance
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

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) führt Daten aus verschiedenen Unternehmenssystemen zusammen, sodass Marketing-Experten ihre Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher müssen Sie sicherstellen, dass Real-Time CDP bei der Verarbeitung Ihrer Daten mit Nutzungsrichtlinien konform ist.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Es spielt in Real-Time CDP eine wichtige Rolle, da Sie Nutzungsrichtlinien definieren, Ihre Daten basierend auf diesen Richtlinien kategorisieren und bei der Durchführung bestimmter Marketing-Aktionen auf Richtlinienverstöße überprüfen können.

Real-Time CDP basiert auf Adobe Experience Platform und daher werden die meisten Data Governance-Funktionen in der [!DNL Experience Platform] -Dokumentation behandelt. Dieses Dokument soll die [Übersicht über Data Governance](../../data-governance/home.md) für [!DNL Experience Platform] ergänzen und die in Real-Time CDP verfügbaren Governance-Funktionen skizzieren. Folgende Themen werden behandelt:

* [Nutzungsbezeichnungen auf Daten anwenden ](#labels)
* [Richtlinien zur Datennutzung verwalten](#policies)
* [Einhaltung von Datennutzungsrichtlinien durchsetzen](#enforce)

## Nutzungsbezeichnungen auf Daten anwenden {#labels}

Mit Data Governance können Sie Nutzungsbezeichnungen auf Ihre Daten anwenden, entweder auf der Datensatz- oder der Datensatzfeldebene. Mit Datennutzungsbezeichnungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren.

Genauere Informationen zum Arbeiten mit Datennutzungsbezeichnungen finden Sie im [Benutzerhandbuch für Datennutzungsbezeichnungen](../../data-governance/labels/overview.md) für Adobe Experience Platform.

## Konfigurieren von Marketing-Aktionen für Ziele {#destinations}

Sie können Datennutzungsbeschränkungen für ein Ziel festlegen, indem Sie Marketing-Aktionen (auch Marketing-Anwendungsfälle genannt) für dieses Ziel definieren. Eine Marketing-Aktion für ein Ziel gibt den Zweck der Daten an, die an dieses Ziel exportiert werden.

>[!NOTE]
>
>Weitere Informationen zu Marketing-Aktionen und deren Verwendung in Datennutzungsrichtlinien finden Sie unter [Datennutzungsrichtlinien - Übersicht](../../data-governance/policies/overview.md) in der [!DNL Experience Platform] -Dokumentation.

Durch die Definition von Marketing-Aktionen für Ziele können Sie sicherstellen, dass alle an diese Ziele gesendeten Profile oder Zielgruppen mit Datennutzungsrichtlinien konform sind. Daher sollten Sie Ihren Zielen entsprechend den Anforderungen Ihres Unternehmens, Richtlinienbeschränkungen für die Aktivierung durchzusetzen, geeignete Marketing-Aktionen hinzufügen.

Marketing-Aktionen können nur beim erstmaligen Einrichten eines Ziels ausgewählt werden. Je nach Zieltyp, mit dem Sie arbeiten, wird die Möglichkeit zur Konfiguration von Marketing-Aktionen an verschiedenen Punkten im Setup-Workflow angezeigt. Anweisungen zum Konfigurieren Ihres bestimmten Ziels finden Sie in der Dokumentation zu [Zielen](../destinations/overview.md) .

## Richtlinien zur Datennutzung verwalten {#policies}

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in Real-Time CDP ausführen bzw. nicht ausführen dürfen. Weitere Informationen finden Sie im Abschnitt &quot;Datennutzungsrichtlinien&quot;in der [!DNL Experience Platform] [Übersicht über Data Governance](../../data-governance/home.md) .

Adobe Experience Platform bietet mehrere zentrale Richtlinien für gängige Anwendungsfälle für Kundenerlebnisse. Diese Richtlinien können in der Benutzeroberfläche angezeigt werden, indem Sie zum Arbeitsbereich **[!UICONTROL Richtlinien]** navigieren und die Registerkarte **[!UICONTROL Durchsuchen]** auswählen. Detailliertere Schritte zum Arbeiten mit Richtlinien in der Benutzeroberfläche, einschließlich der Erstellung eigener benutzerdefinierter Richtlinien, finden Sie im [Richtlinien-Benutzerhandbuch](../../data-governance/policies/user-guide.md) in der [!DNL Experience Platform] -Dokumentation.

## Einhaltung von Datennutzungsrichtlinien durchsetzen {#enforce}

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Beim Aktivieren von Zielgruppen für Ziele in Real-Time CDP erzwingt Data Governance automatisch Nutzungsrichtlinien, falls Verstöße auftreten sollten.

Weitere Informationen finden Sie im Dokument zur [automatischen Richtliniendurchsetzung](../../data-governance/enforcement/auto-enforcement.md) .

## Nächste Schritte

Nachdem Sie die wichtigsten Data Governance-Funktionen in Real-Time CDP eingeführt und wie [!DNL Experience Platform] sie aktiviert hat, lesen Sie nun die [Dokumentation für Data Governance in Adobe Experience Platform](../../data-governance/home.md). Die Dokumentation bietet einen Überblick über wesentliche Data Governance-Konzepte sowie schrittweise Workflows zum Verwalten von Datennutzungsbezeichnungen und -richtlinien.

Das folgende Video bietet einen Überblick über Data Governance in Real-Time CDP, einschließlich der Verwendung von Marketing-Anwendungsfällen für Ziele und Beispiel-Workflows für verschiedene Szenarien:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
