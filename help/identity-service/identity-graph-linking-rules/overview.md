---
title: Verknüpfungsregeln für Identitätsdiagramme
description: Erfahren Sie mehr über die Regeln zur Verknüpfung von Identitätsdiagrammen im Identity Service.
badge: Beta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: a4e5ab14904fe17aa8bab2f8555ae6d535c856e8
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 2%

---

# Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen

>[!AVAILABILITY]
>
>Die Regeln zur Verknüpfung von Identitätsdiagrammen befinden sich derzeit in der Beta-Phase. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten. Die Funktion und die Dokumentation können sich ändern.

Mit Adobe Experience Platform Identity Service und Echtzeit-Kundenprofil ist es einfach, davon auszugehen, dass Ihre Daten perfekt erfasst werden und dass alle zusammengeführten Profile eine einzelne Person über eine Personen-ID darstellen, z. B. eine CRMID. Es gibt jedoch mögliche Szenarien, in denen bestimmte Daten versuchen könnten, mehrere unterschiedliche Profile zu einem einzigen Profil zusammenzuführen (&quot;Diagrammreduzierung&quot;). Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über Identitätsdiagramm-Verknüpfungsregeln bereitgestellt werden, und eine genaue Personalisierung für Ihre Benutzer ermöglichen.

## Erste Schritte

Die folgenden Dokumente sind für das Verständnis der Regeln für die Zuordnung von Identitätsdiagrammen unerlässlich.

* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche der Diagrammsimulation](./graph-simulation.md)
* [Benutzeroberfläche für Identitätseinstellungen](./identity-settings-ui.md)

## Beispielszenarien, in denen eine Diagrammreduzierung möglich ist {#example-scenarios-where-graph-collapse-could-happen}

In diesem Abschnitt werden Beispielszenarien beschrieben, die Sie bei der Konfiguration von Regeln für die Verknüpfung von Identitätsdiagrammen berücksichtigen können.

### Freigegebenes Gerät

Es gibt Fälle, in denen mehrere Anmeldungen auf einem einzelnen Gerät stattfinden können:

| Freigegebenes Gerät | Beschreibung |
| --- | --- |
| Familiencomputer und Tablets | Sowohl Ehemann als auch Ehefrau melden sich auf ihren jeweiligen Bankkonten an. |
| Öffentlicher Kiosk | Reisende an einem Flughafen, die sich mit ihrer Treuekennung anmelden, können Taschen und Bordkarten einchecken. |
| Callcenter | Die Mitarbeiter des Callcenters melden sich auf einem einzelnen Gerät im Namen von Kunden an, die den Kundensupport aufrufen, um Probleme zu lösen. |

![Ein Diagramm einiger gemeinsamer Geräte.](../images/identity-settings/shared-devices.png)

In diesen Fällen wird aus Diagrammsicht eine einzelne ECID mit mehreren CRMIDs verknüpft, ohne dass Einschränkungen aktiviert sind.

Mit den Verknüpfungsregeln für Identitätsdiagramme können Sie:

* Konfigurieren Sie die für die Anmeldung verwendete ID als eindeutige Kennung. Sie können beispielsweise ein Diagramm so einschränken, dass nur eine Identität mit einem CRMID-Namespace gespeichert wird, und so diese CRMID als eindeutige Kennung eines gemeinsam genutzten Geräts definieren.
   * Dadurch können Sie sicherstellen, dass CRMIDs nicht von der ECID zusammengeführt werden.

### Ungültige E-Mail-/Telefonszenarien

Es gibt auch Fälle von Benutzern, die bei der Registrierung falsche Werte als Telefonnummern und/oder E-Mail-Adressen angeben. Wenn in diesen Fällen Beschränkungen nicht aktiviert sind, werden telefonische/E-Mail-bezogene Identitäten letztendlich mit mehreren verschiedenen CRMIDs verknüpft.

![Ein Diagramm, das ungültige E-Mail- oder Telefonszenarien darstellt.](../images/identity-settings/invalid-email-phone.png)

Mit den Verknüpfungsregeln für Identitätsdiagramme können Sie:

* Konfigurieren Sie entweder die CRMID, Telefonnummer oder E-Mail-Adresse als eindeutige Kennung und beschränken Sie so eine Person auf nur eine CRMID, Telefonnummer und/oder E-Mail-Adresse, die mit ihrem Konto verknüpft ist.

### Fehlerhafte oder falsche Identitätswerte

Es gibt Fälle, in denen nicht eindeutige, fehlerhafte Identitätswerte im System erfasst werden, unabhängig vom Namespace. Zu den Beispielen gehören:

* IDFA-Namespace mit dem Identitätswert &quot;user_null&quot;.
   * IDFA-Identitätswerte sollten 36 Zeichen enthalten: 32 alphanumerische Zeichen und vier Bindestriche.
* Namespace für Telefonnummern mit dem Identitätswert &quot;Nicht angegeben&quot;.
   * Telefonnummern dürfen keine Buchstaben enthalten.

Diese Identitäten können zu den folgenden Diagrammen führen, in denen mehrere CRMIDs mit der &quot;schlechten&quot;Identität zusammengeführt werden:

![Ein Diagrammbeispiel für Identitätsdaten mit fehlerhaften oder falschen Identitätswerten.](../images/identity-settings/bad-data.png)

Mit Regeln zur Verknüpfung von Identitätsdiagrammen können Sie die CRMID als eindeutige Kennung konfigurieren, um unerwünschte Profilzusammenbrüche aufgrund dieses Datentyps zu verhindern.

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

* Scott verwendet ein Tablet und öffnet seinen Google Chrome-Browser, um zu nike<span>.com zu gehen, wo er sich anmeldet und nach neuen Basketballschuhen sucht.
   * Hinter den Kulissen protokolliert dieses Szenario die folgenden Identitäten:
      * Ein ECID-Namespace und -Wert für die Verwendung des Browsers
      * Ein CRMID-Namespace und -Wert für den authentifizierten Benutzer (Scott hat sich mit seiner Kombination aus Benutzername und Kennwort angemeldet).
* Sein Sohn Peter benutzt dann das gleiche Tablet und verwendet auch Google Chrome, um zu nike<span>.com zu gehen, wo er sich mit seinem eigenen Konto anmeldet, um nach Fußballausrüstung zu suchen.
   * Hinter den Kulissen protokolliert dieses Szenario die folgenden Identitäten:
      * Derselbe ECID-Namespace und -Wert für den Browser.
      * Ein neuer CRMID-Namespace und -Wert, der den authentifizierten Benutzer darstellt.

Wenn CRMID als eindeutiger Namespace konfiguriert wurde, teilt der Identitätsoptimierungsalgorithmus die CRMIDs in zwei separate Identitätsdiagramme auf, anstatt sie zusammenzuführen.

Wenn Sie keinen eindeutigen Namespace konfigurieren, können unerwünschte Diagrammzusammenführungen auftreten, z. B. zwei Identitäten mit demselben CRMID-Namespace, aber unterschiedliche Identitätswerte (Szenarien wie diese stellen häufig zwei verschiedene Entitäten im selben Diagramm dar).

Sie müssen einen eindeutigen Namespace konfigurieren, um den Identitätsoptimierungsalgorithmus darüber zu informieren, dass Einschränkungen bei den Identitätsdaten erzwungen werden, die in ein bestimmtes Identitätsdiagramm aufgenommen werden.

### Namespace-Priorität {#namespace-priority}

Namespace-Priorität bezieht sich auf die relative Bedeutung von Namespaces im Vergleich zueinander. Die Namespace-Priorität kann über die Benutzeroberfläche konfiguriert werden und Sie können Namespaces in einem bestimmten Identitätsdiagramm einordnen.

Eine Möglichkeit, wie Namespace-Priorität verwendet wird, besteht darin, die primäre Identität von Erlebnisereignisfragmenten (Benutzerverhalten) im Echtzeit-Kundenprofil zu bestimmen. Wenn Prioritätseinstellungen konfiguriert sind, wird die primäre Identitätseinstellung im Web SDK nicht mehr verwendet, um zu bestimmen, welche Profilfragmente gespeichert werden.

Eindeutige Namespaces und Namespace-Prioritäten können im UI-Arbeitsbereich für Identitätseinstellungen konfiguriert werden. Die Auswirkungen ihrer Konfigurationen sind jedoch unterschiedlich:

| | Identity Service | Echtzeit-Kundenprofil |
| --- | --- | --- |
| Eindeutiger Namespace | In Identity Service bezieht sich der Identitätsoptimierungsalgorithmus auf eindeutige Namespaces, um die Identitätsdaten zu bestimmen, die in ein bestimmtes Identitätsdiagramm aufgenommen werden. | Eindeutige Namespaces wirken sich nicht auf das Echtzeit-Kundenprofil aus. |
| Namespace-Priorität | In Identity Service wird bei Diagrammen mit mehreren Ebenen mit Namespace-Priorität bestimmt, dass die entsprechenden Links entfernt werden. | Wenn ein Erlebnisereignis in Profil aufgenommen wird, wird der Namespace mit der höchsten Priorität zur primären Identität des Profilfragments. |

* Die Namespace-Priorität wirkt sich nicht auf das Diagrammverhalten aus, wenn die Grenze von 50 Identitäten pro Diagramm erreicht ist.
* **Namespace-Priorität ist ein numerischer Wert**, der einem Namespace zugewiesen ist und dessen relative Bedeutung angibt. Dies ist eine Eigenschaft eines Namespace.
* **Primäre Identität ist die Identität, in der ein Profilfragment für** gespeichert wird. Ein Profilfragment ist ein Datensatz mit Daten, in dem Informationen über einen bestimmten Benutzer gespeichert werden: Attribute (in der Regel über CRM-Datensätze erfasst) oder Ereignisse (in der Regel aus Erlebnisereignissen oder Online-Daten erfasst).
* Die Namespace-Priorität bestimmt die primäre Identität für Experience Event Fragments.
   * Für Profildatensätze können Sie den Arbeitsbereich &quot;Schemas&quot;in der Experience Platform-Benutzeroberfläche verwenden, um Identitätsfelder, einschließlich der primären Identität, zu definieren. Weitere Informationen finden Sie im Handbuch zum Definieren von Identitätsfeldern in der Benutzeroberfläche ](../../xdm/ui/fields/identity.md) .[
* Wenn ein Erlebnisereignis in der identityMap zwei oder mehr Identitäten mit der höchsten Namespace-Priorität aufweist, wird es von der Erfassung ausgeschlossen, da es als &quot;schlechte Daten&quot;gilt. Wenn die identityMap beispielsweise `{ECID: 111, CRMID: John, CRMID: Jane}` enthält, wird das gesamte Ereignis als ungültige Daten zurückgewiesen, da dies bedeutet, dass das Ereignis sowohl `CRMID: John` als auch `CRMID: Jane` gleichzeitig zugeordnet ist.

Weitere Informationen finden Sie im Handbuch zu [Namespace-Priorität](./namespace-priority.md).

## Nächste Schritte

Weitere Informationen zu Regeln zur Verknüpfung von Identitätsdiagrammen finden Sie in der folgenden Dokumentation:

* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche der Diagrammsimulation](./graph-simulation.md)
* [Benutzeroberfläche für Identitätseinstellungen](./identity-settings-ui.md)