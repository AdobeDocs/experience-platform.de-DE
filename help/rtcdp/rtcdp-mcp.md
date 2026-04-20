---
solution: Real-Time Customer Data Platform
product: real-time customer data platform
title: Arbeiten mit MCP-Clients (Beta)
description: Erfahren Sie, wie Sie Adobe Real-Time CDP mithilfe des MCP-Servers mit MCP-Clients verbinden
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
source-git-commit: 4805570178a923206565c4ee1b55ab6532579d66
workflow-type: tm+mt
source-wordcount: '2376'
ht-degree: 2%

---

# Arbeiten mit MCP-Clients (Beta) {#rtcdp-mcp}

Sie können die Adobe Real-Time CDP-MCP-Integration verwenden, um Zielgruppen, Ziele und den Aktivierungsstatus mit einfachen Eingabeaufforderungen abzufragen - ohne API-Aufrufe zu schreiben oder durch Produktbildschirme zu navigieren. Auf dieser Seite wird erläutert, wie die Integration funktioniert, was Sie damit tun können und wie Sie beginnen können.

>[!AVAILABILITY]
>
>Der Real-Time CDP-MCP-Server wird als **Remote-HTTP-Transport-Server** verteilt, den Benutzer in unterstützten MCP-Clients und App-Plattformen installieren und konfigurieren (z. B. Claude, ChatGPT, Claude Code, Codex, Cursor oder VS-Code). Die Authentifizierung erfolgt über einen **browserbasierten Anmeldefluss** - Wenn Ihr Client zum ersten Mal eine Verbindung zum Server herstellt, wird Ihr Standardbrowser geöffnet, damit Sie sich mit Ihren Adobe-Anmeldeinformationen anmelden und den Zugriff autorisieren können.

## Beta, Sicherheit und rechtliche Hinweise {#mcp-notices}

**Hinweis zur Beta-Dokumentation:** Diese Dokumentation behandelt eine Beta-Funktion und stellt keine endgültige Dokumentation dar. Der hier beschriebene Inhalt bezieht sich auf eine Beta-Version und kann sich vor der allgemeinen Verfügbarkeit ändern. Adobe übernimmt keine Gewähr für die Vollständigkeit oder Richtigkeit dieser Dokumentation.

Durch die Verwendung des Adobe Real-Time CDP MCP Servers (Beta) (“Beta„) erkennen Sie hiermit an, dass der Beta **„wie besehen“ und ohne Gewährleistung jeglicher Art bereitgestellt wird**. Adobe ist nicht verpflichtet, die Beta zu pflegen, zu korrigieren, zu aktualisieren, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die ordnungsgemäße Funktionsweise oder Leistung solcher Beta und/oder Begleitmaterialien zu verlassen. Die Beta gilt als vertrauliche Information von Adobe. Jedes „Feedback“ (Informationen zur Beta-Version, einschließlich, aber nicht beschränkt auf Probleme oder Mängel, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), das Sie Adobe übermitteln, wird hiermit an Adobe übertragen, einschließlich aller Rechte, Titel und Interessen an diesem Feedback.

>[!WARNING]
>
>Das Model Context Protocol (MCP) ist ein aufstrebender Open-Source-Standard, der Sicherheits- oder Zuverlässigkeitsrisiken mit sich bringen kann. Adobe MCP-Server-Integrationen und die zugehörige Dokumentation werden ohne Mängelgewähr und ohne Gewährleistung jeglicher Art bereitgestellt.
>
>Die Verbindung von MCP-Clients oder -Servern mit Adobe-Produkten ist eine vom Kunden gewählte Konfiguration. Die Kunden sind dafür verantwortlich, die Sicherheit und Eignung jeder MCP-Integration zu bewerten. Adobe übernimmt keine Verantwortung für Probleme, die sich aus einer Fehlkonfiguration, einer fehlerhaften Verwendung des MCP, Sicherheitslücken in Drittanbieterimplementierungen oder unbeabsichtigten Aktionen ergeben, die über MCP-fähige Workflows ausgeführt werden.
>
>Um Risiken zu reduzieren, empfiehlt Adobe, Integrationen in einer Sandbox-Umgebung vor der produktiven Verwendung zu testen und alle MCP-initiierten Aktionen und Antworten sorgfältig zu überprüfen und zu validieren, bevor sie bestätigt oder sich auf sie verlassen.

## Was ist das Modell-Kontextprotokoll? {#mcp-overview}

Marketing-, Daten- und Kundenerlebnis-Teams verlassen sich zunehmend auf Chat-basierte Anwendungen und Entwickler-Tools - wie Anthropic Claude, OpenAI ChatGPT, Cursor und Microsoft Copilot Studio -, um ihre tägliche Arbeit zu optimieren. Diese Anwendungen unterstützen das **Model Context Protocol (MCP)**, einen offenen Standard, der es Anwendungen ermöglicht, Backend-Tools auf einheitliche Weise für große Sprachmodelle (LLMs) verfügbar zu machen.

Real-Time CDP bietet jetzt einen MCP-Server, der Zielgruppen-, Ziel- und Aktivierungsvorgänge direkt in jeder MCP-kompatiblen Anwendung aufzeigt. Mit der Real-Time CDP MCP-Integration können verschiedene Benutzertypen um dieselben Segmentierungs- und Aktivierungsdaten zusammenarbeiten, ohne Abfragen an den Adobe Experience Platform REST-APIs zu schreiben oder durch mehrere Bildschirme der Benutzeroberfläche zu navigieren. Kunden können ihre Absichten im Gespräch beschreiben und das LLM die entsprechenden MCP-Tools aufrufen lassen.

## Wichtigste Funktionen {#mcp-capabilities}

Mit dem Real-Time CDP MCP-Server können Sie Zielgruppen und Ziele direkt über Ihren KI-Assistenten überprüfen, zusammenfassen und Fehler beheben. Alle Vorgänge sind **schreibgeschützt** - Die MCP-Serveroberflächen rufen APIs als Klarsprachenantworten ab, damit Sie Folgendes tun können:

* **Sofortige Sichtbarkeit der Zielgruppe** - Fragen Sie nach Zielgruppendefinitionen, Lebenszyklusstatus und Namespace in einfacher Sprache, ohne in Menüs zu navigieren oder Berichte manuell abzurufen.
* **Geschätzte Zielgruppengröße vor Aktivierung** - Vorschau der Mitgliedschaftsanzahl und Konfidenzintervalle für eine PQL- oder SDD-Segmentabfrage, bevor Sie die Erstellung einer Zielgruppe übernehmen.
* **Überprüfen Sie Ihr Aktivierungsportfolio** - Überprüfen Sie konfigurierte Ziele, die Datenflüsse, die sie speisen, und die Quell-/Zielverbindungen hinter jedem Fluss - ohne JSON zu analysieren oder über Produktbildschirme zu springen.
* **Aktivierungsprobleme frühzeitig erkennen** - Oberfläche fehlgeschlagen oder Ziel wird gerade ausgeführt wird in dem Moment ausgeführt, in dem Sie fragen, damit Ihr Team schnell reagieren kann.
* **Zusammenarbeit rund um Live-Daten** - Marketing-Experten, Dateningenieure und Stakeholder können über ihren KI-Assistenten alle dieselben Live-Real-Time CDP-Daten abfragen, was die Abstimmung, Entscheidung und das Zusammengehen erleichtert.

## Verfügbare Tools {#mcp-tools}

Die folgenden Tools werden vom Real-Time CDP MCP-Server bereitgestellt:

| Tool | Beschreibung |
| --- | --- |
| **Durchsuchen vorhandener Zielgruppen** | Auflisten von Zielgruppen mit optionalen Filtern (Name, Entitätstyp, Lebenszyklusstatus, Namespace, Herkunft) oder Abrufen einer bestimmten Zielgruppe nach ID. |
| **Vorschau der Zielgruppenzugehörigkeit** | Schätzen der Größe einer Segmentabfrage (PQL für Profil-Zielgruppen, SDD für relationale/Konto-Zielgruppen) einschließlich Metadaten für Konfidenzintervalle. |
| **Zieltypen auflisten** | Den Katalog der in Ihrer Sandbox verfügbaren Ziel-Connector-Typen anzeigen. |
| **Auflisten der konfigurierten Konten** | Konfigurierte Zielkonten (Basisverbindungen) und deren Authentifizierungsdetails durchsuchen. |
| **Auflisten der konfigurierten Ziele** | Durchsuchen von Ziel-Datenflüssen, filterbar nach Name, Status, Flussspezifikation oder Quell-/Zielverbindung. |
| **Source-Verbindungen auflisten** | Überprüfen Sie Quellverbindungen, die die Informationen zur Datensatzzuordnung für einen Zieldatenfluss enthalten. |
| **Auflisten der Zielverbindungen** | Überprüfen Sie Zielverbindungen, die die Datenformat- und Pfadkonfiguration für ein Ziel enthalten. |
| **Überprüfen von Aktivierungsläufen** | Überprüfen des Ausführungsverlaufs des Ziel-Datenflusses, filtrierbar nach Fluss-ID, Status (Erfolg, fehlgeschlagen, in Bearbeitung) und Abschlusszeitbereich. |

>[!NOTE]
>
>Alle Tools sind **schreibgeschützt**. Schreibvorgänge (Erstellen, Aktualisieren oder Löschen von Zielgruppen, Zielen oder Datenflüssen) werden in der aktuellen Beta-Version nicht unterstützt.

## Anwendungsfälle {#mcp-use-cases}

Die folgenden Beispiele zeigen, wie Sie mit dem [!DNL Adobe Real-Time CDP] MCP-Server in natürlicher Sprache interagieren:

| Ziel | Beispiel-Eingabeaufforderung |
| --- | --- |
| **Zielkatalogerkennung** | „Ist TikTok in meiner Sandbox als Ziel verfügbar?“ / „Für welche Zieltypen sind bereits Konten konfiguriert?“ |
| **Zielinventar nach Typ** | „Listen Sie alle meine Amazon S3-Ziele auf.“ / „Habe ich Ziele für den Datensatzexport eingerichtet?“ |
| **Zielkonfigurations-Audit** | „In welchen Bucket schreibt mein `Loyalty S3 Export`?“ / „Anzeigen des Zielpfads und des Dateiformats für den Datenfluss [ID]&quot; |
| **Kontenstatus** | „Welche meiner Zielkonten verfügen über abgelaufene Anmeldedaten?“ / „Gibt es Pinterest- oder Facebook-Konten mit einem Fehlerstatus?“ |
| **Aktivierungszustand — letzte 24 Stunden** | „Listen Sie jedes Ziel mit einem fehlgeschlagenen Durchlauf in den letzten 24 Stunden auf.“ / „Hat mein Datensatzexportziel in den letzten 24 Stunden Daten gesendet?“ |
| **Aktivierungsverlauf nach Ziel** | „Haben `Weekly Loyalty Export` in den letzten 30 Tagen etwas exportiert?“ / „Anzeigen des vollständigen Ausführungsverlaufs für {NAME}&quot; |
| **Fehleranalyse** | „Was ist die häufigste Fehlerursache bei meinen dateibasierten Zielen diese Woche?“ / „Letzte fehlgeschlagene Ausführungen nach Fehlertyp gruppieren.“ |
| **Zielgruppenerkennung und -filterung** | „Listet alle CSV-basierten Zielgruppen in der `marketing-prod` Sandbox auf.“ / „Für welche Zielgruppen ist eine externe Zielgruppen-ID definiert?“ |
| **Audience-Größenprüfung** | „Zeigen Sie mir alle Zielgruppen mit Größe 0.“ / „Welche Zielgruppen sind größer als 1.000 Profile?“ |
| **Audience-Ablaufprüfung** | „Welche Ziele haben Zielgruppen, deren Enddatum bereits verstrichen ist?“ / „Auflisten der Zielgruppen, die in den nächsten sieben Tagen ablaufen werden.“ |
| **Zielgruppenaktivierungs-Footprint** | „Für welche Ziele sind mehr als 10 Zielgruppen aktiviert?“ / „Welche Zielgruppe wird für die meisten Ziele aktiviert?“ |
| **Cross-Filter: Audience × Activation** | „Zeigen Sie mir Zielgruppen mit einer Größe von mehr als 1.000, die für mindestens zwei Ziele aktiviert sind.“ / „Große Zielgruppen, die nur für ein einzelnes Ziel aktiviert sind.“ |
| **Vorschau der Zielgruppenzugehörigkeit** | „Zeigen Sie eine Vorschau der Mitgliedschaftsgröße für Zielgruppen-`High-Value Loyalty Members` an.“ / „Schätzen Sie die Größe dieser PQL-Abfrage, bevor ich sie speichere: {EXPRESSION}.“ |

## Voraussetzungen {#mcp-prerequisites}

Stellen Sie vor dem Verbinden des Real-Time CDP-MCP-Servers mit dem MCP-Client Folgendes sicher:

* Sie besitzen eine aktive Real-Time CDP-Lizenz.
* Sie haben Zugriff auf einen unterstützten Client, der eine Verbindung zu einem Remote-MCP-Server oder einer benutzerdefinierten MCP-App herstellen kann, z. B. Claude, ChatGPT, Claude Code, Codex, Cursor oder VS-Code.
* Sie haben Ihre Organisations-ID und den Namen der Sandbox, die Sie abfragen möchten.
* Sie verfügen in Adobe Experience Platform über die erforderlichen Berechtigungen zum Anzeigen von Zielgruppen, Zielen und Flow Service-Entitäten.

## Real-Time CDP MCP-Server verbinden {#mcp-connect}

>[!NOTE]
>
>Diese Integration befindet sich in Beta. Client-Menüs, Plananforderungen und Admin-Steuerelemente können je nach Anwendung und Version variieren.

Bevor Sie beginnen, stellen Sie Folgendes sicher:

* Die MCP-Server-Endpunkt-URL: `https://rtcdp-mcp.adobe.io/mcp`.
* Bestätigung, dass Ihre Adobe-Benutzenden Zugriff auf die Experience Platform-Zielorganisation und -Sandbox haben.

Der Real-Time CDP-MCP-Server ist ein **Remote-HTTP-MCP-Server**. In jedem Client folgt die Einrichtung dem gleichen Muster:

1. Hinzufügen der Server-URL.
2. Speichern oder aktivieren Sie die Verbindung.
3. Schließen Sie die **Browser-basierte Adobe-Anmeldung** ab, wenn der Client zum ersten Mal ein Tool aufruft.
4. Geben Sie bei jeder Anfrage `imsOrgId` und `sandboxName` an.

### Installieren in benutzeroberflächenbasierten Clients {#mcp-connect-ui}

#### Claude

Fügen Sie für `claude.ai` und Claude Desktop den Real-Time CDP-MCP-Server als **benutzerdefinierten Connector)** Verwendung von `https://rtcdp-mcp.adobe.io/mcp` hinzu. Fügen Sie es in einzelnen Claude-Plänen unter &quot;**&quot; > „Connectoren“**. In Team- und Enterprise-Plänen muss ein Eigentümer sie möglicherweise zuerst unter **Organisationseinstellungen > Connectoren** hinzufügen. Danach verbindet ihn jeder Benutzer in seinen eigenen Claude-Einstellungen. Aktivieren Sie nach der Konfiguration den Connector in einer Konversation und schließen Sie die Adobe-Browser-Anmeldung bei der ersten Verwendung ab.

#### ChatGPT

Fügen Sie in ChatGPT den Real-Time CDP-MCP-Server als **benutzerdefinierte App/Connector** mithilfe von `https://rtcdp-mcp.adobe.io/mcp` hinzu. Abhängig von Ihrem ChatGPT-Plan kann dies die Genehmigung **Entwicklermodus** und des Arbeitsbereich-Administrators erfordern. Nachdem die App/der Connector erstellt oder aktiviert wurde, verbinden Sie sie über **Einstellungen > Apps** oder **Einstellungen > Apps und Connectoren** und authentifizieren Sie sich über die Adobe-Browser-Anmeldung, wenn Sie dazu aufgefordert werden.

#### Andere benutzeroberflächenbasierte Clients

Fügen Sie für Clients wie Cursor, VS Code oder andere Desktop- und Web-Anwendungen mit Remote-MCP-Unterstützung den Real-Time CDP MCP-Server als **Remote-HTTP**-Server hinzu und verwenden Sie `https://rtcdp-mcp.adobe.io/mcp`. Wenn der Client optionale Kopfzeilen oder Bearer-Token unterstützt, lassen Sie diese leer, es sei denn, Adobe erteilt ausdrücklich eine andere Anweisung. Die Authentifizierung wird bei der ersten Verwendung über den browserbasierten Adobe-Anmeldefluss durchgeführt.

### Installation in technischen Clients {#mcp-connect-technical}

#### Claude Code

Fügen Sie den Server vom Terminal aus hinzu:

```bash
claude mcp add --transport http rtcdp https://rtcdp-mcp.adobe.io/mcp
```

Starten Sie dann Claude Code und führen Sie Folgendes aus:

```text
/mcp
```

Wählen Sie den `rtcdp` aus und schließen Sie den Anmeldevorgang für Adobe in Ihrem Browser ab. Wenn Sie den Server bereits in `claude.ai` hinzugefügt haben, kann er auch automatisch im Claude-Code angezeigt werden, wenn beide dasselbe Konto verwenden.

#### Codex

Fügen Sie den Server vom Terminal aus hinzu:

```bash
codex mcp add rtcdp --url https://rtcdp-mcp.adobe.io/mcp
```

Server authentifizieren:

```bash
codex mcp login rtcdp
```

Überprüfen Sie die Konfiguration:

```bash
codex mcp list
```

Sie können den Server auch direkt zu `~/.codex/config.toml` hinzufügen:

```toml
[mcp_servers.rtcdp]
url = "https://rtcdp-mcp.adobe.io/mcp"
```

### Erforderliche Anfrageparameter {#mcp-connect-params}

Jeder Tool-Aufruf erfordert zwei Parameter, die den Umfang der Anfrage festlegen:

* `imsOrgId` - Ihre Organisations-ID, die der `x-gw-ims-org-id`-Kopfzeile bei nachgelagerten Experience Platform-API-Aufrufen zugeordnet ist.
* `sandboxName` - Der Experience Platform-Sandbox-Name, der der `x-sandbox-name`-Kopfzeile zugeordnet ist.

## Bekannte Einschränkungen (Beta) {#mcp-limitations}

Die folgenden Einschränkungen gelten für die aktuelle Beta-Version des [!DNL Adobe Real-Time CDP] MCP-Servers:

| Einschränkung | Beschreibung | Problemumgehung |
| --- | --- | --- |
| **Schreibgeschützte Oberfläche** | Der MCP-Server stellt nur APIs zum Abrufen bereit. Zielgruppen, Ziele oder Datenflüsse können nicht erstellt, aktualisiert, aktiviert oder gelöscht werden. | Verwenden Sie die Real-Time CDP-Benutzeroberfläche oder die AEP-REST-APIs für Schreibvorgänge. |
| **Keine Interaktions- oder Versandmetriken** | Der MCP-Server gibt keine nachgelagerten Versandstatistiken, Interaktions- oder Konversionsmetriken von Zielplattformen zurück. | Verwenden Sie die eigenen Berichte der Zielplattform, Customer Journey Analytics MCP oder Adobe Analytics MCP für Interaktions- und Konversionsdaten. |
| **Segmentabfrage muss extern erstellt werden** | `Preview Audience Membership` erfordert einen gültigen PQL- oder SDD-Ausdruck als Eingabe. Der MCP-Server erstellt die Abfrage nicht für Sie. | Erstellen Sie den PQL/SDD-Ausdruck in der Segment Builder-Benutzeroberfläche oder über die Segmentierungs-Service-API und fügen Sie ihn dann in die MCP-Eingabeaufforderung ein. |
| **Paginierung über Fortsetzungs-Token** | Listen-Tools geben paginierte Ergebnisse zurück. Für eine vollständige Auflistung über sehr große Sandboxes müssen `continuationToken` verkettet werden. | Engen Sie Abfragen mithilfe von Filtern (Name, Status, Verbindungsspezifikation, Zeitraum) ein, anstatt die vollständige Liste aufzuzählen. |
| **Die Filterung des Aktivierungsdurchgangs ist nur zeitbasiert** | `Inspect Activation Runs` unterstützt das Filtern nach Status und Abschlusszeitstempel (Epoche ms UTC), jedoch nicht direkt nach Fehlertyp oder Zielplattform. | Filtern Sie nach `flowId` ersten (von `List Configured Destinations` abgerufenen) Durchläufen zum Bereich, der für ein bestimmtes Ziel bestimmt ist. |
| **Regionskonfiguration erforderlich** | Tool-Aufrufe schlagen mit HTTP 403 „Benutzerregion fehlt“ fehl, wenn das MCP-Gateway für die Region Ihres Benutzers nicht konfiguriert ist. | Wenden Sie sich vor der ersten Verwendung an den Adobe-Support, um zu bestätigen, dass das Gateway für Ihre Region konfiguriert ist. |

## Häufig gestellte Fragen {#mcp-faq}

+++Welche MCP-Clients werden unterstützt?

Der Real-Time CDP MCP-Server arbeitet mit unterstützten Clients, die eine Verbindung zu Remote-MCP-Servern oder benutzerdefinierten MCP-Apps herstellen können - einschließlich Claude, ChatGPT, Claude Code, Codex, Cursor und VS-Code. Der Einrichtungsfluss hängt vom Client ab: Benutzeroberflächenbasierte Clients fügen den Server normalerweise aus den Einstellungen hinzu, während technische Clients wie Claude Code und Codex ihn aus der Befehlszeile oder den Konfigurationsdateien hinzufügen können.
+++

+++Wie funktioniert die Authentifizierung?

Die Authentifizierung erfolgt über eine **Browser-basierte Anmeldung**. Wenn Ihr MCP-Client zum ersten Mal ein Tool aufruft, wird Ihr Standardbrowser auf einer Adobe-Anmeldeseite geöffnet. Nachdem Sie sich authentifiziert und den Client autorisiert haben, wird die Sitzung eingerichtet und die nachfolgenden Tool-Aufrufe verwenden sie erneut. In Ihrer Client-Konfiguration müssen keine API-Schlüssel oder langlebigen Anmeldedaten gespeichert werden.
+++

+++Auf welche Real-Time CDP-Objekte kann ich über MCP zugreifen?

Sie können auf Zielgruppen, Zieltypen, konfigurierte Zielkonten, Zieldatenflüsse, Quell- und Zielverbindungen und den Ausführungsverlauf der Aktivierung zugreifen. Vorgänge sind schreibgeschützt (APIs abrufen); Schreibvorgänge werden in der aktuellen Version nicht unterstützt.
+++

+++Benötige ich Entwicklerzugriff, um den Real-Time CDP MCP-Server zu verwenden?

Nein. Der MCP-Server ist sowohl für Marketing- als auch für technische Personas konzipiert. Marketing-Experten können mit ihr über natürliche Spracheingaben in jedem unterstützten MCP-Client interagieren, während Dateningenieure und Entwickler sie in Entwickler-Tools verwenden können, die MCP unterstützen.
+++

+++Werden meine Daten an den MCP Client Provider gesendet?

Wenn Sie eine Eingabeaufforderung senden, kann der MCP-Client den entsprechenden Kontext (einschließlich der vom MCP-Server zurückgegebenen Real-Time CDP-Daten) zur Verarbeitung an sein Modell senden. Überprüfen Sie die Datenschutz- und Datenverarbeitungsrichtlinien Ihres MCP-Client-Anbieters, bevor Sie eine Verbindung zu Produktionsdaten herstellen.
+++

+++Welche Berechtigungen benötige ich in Real-Time CDP?

Sie benötigen mindestens **Anzeigen**-Berechtigungen für die Objekte, die Sie abfragen möchten - Zielgruppen, Ziele und Flow Service-Entitäten. Es sind keine Schreibberechtigungen erforderlich, da der MCP-Server nur Lesevorgänge ausführt. Wenden Sie sich an Ihren [!DNL Adobe Experience Platform], wenn Sie sich bezüglich Ihrer aktuellen Zugriffsebene nicht sicher sind.
+++

+++Kann ich den MCP-Server in Sandbox-Umgebungen verwenden?

Ja. Jeder Tool-Aufruf erfordert einen `sandboxName`, sodass der MCP-Server immer die [!DNL Adobe Experience Platform] Sandbox-Konfiguration berücksichtigt. Sie können jede Sandbox abfragen, auf die Sie Zugriff haben, indem Sie ihren Namen in der Eingabeaufforderung angeben.
+++

+++Was ist der Unterschied zwischen der Vorschau-Zielgruppenzugehörigkeit und der Suche nach bestehenden Zielgruppen?

`Search Existing Audiences` gibt Zielgruppen zurück, die bereits in Ihrer Sandbox erstellt und gespeichert wurden. `Preview Audience Membership` verwendet einen rohen PQL- oder SDD-Segmentausdruck und gibt eine Größenschätzung dafür zurück. Dies ist nützlich für die Dimensionierung einer Abfrage *vor* wenn Sie sie als Zielgruppe speichern.
+++

+++Kann ich Konto- sowie Profil-Audiences abfragen?

Ja. Sowohl `Search Existing Audiences` als auch `Preview Audience Membership` unterstützen einen Entitätstypparameter. Profil-Zielgruppen können in PQL oder SDD ausgedrückt werden. Konto-Zielgruppen verwenden immer die SDD-Syntax (relationale Syntax).
+++
