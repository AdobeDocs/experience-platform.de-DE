---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Privacy Service-API-Handbuch
topic-legacy: developer guide
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Privacy Service-API.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
translation-type: tm+mt
source-git-commit: 545ac984d9f9f540fc9121214d40719f9a254379
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Handbuch zur Privacy Service-API

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit der Adobe Experience Platform Privacy Service API.

## Standard-Identitäts-Namensraum {#standard-namespaces}

Alle Identitäten, die an [!DNL Privacy Service] gesendet werden, müssen unter einem bestimmten Identitäts-Namensraum angegeben werden. Identity Namensraums sind eine Komponente von [Adobe Experience Platform Identity Service](../../identity-service/home.md), die den Kontext angibt, auf den sich eine Identität bezieht.

In der folgenden Tabelle sind einige häufig verwendete, vordefinierte Identitätstypen, die von [!DNL Experience Platform] zur Verfügung gestellt werden, zusammen mit den zugehörigen `namespace`-Werten aufgeführt:

| Identitätstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-Mail  | E-Mail | 6 |
| Telefon | Telefon | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] ID für Advertisers | IDFA | 20915 |
| [!DNL Google] Anzeigen-ID | GAID | 20914 |
| [!DNL Windows] BEIHILFE | WAID | 8 |

>[!NOTE]
>
>Jeder Identitätstyp verfügt auch über den ganzzahligen Wert `namespaceId`, der anstelle der `namespace`-Zeichenfolge verwendet werden kann, wenn die `type`-Eigenschaft der Identität auf &quot;namespaceId&quot;gesetzt wird. Weitere Informationen finden Sie im Abschnitt [Namensraum qualifiers](#namespace-qualifiers).

Sie können eine Liste von Identitäts-Namensräumen abrufen, die in Ihrem Unternehmen verwendet werden, indem Sie eine GET an den `idnamespace/identities`-Endpunkt in der [!DNL Identity Service]-API anfordern. Weitere Informationen finden Sie im Handbuch [Identitätsdienst-Entwickler](../../identity-service/api/getting-started.md).

## Namensraum-Qualifikatoren

Wenn Sie einen `namespace`-Wert in der [!DNL Privacy Service]-API angeben, muss ein **Namensraum-Qualifizierer** in einem entsprechenden `type`-Parameter enthalten sein. In der folgenden Tabelle sind die verschiedenen zulässigen Namensraum-Qualifikatoren aufgeführt.

| Qualifizierer | Definition |
| --------- | ---------- |
| Standard | Einer der weltweit definierten Standard-Namensraum, der nicht an einen unternehmensspezifischen Datensatz gebunden ist (z. B. E-Mail, Telefonnummer usw.). Namensraum-ID angegeben. |
| custom | Ein eindeutiger Namensraum, der im Kontext einer Organisation erstellt wurde und nicht über das [!DNL Experience Cloud] freigegeben wurde. Der Wert stellt den Anzeigenamen (&quot;Namensfeld&quot;) dar, nach dem gesucht werden soll. Namensraum-ID angegeben. |
| integrationCode | Integrationscode - ähnlich wie &quot;benutzerspezifisch&quot;, aber spezifisch definiert als Integrationscode einer zu durchsuchenden Datenquelle. Namensraum-ID angegeben. |
| namespaceId | Gibt die tatsächliche ID des Namensraums an, der über den Namensraum-Dienst erstellt oder zugeordnet wurde. |
| nicht registriert | Eine Freiformzeichenfolge, die nicht im Namensraum-Dienst definiert ist und als &quot;wie vorhanden&quot;gilt. Jede Anwendung, die mit solchen Namensräumen umgeht, überprüft diese und verarbeitet sie gegebenenfalls für den Kontext und den Datensatz der Firma. Es wird keine Namensraum-ID angegeben. |
| analytics | Ein benutzerdefinierter Namensraum, der intern in [!DNL Analytics] und nicht im Namensraum-Dienst zugeordnet wird. Dies wird direkt wie von der ursprünglichen Anforderung angegeben ohne Namensraum-ID weitergeleitet |
| target | Ein benutzerdefinierter Namensraum, der intern von [!DNL Target] verstanden wird, nicht im Namensraum-Dienst. Dies wird direkt wie von der ursprünglichen Anforderung angegeben ohne Namensraum-ID weitergeleitet |

## Akzeptierte Produktwerte

In der folgenden Tabelle sind die für die Angabe eines Adobe-Produkts im `include`-Attribut einer Auftragserstellungsanforderung zulässigen Werte aufgeführt.

| Produkt | Wert für die Verwendung im `include`-Attribut |
| --- | --- |
| Adobe Advertising Cloud | `AdCloud` |
| Adobe Analytics | `Analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `Campaign` |
| Adobe Experience Platform | `aepDataLake` |
| Adobe Primetime-Authentifizierung | `primetimeAuthentication` |
| Adobe Target | `Target` |
| Customer Record Service | `CRS` |
| Echtzeit-Kundenprofil | `ProfileService` |
