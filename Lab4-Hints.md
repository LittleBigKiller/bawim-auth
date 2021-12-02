# Identification and Authentication Failures - Podpowiedzi do laboratoriów

<br/>

## Lab 4.1 - Wadliwa logika resetowania haseł
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li>
      Nie wszystkie parametry zapytań są konieczne. Niektóre nie są weryfikowane.
    </li>
    <li>
      Burp Repeater powinien być najbardziej przydatnym narzędziem w tym laboratorium.
    </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li>
      Niektóre pola są ukryte w formularzu. Warto przyjrzeć się samym zapytaniom przy użyciu Burpa.
    </li>
    <li>
      Token resetu hasła nie jest sprawdzany. Można go usunąć zarówno z URL jak i z zawartości zapytania.
    </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      Z włączonym w tle Burpem, kliknij odnośnik "Forgot your password?" i wpisz swoją nazwę użytkownika.
    </li>
    <li>
      Naciśnij przycisk "Email client", żeby zobaczyć, że został przysłany link zmiany hasła.
      Kliknij w link i zmień swoje hasło na dowolne.
    </li>
    <li>
      W Burpie, wejdź w "Proxy" > "HTTP history" i przestudiować zapytania i odpowiedzi w poszukiwaniu resetu hasła.
      Zaobserwuj, że token resetowania jest podawany jako parametr URL.
    </li>
    <li>
      Z włączonym w tle Burpem, kliknij odnośnik "Forgot your password?" i wpisz swoją nazwę użytkownika.
    </li>
    <li>
      Z włączonym w tle Burpem, kliknij odnośnik "Forgot your password?" i wpisz swoją nazwę użytkownika.
    </li>
    <li>
      Z włączonym w tle Burpem, kliknij odnośnik "Forgot your password?" i wpisz swoją nazwę użytkownika.
    </li>
    <li>
      Z włączonym w tle Burpem, kliknij odnośnik "Forgot your password?" i wpisz swoją nazwę użytkownika.
    </li>
  </ol>
</details>

<br/>

## Lab 4.2 - Brute-force hasła przez system zmiany hasła
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li>
      Link do formularza zmiany hasła dostępny jest dopiero dla zalogowanych. 
    </li>
    <li>
      Strona dzieli się zbyt dużą ilością informacji. 
    </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li>
      Ponownie poszukaj ukrytych pól formularza.
    </li>
    <li>
      Witryna najpierw sprawdza poprawność akutualnego hasła, a dopiero potem czy podane nowe hasła się zgadzają.
    </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      PLACEHOLDER
    </li>
  </ol>
</details>
