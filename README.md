<p align="center">
	<img src="https://user-images.githubusercontent.com/63207451/131482957-0f2b9fdb-4e04-4945-87fe-5b193d2c86d4.png" height="200">
<p/>


<h1 align="center">Robotique</h1>

<br>

<p align="center">
Ce repository est une introduction à la robotique. Je vais utiliser pour cela divers outils électroniques, comme la carte Arduino Uno avec laquelle je ferai dans un premier temps des circuits électriques simples, avec des LED, des résistances etc. Puis j'utiliserai un RaspberryPi. Ensuite, je mettrai les compétences acquises avec ces outils en œuvre, au travers de projets concrets sur robots à l'aide d'<b>Arduino</b>, de <b>RaspberryPi</b>, et également avec l'utilisation du système d'exploitation <b>ROS</b> (Robot Operating System). Cette documentation est faite dans un premier temps pour mon propre apprentissage mais pourra également être utile pour toute personne souhaitant se lancer dans la robotique.
Je partagerai toutes les ressources, tels que les documentations, vidéos, tuto, et les achats que je ferai.
<br>
<p/>

<br>

# Liens utiles

- Chaîne YouTube [U=RI](https://www.youtube.com/channel/UCVqx3vXNghSqUcVg2nmegYA) <br>

- Chaîne YouTube [BoilingBrains](https://www.youtube.com/channel/UCKAzZCVzqkdvxX6VLTwyVMQ) <br>


<br>

# Index

1. [La carte Arduino](#La-carte-Arduino)
    1. [Premiers pas avec la carte](#Premiers-pas-avec-la-carte)
        1. [Matériel](#1-Matériel)
        2. [Circuit LED clignotante](#2-Circuit-LED-clignotante)
        3. [Circuit LED avec interrupteur](#3-Circuit-LED-avec-interrupteur)
    3. [Programmation Arduino avec le Robot Elegoo](#Programmation-Arduino-avec-le-Robot-Elegoo)
        1. [Présentation du robot](#presentation-du-robot)
        2. [Montage](#Montage)
        3. [Test de ses fonctionnalités natives](#Test-de-ses-fonctionnalités-natives)
        4. [re-Programmation du robot](#reProgrammation-du-robot)
2. [RaspberryPi](#RaspberryPi)
3. [ROS](#Ros)

<br>
<br>

# La carte Arduino

## Premiers pas avec la carte

### 1. Matériel

- Pour la partie **programmation**, j'utilise le logiciel [Arduino](https://www.arduino.cc/en/software), disponible sur Mac, Windows et Linux. 

L'interface de programmation du logiciel est la suivante : 

```c
void setup(){

}

void loop(){

}

```

La première fonction **setup** est automatiquement exécutée une seule fois lorsque le programme demarre. C'est dans cette fonction qu'il faut mettre toutes les initialisations nécessaires au fonctionnnement du programme.

La deuxième fonction **loop** s'exécute indéfiniment en boucle, c'est là que nous allons mettre les instructions pour controler l'alimentation notamment.  <br>
<br>

- Pour la partie **électronique**, j'utilise une carte Arduino Uno Elegoo disponible avec le robot [Elegoo](https://www.amazon.fr/dp/B078Y9RYM2/ref=cm_sw_r_cp_api_glt_i_dl_2B12HJED9FP60AX0EKTV?_encoding=UTF8&psc=1), et pour la breadboard et tous les composants j'ai acheté un [kit de composants](https://www.amazon.fr/dp/B093BZVCT2/ref=cm_sw_r_cp_api_glt_i_WCNA03QZNRC70HV5HRB7?_encoding=UTF8&psc=1) sur Amazon.

<br>

### 2. Circuit LED clignotante

- Branchements :

La borne positive de la LED (branche longue) est en position d63 et la borne négative (branche courte) est reliée à une patte de la résistance en d62, l'autre patte de la résistance arrive sur un connecteur de la ligne noire qui sera utilisée comme ligne de masse.
Pour finir, On relie ça à la carte Arduino. La ligne de masse de la breadboard (fil noir) est reliée à une des bornes GND de la carte (borne de masse de la carte). La borne + de la LED (fil rouge) est reliée à la borne numérique (digital) numéro 2 de la carte.

<p align="center">
      <img src="https://user-images.githubusercontent.com/63207451/131386637-66ce16c6-93bb-44d0-9f6c-a92942717dc0.jpeg" height="400">
      <img src="https://user-images.githubusercontent.com/63207451/131386700-c1aff9a2-0863-4447-88d6-8bcdef4fe5e9.jpeg" height="400">
	<p/>


- Programme :

```c
void setup(){
  pinMode(2,OUTPUT);
}

void loop(){
  digitalWrite(2,HIGH);
  delay(1000); // en millisecondes 
  digitalWrite(2,LOW);
  delay(1000);
}
```

On règle la borne numérique numéro 2 de la carte Arduino en mode sortie (OUTPUT) dans la fonction setup. <br>
Pour faire clignoter de la LED il faut utiliser la commande digitalWrite qui permet de commander la présence ou non de courant sur une borne numérique de la carte Arduino. Ainsi, en jouant avec la commande delay() qui permet de faire des pauses dans l'exécution on obtient une LED clignotante.

- Résultat :

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131389379-cfc6918e-1a3c-479b-80d6-7bb8af7ab545.gif" height="450">
	<p/>

### 3. Circuit LED avec interrupteur

- Branchements :

<p align="center">
      <img src="https://user-images.githubusercontent.com/63207451/131406133-7d2105a3-8853-4936-9488-da7b28e8e68c.jpeg" height="450">
	<p/>


- Programme :

```c
#define LED_PIN 8
#define BUTTON_PIN 7

byte lastButtonState = LOW;
byte ledState = LOW;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT);
}

void loop() {
  byte buttonState = digitalRead(BUTTON_PIN);
  if (buttonState != lastButtonState) {
    lastButtonState = buttonState;
    if (buttonState == LOW) {
      ledState = (ledState == HIGH) ? LOW: HIGH;
      digitalWrite(LED_PIN, ledState);
    }
  }
}
```

- Résultat :

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131406957-7a7544bc-bc36-4695-9e7d-22d1f81f0952.gif" height="400">
	<p/>


## Programmation Arduino avec le Robot Elegoo

<br>

<br>

<br>

<p align="center"><a href="#Index"><img src="http://randojs.com/images/backToTopButton.png" alt="Haut de la page" height="29"/></a></p>

<br>

<p align="center">
  <a href="https://github.com/antonin-lfv" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97302854-e484da80-1859-11eb-9374-5b319ca51197.png" title="GitHub" width="40" height="40"></a>
  <a href="https://www.linkedin.com/in/antonin-lefevre-565b8b141" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97303444-b2c04380-185a-11eb-8cfc-864c33a64e4b.png" title="LinkedIn" width="40" height="40"></a>
  <a href="mailto:antoninlefevre45@icloud.com" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97303543-cec3e500-185a-11eb-8adc-c1364e2054a9.png" title="Mail" width="40" height="40"></a>
</p>


---------------------------
