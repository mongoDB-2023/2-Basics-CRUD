# 2-Basics-CRUD
1. [Databases,Collections and Documents](#schema1)
2. [The Shell & MongoDB Drivers](#schema2)
3. [Creating Databases & Collections](#schema3)
4. [Understanding JSON Data](#schema4)
5. [Comparating JSON & BSON](#schema5)

<hr>

<a name="schema1"></a>

## 1. Databases,Collections and Documents
![Basics](./img/basics1.png)


**Base de Datos:**

En MongoDB, una base de datos es el contenedor de alto nivel que almacena conjuntos de colecciones. 
Cada base de datos tiene un nombre único.
Las bases de datos no requieren una estructura predefinida y pueden contener múltiples colecciones.
Ejemplo de creación de una nueva base de datos en MongoDB:

**Colección:**

Una colección es un conjunto de documentos en MongoDB. Es análogo a una tabla en bases de datos relacionales.
Las colecciones no tienen un esquema fijo y pueden contener documentos con campos diferentes.
Las colecciones pueden ser creadas automáticamente cuando se insertan documentos en ellas.
Ejemplo de creación de una nueva colección en MongoDB (se crea automáticamente al insertar el primer documento):


**Documento:**

Un documento es una unidad básica de datos en MongoDB. Es un conjunto de pares clave-valor.
Los documentos en una colección pueden tener campos diferentes, lo que significa que cada 
documento puede tener una estructura única.
Los documentos se almacenan en formato BSON (Binary JSON), que es una representación binaria de JSON.




En MongoDB, las colecciones son flexibles en cuanto a la estructura de los documentos que pueden almacenar. 
A diferencia de las tablas en las bases de datos relacionales, donde cada fila debe seguir el mismo esquema, 
en MongoDB, los documentos dentro de una colección pueden tener estructuras diferentes. Esto se conoce como un 
modelo de datos flexible o un esquema dinámico.

En una misma colección, puedes tener documentos con campos diferentes y estructuras variadas. 
Esto significa que un documento puede contener un conjunto específico de campos, mientras que otro documento 
puede tener campos adicionales o diferentes.

<hr>

<a name="schema2"></a>


## 2. The Shell & MongoDB Drivers

- CRUD

https://www.mongodb.com/docs/mongodb-shell/crud/

<hr>

<a name="schema3"></a>

## 3. Creating Databases & Collections

- use base_de_datos
```
test> use flights
switched to db flights
```
Cuando usamos este comando se selecciona la base de datos, pero si la base de datos no existe se creará. 
Hay que tener en cuenta que la base de datos no se creará físicamente en el disco hasta que se 
inserte el primer documento o se realice alguna otra operación en esa base de datos.

- Creando colleción
```
flights> db.flightData.insertOne({})
```

En este caso al haber usado la primera sentecina `use BBDD`, ya estamos en la base de datos que queremos, ahora entrará
en la colección correspondiente si existe, sino existe la crea y además inserta los datos.


<hr>

<a name="schema4"></a>

## 4. Understanding JSON Data

```
[
  {
    "departureAirport": "MUC",
    "arrivalAirport": "SFO",
    "aircraft": "Airbus A380",
    "distance": 12000,
    "intercontinental": true
  },
  {
    "departureAirport": "LHR",
    "arrivalAirport": "TXL",
    "aircraft": "Airbus A320",
    "distance": 950,
    "intercontinental": false
  }
]

```
- Insertar en la colección
```
flights> db.flightData.insertOne({
...     "departureAirport": "MUC",
...     "arrivalAirport": "SFO",
...     "aircraft": "Airbus A380",
...     "distance": 12000,
...     "intercontinental": true
...   })
{
  acknowledged: true,
  insertedId: ObjectId('655f66c6a053c6f344e7bb60')
}

```
- Ver lo que hay dentro de la coleccion
```
flights> db.flightData.find()
[
  {
    _id: ObjectId('655f66c6a053c6f344e7bb60'),
    departureAirport: 'MUC',
    arrivalAirport: 'SFO',
    aircraft: 'Airbus A380',
    distance: 12000,
    intercontinental: true
  },
  {
    _id: ObjectId('655f675ca053c6f344e7bb61'),
    departureAirport: 'LHR',
    arrivalAirport: 'TXL',
    aircraft: 'Airbus A320',
    distance: 950,
    intercontinental: false
  }
]

```
<hr>

<a name="schema1"></a>


## 5. Comparating JSON & BSON
![basics](./img/basics2.png)

En el caso específico de MongoDB, el formato de almacenamiento predeterminado es BSON (Binary JSON). 
MongoDB utiliza BSON para representar documentos almacenados en sus colecciones. Aunque la interfaz de consulta 
y manipulación de datos en MongoDB se asemeja a trabajar con documentos JSON, internamente, los datos se almacenan 
en formato BSON.

Aquí hay algunas razones por las que MongoDB utiliza BSON:

- Eficiencia de Almacenamiento y Transmisión: BSON es un formato binario que resulta más eficiente en términos de 
almacenamiento y ancho de banda en comparación con JSON. Esto es beneficioso para la eficiencia de MongoDB, 
- especialmente cuando se trata de grandes cantidades de datos.

- Tipos de Datos Adicionales: BSON extiende el conjunto de tipos de datos que se pueden representar 
en comparación con JSON estándar. MongoDB utiliza estos tipos de datos adicionales para almacenar información 
específica, como fechas y datos binarios, de una manera más eficiente que si se codificaran directamente en JSON.

- Desempeño en Operaciones de Búsqueda y Indexación: La estructura binaria de BSON permite realizar 
operaciones de búsqueda y indexación más eficientes en comparación con JSON. Esto es fundamental 
para el rendimiento de las consultas en MongoDB, especialmente en entornos donde la velocidad de acceso 
a los datos es crítica.

En resumen, MongoDB utiliza BSON como su formato de almacenamiento interno para aprovechar las ventajas 
de eficiencia y funcionalidad adicional que ofrece en comparación con JSON estándar. Aunque la interfaz 
de MongoDB se presenta de manera similar a JSON, la elección de BSON subyacente contribuye a la eficiencia 
y el rendimiento general del sistema.

