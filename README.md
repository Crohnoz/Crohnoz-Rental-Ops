# Sistema Administrativo de Arriendos

**Selected Engineering Case · Operational Administration System**

Aplicación React/Vite diseñada para digitalizar la administración cotidiana de edificios pequeños: departamentos, arrendatarios, cobros, abonos, vouchers, contratos, boletas y liquidaciones de salida.

Este repositorio funciona como **caso público sanitizado**. La demo utiliza información ficticia y la operación privada permanece separada mediante autenticación, base de datos y políticas de acceso.

## Problema operacional

La administración de arriendos pequeños suele terminar repartida entre planillas, documentos, comprobantes y cálculos manuales. El objetivo del sistema es convertir esas tareas en un flujo explícito, trazable y suficientemente simple para el trabajo diario.

## Qué demuestra

- modelado de departamentos, arrendatarios, cobros y pagos;
- emisión de vouchers con folio correlativo e impresión térmica;
- contratos, boletas y liquidaciones de salida;
- reglas de redondeo con compensación trazable en el cobro siguiente;
- alertas administrativas basadas en reglas;
- respaldo y restauración mediante JSON;
- separación estricta entre demostración pública y operación privada;
- autenticación y aislamiento de datos con Supabase Auth + RLS.

## Arquitectura de publicación

### Demo pública

```env
VITE_APP_MODE=demo
```

- Datos completamente ficticios para 23 departamentos.
- Todos los cambios permanecen en el navegador del visitante.
- Restauración inmediata del estado original de demostración.
- Sin conexión a la base de datos privada.

### Operación privada

```env
VITE_APP_MODE=private
VITE_SUPABASE_URL=https://PROYECTO.supabase.co
VITE_SUPABASE_ANON_KEY=CLAVE_ANON_PUBLICA
```

- Inicio de sesión obligatorio con Supabase Auth.
- Espacio de trabajo centralizado y sincronizado.
- Row Level Security para aislar los datos por propietario.
- Copia temporal de trabajo en `sessionStorage`.
- Los datos reales nunca forman parte del repositorio ni de la demo pública.

La configuración está documentada en [`docs/ENTORNOS_Y_SEGURIDAD.md`](docs/ENTORNOS_Y_SEGURIDAD.md).

## Regla contable de redondeo

El total calculado se redondea al múltiplo de $100 más cercano. La diferencia se registra con signo contrario como `ajusteSiguiente`, permitiendo compensarla en el próximo cobro sin perder trazabilidad.

## Stack

- React
- Vite
- JavaScript
- Supabase Auth
- PostgreSQL / Supabase
- Row Level Security
- Netlify

## Desarrollo local

```bash
cp .env.example .env
npm install
npm run dev
```

Build:

```bash
npm run build
```

## Límites actuales

La implementación privada actual utiliza un propietario por espacio de trabajo. La evolución multiusuario requiere organizaciones, membresías, roles, auditoría por usuario y mayor normalización del dominio.

Este repositorio no pretende exponer datos de clientes ni representar una plataforma SaaS multi-tenant terminada. Su valor público está en mostrar el **problema, las reglas operacionales, la separación de entornos y las decisiones de seguridad**.

## Crohnoz Labs

Parte del portfolio público de ingeniería de Crohnoz Labs.

**Problem → System → Evidence → Scale**

- Perfil y evidencia pública: https://github.com/Crohnoz
- Crohnoz Labs: https://crohnozlabs.cl
