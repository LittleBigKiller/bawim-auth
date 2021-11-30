# Identification and Authentication Failures - Laboratoria

## 0. Przed rozpoczęciem
Przed rozpoczęciem pracy z laboratoriami należy zarejestrować się i zalogować w serwisie [Portswigger](https://portswigger.net/).


## 1. Password-based login
Laboratoria w tej sekcji skupiają się na omijaniu zabezpieczeń opartych na haśle.


### Lab 1.1 - Username enumeration przez różne odpowiedzi
Zadanie - skutecznie stwierdzić, które konto użytkownika istnieje i zalogować się na nie, a następnie wejść na podstronę konta.
To laboratorium jest podatne na `username enumeration` i atak `brute-force` na hasła.
Zarówno nazwa użytkownika jak i hasło znajdują się na poniższych listach:
- [Lista użytkowników](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Witryna daje *zdecydowanie za dużo informacji* użytkownikom i atakującemu.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)


### Lab 1.2 - Username enumeration przez subtelnie różne odpowiedzi
Zadanie - skutecznie stwierdzić, które konto użytkownika istnieje i zalogować się na nie, a następnie wejść na podstronę konta.
To laboratorium jest podatne na `username enumeration` i atak `brute-force` na hasła.
Zarówno nazwa użytkownika jak i hasło znajdują się na poniższych listach (identyczne jak w Lab 1.1):
- [Lista użytkowników](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Tym razem witryna nie daje zbyt dużej ilości informacji, niestety w kod wkradł się błąd.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses)


### Lab 1.3 - Username enumeration przez różnice czasu odpowiedzi
Zadanie - skutecznie stwierdzić, które konto użytkownika (poza podanym) istnieje i zalogować się na nie, a następnie wejść na podstronę konta.
W Tym laboratorium musimy się zrobić nieco bardziej kreatywni, mamy podane poprawne dane logowania na jedno konto w celu łatwiejszego testowania systemu.
- Username: `wiener`, Password: `peter`
- [Lista użytkowników](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Lista haseł](https://portswigger.net/web-security/authentication/auth-lab-passwords)

Tym razem witryna nie ma oczywistego błędu, proces logowania ma jednak dość zróżnicowane czasy odpowiedzi.
- [Laboratorium](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-response-timing)

---


## 2. Password-based login
Laboratoria w tej sekcji skupiają się na omijaniu zabezpieczeń opartych na haśle.
