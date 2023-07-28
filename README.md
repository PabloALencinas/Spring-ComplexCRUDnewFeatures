# CONTINUACION DEL CURSO COMPLETO DE SPRING & SPRING BOOT

# CONTINUAMOS CON EL MISMO PROYECTO AGREGANDO NUEVAS FEATURES A LA APLICACION (luego de spring security)

# Seccion 16 - Local y Multilenguaje I18N

## 1) Configuracion de nuestro sistema multilenguaje y el Locale

    - Nos dirigimos al MvcConfig y alli implementaremos un par de Beans (ver seccion codigo con comentario)
    - Una vez implementado los dos metodos, debemos REGISTRAR el localInterceptor en nuestra app con sobreescritura
    del metodo addInterceptors()
    - RESUMIENDO
        -> DOS BEANS - 1) Resuelve el locale, donde se va a guardar (sesion) - 2) Interceptor que se encarga de cambiar el lenguaje
           segun el parametro dado
        -> Metodo para registrar el INTERCEPTOR 

## 2) Creando archivos de idiomas para los diferentes lenguajes (es_ES, en_US, de_DE and Japanese(my own choice))

    - Estos archivos son el motor, combustible crucial, para que funcione el sistema multilenguaje ya que provee
    todos los textos. Son los traductores.
    - Lo creamos en recursos de la raiz -> UNO por cada idioma

## 3) Crear links en el menu de navegacion para cambiar el idioma

    - Vamos a template, layout y agregamos dicos links dentro del header

## 4) Creando el controlador LocaleController para el manejo de los links y cambios de idioma en la aplicacion 

    - LocaleController y su implementacion (ver codigo) 
    - Dentro del layout modificamos la ruta

## 5) Traducciones en los controladores

    - La idea es pasar al controlador cliente que maneja las request mas importantes de la app, los campos que van a ser
    traducidos y no simplemente el texto plano (VER 'listar' en controlador)
    - Agregamos tambien algunos campos dentro de nuestro properties de cada idioma

## 6) Traduciendo el texto del paginador

## 7) Traduciendo todo el Codigo

    - Este apartado es saltado ya que solo se muestra la app con las traducciones finales.
    - SI DESEA HACERLO, QUEDA COMO TAREA LA TRADUCCION DE TODAS LAS SECCIONES!

# Y AQUI TERMINA LA SECCION 16 - LOCALE Y MULTILENGUAJE I18N 
# CONTINUAMOS CON MAS FEATURES
# Este proyecto continuara con un par mas de features Las cuales son las siguientes

    -> View Technologies: Exportar a PDF
    -> View Technologies: Exportar a Excel
    -> View Technologies: Exportar a CSV (Archivo plano)

## Estas features van a seguir dentro de este proyecto. Una vez terminadas pasaremos a otra seccion con un proyecto nuevo

# Seccion 17 - VIEW TECHNOLOGIES: Exportar a PDF (Exportar el detalle de factura a PDF)

## 1) Configuraciones necesarias y dependencias de OpenPDF (fork de iText)

    - Agregamos al POM.XML la dependencia necesaria para el uso de 'OpenPDF' (Ver mas en repositorio github del proyecto)
    - Agregamos en application.properties para que soporte el mediatypes para PDF
    - TENDREMOS un parametro en el componente que se encarga de manejar los view resolvers para tener diferentes opciones
    de vista. Ejemplo: detalle ver-factura -> ver.html. Podriamos tener lo mismo para devolver en PDF. En vez de dirigir a 
    thymeleaf, lo dirigimos a un resolver para PDF

    - Lo que agregamos al application.properties
        -> spring.mvc.contentnegotiation.favor-parameter=true
        -> spring.mvc.contentnegotiation.media-types.pdf=application/pdf

## 2) Creando la vista PdfView para la factura

    - Como creamos una vista en PDF?
    -> NO hay plantilla, no etiquetas, no xml.. ES UNA CLASE, una clase que debemos implementar con un metodo constructor
    del PDF

    - Creamos un package para la vista del PDF con la clase FacturaPdfView -> Debe estar anotada con @Component, la debemos 
    registrar en el contenedor de Spring. El component DEBE dirigir al metodo que muestra los detalles (ver)
    del FacturaController. 

    - Dentro de la clase implementamos la sobreescritura del metodo "buildPdfDocument"

## 3) Creando el link para exportar a documento PDF

    - Vamos a la vista de detalle factura/ver
    - Una vez implementado el <a> para la factura en pdf ya la podemos ver y descargar desde el template
    - Agregamos mas 'definiciones' a la factura en el FacturaPdfView

## 4) Escribiendo el codigo de las lineas de la Factura en la vista PDF

    - Creamos la tabla numero 3 para el detalle de la factura en la clase FacturaPdfView

## 5) Mejorando el diseno y look and feel de la vista PDF

    - Agregamos algunos parametros de diseno dentro del controlador para la vista en Pdf de la Factura
    - con 'cell' como parametro e invocamos los metodos de diseno de la clase

## 6) Traduciendo la vista PDF a diferentes idiomas (internacionalizacion I18N)

    - La forma de manera de manejar el idioma es a traves del 'MessageSource' y el 'LocaleResolver'


# Seccion 18 - VIEW TECHNOLOGIES: Exportar a Excel (Exportar el detalle de factura a PDF)

## 1) Configuraciones necesarias y dependencias

    - Configuracion y dependencias.
    -> Agregamos en el app.properties la configuracion (parecida al PDF)
    - Libreria de APACHE -> APACHE POI (POI OOXML)
    - Agregamos la dependencias al POM.XML correspondiente a la libreria
    -> CREAMOS UN NUEVO PACKAGE PARA XLS (Parecido como hicimos con PDF)
    - Sobreescribimos el metodo (parecido al PDF) -> buildExcelDocument

## 2) Implementando la clase de vista FacturaXlsxView para la factura

    - Implementamos los metodos y llamadas necesarias para poder llevar los datos a las celdas correspondientes
    a excel.
    - Nos dirigimos a la vista "ver" de factura y agregamos el link para podes ver la factura en formato excel

## 3) Escribiendo el codigo del detalle de la Factura en la vista Excel

    - Crearemos un 'diseno' de como se vera el excel al exportarlo
    - Ver comentarios de implementacion en el codigo (FacturaXlsxView)

## 4) Mejorando el diseno y look and feel de la planilla Excel

    - Implementamos diseno para la planilla (como hemos realizado con PDF) 

## 5) Traduciendo la vista Excel a diferentes idiomas (Internacionalizacion)

    - Implementamos la misma configuracion realizada para el PDF, usando MessagesSourcesAccessor

# Seccion 19 - VIEW TECHNOLOGIES: Exportar a CSV (Archivo plano)

## 1) Configuracion y creando la clase ClienteCsvView

    - Trabajaremos con una Dependencia que nos facilite el trabajo con CSV -> Super CSV
    - Agregamos la dependencia a traves de MAVEN
    - Creamos el package con la clase de manejo del package -> ClienteCsvView
        -> El CSV se utiliza, la mayoria de veces, para un LISTADO una COLLECTION por eso lo haremos con clientes
        y NO para un DETALLE. Ej: Listado de FACTURA no DETALLE, es raro!

    - Sobreescribimos los metodos necesarios a implementar.

## 2) Implementando la clase ClienteCsvView y Link en vista clientes

    - Tenemos que obtener el listado de clientes e implementamos el pasaje a archivo planos del cliente
    - Ahora creamos el link en la vista "listar" de clientes

## Tener mas de una vista con @Component y media types

    - Agregamos una extension para los @Component para evitar el duplicado de vistas
    - PERO si agregamos y luego dentro de nuestro app.properties no esta configurado el CONTENTNEGOTIATON media types
    NO FUNCIONARA.
    -> Agreguemos al ejemplo del csv dentro del app.properties

        -> spring.mvc.contentnegotiation.media-types.csv=text/csv

# Seccion 20 - VIEW TECHNOLOGIES: Convertir a XML

    - Centrado a REST, tanto a XML como JSON
        -> REST: Representacion de un flujo de datos en un formato que sea compatible y estandar, basado en HTTP
    - MUCHAS FORMAS DE APLICAR UN REST
        - UN CONTROLADOR comun y corriente, con un metodo handler response body, representacion de unos datos en REST
        - LA VENTAJA: Nos permite tener un controlador handler tanto para REST con JSON, XML o metodos comun y corrientes
        con vista a html o thymeleaf
        - O UN CONTROLADOR 100% enfocado a REST

    - Implementaremos un controlador con un solo metodo que genere multiples representaciones de VISTAS, necesitamos
    una clase VIEW, se maneja parecido con html, excel, csv.. 
    - Una vista que mantiene un nombre, un tipo de contenido (media type).. lo mismo pero para XML y JSON
    
    - A traves del OBJECT/XML MAPPING, OXM -> Vamos a tener dos opciones
        -> Conversion de OBJETO a XML (Marshalling)
        -> Conversion de XML a OBJETO (Unmarshaller)


## 1) Agregando dependencia JAXB-API solo para JDK 9 o Superior

    - EXPORTAR a XML
    - Desde JDK 9 se elimino el 'API-JAXB', como se elimino del core de JAVA, tenemos que agregar la dependencia de manera
    manual en el POM.XML    
        -> JAXB API » 2.4.0-b180830.0359
        -> JAXB RUNTIME

## 2) Configuracion y creando la clase XML Wrapper

    - Configurando el bean, componente, que se encarga de convertir un OBJETO a un XML
    - En MvcConfig lo implementamos
    - Necesitamos una clase WRAPPER para que envuelva nuestra LISTA ya que xml de por si no puede hacerlo (el conversor)

## 3) Creando la clase view ClienteListXMLView

    - Implementamos la clase para la vista -> CLienteListXMLView y sobreescribimos el metodo que usaremos para la implementacion
    - VER COMMENTS en codigo para mas informacion

## 4) Implementando Link en vista listar clientes

    - Dentro del LISTAR de clientes vamoa a agregar el link para exportar a XML el listado de clientes
    - COMO VENIAMOS TRATANDO al iniciar la aplicacion y tratar de descargar el XML nos sale una excepcion
    - El error se debe a la relacion BIDIRECCIONAL que existe entre FACTURA y CLIENTE
    - Debemos bloquear el acceso de la bidireccion y que sea unidireccional
    - dentro del entity de FACTURA agregamos la anotacion @XmlTransient para arreglar este error

# Seccion 21 - VIEW TECHNOLOGIES: Convertir a JSON 

## 1) Creando la clase view ClienteListJsonView

    - Ya se incluye de forma default de spring, las dependencias necesarias para los JSON
    - No hay que configurar ningun Bean ni nada, esta todo automatizado
    - Creamos la vista JSON e implementamos el codigo necesario
        -> Y no es necesaria una clase Wrapper ya que puede trabajar con cualquier tipo de datos.
    - Creamos el boton en la vista para la descarga

    - TENDREMOS EL MISMO PROBLEMA DE LOOP INFINITO COMO EN CLIENTES POR TEMAS DE BIDIRECCIONALIDAD EN LAS CLASES
        -> En la clase ENTITY de CLiente, en atributo FACTURAS -> @JsonIgnore
    - Nos aparecen atributos dentro del JSON que no nos interesa, como paginables y demas
    - Para sacar esto, en la vista (ClienteListJsonView class) filtramos el cliente, parecido como xml

## 2) Modificar las clases Entities con anotaciones JSON para manejar las referencias

    - Quitamos el JSONIGNORE de factura, ya que nos interesa mostrar
    - EN la clase CLIENTE en vez, de JSONIGNORE en facturas agregamos JSONMANAGEDREFERENCE

    - EN la clase FACTURAS, en el atributo CLIENTES -> agregamos la anotacion @JsonBackReference
    - EN ITEMFACTURA, debemos agregar una anotacion en el atributo PRODUCTO -> @JsonIgnoreProperties({"hibernateLaziInitializer",
    "handler"})

# Seccion 22 - VIEW TECHNOLOGIES: API REST

## 1) Forma usando anotacion @ResponseBody sobre el metodo handler

    - 2da forma para implementar REST en nuestra aplicacion
    - Implementar, NO UNA VISTA, sino un handler controlador que se encarga de renderizar una vista del tipo REST (JSON, XML)
        -> NO HTML, SOLO REST!

    - Copiamos el metodo LISTAR dentro de cliente e implementamos lo necesario alli
    - SI no estamos autenticado no podemos ver los datos, es logico ya que estamos con Spring Security
        -> Para esto nos vamos a SpringSecurityConfig
            - Alli implementamos lo siguiente: agregamos el 'api/listar' dentro del authorizedRequest
            - COMO EN NUESTRO EJEMPLO SOLO TRABAJAMOS CON ROLES AUTENTICADOS, NO SE VERA REFLEJADO ESTE CAMBIO 

    - SI QUEREMOS PODER ENVIAR TANTO JSON COMO XML DEBEMOS AGREGAR LO SIGUIENTE AL CONTROLADOR

        	@GetMapping("/api/listar")
            @ResponseBody // IMPORTANTE, para la respuesta del tipo REST es necesaria esta ANOTACION
            public ClienteList listarRest(){
                return new ClienteList(clienteService.findAll());
            }

## 2) Forma usando anotacion @RestController sobre la clase contoller

    - Como resumen de lo anterior, el @ResponseBody convierte la clase objeto (POJO, entity, cualquier tipo de objeto)  
    en una respuesta JSON o XML
    - Que sucede si quiero aplicar un CONTROLADOR especifico y que este dedicado 100% a una API REST 
        -> ANOTAMOS CON @RestController: Combina dos, @Controller + @ResponseBody (Todos sus metodos van a ser @ResponseBody)

    - Creamos un CONTROLADOR para visualizar esto -> ClienteRestController

# Y AQUI FINALIZA EL PROYECTO COMPLETO ANTES DE JWT
# Como sumario de todo el proyecto hasta aqui tenemos los siguientes conceptos

    AGREGAMOS NUEVAS FEATURES AL PROYECTO QUE TRABAJAMOS EN LAS SECCIONES ANTERIORES (SISTEMA DE FACTURACION C/ SPRING SECURITY)
        - DENTRO DE ESTAS FEATURES NOS ENCONTRAMOS CON 

            -> Locale y Multilenguaje I18N: Traduccion y manejo de idiomas para nuestra aplicacion
            -> Exportar informacion en distintos formatos:
                1) PDF
                2) EXCEL
                3) CSV
                4) XML
                5) JSON
            -> Y el manejo de la arquitectura de software "REST" para el manejo de controlador

# CONTINUAMOS CON EL SIGUIENTE PROYECTO, IMPLEMENTACION DE JWT (JSON WEB TOKEN) PARA SEGURIDAD
# Nombre del proyecto (springboot-data-jpa-v4JWToken)







