---
title: Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen
description: Erfahren Sie mehr über die Regeln für die Verknüpfung von Identitätsdiagrammen im Identity-Dienst.
hide: true
hidefromtoc: true
badge: Alpha
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen

>[!IMPORTANT]
>
>Verknüpfungsregeln für Identitätsdiagramme befinden sich derzeit im Alpha. Die Funktion und die Dokumentation können sich ändern.

## Inhaltsverzeichnis 

* [Übersicht](./overview.md)
* [Beispielszenarien](./example-scenarios.md)
* [Identity Service und Echtzeit-Kundenprofil](identity-and-profile.md)
* [Identitätsverknüpfungslogik](./identity-linking-logic.md)

Mit Adobe Experience Platform Identity Service und Echtzeit-Kundenprofil ist es einfach, davon auszugehen, dass Ihre Daten perfekt erfasst werden und dass alle zusammengeführten Profile eine einzelne Person über eine Personen-ID repräsentieren, z. B. eine CRM-ID. Es gibt jedoch mögliche Szenarien, in denen bestimmte Daten versuchen könnten, mehrere unterschiedliche Profile zu einem einzigen Profil zusammenzuführen (&quot;Profil-Kollaps&quot;). Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über Identitätsdiagramm-Verknüpfungsregeln bereitgestellt werden, und eine genaue Personalisierung für Ihre Benutzer ermöglichen.

## Beispielszenarien, in denen ein Profil-Kollaps auftreten kann

* **Freigegebenes Gerät**: Freigegebenes Gerät bezieht sich auf Geräte, die von mehr als einer Person verwendet werden. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliothekscomputer und Kiosks.
* **Schlechte E-Mail- und Telefonnummern**: Schlechte E-Mail- und Telefonnummern beziehen sich auf Endbenutzer, die ungültige Kontaktinformationen wie &quot;test&quot;registrieren.<span>@test.com&quot; für E-Mail und &quot;+1-111-111-1111&quot; für Telefonnummer.
* **Fehlerhafte oder falsche Identitätswerte**: Fehlerhafte oder ungültige Identitätswerte beziehen sich auf nicht eindeutige Identitätswerte, die CRM-IDs zusammenführen können. Während IDFAs beispielsweise 36 Zeichen haben müssen (32 alphanumerische Zeichen und vier Bindestriche), gibt es Szenarien, in denen ein IDFA mit dem Identitätswert &quot;user_null&quot;erfasst werden kann. Auf ähnliche Weise unterstützen Telefonnummern nur numerische Zeichen, aber ein Namespace für Smartphones mit dem Identitätswert &quot;nicht angegeben&quot;kann erfasst werden.

Weitere Informationen zu Anwendungsszenarios für Identitätsdiagramm-Verknüpfungsregeln finden Sie im Dokument unter [Beispielszenarien](./example-scenarios.md).

## Ziele für die Verknüpfung von Identitätsdiagrammen

Mit den Regeln zur Verknüpfung von Identitätsdiagrammen können Sie:

* Konfigurieren Sie Beschränkungen, um zu verhindern, dass zwei unterschiedliche Personen-IDs zu einem Identitätsdiagramm zusammengeführt werden, sodass ein einzelnes Identitätsdiagramm nur eine Person darstellt.
   * Die von Ihnen konfigurierten Beschränkungen werden dann vom Identitätsoptimierungsalgorithmus erzwungen.
* Konfigurieren Sie Prioritäten, um Online-Ereignisse zu verknüpfen, die von der authentifizierten Person an einen bestimmten Benutzer durchgeführt werden.

### Beschränkungen

Sie können Namespace-Beschränkungen verwenden, um die maximale Anzahl von Identitäten zu definieren, die in einem Diagramm basierend auf einem bestimmten Namespace vorhanden sein können. Sie können beispielsweise festlegen, dass Ihr Diagramm maximal eine Identität mit einem CRM-ID-Namespace enthält, wodurch die Zusammenführung von zwei unterschiedlichen Personen-IDs innerhalb desselben Diagramms verhindert wird.

* Wenn keine Begrenzung konfiguriert ist, kann dies zu unerwünschten Diagrammzusammenführungen führen, z. B. zu zwei Identitäten mit einem CRM-ID-Namespace in einem Diagramm.
* Wenn keine Begrenzung konfiguriert ist, kann das Diagramm so viele Namespaces wie nötig hinzufügen, solange sich das Diagramm innerhalb der Limits befindet (50 Identitäten/Diagramm).
* Wenn ein Limit konfiguriert ist, stellt der Identitätsoptimierungsalgorithmus sicher, dass die Begrenzung erzwungen wird.

### Identitätsoptimierungsalgorithmus

Der Identitätsoptimierungsalgorithmus ist eine Regel, die sicherstellt, dass die Beschränkungen durchgesetzt werden. Der Algorithmus berücksichtigt die neuesten Links und entfernt die ältesten Links, um sicherzustellen, dass ein bestimmtes Diagramm innerhalb der von Ihnen definierten Grenzen bleibt.

Im Folgenden finden Sie eine Liste der Auswirkungen des Algorithmus auf die Zuordnung anonymer Ereignisse zu bekannten Kennungen:

* Die ECID wird dem zuletzt authentifizierten Benutzer zugeordnet, wenn die folgenden Bedingungen erfüllt sind:
   * Wenn CRM-IDs durch ECID (freigegebenes Gerät) zusammengeführt werden.
   * Wenn Begrenzungen auf nur eine CRM-ID konfiguriert sind.

### Priorität

>[!IMPORTANT]
>
>Namespace-Prioritäten sind derzeit nicht für Alpha verfügbar.

Sie können die Namespace-Priorität verwenden, um zu definieren, welche Namespaces wichtiger sind als andere. Die Hierarchie, die Sie für Ihre Namespaces festlegen, wird dann zum Definieren von primären Identitäten und zum Speichern von Profilfragmenten verwendet. Wenn Prioritätseinstellungen konfiguriert sind, wird die primäre Identitätseinstellung im Web SDK nicht mehr verwendet, um zu bestimmen, welche Profilfragmente gespeichert werden.

* Einschränkungen und Priorität sind unabhängige Konfigurationen und tun **not** beeinflussen sich gegenseitig:
   * Beschränkungen sind eine Identitätsdiagrammkonfiguration im Identity Service.
   * Die Priorität ist eine Profilfragmentkonfiguration im Echtzeit-Kundenprofil.
   * Priorität **not** die Limits des Identitätsdiagramms beeinflussen.

>[!BEGINSHADEBOX]

**Beispiel für Namespace-Priorität**

Angenommen, Sie haben die folgende Priorität für Ihre Namespaces konfiguriert:

1. CRM-ID: Stellt einen Benutzer dar.
2. IDFA: Stellt ein Apple-Hardwaregerät dar, z. B. eine iPhone und iPad.
3. GAID: Stellt ein Google-Hardwaregerät dar, z. B. Google Pixel.
4. ECID: Stellt einen Webbrowser dar, z. B. Firefox, Safari und Chrome.
5. AAID: Stellt einen Webbrowser dar.
Wenn ECID und AAID gleichzeitig gesendet werden, stellen beide Identitäten denselben Webbrowser (Duplikat) dar.

Wenn die folgenden Erlebnisereignisse in Experience Platform aufgenommen werden, werden die Profilfragmente dann mit der höheren Priorität im Namespace gespeichert.

**Authentifizierte Ereignisse:**

* Wenn die Identitätszuordnung eine ECID, eine GAID und eine CRM-ID enthält, werden die Ereignisinformationen anhand der CRM-ID (primäre Identität) gespeichert.
   * GAID steht für ein Google-Hardwaregerät (z. B. Google Pixel), ECID für einen Webbrowser (z. B. Google Chrome) und CRM-ID für einen authentifizierten Benutzer.
   * Wenn die Identitätszuordnung eine CRM-ID, eine ECID und eine AAID enthält, werden die Ereignisinformationen anhand der CRM-ID (primäre Identität) gespeichert.

**Nicht authentifizierte Ereignisse:**

* Wenn die Identitätszuordnung eine ECID, IDFA und AAID enthält, werden die Ereignisinformationen gegen den IDFA (primäre Identität) gespeichert.
   * IDFA stellt ein Apple-Hardwaregerät (z. B. iPhone) dar, ECID und AAID stellen beide einen Webbrowser (Safari) dar.

>[!ENDSHADEBOX]

## Nächste Schritte

Weitere Informationen zu Regeln zur Verknüpfung von Identitätsdiagrammen finden Sie in der folgenden Dokumentation:

* [Beispielszenarien für die Konfiguration von Regeln für die Zuordnung von Identitätsdiagrammen](./example-scenarios.md)
* [Identity Service und Echtzeit-Kundenprofil](identity-and-profile.md)
* [Identitätsverknüpfungslogik](./identity-linking-logic.md)
