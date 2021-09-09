<p align="center">
	<img src="https://user-images.githubusercontent.com/63207451/131482957-0f2b9fdb-4e04-4945-87fe-5b193d2c86d4.png" height="200">
<p/>


<h1 align="center">Robotique</h1>

<br>

<p align="center">
Ce repository est une introduction à la robotique. Je vais utiliser pour cela divers outils électroniques, comme la carte Arduino Uno avec laquelle je ferai dans un premier temps des circuits électriques simples, avec des LED, des résistances, des photocapteurs, des panneaux digitaux etc. Puis j'utiliserai un RaspberryPi. Ensuite, je mettrai les compétences acquises avec ces outils en œuvre, au travers de projets concrets sur robots à l'aide d'<b>Arduino</b>, de <b>RaspberryPi</b>, et également avec l'utilisation du système d'exploitation <b>ROS</b> (Robot Operating System). Cette documentation est faite dans un premier temps pour mon propre apprentissage mais pourra également être utile pour toute personne souhaitant se lancer dans la robotique.
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
        4. [Feu tricolore et piéton](#4-Feu-tricolore-et-piéton)
        5. [Générateur de nombres aléatoires avec photocapteur](#5-générateur-de-nombres-aléatoires-avec-photocapteur)
        6. [Compte à rebours 4-digits](#6-Compte-à-rebours)
    3. [Programmation Arduino avec le Robot Elegoo](#Programmation-Arduino-avec-le-Robot-Elegoo)
        1. [Présentation du robot](#présentation-du-robot)
        2. [Montage](#Montage)
        3. [Test de ses fonctionnalités natives](#Test-de-ses-fonctionnalités-natives)
        4. [re-Programmation du robot](#reProgrammation-du-robot)
2. [RaspberryPi](#RaspberryPi)
3. [ROS](#Ros)
    1. [Introduction](#Introduction)

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

- Pour la partie **électronique**, j'utilise une carte **Arduino Uno** de Elegoo disponible [ici](https://www.amazon.fr/gp/product/B01N91PVIS/ref=ppx_yo_dt_b_asin_image_o01_s00?ie=UTF8&psc=1) et la carte **Arduino Uno** de Smraza disponible avec le kit [Smraza](https://www.amazon.fr/gp/product/B01L1XRUKW/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1). Pour la breadboard et tous les composants j'ai acheté un [kit de composants](https://www.amazon.fr/dp/B093BZVCT2/ref=cm_sw_r_cp_api_glt_i_WCNA03QZNRC70HV5HRB7?_encoding=UTF8&psc=1) sur Amazon. (En plus de la petite breadboard du kit Smraza)

<br>

### 2. Circuit LED clignotante

- Branchements :

La borne positive de la LED (branche longue) est en position d63 et la borne négative (branche courte) est reliée à une patte de la résistance en d62, l'autre patte de la résistance arrive sur un connecteur de la ligne noire qui sera utilisée comme ligne de masse.
Pour finir, On relie ça à la carte Arduino. La ligne de masse de la breadboard (fil noir) est reliée à une des bornes GND de la carte (borne de masse de la carte). La borne + de la LED (fil rouge) est reliée à la borne numérique (digital) numéro 2 de la carte.

<br>

<p align="center">
      <img src="https://user-images.githubusercontent.com/63207451/131386637-66ce16c6-93bb-44d0-9f6c-a92942717dc0.jpeg" height="400">
      <img src="https://user-images.githubusercontent.com/63207451/131386700-c1aff9a2-0863-4447-88d6-8bcdef4fe5e9.jpeg" height="400">
	<p/>

<br>

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

<br>

- Résultat :
<br>

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131389379-cfc6918e-1a3c-479b-80d6-7bb8af7ab545.gif" height="450">
	<p/>
<br>

### 3. Circuit LED avec interrupteur

- Branchements :

Vous aurez besoin de 6 fils, 1 LED, 1 bouton, 1 résistance de 220Ω (pour la LED) et une résistance de 330Ω (pour le bouton).

<br>

<p align="center">
      <img src="https://user-images.githubusercontent.com/63207451/131406133-7d2105a3-8853-4936-9488-da7b28e8e68c.jpeg" height="450">
	<p/>

<br>

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
      ledState = (ledState == HIGH) ? LOW: HIGH; // Si ledState = HIGH alors on lui donne la valeur LOW, sinon il reste à HIGH
      digitalWrite(LED_PIN, ledState);
    }
  }
}
```

On change l'état de la sortie de la LED dès que le bouton est pressé.
<br>

- Résultat :
<br>

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131406957-7a7544bc-bc36-4695-9e7d-22d1f81f0952.gif" height="400">
	<p/>
<br>

### 4. Feu tricolore et piéton

- Branchements :

Vous aurez besoin de 2 LED vertes, 2 LED rouges, 1 LED Orange, 6 fils et 5 résistances de 220Ω. Toutes les LED sont branchées directement et indépendamment des autres.
Les 3 LED du haut représentent le feu pour les voitures, et les 2 LED du bas représentent le feu pour les piétons.
<br>

<p align="center">
      <img src="https://user-images.githubusercontent.com/63207451/131541867-2846579e-8e17-4b05-8184-1286aa6c0a24.jpeg" height="450">
      <img src="https://user-images.githubusercontent.com/63207451/131541880-de832cd1-5251-4e71-bc86-f6971fedf710.jpeg" height="450">
	<p/>
<br>

- Programme :

```c
// Temps par couleur et feu
int tempsAttente_rouge = 5000;
int tempsAttente_orange = 1000;
int tempsAttente_vert = 5000;

int temps_traversee = 1000; // Temps pour laisser les piétons et voitures passer entre les feux

 
void setup(){
  pinMode(10, OUTPUT);    // Rouge voiture
  pinMode(9, OUTPUT);     // orange voiture
  pinMode(8, OUTPUT);     // Vert voiture
  
  pinMode(4, OUTPUT);     // Rouge piéton
  pinMode(3, OUTPUT);     // Vert Piéton
}

void loop() {
  digitalWrite(10, HIGH);     // feu rouge voiture allumé
  delay(temps_traversee);     
  
  digitalWrite(4, LOW);       // feu rouge piéton éteint
  digitalWrite(3, HIGH);      // feu vert piéton allumé
  delay(tempsAttente_rouge);
  
  digitalWrite(3, LOW);       // feu vert piéton éteint
  digitalWrite(4, HIGH);      // feu rouge piéton allumé
  delay(temps_traversee);
  
  digitalWrite(10, LOW);      // feu rouge voiture éteint
  digitalWrite(8, HIGH);      // feu vert voiture allumé
  delay(tempsAttente_vert);
  
  digitalWrite(9, HIGH);      // feu orange voiture allumé
  digitalWrite(8, LOW);       // feu vert voiture éteint
  delay(tempsAttente_orange);
  
  digitalWrite(9, LOW);       // feu orange voiture éteint
}

```

On ajoute temps_traversee pour gérer les piétons ou voitures qui finissent de passer.
<br>

- Résultat :

<br>
<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131638632-52da7fbb-754d-4c10-91b9-fba06333820f.gif" height="400">
	<p/>

<br>

### 5. Générateur de nombres aléatoires avec photocapteur

<br>

- Branchements :

|Le photocapteur |<img src="https://user-images.githubusercontent.com/63207451/131916385-b3c5d303-e366-4ca8-b60e-288ebe19d089.jpeg" height="500">|
|---|:---:|
|Les LED|<img src="https://user-images.githubusercontent.com/63207451/131916403-d116d186-109f-4fb7-abf8-18de5eb8e5b5.jpeg" height="500">|
|L'ensemble|<img src="https://user-images.githubusercontent.com/63207451/131916651-ca249960-5d1c-4af4-b562-bde6b5f72509.jpeg" height="400">|

<br>

- Programme :

<br>

```c
const int ECART=60;
const int TEMPO=2000;

void setup(){
  randomSeed(analogRead(1));
  for(int i=2;i<=8;i++){
    pinMode(i,OUTPUT);
  } 
}
void loop(){
  int luminosite1=analogRead(0);
  delay(100);
  int luminosite2=analogRead(0);
  if(luminosite2-luminosite1>ECART){
  
    afficheDe(random(1,7));
    delay(TEMPO);
    eteintDe();
  }
}
void afficheDe(int nombre){

  if(nombre==1){
    digitalWrite(3,HIGH);
  }
  
  if(nombre==2){
    digitalWrite(2,HIGH);
    digitalWrite(6,HIGH);
  }

  if(nombre==3){
    digitalWrite(2,HIGH);
    digitalWrite(6,HIGH);
    digitalWrite(3,HIGH);
  }

  if(nombre==4){
    digitalWrite(2,HIGH);
    digitalWrite(5,HIGH);
    digitalWrite(6,HIGH);
    digitalWrite(8,HIGH);
  }
  if(nombre==5){
    digitalWrite(2,HIGH);
    digitalWrite(3,HIGH);
    digitalWrite(6,HIGH);
    digitalWrite(8,HIGH);
    digitalWrite(5,HIGH);
  }

  if(nombre==6){
    digitalWrite(2,HIGH);
    digitalWrite(3,HIGH);
    digitalWrite(4,HIGH);
    digitalWrite(6,HIGH);
    digitalWrite(7,HIGH);
    digitalWrite(8,HIGH);
  }
}
void eteintDe(){
  for(int i=2;i<=8;i++){
    digitalWrite(i,LOW);
  }
}
```

<br>

- Résultat : À chaque changement de luminosité un nombre aléatoire de LED va s'allumer.

<br>

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131919109-1b0e7a59-c6cb-4f0d-b29a-cb84a8bcdbe9.gif" height="400">
	<p/>

<br>

### 6. Compte à rebours

- Branchements :

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/132715727-6086545f-638c-4c58-91bc-210944b8b87f.png" height="400">
	<p/>

<br>

- Programme :

```c
#define NUM_OF_DIGITS 4

int latch = 4; //74HC595  pin 9 STCP
int cs = 5; //74HC595  pin 10 SHCP
int data = 3; //74HC595  pin 8 DS
int dPins[4] = {11, 10, 9, 8};

unsigned char table[] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x90};

int digit_data[NUM_OF_DIGITS] = {0};

void setup() {
  Serial.begin(115200);
  pinMode(latch, OUTPUT);
  pinMode(cs, OUTPUT);
  pinMode(data, OUTPUT);

  for (int j = 0; j < NUM_OF_DIGITS; j++) pinMode(dPins[j], OUTPUT);

}

void loop() {

  for (int mill=9; mill>-1; mill--){
    for (int cent=9; cent>-1; cent--){
      for (int diz=9; diz>-1; diz--){
        for (int unite=9; unite>-1; unite--){
            Display(3,unite);
            delay(5);
            Display(2,diz);
            delay(5);
            Display(1,cent);
            delay(5);
            Display(0,mill);
            delay(5);
          }
       }
     }
   }
 }


void Display(int id, unsigned char num)
{
  digitalWrite(latch, LOW);
  shiftOut(data, cs, MSBFIRST, table[num]);
  digitalWrite(latch, HIGH);
  for (int j = 0; j < NUM_OF_DIGITS; j++) digitalWrite(dPins[j], LOW);
  digitalWrite(dPins[id], HIGH);
}

```

<br>

- Résultat :

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/132717750-c9e3c9e1-ebe9-477d-8a83-fb92adfa66f6.gif" height="500">
	<p/>

<br>
<br>

## Programmation Arduino avec le Robot Elegoo

<br>

### Présentation du robot

Le robot [Elegoo V4.0](https://www.amazon.fr/dp/B078Y9RYM2/ref=cm_sw_r_cp_api_glt_i_dl_2B12HJED9FP60AX0EKTV?_encoding=UTF8&psc=1) est un robot commandé par une carte Arduino Uno. Il est conçu pour les débutants dans le domaine de la robotique et de l'arduino.

Contenu de la boite :

<br>

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131652126-f72489bb-a37c-4d6c-881f-0e2f7d7f0034.png" height="300">
<img src="https://user-images.githubusercontent.com/63207451/131652194-d1e1caeb-0113-4363-a1ab-843c6352b4fa.png" height="300">
	<p/>

<br>

Caractéristiques :

<center>
	
|Les modes|Les capteurs|
|:--------|:-----------|
|- Évitement d'obstacles|- Capteur ultrasons|
|- Suivi de ligne|- Module de suivi de ligne|
|- Suivi d'un objet qui se déplace devant lui|- Caméra|
|- Vue en première personne| |
|- Contrôle à distance| |
	
</center>

<br>

### Montage

<br>

Plateforme avec la carte arduino, la caméra, le capteur ultrasons et la batterie sur la plateforme des moteurs :

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131740427-8e0de7da-89b4-4e3b-bc3e-2c4fb9dcb53c.jpeg" height="400">
<img src="https://user-images.githubusercontent.com/63207451/131740545-be2181ea-a9ec-4063-9842-f01b64d00cc5.jpeg" height="400">
</p>
<br>

Branchements des composants :

<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131740583-e1e404ef-617d-4bbb-963e-ea6c6f4b4c66.jpeg" height="400">
</p>
<br>

Robot fini :
	
<p align="center">
<img src="https://user-images.githubusercontent.com/63207451/131740635-0fb85701-6383-4bd1-bb8a-8148fee5d11e.jpeg" height="400">
<img src="https://user-images.githubusercontent.com/63207451/131741265-c1e43240-e979-4644-b434-5a178096cd9d.jpeg" height="400">
</p>
<br>

<br>

<br>

<br>

# ROS : Robot Operating System

## Introduction


Les cadres logiciels basés sur ROS exécutent les algorithmes et processus de haut niveau tels que l'inférence des modèles de robot, le filtrage, la génération de stratégies de mouvement, les algorithmes de contrôle, etc. Un contrôleur monté sur un robot est utilisé pour effectuer le contrôle et la détection de bas niveau/embarqué. Il comprend tout ou partie de la commande du moteur, des capteurs de température et à ultrasons, des IMU et des encodeurs de roue, ainsi que d'autres dispositifs.

<br>

<p align="center">
<img width="727" alt="Capture d’écran 2021-09-09 à 18 02 21" src="https://user-images.githubusercontent.com/63207451/132721488-a5ea48c8-5148-4a02-b3d4-9828a7031845.png">
</p>

<br>

<p align="center"><a href="#Index"><img src="http://randojs.com/images/backToTopButton.png" alt="Haut de la page" height="29"/></a></p>

<br>

<p align="center">
  <a href="https://github.com/antonin-lfv" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97302854-e484da80-1859-11eb-9374-5b319ca51197.png" title="GitHub" width="40" height="40"></a>
  <a href="https://www.linkedin.com/in/antonin-lefevre-565b8b141" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97303444-b2c04380-185a-11eb-8cfc-864c33a64e4b.png" title="LinkedIn" width="40" height="40"></a>
  <a href="mailto:antoninlefevre45@icloud.com" class="fancybox" ><img src="https://user-images.githubusercontent.com/63207451/97303543-cec3e500-185a-11eb-8adc-c1364e2054a9.png" title="Mail" width="40" height="40"></a>
</p>


---------------------------
