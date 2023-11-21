---
keywords: Data Governance rtcdp;rtcdp Data Governance;Echtzeit-Data Profil Data Governance
title: Data Governance – Übersicht
description: Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 34%

---

# Data Governance in Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) führt Daten aus verschiedenen Unternehmenssystemen zusammen, sodass Marketing-Experten ihre Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher müssen Sie sicherstellen, dass Real-Time CDP bei der Verarbeitung Ihrer Daten mit Nutzungsrichtlinien konform ist.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Es spielt in Real-Time CDP eine wichtige Rolle, da Sie Nutzungsrichtlinien definieren, Ihre Daten basierend auf diesen Richtlinien kategorisieren und bei der Durchführung bestimmter Marketing-Aktionen auf Richtlinienverstöße überprüfen können.

Real-Time CDP basiert auf Adobe Experience Platform, weshalb der Großteil der Data Governance-Funktionen in der [!DNL Experience Platform] Dokumentation. Dieses Dokument soll die [Data Governance - Übersicht](../../data-governance/home.md) für [!DNL Experience Platform]und beschreibt die Governance-Funktionen, die in Real-Time CDP verfügbar sind. Folgende Themen werden behandelt:

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
>Weitere Informationen zu Marketing-Aktionen und deren Verwendung in Datennutzungsrichtlinien finden Sie unter [Datennutzungsrichtlinien - Übersicht](../../data-governance/policies/overview.md) im [!DNL Experience Platform] Dokumentation.

Durch die Definition von Marketing-Aktionen für Ziele können Sie sicherstellen, dass alle an diese Ziele gesendeten Profile oder Segmente mit Datennutzungsrichtlinien konform sind. Daher sollten Sie Ihren Zielen entsprechend den Anforderungen Ihres Unternehmens, Richtlinienbeschränkungen für die Aktivierung durchzusetzen, geeignete Marketing-Aktionen hinzufügen.

Marketing-Aktionen können nur beim erstmaligen Einrichten eines Ziels ausgewählt werden. Je nach Zieltyp, mit dem Sie arbeiten, wird die Möglichkeit zur Konfiguration von Marketing-Aktionen an verschiedenen Punkten im Setup-Workflow angezeigt. Siehe [Dokumentation zu Zielen](../destinations/overview.md) für Schritte zur Konfiguration Ihres bestimmten Ziels.

## Richtlinien zur Datennutzung verwalten {#policies}

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in Real-Time CDP ausführen bzw. nicht ausführen dürfen. Weiterführende Informationen dazu finden Sie im Abschnitt „Datennutzungsrichtlinien“ unter [!DNL Experience Platform][Data Governance – Übersicht](../../data-governance/home.md) für 

Adobe Experience Platform bietet verschiedene zentrale Richtlinien für gängige Anwendungsfälle bei Kundenerlebnissen. Diese Richtlinien können in der Benutzeroberfläche angezeigt werden, indem Sie zur **[!UICONTROL Richtlinien]** Arbeitsbereich und wählen Sie die **[!UICONTROL Durchsuchen]** Registerkarte. Siehe [Richtlinien-Benutzerhandbuch](../../data-governance/policies/user-guide.md) im [!DNL Experience Platform] Dokumentation für detailliertere Schritte zum Arbeiten mit Richtlinien in der Benutzeroberfläche, einschließlich der Erstellung eigener benutzerdefinierter Richtlinien.

## Einhaltung von Datennutzungsrichtlinien durchsetzen {#enforce}

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Beim Aktivieren von Zielgruppensegmenten für Ziele in Real-Time CDP erzwingt Data Governance automatisch Nutzungsrichtlinien, falls Verstöße auftreten.

Siehe Dokument unter [automatische Richtliniendurchsetzung](../../data-governance/enforcement/auto-enforcement.md) für weitere Informationen.

## Nächste Schritte

Nachdem Sie nun die wichtigsten Data Governance-Funktionen in Real-Time CDP eingeführt haben und wie [!DNL Experience Platform] ermöglicht ihnen, bitte mit der [Dokumentation für Data Governance in Adobe Experience Platform](../../data-governance/home.md). Die Dokumentation bietet einen Überblick über wesentliche Data Governance-Konzepte sowie schrittweise Workflows zum Verwalten von Datennutzungsbezeichnungen und -richtlinien.

Das folgende Video bietet einen Überblick über Data Governance in Real-Time CDP, einschließlich der Verwendung von Marketing-Anwendungsfällen für Ziele und Beispiel-Workflows für verschiedene Szenarien:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
