
<h1 align="center">Robotique</h1>

<br>

<p align="center">
Ce repository sera constitué d'une introduction à la robotique, au travers de projets concrets sur robots à l'aide de cartes <b>Arduino</b> puis de <b>RaspberryPi</b>, mais aussi avec l'utilisation du système d'exploitation <b>ROS</b> (Robot Operating System). Cette documentation est faite dans un premier temps pour mon propre apprentissage mais pourra également être utile pour toute personne souhaitant se lancer dans la robotique.
Je partagerai toutes les ressources, tels que les documentations, vidéos, tuto, et les achats que je ferai.
<br>
<p/>

<br>

# Liens utiles

- Chaîne YouTube [U=RI](https://www.youtube.com/channel/UCVqx3vXNghSqUcVg2nmegYA) <br>

- Chaîne YouTube [BoilingBrains](https://www.youtube.com/channel/UCKAzZCVzqkdvxX6VLTwyVMQ) <br>


<br>

# Index

1. [Arduino](#Arduino)
    1. [Premiers pas](#Premiers-pas)
        1. [Matériel](#Materiel)
        2. [LED clignotante](#LED-clignotante)
        3. [LED en série](#LED-en-série)
    3. [Robot Elegoo](#Robot-Elegoo)
        1. [Présentation](#presentation)
        2. [Montage](#Montage)
2. [RaspberryPi](#RaspberryPi)
3. [ROS](#Ros)

<br>
<br>

# Arduino

## Premiers pas

### 1. Matériel

‣ Pour la partie **programmation**, j'utilise le logiciel [Arduino](https://www.arduino.cc/en/software), disponible sur Mac, Windows et Linux. 

L'interface de programmation du logiciel est la suivante : 

```c
void setup(){

}

void loop(){

}

```

La première fonction **setup** est automatiquement exécutée une seule fois lorsque le programme demarre. C'est dans cette fonction qu'il faut mettre toutes les initialisations nécessaires au fonctionnnement du programme.

La deuxième fonction **loop** s'exécute indéfiniment en boucle, c'est là que nous allons mettre les instructions pour controler l'alimentation notamment.  <br>

‣ Pour la partie **électronique**, j'utilise une carte Arduino Uno Elegoo disponible avec le robot [Elegoo](https://www.amazon.fr/dp/B078Y9RYM2/ref=cm_sw_r_cp_api_glt_i_dl_2B12HJED9FP60AX0EKTV?_encoding=UTF8&psc=1), et pour la breadboard et tous les composants j'ai acheté un [kit de composants](https://www.amazon.fr/dp/B093BZVCT2/ref=cm_sw_r_cp_api_glt_i_WCNA03QZNRC70HV5HRB7?_encoding=UTF8&psc=1) sur Amazon.

<br>

### 2. LED clignotante

‣ Branchements :

<p align="center">
      <img src="https://user-images.githubusercontent.com/63207451/131386637-66ce16c6-93bb-44d0-9f6c-a92942717dc0.jpeg" height="800">
      <img src="https://user-images.githubusercontent.com/63207451/131386700-c1aff9a2-0863-4447-88d6-8bcdef4fe5e9.jpeg" height="800">
	<p/>



‣ Programme :

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
Pour faire clignoter de la LED il faut utiliser la commande digitalWrite qui permet de commander la présence ou non de courant sur une borne numérique de la carte Arduino. Ainsi, en jouant avec la commande delay() qui permet de faire des pauses dans l'exécution on obtient une LED clignotante :

### 3. LED en série




