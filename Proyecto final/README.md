# Proyecto final: Simulacion de eventos con simpy y Pandas

**Nombre:** Carlos Reyniery Rubio Dominguez  
**Cuenta:** 20201003545  
**Catedratico:** Ing. Uayeb Caballero  
**Clase:** Teoria de simulacion  
**Fecha:** 23/08/2024  

## Descripcion del problema de colas elegido


#### Entregas de ordenes por repartidores
El problema de colas que escogi fue inspirado de una experiencia real pasada hace unas semanas atras cuando en cierta ocacion junto con unos compañeros de trabajo (En la practica profesional) pedimos comida a domicilio y surgieron ciertos inconvenientes, en primer lugar, el repartidor llego despues del tiempo estimado, su excusa fue que el restaurante estaba lleno; y, para finalizar, entrego un pedido que no era el esperado.

Entonces, a partir de ahi me surgio la idea de realizar una simulacion en simpy acerca del proceso que toma un repartidor desde el momento que un cliente realiza un pedido, ese pedido es tomado por un repartidor el cual se mueve en su medio de transporte hacia un restaurante (en el caso de esta simulacion), espera en caja, espera mientras preparan su orden, y, finalmente, se dirige hacia la direccion del cliente que pidio la orden.

## Breve explicacion de la simulacion
- Actores
  - Restaurantes:
    Cada restaurante contiene:
      - Numero de personas atendiendo en caja
      - Numero de personas cocinando
  - Clientes
  - Repartidores

Clases
  - Orden
  - Cliente
  -  Repartidor
  - Restaurante