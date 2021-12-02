# Identification and Authentication Failures - Podpowiedzi do laboratoriów

<br/>

## Lab 1.1 - Username enumeration przez różne odpowiedzi
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li> Burp Intruder będzie bardzo przydatny w tym laboratorium. </li>
    <li> Pracuj sprytnie, darmowa wersja Burpa w zupełności wystarczy. </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li> Kluczem w tym laboratorium jest przyjżenie się uważnie odpowiedziom na zapytanie <code>POST /login</code>. </li>
    <li>
      Nie pracuj z dwoma listami na raz. Najpierw skorzystaj z <a href=https://portswigger.net/web-security/authentication/auth-lab-usernames>listy użytkowników</a>.
      Próbuj łamać hasło dopiero jak się dowiesz czyje dokładnie!
    </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li> Z włączonym w tle Burpem wejdź na stronę logowania i wyślij żądanie logowania z całkowicie losowymi danymi. </li>
    <li> W Burpie wejdź w zakładkę "Proxy" > "HTTP history" i znajdź zapytanie <code>POST /login</code>. Wyślij je do Burp Intruder. </li>
    <li> W Burp Intruder, wejdź w zakładkę "Positions". Upewnij się, że <b>attack type</b> ma ustawioną wartość "Sniper". </li>
    <li>
      Naciśnij przycisk "Clear", żeby wyczyścić wszelkie automatycznie przypisane pozycje payloadu. Zaznacz wartość parametru <code>username</code>
      i kliknij "Add", żeby ustawić ją jako pozycję payloadu. Pozycja ta zostanie oznaczona przez dwa symbole <code>§</code>, na przykład:
      <code>username=§invalid-username§</code>. Na razie pozostaw hasło jako dowolną wartość stałą.
    </li>
    <li> W zakładce "Payloads", upewnij się, że <b>payload type</b> jest ustawiony na wartość "Simple List" </li>
    <li>
      W sekcji "Payload Options", wklej <a href=https://portswigger.net/web-security/authentication/auth-lab-usernames>listę użytkowników</a>.
      Nareszcie możemy rozpocząć atak! W tym celu wciśnij klawisz "Start attack". Atak rozpocznie się w nowym oknie.
    </li>
    <li>
      Gdy atak zakończy się, w zakładce "Results" zbadaj kolumnę "Length". Możesz kliknąć w nagłówek kolumny, aby posortować zawarte w niej dane.
      Zauważ, że jedna z wartości jest dłuższa od pozostałych. Porównaj zawartość tej odpowiedzi z pozostałymi. Zwróć uwagę, że pozostałe odpowiedzi
      zawierają wiadomość <code>Invalid username</code>, a ta zawiera <code>Incorrect password</code>. Zanotuj nazwę użytkownika w kolumnie "Payload".
    </li>
    <li>
      Zamknij okno ataku i wróć to zakładki "Positions". Kliknij "Clear", a następnie zmień wartość parametru <code>username</code> na wartość,
      którą udało się zdobyć w poprzednim kroku. Dodaj pozycję payloadu jako wartość parametru <code>password</code>. Rezultat powienien wyglądać
      mniej więcej w ten sposób:<br/><code>username=identified-user&password=§invalid-password§</code>
    </li>
    <li>
      W zakładce "Payloads", wyczyść listę nazw użytkowników i zastąp ją <a href=https://portswigger.net/web-security/authentication/auth-lab-passwords>
      listą potencjalnych haseł</a>. Kliknij "Start attack".
    </li>
    <li>
      Gdy atak zakończy się, popatrz na kolumnę "Status". Zauważ, że każdy request otrzymał odpowiedź z kodem statusu 200, poza jednym,
      który dostał odpowiedź z kodem 302. To sugeruje, że dana próba logowania była skuteczna.
    </li>
    <li> Zaloguj się przy użyciu zidentyfikowanych nazwy użytkownika i hasła i wejdź na podstronę konta użytkownika w celu rozwiązania laboratorium. </li>
  </ol>
</details>

<br/>

## Lab 1.2 - Username enumeration przez subtelnie różne odpowiedzi
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li> Burp Intruder będzie bardzo przydatny w tym laboratorium. </li>
    <li> Tym razem różnica będzie cieżka do zauważenia gołym okiem. Gdyby tylko "Results" miało więcej kolumn... </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li>
      Burp Intruder ma wbudowane wyciąganie danych z odpowiedzi przy użyciu polecenia <b>Grep</b>. Można je znaleźć o zakładce "Options" danego ataku.
      Wyciągnięcie odpowiednich danych z odpowiedzi powinno szybko uświadomić nam, które jest inne od reszty.
    </li>
    <li> Głupio tracić bezpieczeństwo systemu przez błędy interpunkcyjne </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      Z włączonym w tle Burpem wejdź na stronę logowania i wyślij żądanie z błędnymi danymi logowania. Wyśli zapytanie <code>POST /login</code>
      do Burp Intruder i dodaj pozycje payloadu do parametru <b>username</b>.
      </li>
    <li>
      W zakładce "Payloads", upewnij się, że wybrany payload type to "Simple list" i dodaj
      <a href=https://portswigger.net/web-security/authentication/auth-lab-usernames>listę użytkowników</a> jako wartości.
    </li>
    <li>
      W zakładce "Options", w sekcji "Grep - Extract", kliknij "Add". W oknie dialogowym, które się otworzy przewiń odpowiedź, aż natrfisz na wiadomość o błędzie
      <code>Invalid username or password</code>. Użyj myszy, aby zaznaczyć tekst wiadomości. Pozostałe opcje zostaną automatycznie ustawione.
      Naciśnij "OK" i rozpocznij atak.
    </li>
    <li>
      Gdy atak zakończy się, zauważ że pojawiła się dodatkowa kolumna zawierająca wiadomość o błędzie, którą kazaliśmy wyciągnąć z odpowiedzi.
      Posortuj kolumnę w celu znalezienia odpowiedzi, która różni się od pozostałych.
    </li>
    <li>
      Przyjrzyj się uważniej <i>innej</i> odpowiedzi. Zauważ, że zawiera literówkę w wiadomości o błędzie - zamiast kropki programista wpisał spację.
      Zanotuj nazwę użytkownika.
    </li>
    <li>
      Zamknij atak, przejdź do zakładki "Positions". Wstaw zapisaną nazwę użytkownika w pole <b>username</b> i dodaj pozycję payloadu do parametru <b>password</b>:
      <code>username=identified-user&password=§invalid-password§</code>.
    </li>
    <li>
      W zakładce "Payloads", wyczyść listę nazw użytkowników i zastąp ją <a href=https://portswigger.net/web-security/authentication/auth-lab-passwords>
      listą potencjalnych haseł</a>. Kliknij "Start attack".
    </li>
    <li>
      Gdy atak zakończy się, zauważ że jedno żądanie otrzymało odpowiedź z kodem 302. Zanotuj hasło, które zostało użyte w odpowiadającym zapytaniu.
    </li>
    <li>
      Zaloguj się przy użyciu zidentyfikowanych nazwy użytkownika i hasła i wejdź na podstronę konta użytkownika w celu rozwiązania laboratorium.
    </li>
  </ol>
</details>

<br/>

## Lab 1.3 - Username enumeration przez różnice czasu odpowiedzi
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li> Warto rozważyć inne tryby Burp Intrudera niż "Sniper". </li>
    <li> Jak tam ze znajomością nagłówków HTTP? </li>
    <li> Przyjżyj się uważnie czasom odpowiedzi serwera. </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li> Witryna wspiera nagłówek <code>X-Forwarded-For</code>, możemy przy jego użyciu dokonać spoofingu naszego adresu IP. </li>
    <li>
      W ramach ataku będziemy musieli zmieniać jednocześnie dwie wartości między zapytaniami (dodatkowo nasz adres IP).
      Idealnie do tego nadaje się tryb "Pitchfork".
    </li>
    <li> Zauważ, że czas odpowiedzi serwera przy sprawdzaniu hasła dla nieistniejącego konta jest zawsze mniej więcej taki sam. </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      Z włączonym w tle Burpem wejdź na stronę logowania i wyślij żądanie z błędnymi danymi logowania. Wyśli zapytanie <code>POST /login</code>
      do Burp Repeater i poeksperymentuj z różnymi loginami i hasłami. Zauważ, że Twoje IP zostanie zablokowane po kilku nieudanych próbach.
    </li>
    <li>
      Zwróć uwagę, że nagłówek <code>X-Forwarded-For</code> jest wspierany, to pozwoli dokonać spoofingu naszego adresu IP i ominąć opartą o adresy IP ochronę
      serwisu przed atakami brute-force.
    </li>
    <li>
      Kontynuuj eksperymentowanie z loginami i hasłami. Zwróć szczególną uwagę na czasy odpowiedzi serwera. Zawuaż, że jeśli username nie istnieje to czas odpowiedzi
      jest mniej więcej taki sam za każdym razem. Natomiast dla istniejącego konta, czas odpowiedzi zależy od długości podanego (błędnego) hasła.
    </li>
    <li>
      Prześlij zapytanie, z którego korzystaliśmy do Burp Intruder i wybierz attack type "Pitchfork". Wyczyść domyślne pozycje payloadów i dodaj nagłwek
      <code>X-Forwarded-For</code>.
    </li>
    <li>
      Dodaj pozycje payloadu dla nagłówka <code>X-Forwarded-For</code> oraz dla parametru <code>username</code>. Ustaw hasło na dowolny,
      bardzo długi string (około 100 znaków powinno wystarczyć).
    </li>
    <li>
      W zakładce "Payloads", wybierz payload set 1. Ustaw payload type "Numbers". Wybierz zasięg 1-100 i ustaw krok na 1. Ustaw maksymalną ilość cyfr
      po przecinku na 0. Tego użyjemy do spoofingu Twojego IP.
    </li>
    <li>
      Wybierz payload set 2 i dodaj <a href=https://portswigger.net/web-security/authentication/auth-lab-usernames>listę użytkowników</a> jako wartości.
      Rozpocznij atak.
    </li>
    <li>
      Gdy atak zakończy się, w górnej części okna, kliknij "Columns" i zaznacz opcje "Response received" oraz "Response completed".
      Te dwie kolumny są teraz wyświetlane w tabelu rezultatów.
    </li>
    <li>
      Zwróć uwagę, że jeden z tych czasów odpowiedzi był znacznie dłuższy od pozostałych. Powtórz kilkukrotnie to zapytanie i jeśli czas odpowiedzi
      pozostanie porównywalnie długi to zanotuj wykorzystany w tym zapytaniu login.
    </li>
    <li>
      Stwórz kolejny atak w Burp Intruderze na podstawie tego samego zapytania. Dodaj ponownie nagłówek <code>X-Forwarded-For</code> i dodaj
      do niego pozycje payloadu. Wstaw zapisany login jako wartość pola <b>username</b> oraz dodaj pozycję payloadu do parametru <code>password</code>.
    </li>
    <li>
      W zakładce "Payloads" dodaj listę liczb do payload setu 1 i <a href=https://portswigger.net/web-security/authentication/auth-lab-passwords>
      listę potencjalnych haseł</a> do payload setu 2. Rozpocznij atak.
    </li>
    <li>
      Gdy atak zakończy się, zauważ że jedno żądanie otrzymało odpowiedź z kodem 302. Zanotuj hasło, które zostało użyte w odpowiadającym zapytaniu.
    </li>
    <li>
      Zaloguj się przy użyciu zidentyfikowanych nazwy użytkownika i hasła i wejdź na podstronę konta użytkownika w celu rozwiązania laboratorium.
    </li>
  </ol>
</details>
