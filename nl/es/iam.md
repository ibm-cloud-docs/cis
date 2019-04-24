---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM y CIS
{:#iam-and-cis}

IBM Cloud Internet Services (CIS) utiliza IAM para llevar a cabo la autorización y la autenticación.

Si no desea añadir a nadie a su instancia de CIS, puede ignorar esta página.
{:note}

Restringir el acceso por tres ámbitos funcionales de CIS, en base al árbol de navegación: 
* fiabilidad - como por ejemplo DNS, GLB
* seguridad - como por ejemplo Certificado, reglas de cortafuegos de IP y limitación de velocidad
* rendimiento - como por ejemplo Reglas de página, almacenamiento en memoria caché y direccionamiento

Esta sección le indica cómo conseguir un control de acceso preciso de la instancia.

## Roles
{:#iam-and-cis-roles}

Utilice los tres roles siguientes para utilizar IAM
* Lector - Puede obtener información sobre la instancia y sobre el dominio
* Escritor - Puede hacer cambios en la configuración existente
* Gestor - Puede crear o suprimir instancias, dominios, configuración

## Grupos de acceso y usuarios
{:#iam-and-cis-access-groups-users}

Se puede asignar una política directamente a un usuario o a un grupo de acceso.
Recomendamos asignarla a un grupo de acceso para minimizar el número de políticas creadas y para reducir el esfuerzo de gestión de las mismas.

## Memoria caché
{:#iam-and-cis-cache}

Guardamos los resultados de autorización en la memoria caché y utilizamos la memoria caché para tomar una decisión cuando vuelve a llegar la misma solicitud. Cuando la memoria caché alcanza su Tiempo de duración ( 10 min), expira.

## Prácticas recomendadas
{:#iam-and-cis-best-practices}

1. En lugar de modificar una política, suprima la política existente y, a continuación, cree una nueva.

## Escenarios
{:#iam-and-cis-scenarios}

En esta sección se tratan diferentes ejemplos de políticas de acceso creadas a través de CIS. 

### Nivel de dominio con el tipo `config` type
{:#iam-and-cis-scenarios-domain-level}

#### Acceso a un dominio con `security config` en un grupo de acceso
##### Rol de escritor

Bob tiene una instancia de CIS, `cis-test-instance`, y dos dominios, `bob.com` y `bob-ibm.com`.
Bob quiere dar acceso a todos los ingenieros de seguridad de la empresa (sec-group) al rol de escritor solo en la **configuración de seguridad** de **`bob.com`**.

Estos pasos muestran cómo crear una política de IAM para que este escenario sea posible.

Después de iniciar sesión en cis-test-instance, Bob:
1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona el **grupo de acceso** - **sec-group** al que desea proporcionar acceso
1. Selecciona **`bob.com`**
1. Selecciona el rol **Escritor**
1. Selecciona la opción **Configuración de seguridad**
1. Pulsa en **crear política**

En el separador Gestionar:
se crean las políticas siguientes para **sec-group**:

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance 
    name: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domain 
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Config Type
    cfgType: security
```

Ahora sec-group tiene acceso a ver solo `bob.com` y puede modificar los valores que pertenecen a la seguridad. 

##### Actualizar del rol de Escritor al rol de Gestor en un grupo de acceso

Si Bob desea actualizar el rol de sec-group de Escritor a Gestor, tiene que suprimir la política existente. 
1. Va al **separador Gestionar IAM > Grupos de acceso > sec-group > políticas de acceso**
1. Suprime la política siguiente 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

A continuación, Bob tiene que crear la nueva política. 
1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona el **grupo de acceso** - **sec-group** al que desea proporcionar acceso
1. Selecciona **`bob.com`**
1. Selecciona el rol **Gestor**
1. Selecciona la opción **Configuración de seguridad**
1. Pulsa en **crear política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

Si la política existente (escritor) no se suprime, el intento de crear la política para Gestor falla.

##### Actualizar la configuración para incluir Rendimiento junto con Seguridad

Si Bob quiere dar acceso de sec-group de Gestor a la configuración de rendimiento en `bob.com` junto con la seguridad:
1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona el **grupo de acceso** - **sec-group** al que desea proporcionar acceso
1. Selecciona **`bob.com`**
1. Selecciona el rol **Gestor**
1. Selecciona la opción **Configuración de rendimiento**
1. Pulsa en **crear política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### Acceso a todos los dominios con `security config`

Si desea proporcionar acciones de seguridad para `bob.com` y `bob-ibm.com` del ejemplo anterior, debe crear una política nueva repitiendo los pasos para cada dominio. La única diferencia es seleccionar el dominio correspondiente para cada política.

1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona el **grupo de acceso** - **sec-group** al que desea proporcionar acceso
1. Selecciona **`bob.com`**
1. Selecciona el rol **Gestor**
1. Selecciona la opción **Configuración de seguridad**
1. Pulsa en **crear política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona el **grupo de acceso** - **sec-group** al que desea proporcionar acceso
1. Selecciona **`bob-ibm.com`**
1. Selecciona el rol **Gestor**
1. Selecciona la opción **Configuración de seguridad**
1. Pulsa en **crear política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### Acceso a un dominio con `security config` y `reliability config`

Bob tiene una instancia de CIS cis-test-instance y 2 dominios `bob.com` y `bob-ibm.com`.
Bob quiere proporcionar acceso a Tony al rol de Escritor solo para las **acciones de seguridad y fiabilidad** de **`bob-ibm.com`**.

Después de iniciar sesión en cis-test-instance, Bob:
1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona **Tony**, a quien desea proporcionar acceso
1. Selecciona **`bob-ibm.com`**
1. Selecciona el rol **Escritor**
1. Selecciona el recuadro correspondiente a la opción **Seguridad y fiabilidad** 
1. Pulsa en **crear política**

De esta forma se crean dos políticas en el programa de fondo para cada tipo de configuración.

### Nivel de dominio con todos los tipos de configuración
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob desea otorgar acceso de lectura/escritura/gestión a nivel de dominio a Tony.

#### Escritura
Después de iniciar sesión en cis-test-instance, Bob:
1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona **Tony**, a quien desea proporcionar acceso
1. Selecciona **`bob.com`**
1. Selecciona el rol **Escritor**
1. Marca todos los recuadros de Ámbito funcional de CIS
1. Pulsa en **crear política**

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Gestor
Después de iniciar sesión en cis-test-instance, Bob:
1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona **Tony**, a quien desea proporcionar acceso
1. Selecciona **`bob.com`**
1. Selecciona el rol **Gestor**
1. Marca todos los recuadros de Ámbito funcional de CIS
1. Pulsa en **crear política**

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Lector
Después de iniciar sesión en cis-test-instance, Bob:
1. Pulsa en el separador **Cuenta> Acceso** en la barra de navegación
1. Selecciona **Tony**, a quien desea proporcionar acceso
1. Selecciona **`bob.com`**
1. Selecciona el rol **Lector**
  1. Todos los recuadros están preseleccionados para indicar que el usuario necesita acceso de lectura *min* al dominio completo y que no se puede dar acceso parcial a un dominio
1. Pulsa en **crear política**


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### Nivel de instancia - todos los dominios
{:#iam-and-cis-scenarios-instance-level}

Esta política se debe crear y gestionar a través de la página de gestión de IAM.

El acceso a nivel de instancia significa que, de las 10 instancias existentes, Bob puede otorgar a Tony permiso para la Instancia 1.
Tony podrá ver todos los dominios en esta instancia. 

Si Bob desea dar acceso de Escritor o Gestor a lo siguiente, tiene que dar acceso de nivel de instancia:
* Equilibrador de carga - agrupaciones y comprobaciones de estado
* Reglas de acceso de cortafuegos
* Trabajadores 

En la página Gestionar IAM, cree una política de escritor/gestor en la instancia de servicio cis-test-instancia.

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
or
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## Gestionar políticas de IAM 
{:#manage-iam-policies}

CIS permite a los usuarios crear políticas de IAM, pero la gestión se debe realizar a través de la [página de IAM](
https://{DomainName}/iam#/overview).

## Nota
{:#iam-note}
Por cada política creada en la página Acceso en la instancia de CIS, se crearán 2-3 políticas a su vez.

1. El rol de visor de Plataforma de la instancia de servicio permite al usuario añadido ver la instancia en el panel de instrumentos.

**Ejemplo**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. El acceso de lectura a nivel de dominio es el requisito mínimo para un acceso detallado al trabajo.

**Ejemplo**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. La política que ha creado con el tipo de configuración presente.

**Ejemplo**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**Preguntas más frecuentes**
1. ¿Cómo obtengo mi ID de instancia de servicio?

   Copie la CRN en la página de visión general
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   La última parte de la CRN es la instancia de servicio: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.
   
   o
   
   Pulse en la fila que contiene la instancia de CIS en la página principal de la lista de recursos y copie el GUID para el ID de la instancia de servicio.

2. ¡He borrado una política, pero el usuario al cual otorgué la política todavía puede llevar a cabo esa acción!

   CIS almacena en la memoria caché los resultados de la autorización, y el TTL de la memoria caché es de 10 minutos.  
   
   Cuando IAM autoriza, utiliza las políticas de acceso del grupo de acceso y de las propias políticas del usuario antes de tomar una decisión.

3. ¿Qué permisos son necesarios para suministrar servicios de Internet?

   Si no puede crear un recurso y añadirlo a un grupo de recursos, es muy probable que se trate de un problema de acceso. Debe tener, como mínimo, el rol Visor en el propio grupo de recursos y, como mínimo, el rol Editor en el servicio de la cuenta. Puede ponerse en contacto con el administrador de la cuenta para verificar el acceso que tiene asignado en la cuenta. Consulte [Gestión del acceso a los recursos](/docs/iam?topic=iam-iammanidaccser) para obtener más información.
   
 
