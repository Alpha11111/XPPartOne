---
layout: default
title: "Integrating Google Analytics with Cookie Consent"
excerpt: 'Google GDPR for Shopify'
date: 2025-02-10
permalink: /goolge-gdpr/
---

<h2> Integrating Google Analytics with Cookie Consent</h2>

This article explains how to integrate Google Analytics with Cookie Consent mode on a website using JavaScript and HTML.

<h4> Google Analytics Setup</h4>

First, you need to load the Google Analytics tracking script. Below is the script required for integrating Google Analytics with Consent Mode:

```html
<!-- Google Analytics (gtag.js) with Consent Mode -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXX"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
// Initialize Google Consent Mode with default 'deny' tracking
gtag('consent', 'default', {
'ad_storage': 'denied',
'analytics_storage': 'denied',
'personalization_storage': 'denied'
});
// Initialize Google Analytics configuration
gtag('js', new Date());
gtag('config', 'G-XXXXXX', { anonymize_ip: true });
</script>
<style>
#cookie-banner {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  width: 90%;
  max-width: 400px;
  background: #fff;
  padding: 15px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  font-family: Arial, sans-serif;
  font-size: 14px;
  text-align: center;
  display: flex;
  flex-direction: column;
  z-index: 9999;
}
.btn-yes {
  background: #0073e6;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}
.btn-no {
  background: #e0e0e0;
  color: #333;
  border: none;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}
</style>

<!-- Cookie Consent Banner -->
<div id="cookie-banner" style="display:none">
  <p style="margin: 0; color: #333;">We use cookies to enhance your experience. Do you consent?</p>
  <button class="btn-yes" onclick="acceptCookies()">Accept</button>
  <button class="btn-no" onclick="rejectCookies()">Deny</button>
</div>
<script>
function setCookie(name, value, days) {
  let expires = "";
  if (days) {
    let date = new Date();
    date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
    expires = "; expires=" + date.toUTCString();
  }
  document.cookie = name + "=" + value + "; path=/; SameSite=Lax; Secure" + expires;
}

function getCookie(name) {
  let match = document.cookie.match(new RegExp('(^| )' + name + '=([^;]+)'));
  return match ? match[2] : null;
}

function showCookieBanner() {
  let userLang = navigator.language || navigator.userLanguage;
  let userTimeZone = Intl.DateTimeFormat().resolvedOptions().timeZone; // Get the time zone
  let euLanguages = ["de", "fr", "es", "it", "nl", "pl", "sv", "da", "fi", "cs", "hu", "pt", "el", "sk", "lt", "lv", "et", "bg", "ro", "sl", "hr", "mt"];
  let euTimeZones = [
    "Europe/Amsterdam", "Europe/Andorra", "Europe/Athens", "Europe/Belgrade", "Europe/Berlin", "Europe/Bratislava",
    "Europe/Brussels", "Europe/Bucharest", "Europe/Budapest", "Europe/Chisinau", "Europe/Copenhagen",
    "Europe/Dublin", "Europe/Gibraltar", "Europe/Helsinki", "Europe/Lisbon", "Europe/Ljubljana", "Europe/London",
    "Europe/Luxembourg", "Europe/Madrid", "Europe/Malta", "Europe/Oslo", "Europe/Paris", "Europe/Prague",
    "Europe/Riga", "Europe/Rome", "Europe/Stockholm", "Europe/Tallinn", "Europe/Vienna", "Europe/Vilnius", "Europe/Warsaw"
  ]; // EU and major European time zones

  if (euLanguages.some(lang => userLang.startsWith(lang)) || euTimeZones.includes(userTimeZone)) {
    let consent = getCookie('user_consent');
    if (!consent) {
      document.getElementById('cookie-banner').style.display = 'block';
    }
  }
}

function acceptCookies() {
  setCookie('user_consent', 'granted', 365);
  gtag('consent', 'update', {
    'ad_storage': 'granted',
    'analytics_storage': 'granted',
    'personalization_storage': 'granted'
  });
  document.getElementById('cookie-banner').style.display = 'none';
}

function rejectCookies() {
  setCookie('user_consent', 'denied', 365);
  document.getElementById('cookie-banner').style.display = 'none';
}

window.onload = showCookieBanner; // Check location on page load
</script>
