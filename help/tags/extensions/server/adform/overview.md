---
keywords: Integration von adform; adform;
title: Adform-Integration für nicht authentifiziertes Retargeting
description: Durch diese Adobe Experience Platform-Integration können Sie Benutzende basierend auf ECID erneut ansprechen.
last-substantial-update: 2025-03-26T00:00:00Z
source-git-commit: 23da6e12b1f5bdc37240d7aa11a44e040b29e3f7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# [!DNL Adform] - Übersicht

Die [[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud)-Erweiterung ermöglicht die Server-seitige Ereignisweiterleitung in Adobe Experience Platform und ermöglicht es Werbetreibenden, Medienagenturen und Publishern, Daten direkt mit dem ID-Fusion-System von Adform zu synchronisieren. Diese Integration ermöglicht es Unternehmen, Zielgruppen über mehrere Kanäle anzusprechen, wodurch die Kampagnenleistung verbessert wird, und bietet maßgeschneiderte Lösungen, um digitale Werbestrategien zu verfeinern und die Effektivität der Anzeigenausgaben zu maximieren.

Im Gegensatz zum herkömmlichen Client-seitigen Tracking macht diese Erweiterung Cookies von Drittanbietern überflüssig, indem Erstanbieter-IDs verwendet werden. Dabei handelt es sich insbesondere um die ECID (Experience Cloud ID), die mit Adform synchronisiert wird. Dies ermöglicht ein nahtloses Zielgruppen-Retargeting, ohne dass eine Client-seitige JavaScript-Bereitstellung erforderlich ist.

In diesem Handbuch wird beschrieben, wie Sie die -Erweiterung installieren, konfigurieren und bereitstellen, um Ereignisse aus den digitalen Eigenschaften einer Marke über Adobes Edge Network an Adform weiterzuleiten und so ein nahtloses Retargeting von Besucherinnen und Besuchern zu ermöglichen.

## Offsite-Retargeting

Durch Offsite-Retargeting können Sie potenzielle Kunden erneut ansprechen, die Ihre Website besucht, aber nicht konvertiert haben. Adform hilft Ihnen, diese Zielgruppen plattformübergreifend zu erreichen, indem es die Markenpräsenz stärkt und die Konversionsmöglichkeiten erhöht. Verwenden Sie diese Integration für Folgendes:

* Erneutes Ansprechen unbekannter Besucher ohne Verwendung von Drittanbieter-Cookies.
* Aktivieren Sie Zielgruppen direkt auf ECIDs, ohne alternative Kennungen von Drittanbieterfirmen-Cookies oder zusätzliche Tags in Ihren digitalen Eigenschaften zu verwenden.

Adform hilft Ihnen bei Folgendem:

* Machen Sie Ihre Erstanbieter-Zielgruppen, die auf ECIDs gekennzeichnet sind, einfach zu adressierbaren IDs für digitale Werbekampagnen.
* Verknüpfen Sie ECIDs mit mehr als 40 angebotspflichtigen ID-Lösungen, um Ihre Reichweite, Häufigkeit und Leistung in Bezug auf Ihre Zielgruppen zu optimieren.

### Server-seitige Zielgruppenaktivierung mit [!DNL Adform] {#server-side-activation}

Im Gegensatz zu herkömmlichen Client-seitigen ID-Bereitstellungen müssen Sie bei dieser Integration die Lösung eines ID-Anbieters nicht in Ihren digitalen Eigenschaften bereitstellen. Stattdessen wird die Server-seitige Zielgruppenaktivierung durch die Verwendung von ECIDs ermöglicht, die bereits mit Adform synchronisiert sind. Zu den wichtigsten Vorteilen gehören:

* **Keine Client-seitige JavaScript-Bereitstellung**: Sie müssen die Client-seitige Besuchererkennungslogik nicht verwalten und Client-seitige IDs nicht in langlebige stabile Versionen entschlüsseln.
* **Nahtlose Zielgruppensynchronisierung**: ECIDs werden dem internen ID-Diagramm von Adform zugeordnet, was ein effizientes Retargeting plattformübergreifend ermöglicht.
* **Verbesserte Reichweite und Deduplizierung**: Das ID-Fusionsdiagramm verbindet ECIDs mit mehreren IDs, um einen hochwertigen Zielgruppenabgleich zu gewährleisten.

## Voraussetzungen {#prerequisites}

Stellen Sie vor der Integration von Adform mit Adobe sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. **Einrichtung von Adobe Web SDK**: Die Adobe Web SDK muss implementiert werden, um die Datenerfassung und Ereignisweiterleitung zu erleichtern.

2. **CDP- oder Verbindungs-SKU**: Sie müssen entweder über die Adobe Customer Data Platform (CDP) Prime- oder Ultimate-SKU oder über die Verbindungs-SKU verfügen, um eine nahtlose Client- und Server-seitige Kommunikation zu ermöglichen.

3. **Adobe Experience Platform Edge Network-Konfiguration**:
   * Stellen Sie sicher, dass der Edge Network für die Unterstützung der Echtzeit-Ereignisweiterleitung für Offsite-Retargeting konfiguriert ist. Weitere Informationen finden Sie [&#x200B; Handbuch „Erste Schritte &#x200B;](https://experienceleague.adobe.com/de/docs/experience-platform/tags/event-forwarding/getting-started) der Ereignisweiterleitung“ von Adobe.
   * Dieser Schritt ist wichtig, um Daten effizient an den Server-seitigen Endpunkt von Adform zu übertragen.

Sobald diese Voraussetzungen erfüllt sind, können Sie mit der Konfiguration und Bereitstellung der [!DNL Adform]-Erweiterung fortfahren.

## [!DNL Adform]-Erweiterung konfigurieren {#configure-adform-extension}

Gehen Sie wie in den folgenden Abschnitten beschrieben vor, um die [!DNL Adform]-Erweiterung zu konfigurieren.

### Installieren und Konfigurieren der Erweiterung

Navigieren Sie in der Benutzeroberfläche der Ereignisweiterleitung zur [!DNL Adform extension] und geben Sie die erforderlichen Werte ein:

| Eingabe | Beschreibung |
| --- | --- |
| Tracking-Setup-ID | Die von Adform für das Tracking von Ereignissen bereitgestellte eindeutige Kennung. |
| Globale Domain | Verwenden Sie `a1.adform.net`, um die Leistung zu optimieren und regionale Latenzprobleme zu vermeiden. |

Speichern Sie die Konfiguration, nachdem Sie diese Details eingegeben haben.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### Tracking-Parameter definieren

Die Aktion „Verfolgen“ ist die primäre Ereignisregel. Sie umfasst Trigger, die auf vordefinierten Aktionen basieren, `page load.` der Regel die folgenden Parameter:

**Erforderliche Parameter:**

| Parameter | Beschreibung |
| --- | --- |
| `Page Name` | Identifiziert die Seite oder Benutzeraktion. |
| `User Agent` | Erfasst Informationen zum Zielgruppen-Abgleich. |
| `IP Address` | Entscheidend für genaues Targeting und Retargeting. |

**Empfohlene Parameter:**

| Parameter | Beschreibung |
| --- | --- |
| `Page URL` | Identifiziert die Seite oder Benutzeraktion. |
| `Referral URL` | Erfasst Informationen zum Zielgruppen-Abgleich. |
| `ECID` | Entscheidend für genaues Targeting und Retargeting. |
| `Source Domain` | Entscheidend für genaues Targeting und Retargeting. |

<!-- ![Tracking parameters for Adform]() -->

### Regel anfügen

Die Erweiterung muss an eine Regel angehängt sein, damit sie ordnungsgemäß funktioniert. Wenn keine Bedingungen festgelegt sind, erstellen Sie eine globale Regel, um sicherzustellen, dass sie immer ausgeführt wird.

>[!NOTE]
>
>Wenn die Erweiterung nicht ausgelöst wird, stellen Sie sicher, dass sie an eine gültige Regel in der Adobe Experience Platform-Datenerfassung angehängt ist.

<!-- ![Attach a rule to the Adform extension]() -->

## Validieren und Bereitstellen

Stellen Sie sicher, dass die Erweiterung korrekt installiert und konfiguriert ist und dass alle erforderlichen Datenelemente zugeordnet werden, einschließlich:
* [ECID](/help/identity-service/features/ecid.md)
* Seitenname
* Verweis-URL
* Benutzeragent
* IP-Adresse

Nachdem Sie alle erforderlichen Felder eingegeben und den Test abgeschlossen haben, wählen Sie **Erstellen** aus, um die Erweiterung bereitzustellen.

## Nächste Schritte

Sie sollten jetzt wissen, wie Adform mit den Server-seitigen Funktionen von Adobe integriert wird, und die Machbarkeit der Integration in Ihre bestehende Infrastruktur bewerten. Weitere Informationen finden Sie in [offiziellen Dokumentation von Adform](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud).