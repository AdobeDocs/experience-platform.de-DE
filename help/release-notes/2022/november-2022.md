---
title: Adobe Experience Platform – Versionshinweise November 2022
description: Die Versionshinweise von November 2022 für Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: ht
source-wordcount: '454'
ht-degree: 100%

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
| [!DNL AWS]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten an [!DNL Amazon Web Services] ([!DNL AWS]) über eine Erweiterung für die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) senden. Weiterführende Informationen dazu finden Sie in der [[!DNL AWS] Übersicht der Erweiterungen](../../tags/extensions/server/aws/overview.md). |
| [!DNL Google Ads Enhanced Conversions]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Konvertierungsdaten an [!DNL Google Ads] senden, indem Sie eine Erweiterung für die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) verwenden. Weiterführende Informationen dazu finden Sie in der [[!DNL Google Ads Enhanced Conversions] Übersicht der Erweiterungen](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md). |
| [!DNL Microsoft Azure]-Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten mithilfe einer Erweiterung zur [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) an [!DNL Microsoft Azure] senden. Weiterführende Informationen dazu finden Sie in der [[!DNL Microsoft Azure] Übersicht der Erweiterungen](../../tags/extensions/server/azure/overview.md). |

Weitere Informationen zu den Datenerfassungsfunktionen von Platform finden Sie unter [Datenerfassung – Übersicht](../../collection/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zuweisen von Feldern zu benutzerdefinierten Klassen beim direkten Hinzufügen zu einem Schema | Wenn Sie [ein einzelnes Feld direkt zu einem Schema hinzufügen](../../xdm/ui/resources/schemas.md#add-individual-fields), konnten Sie das Feld bisher nur einer Feldergruppe als übergeordnete Ressource zuweisen. Jetzt können Sie zusätzlich zu den Feldergruppen [das Feld stattdessen einer benutzerdefinierten Klasse](../../xdm/ui/resources/schemas.md#add-to-class) als übergeordnete Ressource zuweisen. |

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
