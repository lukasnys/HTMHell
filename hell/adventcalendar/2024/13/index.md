---
title: "Improving User Experience for Multilingual Web Browsing"
layout: layouts/advent.md
author: "Anastasiia Batarei"
author_bio: "Short intro about yourself"
date: 2024-12-13
author_links:
  - label: "X (Twitter)"
    url: "https://x.com/html_diva_en"
    link_label: "@html_diva_en"
  - label: "LinkedIn"
    url: "https://www.linkedin.com/in/anastasiia-batarei/"
    link_label: "anastasiia-batarei"
active: true
intro: '<p>In the article I talk about improving user experience on multilingual websites by using the translate="no" attribute to prevent incorrect translations of names, emails, and technical terms. This simple HTML trick ensures better accessibility and usability for global audiences.</p>'
image: "advent_13"
---
<!-- MM: Please don't forget to add a short bio in line 5 "author_bio" -->
<!-- SS: I always love a good article on localization coming from a country with multiple languages -->
<!--
  KS: Something strikes me as odd about the phrase "foreign websites."
  I think you could just rewrite the sentence without it, and go with
  "...the experience of browsing websites whose content is fully or..."
-->
Today, I’d like to talk about the experience of browsing foreign websites, where content is fully or partially in a language different from the user’s native one. This situation is common for users visiting government portals, local service providers, or international marketplaces where essential information may appear in unfamiliar languages. 
In these cases, users often rely on the browser’s auto-translate feature, which modern browsers offer by default. When you open a page in a different language from your preferred setting, the browser will prompt you to translate it automatically.
<!-- MM: All browsers? Consider changing it to "which many modern browsers"-->

<img src="google-translate-popup.png" width="800" height="161" loading="lazy" alt="A screenshot from Google Translate. It displays language selection options, with Dutch on the left and English on the right. English is selected as the target language.">
<!-- MM: Consider this shorter alt "Language selection options in Google Translate: Dutch and English." -->

Browser auto-translation relies on the lang attribute set on the HTML element:

```html
<html lang="en"></html>
```

However, automatic translations can sometimes be inaccurate or misleading, especially when it comes to proper names, email addresses, branded names, or technical terms that should remain untranslated.
<!-- MM: Are you sure that tools like Google translate actually translate email addresses? -->

For example, let’s see what happens when a user’s name, like Joke (a Dutch feminine name pronounced [ˈjoːkə]), is displayed on an English page that is then auto-translated into Dutch:

However, automatic translations can sometimes be inaccurate or misleading.

```html
<!-- Original content in English -->
<p>Name: Joke</p>
<p>Email: joke@test.com</p>

<!-- Translated content in Dutch -->
<p>Naam: Grap</p>
<p>E-mailadres: grap@test.com</p>
```

<!-- SS: I checked this in chrome and seems like the email doesn't get translated. I think verifying this once, and maybe mentioning which browser you saw this behaviour would be good -->

The Dutch word “Grap” means “joke” – a thing that someone says to cause amusement – turning the name into something unintended and causing confusion.

To prevent such misinterpretations, we can use the `translate` attribute with the value `"no"` to disable automatic translation for specific pieces of content:

```html
<!-- Original content in English -->
<p>Name: <span translate="no">Joke</span></p>
<p>Email: <span translate="no">joke@test.com</span></p>

<!-- Translated content in Dutch -->
<p>Naam: <span translate="no">Joke</span></p>
<p>E-mailadres: <span translate="no">joke@test.com</span></p>
```

With this adjustment, the display remains accurate across languages, preventing incorrect translations and enhancing user trust. Misleading translations can create uncertainty and may cause users to double-check information unnecessarily, impacting accessibility, usability, and overall experience. Ideally, users should navigate with confidence, and as developers, we can implement this small change to make their experience smoother.

<p class="highlight">
<strong>Note:</strong> Before the <code>translate</code> attribute was part of the HTML specification, translation engines offered similar tools. For example, Google and Microsoft’s translation engines support the class <code>notranslate</code>, which worked similarly:
</p>

```html
<p>Name: <span class="notranslate">Joke</span></p>
<p>Email: <span class="notranslate">joke@test.com</span></p>
```

However, using the `translate="no"` attribute, which is now part of the HTML specification, is a more robust and reliable approach, ensuring consistency across current and future translation APIs and localization standards.

<!-- SS: Maybe link the "HTML specification" phrase to something like https://www.w3.org/International/questions/qa-translate-flag? -->