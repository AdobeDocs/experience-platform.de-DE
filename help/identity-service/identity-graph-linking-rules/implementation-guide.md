---
title: Implementierungshandbuch für Regeln zur Identitätsdiagrammzuordnung
description: Erfahren Sie mehr über die empfohlenen Schritte zur Implementierung Ihrer Daten mit Regelkonfigurationen für die Identitätsdiagrammzuordnung.
badge: Beta
exl-id: 368f4d4e-9757-4739-aaea-3f200973ef5a
source-git-commit: adfb1e83289435e6991d4cdd2e2a45e3d5a9b32f
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 3%

---

# Implementierungshandbuch für Regeln zur Identitätsdiagrammzuordnung

>[!AVAILABILITY]
>
>Die Regeln zur Verknüpfung von Identitätsdiagrammen befinden sich derzeit in der Beta-Phase. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten. Die Funktion und die Dokumentation können sich ändern.

Lesen Sie dieses Dokument, um eine schrittweise Anleitung zur Implementierung Ihrer Daten mit dem Adobe Experience Platform Identity-Dienst zu erhalten.

Schrittweise Anleitung:


1. [Vollständige Voraussetzungen für die Implementierung](#prerequisites-for-implementation)
2. [Erstellen der erforderlichen Identitäts-Namespaces](#namespace)
3. [Verwenden Sie das Tool zur Diagrammsimulation, um sich mit dem Identitätsoptimierungsalgorithmus vertraut zu machen.](#graph-simulation)
4. [Verwenden Sie das Tool für Identitätseinstellungen, um Ihre eindeutigen Namespaces zu bestimmen und die Prioritätseinstufung für Ihre Namespaces zu konfigurieren](#identity-settings)
5. [Erstellen eines Experience-Datenmodell (XDM)-Schemas](#schema)
6. [Erstellen eines Datensatzes](#dataset)
7. [Daten auf Experience Platform erfassen](#ingest)

## Voraussetzungen für die Implementierung {#prerequisites-for-implementation}

In diesem Abschnitt werden die erforderlichen Schritte beschrieben, die Sie vor der Implementierung der Regeln zur Identitätsdiagrammverknüpfung mit Ihren Daten durchführen müssen.

### Eindeutiger Namespace

#### Namespace-Anforderung für eine Person {#single-person-namespace-requirement}

Sie müssen sicherstellen, dass der eindeutige Namespace mit der höchsten Priorität immer in jedem Profil vorhanden ist. Dadurch kann Identity Service die entsprechende Personenkennung in einem bestimmten Diagramm erkennen.

+++Auswählen , um ein Beispiel für ein Diagramm ohne Namespace für eine einzelne Person anzuzeigen

Ohne einen eindeutigen Namespace zur Darstellung Ihrer Personen-IDs erhalten Sie möglicherweise ein Diagramm, das Links zu unterschiedlichen Personen-IDs mit derselben ECID enthält. In diesem Beispiel sind sowohl B2BCRM als auch B2CCRM gleichzeitig mit derselben ECID verknüpft. Dieses Diagramm legt nahe, dass Tom mithilfe seines B2C-Anmeldekontos mithilfe seines B2C-Anmeldekontos mit Summer ein Gerät freigegeben hat, das er mit seinem B2B-Anmeldekonto genutzt hat. Das System erkennt jedoch, dass es sich um ein Profil handelt (Diagrammausfall).

![Ein Diagrammszenario, bei dem zwei Personen-IDs mit derselben ECID verknüpft sind.](../images/graph-examples/multi_namespaces.png)

+++

+++Auswählen , um ein Beispiel für ein Diagramm mit einem Namespace für eine einzelne Person anzuzeigen

Bei einem eindeutigen Namespace (in diesem Fall einer CRMID anstelle zweier unterschiedlicher Namespaces) kann Identity Service die Personenkennung erkennen, die zuletzt mit der ECID verknüpft wurde. Da in diesem Beispiel eine eindeutige CRMID vorhanden ist, kann Identity Service ein Szenario mit einem &quot;freigegebenen Gerät&quot;erkennen, bei dem zwei Entitäten dasselbe Gerät gemeinsam nutzen.

![Ein Szenario mit einem freigegebenen Gerätediagramm, in dem zwei Personen-IDs mit derselben ECID verknüpft sind, der ältere Link jedoch entfernt wird.](../images/graph-examples/crmid_only_multi.png)

+++

### Namespace-Prioritätskonfiguration

Wenn Sie den [Adobe Analytics-Quell-Connector](../../sources/tutorials/ui/create/adobe-applications/analytics.md) zum Erfassen von Daten verwenden, müssen Sie Ihren ECIDs eine höhere Priorität als der Adobe Analytics ID (AAID) zuweisen, da Identity Service AAID blockiert. Durch die Priorisierung von ECID können Sie das Echtzeit-Kundenprofil anweisen, nicht authentifizierte Ereignisse anstelle von AAID in ECID zu speichern.

### XDM-Erlebnisereignisse

* Während des Prozesses vor der Implementierung müssen Sie sicherstellen, dass die authentifizierten Ereignisse, die Ihr System an Experience Platform sendet, immer eine Personenkennung wie CRMID enthalten.
* Senden Sie beim Senden von Ereignissen mit XDM-Erlebnisereignissen keine leere Zeichenfolge als Identitätswert. Dies führt zu Systemfehlern.

+++Auswählen , um ein Beispiel einer Payload mit einer leeren Zeichenfolge anzuzeigen

Im folgenden Beispiel wird ein Fehler zurückgegeben, da der Identitätswert für `Phone` als leere Zeichenfolge übermittelt wird.

```json
    "identityMap": {
        "ECID": [
            {
                "id": "24165048599243194405404369473457348936",
                "primary": false
            }
        ],
        "Phone": [
            {
                "id": "",
                "primary": true
            }
        ]
    }
```

+++

Sie müssen sicherstellen, dass Sie beim Senden von Ereignissen mit XDM-Erlebnisereignissen über eine voll qualifizierte Identität verfügen.

+++Auswählen , um ein Beispiel für ein Ereignis mit einer vollständig qualifizierten Identität anzuzeigen

```json
    "identityMap": {
        "ECID": [
            {
                "id": "24165048599243194405404369473457348936",
                "primary": false
            }
        ]
    }
```

+++

## Berechtigungen festlegen {#set-permissions}

Der erste Schritt im Implementierungsprozess für Identity Service besteht darin sicherzustellen, dass Ihr Experience Platform-Konto einer Rolle hinzugefügt wird, die über die erforderlichen Berechtigungen verfügt. Ihr Administrator kann Berechtigungen für Ihr Konto konfigurieren, indem Sie zur Benutzeroberfläche &quot;Berechtigungen&quot;in Adobe Experience Cloud navigieren. Dort muss Ihr Konto einer Rolle mit den folgenden Berechtigungen hinzugefügt werden:

* [!UICONTROL Identitätseinstellungen anzeigen]: Wenden Sie diese Berechtigung an, um eindeutige Namespaces und Namespace-Priorität auf der Durchsuchen-Seite des Identitäts-Namespace anzeigen zu können.
* [!UICONTROL Identitätseinstellungen bearbeiten]: Wenden Sie diese Berechtigung an, um Ihre Identitätseinstellungen bearbeiten und speichern zu können.

Weitere Informationen zu Berechtigungen finden Sie im [Berechtigungshandbuch](../../access-control/abac/ui/permissions.md).

## Erstellen Ihrer Identitäts-Namespaces {#namespace}

Wenn Ihre Daten dies erfordern, müssen Sie zunächst die entsprechenden Namespaces für Ihre Organisation erstellen. Anweisungen zum Erstellen eines benutzerdefinierten Namespace finden Sie im Handbuch zum Erstellen eines benutzerdefinierten Namespace in der Benutzeroberfläche ](../features/namespaces.md#create-custom-namespaces).[

## Tool zur Diagrammsimulation verwenden {#graph-simulation}

Navigieren Sie anschließend zum [Tool zur Diagrammsimulation](./graph-simulation.md) in der Benutzeroberfläche des Identity Service-Arbeitsbereichs. Mit dem Simulationstool für Diagramme können Sie Identitätsdiagramme simulieren, die mit einer Vielzahl verschiedener eindeutiger Namespace- und Namespace-Prioritätskonfigurationen erstellt wurden.

Durch die Erstellung verschiedener Konfigurationen können Sie mit dem Tool für die Diagrammsimulation erfahren, wie der Identitätsoptimierungsalgorithmus und bestimmte Konfigurationen das Verhalten Ihres Diagramms beeinflussen können.

## Identitätseinstellungen konfigurieren {#identity-settings}

Sobald Sie eine bessere Vorstellung davon haben, wie sich Ihr Diagramm verhalten soll, navigieren Sie zum [Tool für Identitätseinstellungen](./identity-settings-ui.md) in der Benutzeroberfläche des Identity Service-Arbeitsbereichs.

Verwenden Sie das Tool für Identitätseinstellungen, um Ihre eindeutigen Namespaces zu bestimmen und Ihre Namespaces nach Priorität zu konfigurieren. Sobald Sie mit der Anwendung Ihrer Einstellungen fertig sind, müssen Sie mindestens sechs Stunden warten, bis Sie mit der Datenerfassung fortfahren können, da es mindestens sechs Stunden dauert, bis neue Einstellungen in Identity Service angezeigt werden.

## Erstellen eines XDM-Schemas {#schema}

Nachdem Sie Ihre eindeutigen Namespaces und Namespace-Prioritäten festgelegt haben, können Sie jetzt mit der erforderlichen Einrichtung fortfahren, um Ihre Daten zu erfassen. Zunächst müssen Sie ein XDM-Schema erstellen. Abhängig von Ihren Daten müssen Sie möglicherweise ein Schema für sowohl XDM Individual Profile als auch XDM ExperienceEvent erstellen.

Um Daten in das Echtzeit-Kundenprofil zu erfassen, müssen Sie sicherstellen, dass Ihr Schema mindestens ein Feld enthält, das als primäre Identität ausgewiesen wurde. Durch Festlegen einer primären Identität können Sie ein bestimmtes Schema für die Profilerfassung aktivieren.

Anweisungen zum Erstellen eines Schemas finden Sie in der Anleitung zum [Erstellen eines XDM-Schemas in der Benutzeroberfläche](../../xdm/tutorials/create-schema-ui.md).

## Erstellen eines Datensatzes {#dataset}

Erstellen Sie anschließend einen Datensatz, um eine Struktur für die Daten bereitzustellen, die Sie erfassen werden. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze funktionieren gemeinsam mit Schemas und zur Aufnahme von Daten in das Echtzeit-Kundenprofil muss Ihr Datensatz für die Profilaufnahme aktiviert sein. Damit Ihr Datensatz für Profil aktiviert werden kann, muss er auf ein Schema verweisen, das für die Profilaufnahme aktiviert ist.

Anweisungen zum Erstellen eines Datensatzes finden Sie im [Benutzerhandbuch zur Datensatz-Benutzeroberfläche](../../catalog/datasets/user-guide.md).

## Daten erfassen {#ingest}

An dieser Stelle sollten Sie Folgendes haben:

* Die erforderlichen Berechtigungen für den Zugriff auf Identity Service-Funktionen.
* Namespaces für Ihre Daten.
* Ausgewählte eindeutige Namespaces und konfigurierte Prioritäten für Ihre Namespaces.
* Mindestens ein XDM-Schema. (Abhängig von Ihren Daten und Ihrem spezifischen Anwendungsfall müssen Sie möglicherweise sowohl Profil- als auch Erlebnisereignisschemas erstellen.)
* Ein Datensatz, der auf Ihrem Schema basiert.

Sobald Sie alle oben aufgelisteten Elemente haben, können Sie mit der Erfassung Ihrer Daten zu Experience Platform beginnen. Sie können die Datenerfassung auf verschiedene Arten durchführen. Sie können die folgenden Dienste verwenden, um Ihre Daten zum Experience Platform zu bringen:

* [Batch- und Streaming-Erfassung](../../ingestion/home.md)
* [Datenerfassung in Experience Platform](../../collection/home.md)
* [Experience Platform-Quellen](../../sources/home.md)

>[!TIP]
>
>Nach der Erfassung Ihrer Daten ändert sich die XDM-Rohdaten-Payload nicht mehr. Möglicherweise werden Ihre primären Identitätskonfigurationen weiterhin in der Benutzeroberfläche angezeigt. Diese Konfigurationen werden jedoch durch Identitätseinstellungen überschrieben.

Verwenden Sie für jedes Feedback die Option **[!UICONTROL Beta feedback]** im UI-Arbeitsbereich des Identity Service.

## Überprüfen Ihrer Diagramme {#validate}

Verwenden Sie das Identitäts-Dashboard, um Einblicke in den Zustand Ihrer Identitätsdiagramme zu erhalten, z. B. Ihre gesamten Trends bei Identitätszählung und Diagrammanzahl, Identitätszählung nach Namespace und Diagrammanzahl nach Diagrammgröße. Sie können das Identitäts-Dashboard auch verwenden, um Trends in Diagrammen mit zwei oder mehr Identitäten anzuzeigen, die nach Namespace organisiert sind.

Wählen Sie die Auslassungszeichen (`...`) aus und wählen Sie dann **[!UICONTROL Mehr anzeigen]** , um weitere Informationen zu erhalten und zu überprüfen, ob keine ausgeblendeten Diagramme vorhanden sind.

## Anhang {#appendix}

In diesem Abschnitt finden Sie weitere Informationen, auf die Sie bei der Implementierung Ihrer Identitätseinstellungen und eindeutigen Namespaces verweisen können.

### Dangling loginID scenario {#dangling-loginid-scenario}

Das folgende Diagramm simuliert ein &quot;gefährliches&quot;loginID-Szenario. In diesem Beispiel sind zwei verschiedene loginIDs an dieselbe ECID gebunden. `{loginID: ID_C}` ist jedoch nicht mit der CRMID verknüpft. Identity Service kann daher nicht erkennen, dass diese beiden loginIDs zwei verschiedene Entitäten darstellen.

>[!BEGINTABS]

>[!TAB Ambiguous loginID]

In diesem Beispiel bleibt `{loginID: ID_C}` verwundbar und ist nicht mit einer CRMID verknüpft. Somit bleibt die Personenentität, mit der diese loginID verknüpft werden soll, mehrdeutig.

![Ein Beispiel für ein Diagramm mit einem &quot;gefährlichen&quot; loginID-Szenario.](../images/graph-examples/dangling_example.png)

>[!TAB loginID ist mit einer CRMID verknüpft]

In diesem Beispiel ist `{loginID: ID_C}` mit `{CRMID: Tom}` verknüpft. Daher kann das System erkennen, dass diese loginID mit Tom verknüpft ist.

![LoginID ist mit einer CRMID verknüpft.](../images/graph-examples/id_c_tom.png)

>[!TAB loginID ist mit einer anderen CRMID verknüpft]

In diesem Beispiel ist `{loginID: ID_C}` mit `{CRMID: Summer}` verknüpft. Daher kann das System erkennen, dass diese loginID mit einer anderen Entität, in diesem Fall Summer, verknüpft ist.

Dieses Beispiel zeigt auch, dass Tom und Summer Personen voneinander trennen, die ein Gerät teilen, das durch `{ECID: 111}` dargestellt wird.

![LoginID ist mit einer anderen CRMID verknüpft.](../images/graph-examples/id_c_summer.png)

>[!ENDTABS]

## Nächste Schritte

Weitere Informationen zu Regeln zur Verknüpfung von Identitätsdiagrammen finden Sie in der folgenden Dokumentation:

* [Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen](./overview.md)
* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche der Diagrammsimulation](./graph-simulation.md)
* [Benutzeroberfläche für Identitätseinstellungen](./identity-settings-ui.md)
