<h1>MODELO DIMENSIONAL PARA EL REGISTRO DE ORDENES A TRAVÉS DE APLICACIÓN DE DELIVERY</h1> 

<h2>Descripción del Proyecto</h2>
<p>Proyecto desarrollado en la Especialización de la Ingeniería de Datos de la Universidad de El Salvador para construir un DataWarehouse que pueda ser utilizado para dar respuestas analíticas de interés para el proceso de negocio seleccionado para este caso de análisis se pone en estudio el servicio de delivery a través de una aplicación que reúne  datos que necesitan de un tratamiento y transformación.</p>

<h2>Descripción del Dataset</h2>
<p>El dataset contiene un conjunto de datos que han sido almacenado durante el tiempo en base de datos por medio de aplicación de servicio de comida a domicilio en Oman llamada Akeed. Esta aplicación registra las ordenes de pedidos realizado por los clientes desde varias ubicaciones a proveedores de restaurantes.</p>

<h2>Reglas de Negocio </h2>
<p>Akeed es una empresa de servicio de delivery a traves de su aplicación movil en Oman. Esta es una plataforma d eentrega de alimentos con la red más grande con 1,100 restaurantes y tiendas comestibles.

A continuación, se detalla los pasos del modelo de negocio para la obtención del servicio:</p>
<ol>
  <li><i>Búsqueda:</i> en la aplicación, ingresar la ubicación para mostrarle los restaurantes y puntos de venta de comida que se encuentran a su alrededor. Buscar y elegir entre restaurantes, tiendas de alimentación, dulces y repostería.</li>
  <li><i>Ordenar:</i> explorar en la selección por cocina, precio o calificación. Ver imágenes de los platos y seleccionar las opciones agregando al carrito.</li>
  <li><i>Pago:</i> se permite el pago en línea o cuando llegue el repartidor, se puede pagar en efectivo o con tarjeta contra reembolso.</li>
  <li><i>Entrega:</i> el repartidor recoge el pedido una vez que está listo y lo entrega a su ubicación.</li>
</ol>

<h2>Modelo de Datos</h2>
<img src="https://user-images.githubusercontent.com/18757517/150695568-5aa53417-e324-48d0-9fe6-a0d4c6b7e4a1.jpeg">

<h2>Caracteristicas del Modelo Dimensional </h2>
<h3>Star Schema</h3>
<p>El modelo dimensional este modelado bajo el enfoque de esquema estrella. Los datos se encuentran organizados en la fact table y dimensiones que almacena los eventos del proceso de negocio y las métricas.</p>

  <h4>Tablas de Dimensiones:</h4>
  <p>Describen el contexto de los eventos del proceso, en este caso describen las entidades contextuales del registro de ordenes en la aplicación de delivery. Las dimensiones del modelo dimensional propuesto son: <i>Order dimension, Customer dimensión, Date dimensión, Vendor dimensión, Location dimensión, Tag dimensión</i>.
</p>
  <h4>Tabla de Hechos:</h4>
<p>Contiene el registro de eventos del modelo dimensional, en este caso de estudio almacena el registro de órdenes a través de la aplicación.
  Esta tabla de hechos o fact table almacena las claves de las dimensiones y las métricas definidas en el modelo dimensional. La fact table definida en el modelo es: <i>Order    registration fact table </i>.

  <h3>Slowly Changing Dimensions</h3>
    <h4>SCD Tipo 0: Valores Estáticos</h4>
    <p>La <i>Date Dimensión </i> aplicará SCD Tipo 0 ya que la dimensión tiene valores estáticos el valor de sus atributos nunca cambiarán en el tiempo, si se añaden columnas o  registros no afectan a sus atributos existentes en sus datos.   </p>
    <h4>SCD Tipo 1: Valores Sobre Escritos</h4>
    <p>Las dimensiones con SCD Tipo 1 son dimensiones que pueden cambiar en el tiempo, la estrategia es sobrescribir sus valores. Estas dimensiones con SCD1 reflejan el estado más reciente en sus atributos. Al usar SCD1 se pierde la historia y es difícil determinar cuándo ocurren estos cambios. En el modelo dimensional se aplica SCD1 porque no se tiene interés en la historia en ciertos atributos en valores en las dimensiones. 

Se le aplicará SCD tipo 1 a las siguientes dimensiones: <i>Orden Dimensión, Customer Dimensión, Vendor Dimensión, Location Dimension</i>.
</p>

<h2>Arquitectura Funcional</h2>
<img src="https://user-images.githubusercontent.com/18757517/150696635-0b4a95d2-5629-4f35-bbd5-f6f543c9c385.png" >

<h3>Data sources:</h3>
<p>Los datos son obtenidos en formato de csv de un repositorio de datos llamado Kaggle, siendo este un repositorio de datos que permite la exploración de distintos dataset que brindan los insumos necesarios para la creación de modelos en un entorno de ciencia de datos basado en la web. En este punto los datos son obtenido en su forma más pura, con muchas inconsistencias en formatos, campos vacíos etc.</p>
<h3>Data lake:</h3>
<p>
  <i>Raw data zone</i>:
Los datos se ingieren sin procesamiento y se almacenan en su formato nativo. Esta zona permite a los usuarios encontrar la versión original de los datos para sus análisis facilitar los tratamientos posteriores.
  
<i>Process zone</i>:
En esta zona los usuarios pueden transformar los datos según sus requisitos y almacenar todos los datos intermedios. El procesamiento de datos incluye lotes y/o procesamiento en tiempo real. Esta zona permite a los usuarios procesar datos (selección, proyección, unión, agregación, etc.) para su análisis de datos.

<i>Access zone</i>:
La zona de acceso almacena todos los datos disponibles para el análisis de datos y proporciona el acceso a los datos. Esta zona permite el consumo de datos de autoservicio para diferentes análisis (informes, análisis estadístico, inteligencia empresarial análisis, algoritmos de aprendizaje automático).
</p>
<h3>Data Consumption</h3>
<p>El consume de datos es a través de Power BI como una herramienta basada en la nube que permite unir diferentes fuentes de datos, analizarlos y presentar un análisis de estos a través de informes y paneles.</p>
