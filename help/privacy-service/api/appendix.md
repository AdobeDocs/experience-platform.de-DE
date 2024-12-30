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
ht-degree: 6%

---

# Anhang zum Privacy Service-API-Handbuch

Die folgenden Abschnitte enthalten zusätzliche Informationen zur Arbeit mit der Adobe Experience Platform Privacy Service-API.

## Standard-Identity-Namespaces {#standard-namespaces}

Alle Identitäten, die an [!DNL Privacy Service] gesendet werden, müssen unter einem bestimmten Identity-Namespace bereitgestellt werden. Identity-Namespaces sind eine Komponente von [Adobe Experience Platform Identity Service](../../identity-service/home.md) die den Kontext angeben, auf den sich eine Identität bezieht.

In der folgenden Tabelle sind einige häufig verwendete, vordefinierte Identitätstypen aufgeführt, die von [!DNL Experience Platform] bereitgestellt werden, zusammen mit den zugehörigen `namespace`:

| Identitätstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-Mail | `Email` | `6` |
| Telefon | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| [!DNL Apple]-ID für Werbetreibende | `IDFA` | `20915` |
| [!DNL Google]-ID | `GAID` | `20914` |
| [!DNL Windows] | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Jeder Identitätstyp verfügt außerdem über einen `namespaceId` ganzzahligen Wert, der anstelle der `namespace` Zeichenfolge verwendet werden kann, wenn die `type` Eigenschaft der Identität auf „namespaceId“ festgelegt wird. Weitere Informationen finden Sie im Abschnitt [Namespacequalifizierer](#namespace-qualifiers).

Sie können eine Liste der von Ihrem Unternehmen verwendeten Identity-Namespaces abrufen, indem Sie eine GET-Anfrage an den `idnamespace/identities`-Endpunkt in der [!DNL Identity Service]-API stellen. Weitere Informationen finden Sie [Identity Service](../../identity-service/api/getting-started.md)Entwicklerhandbuch).

## Namespace-Qualifizierer

Beim Angeben eines `namespace` in der [!DNL Privacy Service]-API muss **(Namespace-**) in einen entsprechenden `type` eingefügt werden. In der folgenden Tabelle sind die verschiedenen zulässigen Namespace-Qualifizierer aufgeführt.

| Qualifizierer | Definition |
| --------- | ---------- |
| `standard` | Einer der global definierten Standard-Namespaces, die nicht an einen einzelnen Unternehmensdatensatz gebunden sind (z. B. E-Mail, Telefonnummer usw.). Namespace-ID angegeben. |
| `custom` | Ein eindeutiger Namespace, der im Kontext einer Organisation erstellt und nicht über die [!DNL Experience Cloud] hinweg freigegeben wird. Der Wert stellt den Anzeigenamen („name“-Feld) dar, nach dem gesucht werden soll. Namespace-ID angegeben. |
| `integrationCode` | Integrations-Code - ähnlich wie „custom“, aber speziell definiert als der Integrations-Code einer zu suchenden Datenquelle. Namespace-ID angegeben. |
| `namespaceId` | Gibt an, dass der Wert die tatsächliche ID des Namespace ist, der über den Namespace-Service erstellt oder zugeordnet wurde. |
| `unregistered` | Eine Freiformzeichenfolge, die nicht im Namespace-Service definiert ist und unverändert übernommen wird. Jede Anwendung, die diese Art von Namespaces verarbeitet, vergleicht sie und verarbeitet sie, sofern für den Unternehmenskontext und den Datensatz geeignet. Es wird keine Namespace-ID angegeben. |
| `analytics` | Ein benutzerdefinierter Namespace, der intern in [!DNL Analytics] und nicht im Namespace-Service zugeordnet ist. Dieser wird direkt, wie in der ursprünglichen Anfrage angegeben, ohne Namespace-ID übergeben |
| `target` | Ein benutzerdefinierter Namespace, der intern von [!DNL Target] verstanden wird, nicht im Namespace-Service. Dieser wird direkt, wie in der ursprünglichen Anfrage angegeben, ohne Namespace-ID übergeben |

{style="table-layout:auto"}

## Akzeptierte Produktwerte

In der folgenden Tabelle sind die akzeptierten Werte für die Angabe eines Adobe-Produkts im `include` einer Vorgangserstellungsanfrage aufgeführt.

>[!NOTE]
>
>Bei den Werten für die Liste der Produkte wird nicht zwischen Groß- und Kleinschreibung unterschieden. Camel-Case wird empfohlen, aber nicht erzwungen.

| Produkt | Wert zur Verwendung im `include` |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (Echtzeit-Kundenprofil) | `profileService` |
| Adobe Pass-Authentifizierung | `primetimeAuthentication` |
| Adobe Target | `target` |
| Kundenattribute (CRM) | `CRS` |
| Kunden-Journey-Management | `cjm` |
| Identity Service | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
