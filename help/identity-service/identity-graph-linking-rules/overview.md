---
title: Verknüpfungsregeln für Identitätsdiagramme
description: Erfahren Sie mehr über die Verknüpfungsregeln für Identitätsdiagramme in Identity Service.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 6efd9c8fd1acce08027905f2e3c005a88a429a12
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 8%

---

# [!DNL Identity Graph Linking Rules] – Übersicht {#identity-graph-linking-rules-overview}

>[!CONTEXTUALHELP]
>id="platform_identities_linkingrules_overview"
>title="Verknüpfungsregeln für Identitätsdiagramme"
>abstract="Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über die Verknüpfungsregeln für Identitätsdiagramme bereitgestellt werden, und eine genaue Personalisierung für Ihre Benutzer ermöglichen."

>[!IMPORTANT]
>
>Wenden Sie sich an Ihr Adobe-Konto-Team, wenn Sie eine bestehende Sandbox haben, in der reduzierte Diagramme nach dem Aktivieren der Identitätseinstellungen nicht mehr reduziert („korrigiert„) werden müssen.

Mit Adobe Experience Platform Identity Service und dem Echtzeit-Kundenprofil ist es einfach anzunehmen, dass Ihre Daten perfekt aufgenommen werden und dass alle zusammengeführten Profile über eine Personenkennung, wie z. B. eine CRMID, eine einzelne Person darstellen. Es gibt jedoch mögliche Szenarien, in denen bestimmte Daten versuchen könnten, mehrere unterschiedliche Profile zu einem einzigen Profil zusammenzuführen („Diagrammausblendung„). Um diese unerwünschten Zusammenführungen zu verhindern, können Sie Konfigurationen verwenden, die über [!DNL Identity Graph Linking Rules] bereitgestellt werden, und eine genaue Personalisierung für Ihre Benutzerinnen und Benutzer ermöglichen.

## Erste Schritte

Die folgenden Dokumente sind für das Verständnis von [!DNL Identity Graph Linking Rules] unerlässlich.

* [Algorithmus zur Identitätsoptimierung](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche für die Diagrammsimulation](./graph-simulation.md)
* [Benutzeroberfläche für Identitätseinstellungen](./identity-settings-ui.md)

## Videobibliothek

Sehen Sie sich die folgenden Videos an, um mehr über einige der grundlegenden Aspekte der Regeln für die Verknüpfung von Identitätsdiagrammen zu erfahren.

<!-- CARDS
{target = _blank}
* https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/overview
* https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation 

    {description = Learn how to use the graph simulator to test out identity graph linking rules.}

* https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings
    {description = Learn how to enable and configure identity graph linking rules to build accurate customer profiles}
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules overview">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" title="Überblick über die Verknüpfungsregeln für Identitätsdiagramme" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3448250/?format=jpeg&nocache=1747851655227" alt="Überblick über die Verknüpfungsregeln für Identitätsdiagramme"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" title="Überblick über die Verknüpfungsregeln für Identitätsdiagramme">Überblick über die Regeln für die Verknüpfung von Identitätsdiagrammen</a>
                    </p>
                    <p class="is-size-6">Verschaffen Sie sich einen Überblick darüber, wie Datenarchitektinnen und -architekten mit Regeln für die Verknüpfung von Identitätsdiagrammen genaue Kundenprofile sicherstellen und das Reduzieren von Diagrammen verhindern können.</p>
                </div>
                <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/overview" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">beobachten</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Graph Simulation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" title="Regeln zur Verknüpfung von Identitätsdiagrammen - Diagrammsimulation" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3444032/?format=jpeg&nocache=1747851655237" alt="Regeln zur Verknüpfung von Identitätsdiagrammen - Diagrammsimulation"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" title="Regeln zur Verknüpfung von Identitätsdiagrammen - Diagrammsimulation">Regeln für die Verknüpfung von Identitätsdiagrammen – Diagrammsimulation</a>
                    </p>
                    <p class="is-size-6">Erfahren Sie, wie Sie mit dem Diagrammsimulator Identitätsdiagramm-Verknüpfungsregeln testen können.</p>
                </div>
                <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/graph-simulation" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">beobachten</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Identity graph linking rules - Identity settings">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" title="Verknüpfungsregeln für Identitätsdiagramme - Identitätseinstellungen" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3458487/?format=jpeg&nocache=1747851655218" alt="Verknüpfungsregeln für Identitätsdiagramme - Identitätseinstellungen"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" title="Verknüpfungsregeln für Identitätsdiagramme - Identitätseinstellungen">Verknüpfungsregeln für Identitätsdiagramme - Identitätseinstellungen</a>
                    </p>
                    <p class="is-size-6">Erfahren Sie, wie Sie Regeln zur Identitätsdiagramm-Verknüpfung aktivieren und konfigurieren, um genaue Kundenprofile zu erstellen</p>
                </div>
                <a href="https://experienceleague.adobe.com/de/docs/platform-learn/tutorials/identities/graph-linking-rules/identity-settings" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">beobachten</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


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

Sie können einen Namespace mithilfe des Arbeitsbereichs der Benutzeroberfläche für Identitätseinstellungen so konfigurieren, dass er eindeutig ist. Dadurch wird dem Identitätsoptimierungsalgorithmus mitgeteilt, dass ein bestimmtes Diagramm nur eine Identität haben kann, die diesen eindeutigen Namespace enthält. Dadurch wird verhindert, dass zwei unterschiedliche Personenkennungen innerhalb desselben Diagramms zusammengeführt werden.

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
| Eindeutiger Namespace | In Identity Service bezieht sich der Algorithmus zur Identitätsoptimierung auf eindeutige Namespaces, um die Identitätsdaten zu bestimmen, die in ein bestimmtes Identitätsdiagramm aufgenommen werden. | Eindeutige Namespaces wirken sich nicht auf das Echtzeit-Kundenprofil aus. |
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