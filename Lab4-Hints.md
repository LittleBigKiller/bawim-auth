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
      W Burpie, wejdź w "Proxy" > "HTTP history" i przestudiuj zapytania i odpowiedzi w poszukiwaniu procesu resetu hasła.
      Zaobserwuj, że token resetowania jest podawany jako parametr URL. Zauważ, że gdy wpiszesz nowe hasło, zapytanie
      <code>POST /forgot-password?temp-forgot-password-token</code> zawiera username w ukrytym polu. Prześlij to zapytanie do Burp Repeatera.
    </li>
    <li>
      W Burp Repeaterze, zaobserwuj że funkcjonalność zmiany hasła nadal działa, nawet jeśli usuniesz wartość parametru <code>temp-forgot-password-token</code>
      w treści zapytania. To potwierdza, że nie token nie jest sprawdzany przy zmianie hasła.
    </li>
    <li>
      W swojej przeglądarce, zainicjuj nową zmianę hasła i zmień ponownie swoje hasło. Ponownie prześlij żądanie
      <code>POST /forgot-password?temp-forgot-password-token</code> do Burp Repeatera.
    </li>
    <li>
      W Burp Repeaterze, usuń wartość parametru <code>temp-forgot-password-token</code> zarówno w URL jak i w treści zapytania.
      Zmień wartość parametru <code>username</code> na <code>carlos</code>. Ustaw nowe hasło na dowolną wartość, którą zanotujesz.
    </li>
    <li>
      W swojej przeglądarcie, zaloguj się na konto Carlos'a przy użyciu świeżo ustawionego hasła. Wejdź w zakładkę "My Account", żeby rozwiązać laboratorium.
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
      Z włączonym w tle Burpem, zaloguj się na swoje konto i poeksperymentuj z funkcjonalnością zmiany hasła. Zaobserwuj,
      że nazwa użytkownika jest podawana w ukrytym polu zapytania.
    </li>
    <li>
      Zaobserwuj zachowanie strony, kiedy podamy błędne aktualne hasło. Jeśli dwa wpisy dla nowego hasła zgadzają się, konto jest zablokowane.
      Natomiast jeśli wpiszesz dwa różne nowe hasła, zwyczajnie wyświetli się wiadomość o błędzie o treści <code>Current password is incorrect</code>.
      Jeśli wpiszesz poprawne aktualne hasło, ale dwa różne nowe hasła, wiadomość brzmi <code>New passwords do not match</code>.
      Możemy użyć tych wiadomości do odkrycia proprawnych haseł.
    </li>
    <li>
      Wpisz swoje aktualne hasło i dwa nowe hasła, które się nie zgadzają. Prześlij wykorzstywane zapytanie do Burp Intrudera.
    </li>
    <li>
      W Burp Intruderze, zmień wartość parametru <code>username</code> na <code>carlos</code> i dodaj pozycję payloadu do parametru <code>current-password</code>
      Upewnij się, że parametry new password mają dwie różne wartości. Na przykład:
      <code>username=carlos&current-password=§incorrect-password§&new-password-1=123&new-password-2=abc</code>
    </li>
    <li>
      W zakładce "Payloads", wstaw <a href=https://portswigger.net/web-security/authentication/auth-lab-passwords>listę potencjalnych haseł</a> jako payload set.
    </li>
    <li>
      W zakładce "Options", dodaj zasadę Grep - Match, która zaznaczy wszystkie odpowiedzi z błędem <code>New passwords do not match</code>. Rozpocznij atak.
    </li>
    <li>
      Kiedy atak się zakończy, zauważ że jedna z odpowiedzi została oznaczona, że zawiera wiadomość <code>New passwords do not match</code>. Zanotuj to hasło.
    </li>
    <li>
      W swojej przeglądarce, wyloguj się ze swojego konta i zaloguj się na konto <code>carlos</code> przy użyciu zidentyfikowanego przed chwilą hasła.
    </li>
    <li>
      Kliknij zakładkę "My account", żeby rozwiązać laboratorium.
    </li>
  </ol>
</details>
