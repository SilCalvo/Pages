
<html><head>
  
  <meta content="text/html; charset=ISO-8859-1" http-equiv="content-type">
  <title>P2_Follow_Line</title>


  <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background-image: url('images.png'); /* Asegúrate de que la ruta sea correcta */
            background-size: cover; /* Asegura que la imagen cubra todo el fondo */
           background-repeat: no-repeat; /* No repetir la imagen */
            background-attachment: fixed; /* Mantiene la imagen fija */
            background-position: center; /* Centra la imagen */
            color: white; /* Cambia el color del texto si es necesario */
            height: 100vh; /* Asegura que el body tenga altura completa */
            display: flex; /* Usamos flexbox para alinear el contenido */
        }
        .sidebar {
            width: 200px; /* Ancho del índice */
            position: sticky; /* Fijo al desplazarse */
            top: 0; /* Se mantiene en la parte superior */
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.7); /* Fondo semi-transparente */
            border-radius: 8px; /* Bordes redondeados */
            margin-right: 20px; /* Espaciado a la derecha */
        }
        .content {
            padding: 20px; /* Espaciado alrededor del contenido */
            background-color: rgba(0, 0, 0, 0.5); /* Fondo semi-transparente para mejorar la legibilidad */
            max-width: 800px; /* Limita el ancho del contenido */
            margin: auto; /* Centra el contenido */
            border-radius: 8px; /* Bordes redondeados */
            flex: 1; /* Permite que el contenido ocupe el espacio restante */
        }
    </style>
</head><body>
<div class="sidebar">
<h3>Índice</h3>
<ul>
  <li><a href="#INTRODUCCION">Introducción</a></li>
  <li><a href="#PID">PID</a></li>
  <li><a href="#MODELOS_SIMPLE_VS_ACKERMAN">Modelo Simple vs Ackerman</a></li>
  <li><a href="#PROCESAMIENTO_DE_IMAGEN">Procesamiento de Imagen</a></li>
  <li><a href="#CASOS_CONTROLADOS">Casos Controlados</a></li>
  <li><a href="#PRUEBAS">Pruebas</a></li>
  <li>Resultado Final</li>
</ul>
</div>

<div class="content">
<div style="text-align: center;"><big><big><span style="font-weight: bold;"> PRACTICA 2 FOLLOW LINE </span><br style="font-weight: bold;">
<span style="font-weight: bold;">
Silvia Calvo Cabello</span></big></big><br>
</div>

<br>
<ul>
  <li><a name="INTRODUCCION"></a><span style="font-weight: bold;">
INTRODUCCIÓN</span></li>
</ul>

Mediante Unibotics (página para la simulación de distintos proyectos)
realizar un programa para un coche de Fórmula 1 autónomo. Para ello
consta de una cámara frontal para reconocer la línea del circuito a
seguir. Este debe ser lo más rápido y estable posible, realizando este
control mediante un PID.<br>
<br>
<ul>
  <li><span style="font-weight: bold;"><a name="PID"></a>
PID</span></li>
</ul>

Es un controlador de lazo cerrado el cual intenta minimizar el error y
hacer el sistema lo más rápido posible. Existen varios tipos de estos
controladores (P, PD, PI, PID) <br><span style="font-weight: bold;">
P - Proporcional - </span>Es inversamente proporcional al error, cuanto mayor
sea su valor, más rápidamente reaccionará al error instantáneo.<br><span style="font-weight: bold;">
I - Integral </span>- Calcula la integral del error para minimizar el offset
(el error estable), cuanto mayor sea su valor ...<br><span style="font-weight: bold;">
D - Derivativo -</span> Calcula la derivada del error para suavizar o exagerar
los cambios del error, cuanto mayor sea su valor ...<br>
<br>
Para esta práctica se ha seleccionado un controlador <span style="font-weight: bold;">PD (kp*error +
kd*de/dt)</span>.
Como las muestras del sistema son discretas, para el derivativo se
calculará con la resta de tiempo entre muestras.<br>
<br>
<ul>
  <li><span style="font-weight: bold;"><a name="MODELOS_SIMPLE_VS_ACKERMAN"></a>
MODELOS SIMPLE VS ACKERMAN</span></li>
</ul>

Como ya he mencionado antes, para esta práctica se está usando
Unibotics para la simulación de los proyectos, y esta da dos opciones a
la hora de controlar el coche de Fórmula 1. Primero mediante el giro
roomba, indicando que la velocidad angular que recibe el modelo es la
que gira, está el modelo Ackerman, este funciona de manera que la
velocidad angular gira las ruedas principales del coche y las
secundarias no se mueven. Para esta práctica primero se realizará con
el modelo simple y después el Ackerman<br>
<br>
<ul>
  <li><span style="font-weight: bold;"><a name="PROCESAMIENTO_DE_IMAGEN"></a>
PROCESAMIENTO DE IMAGEN</span> </li>
</ul>

El coche de Fórmula 1 consta de una cámara de visión en la parte
frontal, para manejar dicha información necesitaremos las librerías de
OpenCV (cv2) y Numpy. <br>
Como la imagen recibida está a color y la línea a seguir es
distinguible, trabajaremos la imagen aplicando un filtro de color para
quedarnos solo con la línea roja (hay que tener en cuenta que hay
colores como el blanco que también tienen componente roja por lo que
hay que filtrar por ellos también). A continuación, para distinguir
hacia donde va la línea sacaremos de la una franja destacada (desde los
240 píxeles a los 280 píxeles en la componente y) sacaremos los índices
de todos estos píxeles que han pasado el filtrado y haremos una media,
de esta manera podremos comprobar hacia dónde va la línea comparándola
con el centro de la imagen. <br>
<br>
<ul>
  <li><span style="font-weight: bold;"><a name="CASOS_CONTROLADOS"></a>
CASOS CONTROLADOS</span></li>
</ul>
<ol>
  <li><span style="text-decoration: underline;">
No ver la línea al empezar el circuito:</span> Si al empezar el programa el
coche no ve la línea roja que debe seguir, girará hasta encontrarla.</li>
  <li><span style="text-decoration: underline;">
Calibración al inicio: </span>La cámara frontal no está situada en el centro
del coche, por lo que hay que calibrarla poniendo el coche en el centro
de la línea.</li>
  <li style="text-decoration: underline;">
Perder la línea en mitad del circuito:</li>
</ol>

<br>
<ul>
  <li><a name="PRUEBAS"></a><span style="font-weight: bold;">PRUEBAS</span></li>
</ul>
<span style="text-decoration: underline;">Primer internto: </span>Circuito:
Simple&nbsp; Conduccion: Simple Vision:RGB Controlador: PD(0.005 0.015)
Velocidad: 4 tiempo: 280 s Problemas: Va muy lento<br>
<br>
<span style="text-decoration: underline;">Segundo intento:</span>
Circuito: Simple&nbsp; Conduccion: Simple Vision:RGB Controlador:
PD(0.009 0.02) Velocidad: 8 tiempo: 130 s Problemas: Oscila bastante en
las curvas.<br>
<br>

<br>
</div>

</body></html>
