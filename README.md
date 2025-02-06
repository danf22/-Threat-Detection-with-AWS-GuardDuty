
<img width="924" alt="architecture-complete (5)" src="https://github.com/user-attachments/assets/fb589ba6-0d48-45fb-bd2e-d8de638e62e6" />

# Threat Detection with AWS GuardDuty

Este proyecto tiene como objetivo proporcionar una comprensión práctica de la detección de amenazas en la nube utilizando **Amazon GuardDuty**. A través de un ejercicio práctico, se despliega una aplicación web vulnerable, se simulan ataques y luego se utiliza **Amazon GuardDuty** para detectar esas amenazas. Es una manera excelente de aprender a detectar amenazas en un entorno en la nube.

## Conceptos clave

- **Amazon GuardDuty**
- **Amazon CloudFront**
- **Amazon S3**
- **AWS CloudFormation**
- **OWASP Juice Shop**

## Objetivos del proyecto

El proyecto tiene como objetivo proporcionar una comprensión práctica sobre la seguridad en la nube y la detección de amenazas mediante los siguientes pasos:

1. **Aprender haciendo:** Actuar como atacante y defensor para comprender cómo se detectan y explotan las vulnerabilidades en un entorno controlado.
2. **Uso de una aplicación web vulnerable:** Se utiliza **OWASP Juice Shop**, una aplicación web deliberadamente vulnerable, para simular ataques.
3. **Simulación de ataques comunes:**
   - **Inyección SQL**
   - **Inyección de comandos**
   - **Exfiltración de datos**

## Instrucciones para la implementación

### Requisitos

1. Tener una cuenta activa de AWS.
2. Conocimientos básicos sobre AWS y sus servicios (EC2, S3, CloudFormation, etc.).
3. Conocimiento básico de **OWASP Juice Shop** y las vulnerabilidades comunes.

### Despliegue de la infraestructura

El proyecto se despliega utilizando **AWS CloudFormation**, lo cual automatiza la creación de todos los recursos necesarios:

1. **VPC** para el entorno.
2. **Subredes y grupos de seguridad** para controlar el tráfico.
3. Una **instancia EC2** para alojar la aplicación Juice Shop.
4. Un **bucket de S3** para almacenar los datos.
5. **GuardDuty** para la detección continua de amenazas.

Puedes revisar la plantilla de CloudFormation para ver los recursos que se crean en AWS.

### Ataques simulados

#### 1. **Inyección SQL**
- Se ingresa una consulta SQL maliciosa en el campo de la contraseña para omitir la autenticación.
- Ejemplo de inyección: `' OR 1=1;--`.

#### 2. **Inyección de comandos**
- Se insertan comandos maliciosos en el campo de nombre de usuario, forzando al sistema a almacenar credenciales temporales de AWS en un archivo JSON público.
- Esto revela una vulnerabilidad en el manejo de las entradas por parte de la aplicación.

#### 3. **Exfiltración de datos**
- Se toman las credenciales robadas y se usa la CLI de AWS para acceder y copiar un archivo llamado **secret-information.txt** de un bucket de S3.

## Análisis con Amazon GuardDuty

**Amazon GuardDuty** monitorea continuamente el entorno en busca de actividades sospechosas. Después de simular los ataques, se utiliza GuardDuty para detectar los eventos y generar informes detallados que incluyen:

- Qué ocurrió
- Cuándo ocurrió
- Qué recursos fueron afectados

GuardDuty detecta las actividades inusuales, como el acceso no autorizado a los buckets de S3, y proporciona detalles importantes, como qué rol fue comprometido y qué acciones de API se ejecutaron.

### Detección de malware

Además de la detección de intrusiones, también se puede probar la detección de malware utilizando un archivo **EICAR**, que es un archivo de prueba de malware sintético. GuardDuty lo detecta inmediatamente como una amenaza.

## Limpieza del entorno

Es importante eliminar todos los recursos después de la prueba para evitar riesgos:

1. Eliminar la pila de **CloudFormation**.
2. Borrar el archivo de credenciales robadas.
3. Confirmar que el entorno esté limpio y que no queden recursos expuestos.

## Conclusión

Este proyecto resalta cómo una **mala validación de entradas** puede conducir a **filtraciones de datos**. Un atacante no necesita habilidades avanzadas para explotar vulnerabilidades como inyecciones SQL o de comandos. Con una validación de entradas deficiente, un atacante puede obtener acceso a recursos críticos y exfiltrar datos sensibles.

**Amazon GuardDuty** es una herramienta poderosa para la defensa, que utiliza **machine learning** para identificar amenazas en patrones de tráfico y registros. Aunque no puede detener todas las amenazas, es una excelente manera de detectar señales de alerta en tiempo real.

## Puntos clave para recordar

- **Usar sistemas seguros para hacer pruebas**, como OWASP Juice Shop.
- **Desplegar la infraestructura con código** para tener control total de los recursos.
- **Realizar ataques y documentar los pasos** que llevan a una brecha de seguridad.
- **Observar cómo responde GuardDuty** y verificar si detecta la intrusión.
- **Eliminar todos los recursos** después de la prueba para evitar riesgos.

Este proyecto te ayudará a comprender la **gestión de riesgos de seguridad** en un entorno de nube. Es importante realizar pruebas continuas, mantener las estrategias de seguridad actualizadas y explorar nuevos vectores de amenazas. Comenzar con un proyecto estructurado como este te permitirá entender mejor cómo defender un entorno de nube.

## Recursos adicionales

- [Documentación de AWS GuardDuty](https://aws.amazon.com/guardduty/)
- [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)
- [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
