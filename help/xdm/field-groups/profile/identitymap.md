---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemas;Schemata;identityMap;identität zuordnen;Identität zuordnen;Schema-Design;map;Map;Vereinigungsschema;Vereinigung
title: Schemafeldgruppe für IdentityMap
description: Erfahren Sie mehr über die Klasse XDM Individual Profile .
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 76%

---

# Schemafeldgruppe für [!UICONTROL IdentityMap] 

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL IdentityMap] ist eine standardmäßige Schemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Die Feldergruppe stellt ein einzelnes Zuordnungsfeld bereit, das eine Reihe von Benutzeridentitäten enthält, die vom Namespace angegeben wurden.

![Ein Diagramm der Schemafeldgruppe [!UICONTROL IdentityMap]](../../images/field-groups/identitymap.png)

Siehe den Abschnitt zu Identitätszuordnungen in [Grundlagen der Schemakomposition](../../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall, einschließlich der Vor- und Nachteile.

**Beispiel**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Weitere Informationen zur Feldergruppe finden Sie im Abschnitt [full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) im öffentlichen XDM-Repository.
