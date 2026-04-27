# Rapport LAB 1 — Setup Frida

**Date :** 27/04/2026
**Analyste :** Oussama Bagy
**Émulateur :** Android Emulator 5554 (API 30, x86)
**Frida :** v17.9.1

---

## 1. Installation de Frida



Frida a été installé avec succès sur l’environnement Windows avec **Python 3.10.11**.
La vérification a confirmé la présence de la version : **17.9.1**.

---

## 2. Vérification de l’environnement Android

[📸 Photo 3 — adb devices]
[📸 Photo 4 — ro.product.cpu.abi = x86]

L’émulateur Android a été détecté correctement via ADB.

**Informations relevées :**

* Identifiant : **emulator-5554**
* Architecture CPU : **x86 (ia32)**

---

## 3. Déploiement de frida-server

[📸 Photo 5 — push + chmod + lancement]

Le serveur Frida a été transféré vers l’émulateur Android puis exécuté.

**Commandes utilisées :**

* `adb push frida-server /data/local/tmp/`
* `chmod 755 frida-server`
* `./frida-server &`

Le serveur a démarré en arrière-plan avec succès.

---

## 4. Test de communication

[📸 Photo 6 — frida-ps -U]

Le test de connexion a confirmé que **Frida communique correctement avec l’émulateur**, avec affichage de la liste des processus Android actifs.

---

## 5. Injection Java

[📸 Photo 7 — Java.perform OK]

Un script JavaScript `hello.js` a été injecté dans l’application :

`owasp.mstg.uncrackable1`

Le script a exécuté correctement la fonction :

`Java.perform()`

**Résultat observé :**
`[+] Frida Java.perform OK`

---

## 6. Console interactive

[📸 Photo 8 — Process.arch]
[📸 Photo 9 — Process.mainModule]
[📸 Photo 10 — Java.available]

Les informations récupérées depuis la console interactive sont :

* `Process.arch` = **ia32**
* `Process.mainModule` = **app_process32**
* `Java.available` = **true**

Ces résultats confirment que l’instrumentation Java fonctionne correctement.

---

## 7. Détection des bibliothèques cryptographiques

[📸 Photo 11 — libssl + libcrypto]

Les bibliothèques de chiffrement présentes dans le processus ont été identifiées.

**Bibliothèques détectées :**

* `libcrypto.so` → OpenSSL
* `libjavacrypto.so` → Java Crypto
* `libssl.so` → TLS / SSL

---

## 8. Hook de débogage Java

[📸 Photo 12 — Hook Debug chargé]

Le script `hook_debug.js` a été injecté afin d’intercepter la méthode :

`isDebuggerConnected()`

**Résultat :**
`[+] Hook Debug chargé`

Cette étape montre la capacité de Frida à modifier dynamiquement le comportement d’une application Android.

---

## 9. Nettoyage de l’environnement

[📸 Photo 13 — pkill frida-server]

Le serveur Frida a été arrêté proprement après la fin des tests.

**Commande utilisée :**

* `pkill frida-server`

L’environnement a ainsi été remis dans son état initial.

---

## Conclusion

Ce laboratoire a permis de :

* Installer et configurer Frida sur Windows
* Déployer `frida-server` sur un émulateur Android
* Vérifier la communication avec l’appareil
* Injecter des scripts JavaScript dans une application
* Explorer un processus Android en mémoire
* Identifier des bibliothèques sensibles
* Hooker des méthodes Java critiques

Ce lab constitue une base essentielle pour l’analyse dynamique et le reverse engineering d’applications Android avec Frida.
