---
description: Skriv till Excell efter en mall
---

# Övning 5

Projektledaren vill ha en Excell med en flik för de filer som inte finns i leveransmappen och att den ska följa mallen som används i uppdraget. Din uppgift är att låta FME använda befintlig mall och format för din Excell-fil.

\
Mall att använda finns i C:\FMEData2025\Data\Informationssamordnare\15\_Kontroll (1568-C1-21-06033\_mall.xlsx).&#x20;

Hur det fungerar:\
FME behöver veta vilka celler som den ska skriva till i din mall. I Excell behöver du därför definiera området i Namnhanteraren under Formler, en så kallad Name range. Döp denna till något lämpligt då den används i skriptet.

\
I ditt skript, lägg till en excell writer och i parameters ange likt nedan:

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Koppla din writer till output-porten för UnmergedRequestor och gå in på writerns\
parametrar. Under writer parameters, ange yes för Overwrite Existing File samt\
ange Template File till mallfilen.

\
I writerns properties, ange I Sheet Name flikens namns nedsträck det du döpte\
Name range till i excell filen (blad1/namn).

\
Under Drop/Truncate sätt Truncate Existing Sheet/Name Range till Yes, den\
andra till No.

\
I fliken User Attributes, se till så att du inte har fler attribut än vad din Name\
Range har.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Klicka OK. Stäng Excellmall-filen (annars failar körnignen) och kör sedan\
skriptet.

