---
title: Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen
description: Erfahren Sie mehr über die Regeln für die Verknüpfung von Identitätsdiagrammen im Identity-Dienst.
hide: true
hidefromtoc: true
badge: Alpha
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: f21b5519440f7ffd272361954c9e32ccca2ec2bc
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen

>[!IMPORTANT]
>
>Verknüpfungsregeln für Identitätsdiagramme befinden sich derzeit im Alpha. Die Funktion und die Dokumentation können sich ändern.

## Inhaltsverzeichnis 

* [Übersicht](./overview.md)
* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Beispielszenarien](./example-scenarios.md)

Mit Adobe Experience Platform Identity Service und Echtzeit-Kundenprofil ist es einfach, davon auszugehen, dass Ihre Daten perfekt erfasst werden und dass alle zusammengeführten Profile eine einzelne Person über eine Personen-ID repräsentieren, z. B. eine CRM-ID. Es gibt jedoch mögliche Szenarien, in denen bestimmte Daten versuchen könnten, mehrere unterschiedliche Profile zu einem einzigen Profil zusammenzuführen (&quot;Profil-Kollaps&quot;). Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über Identitätsdiagramm-Verknüpfungsregeln bereitgestellt werden, und eine genaue Personalisierung für Ihre Benutzer ermöglichen.

## Beispielszenarien, in denen ein Profil-Kollaps auftreten kann

* **Freigegebenes Gerät**: Freigegebenes Gerät bezieht sich auf Geräte, die von mehr als einer Person verwendet werden. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliothekscomputer und Kiosks.
* **Schlechte E-Mail- und Telefonnummern**: Schlechte E-Mail- und Telefonnummern beziehen sich auf Endbenutzer, die ungültige Kontaktinformationen wie &quot;test&quot;registrieren.<span>@test.com&quot; für E-Mail und &quot;+1-111-111-1111&quot; für Telefonnummer.
* **Fehlerhafte oder falsche Identitätswerte**: Fehlerhafte oder ungültige Identitätswerte beziehen sich auf nicht eindeutige Identitätswerte, die CRM-IDs zusammenführen können. Während IDFAs beispielsweise 36 Zeichen haben müssen (32 alphanumerische Zeichen und vier Bindestriche), gibt es Szenarien, in denen ein IDFA mit dem Identitätswert &quot;user_null&quot;erfasst werden kann. Auf ähnliche Weise unterstützen Telefonnummern nur numerische Zeichen, aber ein Namespace für Smartphones mit dem Identitätswert &quot;nicht angegeben&quot;kann erfasst werden.

Weitere Informationen zu Anwendungsszenarios für Identitätsdiagramm-Verknüpfungsregeln finden Sie im Dokument unter [Beispielszenarien](./example-scenarios.md).

## Ziele für die Verknüpfung von Identitätsdiagrammen

Mit den Regeln zur Verknüpfung von Identitätsdiagrammen können Sie:

* Erstellen Sie ein einzelnes Identitätsdiagramm/zusammengeführtes Profil für jeden Benutzer, indem Sie eindeutige Namespaces (Beschränkungen) konfigurieren. Dadurch wird verhindert, dass zwei unterschiedliche Personen-IDs zu einem Identitätsdiagramm zusammengeführt werden.
* Verknüpfen Sie Online-authentifizierte Ereignisse mit der Person, indem Sie Prioritäten konfigurieren.

### Beschränkungen

Ein eindeutiger Namespace ist eine Kennung, die eine Person darstellt, z. B. CRM-ID, Anmelde-ID und Hash-E-Mail. Wenn ein Namespace als eindeutig gekennzeichnet ist, darf ein Diagramm nur eine Identität mit diesem Namespace (`limit=1`). Dadurch wird verhindert, dass zwei unterschiedliche Personen-IDs innerhalb desselben Diagramms zusammengeführt werden.

* Wenn keine Begrenzung konfiguriert ist, kann dies zu unerwünschten Diagrammzusammenführungen führen, z. B. zu zwei Identitäten mit einem CRM-ID-Namespace in einem Diagramm.
* Wenn keine Begrenzung konfiguriert ist, kann das Diagramm so viele Namespaces wie nötig hinzufügen, solange sich das Diagramm innerhalb der Limits befindet (50 Identitäten/Diagramm).
* Wenn ein Limit konfiguriert ist, stellt der Identitätsoptimierungsalgorithmus sicher, dass die Begrenzung erzwungen wird.

### Identitätsoptimierungsalgorithmus

Der Identitätsoptimierungsalgorithmus ist eine Regel, die sicherstellt, dass die Beschränkungen durchgesetzt werden. Der Algorithmus berücksichtigt die neuesten Links und entfernt die ältesten Links, um sicherzustellen, dass ein bestimmtes Diagramm innerhalb der von Ihnen definierten Grenzen bleibt.

Im Folgenden finden Sie eine Liste der Auswirkungen des Algorithmus auf die Zuordnung anonymer Ereignisse zu bekannten Kennungen:

* Die ECID wird dem zuletzt authentifizierten Benutzer zugeordnet, wenn die folgenden Bedingungen erfüllt sind:
   * Wenn CRM-IDs durch ECID (freigegebenes Gerät) zusammengeführt werden.
   * Wenn Begrenzungen auf nur eine CRM-ID konfiguriert sind.

Weitere Informationen finden Sie im Dokument unter [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md).

### Priorität

>[!IMPORTANT]
>
>Namespace-Prioritäten sind derzeit nicht für Alpha verfügbar.

Sie können die Namespace-Priorität verwenden, um zu definieren, welche Namespaces wichtiger sind als andere. Die Priorität, die Sie für Ihre Namespaces festlegen, wird dann zur Definition von primären Identitäten verwendet. Dies ist die Identität, die Profilfragmente (Attribut- und Ereignisdaten) im Echtzeit-Kundenprofil speichert. Wenn Prioritätseinstellungen konfiguriert sind, wird die primäre Identitätseinstellung im Web SDK nicht mehr verwendet, um zu bestimmen, welche Profilfragmente gespeichert werden.

* Einschränkungen und Priorität sind unabhängige Konfigurationen und tun **not** beeinflussen sich gegenseitig:
   * Beschränkungen sind eine Identitätsdiagrammkonfiguration im Identity Service.
   * Die Priorität ist eine Profilfragmentkonfiguration im Echtzeit-Kundenprofil.
   * Priorität **not** die Limits des Identitätsdiagramms beeinflussen.
* **Namespace-Priorität ist ein numerischer Wert** einem Namespace zugewiesen ist, der seine relative Bedeutung angibt. Dies ist eine Eigenschaft eines Namespace.
* **Primäre Identität ist die Identität, mit der ein Profilfragment gespeichert wird.**. Ein Profilfragment ist ein Datensatz mit Daten, in dem Informationen über einen bestimmten Benutzer gespeichert werden: Attribute (in der Regel über CRM-Datensätze erfasst) oder Ereignisse (in der Regel aus Erlebnisereignissen oder Online-Daten erfasst).
* Die Namespace-Priorität bestimmt die primäre Identität für Erlebnisereignisse.
   * Für Profildatensätze können Sie den Arbeitsbereich &quot;Schemas&quot;in der Experience Platform-Benutzeroberfläche verwenden, um Identitätsfelder, einschließlich der primären Identität, zu definieren. Lesen Sie das Handbuch unter [Identitätsfelder in der Benutzeroberfläche definieren](../../xdm/ui/fields/identity.md) für weitere Informationen.

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

* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Beispielszenarien für die Konfiguration von Regeln für die Zuordnung von Identitätsdiagrammen](./example-scenarios.md)
