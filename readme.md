# Actividad UD05.1 - Validación de XML con XSD y Expresiones Regulares

## Estructura del proyecto
- `usuarios.xml` - Documento XML con datos de 3 usuarios
- `usuarios.xsd` - Esquema XSD con todas las validaciones

## Restricciones implementadas

### 1. ID de usuario (atributo)
- Patrón: `U[0-9]{3}`
- Ejemplo: U001, U002, U003

### 2. Nombre de usuario
- **Expresión regular:** `[a-z][a-z0-9._]{3,19}`
- **Justificación:** Comienza con minúscula, permite minúsculas, números, punto y guion bajo.
- **Longitud:** 4-20 caracteres
- **Ejemplos:** maria.garcia, juan_perez, ana.martinez

### 3. Estructura XML
He optado por esta estructura porque utiliza un elemento raíz <usuarios> que contiene la colección completa de usuarios, lo que permite agrupar múltiples registros de forma lógica y escalable, facilitando la incorporación de nuevos usuarios en el futuro. Cada usuario está representado por un elemento <usuario> con un atributo id único, lo que permite identificar cada registro, siendo más apropiado usar un atributo en lugar de un elemento hijo para este propósito al tratarse de un metadato. Todos los datos personales aparecen como elementos anidados dentro de cada usuario, formando una jerarquía clara "un usuario tiene un nombre, un email, etc."

### 4. Email
- **Expresión regular:** Basada en RFC 5322
- **Justificación:** Sigue el estándar internacional para direcciones de correo
- **Caracteres permitidos:** a-z, 0-9, ! # $ % & ' * + - / = ? ^ _ ` { | } ~ . 
- **Ejemplos:** maria.garcia@email.com, juan.perez@empresa.es

### 5. Teléfono (España)
- **Expresión regular:** `(\+34|0034)?[6-9][0-9]{8}`
- **Justificación:** Formato español: prefijo opcional +34 o 0034, seguido de 9 dígitos (móviles empiezan por 6, 7; fijos por 8, 9)
- **Ejemplos:** +34612345678, 954123456, 935551122

### 6. Código Postal (España)
- **Expresión regular:** `[0-5][0-9]{4}`
- **Justificación:** Los códigos postales en España tienen 5 dígitos, el primero indica la provincia (0-5)
- **Ejemplos:** 28001 (Madrid), 41001 (Sevilla), 08001 (Barcelona)

### 7. Contraseña
- **Expresión regular:** `^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*()\-_=+]).{8,}$`
- **Justificación:** Cumple con los estándares de seguridad OWASP:
  - Mínimo 8 caracteres
  - Al menos una letra minúscula
  - Al menos una letra mayúscula
  - Al menos un número
  - Al menos un carácter especial (!@#$%^&*()-_=+)
- **Ejemplos:** Passw0rd!23, Secure#Pass99, Comp!exPwd777

## 8. Expresiones regulares diseñadas en regex101.com
Use https://regex101.com/ para comprobar todas las expresiones antes de implementarlas en el XSD