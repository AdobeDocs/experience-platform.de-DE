---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Anhang zum Privacy Service-API-Handbuch
topic-legacy: developer guide
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Privacy Service-API.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: a4f6801cc85624274716889bdda0146fa38eb4b7
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 9%

---

# Anhang zum Handbuch zur Privacy Service-API

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit der Adobe Experience Platform Privacy Service-API.

## Standardmäßige Identitäts-Namespaces {#standard-namespaces}

Alle Identitäten, die an [!DNL Privacy Service] gesendet werden, müssen unter einem bestimmten Identitäts-Namespace bereitgestellt werden. Identitäts-Namespaces sind eine Komponente von [Adobe Experience Platform Identity Service](../../identity-service/home.md) , die den Kontext angibt, auf den sich eine Identität bezieht.

In der folgenden Tabelle sind mehrere häufig verwendete, vordefinierte Identitätstypen aufgeführt, die von [!DNL Experience Platform] bereitgestellt werden, zusammen mit den zugehörigen `namespace`-Werten:

| Identitätstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-Mail  | `Email` | `6` |
| Telefon | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] ID für Advertisers | `IDFA` | `20915` |
| [!DNL Google] Anzeigen-ID | `GAID` | `20914` |
| [!DNL Windows] BEIHILFE | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Jeder Identitätstyp hat auch einen Integer-Wert `namespaceId`, der anstelle der Zeichenfolge `namespace` verwendet werden kann, wenn die `type` -Eigenschaft der Identität auf &quot;namespaceId&quot;gesetzt wird. Weitere Informationen finden Sie im Abschnitt [Namespace-Qualifikatoren](#namespace-qualifiers) .

Sie können eine Liste der von Ihrem Unternehmen verwendeten Identitäts-Namespaces abrufen, indem Sie eine GET-Anfrage an den Endpunkt `idnamespace/identities` in der API [!DNL Identity Service] stellen. Weitere Informationen finden Sie im [Entwicklerhandbuch für Identity Service](../../identity-service/api/getting-started.md).

## Namespace-Kennungen

Bei der Angabe eines `namespace`-Werts in der [!DNL Privacy Service]-API muss ein **Namespace-Qualifizierer** in einem entsprechenden `type`-Parameter enthalten sein. In der folgenden Tabelle sind die verschiedenen akzeptierten Namespace-Qualifikatoren aufgeführt.

| Qualifizierer | Definition |
| --------- | ---------- |
| `standard` | Einer der Standard-Namespaces, der global definiert wird und nicht an einen bestimmten Datensatz der Organisation gebunden ist (z. B. E-Mail, Telefonnummer usw.). Namespace-ID wird bereitgestellt. |
| `custom` | Ein eindeutiger Namespace, der im Kontext einer Organisation erstellt wurde und nicht über [!DNL Experience Cloud] freigegeben wurde. Der Wert stellt den Anzeigenamen (&quot;name&quot;-Feld) dar, nach dem gesucht werden soll. Namespace-ID wird bereitgestellt. |
| `integrationCode` | Integrationscode - ähnlich wie &quot;benutzerdefiniert&quot;, jedoch speziell definiert als Integrationscode einer zu suchenden Datenquelle. Namespace-ID wird bereitgestellt. |
| `namespaceId` | Gibt an, dass der Wert die tatsächliche ID des Namespace ist, der über den Namespace-Dienst erstellt oder zugeordnet wurde. |
| `unregistered` | Eine Freiform-Zeichenfolge, die nicht im Namespace-Dienst definiert ist und &quot;unverändert&quot;angewendet wird. Jede Anwendung, die diese Arten von Namespaces verarbeitet, überprüft sie und behandelt sie gegebenenfalls für den Unternehmenskontext und den Datensatz. Es wird keine Namespace-ID angegeben. |
| `analytics` | Ein benutzerdefinierter Namespace, der intern in [!DNL Analytics] und nicht im Namespace-Dienst zugeordnet wird. Dies wird direkt übergeben, wie von der ursprünglichen Anfrage angegeben, ohne Namespace-ID |
| `target` | Ein benutzerdefinierter Namespace, der intern von [!DNL Target] verstanden wird, nicht im Namespace-Dienst. Dies wird direkt übergeben, wie von der ursprünglichen Anfrage angegeben, ohne Namespace-ID |

{style=&quot;table-layout:auto&quot;}

## Angenommene Produktwerte

In der folgenden Tabelle sind die zulässigen Werte für die Angabe eines Adobe-Produkts im Attribut `include` einer Anforderung zur Auftragserstellung aufgeführt.

| Produkt | Wert zur Verwendung im Attribut `include` |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform | `AdobeCloudPlatform` |
| Adobe Primetime-Authentifizierung | `primetimeAuthentication` |
| Adobe Target | `target` |
| Automatisierungsprodukt | `automationProduct` |
| Kundenattribute (CRS) | `CRS` |
| Echtzeit-Kundenprofil | `profileService` |

{style=&quot;table-layout:auto&quot;}