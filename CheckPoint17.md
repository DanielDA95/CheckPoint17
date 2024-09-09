

## **¿Qué significa CRUD?**

CRUD es un conjunto de operaciones básicas que se utilizan para manipular datos en una aplicación. Estas operaciones son las acciones fundamentales que realizamos cuando interactuamos con bases de datos o sistemas que manejan información.

CRUD es un acrónimo que significa:

1. **Create (Crear)**: Se refiere a la operación de agregar nuevos datos a una base de datos o sistema.
2. **Read (Leer)**: Hace referencia a la acción de recuperar datos almacenados para su visualización o uso.
3. **Update (Actualizar)**: Significa modificar o actualizar un registro ya existente en la base de datos.
4. **Delete (Eliminar)**: Es la acción de eliminar un registro o dato de la base de datos.

### **Ejemplos:**

- **Crear (Create)**: Imagina que te registras en una tienda en línea. Al completar el formulario con tu nombre, correo y contraseña, el sistema realiza una operación de "Crear" para guardar esa nueva información en su base de datos. 

```javascript
app.post('/users', (req, res) => {
    const nuevoUsuario = new Usuario(req.body);
    nuevoUsuario.save();
    res.send("Usuario creado con éxito.");
});
```

- **Leer (Read)**: Luego de registrarte, quieres ver tu perfil de usuario. El sistema hace una operación de "Leer" para recuperar tus datos y mostrártelos.

```javascript
app.get('/users/:id', (req, res) => {
    Usuario.findById(req.params.id).then(user => res.send(user));
});
```

- **Actualizar (Update)**: Si decides cambiar tu dirección o tu número de teléfono, el sistema realizará una operación de "Actualizar" para modificar tu información en la base de datos.

```javascript
app.put('/users/:id', (req, res) => {
    Usuario.findByIdAndUpdate(req.params.id, req.body).then(() => res.send("Usuario actualizado."));
});
```

- **Eliminar (Delete)**: Si decides eliminar tu cuenta, el sistema utiliza una operación de "Eliminar" para borrar tu información de la base de datos.

```javascript
app.delete('/users/:id', (req, res) => {
    Usuario.findByIdAndDelete(req.params.id).then(() => res.send("Usuario eliminado."));
});
```

### **Beneficios de CRUD**:

- **Organización**: CRUD establece un marco claro para estructurar las operaciones que una aplicación necesita para interactuar con los datos.
- **Reusabilidad**: Una vez que tienes implementadas estas operaciones, es fácil mantener el código y aplicar cambios.
- **Escalabilidad**: Puedes integrar fácilmente nuevas funcionalidades o modificar las existentes sin afectar la arquitectura principal de la aplicación.

---

## **¿Qué es un operador ternario?**

Un **operador ternario** es una forma concisa de escribir una estructura condicional en un solo renglón, en lugar de utilizar un bloque completo `if-else`. Un operador ternario evalúa una condición y devuelve uno de dos valores: uno si la condición es verdadera y otro si es falsa. Este operador es ideal cuando tienes una simple decisión que tomar en función de una comparación o evaluación.

### **Sintaxis**:

```javascript
condición ? valor_si_verdadero : valor_si_falso;
```

### **Ejemplo**:

Imagina que en un sistema de e-commerce quieres mostrar un mensaje que indique si un producto está disponible o no, basado en el inventario. Si el `stock` del producto es mayor a cero, mostrarás "Disponible", de lo contrario, mostrarás "Agotado".

```javascript
let stock = 5;
let mensaje = stock > 0 ? "Disponible" : "Agotado";
console.log(mensaje);  // Resultado: Disponible
```

Si `stock` es 0, entonces el resultado sería "Agotado".

### **Beneficios del operador ternario**:

- **Código más limpio**: Reduce la cantidad de líneas necesarias para ejecutar una condición simple.
- **Legibilidad en casos sencillos**: Para condiciones simples, hace que el código sea más fácil de entender al mantener todo en una sola línea.

---

## **¿Qué tipo de solicitud de API hacemos cuando queremos eliminar datos?**

Cuando quieres eliminar un recurso en una API, utilizas el método HTTP **DELETE**. Este método se usa para eliminar un registro en el servidor, ya sea un usuario, un archivo, una entrada de un blog o cualquier otro tipo de dato que desees borrar.

### **Ejemplo en la vida real**:

Supongamos que tienes una aplicación que administra tareas. Si el usuario decide eliminar una tarea que ya ha completado, el sistema hará una solicitud DELETE a la API para eliminar esa tarea del servidor.

```javascript
fetch('https://api.example.com/tareas/1', {
    method: 'DELETE'
})
.then(response => response.json())
.then(data => console.log("Tarea eliminada:", data));
```

En este ejemplo, la solicitud DELETE envía la petición al servidor para eliminar la tarea con ID 1 de la base de datos.

### **Beneficios del método DELETE**:

- **Eficiente y directo**: DELETE está específicamente diseñado para eliminar datos, lo que deja claro para otros desarrolladores el propósito de la solicitud.
- **Seguridad**: Muchas veces, se requieren permisos específicos para ejecutar una solicitud DELETE, lo que ayuda a proteger los datos de ser eliminados accidentalmente o por usuarios no autorizados.

---

## **¿Qué tipo de solicitud de API hacemos cuando queremos actualizar los datos?**

Para actualizar datos en una API, usamos los métodos HTTP **PUT** o **PATCH**. Ambos métodos permiten modificar información en el servidor, pero tienen diferencias importantes:

1. **PUT**: Se utiliza cuando quieres reemplazar por completo un recurso existente con un nuevo conjunto de datos. Con PUT, envías todo el objeto o recurso.
   
   ```javascript
   fetch('https://api.example.com/usuarios/1', {
       method: 'PUT',
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify({ nombre: 'Juan', email: 'juan@example.com' })
   })
   .then(response => response.json())
   .then(data => console.log("Usuario actualizado:", data));
   ```

2. **PATCH**: Se utiliza cuando solo quieres actualizar ciertos campos de un recurso. Por ejemplo, si solo quieres cambiar el correo electrónico de un usuario, usas PATCH para modificar solo esa parte, sin enviar todo el objeto.

   ```javascript
   fetch('https://api.example.com/usuarios/1', {
       method: 'PATCH',
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify({ email: 'nuevoemail@example.com' })
   })
   .then(response => response.json())
   .then(data => console.log("Correo actualizado:", data));
   ```

### **Beneficios del método PUT y PATCH**:

- **Control granular**: Puedes elegir entre actualizar completamente un recurso (PUT) o solo una parte (PATCH), dependiendo de tus necesidades.
- **Claridad y organización**: Estos métodos están bien definidos en el protocolo HTTP, lo que facilita la comunicación y el mantenimiento del código.

---

## **¿Qué es el código dinámico?**

El **código dinámico** es aquel que se genera o cambia mientras se ejecuta un programa. En lugar de ser fijo o estático, el código dinámico responde a las condiciones y entradas del usuario o del sistema, permitiendo que el comportamiento del programa se adapte a las circunstancias.

Por ejemplo, en un sitio web, puedes generar contenido dinámico dependiendo de la información que el usuario ingrese o seleccione. El código no está predefinido, sino que se genera en tiempo real.

### **Ejemplo en la vida real**:

Supongamos que en una tienda en línea quieres mostrar recomendaciones de productos personalizadas según el historial de compras del usuario. El código dinámico puede generar una lista de productos recomendados cada vez que el usuario accede a la página, basado en sus intereses previos.

```javascript
let historialCompras = ['zapatos', 'camisas'];
let productosRecomendados = obtenerRecomendaciones(historialCompras);
productosRecomendados.forEach(producto => {
    console.log("Producto recomendado:", producto);
});
```

El código anterior genera una lista de productos recomendados de manera dinámica, en función del historial de compras del usuario.

### **Beneficios del código dinámico**:

- **Flexibilidad**: El código dinámico permite adaptar el comportamiento de una aplicación en tiempo real según las circunstancias.
- **Personalización**: Puedes ofrecer experiencias personalizadas a los usuarios, lo que mejora la interacción y satisfacción en plataformas como tiendas en línea o redes sociales.

---

Espero que estas explicaciones detalladas te ayuden a comprender mejor los conceptos y cómo aplicarlos en situaciones reales de programación.
