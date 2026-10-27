<!-- suite
id: @S1731bdc9
-->
# Selected language translates the navigation and is kept after reload

<!-- test
id: @T3e5f88d2
priority: low
tags: TC-I18N-001, ui, i18n, REQ-I18N-01, regression
-->
## Selected language translates the navigation and is kept after reload

## Preconditions

- A new browser session with the browser language English and no language chosen before.

## Steps

1. Open the home page.
*Expected*: The language switcher shows "EN" and the navigation shows "Home", "Categories", "Contact" and "Sign in".
2. Select "DE" in the language switcher.
*Expected*: The switcher shows "DE" and the navigation shows "Start", "Kategorien", "Kontakt" and "Einloggen".
3. Reload the page.
*Expected*: The switcher still shows "DE" and the navigation is still in German.
4. Repeat steps 2 and 3 for "EL", "ES", "FR", "NL" and "TR".
*Expected*: Before and after the reload the "Categories" menu shows "Κατηγορίες" (EL), "Categorías" (ES), "Catégories" (FR), "Categorieën" (NL) and "Kategoriler" (TR), and "Sign in" shows "Σύνδεση", "Iniciar sesión", "Se connecter", "Inloggen" and "Giriş Yap".
5. Select "EN".
*Expected*: The switcher shows "EN" and the navigation shows "Home", "Categories", "Contact" and "Sign in" again.
