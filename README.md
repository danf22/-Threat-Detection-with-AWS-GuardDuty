
<img width="924" alt="architecture-complete (5)" src="https://github.com/user-attachments/assets/fb589ba6-0d48-45fb-bd2e-d8de638e62e6" />

# -Threat-Detection-with-AWS-GuardDuty
Esa es la idea detrás del proyecto Detección de amenazas con GuardDuty. Es un ejercicio práctico donde despliego una aplicación web vulnerable, la ataco y luego uso Amazon GuardDuty para detectar esos ataques. El objetivo es obtener una comprensión práctica de la detección de amenazas. Si quiero aprender a detectar amenazas en un entorno en la nube, la mejor manera es simularlas yo mismo.

Trabajar con una aplicación web vulnerable es una forma efectiva de aprender sobre amenazas de seguridad. Hay un proyecto que involucra una aplicación llamada OWASP Juice Shop, que contiene múltiples vulnerabilidades. La idea es desplegarla en AWS y luego observar cómo Amazon GuardDuty detecta acciones sospechosas cuando se realizan ataques.

Conceptos clave
Amazon GuardDuty
Amazon CloudFront
Amazon S3
AWS CloudFormation
OWASP Juice Shop
Comencé utilizando una plantilla de AWS CloudFormation. La plantilla crea automáticamente los componentes subyacentes:

Una VPC para el entorno
Subredes y grupos de seguridad para el control del tráfico
Una instancia EC2 que aloja Juice Shop
Un bucket de S3 para almacenar datos
GuardDuty para la detección continua de amenazas
CloudFormation ayuda a evitar la configuración manual. Se puede revisar la plantilla para ver todos los recursos que AWS creará.

Principales ideas del proyecto
Aprender haciendo

La mejor manera de entender la ciberseguridad es practicarla. En este proyecto, actúo como atacante y defensor. Explotar vulnerabilidades en un entorno controlado y luego analizar cómo se detectan esas amenazas proporciona una perspectiva invaluable.

Uso de una aplicación web vulnerable

El proyecto utiliza OWASP Juice Shop, una aplicación web creada con vulnerabilidades intencionales. Está diseñada para que los profesionales de seguridad puedan practicar la explotación de fallos sin causar daño real. Se despliega con AWS CloudFormation, que automatiza la configuración de la infraestructura.

Simulación de ataques comunes

Se simulan tres tipos de ataques:

Inyección SQL: Omitiendo la autenticación mediante código SQL malicioso.
Inyección de comandos: Ejecutando comandos maliciosos en el servidor web.
Exfiltración de datos: Robando información confidencial de un bucket de S3.
Análisis de resultados con GuardDuty
Amazon GuardDuty es un servicio basado en machine learning que supervisa el entorno AWS en busca de actividades sospechosas. Después de simular los ataques, uso GuardDuty para detectarlos. El servicio proporciona hallazgos detallados, como qué ocurrió, cuándo y qué recursos se vieron afectados.

Ejemplo de ataques y detección

Inyección SQL
La aplicación tiene una página de inicio de sesión con un campo de correo electrónico y contraseña.
Se usa una consulta maliciosa como: ' OR 1=1;-- en el campo de contraseña para omitir la autenticación.
Esto manipula la lógica de la consulta y permite acceso no autorizado.
Inyección de comandos
Se ingresan comandos maliciosos en el campo de nombre de usuario.
Estos comandos fuerzan al sistema a almacenar credenciales temporales de AWS en un archivo JSON público.
Esto revela una vulnerabilidad en la validación de entrada de la aplicación.
Exfiltración de datos
Se usan las credenciales robadas para crear un perfil en la CLI de AWS.
Luego, se copia un archivo "secret-information.txt" de un bucket de S3.
Esto confirma que el atacante puede acceder y extraer datos sensibles.
¿Cómo responde GuardDuty?
GuardDuty supervisa el entorno en tiempo real y reporta eventos sospechosos en aproximadamente 15 minutos. En este caso, marcó la actividad inusual en S3, mostrando qué rol fue comprometido y qué acciones de API se ejecutaron.

Otra prueba interesante es la protección contra malware de GuardDuty. Para probarla, se puede subir un archivo EICAR, que es un malware de prueba inofensivo. GuardDuty lo detecta inmediatamente y registra un nuevo hallazgo.
