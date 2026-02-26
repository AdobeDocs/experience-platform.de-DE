---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Anhang zum Privacy Service-API-Handbuch
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Privacy Service-API.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 9b3fb0d545408369d96a3fc7c5c6e9c098af9933
workflow-type: tm+mt
source-wordcount: '552'
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
| Adobe Advertising Cloud-ID | `AdCloud` | `411` |
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

## Namespace-Qualifizierer {#namespace-qualifiers}

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

## Akzeptierte Produktwerte {#accepted-product-values}

In diesem Abschnitt werden die Produktkennungswerte aufgelistet, die beim Erstellen von Privacy Service-Aufträgen (API oder Benutzeroberfläche) im `include` akzeptiert werden. Verwenden Sie diese Werte im `include`-Array Ihrer Vorgangsanfrage.

In der folgenden Tabelle sind die unterstützten Produkte, ihre Anzeigenamen in der Benutzeroberfläche und die entsprechenden Codewerte aufgeführt.

>[!NOTE]
>
>- Bei Produktwerten wird nicht zwischen Groß- und Kleinschreibung unterschieden. Aus Konsistenzgründen wird die Groß-/Kleinschreibung von Camel empfohlen.
>- Nur die oben aufgeführten Produkte werden in der Benutzeroberfläche und API unterstützt. Wenn ein Produkt nicht für Ihr Unternehmen bereitgestellt wurde, kann es ignoriert werden oder einen Validierungsfehler verursachen. Informationen zur Bestätigung der Berechtigung finden Sie in der Adobe-Vertrags- oder Bereitstellungsdokumentation.

| Name des Markenprodukts | Anzeigename der Benutzeroberfläche | Wert `include` |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform (Profilspeicher) | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform (Data Lake) | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| Kundenattribute | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| Identity Service | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
