---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: fddefb7de85b5dcb8c8721e14d04efc0567ccae4
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 17%

---

# Hinweise zu Vorabversionen von Adobe Experience Platform

>[!IMPORTANT]
>
>Dieses Dokument ist als **Vorschau** der Versionshinweise für den aktuellen Monat gedacht. Release-Elemente können sich ändern und in der endgültigen Version hinzugefügt oder entfernt werden.

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Versionsdatum: Mittwoch, 29. Juli 2025**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Ziele](#destinations)
- [Datenaufnahme](#ingestion)
- [Abfrage-Service](#query-service)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandboxes](#sandboxes)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Aktualisierte Ziele**

| Ziel | Beschreibung |
| --- | --- |
| Konsolidierung von Marketo-Zielkarten | Marketo V2- und Marketo Engage-Zielkarten für die Personensynchronisierung wurden in einer einzigen, einheitlichen Zielkarte zusammengefasst. Diese Konsolidierung vereinfacht den Zielauswahlprozess und bietet ein optimiertes Erlebnis für Marketo-Integrationen. |

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Erweiterte Datenstrominformationen für Edge-Ziele | Verbesserte Informationen in der rechten Leiste für Adobe Target- und benutzerdefinierte Personalization-Ziele zeigen jetzt den Datenstromnamen an, bieten eine klarere Sichtbarkeit der zugehörigen Datenstromkonfigurationen und reduzieren die Verwirrung bei der Überprüfung vorhandener Datenflüsse. Der **[!UICONTROL Datenstrom-ID]**-Selektor im Zielkonfigurationsbildschirm wurde zu **[!UICONTROL Datenstrom]** aktualisiert, um die Klarheit in der Benutzeroberfläche zu verbessern. |
| Sichtbarkeit von Marketing-Aktionen bei der Zielauswahl | Marketing-Aktionen werden jetzt in der rechten Leiste der Registerkarte **[!UICONTROL Durchsuchen]** und auf der Seite **[!UICONTROL Datenflussausführungen]** angezeigt, sodass Sie Änderungen an Marketing-Aktionen sofort sehen können, ohne dass eine Navigation zur Ansichtsseite erforderlich ist. Diese Verbesserung verbessert das Benutzererlebnis, da die Konfiguration von Marketing-Aktionen während der Zieleinrichtung einfacher überprüft werden kann. |
| (Eingeschränkte Beta-Version) Bearbeiten von Marketing-Aktionen für Ziele | Sie können jetzt Marketing-Aktionen für vorhandene Ziele bearbeiten. Diese Funktion befindet sich in einer begrenzten Beta-Phase. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff zu erhalten. |
| Kontonamen und Beschreibungen für Zielverbindungen | Sie können jetzt beim Herstellen einer Verbindung zu Zielen Kontonamen und Beschreibungen hinzufügen, um eine bessere Verwaltung von Zielen mit mehreren Konten zu ermöglichen. |

**Fehlerbehebungen**

| Problem | Beschreibung |
| --- | --- |
| Bildlauffunktion für Kategorien | Es wurde ein Problem behoben, bei dem das seitliche Menü Kategorien im Ziel- und Quellkatalog beim Bewegen der Maus nicht ordnungsgemäß gescrollt wurde, was die Navigationsbenutzerfreundlichkeit für Benutzende, die Zielkategorien durchsuchen, verbessert hat. |

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Datenaufnahme {#ingestion}

Experience Platform bietet ein umfassendes Framework für die Datenaufnahme, das sowohl die Batch- als auch die Streaming-Datenaufnahme aus verschiedenen Quellen unterstützt.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für die Überwachung der Aufnahme von Streaming-Profilen | Die Echtzeit-Überwachung für die Aufnahme von Streaming-Profilen ist jetzt verfügbar und bietet Transparenz in Metriken zu Durchsatz, Latenz und Datenqualität. Dies unterstützt proaktive Warnhinweise und umsetzbare Einblicke, um Dateningenieuren dabei zu helfen, Kapazitätsverletzungen und Aufnahmeprobleme zu identifizieren. |

Weitere Informationen finden Sie unter [Übersicht über die Datenaufnahme](../ingestion/home.md).

## Abfrage-Service {#query-service}

Adobe Experience Platform Query Service bietet eine robuste SQL-Schnittstelle für die Datenanalyse und -erkundung auf der gesamten Plattform.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbessertes Sitzungsmanagement | Data Distiller bietet jetzt erweiterte Sitzungsverwaltungsfunktionen, eine bessere Kontrolle über Benutzersitzungen und eine verbesserte Leistungsüberwachung in Entwicklungs- und Produktionsumgebungen. |
| Unterstützung für nicht ablaufende Zugangsdaten und Passwortzeichenbeschränkungen | Data Distiller unterstützt jetzt nicht ablaufende Anmeldeinformationen mit bestimmten Zeichenbeschränkungen. Kennwörter erfordern mindestens eine Zahl, einen Kleinbuchstaben, einen Großbuchstaben und ein Sonderzeichen, das Dollarzeichen ($) wird jedoch nicht unterstützt. Zu den empfohlenen Sonderzeichen gehören `!, @, #, ^, or &`. |
| Verbesserte Performance und Konsistenz in allen Umgebungen | Die Leistung von Data Distiller ist jetzt zwischen Entwicklungs- und Produktions-Sandboxes konsistent, wobei ähnliche Backend-Ressourcen in beiden Umgebungen verfügbar sind. Die Anzahl der verbrauchten Rechenstunden kann je nach Datenvolumen und den verfügbaren Backend-Rechenressourcen zur Verarbeitungszeit variieren. |

Weitere Informationen finden Sie unter [Query Service - Übersicht](../query-service/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B edition bietet umfassende Funktionen für das B2B-Kundendaten-Management, mit denen Unternehmen einheitliche Kundenprofile erstellen, anspruchsvolle B2B-Zielgruppen erstellen und Daten über verschiedene Marketing-Kanäle hinweg aktivieren können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| B2B-Architekturaktualisierung | Experience Platform führt ein Upgrade auf eine neue B2B-Architektur durch, die erhebliche Verbesserungen für Zielgruppen mit mehreren Entitäten mit B2B-Attributen mit sich bringt. Dieses Upgrade konsolidiert die Unterstützung von Zusammenführungsrichtlinien, verbessert die Genauigkeit der Zielgruppenzählung und verbessert die Funktionen zur Entitätsauflösung. |
| Zusammenführungsrichtlinien-Konsolidierung für Audiences mit mehreren Entitäten | Zielgruppen mit mehreren Entitäten mit B2B-Attributen unterstützen jetzt nur noch eine einzige Zusammenführungsrichtlinie, die standardmäßige Zusammenführungsrichtlinie, anstatt mehrere Zusammenführungsrichtlinien zu unterstützen. Diese Änderung sorgt für eine konsistente Zielgruppenkomposition und vereinfacht die Verwaltung der Zusammenführungslogik. |
| Aktualisierungen der Begrenzungen für Konto-Zielgruppen | Konto-Zielgruppen verfügen nicht mehr über die vorherigen Einschränkungen eines 30-tägigen Lookback-Fensters für Erlebnisereignisse, benutzerdefinierte Entitätsbeschränkungen oder Einschränkungen bei der Verwendung `inSegment` Ereignisse. Diese Aktualisierungen bieten mehr Flexibilität bei der Erstellung komplexer B2B-Zielgruppendefinitionen. |
| Verbesserte Anzahl der Zielgruppen für B2B-Entitäten | Schätzungen der Zielgruppengröße für Zielgruppen mit B2B-Entitäten wie Konten und Opportunities sind jetzt exakt, basierend auf den Ergebnissen der Echtzeit-Segmentierung. Diese Verbesserung bietet genauere und zuverlässigere Schätzungen für Zielgruppen mit komplexen B2B-Beziehungen. |
| Konto-Momentaufnahmen für die Zielgruppenzugehörigkeit | Details zur Zielgruppenzugehörigkeit sind jetzt für Kontoentitäten in Schnappschuss-Exporten enthalten, was den Zugriff auf den Zielgruppenstatus, Zeitstempel und Mitgliedschaftsindikatoren auf Kontoebene ermöglicht. Dies führt zu Funktionsgleichheit zwischen Profil- (Person) und Konto-Segmentierungsmodellen. |
| Sandbox-Tooling-Änderungen für Audiences mit mehreren Entitäten | Der Import von Audiences mit mehreren Entitäten mit B2B-Entitäten und Erlebnisereignissen, die vor der Migration exportiert wurden, wird nicht mehr unterstützt. Diese Zielgruppen schlagen bei der Importvalidierung fehl und können nicht automatisch in die neue Architektur konvertiert werden. Zielgruppen müssen nach der Migration erneut exportiert werden, bevor sie in Ziel-Sandboxes importiert werden. |
| Einstellung von B2B-Entitäts-APIs | Die Erstellung einer Zielgruppe über die API für B2B-Entitäten (Konto, Opportunity, Konto-Personen-Beziehung, Opportunity-Personen-Beziehung, Kampagne, Kampagnenmitglied, Marketing-Liste und Marketing-Listenmitglied) wird jetzt nicht mehr unterstützt. Darüber hinaus werden Vorgänge zum Suchen und Löschen von Profilzugriffs-APIs für diese B2B-Entitäten ebenfalls nicht mehr unterstützt. |
| Aktualisierungen des Identity-Namespace für die Entitätsauflösung | Konto- und Opportunity-Entitäten verwenden jetzt die zeitprioritätsbasierte Zusammenführung mit bestimmten Identity-Namespaces (`b2b_account` für Konto, `b2b_opportunity` für Opportunity). Alle anderen Entitäten werden mit primären Identitätsüberschneidungen vereinheitlicht, die durch zeitprioritätsbasiertes Zusammenführen zusammengeführt werden. |

Weitere Informationen finden Sie im Abschnitt [Übersicht über Real-Time CDP B2B edition](../rtcdp/b2b-overview.md).

## Sandboxes {#sandboxes}

Experience Platform wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Änderungen an Audience-Importen mit mehreren Entitäten | Die Sandbox-Tools wurden aktualisiert, um das neue Upgrade der B2B-Architektur zu unterstützen. Audiences mit mehreren Entitäten, die B2B-Entitäten und Erlebnisereignisse enthalten, müssen nach dem Architekturupgrade erneut exportiert werden, bevor sie über Sandbox-Tools in Ziel-Sandboxes importiert werden. Der Import von Versionen vor einem Upgrade schlägt die Validierung fehl. |

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Externe Zielgruppen-API | Sie können die API für externe Zielgruppen verwenden, um extern generierte Zielgruppen programmgesteuert in Adobe Experience Platform zu importieren. |

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Quellen**

| Quelle | Beschreibung |
| --- | --- |
| Unterstützung für [!DNL Didomi] (Streaming-SDK) | Der [!DNL Didomi]-Quell-Connector ermöglicht es Ihnen, Einverständnisverwaltungs-Daten aus der Plattform von [!DNL Didomi] aufzunehmen, wodurch die Einhaltung von Datenschutzbestimmungen und einverständnisbasierte Marketing-Strategien unterstützt wird. |

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für die Änderungsdatenerfassung in ausgewählten Quellen | Sie können jetzt Datenflüsse erstellen, die die Änderungsdatenerfassung für die inkrementelle Aufnahme mithilfe von Quell-Connectoren ermöglichen. Mit dieser Funktion können Kunden den Datentyp für die inkrementelle Aufnahme ändern, die Datenfrische verbessern und den Verarbeitungsaufwand reduzieren. |
| Unterstützung für das weiche Löschen von Datensätzen in [!DNL Salesforce] | Die [!DNL Salesforce]-Quelle unterstützt jetzt die Einbeziehung von vorläufig gelöschten Datensätzen über einen optionalen `includeDeletedObjects`. Bei der Einstellung „true“ können Kunden vorläufig gelöschte Datensätze in ihre [!DNL Salesforce] einbeziehen und in Experience Platform importieren. |

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).
