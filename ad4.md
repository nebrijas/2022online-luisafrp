## ad4
## Luisa Fernanda Restrepo
## Uso de la api covid con pandas
En esta práctica y la ad4 vamos a utilizar "pandas" una libreria para trabajar sobre los datos de covid19 y analizarlos desde la una api con información cuya URL es: https://covid19api.com/

Instalación de la librería
Para instalar la librería "pandas" usaremos la función "pip". La exclamación es necesaria para que se ejecute.

```python
!pip install pandas
```
## Configuración de pandas
Para importar utilizaremos la convención "pd" como abreviatura para llamar a la librería.

```python
import pandas as pd
```
## Crear variables
Las variables se asignan con el signo "=" y los escribimos entrecomillados por ser una cadena de carácteres.

```python
miurl = "https://api.covid19api.com/countries"
```
```python
miurl
```

## Empieza la magia de pandas
Creamos un dataframe
La abreviatura que se emplea para dataframe es "df". Existe una función "read_json()" que lee el formato "json" (java script). Dentro del parentesis ponemos el formato de lo que queremos que lea el dataframe, que en este caso es nuestra url.

```python
df = pd.read_json(url)
```

Para visualizar los datos llamamos al objeto. La información se nos muestra en una tabla que contiene 3 columnas y una fila de control de pandas que indica las entradas del dataframe.

```python
df
```
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>Slug</th>
      <th>ISO2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Angola</td>
      <td>angola</td>
      <td>AO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Georgia</td>
      <td>georgia</td>
      <td>GE</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ireland</td>
      <td>ireland</td>
      <td>IE</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Slovenia</td>
      <td>slovenia</td>
      <td>SI</td>
    </tr>
    <tr>
      <th>4</th>
      <td>French Guiana</td>
      <td>french-guiana</td>
      <td>GF</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>243</th>
      <td>Sri Lanka</td>
      <td>sri-lanka</td>
      <td>LK</td>
    </tr>
    <tr>
      <th>244</th>
      <td>Canada</td>
      <td>canada</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>245</th>
      <td>Kuwait</td>
      <td>kuwait</td>
      <td>KW</td>
    </tr>
    <tr>
      <th>246</th>
      <td>Libya</td>
      <td>libya</td>
      <td>LY</td>
    </tr>
    <tr>
      <th>247</th>
      <td>Seychelles</td>
      <td>seychelles</td>
      <td>SC</td>
    </tr>
  </tbody>
</table>
<p>248 rows × 3 columns</p>
</div>

## Exploración de la tabla
Para ver las entradas de la tabla (el número que se le ponga es la cantidad de datos que quieres visualizar tanto de los primeros datos como los últimos) utilizamos la función head o tail:

```python
df.head(12)
```
