# Plataforma de Gestión de Acompañamiento Estudiantil - Backend

## 📋 Descripción

Esta es la API REST backend para la Plataforma de Gestión de Acompañamiento Estudiantil (PIGAE), desarrollada con JSON Server. La plataforma permite:

- **DOCENTES**: Gestionar materias, grupos, registrar notas, asistencias y necesidades de estudiantes
- **ESTUDIANTES**: Gestionar su perfil, habilidades y consultar su información académica
- **FAMILIARES**: Consultar información autorizada del estudiante vinculado (solo lectura)
- **PROFESIONALES**: Realizar seguimiento a las necesidades estudiantiles

## 🚀 Tecnologías Utilizadas

- **JSON Server** v1.0.0-beta.3 - Mock REST API basado en archivo JSON
- **Node.js** - Entorno de ejecución

## 📁 Estructura del Proyecto

```
plataforma-gestion-acompanamiento-estudiantil-back/
├── database.json       # Base de datos JSON con todos los endpoints
├── package.json        # Configuración del proyecto y dependencias
├── README.MD          # Documentación del proyecto
└── public/            # Archivos estáticos (si es necesario)
```

## 🛠️ Instalación y Configuración

### Prerrequisitos
- Node.js (versión 14 o superior)
- npm o yarn

### Pasos de instalación

1. **Clonar el repositorio**
   ```bash
   git clone <url-del-repositorio>
   cd plataforma-gestion-acompanamiento-estudiantil-back
   ```

2. **Instalar dependencias**
   ```bash
   npm install
   ```

3. **Ejecutar el servidor**
   ```bash
   npm start
   ```

El servidor se ejecutará en `http://localhost:3000`

## 📊 Modelo de Datos

### Usuarios
```json
{
  "id": 101,
  "nombre": "Jaime Zapata",
  "correo": "jaime.zapata@cesde.edu.co",
  "rol": "DOCENTE", // DOCENTE | ESTUDIANTE | FAMILIAR
  "estado": "ACTIVO"  // ACTIVO | INACTIVO
}
```

### Estudiantes
```json
{
  "id": 202,
  "usuario_id": 102,
  "programa": "Desarrollo de Software",
  "semestre": 5
}
```

### Docentes
```json
{
  "id": 301,
  "usuario_id": 101,
  "especialidad": "Front-end",
  "departamento": "Sistemas"
}
```

### Familiares
```json
{
  "id": 403,
  "usuario_id": 103,
  "parentesco": "Padre",
  "telefono": "3001234567"
}
```

### Perfiles
```json
{
  "id": 501,
  "estudiante_id": 202,
  "resumen": "Desarrolladora Front-end junior.",
  "intereses": "UX/UI, Open Source"
}
```

### Habilidades
```json
{
  "id": 601,
  "perfil_id": 501,
  "nombre": "React JS",
  "nivel": "Avanzado", // Básico | Intermedio | Avanzado
  "tipo": "técnica"     // técnica | blanda
}
```

### Vínculos Familiares
```json
{
  "id": 901,
  "familiar_id": 403,
  "estudiante_id": 202,
  "autorizado": true
}
```

### Materias
```json
{
  "id": 1001,
  "nombre": "Desarrollo Front-end",
  "codigo": "FE001",
  "docente_id": 301
}
```

### Grupos
```json
{
  "id": 1101,
  "nombre": "G5-A",
  "materia_id": 1001,
  "semestre": 5
}
```

### Notas
```json
{
  "id": 1201,
  "valor": 4.5,
  "tipoEvaluacion": "Parcial",
  "estudiante_id": 202,
  "materia_id": 1001,
  "grupo_id": 1101
}
```
**Nota**: Solo los docentes pueden crear/editar notas.

### Asistencias
```json
{
  "id": 1301,
  "fecha": "2024-09-05",
  "estado": "PRESENTE", // PRESENTE | AUSENTE | TARDANZA
  "estudiante_id": 202,
  "grupo_id": 1101
}
```
**Nota**: Solo los docentes pueden registrar asistencias.

### Necesidades
```json
{
  "id": 1501,
  "tipo": "ACADÉMICO",    // ACADÉMICO | EMOCIONAL | ECONÓMICO
  "descripcion": "Dificultad en Spring Boot.",
  "estudiante_id": 202,
  "estado": "EN ATENCIÓN" // PENDIENTE | EN ATENCIÓN | RESUELTA
}
```

### Profesionales
```json
{
  "id": 1401,
  "nombre": "Maria Elena",
  "area": "Psicología"
}
```

### Seguimientos
```json
{
  "id": 1601,
  "necesidad_id": 1501,
  "fecha": "2024-09-17",
  "descripcion": "Primera sesión de tutoría."
}
```

### Categorías de Necesidad
```json
{
  "id": 1801,
  "nombre": "Emocional"
}
```

### Accesos Familiares
```json
{
  "id": 1701,
  "familiar_id": 403,
  "fecha_acceso": "2024-09-25T18:30:00Z",
  "accion_realizada": "Consulta de notas"
}
```

## 🔗 Endpoints de la API

### Base URL
```
http://localhost:3000
```

### Usuarios
- `GET /usuarios` - Obtener todos los usuarios
- `GET /usuarios/:id` - Obtener usuario por ID
- `POST /usuarios` - Crear nuevo usuario
- `PUT /usuarios/:id` - Actualizar usuario
- `DELETE /usuarios/:id` - Eliminar usuario

### Estudiantes
- `GET /estudiantes` - Obtener todos los estudiantes
- `GET /estudiantes/:id` - Obtener estudiante por ID
- `GET /estudiantes?usuario_id=:id` - Obtener estudiante por usuario
- `POST /estudiantes` - Crear nuevo estudiante
- `PUT /estudiantes/:id` - Actualizar estudiante
- `DELETE /estudiantes/:id` - Eliminar estudiante

### Docentes
- `GET /docentes` - Obtener todos los docentes
- `GET /docentes/:id` - Obtener docente por ID
- `GET /docentes?usuario_id=:id` - Obtener docente por usuario
- `POST /docentes` - Crear nuevo docente
- `PUT /docentes/:id` - Actualizar docente
- `DELETE /docentes/:id` - Eliminar docente

### Familiares
- `GET /familiares` - Obtener todos los familiares
- `GET /familiares/:id` - Obtener familiar por ID
- `POST /familiares` - Crear nuevo familiar
- `PUT /familiares/:id` - Actualizar familiar
- `DELETE /familiares/:id` - Eliminar familiar

### Perfiles
- `GET /perfiles` - Obtener todos los perfiles
- `GET /perfiles/:id` - Obtener perfil por ID
- `GET /perfiles?estudiante_id=:id` - Obtener perfil de un estudiante
- `POST /perfiles` - Crear nuevo perfil (solo estudiantes)
- `PUT /perfiles/:id` - Actualizar perfil (solo el propio estudiante)
- `DELETE /perfiles/:id` - Eliminar perfil

### Habilidades
- `GET /habilidades` - Obtener todas las habilidades
- `GET /habilidades/:id` - Obtener habilidad por ID
- `GET /habilidades?perfil_id=:id` - Obtener habilidades de un perfil
- `POST /habilidades` - Crear nueva habilidad
- `PUT /habilidades/:id` - Actualizar habilidad
- `DELETE /habilidades/:id` - Eliminar habilidad

### Vínculos
- `GET /vinculos` - Obtener todos los vínculos
- `GET /vinculos?familiar_id=:id` - Obtener vínculos de un familiar
- `GET /vinculos?estudiante_id=:id` - Obtener vínculos de un estudiante
- `POST /vinculos` - Crear nuevo vínculo
- `PUT /vinculos/:id` - Actualizar vínculo
- `DELETE /vinculos/:id` - Eliminar vínculo

### Materias
- `GET /materias` - Obtener todas las materias
- `GET /materias/:id` - Obtener materia por ID
- `GET /materias?docente_id=:id` - Obtener materias de un docente
- `POST /materias` - Crear nueva materia
- `PUT /materias/:id` - Actualizar materia
- `DELETE /materias/:id` - Eliminar materia

### Grupos
- `GET /grupos` - Obtener todos los grupos
- `GET /grupos/:id` - Obtener grupo por ID
- `GET /grupos?materia_id=:id` - Obtener grupos de una materia
- `POST /grupos` - Crear nuevo grupo
- `PUT /grupos/:id` - Actualizar grupo
- `DELETE /grupos/:id` - Eliminar grupo

### Notas
- `GET /notas` - Obtener todas las notas
- `GET /notas/:id` - Obtener nota por ID
- `GET /notas?estudiante_id=:id` - Obtener notas de un estudiante
- `GET /notas?materia_id=:id` - Obtener notas de una materia
- `POST /notas` - Crear nueva nota (solo docentes)
- `PUT /notas/:id` - Actualizar nota (solo docentes)
- `DELETE /notas/:id` - Eliminar nota

### Asistencias
- `GET /asistencias` - Obtener todas las asistencias
- `GET /asistencias/:id` - Obtener asistencia por ID
- `GET /asistencias?estudiante_id=:id` - Obtener asistencias de un estudiante
- `GET /asistencias?grupo_id=:id` - Obtener asistencias de un grupo
- `POST /asistencias` - Crear nueva asistencia (solo docentes)
- `PUT /asistencias/:id` - Actualizar asistencia (solo docentes)
- `DELETE /asistencias/:id` - Eliminar asistencia

### Necesidades
- `GET /necesidades` - Obtener todas las necesidades
- `GET /necesidades/:id` - Obtener necesidad por ID
- `GET /necesidades?estudiante_id=:id` - Obtener necesidades de un estudiante
- `POST /necesidades` - Crear nueva necesidad
- `PUT /necesidades/:id` - Actualizar necesidad
- `DELETE /necesidades/:id` - Eliminar necesidad

### Profesionales
- `GET /profesionales` - Obtener todos los profesionales
- `GET /profesionales/:id` - Obtener profesional por ID
- `POST /profesionales` - Crear nuevo profesional
- `PUT /profesionales/:id` - Actualizar profesional
- `DELETE /profesionales/:id` - Eliminar profesional

### Seguimientos
- `GET /seguimientos` - Obtener todos los seguimientos
- `GET /seguimientos/:id` - Obtener seguimiento por ID
- `GET /seguimientos?necesidad_id=:id` - Obtener seguimientos de una necesidad
- `POST /seguimientos` - Crear nuevo seguimiento
- `PUT /seguimientos/:id` - Actualizar seguimiento
- `DELETE /seguimientos/:id` - Eliminar seguimiento

### Categorías de Necesidad
- `GET /categorias-necesidad` - Obtener todas las categorías
- `GET /categorias-necesidad/:id` - Obtener categoría por ID
- `POST /categorias-necesidad` - Crear nueva categoría
- `PUT /categorias-necesidad/:id` - Actualizar categoría
- `DELETE /categorias-necesidad/:id` - Eliminar categoría

### Accesos Familiares
- `GET /accesos_familiar` - Obtener todos los accesos
- `GET /accesos_familiar/:id` - Obtener acceso por ID
- `GET /accesos_familiar?familiar_id=:id` - Obtener accesos de un familiar
- `POST /accesos_familiar` - Registrar nuevo acceso
- `PUT /accesos_familiar/:id` - Actualizar acceso
- `DELETE /accesos_familiar/:id` - Eliminar acceso


### Estados de Entidades
- **Usuarios**: `ACTIVO`, `INACTIVO`
- **Asistencias**: `PRESENTE`, `AUSENTE`, `TARDANZA`
- **Necesidades**: `PENDIENTE`, `EN ATENCIÓN`, `RESUELTA`
- **Vínculos**: `autorizado: true/false`
- **Niveles de Habilidad**: `Básico`, `Intermedio`, `Avanzado`
- **Tipos de Habilidad**: `técnica`, `blanda`
- **Roles**: `DOCENTE`, `ESTUDIANTE`, `FAMILIAR`
- **Tipos de Necesidad**: `ACADÉMICO`, `EMOCIONAL`, `ECONÓMICO`
- **Categorías de Necesidad**: `Emocional`, `Académico`

## 🔧 Configuración Adicional

### Variables de Entorno
El proyecto utiliza la configuración por defecto de JSON Server. Para personalizar el puerto:

### CORS
JSON Server maneja automáticamente las políticas CORS para desarrollo.

## 📝 Scripts Disponibles

- `npm start` - Inicia el servidor JSON Server
- `npm install` - Instala las dependencias del proyecto

## 🤝 Contribución

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/NuevaCaracteristica`)
3. Commit tus cambios (`git commit -m 'Añadir nueva característica'`)
4. Push a la rama (`git push origin feature/NuevaCaracteristica`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## 👥 Autores

- **Jaime Zapata** - *Desarrollo inicial*

## 🏫 Institución

**Centro de Estudios de Sistemas y Desarrollo Empresarial (CESDE)**
Programa: Desarrollo de Software

---

*Este proyecto es parte del desarrollo de la Plataforma de Gestión de Acompañamiento Estudiantil para mejorar el seguimiento y apoyo a los estudiantes.*