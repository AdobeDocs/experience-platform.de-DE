---
keywords: Datenverwaltung rtcdp;rtcdp Datenverwaltung;Echtzeit-Daten-Profil-Datenverwaltung
title: Data Governance – Übersicht
seo-title: Data Governance in der Echtzeit-Kundendatenplattform
description: 'Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. '
seo-description: 'Mit Data Governance können Sie Kundendaten verwalten und bei der Verwendung von Daten die Einhaltung von Vorschriften, Einschränkungen und Richtlinien sicherstellen. '
translation-type: tm+mt
source-git-commit: 5435661d750c4138ea6a2d40619a48236b7b1e4f
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 44%

---


# [!DNL Data Governance] in Echtzeit-CDP

[!DNL Real-time Customer Data Platform] (Echtzeit-CDP) führt Daten aus mehreren Unternehmenssystemen zusammen, sodass Marketingexperten ihre Kunden besser identifizieren, verstehen und binden können. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Daher muss sichergestellt sein, dass die Echtzeit-Kundendatenplattform bei der Verarbeitung Ihrer Daten mit den Nutzungsrichtlinien konform ist.

Mit Adobe Experience Platform [!DNL Data Governance] können Sie Kundendaten verwalten und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung sicherstellen. Data Governance spielt in der Echtzeit-Kundendatenplattform eine zentrale Rolle und erlaubt es Ihnen, Nutzungsrichtlinien zu definieren, Daten anhand dieser Richtlinien zu kategorisieren und bei Ausführung bestimmter Marketing-Aktionen auf Richtlinienverletzungen zu prüfen.

Die Echtzeit-CDP basiert auf Adobe Experience Platform, und deshalb werden die meisten [!DNL Data Governance]-Funktionen in der [!DNL Experience Platform]-Dokumentation behandelt. Dieses Dokument dient als Ergänzung zu [Data Governance – Übersicht](../../data-governance/home.md) für und bietet Informationen zu den Governance-Funktionen, die in der Echtzeit-Kundendatenplattform verfügbar sind.[!DNL Experience Platform] Folgende Themen werden behandelt:

* [Nutzungsbezeichnungen auf Daten anwenden](#labels)
* [Richtlinien zur Datennutzung verwalten](#policies)
* [Einhaltung von Datennutzungsrichtlinien durchsetzen](#enforce)

## Nutzungsbezeichnungen auf Daten anwenden  {#labels}

[!DNL Data Governance]Mit können Sie Nutzungsbezeichnungen auf Ihre Daten anwenden, entweder auf der Datensatz- oder der Datensatzfeldebene. Mit Datennutzungsbezeichnungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren.

Genauere Informationen zum Arbeiten mit Datennutzungsbezeichnungen finden Sie im [Benutzerhandbuch für Datennutzungsbezeichnungen](../../data-governance/labels/overview.md) für Adobe Experience Platform.

## Konfigurieren von Marketingaktionen für Ziele {#destinations}

Sie können Datenverwendungsbeschränkungen für ein Ziel festlegen, indem Sie Marketingaktionen (auch als Marketing-Anwendungsfälle bezeichnet) für dieses Ziel definieren. Eine Marketingaktion für ein Ziel gibt den Zweck der Daten an, die an dieses Ziel exportiert werden.

>[!NOTE]
>
>Weitere Informationen zu Marketingaktionen und deren Verwendung in Datenverwendungsrichtlinien finden Sie in der [Übersicht über Datenverwendungsrichtlinien](../../data-governance/policies/overview.md) in der [!DNL Experience Platform]-Dokumentation.

Durch das Definieren von Marketingaktionen für Ziele können Sie sicherstellen, dass alle an diese Ziele gesendeten Profil oder Segmente mit den Datenverwendungsrichtlinien übereinstimmen. Daher sollten Sie Ihren Zielen entsprechend den Anforderungen Ihres Unternehmens, Richtlinienbeschränkungen für die Aktivierung durchzusetzen, entsprechende Marketingaktionen hinzufügen.

Marketingaktionen können nur beim erstmaligen Einrichten eines Ziels ausgewählt werden. Je nach Zieltyp, mit dem Sie arbeiten, wird die Möglichkeit zur Konfiguration von Marketingaktionen an verschiedenen Punkten im Setup-Arbeitsablauf angezeigt. Anweisungen zum Konfigurieren des jeweiligen Ziels finden Sie in der Dokumentation zu [Zielen](../destinations/overview.md).

## Datennutzungsrichtlinien verwalten {#policies}

Damit Datennutzungsbezeichnungen die Datenkonformität effektiv unterstützen können, müssen Sie Datennutzungsrichtlinien definieren und aktivieren. Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die Sie für Daten in der Echtzeit-Kundendatenplattform ausführen bzw. nicht ausführen dürfen. Weiterführende Informationen dazu finden Sie im Abschnitt „Datennutzungsrichtlinien“ unter [!DNL Experience Platform][Data Governance – Übersicht](../../data-governance/home.md) für 

Adobe Experience Platform bietet verschiedene zentrale Richtlinien für gängige Anwendungsfälle bei Kundenerlebnissen. Diese Richtlinien können in der Benutzeroberfläche angezeigt werden, indem Sie zum Arbeitsbereich **[!UICONTROL Richtlinien]** navigieren und die Registerkarte **[!UICONTROL Durchsuchen]** auswählen. Detailliertere Anweisungen zum Arbeiten mit Richtlinien in der Benutzeroberfläche finden Sie im [Richtlinien-Benutzerhandbuch](../../data-governance/policies/user-guide.md) in der [!DNL Experience Platform]-Dokumentation, einschließlich der Erstellung eigener benutzerdefinierter Richtlinien.

## Einhaltung von Datennutzungsrichtlinien durchsetzen {#enforce}

Nachdem Sie Daten gekennzeichnet und Nutzungsrichtlinien definiert haben, können Sie die Einhaltung von Datennutzungsrichtlinien erzwingen. Beim Aktivieren von Segmenten der Audience in Zielen in CDP in Echtzeit erzwingt [!DNL Data Governance] automatisch Nutzungsrichtlinien, falls Verstöße auftreten sollten.

Weitere Informationen finden Sie im Dokument [Automatische Richtliniendurchsetzung](../../data-governance/enforcement/auto-enforcement.md).

## Nächste Schritte

Nachdem Sie nun die wichtigsten [!DNL Data Governance]-Funktionen in Echtzeit-CDP und deren Aktivierung durch [!DNL Experience Platform] eingeführt haben, lesen Sie die [Dokumentation für Datenverwaltung unter Adobe Experience Platform](../../data-governance/home.md). Die Dokumentation bietet einen Überblick über grundlegende Konzepte von [!DNL Data Governance] sowie schrittweise Workflows für die Verwaltung von Datenverwendungsbeschriftungen und -richtlinien.

Das folgende Video bietet einen Überblick über [!DNL Data Governance] in Echtzeit-CDP, einschließlich der Verwendung von Anwendungsfällen für das Marketing bei Zielen und Workflows für verschiedene Szenarien:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)