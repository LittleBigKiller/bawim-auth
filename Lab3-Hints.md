# Identification and Authentication Failures - Podpowiedzi do laboratoriów

<br/>

## Lab 3.1 - Proste ominięcie dwuskładnikowego uwierzytelniania
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li>
      Czasami na niektóre podstrony jesteśmy przekierowywani, ale nie są one konieczne.
    </li>
    <li>
      Jedynym potrzebnym w tym laboratorium narzędziem jest przeglądarka internetowa.
    </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li>
      Zacznij od zalogowania się na swoje konto i zobaczenia jak przebiega ten proces. Gdzie się zaczyna, a gdzie kończy.
    </li>
    <li>
      Czasem warto sprawdzić, czy wszystkie kroki danego procesu są konieczne.
    </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      Zaloguj się na swoje konto. Twój kod weryfikacji dwuskładnikowej zostanie wysłany na email. Kliknij przycisk "Email client",
      aby uzyskać dostęp do swojej skrzynki mailowej.
    </li>
    <li>
      Wejdź na stronę konta i zanotuj jej adres URL.
    </li>
    <li>
      Wyloguj się ze swojego konta.
    </li>
    <li>
      Zaloguj się przy użyciu danych logowania ofairy.
    </li>
    <li>
      Kiedy pojawi się formularz proszący o kod 2FA, zwyczajnie ręcznie zmień URL na <code>/my-account</code>.
      Laboratorium zostanie rozwiązane kiedy strona się załaduje.
    </li>
  </ol>
</details>

<br/>

## Lab 3.2 - Wadliwa logika dwuskładnikowego uwierzytelniania
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li>
      Hasło ofiary jest nam absolutnie zbędne. Wystarczy luka w 2FA.
    </li>
    <li>
      Nie wszystkie pola w zapytaniach są widoczne gołym okiem, czasem potrzeba skorzystać z narzędzi.
    </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li>
      Sprawdź jak informowany jest serwer dla kogo wykonujemy zapytanie wysyłające kod 2FA.
    </li>
    <li>
      Inaczej niż w poprzednich laboratoriach, musisz wczytać w przeglądarce odpowiedź na zapytanie z narzędzia Burp.
    </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      Z włączonym w tle Burpem zaloguj się na swoje konto i zbadaj proces weryfikacji dwuskładnikowej. Zauważ, że w zapytaniu <code>POST /login2</code>,
      parametr <code>verify</code> jest używany do wskazania, na które konto próbujemy się zalogować.
    </li>
    <li>
      Wyloguj się ze swojego konta.
    </li>
    <li>
      Prześlij żądanie <code>GET /login2</code> do Burp Repeater. Zmień wartość parametru <code>verify</code> na <code>carlos</code> i wyśli zapytanie.
      To sprawi, że dla Carlosa zostanie wygenerowany kod 2FA.
    </li>
    <li>
      Wejdź na stronę logowania, wpisz swoją nazwę użytkownika i hasło. Następnie podaj zły kod 2FA.
    </li>
    <li>
      Prześlij żądanie <code>POST /login2</code> do Burp Intruder.
    </li>
    <li>
      W Burp Intruder, ustaw parametr <code>verify</code> na <code>carlos</code> i dodaj pozycje payloadu do parametru <code>mfa-code</code>.
      Złam kod 2FA atakiem brute-force.
      <br/>
      Porada dla użytkowników wersji darmowej - pamiętaj, że możesz 1 ataku z 1000 zapytań rozbić na np. 10 ataków po 100 zapytań.
    </li>
    <li>
      Załąduj odpowiedź ze statusem 302 w swojej przeglądarce.
    </li>
    <li>
      Wejdź w zakładkę "My account" w celu rozwiązania laboratorium.
    </li>
  </ol>
</details>
