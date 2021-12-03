# Identification and Authentication Failures - Laboratoria

<br/>

## 0. Przed rozpoczęciem

Przed rozpoczęciem pracy z laboratoriami należy zarejestrować się i zalogować w serwisie [Portswigger](https://portswigger.net/).

Do każdego zestawu labów dołączony jest zestaw podpowiedzi. Są one 3 stopniowe - drobne, duże i rozwiązanie krok po kroku. Odnośniki do nich dostępne są poniżej linków do labu.

<br/><br/>

---

## 1. Uwierzytelnianie hasłem
Laboratoria w tej sekcji skupiają się na omijaniu zabezpieczeń opartych na haśle.

<br/>

### Lab 1.1 - Username enumeration przez różne odpowiedzi
Zadanie - Skutecznie stwierdzić, które konto użytkownika istnieje i złamać jego hasło, a następnie wejść na podstronę konta.
To laboratorium jest podatne na `username enumeration` i atak `brute-force` na hasła.
Zarówno nazwa użytkownika jak i hasło znajdują się na poniższych listach:
- [Lista użytkowników](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Witryna daje *zdecydowanie za dużo informacji* użytkownikom i atakującemu.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)
- [Podpowiedzi](https://github.com/LittleBigKiller/bawim-auth/blob/master/Lab1-Hints.md#lab-11---username-enumeration-przez-r%C3%B3%C5%BCne-odpowiedzi)

<br/>

### Lab 1.2 - Username enumeration przez subtelnie różne odpowiedzi
Zadanie - Skutecznie stwierdzić, które konto użytkownika istnieje i złamać jego hasło, a następnie wejść na podstronę konta.
To laboratorium jest podatne na `username enumeration` i atak `brute-force` na hasła.
Zarówno nazwa użytkownika jak i hasło znajdują się na poniższych listach (identyczne jak w Lab 1.1):
- [Lista użytkowników](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Tym razem witryna nie daje zbyt dużej ilości informacji, niestety w kod wkradł się błąd.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses)
- [Podpowiedzi](https://github.com/LittleBigKiller/bawim-auth/blob/master/Lab1-Hints.md#lab-11---username-enumeration-przez-r%C3%B3%C5%BCne-odpowiedzi)

<br/>

### Lab 1.3 - Username enumeration przez różnice czasu odpowiedzi
Zadanie - Skutecznie stwierdzić, które konto użytkownika (poza podanym) istnieje i złamać jego hasło, a następnie wejść na podstronę konta.
W Tym laboratorium musimy się zrobić nieco bardziej kreatywni, mamy podane poprawne dane logowania na jedno konto w celu łatwiejszego testowania systemu.
- Twój login: `wiener`
- Twoje hasło: `peter`
- [Lista użytkowników](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Tym razem witryna nie ma oczywistego błędu, ale pamiętaj! Cierpliwość jest cnotą.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-response-timing)
- [Podpowiedzi](https://github.com/LittleBigKiller/bawim-auth/blob/master/Lab1-Hints.md#lab-13---username-enumeration-przez-r%C3%B3%C5%BCnice-czasu-odpowiedzi)

<br/><br/>

---

## 2. Rate limit i blokada konta
Laboratoria w tej sekcji skupiają się na omijaniu wadliwej ochrony przed atakami typu brute-force oraz nadużywaniu blokowania kont w celu ataku.

<br/>

### Lab 2.1 - Zepsuta ochrona przed brute-force i blokada IP
Zadanie - Zalogować się na podane konto użytkownika, a następnie wejść na podstronę konta.
W Tym laboratorium zadanie jest nieco inne, już nie przejmujemy się username enumeration.
Mamy podany login ofiary oraz poprawne dane logowania na istniejące konto w celu łatwiejszego testowania systemu.
- Twój login: `wiener`
- Twoje hasło: `peter`
- Login ofiary: `carlos`
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Tym razem witryna aktywnie broni się przed atakiem, warto zacząć od zbadania ochrony.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-broken-bruteforce-protection-ip-block)
- [Podpowiedzi](https://github.com/LittleBigKiller/bawim-auth/blob/master/Lab2-Hints.md#lab-21---zepsuta-ochrona-przed-brute-force-i-blokada-ip)

<br/>

### Lab 2.2 - Username enumeration przez blokady kont
Zadanie - Skutecznie stwierdzić, które konto użytkownika istnieje i złamać jego hasło, a następnie wejść na podstronę konta.
Zarówno nazwa użytkownika jak i hasło znajdują się na poniższych listach (identyczne jak w poprzednich labach):
- [Lista użytkowników](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

System obrony z poprzedniego labu już nie jest problemem. Teraz użytkownicy muszą uważać na zbyt częste wpisywanie błędnych haseł.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock)
- [Podpowiedzi](https://github.com/LittleBigKiller/bawim-auth/blob/master/Lab2-Hints.md#lab-22---username-enumeration-przez-blokady-kont)

<br/><br/>

---

## 3. Dwuskładnikowe Uwierzytelnianie
Laboratoria w tej sekcji skupiają się na omijaniu wadliwego dwuskładnikowego uwierzytelniania.

<br/>

### Lab 3.1 - Proste ominięcie dwuskładnikowego uwierzytelniania
Zadanie - Zalogować się na konto ofiary, a następnie wejść na podstronę konta.
Mamy dostęp do konta testowego i konta ofiary:
- Twój login: `wiener`
- Twoje hasło: `peter`
- Login ofiary: `carlos`
- Hasło ofiary: `montoya`

Dodatkowo mamy dostęp do konta email powiązanego z kontem testowym w zakładce "Email client". Jest ono używane do otrzymywania kodów 2FA.

Witryna stała się bezpieczniejsza, teraz wykorzystuje wieloskładnikowe uwierzytelnianie. Niestety znajomość hasła ofiary może nie być wystarczająca.
- [Laboratorium](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass)
- [Podpowiedzi](https://github.com/LittleBigKiller/bawim-auth/blob/master/Lab3-Hints.md#lab-31---proste-omini%C4%99cie-dwusk%C5%82adnikowego-uwierzytelniania)

<br/>

### Lab 3.2 - Wadliwa logika dwuskładnikowego uwierzytelniania
Zadanie - Zalogować się na konto ofiary, a następnie wejść na podstronę konta.
Mamy dostęp do konta testowego i znamy login konta ofiary:
- Twój login: `wiener`
- Twoje hasło: `peter`
- Login ofiary: `carlos`

Dodatkowo mamy dostęp do konta email powiązanego z kontem testowym w zakładce "Email client". Jest ono używane do otrzymywania kodów 2FA.

2FA tym razem działa, ale z dużym błędem w logice. Ofiara nawet nie będzie musiała próbować się zalogować.
- [Laboratorium](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic)
- [Podpowiedzi](https://github.com/LittleBigKiller/bawim-auth/blob/master/Lab3-Hints.md#lab-32---wadliwa-logika-dwusk%C5%82adnikowego-uwierzytelniania)

<br/><br/>

---

## 4. Wadliwe resetowanie haseł
Laboratoria w tej sekcji skupiają się na nadużywaniu wadliwie zaimplementowanych systemów resetowania haseł.

<br/>

### Lab 4.1 - Wadliwa logika resetowania haseł
Zadanie - Zalogować się na konto ofiary, a następnie wejść na podstronę konta.
Mamy dostęp do konta testowego i loginu konta ofiary:
- Twój login: `wiener`
- Twoje hasło: `peter`
- Login ofiary: `carlos`

Dodatkowo mamy dostęp do konta email powiązanego z kontem testowym w zakładce "Email client". Jest ono używane do otrzymywania linków resetu hasła.

Tym razem przyglądamy się mechanizmowi resetowania hasła na witrynie. Zapewne i tym razem nie jest napisany zbyt dobrze.
- [Laboratorium](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-broken-logic)

<br/>

### Lab 4.2 - Brute-force hasła przez system zmiany hasła
Zadanie - Zalogować się na konto ofiary, a następnie wejść na podstronę konta.
Mamy dostęp do konta testowego i loginu konta ofiary oraz listy prawdopodobnych haseł:
- Twój login: `wiener`
- Twoje hasło: `peter`
- Login ofiary: `carlos`
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Dodatkowo mamy dostęp do konta email powiązanego z kontem testowym w zakładce "Email client". Jest ono używane do otrzymywania kodów 2FA.

Witryna ponownie daje nam *zdecydowanie za dużo informacji*.
- [Laboratorium](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-brute-force-via-password-change)
