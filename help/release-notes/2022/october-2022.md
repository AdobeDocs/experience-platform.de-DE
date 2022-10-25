---
title: Adobe Experience Platform - Versionshinweise, Oktober 2022
description: Die Versionshinweise für Adobe Experience Platform vom Oktober 2022.
source-git-commit: 098b4b7a0dcd3ddfcd13f7dd473c4fa6832d23df
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 54%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 26. Oktober 2022**

Neue Funktionen in Adobe Experience Platform:

- [Vom Kunden verwaltete Schlüssel](#cmk)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Experience-Datenmodell (XDM)](#xdm)
- [Quellen](#sources)

## Vom Kunden verwaltete Schlüssel {#cmk}

Alle in Adobe Experience Platform gespeicherten Daten werden im Ruhezustand mithilfe von Schlüsseln auf Systemebene verschlüsselt. Wenn Sie eine Anwendung verwenden, die auf Platform aufbaut, können Sie jetzt stattdessen eigene Verschlüsselungsschlüssel verwenden, um die Datensicherheit zu verbessern.

Siehe Übersicht unter [kundenverwaltete Schlüssel](../../landing/governance-privacy-security/customer-managed-keys.md) für Details zur Funktion.

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Umgang mit sensiblen Daten für Datastreams | Datastreams nutzt jetzt verschiedene Platform-Technologien, um sensible Daten, wie sie durch Vorschriften wie den Health Insurance Portability and Accounability Act (HIPAA) durchgesetzt werden, angemessen zu handhaben. Siehe Abschnitt zu [Umgang mit sensiblen Daten in Datenströmen](../../edge/datastreams/overview.md#sensitive) für weitere Informationen. |
| [!DNL Splunk] Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten an senden [!DNL Splunk] mit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) -Erweiterung. Siehe [[!DNL Splunk] Erweiterungsübersicht](../../tags/extensions/web/splunk/overview.md) für weitere Informationen. |
| [!DNL Zendesk] Erweiterung für die Ereignisweiterleitung | Sie können jetzt Daten an senden [!DNL Zendesk] mit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) -Erweiterung. Siehe [[!DNL Zendesk] Erweiterungsübersicht](../../tags/extensions/web/zendesk/overview.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Datentyp | [[!UICONTROL Informationen zu Sitzungsdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Die `authorized` von einem booleschen Typ in eine Zeichenfolge. `season` und `episode` wurden von Ganzzahlen in Zeichenfolgen geändert. |
| Datentyp | [[!UICONTROL Informationen zu Werbedetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` wurde in `friendlyName`und `ID` wurde in `name`. |
| Datentyp | [[!UICONTROL Informationen zu Fehlerdetails]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` wurde in `name` umbenannt.  |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- | 
| Beta-Verfügbarkeit der Adobe Workfront-Quelle | Verwenden Sie die [Adobe Workfront-Quelle](../../sources/connectors/adobe-applications/workfront.md) , um Ihre Workfront-Daten in die Experience Platform zu bringen und Anwendungsfälle auszuführen, z. B. die Kombination Ihrer Arbeitsdatensätze mit Drittanbieterdaten, die Anwendung von Verlaufs- und Zeitreihenanalysen auf Arbeitsdatensätze und die Abfrage von Arbeitsdaten mit SQL. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer Workfront-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Beta-Verfügbarkeit der Oracle Service Cloud-Quelle | Verwenden Sie die Oracle Service Cloud-Quelle, um Daten aus Ihrem Oracle Service Cloud-Konto in Experience Platform aufzunehmen. Weitere Informationen finden Sie in der Dokumentation unter [Oracle Service Cloud-Quelle](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Weiterführende Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
