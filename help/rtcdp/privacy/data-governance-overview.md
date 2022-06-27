---
keywords: Data Governance rtcdp;rtcdp Data Governance;Echtzeit-Data Profil Data Governance
title: Data Governance – Übersicht
description: 'Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. '
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 51%

---

# Data Governance in der Echtzeit-Kundendatenplattform

[!DNL Real-time Customer Data Platform] (Echtzeit-Kundendatenplattform) führt Daten aus verschiedenen Unternehmenssystemen zusammen, sodass Marketing-Experten ihre Kunden besser identifizieren, verstehen und ansprechen können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher muss sichergestellt sein, dass die Echtzeit-Kundendatenplattform bei der Verarbeitung Ihrer Daten mit den Nutzungsrichtlinien konform ist.

Mit Data Governance in Adobe Experience Platform können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. Data Governance spielt in der Echtzeit-Kundendatenplattform eine zentrale Rolle und erlaubt es Ihnen, Nutzungsrichtlinien zu definieren, Daten anhand dieser Richtlinien zu kategorisieren und bei Ausführung bestimmter Marketing-Aktionen auf Richtlinienverletzungen zu prüfen.

Die Echtzeit-Kundendatenplattform basiert auf Adobe Experience Platform. Daher werden die meisten Data Governance-Funktionen im Abschnitt [!DNL Experience Platform] Dokumentation. Dieses Dokument dient als Ergänzung zu [Data Governance – Übersicht](../../data-governance/home.md) für und bietet Informationen zu den Governance-Funktionen, die in der Echtzeit-Kundendatenplattform verfügbar sind.[!DNL Experience Platform] Folgende Themen werden behandelt:

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

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in der Echtzeit-Kundendatenplattform ausführen bzw. nicht ausführen dürfen. Weiterführende Informationen dazu finden Sie im Abschnitt „Datennutzungsrichtlinien“ unter [!DNL Experience Platform][Data Governance – Übersicht](../../data-governance/home.md) für 

Adobe Experience Platform bietet verschiedene zentrale Richtlinien für gängige Anwendungsfälle bei Kundenerlebnissen. Diese Richtlinien können in der Benutzeroberfläche angezeigt werden, indem Sie zur **[!UICONTROL Richtlinien]** Arbeitsbereich und wählen Sie die **[!UICONTROL Durchsuchen]** Registerkarte. Siehe [Richtlinien-Benutzerhandbuch](../../data-governance/policies/user-guide.md) im [!DNL Experience Platform] Dokumentation für detailliertere Schritte zum Arbeiten mit Richtlinien in der Benutzeroberfläche, einschließlich der Erstellung eigener benutzerdefinierter Richtlinien.

## Einhaltung von Datennutzungsrichtlinien durchsetzen {#enforce}

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Beim Aktivieren von Zielgruppensegmenten in der Echtzeit-Kundendatenplattform erzwingt Data Governance automatisch Nutzungsrichtlinien, falls Verstöße auftreten sollten.

Siehe Dokument unter [automatische Richtliniendurchsetzung](../../data-governance/enforcement/auto-enforcement.md) für weitere Informationen.

## Nächste Schritte

Jetzt wurden Sie mit den wichtigsten Data Governance-Funktionen in der Echtzeit-Kundendatenplattform und der [!DNL Experience Platform] ermöglicht ihnen, bitte mit der [Dokumentation für Data Governance in Adobe Experience Platform](../../data-governance/home.md). Die Dokumentation bietet einen Überblick über wesentliche Data Governance-Konzepte sowie schrittweise Workflows zum Verwalten von Datennutzungsbezeichnungen und -richtlinien.

Das folgende Video bietet einen Überblick über Data Governance in der Echtzeit-Kundendatenplattform, einschließlich der Verwendung von Marketing-Anwendungsfällen für Ziele und Beispiel-Workflows für verschiedene Szenarien:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
