---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Anhang zum Privacy Service-API-Handbuch
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Privacy Service-API.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 7%

---

# Anhang zum Privacy Service API-Handbuch

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit der Adobe Experience Platform Privacy Service-API.

## Standardmäßige Identitäts-Namespaces {#standard-namespaces}

Alle Identitäten, die an gesendet werden [!DNL Privacy Service] muss unter einem bestimmten Identitäts-Namespace angegeben werden. Identity-Namespaces sind eine Komponente von [Adobe Experience Platform Identity-Dienst](../../identity-service/home.md) , der den Kontext angibt, auf den sich eine Identität bezieht.

In der folgenden Tabelle sind mehrere häufig verwendete, vordefinierte Identitätstypen aufgeführt, die von [!DNL Experience Platform]zusammen mit den zugehörigen `namespace` -Werte:

| Identitätstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-Mail | `Email` | `6` |
| Telefon | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| [!DNL Apple] ID für Advertiser | `IDFA` | `20915` |
| [!DNL Google] Anzeigen-ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Jeder Identitätstyp verfügt auch über eine `namespaceId` ganzzahliger Wert, der anstelle der `namespace` Zeichenfolge beim Festlegen der `type` -Eigenschaft auf &quot;namespaceId&quot;gesetzt. Siehe Abschnitt zu [Namespace-Qualifikatoren](#namespace-qualifiers) für weitere Informationen.

Sie können eine Liste der von Ihrem Unternehmen verwendeten Identitäts-Namespaces abrufen, indem Sie eine GET-Anfrage an die `idnamespace/identities` -Endpunkt im [!DNL Identity Service] API. Siehe [Entwicklerhandbuch für Identity Service](../../identity-service/api/getting-started.md) für weitere Informationen.

## Namespace-Kennungen

Beim Festlegen einer `namespace` Wert in [!DNL Privacy Service] API, eine **Namespace-Qualifizierer** muss in einem entsprechenden `type` -Parameter. In der folgenden Tabelle sind die verschiedenen akzeptierten Namespace-Qualifikatoren aufgeführt.

| Qualifizierer | Definition |
| --------- | ---------- |
| `standard` | Einer der Standard-Namespaces, der global definiert wird und nicht an einen bestimmten Datensatz der Organisation gebunden ist (z. B. E-Mail, Telefonnummer usw.). Namespace-ID wird bereitgestellt. |
| `custom` | Ein eindeutiger Namespace, der im Kontext einer Organisation erstellt wurde und nicht über die [!DNL Experience Cloud]. Der Wert stellt den Anzeigenamen (&quot;name&quot;-Feld) dar, nach dem gesucht werden soll. Namespace-ID wird bereitgestellt. |
| `integrationCode` | Integrationscode - ähnlich wie &quot;benutzerdefiniert&quot;, jedoch speziell definiert als Integrationscode einer zu suchenden Datenquelle. Namespace-ID wird bereitgestellt. |
| `namespaceId` | Gibt an, dass der Wert die tatsächliche ID des Namespace ist, der über den Namespace-Dienst erstellt oder zugeordnet wurde. |
| `unregistered` | Eine Freiform-Zeichenfolge, die nicht im Namespace-Dienst definiert ist und &quot;unverändert&quot;angewendet wird. Jede Anwendung, die diese Arten von Namespaces verarbeitet, überprüft sie und behandelt sie gegebenenfalls für den Unternehmenskontext und den Datensatz. Es wird keine Namespace-ID angegeben. |
| `analytics` | Ein benutzerdefinierter Namespace, der intern in [!DNL Analytics], nicht im Namespace-Dienst. Dies wird direkt wie in der ursprünglichen Anfrage angegeben ohne Namespace-ID übergeben. |
| `target` | Ein benutzerdefinierter Namespace, der intern von [!DNL Target], nicht im Namespace-Dienst. Dies wird direkt wie in der ursprünglichen Anfrage angegeben ohne Namespace-ID übergeben. |

{style="table-layout:auto"}

## Angenommene Produktwerte

In der folgenden Tabelle sind die zulässigen Werte für die Angabe eines Adobe-Produkts im `include` -Attribut einer Anforderung zur Auftragserstellung.

>[!NOTE]
>
>Bei den Werten für die Produktliste wird nicht zwischen Groß- und Kleinschreibung unterschieden. Camel-Case wird empfohlen, aber nicht erzwungen.

| Produkt | Wert zur Verwendung in `include` attribute |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (Echtzeit-Kundenprofil) | `profileService` |
| Adobe Pass-Authentifizierung | `primetimeAuthentication` |
| Adobe Target | `target` |
| Kundenattribute (CRS) | `CRS` |
| Journey-Management von Kunden | `cjm` |
| Identity Service | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
