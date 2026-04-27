# Rapport LAB 1 — Setup Frida

**Date :** 27/04/2026
**Analyste :** Oussama Bagy
**Émulateur :** Android Emulator 5554 (API 30, x86)
**Frida :** v17.9.1

---

## 1. Installation de Frida

<img width="847" height="173" alt="image" src="https://github.com/user-attachments/assets/aa98c55a-c5a6-439e-95af-3dd222c3e4c1" />


Frida a été installé avec succès sur l’environnement Windows avec **Python 3.10.11**.
La vérification a confirmé la présence de la version : **17.9.1**.

---

## 2. Vérification de l’environnement Android

<img width="1322" height="189" alt="image" src="https://github.com/user-attachments/assets/5bea7bc1-23a5-42f0-9064-757f1b3751db" />


L’émulateur Android a été détecté correctement via ADB.

**Informations relevées :**

* Identifiant : **emulator-5554**
* Architecture CPU : **x86 (ia32)**

---

## 3. Déploiement de frida-server

<img width="1489" height="295" alt="image" src="https://github.com/user-attachments/assets/1247d6ba-15e6-4805-8a4f-80de7f2e7a73" />


Le serveur Frida a été transféré vers l’émulateur Android puis exécuté.

**Commandes utilisées :**

* `adb push frida-server /data/local/tmp/`
* `chmod 755 frida-server`
* `./frida-server &`

Le serveur a démarré en arrière-plan avec succès.

---

## 4. Test de communication

<img width="1272" height="625" alt="image" src="https://github.com/user-attachments/assets/b01f4c3b-0514-4e30-b058-29a65d82e487" />


Le test de connexion a confirmé que **Frida communique correctement avec l’émulateur**, avec affichage de la liste des processus Android actifs.

---

## 5. Injection Java

<img width="1368" height="450" alt="image" src="https://github.com/user-attachments/assets/5730ee0b-e23f-42e7-b357-1b9773a14827" />


Un script JavaScript `hello.js` a été injecté dans l’application :

`owasp.mstg.uncrackable1`

Le script a exécuté correctement la fonction :

`Java.perform()`

**Résultat observé :**
`[+] Frida Java.perform OK`

---

## 6. Console interactive

<img width="1107" height="682" alt="image" src="https://github.com/user-attachments/assets/63d2063f-012a-4770-92d4-21be504c0969" />

Les informations récupérées depuis la console interactive sont :

* `Process.arch` = **ia32**
* `Process.mainModule` = **app_process32**
* `Java.available` = **true**

Ces résultats confirment que l’instrumentation Java fonctionne correctement.

---

## 7. Détection des bibliothèques cryptographiques

<img width="1401" height="598" alt="image" src="https://github.com/user-attachments/assets/55123ab8-f0cb-4c14-9fc0-258e96dbbadb" />


Les bibliothèques de chiffrement présentes dans le processus ont été identifiées.

**Bibliothèques détectées :**

* `libcrypto.so` → OpenSSL
* `libjavacrypto.so` → Java Crypto
* `libssl.so` → TLS / SSL

---

## 8. Hook de débogage Java

<img width="1155" height="435" alt="image" src="https://github.com/user-attachments/assets/8da01057-1bb1-42e4-bc65-a842b0fc1d23" />


Le script `hook_debug.js` a été injecté afin d’intercepter la méthode :

`isDebuggerConnected()`

**Résultat :**
`[+] Hook Debug chargé`

Cette étape montre la capacité de Frida à modifier dynamiquement le comportement d’une application Android.

---

## 9. Nettoyage de l’environnement

<img width="1196" height="90" alt="image" src="https://github.com/user-attachments/assets/3fd4f89a-b36a-4fd4-8d76-6884fce73e42" />


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
