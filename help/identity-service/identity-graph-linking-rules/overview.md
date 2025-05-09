---
title: Verknüpfungsregeln für Identitätsdiagramme
description: Erfahren Sie mehr über die Verknüpfungsregeln für Identitätsdiagramme in Identity Service.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: a309f0dca5ebe75fcb7abfeb98605aec2692324d
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 7%

---

# [!DNL Identity Graph Linking Rules] – Übersicht {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="Verknüpfungsregeln für Identitätsdiagramme"
>abstract="Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über die Verknüpfungsregeln für Identitätsdiagramme bereitgestellt werden, und präzisere Personalisierung für Ihre Benutzenden ermöglichen."

>[!AVAILABILITY]
>
>Regeln zur Identitätsdiagramm-Verknüpfung sind derzeit nur eingeschränkt verfügbar und können von allen Kunden in Entwicklungs-Sandboxes aufgerufen werden.
>
>* **Aktivierungsanforderungen**: Die Funktion bleibt inaktiv, bis Sie Ihre [!DNL Identity Settings] konfigurieren und speichern. Ohne diese Konfiguration funktioniert das System weiterhin normal, ohne dass sich das Verhalten ändert.
>* **Wichtige Hinweise**: Während dieser eingeschränkten Verfügbarkeitsphase kann die Segmentierung nach Edge zu unerwarteten Segmentzugehörigkeitsergebnissen führen. Streaming und Batch-Segmentierung funktionieren jedoch erwartungsgemäß.
>* **Nächste Schritte**: Informationen zum Aktivieren dieser Funktion in Produktions-Sandboxes erhalten Sie von Ihrem Adobe-Account-Team.

Mit Adobe Experience Platform Identity Service und dem Echtzeit-Kundenprofil ist es einfach anzunehmen, dass Ihre Daten perfekt aufgenommen werden und dass alle zusammengeführten Profile über eine Personenkennung, wie z. B. eine CRMID, eine einzelne Person darstellen. Es gibt jedoch mögliche Szenarien, in denen bestimmte Daten versuchen könnten, mehrere unterschiedliche Profile zu einem einzigen Profil zusammenzuführen („Diagrammausblendung„). Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über [!DNL Identity Graph Linking Rules] bereitgestellt werden, und eine genaue Personalisierung für Ihre Benutzerinnen und Benutzer ermöglichen.

Sehen Sie sich das folgende Video an, um weitere Informationen zur Verwendung von [!DNL Identity Graph Linking Rules] zu erhalten:

>[!VIDEO](https://video.tv.adobe.com/v/3448281/?learn=on&enablevpops&captions=ger)

## Erste Schritte

Die folgenden Dokumente sind für das Verständnis von [!DNL Identity Graph Linking Rules] unerlässlich.

* [Algorithmus zur Identitätsoptimierung](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche für die Diagrammsimulation](./graph-simulation.md)
* [Benutzeroberfläche für Identitätseinstellungen](./identity-settings-ui.md)

## Szenarien zum Zusammenführen von Diagrammen {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="Szenarien zum Zusammenführen von Diagrammen"
>abstract="Es gibt mehrere Gründe, warum Diagramme zusammengeführt werden oder mehrere Personenentitäten darstellen können."

In diesem Abschnitt werden Beispielszenarien beschrieben, die Sie bei der Konfiguration von [!DNL Identity Graph Linking Rules] berücksichtigen können.

### Freigegebenes Gerät

Es gibt Fälle, in denen sich ein Gerät mehrmals anmelden kann:

| Freigegebenes Gerät | Beschreibung |
| --- | --- |
| Familien-Computer und Tablets | Ehemann und Ehefrau melden sich beide auf ihren jeweiligen Bankkonten an. |
| Öffentlicher Kiosk | Reisende an einem Flughafen, die sich mit ihrem Treueprogramm-Ausweis einloggen, um ihre Gepäckstücke einzuchecken und Bordkarten auszudrucken. |
| Callcenter | Callcenter-Mitarbeiter melden sich auf einem einzelnen Gerät im Namen von Kunden an, die den Support anrufen, um Probleme zu lösen. |

![Abbildung einiger gemeinsam genutzter Geräte.](../images/identity-settings/shared-devices.png)

In diesen Fällen wird eine einzelne ECID aus Diagrammsicht und ohne aktivierte Beschränkungen mit mehreren CRMIDs verknüpft.

Mit [!DNL Identity Graph Linking Rules] können Sie:

* Konfigurieren Sie die ID, die für die Anmeldung als eindeutige Kennung verwendet wird. Sie können beispielsweise ein Diagramm so beschränken, dass nur eine Identität mit einem CRMID-Namespace gespeichert wird, und diese CRMID daher als eindeutige Kennung eines gemeinsam genutzten Geräts definieren.
   * Auf diese Weise können Sie sicherstellen, dass CRMIDs nicht von der ECID zusammengeführt werden.

### Ungültige E-Mail-/Telefonszenarien

Es gibt auch Instanzen von Benutzern, die bei der Registrierung gefälschte Werte als Telefonnummern und/oder E-Mail-Adressen angeben. Wenn keine Beschränkungen aktiviert sind, werden in diesen Fällen Identitäten, die mit Telefon/E-Mail in Verbindung stehen, mit mehreren verschiedenen CRM-IDs verknüpft.

![Ein Diagramm, das ungültige E-Mail- oder Telefonszenarien darstellt.](../images/identity-settings/invalid-email-phone.png)

Mit [!DNL Identity Graph Linking Rules] können Sie:

* Konfigurieren Sie entweder die CRMID, Telefonnummer oder E-Mail-Adresse als eindeutige Kennung und beschränken Sie daher eine Person auf nur eine CRMID, Telefonnummer und/oder E-Mail-Adresse, die mit ihrem Konto verknüpft ist.

### Fehlerhafte oder fehlerhafte Identitätswerte

Es gibt Fälle, in denen nicht eindeutige, fehlerhafte Identitätswerte unabhängig vom Namespace in das System aufgenommen werden. Zu den Beispielen gehören:

* IDFA-Namespace mit dem Identitätswert „user_null“.
   * IDFA-Identitätswerte sollten 36 Zeichen lang sein: 32 alphanumerische Zeichen und vier Bindestriche.
* Telefonnummern-Namespace mit dem Identitätswert „nicht angegeben“.
   * Telefonnummern dürfen keine Buchstaben enthalten.

Diese Identitäten können zu folgenden Diagrammen führen, bei denen mehrere CRMIDs mit der „fehlerhaften“ Identität zusammengeführt werden:

![Ein Diagrammbeispiel für Identitätsdaten mit fehlerhaften oder fehlerhaften Identitätswerten.](../images/identity-settings/bad-data.png)

Mit [!DNL Identity Graph Linking Rules] können Sie die CRMID als eindeutige Kennung konfigurieren, um das Reduzieren unerwünschter Profile aufgrund dieses Datentyps zu verhindern.

## [!DNL Identity Graph Linking Rules] {#identity-graph-linking-rules}

Mit [!DNL Identity Graph Linking Rules] können Sie:

* Erstellen Sie für jeden Benutzer ein einzelnes Identitätsdiagramm bzw. ein zusammengeführtes Profil, indem Sie eindeutige Namespaces konfigurieren. Dadurch wird verhindert, dass zwei unterschiedliche Personenkennungen zu einem Identitätsdiagramm zusammengeführt werden.
* Verknüpfen Sie authentifizierte Online-Ereignisse mit der Person, indem Sie Prioritäten konfigurieren

### Terminologie {#terminology}

| Terminologie | Beschreibung |
| --- | --- |
| Eindeutiger Namespace | Ein eindeutiger Namespace ist ein Identity-Namespace, der im Kontext eines Identitätsdiagramms als eigenständig eingerichtet wurde. Sie können einen Namespace mithilfe der Benutzeroberfläche so konfigurieren, dass er eindeutig ist. Nachdem ein Namespace als eindeutig definiert wurde, kann ein Diagramm nur eine Identität haben, die diesen Namespace enthält. |
| Namespace-Priorität | Die Namespace-Priorität bezieht sich auf die relative Bedeutung von Namespaces untereinander. Die Namespace-Priorität kann über die Benutzeroberfläche konfiguriert werden. Sie können Namespaces in einem bestimmten Identitätsdiagramm nach Rang ordnen. Nach der Aktivierung werden Prioritätsnamen in verschiedenen Szenarien verwendet, z. B. als Eingabe für den Identitätsoptimierungsalgorithmus und zur Bestimmung der primären Identität für Erlebnisereignisfragmente. |
| Algorithmus zur Identitätsoptimierung | Der Algorithmus zur Identitätsoptimierung stellt sicher, dass Richtlinien, die durch die Konfiguration eines eindeutigen Namespace und von Namespace-Prioritäten erstellt wurden, in einem bestimmten Identitätsdiagramm durchgesetzt werden. |

### Eindeutiger Namespace {#unique-namespace}

Sie können einen Namespace mithilfe des Arbeitsbereichs der Benutzeroberfläche für Identitätseinstellungen so konfigurieren, dass er eindeutig ist. Dadurch wird dem Identitätsoptimierungsalgorithmus mitgeteilt, dass ein bestimmtes Diagramm möglicherweise nur eine Identität hat, die diesen eindeutigen Namespace enthält. Dadurch wird verhindert, dass zwei unterschiedliche Personenkennungen innerhalb desselben Diagramms zusammengeführt werden.

Betrachten Sie das folgende Szenario:

* Scott verwendet ein Tablet und öffnet seinen Google Chrome-Browser, um zu acme<span>.com zu gehen, wo er sich anmeldet und nach neuen Basketballschuhen sucht.
   * Hinter den Kulissen werden in diesem Szenario die folgenden Identitäten protokolliert:
      * Ein ECID-Namespace und ein -Wert, die die Verwendung des Browsers darstellen
      * Ein CRMID-Namespace und ein -Wert zur Darstellung des authentifizierten Benutzers (Scott hat sich mit seiner Kombination aus Benutzername und Kennwort angemeldet).
* Sein Sohn Peter verwendet dann das gleiche Tablet und verwendet auch Google Chrome, um zu acme<span>.com zu gehen, wo er sich mit seinem eigenen Konto anmeldet, um nach Fußballgeräten zu suchen.
   * Hinter den Kulissen werden in diesem Szenario die folgenden Identitäten protokolliert:
      * Derselbe ECID-Namespace und derselbe Wert für den Browser.
      * Ein neuer CRMID-Namespace und -Wert, der den authentifizierten Benutzer darstellt.

Wenn CRMID als eindeutiger Namespace konfiguriert wurde, teilt der Identitätsoptimierungsalgorithmus die CRMIDs in zwei separate Identitätsdiagramme auf, anstatt sie zusammenzuführen.

Wenn Sie keinen eindeutigen Namespace konfigurieren, erhalten Sie möglicherweise unerwünschte Diagrammzusammenführungen, z. B. zwei Identitäten mit demselben CRM-Namespace, aber unterschiedlichen Identitätswerten (Szenarien wie diese stellen oft zwei verschiedene Personenentitäten im selben Diagramm dar).

Sie müssen einen eindeutigen Namespace konfigurieren, um den Identitätsoptimierungsalgorithmus darüber zu informieren, Einschränkungen für die Identitätsdaten durchzusetzen, die in ein bestimmtes Identitätsdiagramm aufgenommen werden.

### Namespace-Priorität {#namespace-priority}

Die Namespace-Priorität bezieht sich auf die relative Bedeutung von Namespaces untereinander. Die Namespace-Priorität kann über die Benutzeroberfläche konfiguriert werden, und Sie können Namespaces in einem bestimmten Identitätsdiagramm nach Rang ordnen.

Eine Möglichkeit, die Namespace-Priorität zu verwenden, besteht darin, die primäre Identität von Erlebnisereignisfragmenten (Benutzerverhalten) im Echtzeit-Kundenprofil zu bestimmen. Wenn Prioritätseinstellungen konfiguriert sind, wird die primäre Identitätseinstellung in Web SDK nicht mehr verwendet, um zu bestimmen, welche Profilfragmente gespeichert werden.

Eindeutige Namespaces und Namespace-Prioritäten können beide im Arbeitsbereich der Benutzeroberfläche für Identitätseinstellungen konfiguriert werden. Die Auswirkungen ihrer Konfigurationen sind jedoch unterschiedlich:

| | Identity Service | Echtzeit-Kundenprofil |
| --- | --- | --- |
| Eindeutiger Namespace | In Identity Service bezieht sich der Identitätsoptimierungsalgorithmus auf eindeutige Namespaces, um die Identitätsdaten zu bestimmen, die in ein bestimmtes Identitätsdiagramm aufgenommen werden. | Eindeutige Namespaces wirken sich nicht auf das Echtzeit-Kundenprofil aus. |
| Namespace-Priorität | Bei Diagrammen mit mehreren Ebenen bestimmt die Namespace-Priorität im Identity Service, dass die entsprechenden Links entfernt werden. | Wenn ein Erlebnisereignis in Profile aufgenommen wird, wird der Namespace mit der höchsten Priorität zur primären Identität des Profilfragments. |

* Die Namespace-Priorität beeinflusst das Diagrammverhalten nicht, wenn die Beschränkung von 50 Identitäten pro Diagramm erreicht wird.
* **Die Namespace-Priorität ist ein numerischer Wert** der einem Namespace zugewiesen ist, um dessen relative Bedeutung anzugeben. Dies ist eine Eigenschaft eines Namespace.
* **Die Primäre Identität ist die Identität, für die ein Profilfragment gespeichert wird**. Ein Profilfragment ist ein Datensatz mit Daten, die Informationen zu einem bestimmten Benutzer speichern: Attribute (normalerweise über CRM-Datensätze aufgenommen) oder Ereignisse (normalerweise aus Erlebnisereignissen oder Online-Daten aufgenommen).
* Die Namespace-Priorität bestimmt die primäre Identität für Experience Event-Fragmente.
   * Für Profildatensätze können Sie den Arbeitsbereich Schemata in der Experience Platform-Benutzeroberfläche verwenden, um Identitätsfelder zu definieren, einschließlich der Primäridentität. Weitere Informationen finden Sie im Handbuch unter [Definieren von Identitätsfeldern in ](../../xdm/ui/fields/identity.md) Benutzeroberfläche“.
* Wenn ein Erlebnisereignis zwei oder mehr Identitäten mit der höchsten Namespace-Priorität in der identityMap hat, wird es bei der Aufnahme abgelehnt, da es als „fehlerhafte Daten“ betrachtet wird. Wenn die identityMap beispielsweise `{ECID: 111, CRMID: John, CRMID: Jane}` enthält, wird das gesamte Ereignis als ungültige Daten zurückgewiesen, da dies bedeutet, dass das Ereignis gleichzeitig sowohl `CRMID: John` als auch `CRMID: Jane` zugeordnet ist.

Weitere Informationen finden Sie im Handbuch unter [Namespace-Priorität](./namespace-priority.md).

## Nächste Schritte

Weitere Informationen zu [!DNL Identity Graph Linking Rules] finden Sie in der folgenden Dokumentation:

* [Algorithmus zur Identitätsoptimierung](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche für die Diagrammsimulation](./graph-simulation.md)
* [Benutzeroberfläche für Identitätseinstellungen](./identity-settings-ui.md)
