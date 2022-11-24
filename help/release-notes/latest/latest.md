---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f8e8ec0fb13fc988d47bb3bbe85f953e66b33f13
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 79%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 23. November 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Experience-Datenmodell (XDM)](#xdm)
- [Quellen](#sources)

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL AWS]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten an senden [!DNL Amazon Web Services] ([!DNL AWS]) mithilfe einer [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) -Erweiterung. Weiterführende Informationen dazu finden Sie in der [[!DNL AWS] Übersicht der Erweiterungen](../../tags/extensions/server/aws/overview.md). |
| [!DNL Google Ads Enhanced Conversions]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Konversionsdaten an senden [!DNL Google Ads] mit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) -Erweiterung. Weiterführende Informationen dazu finden Sie in der [[!DNL Google Ads Enhanced Conversions] Übersicht der Erweiterungen](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md). |
| [!DNL Microsoft Azure]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten mithilfe einer Erweiterung zur [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) an [!DNL Microsoft Azure] senden. Weiterführende Informationen dazu finden Sie in der [[!DNL Microsoft Azure] Übersicht der Erweiterungen](../../tags/extensions/server/azure/overview.md). |

Weitere Informationen zu den Datenerfassungsfunktionen von Platform finden Sie unter [Datenerfassung - Übersicht](../../collection/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Weisen Sie beim direkten Hinzufügen zu einem Schema benutzerdefinierten Klassen Felder zu | Wann [Hinzufügen eines einzelnen Felds direkt zu einem Schema](../../xdm/ui/resources/schemas.md#add-individual-fields), konnten Sie zuvor nur das Feld einer Feldergruppe als übergeordnete Ressource zuweisen. Zusätzlich zu den Feldergruppen können Sie [das Feld einer benutzerdefinierten Klasse zuweisen](../../xdm/ui/resources/schemas.md#add-to-class) als übergeordnete Ressource. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- | 
| Beta-Verfügbarkeit der Oracle Service Cloud-Quelle | Verwenden Sie die Oracle Service Cloud-Quelle, um Daten aus Ihrem Oracle Service Cloud-Konto in Experience Platform aufzunehmen. Weitere Informationen finden Sie in der Dokumentation zur [Oracle Service Cloud-Quelle](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Weiterführende Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).