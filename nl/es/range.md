---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Rango
{:#cis-range}

La característica Rango ofrece protección de DDoS, equilibrio de carga y aceleración de contenido a cualquier protocolo basado en TCP. 
Rango es un Proxy TCP global que se ejecuta en nodos edge de CIS/Cloudflare. 

El Rango se puede utilizar para: 
* Proteger los puertos y protocolos TCP de los ataques de **DDoS de capa 3 y 4**. 
* Reducir la capacidad de los atacantes de espiar y robar datos confidenciales habilitando el **cifrado TLS**.
* Integrar con el cortafuegos de IP de CIS, lo que permite bloquear o presentar un desafío a las direcciones IP o a rangos IP enteros, cuando intentan alcanzar sus servicios TCP. 
* Configurar equilibradores de carga con comprobaciones de estado de TCP, migración tras error y políticas de dirección para dictar dónde debe fluir el tráfico.

## Cómo empezar con el Rango
{:#getting-started-with-range}

El Rango sólo está disponible para los clientes de Empresa con un coste adicional, y el precio es según el uso de ancho de banda.
{:note}

### Añadir una aplicación
{:#range-add-an-application}
Siga estos pasos para añadir una aplicación.

1. Vaya a **Seguridad > Rango**
1. Pulse el botón **Añadir aplicación** 
1. Especifique el nombre de la aplicación en el primer campo de entrada. La aplicación pasa a estar asociada con un nombre DNS en el dominio de CIS.
1. Especifique el puerto edge en el campo de entrada siguiente. Permaneceremos a la escucha de conexiones entrantes en estas direcciones de este puerto. Las conexiones a estas direcciones se redireccionan al origen. (La redirección por proxy está soportada en todos los puertos excepto en el puerto 21).
1. En la sección Origen, especifique la dirección IP y el puerto de origen de la aplicación TCP. También puede seleccionar un equilibrador de carga existente
1. Habilite el cortafuegos de IP. Cuando está habilitado, se aplican las reglas de cortafuegos con una acción de "bloqueo" o "lista blanca" para esta aplicación. Las reglas de país o basadas en el ASN todavía no están soportadas.
1. Habilite el protocolo proxy si tiene un proxy en línea que admita el protocolo PROXY v1. Esta característica es útil si está ejecutando un servicio que requiere conocimiento de la IP de cliente real. En la mayoría de los casos, este valor debe permanecer inhabilitado. 
1. Pulse **Suministro**

El protocolo proxy añade antes de cada conexión una cabecera que informa de la dirección IP y el puerto del cliente. Una cabecera de protocolo proxy tiene el formato: 
  * SERIE_PROXY + espacio + PROTOCOLO_INET + espacio + IP_CLIENTE + espacio + IP_PROXY + espacio + PUERTO_CLIENTE + espacio + PUERTO_PROXY + "\r\n"
  * A continuación, se muestra una línea de protocolo Proxy de ejemplo para una dirección IPv4
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * A continuación, se muestra una línea de protocolo Proxy de ejemplo para una dirección IPv6:
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
El suministro de una aplicación de Rango incurrirá en costes adicionales, en función de la cantidad de ancho de banda utilizado por app.
{:note}

La aplicación aparece ahora en un mosaico con las propiedades siguientes:
  * Nombre de aplicación
  * Puerto Edge
  * Origen y puerto
  * Conexiones desde la última hora (sondeado cada minuto)
  * Rendimiento desde la última hora (sondeado cada minuto)
  * El menú de desbordamiento (esquina superior derecha) permite lo siguiente 
    * Editar la aplicación
    * Ver métricas para la aplicación especificada
    * Suprimir la aplicación 
    
Cuando se crea una aplicación de Rango, se le asigna una dirección IPv4 y una dirección IPv6 exclusivas. Estas direcciones IP no son estáticas y pueden estar sujetas a cambios. Puede determinar la dirección IP asignada utilizando el DNS. El nombre DNS devolverá siempre la dirección IP asignada a la aplicación.     
    
### Ver métricas
{:#range-view-metrics}
Ahora su aplicación está lista para redirigir tráfico TCP a través de Cloudflare/CIS.

Vaya a **Métricas > Rango** para ver el número de conexiones a aplicaciones y el tráfico de rendimiento.
Los gráficos muestran métricas para un máximo de 10 aplicaciones. 
{:note}

Las métricas de aplicación se pueden conmutar mediante la tecla del gráfico o pulsando el botón **Seleccionar aplicaciones**. El marco de tiempo de datos Métricas se puede cambiar utilizando el menú desplegable.

## Mosaicos de app de Rango
{:#range-apptiles}
Después de crear unas cuantas app, la página **Seguridad > Rango** contendrá mosaicos de aplicaciones. Los mosaicos de aplicación contienen la información siguiente:
* Nombre de aplicación
* Puerto Edge
* Origen y puerto
* Conexiones desde la última hora (sondeado cada minuto)
* Rendimiento desde la última hora (sondeado cada minuto)


El mosaico de aplicación también contiene un menú de desbordamiento en la esquina superior (3 puntos). El menú de desbordamiento proporciona a los usuarios la opción de:
* editar la aplicación
* ver métricas para la aplicación especificada
  * esto lleva al usuario a la página **Métricas > Rango**, que muestra las métricas sólo para esa aplicación
* suprimir la aplicación


## Ejemplos de uso de la API
{:#range-api-usage-examples}
Éstos son ejemplos de cómo crear y listar aplicaciones utilizando Rango.

### Crear app de Rango
{:#create-range-app}
Hay dos maneras de designar un origen en una app de Rango
1. IP de origen - utilizando el parámetro `origin_direct`
2. Equilibrador de carga - utilizando los parámetros `origin_dns` y `origin_port`

**Solicitud:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**Respuesta:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Solicitud:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**Respuesta:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Nombre DNS:** la aplicación está asociada a un nombre DNS del dominio.

**Puerto de protocolo/edge:** el puerto donde se ejecuta la aplicación. Las conexiones a estas direcciones se redireccionan al origen.

**Origen directo:** es la IP donde se ejecuta la aplicación y el puerto por donde desea que fluya el tráfico desde el extremo hasta el origen.

**Cortafuegos de IP:** si está habilitado, se aplican las reglas de cortafuegos con una acción de bloqueo para esta aplicación de Rango.

**Protocolo PROXY:** habilítelo si tiene un proxy en línea que admita el protocolo PROXY v1. En la mayoría de los casos, este valor permanece inhabilitado.

**DNS de origen:** es el nombre del equilibrador de carga que desea establecer como origen.

**Puerto de origen:** es el puerto de su servicio. 

### Listar todas las apps
{:#range-list-all-apps}

**Solicitud:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**Respuesta:**
```
{
    "result": [
        {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### Listar una app de Rango específica
{:#range-list-a-specific-range-app}
**Solicitud:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**Respuesta:**
App que utiliza IP de origen
```
{
    "result": {
        "id": "4f70c3d4f20546b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
} 
```

App que utiliza un equilibrador de carga
```
{
    "result": {
        "id": "555359036e7f4acc82d69b916f62caba",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
            "name": "test_update"
        },
        "origin_port": 76,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-10T22:26:47.167008Z",
        "modified_on": "2019-01-10T22:26:47.167008Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}

```
