# Almacén Tito — Backend

Base de datos y lógica del servidor del sistema de inventario del almacén de don Tito, en [Supabase](https://supabase.com).
Las pantallas están en [almacen-tito-front](https://github.com/kndre7247-ship-it/almacen-tito-front).

## Qué hay aquí

```
supabase/
├── migrations/  Un archivo SQL por cada cambio en la base de datos, en orden
└── seed.sql     Datos iniciales (categorías, etc.)
```

Tablas, permisos por rol (RLS) y funciones se escriben **solo** en archivos de `migrations/`, nunca directo en el panel de Supabase.

## Ambientes

| Proyecto Supabase      | Project ID             | Para qué                             |
| ---------------------- | ---------------------- | ------------------------------------ |
| `almacen-tito-pruebas` | `iohcmehzmgypzgopvuga` | Probar cambios                       |
| `almacen-tito`         | `fukgtzjgjzkcekfcsnwj` | Producción, solo cambios ya probados |

La CLI queda vinculada siempre a **pruebas**. Para subir a producción se vincula temporalmente y luego se vuelve a pruebas.

## Requisitos

- [Node.js](https://nodejs.org) 20.19 o superior
- Cuenta en Supabase con acceso a la organización **Almacén Tito**

## Primera vez

```bash
npm install
npx supabase login
npx supabase link --project-ref iohcmehzmgypzgopvuga
```

## Comandos

Los comandos que hablan con la base de datos llevan **`--remote`**. Sin eso, la CLI busca un Supabase local en Docker, que no usamos.

| Comando                                | Qué hace                                            |
| -------------------------------------- | --------------------------------------------------- |
| `npx supabase migration new nombre`    | Crea un archivo de migración vacío con fecha y hora |
| `npx supabase migration list --remote` | Compara migraciones locales con las del proyecto    |
| `npx supabase db push --remote`        | Aplica las migraciones nuevas al proyecto vinculado |

## Forma de trabajo

**Ramas**

- `main`: producción
- `develop`: pruebas
- `feature/SCRUM-XX-nombre`: una por historia de Jira; sale de `develop` y vuelve a `develop`

**Commits**: prefijo según el tipo y la clave de Jira al final.

```
[BD] Tabla productos (SCRUM-59)
[Backend] Función registrar_merma (SCRUM-95)
```

Si una historia toca front y backend, se publica **primero el backend**.
