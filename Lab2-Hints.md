# Identification and Authentication Failures - Podpowiedzi do laboratoriów

<br/>

## Lab 2.1 - Username enumeration przez blokady kont
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li>
      Spróbuj wywołać zablokowanie konta i zaobserwuj informacje zwrotne.
      Witryna znów dzieli się zbyt wielką ilością informacji.
    </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li>
      Zwróć uwagę, że informacje zwrotne przy próbie zablokowania różnią się dla istniejących i nieistniejących kont.
    </li>
    <li>
      Nie zawsze musisz wykorzystywać Burp Intruder, żeby gdzieś się dostać. Możesz go również wykorzystać do szybkiego uruchomienia zabezpieczenia.
    </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      Z włączonym w tle Burpem zbadaj stronę logowania i wpisz niepoprawne dane logowania. Prześlij zapytanie <code>POST /login</code> do Burp Intruder.
    </li>
    <li>
      Zależnie od wersji Burpa, z której korzystamy:
      <ul>
        <li>
          W wersji płatnej, bądź dla cierpliwych:
          <ol>
            <li>
              Wybierz typ ataku "Cluster bomb". Dodaj pozycje payloadu do parametru <code>username</code>. Dodaj pustą pozycje payloadu na koniec zapytania
              przez dwukrotne naciśnięcie "Add §". Rezultat powinien wyglądać mniej więcej tak:<br/>
              <code>username=§invalid-username§&password=example§§</code>.
            </li>
            <li>
              W zakładce "Payloads" dodaj <a href="https://portswigger.net/web-security/authentication/auth-lab-usernames">listę nazw użytkownika</a>
              jako payload set 1. W drugim secie wybierz typ "Null payloads" i wybierz opcję generowania 5 payloadów. Rozpocznij atak.
            </li>
            <li>
              W rezultatach, zauważ że jedna z odpowiedzi dla jednej z nazw użytkownika jest dłuższa od pozostałych. Po dokładniejszej inspekcji okazuje się,
              że zawiera inną wiadomość o błędzie: <code>You have made too many incorrect login attempts</code>. Zanotuj odpowiadającą mu nazwę użytkownika.
            </li>
          </ol>
        </li>
        <li>
          W wersji darmowej:
          <ol>
            <li>
              Wybierz typ ataku "Sniper". Dodaj pozycje payloadu do parametru <code>username</code>.
              Rezultat powinien wyglądać mniej więcej tak:<br/>
              <code>username=§invalid-username§&password=example</code>.
            </li>
            <li>
              W zakładce "Payloads" dodaj <a href="https://portswigger.net/web-security/authentication/auth-lab-usernames">listę nazw użytkownika</a>
              jako payload set 1. Pięciokrotnie rozpocznij atak (naciśnij "Start attack" 5 razy po sobie).
            </li>
            <li>
              W rezultatach (najpewniej ataku numer 5), zauważ że jedna z odpowiedzi dla jednej z nazw użytkownika jest dłuższa od pozostałych.
              Po dokładniejszej inspekcji okazuje się, że zawiera inną wiadomość o błędzie: <code>You have made too many incorrect login attempts</code>.
              Zanotuj odpowiadającą mu nazwę użytkownika.
            </li>
          </ol>
        </li>
      </ul>
    </li>
    <li>
      Stwórz nowy atak w Burp Intruder na podstawie zapytania na <code>POST /login</code>, ale tym razem typu "Sniper".
      Ustaw parametr <code>username</code> na zanotowany i dodaj pozycje payloadu do parametru <code>password</code>.
    </li>
    <li>
      Ustaw <a href=https://portswigger.net/web-security/authentication/auth-lab-passwords>listę potencjalnych haseł</a> jako payload set 1.
      Stwórz zasadę Grep, która wyodrębni nam wiadomość o błędzie. Rozpocznij atak.
    </li>
    <li>
      W rezultatach ataku, popatrz na kolumnę wyników Grepa. Zauważ, że jest tam kilka różnych wiadomości o błędach, ale jedna z odpowiedzi nie zawiera żadnej.
      Zanotuj związane z nią hasło.
    </li>
    <li>
      Poczekaj minutę, żeby pozwolić blokadzie konta na zresetowanie.
      Zaloguj się przy użyciu zidentyfikowanych nazwy użytkownika i hasła i wejdź na podstronę konta użytkownika w celu rozwiązania laboratorium.
    </li>
  </ol>
</details>

<br/>

## Lab 2.2 - Zepsuta ochrona przed brute-force i blokada IP
<details>
  <summary>Drobna podpowiedź</summary>
  <ol>
    <li>
      Zacznij pracę od zbadania zabezpeczeń przed atakami brute-force. Ominięcie ich to priorytet.
    </li>
  </ol>
</details>

<details>
  <summary>Duża podpowiedź</summary>
  <ol>
    <li>
       Licznik niepoprawnych logowań nie jest dla konta, jest dla adresu IP.
    </li>
    <li>
      Ponownie przydatny będzie tryb ataku "Pitchfork".
    </li>
    <li>
      Blokada IP tym razem nie jest wrażliwa na <code>X-Forwarded-For</code>.
    </li>
  </ol>
</details>

<details>
  <summary>Krok po kroku</summary>
  <ol>
    <li>
      Z włączonym w tle Burpem zbadaj stronę logowania. Zauważ, że po trzech nieudanych próbach logowania z rzędu, Twoje IP zostanie zablokowane,
      ale zwróć również uwagę, że skuteczne zalogowanie się resetuje licznik błędnych logowań.
    </li>
    <li>
      Wstaw błędną nazwę użytkownia i hasło, prześlij zapytanie <code>POST /login</code> do Burp Intrudera. Stwórz atak pitchfork z pozycjami payloadu
      zarówno w parametrze <code>username</code> jak i <code>password</code>.
    </li>
    <li>
      W zakładce "Payloads" wybierz payload set 1. Dodaj listę payloadów, która zmiennie używa Twojej nazwy użytkownika i <code>carlos</code>.
      Upewnij się, że Twoja nazwa użytkownika jest pierwsza oraz że <code>carlos</code> powtarza się przynajmniej 100 razy.
    </li>
    <li>
      Edytuj <a href=https://portswigger.net/web-security/authentication/auth-lab-passwords>listę potencjalnych haseł</a> i wstaw swoje hasło przed każdym.
      Upewnij się, że pozycje Twojego hasła pokrywają się z Twoją nazwą użytkownika na liście nazw użytkownika.
    </li>
    <li>
      Dodaj powyżej opisaną listę jako payload set 2 i rozpocznij atak.
    </li>
    <li>
      Kiedy atak zakończy się, ukryj odpowiedzi o kodzie statusu 200. Pozortuj pozostałe odpowiedzi według pola username.
      Powinna być dokładnie jedna odpowiedź z kodem 302 dla zapytań z nazwą użytkownika <code>carlos</code>. Zanotuj hasło w kolumnie "Payload 2" tego zapytania.
    </li>
    <li>
      Zaloguj się na konto Carlos'a przy użyciu zidentyfikowanego hasła i wejdź na podstronę konta użytkownika w celu rozwiązania laboratorium.
    </li>
  </ol>
</details>
