---
title: Adobe Experience Platform – Versionshinweise März 2023
description: Versionshinweise März 2023 für Adobe Experience Platform.
source-git-commit: 48cd7f670ab7d42d2b0c54bb549d37aa3b9ebe66
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 42%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 29. März 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [Datenvorbereitung](#data-prep)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neuer Schnellstart-Workflow für die Meta Conversions-API (Beta) | Greifen Sie über den Startseite der Datenerfassung auf neue Schnellstartarbeitsabläufe unter &quot;Erste Schritte&quot;zu! Die [Schnellstart-Workflow für die Meta Conversions-API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) ermöglicht Kunden die schnelle Erfassung und Weiterleitung von Ereignisdaten, serverseitig zu Meta für Anzeigenkonversionen in nur wenigen einfachen Schritten. |
| Neuer Schnellstart-Workflow für Mobile SDK (Beta) | Greifen Sie über den Startseite der Datenerfassung auf neue Schnellstartarbeitsabläufe unter &quot;Erste Schritte&quot;zu! Die [Schnellstartarbeitsablauf für das Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) ermöglicht Ihnen die schnelle Implementierung des Mobile SDK und die Validierung einfacher mobiler Ereignisse in nur wenigen einfachen Schritten. |
| [!DNL Braze] Ereignisweiterleitungs-Erweiterung | Die [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Mit der Ereignisweiterleitungs-Erweiterung können Sie die im Adobe Experience Platform Edge Network erfassten Daten nutzen und an senden. [!DNL Braze] in Form von serverseitigen Ereignissen, bei denen die [!DNL Braze] APIs für die Benutzerverfolgung. |
| [!DNL Mixpanel] Ereignisweiterleitungs-Erweiterung | Die [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) -Erweiterung ermöglicht es Kunden, die Ereignisweiterleitung zu nutzen, um Ereignisinformationen im Adobe Experience Platform Edge Network zu erfassen und über die Track Events-API an Mixpanel zu senden. |

{style="table-layout:auto"}

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Funktionen für die Kodierung und Dekodierung von URL-Zeichenfolgen | <ul><li>Die `get_url_encoded` -Funktion verwendet eine URL als Eingabe und ersetzt oder kodiert Sonderzeichen durch ASCII-Zeichen.</li><li>Die `get_url_decoded` nimmt eine URL als Eingabe und dekodiert ASCII-Zeichen in Sonderzeichen.</li></ul> Weitere Informationen finden Sie im Abschnitt [Handbuch zu Datenvorbereitung-Funktionen](../../data-prep/functions.md). Eine umfassende Liste der reservierten Zeichen und der zugehörigen kodierten Zeichen finden Sie im Handbuch unter [Sonderzeichen](../../data-prep/functions.md#special-characters). |

Weitere Informationen zur Datenvorbereitung finden Sie im [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Profilmetriken | Um eine genauere Darstellung der Profilmetriken zu erhalten, werden Mitgliedschaftsaufschlüsselungen und Abwanderungsmetriken kombiniert und jetzt über einen Zeitraum von 24 Stunden berechnet. Weitere Informationen finden Sie unter [Handbuch zur Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md) |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verfügbarkeit der Betaversion von [!DNL Chatlio] | Die [!DNL Chatlio] -Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Chatlio] Quelle zum Streamen Ihrer [!DNL Chatlio] Ereignisdaten in Experience Platform. Weitere Informationen finden Sie im [[!DNL Chatlio] Überblick](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Verfügbarkeit der Betaversion von [!DNL Customer.io] | Die [!DNL Customer.io] -Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Customer.io] -Quelle, um Ihre Kundenereignisdaten an Experience Platform zu streamen. Weitere Informationen finden Sie im [[!DNL Customer.io] Überblick](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Verfügbarkeit der Betaversion von [!DNL Pendo] | Die [!DNL Pendo] -Quelle ist jetzt in der Beta-Version verfügbar. Verwenden Sie die [!DNL Pendo] -Quelle, um Ihre Produktanalysedaten an Experience Platform zu streamen. Weitere Informationen finden Sie im [[!DNL Pendo] Überblick](../../sources/connectors/analytics/pendo-webhook.md). |
| Unterstützung für Datenflussentwürfe | Sie können jetzt die Flow Service-API verwenden, um Ihre Datenflüsse auf den Entwurfsstatus festzulegen. Entworfene Datenflüsse können später aktualisiert und mit neuen Informationen veröffentlicht werden. Weitere Informationen finden Sie im Handbuch unter [Festlegen der Datenflüsse für Quellen als Entwürfe](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
