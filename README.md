### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

### Autores: Tomas Suarez y Camilo Murcia

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/es-es/free/students/). Al hacerlo usted contará con $100 USD para gastar durante 12 meses.
Antes de iniciar con el laboratorio, revise la siguiente documentación sobre las [Azure Functions](https://www.c-sharpcorner.com/article/an-overview-of-azure-functions/)

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

Realizado:

![image](https://github.com/user-attachments/assets/2d57fa46-03e1-4dda-9e6c-106d9530170f)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

Realizado:

![image](https://github.com/user-attachments/assets/16e060aa-b1ad-4693-8208-71ccdfb52637)


3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

Realizado: 

![image](https://github.com/user-attachments/assets/6393fcc9-8c76-4550-b9d8-43f6169a434e)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

Realizado: ![image](https://github.com/user-attachments/assets/5e06163d-3f0f-41f3-beb1-13335b55fef6)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

Se crea el archivo de Fibonacci.postman_collection.json para poder escribir la configuracion necesaria.
![image](https://github.com/user-attachments/assets/7001fbc3-f8a5-4b9c-9558-e006715767ba)

Se utiliza el siguiente comando para poder enviar las peticiones concurrentes:

   ```bash
    cd postman
    newman run Fibonacci.postman_collection.json -n 10
   ```

6. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

![image](https://github.com/user-attachments/assets/21e77349-1347-4d41-9eec-a04cf374d56a)

Prueba para 300000:

![image](https://github.com/user-attachments/assets/7b316817-fb66-46d8-91c7-361c108a2eaf)

Prueba para 400000:

![image](https://github.com/user-attachments/assets/49229591-b005-4f0f-9dfb-b68bbcf4f418)

Prueba con 1000000:

![image](https://github.com/user-attachments/assets/6875b21a-b03d-4b35-96ef-875eb6f466c6)

Despues de esperar 5 minutos sube un poco el tiempo de respuesta, algo que tambien se noto, es que al intentar enviar peticiones con valores muy grandes, ocurren errores de recursion, por lo que no se recibe una respuesta por parte de la funcion.

**Preguntas**

* ¿Qué es un Azure Function?
* ¿Qué es serverless?
* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?
* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?
* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos.
* ¿Por qué la memoization falla o no funciona de forma correcta?
* ¿Cómo funciona el sistema de facturación de las Function App?
* Informe
