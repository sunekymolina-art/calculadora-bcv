# calculadora-bcv (frontend)

Frontend de la Calculadora BCV: un solo archivo `index.html` (HTML/CSS/JS puro), desplegado en Vercel.
Usuario: perfil no técnico, trabaja en español, necesita pasos exactos para git y terminal (PowerShell: no usar `&&`).

## Entornos
- Producción: rama `main` -> https://calculadora-bcv-two.vercel.app (backend: bcv-rates-api-production.up.railway.app)
- Development: rama `dev` -> https://calculadora-bcv-git-dev-sunekymolina-arts-projects.vercel.app (backend: bcv-rates-api-development.up.railway.app)
- Al pasar de `dev` a `main`, cambiar la constante `API` al backend de producción.
- Probar local con `start index.html` (el login de Auth0 solo funciona desde las URLs de Vercel).

## Login
- Login propio: POST {API}/api/auth/login -> token en localStorage (`bcv_token`, `bcv_email`).
- Todos los fetch al backend llevan `Authorization: Bearer <token>`; si responde 401, limpiar token y volver al login.
- Tras el login debe llamarse a init() (hubo un bug: el calendario no funcionaba hasta refrescar; verificar que siga corregido).
- Usuarios beta se crean a mano en Auth0 (sign-ups deshabilitados).

## Funcionalidades
- Monedas Bs, USD, EUR, UVC; resultados de todas las monedas a la vez, con copiar número y copiar en letras (MAYÚSCULAS).
- Fórmulas: todo pasa por Bs (USD*dolar, EUR*euro, UVC*idi).
- Radio Bs digitales / soberanos (soberanos = monto / 1.000.000).
- Fecha: texto DD/MM/AAAA + calendario propio, fines de semana deshabilitados, manejo de feriados (404).
- Formato venezolano (1.000.000,00); punto o coma del teclado numérico = decimal.
- Acumulador con suma/resta (teclas + y -), historial en localStorage, sección Interés de Mora (capital * 16,80% / 360 * días, en USD).
- Línea de tasa por resultado y footer con las fechas en DD/MM/YYYY.