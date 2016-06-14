---
# required metadata

title: [TYTUŁ ARTYKUŁU | NAZWA USŁUGI]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Szablon metadanych i języka Markdown

Ten szablon docs.ms zawiera przykłady składni języka Markdown oraz wytyczne dotyczące konfiguracji metadanych. Jest on dostępny w katalogu głównym każdego repozytorium pilotażu EM (np. ~/Azure-RMSDocs-pr/template.md) i należy go odczytywać jako plik markdown, przy czym można odwołać się do [opublikowanej wersji](https://stage.docs.microsoft.com/en-us/rights-management/template), aby zobaczyć, jak są realizowane przykłady składni języka Markdown.

Podczas tworzenia pliku markdown należy skopiować szablon do nowego pliku, uzupełnić metadane w sposób opisany poniżej, ustawić nagłówek H1 powyżej jako tytuł artykułu i usunąć zawartość. 


## Metadane 

Pełen blok metadanych znajduje się powyżej i jest podzielony na pola wymagane i opcjonalne. Więcej szczegółowych informacji zawiera [arkusz porad związanych z metadanymi OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data). Ważne uwagi:

- Pomiędzy dwukropkiem (:) i wartością elementu metadanych **musi** znajdować się spacja.
- Jeśli opcjonalny element metadanych nie ma wartości, należy ująć go w komentarzu, poprzedzając symbolem # (nie należy pozostawiać pustego elementu ani używać wartości „n/d”). Dodając wartość do elementu, który został ujęty w komentarzu, należy usunąć symbol #.
- Dwukropki w wartości (np. tytule) przerywają działanie analizatora składni metadanych. Zamiast nich należy użyć kodu HTML &#58 (np. „title: Azure Rights Management&#58; podstawy | Azure RMS”).
- **title**: ten tytuł pojawi się w wynikach wyszukiwarki. Tytuł powinien kończyć się symbolem kreski pionowej (|), po którym następuje nazwa usługi (zobacz przykład powyżej). Tytuł nie musi (i prawdopodobnie nie powinien) być taki sam jak tytuł w nagłówku H1. Powinien zawierać około 65 znaków (łącznie z ciągiem | NAZWA USŁUGI)
- **author**, **manager**, **reviewer**: pole „author” powinno zawierać **nazwę użytkownika usługi Github** autora, a nie jego alias.  Z kolei pola „manager” i „reviewer” powinny zawierać aliasy. Wartość ms.reviewer określa imię i nazwisko kierownika projektu powiązanego z artykułem lub usługą.
- **ms.assetid**: identyfikator GUID artykułu z witryny CAPS. Podczas tworzenia nowego pliku markdown uzyskaj identyfikator GUID ze strony [https://www.guidgenerator.com](https://www.guidgenerator.com). 
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: możliwe wartości tych elementów można znaleźć [tutaj](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## Podstawy składni języka Markdown i GFM

Obsługiwane są wszystkie podstawowe i powiązane z usługą Github elementy składni języka Markdown. Aby uzyskać więcej informacji na ten temat, zobacz:

- [Podstawowa składnia języka Markdown](https://daringfireball.net/projects/markdown/syntax)
- [Dokumentacja dotycząca składni języka Markdown powiązanej z usługą Github (GFM)](https://guides.github.com/features/mastering-markdown)

## Nagłówki

Przykłady nagłówków pierwszego i drugiego stopnia znajdują się powyżej. 

W temacie **musi** znajdować się wyłącznie jeden nagłówek pierwszego stopnia, który będzie wyświetlany jako tytuł na stronie.  

Nagłówki drugiego stopnia spowodują wygenerowanie na stronie spisu treści, który pojawi się w sekcji „W tym artykule” pod tytułem strony.

### Nagłówek trzeciego stopnia
#### Nagłówek czwartego stopnia
##### Nagłówek piątego stopnia
###### Nagłówek szóstego stopnia

## Style tekstu

*Kursywa* 

**Pogrubienie** 

~~Przekreślenie~~



## Linki

Aby utworzyć link do pliku markdown w tym samym repozytorium, użyj [linków względnych](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2). 

- Przykład: [Co to jest usługa Azure Rights Management](./understand-explore/what-is-azure-rights-management.md)

Aby utworzyć link do nagłówka w tym samym pliku markdown, wyświetl źródło opublikowanego artykułu, wyszukaj identyfikator nagłówka (np. `id="blockquote"`), a następnie utwórz link według schematu # + identyfikator (np. `#blockquote`).

- Przykład: [Cytaty](#blockquote)

Aby utworzyć link do nagłówka w pliku markdown w tym samym repozytorium, użyj schematu link względny + link z hasztagiem.

- Przykład: [przegląd techniczny procesu rejestracji](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Aby utworzyć link do pliku zewnętrznego, użyj pełnego adresu URL jako linku.

- Przykład: [Github](http://www.github.com)

Jeśli w pliku markdown występuje adres URL, zostanie on przekształcony w link możliwy do kliknięcia.

- Przykład: http://www.github.com

## Listy

### Listy uporządkowane

1. To 
1. jest
1. przykład
1. listy uporządkowanej
1. Lista  


#### Lista uporządkowana z osadzoną listą

1. To
1. jest
1. przykład
1. osadzonej
    1. Julia
    1. Romeo
1. listy uporządkowanej
1. lista


### Listy nieuporządkowane

- To
- jest
- przykład
- listy punktowanej
- lista


##### Lista nieuporządkowana z osadzonymi listami

- Ta 
- lista punktowana 
- lista
    - Rozalina
    - Merkucjo
- zawiera  
- inne
    1. Tybalt
    1. Marta
- listy


## Zasada pozioma

---

## Tabele

| Tabele        | są           | super  |
| ------------- |:-------------:| -----:|
| kolumna 3 jest      | wyrównana do prawej | 1600 USD |
| kolumna 2 jest      | wyśrodkowana      |   12 USD |
| kolumna 1 jest domyślnie | wyrównana do lewej     |    1 USD |


## Kod

### Blok kodu

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Wbudowany kod

To jest przykład kodu wbudowanego `in-line code`.

## Cytaty

> Susza trwała już dziesięć milionów lat. Panowanie olbrzymich jaszczurów dawno dobiegło końca. Tutaj na równiku — na kontynencie, który kiedyś będzie znany jako Afryka — toczyła się coraz bardziej zaciekła walka o przetrwanie, której zwycięzcę trudno było przewidzieć. Na tej jałowej, wyschniętej ziemi mogło powieść się tylko małym, szybkim i dzikim. Tylko tacy mogli liczyć na przetrwanie.

## Obrazy

### Obraz statyczny

![to jest tekst alternatywny](./media/AzRMS_elements.png)

### Obraz połączony

[![atekst alternatywny połączonego obrazu(./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### Animowany plik GIF

![animowany plik GIF](./media/hololens.gif)

## Alerty

### Uwaga

> [!NOTE] To jest UWAGA

### Ostrzeżenie

> [!WARNING] To jest OSTRZEŻENIE

### Porada

> [!TIP] To jest PORADA

### Ważne

> [!IMPORTANT] To jest informacja WAŻNE

## Filmy

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## rozszerzenia docs.ms
To są dostępne rozszerzenia:

### Przycisk

> [!div class="button"] [linki przycisków](/rights-management)

### Selektor

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### Krok po kroku

>[!div class="step-by-step"] [Wstecz](https://www.example.com)
[Dalej](https://www.example.com)

<!--HONumber=May16_HO3-->


