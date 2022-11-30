## Ad3
## Ejercicio de programación literaria 

En este ejercicio vamos a transformar un código de Python para lograr un scraping de una web, en un ejercicio de programación literaria con Jupyter.

Lo primero es que vamos a instalar las librerías que nos van a ayudar a leer el código phyton:


```python
! pip install requests
```

    Requirement already satisfied: requests in c:\users\luisa\anaconda3\lib\site-packages (2.28.1)
    Requirement already satisfied: certifi>=2017.4.17 in c:\users\luisa\anaconda3\lib\site-packages (from requests) (2022.9.14)
    Requirement already satisfied: idna<4,>=2.5 in c:\users\luisa\anaconda3\lib\site-packages (from requests) (3.3)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in c:\users\luisa\anaconda3\lib\site-packages (from requests) (1.26.11)
    Requirement already satisfied: charset-normalizer<3,>=2 in c:\users\luisa\anaconda3\lib\site-packages (from requests) (2.0.4)
    


```python
! pip install termcolor
```

    Collecting termcolor
      Downloading termcolor-2.1.1-py3-none-any.whl (6.2 kB)
    Installing collected packages: termcolor
    Successfully installed termcolor-2.1.1
    


```python
import requests
import time
import csv
import re
from bs4 import BeautifulSoup
import os
import pandas as pd
from termcolor import colored
```

Ahora vamos a llamar a la página de resultados.


```python
resultados = []
```

Y la información que vamos a descargar será de la URL del El País y en ella nos cercioramos de que no haya error.


```python
req = requests.get("https://resultados.elpais.com")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup = BeautifulSoup(req.text, 'html.parser')
```

Ahora le pedimos a la librería que encuentre y que luego imprima la información que le pedimos, en este caso todas las etiquetas "h2".


```python
tags = soup.findAll("h2")
```


```python
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    El Mundial, en vivo
    Universo Mundial
    El calendario a seguir desde América
    ¿Quién va a ganar? Simulador y pronóstico de cada selección 
    La ‘newsletter’
    Nueva York internará en psiquiátricos contra su voluntad a las personas sin hogar con trastornos mentales graves
    Boric y Castillo acuerdan celebrar en Lima la cumbre de la Alianza del Pacífico suspendida 
    El líder del grupo ultraderechista Oath Keepers, culpable por sedición por el asalto al Capitolio
    La doble respuesta de China a las protestas: acelerar la vacunación de los mayores y descabezar las manifestaciones 
    Rusia culpa a EE UU de la cancelación del encuentro bilateral sobre control de armas nucleares
    El autor cubano Carlos Manuel Álvarez gana el Premio Anagrama de Crónica
    Lectura del tarot con Gioconda Belli y Julián Herbert: “Una transmisión de energía en las cartas”
    Brenda Ríos: “Hace falta reírse de ‘Cien años de soledad”
    Una radiografía (incompleta) para descubrir qué está leyendo Latinoamérica
    El imperio contraataca: EE UU derrota a Irán y se mete en octavos
    Varvaridades
    Inglaterra golea a Gales (3-0) y se clasifica para octavos como primera de grupo
    Ecuador queda eliminada y Senegal  devuelve a África a los octavos
    Qatar se despide del Mundial con tres derrotas, la peor anfitriona de la historia
    ¿Qué opciones tiene cada selección para pasar a octavos de final del Mundial?
    Kirchner, a los jueces que la investigan: “Este tribunal es un pelotón de fusilamiento”
    Ideas neonazis y víctima de acoso: así es el joven que asesinó a cuatro personas en dos colegios de Brasil  
    ¿Dónde está La Barbie? El misterio revive el mito criminal de Édgar Valdez Villarreal
    Venezuela anuncia un crecimiento de 18 puntos del PIB para 2022
    Asesinado en Nariño el director de un canal de televisión regional durante un reportaje
    Una banda secuestra durante horas un hospital de Ecuador
    Darío Villamizar: “Es el final del ciclo guerrillero en América Latina”
    Gardel y el Barça, un idilio cien años escondido
    En busca de una solución para los dolores que se creían inventados
    Encontrarse en la transexualidad: la odisea de Harry, el chico que quiso ser monja
    Tragedia en la frontera de Melilla: el papel de Marruecos y España en las muertes del 24-J
    Agonía a ambos lados de la frontera de Melilla
    ‘Podcast’ | Cinco meses investigando la tragedia de Melilla
    Ideas de regalos para el jardinero
    Guía de regalos para el ‘foodie’
    Pon nombre a lo que te pasa para sentirte mejor
    Volver a empezar
    Borges, 'Funes el memorioso' y la neurona Jennifer Aniston
    Joseph Henrich, antropólogo: “El mejor antídoto contra el supremacismo blanco es discutir ideas”
    Así acaba el dinero de los fondos de inversión más verdes en empresas contaminantes
    Estados Unidos prepara una ley para evitar una huelga de ferrocarriles en vísperas de Navidad
    Una autopista para dejarse llevar
    Los ciberdelincuentes aprovechan el caos en Twitter para lanzar campañas de ‘phishing’
    Síntomas de rebeldía en China
    “¿De qué color es el hambre, mamá?”
    Enzensberger y la distancia crítica
    El siglo de María Pimentel
    ‘Que sepan que sabemos’: traducen los megaproyectos de López Obrador a lenguas indígenas
    América Latina puede convertirse en un referente mundial de la transición energética justa
    De luz y oscuridad: el 70% de los casos de ceguera infantil en México son prevenibles
    Las guatemaltecas que estudian ingeniería para llevar luz a sus comunidades
    Eliseo, ‘el encargado’ corrupto que seduce y repele en Argentina 
    ‘Canina’: la maternidad con pelo y colmillos
    Bono se desnuda emocionalmente en su concierto más atípico 
    Rolling Blackouts Coastal Fever, la banda de rock más chisporroteante y luminosa de Australia
    La lección magistral de Bob Dylan sobre Elvis
    ¿Selfie sí o selfie no en Art Basel?
    De las galerías a las calles: así se hizo importante Miami para el arte del mundo
    Jennifer Lopez pensó que “iba a morir” después de su ruptura con Ben Affleck
    Por qué encontrar pareja parece hoy misión imposible
    ¿A qué sabe un vino de 160 años? Apuntes de una cata histórica en Marqués de Riscal
    Camila rompe una de las tradiciones históricas de la monarquía: no tendrá damas de compañía 
    ‘Argentina, 1985’, un debate nacional entre la ficción y la memoria
    Madrid, la nueva Miami: así se han hecho con la capital española los ricos latinoamericanos
    Neofascistas, nacionalpopulistas, tecnosoberanistas. ¿Cómo llamamos a las nuevas derechas radicales? 
    Macondo Inundado: el pueblo donde nunca deja de llover 
    Qatar 2022, el único Mundial donde es posible ver dos partidos en un mismo día
    ¿Qué estrella tuvo el mejor debut en el Mundial? El ‘tier list’ de Jesús Gallego, Bruno Alemany y Aritz Gabilondo
    Enredados en el Mundial | Los jugadores iraníes vuelven a cantar el himno y ha nacido una estrella en EE UU
    Migrantes haitianos crean microeconomía en Tapachula
    Puerto Rico lucha por mantener sus playas públicas
    3 claves para entender las protestas por el censo en Bolivia
    Protests spread across China as anger builds over Xi Jinping’s zero-Covid policy 
    Tracing Columbus’s DNA: Two exhumations in Spain seek to determine the explorer’s lineage once and for all
    Europe says goodbye to ‘airplane mode’: Passengers can talk on the phone while flying
    Parasite makes wolves bolder, more likely to become pack leaders
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    Toda la actualidad científica en el boletín de Materia
    Letras Americanas: la actualidad literaria de un continente vista por el escritor Emiliano Monge
    Ideas: reportajes y entrevistas para entender el mundo
    El Kremlin silencia el dolor de las mujeres rusas que critican la guerra de Ucrania 
    El primer ministro de Rumania: “Necesitamos un esfuerzo común en la OTAN para defender cada centímetro de territorio frente a Rusia”  
    La justicia investiga si el Gobierno de Macron favoreció a consultoras privadas en las dos últimas campañas presidenciales en Francia
    Aquí puede buscar si ha sido engañado por la estafa internacional de las criptomonedas
    El secreto de la pirámide
    El futuro de las compras: más redes sociales, pago a plazos y vuelta de la tienda física
     El Papa detecta fallos en Caritas Internationalis y cesa a sus responsables 
    La Iglesia italiana da por primera vez cifras de los abusos cometidos por el clero
    El Senado de EE UU da un paso clave para blindar el matrimonio homosexual frente al Supremo
    Muere Hans Magnus Enzensberger, gran intelectual alemán del siglo XX
    ‘Close’, una mirada conmovedora a la fragilidad de la preadolescencia
    La gran retrospectiva de Vermeer en Ámsterdam aviva la polémica sobre la autoría de ‘Muchacha con flauta’
    “Houston, tenemos un nuevo récord”: ‘Orion’ llega más lejos que ninguna otra nave diseñada para llevar astronautas
    Joseph Henrich, antropólogo evolutivo: “El mejor antídoto contra el supremacismo blanco es más ciencia y discutir ideas”
    Infarto, cáncer, alzhéimer… Así aumenta la mala salud de sus encías el riesgo de sufrir otras enfermedades
    La Juventus cierra por sorpresa una era con un cambio de su cúpula en medio de investigaciones judiciales
    Dimite Mattia Binotto, director de Ferrari
    James Rhodes: “Me pilló fuera de juego meterme en política”
    Operación ‘OS35’: cómo rescatar un gigante de 40.288 toneladas varado a la sombra de Gibraltar
    ¿Podré matar a una rata que entre en mi casa? Claves de la reforma del Código Penal para castigar más el maltrato animal
    La izquierda retira por sorpresa y a última hora la propuesta para abolir los toros en Francia 
    La mitad de las mujeres programadoras ha renunciado a un puesto por no haber recibido apoyo 
    Damian Burns, director de Twitch Europa: “No me importaría que mi hija fuera ‘streamer’”
    Los ciberdelincuentes aprovechan el caos en Twitter para lanzar campañas de ‘phishing’
    El Supremo avala reducir las penas cuando lo permita la ‘ley del solo sí es sí’, pero insta a analizar cada a caso
    Unidas Podemos advierte con “preocupación” que el PSOE bloquea leyes sociales por cálculos políticos
    La división entre Arrimadas y Bal se agudiza: el diputado abre la puerta a concurrir a las primarias de Ciudadanos
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    ‘No me gusta conducir’: en qué se parece hacer una serie a aprender a conducir’, por Paloma Rando
    ‘The Peripheral’, realidad, ficción y un futuro ciberpunk con los creadores de ‘Westworld’
    Windsor desvela su decoración navideña en las primeras festividades sin Isabel II y con Carlos III como rey
    Camila y los 1.000 osos Paddington: la reina entrega a una ONG infantil los peluches en homenaje a Isabel II
    Stallone vs. Schwarzenegger, la “competición” eterna: “Éramos antagonistas. Soñaba con pegarle y él con pegarme a mí”
    Muchos hombres, una sola mujer
    El misterio de Manuel Carrasco: cómo salir de una barriada de pescadores y acabar siendo un cantante que llena estadios
    Neofascistas, nacionalpopulistas, tecnosoberanistas. ¿Cómo llamamos a las nuevas derechas radicales? 
    Marina Otero, la bailarina argentina que lleva al límite el cuerpo y la provocación
    Madrid, la nueva Miami: así se han hecho con la capital los ricos latinoamericanos
    Si no tiene ahorros, esta es una de las pocas alternativas para comprar casa
    Cuando la furia de Twitter empaña un (interesante) debate narrativo
    Las nuevas coordenadas culturales de Latinoamérica
    Abuelas empoderadas para sobrevivir en los países jóvenes del sur 
    Al-Hol: la prisión al aire libre a la que nadie quiere mirar
    Oyambre, Son Bou y otras nueve playas españolas para un baño de historia
    Cómo actuar ante el caos de los aeropuertos: qué hacer frente a retrasos y cancelaciones de un vuelo
    La bestial tensión sexual entre Bruce Willis y Cybill Shepherd en ‘Luz de luna’, la serie en la que la actriz tuvo mucho que decir
    Samantha Hudson: “Me va bien económicamante, pero no soy Paula Echevarría”
    Una Heidi matanazis y un Winnie the Pooh asesino en serie: ¿por qué los clásicos infantiles se han vuelto ultraviolentos?
    “Tu canción es una basura”: así juzgamos la música por motivos que nada tienen que ver con la calidad 
    Para qué sirve cada tipo de cebolla (y un truco para no llorar al picarla)
    Pollo asado con pomelo y dátiles
    Blackstone pone a prueba al mercado con la venta de viviendas de alquiler de Testa
    Los satélites de Vox: cómo la ultraderecha utiliza una red de asociaciones para aparentar apoyo social a sus postulados
    Suárez lllana anuncia que deja su escaño y Oskar Matute no defrauda con su reacción
    Un nuevo lesionado en Brasil
    Lobos de Ámsterdam. Booking.com, el monopolio de la última habitación
    Así era el final original (y emotivo) de The Walking Dead que se rodó y se cambió a última hora
    

Ahora vamos a hacer un segundo pedido a otra página de El País, la sección internacional.


```python
req2 = requests.get("https://elpais.com/internacional")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup2 = BeautifulSoup(req2.text, 'html.parser')
```

Ahora le pido todos los "h2".


```python
tags = soup2.findAll("h2")
```

Ahora le pedimos que los imprima.


```python
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    La doble respuesta de China a las protestas: acelerar la vacunación de los mayores y descabezar las manifestaciones 
    La OTAN redobla su alerta sobre una China en ebullición
    Hojas en blanco contra el cerrojo de la política de cero covid en China
    “¿De qué color es el hambre, mamá?”
    China: una protesta nacional
    Publicar no es un delito
    La vida bajo los bombardeos rusos
    Democracias a la defensiva
    El relator de la ONU para los derechos de los migrantes: “Es lamentable que no se haya aclarado la tragedia de Melilla cinco meses después”
    Rusia culpa a EE UU de la cancelación del encuentro bilateral sobre control de armas nucleares
    Rishi Sunak anuncia el fin de la “era dorada” en la relación con China
    Los medios reclaman el fin del abuso del sistema judicial del Reino Unido por parte de los oligarcas rusos
    La alta abstención marca un nuevo escenario político en Cuba    
    La granja de los horrores de Ucrania: 2.000 vacas muertas y un reguero de minas que explican la devastación de la agricultura en el país
    Rusia cancela el primer encuentro previsto con EE UU desde el inicio de la guerra de Ucrania 
    China responde a las protestas con un fuerte despliegue de seguridad en Pekín y Shanghái
    Hartazgo, estragos económicos y accidentes mortales: claves para entender las protestas en China
    Las protestas se extienden en China contra la política de covid cero
    La OTAN acusa a Putin de usar el invierno como arma de guerra contra Ucrania
    Estados Unidos prepara una ley para evitar una huelga de ferrocarriles en vísperas de Navidad
    “¿De qué color es el hambre, mamá?”
    Venezuela anuncia un crecimiento económico de 18 puntos del PIB para 2022
    Una banda secuestra durante horas un hospital de Ecuador
    Ideas neonazis y víctima de acoso: así es el joven que asesinó a cuatro personas en dos colegios de Brasil  
    

Ahora hacemos el ejercicio con la página de opinión, igual mirando que no haya error y solicitando los "h2".


```python
req3 = requests.get("https://elpais.com/opinion")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup3 = BeautifulSoup(req3.text, 'html.parser')

```


```python
tags = soup3.findAll("h2")

```

Ya pedimos los títulos h2, ahora le pedimos que los imprima.


```python
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Síntomas de rebeldía en China
    Las familias también cambian
    Millones de razones de cambio en China
    Ciclos conservadores
    ‘A compás’
    En tiempos de confusión
    La derecha y el Derecho
    Uno es la música que escucha 
    Enzensberger y la distancia crítica
    Sánchez al frente de la Internacional Socialista 
    La UE y la inmigración
    Delitos contra la Constitución: rebelión y sedición 
    Publicar no es un delito
    La tertuliana de ultraderecha y el bulo tránsfobo contra Begoña Gómez, la mujer de Pedro Sánchez
    Lengua migrante 
    El Roto
    Flavita Banana
    Riki Blanco
    Peridis
    Sciammarella
    Envía tu carta
    Mucho texto
    El desprestigio de la sanidad pública va calando
    Lucha feminista no solo en días mundiales
    Noticias positivas en tiempos caóticos
    Bomba nuclear en Barcelona
    Una maldita lista en tiempos airados
    El defensor del lector contesta
    

Ahora hacemos el pedido 4 con la sección España.


```python
req4 = requests.get("https://elpais.com/espana/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup4 = BeautifulSoup(req4.text, 'html.parser')
```

Pedimos que encuentre los "h2" y luego que los imprima.

tags = soup4.findAll("h2")



```python
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)    
```

    El Congreso rechaza la revisión de la ley del ‘solo sí es sí’
    El Constitucional acuerda apremiar al Poder Judicial para que nombre a sus dos magistrados
    Pedro Sánchez renueva el Tribunal Constitucional con el exministro de Justicia Juan Carlos Campo
    Alberto Núñez Feijóo, nacionalista
    La caverna
    Aunque nos tiemble la barbilla
    Orfandad representativa
    Otra forma de violencia política
    Documental | Tragedia en la frontera de Melilla: el papel de Marruecos y España en las muertes del 24-J
    El Supremo avala reducir las penas cuando lo permita la ‘ley del solo sí es sí’, pero insta a analizar cada a caso
    Interior insiste en que no hubo ningún muerto en suelo español en la tragedia de Melilla
    El Gobierno se defiende en medio de la tormenta: “El Constitucional no es un órgano judicial”
    La elección de Juan Carlos Campo para el Tribunal Constitucional, una vida entre el juzgado y la política
    La controversia de los nombramientos del Ejecutivo para el Constitucional puede llevar al choque de trenes entre instituciones
    Vox abandona el pleno del Congreso tras exigirle la Presidencia retirar una acusación de “filoetarras”
    Adolfo Suárez Illana abandona la política y renuncia a su acta de diputado del PP 
    Agonía a ambos lados de la frontera de Melilla
    Salvamento Marítimo rescata a tres polizones en Las Palmas que viajaron 11 días en el timón de un petrolero
    El PP agita un adelanto electoral en la Comunidad Valenciana 
    Hay casi 4.000 cervezas artesanas españolas. ¿Cómo probarlas todas?
    El cambio hacia un consumo sostenible empieza por los pies
    

Por último hacemos el mismo ejercicio con la sección economía.


```python
req5 = requests.get("https://elpais.com/economia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup5 = BeautifulSoup(req5.text, 'html.parser')
```

Pedimos que la libería "soup" encuentre todos los tags "h2" y que los imprima.


```python
tags = soup5.findAll("h2")

```


```python
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    La inflación se modera por cuarto mes consecutivo y se sitúa en el 6,8% en noviembre
    Los bancos reabren su convenio y pactan una subida salarial del 4,5% en 2023
    Una autopista para dejarse llevar
    Los agujeros legales de las finanzas sostenibles: así acaba el dinero de los fondos de inversión más verdes en empresas contaminantes
    La moda de la sostenibilidad
    Impuesto erróneo a la banca
    Sufrimientos evitables
    El coste de la vida
    La intermediación del ahorro y su evolución
    La inflación en Alemania se modera por primera vez desde julio y regresa al 10%
    El Banco de España prevé que la economía siga creciendo este trimestre
    Los bancos extranjeros pagarán unos 300 millones por el impuesto extraordinario al sector
    El 20% de los trabajadores cobra menos que el salario mínimo
    Hacienda gana contra ‘El Rubius’: la justicia dice que pagó menos impuestos de lo que debía 
    Primark invertirá 100 millones para crecer en España y crear 1.000 empleos en dos años
    La moda de la sostenibilidad
    La CNMV advierte de que las criptomonedas están “vacías de contenido y son ‘inútiles” como inversión
    El proyecto para reindustrializar Nissan sale adelante pero consigue solo la mitad de los avales
    EasyJet reduce un 80% sus pérdidas anuales tras el mejor verano de su historia
    Así quedarán las pensiones en 2023: las prestaciones máximas superarán los 3.000 euros brutos por primera vez
    Madrid, la nueva Miami: así se han hecho con la capital los ricos latinoamericanos
    Si no tiene ahorros, esta es una de las pocas alternativas para comprar casa
    Los efectos de una economía de andar por casa
    Caballos al galope: un negocio con un impacto económico de 7.400 millones de euros
    Los impuestos que se necesitan para construir la sociedad del futuro
    La CNMC congela las tarifas de Aena para 2023 ante las dudas sobre la evolución del tráfico
    Escrivá propone elevar a 30 años el periodo para calcular la pensión y descartar los dos peores ejercicios
    Tecnológicas, dólar y bonos tocan suelo tras un año en caída libre
    El método de Antonio Resines para afrontar cambios en las empresas
    Por primera vez un juez declara nulo un contrato de alquiler por aplicación de la perspectiva de género
    Visitas a centros de acogida y muchas horas de estudio: así se forman los jueces en materia de género
    La justicia obliga a Iberia a controlar el peso de las maletas para que los azafatos no se lesionen
    La difícil tarea de recuperar el talento investigador que un día hizo las maletas
    Descubre las formaciones de marketing ‘online’ más buscadas (y económicas) de 2023
    La quinta edición de EnlightED aborda los retos del aprendizaje y la educación en la era digital  
    Logística de ida y vuelta, cuando la solución está en reciclar menos y reutilizar más
    Logística y digitalización, el manual de supervivencia para pymes
    Empleados satisfechos, empresas de éxito
    Diez claves del bienestar corporativo para empresas de éxito
    Las aventuras de un par de calcetines que dan empleo a todo un pueblo
    Cultura financiera como punto de partida para volver a empezar
    Las soluciones digitales que necesita mi negocio 
    Las fórmulas de financiación más adecuadas para mi negocio
    Alexia Putellas, un Balón de Oro a base de “esfuerzo, constancia, disciplina y saber reinventarse”
    El método Muñoz para triunfar en cada reto que se propone
    ¿Por qué muchos inversores están volviendo a confiar en Japón?
    ¿Por qué se está enfriando la economía china?
    No una, sino cinco ‘startups’ para la esperanza
    Si tú lo imaginas, yo te lo imprimo
    Cómo garantizar la seguridad en un mundo de amenazas híbridas
    ¿Cuáles son los dilemas éticos del uso de la inteligencia artificial?
    La educación financiera se convierte en la llave de la inclusión
    Hacia un 2025 más justo, más conectado y más sostenible
    ‘La mirada del paciente’: historias sin filtro detrás de las personas
    Cómo conseguir ayudas a la digitalización para autónomos y pymes con Kit Digital
    Un brindis con vino español por la sostenibilidad, la economía y el empleo
    

Ahora, habiendo ejemplificado cómo se hace paso a paso, hacemos el requerimiento para todas las demás secciones.


```python
req6 = requests.get("https://elpais.com/sociedad/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup6 = BeautifulSoup(req6.text, 'html.parser')

tags = soup6.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req7 = requests.get("https://elpais.com/educacion/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup7 = BeautifulSoup(req7.text, 'html.parser')

tags = soup7.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req8 = requests.get("https://elpais.com/clima-y-medio-ambiente/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup8 = BeautifulSoup(req8.text, 'html.parser')

tags = soup8.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req9 = requests.get("https://elpais.com/ciencia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup9 = BeautifulSoup(req9.text, 'html.parser')

tags = soup9.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req10 = requests.get("https://elpais.com/cultura/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup10 = BeautifulSoup(req10.text, 'html.parser')

tags = soup10.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req11 = requests.get("https://elpais.com/babelia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup11 = BeautifulSoup(req11.text, 'html.parser')

tags = soup11.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req12 = requests.get("https://elpais.com/deportes/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup12 = BeautifulSoup(req12.text, 'html.parser')

tags = soup12.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req13 = requests.get("https://elpais.com/tecnologia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup13 = BeautifulSoup(req13.text, 'html.parser')

tags = soup13.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req14 = requests.get("https://elpais.com/tecnologia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup14 = BeautifulSoup(req14.text, 'html.parser')

tags = soup14.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req15 = requests.get("https://elpais.com/gente/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup15 = BeautifulSoup(req15.text, 'html.parser')

tags = soup15.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req16 = requests.get("https://elpais.com/television/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup16 = BeautifulSoup(req16.text, 'html.parser')

tags = soup16.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)

req17 = requests.get("https://elpais.com/eps/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup17 = BeautifulSoup(req17.text, 'html.parser')

tags = soup17.findAll("h2")

for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)


os.system("clear")

print(colored("A continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:", 'blue', attrs=['bold']))
print(colored("Feminismo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "feminismo" in s]
print("\n".join(str_match))

print(colored("Igualdad", 'green', attrs=['bold']))

str_match = [s for s in resultados if "igualdad" in s]
print("\n".join(str_match))

print(colored("Mujeres", 'green', attrs=['bold']))

str_match = [s for s in resultados if "mujeres" in s]
print("\n".join(str_match))

print(colored("Mujer", 'green', attrs=['bold']))

str_match = [s for s in resultados if "mujer" in s]
print("\n".join(str_match))

print(colored("Brecha salarial", 'green', attrs=['bold']))

str_match = [s for s in resultados if "brecha salarial" in s]
print("\n".join(str_match))

print(colored("Machismo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "machismo" in s]
print("\n".join(str_match))

print(colored("Violencia", 'green', attrs=['bold']))

str_match = [s for s in resultados if "violencia" in s]
print("\n".join(str_match))

print(colored("Maltrato", 'green', attrs=['bold']))

str_match = [s for s in resultados if "maltrato" in s]
print("\n".join(str_match))

print(colored("Homicidio", 'green', attrs=['bold']))

str_match = [s for s in resultados if "homicidio" in s]
print("\n".join(str_match))

print(colored("Género", 'green', attrs=['bold']))

str_match = [s for s in resultados if "género" in s]
print("\n".join(str_match))

print(colored("Asesinato", 'green', attrs=['bold']))

str_match = [s for s in resultados if "asesinato" in s]
print("\n".join(str_match))

print(colored("Sexo", 'green', attrs=['bold']))

str_match = [s for s in resultados if "sexo" in s]
print("\n".join(str_match))

```

    Pilar Bonet dedica a los periodistas que cubren la guerra de Ucrania el premio Francisco Cerecedo de periodismo 
    Vila-real concede la medalla de oro al colegio de los carmelitas dos meses después de destaparse un caso de abusos
    Cinco jóvenes procesados en Murcia por una agresión sexual en grupo que además grabaron y difundieron por redes sociales 
    La caja de resonancia de la angustia vital
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    Los secretos atronadores del secretario general
    Balance de la COP27: un fondo para los más vulnerables mientras la meta de los 1,5 grados se aleja
    La ley de trata garantizará la asistencia y protección de las víctimas sin necesidad de denuncia
    EE UU ordena retirar un innovador tratamiento contra el cáncer que España acaba de incorporar a la sanidad pública 
    Derechos Sociales culpa al ala socialista del Gobierno de “constantes retrasos” en la aprobación de la ley de familias
    La escuela concertada matricula a la mitad del alumnado desfavorecido que le correspondería
    Alex Rafalowicz, abogado: “Los combustibles fósiles son una amenaza existencial como las armas nucleares”
    Igualdad negocia a contra reloj con Interior y Justicia el texto de la ley de trata que irá mañana a Consejo de Ministros 
    La expulsión de una clase en un colegio de Palma tras colocar una bandera de España deriva en graves amenazas a una profesora 
    Los médicos privados se sienten “humillados” por las aseguradoras: los técnicos cobran 60 euros por arreglar una lavadora y los sanitarios, 10 por consulta
    Los ayuntamientos de Madrid se sitúan un año más a la cola en servicios sociales
    Kelley Robinson: “Han declarado una guerra cultural contra nuestros hijos”
    La caja de resonancia de la angustia vital
    Unas gafas que cambian la forma de ver el mundo
    Cambia tu relación con los papeles de la cocina
    Social, clínica y en primera persona. Tres visiones del VIH 
    Enfermería, los profesionales de las ‘curas invisibles’ en las personas con VIH
    Sostenibilidad y... ¡acción! 
    La huella de carbono, el rastro que marca el futuro del planeta
    Psoriasis, en las profundidades de la piel
    Contar para sanar
    La nueva revolución agrícola 
    Nuevos talentos de la economía circular
    Lo lejos que se puede llegar con otra metodología educativa 
    Cuando el empleo se convierte en la mejor terapia 
    A solas con la obesidad
    Freno y marcha atrás en la obesidad infantil
    “La ópera, como la naturaleza, está viva, y debe evolucionar para ser eterna” 
    ¿Hasta dónde puede llegar el ser humano? El viaje a la oscuridad más absoluta
    Acuicultura: la importancia de comer ‘azul’ para vivir en verde
    El cultivo de pescado español, a la vanguardia del planeta
    El futuro de la aviación verde
    En busca de la eficiencia energética en los aeropuertos
    Un día en el servicio de ayuda a domicilio
    Trabajadores esenciales. Los que nunca paran
    Consejos para alimentar correctamente a los animales de compañía
    Cuidados y necesidades de perros y gatos en su etapa sénior
    Combatir el desperdicio alimentario desde la cesta de la compra
    Kilómetro cero para llenar la despensa
    Acompañamiento, el modelo alternativo de acogida de refugiados
    El metro como refugio. De los andenes de Madrid en 1936 a los de Kiev en 2022
    Yogures con menos azúcar, paso firme hacia la alimentación infantil del futuro
    Invisible, pero vital: el ciclo de las aguas subterráneas
    La bomba de calor, el sistema de climatización más sostenible y eficiente
    La escuela concertada matricula a la mitad del alumnado desfavorecido que le correspondería
    El Gobierno dará un subsidio de 400 euros anuales a los alumnos con necesidades especiales
    La expulsión de una clase en un colegio de Palma tras colocar una bandera de España deriva en graves amenazas a una profesora 
    Pobreza en el Olimpo académico de EE UU: la huelga en la Universidad de California es ya una de las más grandes del país
    El primer Mundial en horario lectivo y con ‘smartphones’ se juega también en los institutos
    El cabecilla de los cánticos machistas del Elías Ahuja vuelve al colegio mayor pese a anunciarse su expulsión definitiva
    La nueva ley de enseñanzas artísticas endurecerá los requisitos para ser profesor y hará más homogéneas las pruebas de acceso del alumnado
    Una madre denuncia insultos homófobos a su hija en un colegio de Madrid: “Su tutor nos dijo que tenemos que respetar la opinión de los demás”
    Cataluña aprueba un complemento para ampliar la jornada a los profesores de informática de FP
    Más de 6.000 estudiantes de FP empezaron tarde el curso por el largo proceso de inscripción en Cataluña
    Cuando la escuela se convierte en un gueto: América Latina tiene las primarias más segregadas del mundo
    Evaluar competencias
    La Selectividad a los 50: ¿cirugía mayor o estiramiento facial?
    La libertad de elección de centro educativo y los cheques escolares en Madrid
    Selectividad: Desatar el nudo gordiano
    El nuevo sistema para evaluar los conocimientos digitales de los profesores valdrá en toda España
    Ofrecer comedor gratis en todos los colegios públicos es “alcanzable y urgente”: costaría 1.664 millones al año, según la ONG Educo  
    Una fórmula para que la escuela pública compita mejor con la concertada
    La pérdida de alumnos por el descenso de la natalidad está afectando con más fuerza a la escuela pública que a la concertada
    La disparidad de resultados entre autonomías en la EVAU se origina en la escuela, no en el examen 
    Las autonomías del PP critican la nueva Selectividad porque no prevé un examen único para todo el Estado
    La escalada vertiginosa de notas en Bachillerato: los sobresalientes de los que llegan a Selectividad se doblan en seis años
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    El techo de cristal del grado medio de FP: candidatos demasiado preparados se quedan con los puestos
    César Rendueles: “Hay universidades privadas que son como academias de conducir con pretensiones”
    La fuga de miles de médicos agrava el déficit de especialistas en España
    Jóvenes tutelados en la Universidad: “Tu pasado no tiene por qué condicionar tu futuro”
    Si tu familia está desahogada estudiarás Medicina y dobles grados, si no, Óptica o Educación 
    Pon nombre a lo que te pasa para sentirte mejor
    Volver a empezar
    Borges, 'Funes el memorioso' y la neurona Jennifer Aniston
    Alex Rafalowicz, abogado: “Los combustibles fósiles son una amenaza existencial como las armas nucleares”
    Los agujeros legales de las finanzas sostenibles: así acaba el dinero de los fondos de inversión más verdes en empresas contaminantes
    Gobierno y Junta chocan por Doñana mientras se agrava el deterioro ecológico 
    Linces y águilas imperiales se refugian en fincas privadas que se alían con conservacionistas  
    ¿Podré matar a una rata que entre en mi casa? Claves de la reforma del Código Penal para castigar más el maltrato animal
    El precio del Ave Madrid-Barcelona cae un 43% pero sube un 14% en las líneas sin competencia 
    El plan del Gobierno para las reservas de agua mantiene intacta la alta presión del regadío
    Operación ‘OS35’: cómo rescatar un gigante de 40.288 toneladas varado a la sombra de Gibraltar
    Balance de la COP27: un fondo para los más vulnerables mientras la meta de los 1,5 grados se aleja
    Clemente Álvarez, premio a la conservación de la biodiversidad de la Fundación BBVA: “Debemos difundir la voz de alarma de los científicos”
    Investigan la brutalidad en una montería en la Sierra de Segura de Jaén 
    El cambio climático perjudica su salud
    Por qué comer animales puede ayudar a luchar contra el cambio climático
    Por qué hay que dejar de comer animales para luchar contra el cambio climático
    Bombas de carbono 
    Crisis de los insectos: esto no es un armagedón sino una debacle provocada por los humanos
    El quebrantahuesos reconquista los cielos 
    Un año de crisis climática sin fin
    Ríos imposibles: las 171.000 barreras que rompen el curso de agua en España
    Pon nombre a lo que te pasa para sentirte mejor
    Volver a empezar
    Borges, 'Funes el memorioso' y la neurona Jennifer Aniston
    Los hogares más pobres reducen su consumo de refrescos casi 11 litros en un año por la subida del IVA
    Por qué unas personas resisten el estrés mejor que otras 
    Joseph Henrich, antropólogo evolutivo: “El mejor antídoto contra el supremacismo blanco es más ciencia y discutir ideas”
    “Houston, tenemos un nuevo récord”: ‘Orion’ llega más lejos que ninguna otra nave diseñada para llevar astronautas
    En busca de una solución para los dolores que se creían inventados
    Un parásito ‘elige’ qué lobo será el líder de la manada
    Pobreza en el Olimpo académico de EE UU: la huelga en la Universidad de California es ya una de las más grandes del país
    Josefa Ros Velasco, filósofa: “Si alguien se aburre suele darse a la botella, cuando le pasa a un país suele darse una revuelta”
    La insólita historia de la mujer que descubrió el primer antibiótico español
    Hilda Hudson, la primera conferenciante en el gran congreso internacional de matemáticas
    De León al espacio, pasando por una pequeña universidad pública: “Invirtiendo en ciencia se puede llegar a lo más alto”
    “Soñamos con ir a la Luna, pero no llegaremos a Marte” 
    Pablo Álvarez y Sara García, primeros astronautas españoles de la ESA en 30 años
    Una vacuna universal contra la gripe que usa la tecnología de ARN, probada con éxito en ratones
    Palabras y árboles
    Europa resucita su misión para taladrar Marte en busca de vida en 2028  
    ¿Cómo nos afecta en la Tierra la formación de un agujero negro?: tres grandes físicos lo desvelan
    Hilda Hudson, la primera conferenciante en el gran congreso internacional de matemáticas
    Por qué el entrelazamiento cuántico revoluciona nuestro entendimiento de la naturaleza
    La órbita del telescopio ‘James Webb’ y el problema de los tres cuerpos
    Cien años de las ecuaciones que expandieron el universo
    Sangaku
    El tamiz de Apolonio
    La respuesta a la gran pregunta
    El aroma de la inspiración y la piedra de la locura
    ‘Los hijos de Hansen’ y la marginación social provocada por la lepra
    Los fractales y su estructura narrativa como parte del relato
    El amanecer de todo y el dinosaurio como animal modernista
    Los universos paralelos de un visionario científico llamado Philip K. Dick
    ¿Por qué son rocosos los satélites de los planetas gaseosos?
    ¿Es nueva la producción de alimentos en macrogranjas? 
    ¿Cómo se ve el cielo nocturno desde el ecuador?
    ¿Por qué las olas van siempre hacia la playa?
    Listeria: el patógeno que trae de cabeza a la industria alimentaria
    Ciencia para derrumbar el mito de que la soja es mala para prevenir el cáncer de mama
    Cuidado con las conservas caseras: es importante hacerlas bien
    Una propuesta alternativa, barata y saludable a la nueva cesta de la compra
    Aditivos, propiedades saludables y fechas de caducidad: guía para entender las etiquetas alimentarias
    Almodóvar, en la lectura de la obra de Paco Bezerra: “Nunca imaginé que iba a asistir hoy a un acto contra la censura”
    ¿Especulación, algoritmos locos o codicia? El misterio de los libros de segunda mano con precios desorbitados
    ‘Canina’: la maternidad con pelo y colmillos
    ¿Cómo empezó?
    ‘Company’ y el olor de la gran manzana
    Charlie Watts: el bicho más raro de The Rolling Stones
    Meter la mano en la vaca 
    Bono se desnuda emocionalmente en Madrid en su concierto más atípico
    Cartel de Primavera Sound 2023, tanto Barcelona como Madrid: Rosalía, Kendrick Lamar, Blur o Depeche Mode
    Rolling Blackouts Coastal Fever, la banda de rock más chisporroteante y luminosa de Australia
    ¿Cómo empezó?
    Viviendas de lujo sostenible
    Así era el rostro de san Isidro Labrador, muerto hace diez siglos   
    La encrucijada del Reina Sofía: ¿quién sucederá a Borja-Villel en la dirección de uno de los museos más importantes del mundo?
    La cultura abraza las historias trans 
    Momias a dos velas: la excavación estrella de la egiptología española afronta una crítica falta de fondos en su momento más decisivo
    El monasterio burgalés que falsificó en el siglo XII una herencia para quedarse con una valiosa iglesia
    La FIL pone una vela al libro y otra al balón
    Videoanálisis | La FIL mastodóntica y popular está de vuelta
    Carmen Machi: “Que te metieran mano en el metro nos parecía normal”
    Santo Estevo, el monasterio al que todos le tienen fe
    La Calahorra de siempre, más viva que nunca
    La novela negra del siglo XXI no existe (sin Michael Connelly)
    'Company, el Musical' llega a Madrid
    Disfruta de 'El Cascanueces' en Cine Yelmo
    Fernando Cayo es Scrooge en 'Cuento de Navidad'
    'El Guardaespaldas, el musical' llega a tu ciudad
    La temida voltereta de la abolición de los toros en el sur de Francia quedó en un susto
    Las obras de mejora de la plaza de toros de Las Ventas comienzan en diciembre
    Actos a favor y en contra de los toros en Francia antes de que se debata su prohibición
    Luis Miguel Leiro, picador premiado y desencantado: “Amo y respeto a los animales, pero el toro ha nacido para la lidia”
    La lección magistral de Bob Dylan sobre Elvis
    Cuando la furia de Twitter empaña un (interesante) debate narrativo
    La curva de la semana: sube Cristina Morales, está aquí Aldo Manucio, baja Rosalía
    Las nuevas coordenadas culturales de Latinoamérica
    Las más bellas cartas de amor en castellano, las memorias de Marguerite Duras y otros libros de la semana
    Amor mío queridísimo: la delicadeza sentimental de Felisberto Hernández
    Ellas fueron modernas: cuatro artistas alemanas en la vorágine del cambio de siglo
    Anacrónicas y audaces: las cantautoras latinas que renuevan la música de raíz
    Los mejores libros infantiles y juveniles de noviembre
    Palabra de Kafka
    Una ‘Yerma’ con poco nervio y zozobra
    Lo que jode es la respuesta: la diferencia entre crítica, cancelación y censura
    Edmonia, Frida y Amrita: tres mestizas
    La basura se lee con anteojos
    Mi otoño alemán
    ‘Percusión’: una novela del pasado para recordar el futuro
    Pere Gimferrer dentro del laberinto
    ‘La brecha’: cómo cambiar un mundo mal hecho
    ‘Tu sueño imperios han sido’: la historia boca arriba
    Nona Fernández: “En Chile intentan que conciliemos el sueño otra vez”
    Cristina Lucas: “Todo lo que se publicita está sobrevalorado”
    Enrique Gracián: “Hay infinitos más grandes que otros”
    Àlex Brendemühl: “La serie sobre el rey emérito no te deja indiferente”
    Marta Etura: “De no ser actriz, habría sido matrona”
    Última hora
    El calendario
    Universo Mundial
    Las predicciones
    La ‘newsletter’
    El imperio contraataca: EE UU derrota a Irán y se mete en octavos
    Inglaterra marca distancias
    Gareth Bale, lesionado y eliminado del Mundial: “Seguiré mientras pueda y me quieran” 
    Difícil separar la política del deporte
    Inglaterra - Gales, matar al hermano
    España eleva su crédito por derecho
    La elevación del delito
    Bélgica, bajo fuego amigo en el Mundial
    Senegal derrota a una reservona Ecuador y devuelve a África a los octavos de final de un Mundial
    Qatar se despide del Mundial con tres derrotas, la peor anfitriona de la historia
    Qatar reconoce la muerte de al menos 400 trabajadores migrantes en la preparación del Mundial
    Resumen de la jornada 10 del Mundial de Qatar 2022 
    Todos los ofendidos de Irán, contra EE UU 
    La fascinante vida del último buscador de perlas de Qatar  
    Dimite Mattia Binotto, director de Ferrari
    James Rhodes: “Me pilló fuera de juego meterme en política”
    Gareth Bale, lesionado y eliminado del Mundial: “Seguiré mientras pueda y me quieran” 
    Bruno Fernandes somete a Uruguay 
    Gareth Bale, lesionado y eliminado del Mundial: “Seguiré mientras pueda y me quieran” 
    Bruno Fernandes somete a Uruguay 
    Los aficionados opinan sobre el Mundial de Qatar: de “Se celebra en un lugar triste” a “La culpa no es del fútbol” 
    Última hora del Mundial de Qatar: vídeo en directo | Fútbol Sapiens
    Día 10 de Qatar 2022 | Iturralde analiza el no gol de Cristiano Ronaldo
    La moneda que cambió para siempre el destino de España en los Mundiales
    Cómo no perderte ni un solo minuto del Mundial
    Las promesas del baloncesto español piden consejo a Sergio Scariolo
    A toda mecha hacia el mundial de la consagración
    Cómo disfrutar de la montaña con todas las garantías
    Así hemos contado la victoria de Brasil ante Suiza en la segunda jornada de la fase de grupos del Mundial de Qatar 2022
    Enredados en el Mundial: Füllkrug, el nuevo héroe de Alemania
    Rubiales, sobre el futuro de Luis Enrique: “Nunca podremos pagarle 20 millones de euros. Hablaremos tras el Mundial, pero no se puede dilatar”
    ¿Quién de España jugó mejor contra Alemania? El ‘tier list’ de Jesús Gallego, Antón Meana y Joaquín Maroto
    ¿Quién va a ganar el Mundial de Qatar? Simulador y pronóstico actualizado de cada selección 
    Difícil separar la política del deporte
    El ‘Chucky’ Lozano, Alexis Vega y las cadenas del gol en México
    Dimite Mattia Binotto, director de Ferrari
    El problema de la cultura ‘brogrammer’: “Se está excluyendo la mirada femenina de las soluciones tecnológicas que van a modelar el futuro”
    Los ciberdelincuentes aprovechan el caos en Twitter para lanzar campañas de ‘phishing’
    Damian Burns, director de Twitch Europa: “No me importaría que mi hija fuera ‘streamer’”
    Adrian Hon, diseñador de videojuegos: “Las empresas y gobiernos usan juegos para controlarnos”
    Mastodon: qué es y cómo funciona la red social en la que los usuarios deciden qué está permitido
    Así serán las nuevas marcas de verificación en Twitter: azul, oro y gris
    Gafas con funciones de un móvil, ‘Photoshop’ instantáneo y otros inminentes avances gracias a los nuevos chips
    Elon Musk ya edita tuits y Twitter no se ha hundido aún, ¿qué hará en el futuro?
    Elon Musk declara una “amnistía general” en Twitter para las cuentas suspendidas
    Así está fallando Twitter: racismo, derechos de autor y desprotección en dictaduras
    Quo Vadis, Elon Musk: por qué el colapso de Twitter no es un divertimento
    Candid Wüest: “Si alguien ‘apaga’ Ucrania, probablemente haya una respuesta y eso no interesa porque todos los países son vulnerables”
    El reclutamiento de personal se reinventa en las redes: “Se crea una relación de confianza entre los candidatos y las empresas mucho antes de haber contacto directo”
    El biógrafo de Elon Musk: “Para él, el caos es el procedimiento operativo estándar”
    Aplicaciones, relojes y etiquetas QR ayudan a evitar la desaparición de personas con demencia
    La banca confía en tumbar en los tribunales el nuevo impuesto al sector
    Los cuatro coches que llegaron a España en el año de los Juegos y la Expo
    Ocho mil millones de cursis
    Guía de viaje a la nube: una aventura con escalas
    Árboles tuiteros contra la ceguera botánica
    De Baudelaire a Midjourney: los nuevos “enemigos mortales del arte”
    El problema de la cultura ‘brogrammer’: “Se está excluyendo la mirada femenina de las soluciones tecnológicas que van a modelar el futuro”
    Los ciberdelincuentes aprovechan el caos en Twitter para lanzar campañas de ‘phishing’
    Damian Burns, director de Twitch Europa: “No me importaría que mi hija fuera ‘streamer’”
    Adrian Hon, diseñador de videojuegos: “Las empresas y gobiernos usan juegos para controlarnos”
    Mastodon: qué es y cómo funciona la red social en la que los usuarios deciden qué está permitido
    Así serán las nuevas marcas de verificación en Twitter: azul, oro y gris
    Gafas con funciones de un móvil, ‘Photoshop’ instantáneo y otros inminentes avances gracias a los nuevos chips
    Elon Musk ya edita tuits y Twitter no se ha hundido aún, ¿qué hará en el futuro?
    Elon Musk declara una “amnistía general” en Twitter para las cuentas suspendidas
    Así está fallando Twitter: racismo, derechos de autor y desprotección en dictaduras
    Quo Vadis, Elon Musk: por qué el colapso de Twitter no es un divertimento
    Candid Wüest: “Si alguien ‘apaga’ Ucrania, probablemente haya una respuesta y eso no interesa porque todos los países son vulnerables”
    El reclutamiento de personal se reinventa en las redes: “Se crea una relación de confianza entre los candidatos y las empresas mucho antes de haber contacto directo”
    El biógrafo de Elon Musk: “Para él, el caos es el procedimiento operativo estándar”
    Aplicaciones, relojes y etiquetas QR ayudan a evitar la desaparición de personas con demencia
    La banca confía en tumbar en los tribunales el nuevo impuesto al sector
    Los cuatro coches que llegaron a España en el año de los Juegos y la Expo
    Ocho mil millones de cursis
    Guía de viaje a la nube: una aventura con escalas
    Árboles tuiteros contra la ceguera botánica
    De Baudelaire a Midjourney: los nuevos “enemigos mortales del arte”
    Xuso Jones: “Tengo muchos más seguidores por mis ‘tips’ de limpieza que por mi música. Y me encanta”
    Sara Carbonero, tras recibir el alta hospitalaria por su operación: “Me siento en paz y agradecida con la vida”
    La jueza archiva la denuncia de María León contra los policías que la detuvieron en Sevilla
    Jennifer Lopez pensó que “iba a morir”después de su ruptura con Ben Affleck
    Por qué encontrar pareja parece hoy misión imposible
    Dwayne Johnson vuelve a la tienda donde robó chocolatinas de niño y se gasta 300 dólares 
    Camila rompe una de las tradiciones históricas de la monarquía: no tendrá damas de compañía 
    Helena Bonham Carter defiende a su amigo Johnny Depp y critica la cultura de la cancelación: “Hay una caza de brujas”
    El silencio es el nuevo lujo: cómo vivir en un mundo cada vez más ruidoso nos ha hecho pagar por algo gratuito
    Confesiones de la mujer que lleva 40 años decidiendo quién será James Bond
    Atún rojo: el inesperado nexo cultural que une a Japón con el Mediterráneo
    Las excentricidades imposibles de las Kardashian: de escáneres cerebrales a 700 dólares en gominolas de cannabis
    Mis séptimos Premios Icon
    Achilles Ion Gabriel, el surrealista de Camper: “No hago zapatos para museos, sino para la gente” 
    El regreso discreto de Mario Testino: “A mi edad, no creo que mi percepción de la moda sea la correcta ni la que el mundo necesita”
    Manuel Outumuro toca cumbre
    Diane de Beauvau-Craon, la última princesa rebelde: “Me drogué mucho, bebí mucho alcohol, me acosté con muchos gais y aquí sigo”
    Marta Ortega reúne en A Coruña a grandes protagonistas de la moda internacional en la inauguración de la muestra sobre Steven Meisel
    En los secaderos ancestrales del pimentón de la Vera, el oro rojo de Cáceres
    Las abuelas que han viralizado el arte de elaborar la pasta italiana 
    Humaredas mediáticas, monotonía, discursos vacíos y otras amenazas y retos de la gastronomía 
    Sumer, el ‘kebab’ artesano de barrio en Madrid que acoge tertulias filosóficas
    El robot de cocina más famoso del mundo ha conquistado ya tres millones de hogares españoles
    Lorena Castell, ganadora de ‘MasterChef Celebrity 7’
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    Eliseo, ‘el encargado’ corrupto que seduce y repele en Argentina 
    ‘No me gusta conducir’: en qué se parece hacer una serie a aprender a conducir
    ‘Ummo’, un guirigay intergaláctico
    Adiós a Ellen Pompeo, la funcionaria de la tele
    ‘This England’
    ‘Masterchef Celebrity’ ya tiene a sus dos finalistas, tras la “rendición” de Patricia Conde
    ‘The Peripheral’, realidad, ficción y un futuro ciberpunk con los creadores de ‘Westworld’
    El ‘bon vivant’ acorralado de la FIFA que grabó a sus amigos
    Leonor Lavado: “Somos como hablamos: la voz es nuestro ADN psicológico”
    ¿Qué ocurre tras la edad de oro de la televisión? El mismo oro, aunque enterrado bajo una oferta masiva
    ‘La ruta’: por qué nos invade la nostalgia del ‘after’
    La veteranía de María del Monte y Francisco se mide con la juventud de María Terremoto y Juanlu Montoya en los premios Radiolé  
    La violencia machista entre los adolescentes, el drama que ni ellos quieren reconocer
    ‘La Sagrada Familia’ rescata el mito Pujol y disecciona su caída
    Eurovisión permitirá votos de espectadores de todo el mundo a partir de 2023
    ¿Qué ver hoy en TV? Martes 29 de noviembre de 2022
    Las series de agosto de 2022: ‘La casa del dragón’ en HBO Max; ‘Sandman’ en Netflix y otras
    Nueve capítulos para recordar ‘The Wire’ en su 20º aniversario
    Harry Palmer: el tercer vértice del mágico triángulo de espías británicos
    Las series de junio de 2022: ‘The Boys’ en Amazon Prime Video; ‘Peaky Blinders’ en Netflix y otras
    ¿A qué sabe un vino de 160 años? Apuntes de una cata histórica en Marqués de Riscal
    Las abuelas que han viralizado el arte de elaborar la pasta italiana 
    David LaChapelle, en busca de Dios
    Muchos hombres, una sola mujer
    El misterio de Manuel Carrasco: cómo salir de una barriada de pescadores y acabar siendo un cantante que llena estadios
    Ishida, los ‘dioses’ de la cocina japonesa: “Tenemos que dejar de desear tantas cosas, y hay que hacerlo ya”  
    Los guardianes de la ensaladilla rusa, la tapa popular que subió a los altares ‘gourmet’ 
    Humaredas mediáticas, monotonía, discursos vacíos y otras amenazas y retos de la gastronomía 
    Cerdo pío negro, el inesperado rival del ibérico
    Narcisistas, ansiosos, pasivo-agresivos… Cinco claves para tratar con personas difíciles
    Al fondo, invisibles, las pirámides
    Todo es mejor con chocolate y estas cinco recetas lo demuestran
    Sangre, sudor y petróleo: la materia prima del Mundial de Qatar según un artista ruso
    Los Audi RS 6 Avant y RS 7 más potentes de la historia
    El milagro alemán
    Consuelo
    Sin tiempo
    La bióloga que se propuso repoblar los bosques de Brasil
    Un parche para conseguir que las vacunas sean más baratas y accesibles
    Cerdo pío negro, el inesperado rival del ibérico
    Ishida, los ‘dioses’ de la cocina japonesa: “Tenemos que dejar de desear tantas cosas, y hay que hacerlo ya”  
    El secreto del maíz gigante mexicano que bajó del volcán
    ‘Mis primeros recuerdos’, por Daniel Barenboim
    El indómito espíritu creativo de Picasso
    Medio siglo sin Picasso
    Paloma Picasso se confiesa con Nuccio Ordine
    El amigo de Picasso sin el que no estaría en España el ‘Guernica’
    Tommy Hilfiger: “Muchos de nuestros clientes van a vivir en el metaverso. De hecho, ya lo hacen”
    Storm Pablo: el estilista que convirtió a Bad Bunny en icono también de la moda
    El hombre que cultiva las flores más caras para los perfumes más especiales
    Una casa junto al lago Como que es pura diversión 
    Desayuno a la mexicana entre hípsters de mañaneo y polis con más apetito que buena fama
    El misterio Picasso
    Isabel II: el reinado de la imagen
    Un día en la vida de un país: San Sebastián-Cádiz en 16 horas
    Luces y sombras de Robert Mapplethorpe
    A continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:
    Feminismo
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    Igualdad
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    Mujeres
    El Kremlin silencia el dolor de las mujeres rusas que critican la guerra de Ucrania 
    La mitad de las mujeres programadoras ha renunciado a un puesto por no haber recibido apoyo 
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    Mujer
    El Kremlin silencia el dolor de las mujeres rusas que critican la guerra de Ucrania 
    La mitad de las mujeres programadoras ha renunciado a un puesto por no haber recibido apoyo 
    Muchos hombres, una sola mujer
    La tertuliana de ultraderecha y el bulo tránsfobo contra Begoña Gómez, la mujer de Pedro Sánchez
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    La insólita historia de la mujer que descubrió el primer antibiótico español
    Confesiones de la mujer que lleva 40 años decidiendo quién será James Bond
    Muchos hombres, una sola mujer
    Brecha salarial
    
    Machismo
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    Violencia
    Otra forma de violencia política
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    La violencia machista entre los adolescentes, el drama que ni ellos quieren reconocer
    Maltrato
    ¿Podré matar a una rata que entre en mi casa? Claves de la reforma del Código Penal para castigar más el maltrato animal
    ¿Podré matar a una rata que entre en mi casa? Claves de la reforma del Código Penal para castigar más el maltrato animal
    Homicidio
    
    Género
    Americanas: Reportajes y noticias sobre feminismo e historias con enfoque de género de la región
    Por primera vez un juez declara nulo un contrato de alquiler por aplicación de la perspectiva de género
    Visitas a centros de acogida y muchas horas de estudio: así se forman los jueces en materia de género
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    Asesinato
    
    Sexo
    
    


```python

```
