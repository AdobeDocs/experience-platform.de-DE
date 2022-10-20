---
title: Übersicht über Splunk-Erweiterung
description: Erfahren Sie mehr über die Splunk-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
source-git-commit: cad6d78868ac89be325faa58f567b89869bfff02
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 2%

---

# Übersicht über Splunk-Erweiterungen

[Splunk](https://www.splunk.com) ist eine Beobachtbarkeitsplattform, die Suche, Analyse und Visualisierung für umsetzbare Einblicke in Ihre Daten bietet. Der Splunk [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) -Erweiterung nutzt die [Splunk-HTTP-Ereignis-Collector-REST-API](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) , um Ereignisse vom Adobe Experience Platform Edge Network an die [Splunk-HTTP-Ereigniserfassung](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

Splunk verwendet Träger-Token als Authentifizierungsmechanismus für die Kommunikation mit der Splunk Event Collector API.

## Anwendungsbeispiele {#use-cases}

Marketing-Teams können die -Erweiterung für die folgenden Anwendungsfälle verwenden:

| Anwendungsfall | Beschreibung |
| --- | --- |
| Analyse des Kundenverhaltens | Unternehmen können Kundeninteraktions-Ereignisdaten von ihrer Website erfassen und relevante Ereignisse an Splunk weiterleiten. Marketing- und Analyseteams können dann nachfolgende Analysen innerhalb der Splunk-Plattform durchführen, um wichtige Benutzerinteraktionen und -verhalten zu verstehen. Die Splunk-Plattform kann verwendet werden, um Diagramme, Dashboards oder andere Visualisierungen zu generieren, um geschäftliche Stakeholder zu informieren. |
| Skalierbare Suche nach großen Datensätzen | Unternehmen können Transaktions- oder Konversationseingaben als Ereignisdaten von der Website erfassen und Ereignisse an Splunk weiterleiten. Analytics-Teams können dann die skalierbaren Indexierungsfunktionen von Splunk nutzen, um große Datensätze zu filtern und zu verarbeiten, um geschäftliche Einblicke zu gewinnen und fundierte Entscheidungen zu treffen. |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

Sie müssen über ein Splunk-Konto verfügen, um diese Erweiterung verwenden zu können. Sie können sich für ein Splunk-Konto im [Splunk-Homepage](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> Die Splunk-Erweiterung unterstützt sowohl Splunk Cloud- als auch Splunk-Unternehmensinstanzen. Dieses Handbuch dokumentiert eine Implementierung mithilfe von [Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) als Referenz. Der Konfigurationsprozess für [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) ist ähnlich, erfordert jedoch spezifische Anweisungen von Ihrem Splunk-Enterprise-Administrator.

Sie müssen auch über die folgenden technischen Werte verfügen, um die Erweiterung zu konfigurieren:

* Ein [Ereignis-Sammlungstoken](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). Token haben in der Regel das UUIDv4-Format wie folgt: `12345678-1234-1234-1234-1234567890AB`.
* Die Adresse und den Port der Splunk-Plattforminstanz für Ihr Unternehmen. Die Adresse und der Anschluss einer Plattforminstanz haben in der Regel das folgende Format: `mysplunkserver.example.com:443`.
   >[!IMPORTANT]
   >
   > Splunk-Endpunkte, auf die in der Ereignisweiterleitung verwiesen wird, sollten nur Port verwenden `443`. Nicht standardmäßige Ports werden derzeit in Implementierungen der Ereignisweiterleitung nicht unterstützt.

## Splunk-Erweiterung installieren {#install}

Navigieren Sie zur Installation der Splunk-Event-Collector-Erweiterung in der Benutzeroberfläche zu **Ereignisweiterleitung** und wählen Sie eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, navigieren Sie zu **Erweiterungen** > **Katalog**. Suchen Sie nach &quot;[!DNL Splunk]&quot;, und wählen Sie dann **[!DNL Install]** in der Splunk-Erweiterung.

![Schaltfläche &quot;Installieren&quot;für die Splunk-Erweiterung, die in der Benutzeroberfläche ausgewählt wird](../../../images/extensions/splunk/install.png)

## Splunk-Erweiterung konfigurieren {#configure_extension}

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Lesen Sie vor dem Start alle Konfigurationsschritte durch, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Auswählen **Erweiterungen** in der linken Navigation. under **Installiert** auswählen **Konfigurieren** in der Splunk-Erweiterung.

![Schaltfläche &quot;Konfigurieren&quot;für die Splunk-Erweiterung, die in der Benutzeroberfläche ausgewählt wird](../../../images/extensions/splunk/configure.png)

Für **[!UICONTROL HTTP-Ereignis-Sammlungs-URL]** Geben Sie die Adresse und den Port Ihrer Splunk-Plattforminstanz ein. under **[!UICONTROL Zugriffstoken]** eingeben [!DNL Event Collector Token] -Wert. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![In der Benutzeroberfläche ausgefüllte Konfigurationsoptionen](../../../images/extensions/splunk/input.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config_rule}

Erstellen einer neuen Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel die [!UICONTROL Splunk] Erweiterung und wählen Sie dann die [!UICONTROL Ereignis erstellen] Aktionstyp. Zusätzliche Steuerelemente scheinen das Splunk-Ereignis weiter zu konfigurieren.

![Aktionskonfiguration definieren](../../../images/extensions/splunk/action-configurations.png)

Der nächste Schritt besteht darin, die Eigenschaften des Splunk-Ereignisses Datenelementen zuzuordnen, die Sie zuvor erstellt haben. Die unterstützten optionalen Zuordnungen, die auf den konfigurierbaren Eingabeereignisdaten basieren, sind unten aufgeführt. Siehe Abschnitt [Splunk-Dokumentation](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) für weitere Informationen.

| Feldname | Beschreibung |
| --- | --- |
| [!UICONTROL Ereignis ]<br><br>**(ERFORDERLICH)** | Geben Sie an, wie Sie die Ereignisdaten bereitstellen möchten. Ereignisdaten können der `event` -Schlüssel im JSON-Objekt in der HTTP-Anforderung oder es kann sich um rohen Text handeln. Die `event` -Schlüssel befindet sich im JSON-Ereignis-Paket auf derselben Ebene wie die Metadatenschlüssel. Innerhalb der `event` geschweifte Klammern verwenden, können die Daten in jeder gewünschten Form vorliegen (z. B. Zeichenfolge, Zahl, ein anderes JSON-Objekt usw.). |
| [!UICONTROL Host] | Der Hostname des Clients, von dem Sie Daten senden. |
| [!UICONTROL Quellentyp] | Der Quelltyp, der den Ereignisdaten zugewiesen werden soll. |
| [!UICONTROL Quelle] | Der Quellwert, der den Ereignisdaten zugewiesen werden soll. Wenn Sie beispielsweise Daten von einer App senden, die Sie entwickeln, setzen Sie diesen Schlüssel auf den Namen der App. |
| [!UICONTROL Index] | Der Name des Index der Ereignisdaten. Der hier angegebene Index muss sich in der Liste der zulässigen Indizes befinden, wenn der Indexparameter des Tokens festgelegt ist. |
| [!UICONTROL Zeit] | Die Ereigniszeit. Das Standardzeitformat ist UNIX-Zeit (im Format `<sec>.<ms>`) und hängt von Ihrer lokalen Zeitzone ab. Beispiel: `1433188255.500` gibt 1433188255 Sekunden und 500 Millisekunden nach Epoche oder Montag, den 1. Juni 2015 bei 7 an:50:17.00 Uhr GMT. |
| [!UICONTROL Felder] | Geben Sie ein unformatiertes JSON-Objekt oder einen Satz von Schlüssel-Wert-Paaren an, die explizite benutzerdefinierte Felder enthalten, die zur Indexzeit definiert werden sollen.  Die `fields` -Schlüssel gilt nicht für Rohdaten.<br><br>Anforderungen, die die `fields` -Eigenschaft muss an die `/collector/event` -Endpunkt oder andernfalls werden sie nicht indiziert. Weitere Informationen finden Sie in der Splunk-Dokumentation unter [Indexierte Feldextraktionen](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### Daten in Splunk überprüfen {#validate}

Überprüfen Sie nach dem Erstellen und Ausführen der Ereignisweiterleitungsregel, ob das an die Splunk-API gesendete Ereignis wie erwartet in der Splunk-Benutzeroberfläche angezeigt wird. Wenn die Ereigniserfassung und Experience Platform erfolgreich integriert wurden, werden Ereignisse in der Splunk-Konsole wie folgt angezeigt:

![Ereignisdaten, die während der Validierung in der Splunk-Benutzeroberfläche angezeigt werden](../../../images/extensions/splunk/splunk-data.png)

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie die Splunk-Ereignisweiterleitungs-Erweiterung in der Benutzeroberfläche installieren und konfigurieren. Weitere Informationen zur Erfassung von Ereignisdaten in Splunk finden Sie in der offiziellen Dokumentation:

* [Einrichten und Verwenden der HTTP-Ereigniserfassung im Splunk-Web ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [Einrichten der Authentifizierung mit Token](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [Fehlerbehebung bei der HTTP-Ereigniserfassung](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (listet auch ein Kompendium von [mögliche Fehlercodes](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
