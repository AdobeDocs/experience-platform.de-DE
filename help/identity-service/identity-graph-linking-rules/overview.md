---
title: Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen
description: Erfahren Sie mehr über die Regeln für die Verknüpfung von Identitätsdiagrammen im Identity-Dienst.
badge: Beta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 67b08acaecb4adf4d30d6d4aa7b8c24b30dfac2e
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 1%

---

# Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen

>[!AVAILABILITY]
>
>Diese Funktion ist noch nicht verfügbar. Das Betaprogramm für Regeln zur Identitätsdiagrammverlinkung wird voraussichtlich im Juli für Entwicklungs-Sandboxes beginnen. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten.

## Inhaltsverzeichnis 

* [Übersicht](./overview.md)
* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Beispielszenarien](./example-scenarios.md)

Mit Adobe Experience Platform Identity Service und Echtzeit-Kundenprofil ist es einfach, davon auszugehen, dass Ihre Daten perfekt erfasst werden und dass alle zusammengeführten Profile eine einzelne Person über eine Personen-ID repräsentieren, z. B. eine CRM-ID. Es gibt jedoch mögliche Szenarien, in denen bestimmte Daten versuchen könnten, mehrere unterschiedliche Profile zu einem einzigen Profil zusammenzuführen (&quot;Diagrammreduzierung&quot;). Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über Identitätsdiagramm-Verknüpfungsregeln bereitgestellt werden, und eine genaue Personalisierung für Ihre Benutzer ermöglichen.

## Beispielszenarien, in denen eine Diagrammreduzierung möglich ist

* **Freigegebenes Gerät**: Freigegebenes Gerät bezieht sich auf Geräte, die von mehr als einer Person verwendet werden. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliothekscomputer und Kiosks.
* **Schlechte E-Mail- und Telefonnummern**: Schlechte E-Mail- und Telefonnummern beziehen sich auf Endbenutzer, die ungültige Kontaktinformationen wie &quot;test&quot;registrieren.<span>@test.com&quot; für E-Mail und &quot;+1-111-111-1111&quot; für Telefonnummer.
* **Fehlerhafte oder falsche Identitätswerte**: Fehlerhafte oder ungültige Identitätswerte beziehen sich auf nicht eindeutige Identitätswerte, die CRM-IDs zusammenführen können. Während IDFAs beispielsweise 36 Zeichen haben müssen (32 alphanumerische Zeichen und vier Bindestriche), gibt es Szenarien, in denen ein IDFA mit dem Identitätswert &quot;user_null&quot;erfasst werden kann. Auf ähnliche Weise unterstützen Telefonnummern nur numerische Zeichen, aber ein Namespace für Smartphones mit dem Identitätswert &quot;nicht angegeben&quot;kann erfasst werden.

Weitere Informationen zu Anwendungsszenarios für Identitätsdiagramm-Verknüpfungsregeln finden Sie im Dokument unter [Beispielszenarien](./example-scenarios.md).

## Verknüpfungsregeln für Identitätsdiagramme {#identity-graph-linking-rules}

Mit den Regeln zur Verknüpfung von Identitätsdiagrammen können Sie:

* Erstellen Sie ein einzelnes Identitätsdiagramm/zusammengeführtes Profil für jeden Benutzer, indem Sie eindeutige Namespaces konfigurieren, was verhindert, dass zwei unterschiedliche Personen-IDs zu einem Identitätsdiagramm zusammengeführt werden.
* Verknüpfen Sie Online-authentifizierte Ereignisse mit der Person, indem Sie Prioritäten konfigurieren.

### Terminologie {#terminology}

| Terminologie | Beschreibung |
| --- | --- |
| Eindeutiger Namespace | Ein eindeutiger Namespace ist ein Identitäts-Namespace, der eingerichtet wurde, um im Kontext eines Identitätsdiagramms getrennt zu sein. Sie können einen Namespace über die Benutzeroberfläche so konfigurieren, dass er eindeutig ist. Sobald ein Namespace als eindeutig definiert wurde, darf ein Diagramm nur eine Identität enthalten, die diesen Namespace enthält. |
| Namespace-Priorität | Namespace-Priorität bezieht sich auf die relative Bedeutung von Namespaces im Vergleich zueinander. Die Namespace-Priorität kann über die Benutzeroberfläche konfiguriert werden. Sie können Namespaces in einem bestimmten Identitätsdiagramm nach Rang ordnen. Nach der Aktivierung wird die Priorität der Namen in verschiedenen Szenarien verwendet, z. B. in der Eingabe für den Identitätsoptimierungsalgorithmus und zur Bestimmung der primären Identität für Erlebnisereignisfragmente. |
| Identitätsoptimierungsalgorithmus | Der Identitätsoptimierungsalgorithmus stellt sicher, dass Richtlinien, die durch die Konfiguration eines eindeutigen Namespace und Namespace-Prioritäten erstellt werden, in einem bestimmten Identitätsdiagramm durchgesetzt werden. |

### Eindeutiger Namespace {#unique-namespace}

Sie können einen Namespace mithilfe des Arbeitsbereichs für die Benutzeroberfläche der Identitätseinstellungen so konfigurieren, dass er eindeutig ist. Informiert den Identitätsoptimierungsalgorithmus dazu, dass ein bestimmtes Diagramm möglicherweise nur eine Identität mit diesem eindeutigen Namespace enthält. Dies verhindert die Zusammenführung zweier unterschiedlicher Personen-IDs innerhalb desselben Diagramms.

Betrachten Sie das folgende Szenario:

* Scott verwendet ein Tablet und öffnet seinen Google Chrome-Browser, um zu nike zu wechseln.<span>.com, wo er sich anmeldet und nach neuen Basketballschuhen sucht.
   * Hinter den Kulissen protokolliert dieses Szenario die folgenden Identitäten:
      * Ein ECID-Namespace und -Wert für die Verwendung des Browsers
      * Ein CRM-ID-Namespace und -Wert für den authentifizierten Benutzer (Scott hat sich mit seiner Kombination aus Benutzername und Kennwort angemeldet).
* Sein Sohn Peter verwendet dann dasselbe Tablet und verwendet auch Google Chrome, um zu nike<span>.com, wo er sich mit seinem eigenen Konto anmeldet, um nach Fußballausrüstung zu suchen.
   * Hinter den Kulissen protokolliert dieses Szenario die folgenden Identitäten:
      * Derselbe ECID-Namespace und -Wert für den Browser.
      * Ein neuer CRM-ID-Namespace und -Wert, der den authentifizierten Benutzer darstellt.

Wenn die CRM-ID als eindeutiger Namespace konfiguriert wurde, teilt der Identitätsoptimierungsalgorithmus die CRM-IDs in zwei separate Identitätsdiagramme auf, anstatt sie zusammenzuführen.

Wenn Sie keinen eindeutigen Namespace konfigurieren, können unerwünschte Diagrammzusammenführungen auftreten, z. B. zwei Identitäten mit demselben CRM-ID-Namespace, aber unterschiedliche Identitätswerte (Szenarien wie diese stellen häufig zwei verschiedene Personen-Entitäten im selben Diagramm dar).

Sie müssen einen eindeutigen Namespace konfigurieren, um den Identitätsoptimierungsalgorithmus darüber zu informieren, dass Einschränkungen bei den Identitätsdaten erzwungen werden, die in ein bestimmtes Identitätsdiagramm aufgenommen werden.

### Namespace-Priorität {#namespace-priority}

Namespace-Priorität bezieht sich auf die relative Bedeutung von Namespaces im Vergleich zueinander. Die Namespace-Priorität kann über die Benutzeroberfläche konfiguriert werden und Sie können Namespaces in einem bestimmten Identitätsdiagramm einordnen.

Eine Methode, bei der Namespace-Priorität verwendet wird, ist die Bestimmung der primären Identität von Erlebnisereignisfragmenten (Benutzerverhalten) im Echtzeit-Kundenprofil. Wenn Prioritätseinstellungen konfiguriert sind, wird die primäre Identitätseinstellung im Web SDK nicht mehr verwendet, um zu bestimmen, welche Profilfragmente gespeichert werden.

Eindeutige Namespaces und Namespace-Prioritäten können im UI-Arbeitsbereich für Identitätseinstellungen konfiguriert werden. Die Auswirkungen ihrer Konfigurationen sind jedoch unterschiedlich:

| | Identity Service | Echtzeit-Kundenprofil |
| --- | --- | --- |
| Eindeutiger Namespace | In Identity Service bezieht sich der Identitätsoptimierungsalgorithmus auf eindeutige Namespaces, um die Identitätsdaten zu bestimmen, die in ein bestimmtes Identitätsdiagramm aufgenommen werden. | Eindeutige Namespaces wirken sich nicht auf das Echtzeit-Kundenprofil aus. |
| Namespace-Priorität | In Identity Service wird bei Diagrammen mit mehreren Ebenen mit Namespace-Priorität bestimmt, dass die entsprechenden Links entfernt werden. | Wenn ein Erlebnisereignis in Profil aufgenommen wird, wird der Namespace mit der höchsten Priorität zur primären Identität des Profilfragments. |

* Die Namespace-Priorität wirkt sich nicht auf das Diagrammverhalten aus, wenn die Grenze von 50 Identitäten pro Diagramm erreicht ist.
* **Namespace-Priorität ist ein numerischer Wert** einem Namespace zugewiesen ist, der seine relative Bedeutung angibt. Dies ist eine Eigenschaft eines Namespace.
* **Primäre Identität ist die Identität, mit der ein Profilfragment gespeichert wird.**. Ein Profilfragment ist ein Datensatz mit Daten, in dem Informationen über einen bestimmten Benutzer gespeichert werden: Attribute (in der Regel über CRM-Datensätze erfasst) oder Ereignisse (in der Regel aus Erlebnisereignissen oder Online-Daten erfasst).
* Die Namespace-Priorität bestimmt die primäre Identität für Experience Event Fragments.
   * Für Profildatensätze können Sie den Arbeitsbereich &quot;Schemas&quot;in der Experience Platform-Benutzeroberfläche verwenden, um Identitätsfelder, einschließlich der primären Identität, zu definieren. Lesen Sie das Handbuch unter [Identitätsfelder in der Benutzeroberfläche definieren](../../xdm/ui/fields/identity.md) für weitere Informationen.

Weitere Informationen finden Sie im Handbuch unter [Namespace-Priorität](./namespace-priority.md).

## Nächste Schritte

Weitere Informationen zu Regeln zur Verknüpfung von Identitätsdiagrammen finden Sie in der folgenden Dokumentation:

* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md).
* [Namespace-Priorität](./namespace-priority.md).
* [Beispielszenarien für die Konfiguration von Regeln für die Zuordnung von Identitätsdiagrammen](./example-scenarios.md).
