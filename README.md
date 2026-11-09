# Proyecto-Ingenieria-de-software2
# TiendaDP

Tienda en línea hecha en Java para el parcial de Patrones de Diseño de Ingeniería de Software 2 (propuesta 1). Se puede usar por consola o con una interfaz gráfica en Swing, y las dos usan la misma lógica por debajo.

**Integrantes:** Juan Ospina, Juan Rodriguez y Erick Penagos

**Entrega final:** 23 de noviembre de 2026

> Este proyecto todavía está en desarrollo. Lo que está acá es el plan que hicimos antes de programar, así que algunos nombres de clases o detalles pueden cambiar. Cuando terminemos el código lo revisamos contra esto y lo actualizamos.

---

## De qué trata

La idea es un sistema de compras con catálogo, carrito y cierre de pedido. El cliente escoge productos, les agrega extras, el sistema le calcula los descuentos, paga con un medio de pago simulado y al final se genera una factura. También hay un modo administrador para registrar productos, reponer stock y crear cupones.

Todo está en Java 17 y los precios son en pesos colombianos (COP) con IVA incluido. Para el dinero usamos `BigDecimal` y no `double`, para no tener problemas con los decimales.

---

## Alcance

La propuesta del profe trae una lista de opciones y cada grupo decide cuáles hace. Esto es lo que decidimos nosotros.

### Lo que sí vamos a hacer

- **Catálogo con tres categorías:** ropa, tecnología y alimentos. Cada una tiene sus propios atributos, y esa es la primera parte del sistema donde hay variación.
- **Carrito de compras:** agregar, quitar y cambiar cantidad. Es el centro de todo el flujo de compra, y de ahí dependen los descuentos y los extras.
- **Descuentos:** por cantidad, por temporada, por cliente frecuente y por cupón. Algunos se pueden acumular y otros no, y esas reglas pueden cambiar con el tiempo.
- **Medios de pago simulados:** tarjeta, transferencia y contra entrega. Cada uno valida cosas distintas y cobra recargos distintos.
- **Extras sobre un producto:** garantía extendida, empaque de regalo y envío express. Se pueden combinar como uno quiera.
- **Aviso de reposición:** si un producto está agotado y vuelve a tener stock, los clientes que se suscribieron reciben un aviso.
- **Historial de pedidos y factura:** la factura se genera como texto formateado y se ve en consola y en ventana.
- **Modo administrador** (sin contraseña): registrar productos, reponer stock y crear cupones. Lo necesitamos para poder demostrar las categorías y los avisos de reposición.

### Lo que dejamos por fuera

| Qué | Por qué |
|---|---|
| Base de datos o archivos | Los datos viven en memoria mientras corre el programa. Dejamos una interfaz `Repositorio` para poder cambiarlo después sin romper nada. |
| Registro de usuarios con contraseña | El cliente se elige o se crea solo con un nombre. Una contraseña no aporta nada a los patrones. |
| Pasarelas de pago reales | El enunciado pide que los pagos sean simulados. |
| Logística de envíos, devoluciones y cancelaciones | El envío express es solo un extra con costo. Lo demás agranda el sistema pero no agrega variación nueva. |
| Correos o SMS reales | Los avisos llegan a una bandeja de avisos del cliente, que se ve en consola y en la GUI. |
| Aplicación web | El enunciado dice que no es obligatoria y no da puntos extra. |

### Dónde hay variación o cambio frecuente

El enunciado pide mínimo tres zonas y nosotros tenemos cinco:

1. Las categorías de producto
2. Los descuentos
3. Los medios de pago
4. Los extras
5. Los avisos de reposición

Los porcentajes, recargos y demás valores que aparecen más abajo son una propuesta inicial nuestra. En el código van a quedar como constantes que se puedan cambiar fácil.

---

## Requisitos funcionales

**RF-01.** Registrar productos con su categoría y los atributos de esa categoría:
- Ropa: talla y color
- Tecnología: marca y meses de garantía
- Alimentos: fecha de vencimiento y si necesita refrigeración

Todo producto tiene código, nombre y precio base.

**RF-02.** Ver el catálogo completo y filtrarlo
