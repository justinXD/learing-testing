# learing-testing
# 🧪 Testing Path: de cero a testing profesional con Python, TypeScript y AWS

Repositorio de aprendizaje práctico para dominar el **testing de software** con las herramientas estándar de la industria, aplicado a los escenarios que realmente aparecen en el trabajo diario: funciones de negocio, Lambdas, servicios AWS, infraestructura como código, APIs, interfaces web y sistemas con IA generativa.

> **Cómo se aprende aquí:** la IA actúa como maestro y mentor. Cada ejercicio se resuelve de forma guiada, con explicación detallada del código y un reto de mejora al final. La meta no es copiar soluciones, sino entender *por qué* una prueba está escrita de cierta manera y *qué riesgo* cubre.

---

## 📌 Propósito

El testing es una de las habilidades más demandadas y menos practicadas de forma deliberada. Este repo busca cerrar esa brecha con tres objetivos:

1. **Entender, no memorizar.** Cada concepto (mock, fixture, aserción, pirámide de pruebas) se explica con el problema que resuelve antes de usar la herramienta.
2. **Dominar dos ecosistemas en paralelo.** Cada concepto se ve en **Python (pytest)** y en **TypeScript (Jest)**. Los conceptos son los mismos; cambia la sintaxis y el ecosistema, y compararlos refuerza ambos.
3. **Probar lo que se encuentra en la vida real.** Los ejercicios son genéricos pero modelan casos comunes: cálculo de precios, validación de datos, handlers de Lambda, colas, tablas, stacks de CDK y agentes de IA.

Al terminar, la persona que recorra esta ruta debería poder:

- Diseñar una estrategia de pruebas razonable para un servicio nuevo.
- Escribir pruebas legibles, rápidas y que fallen por las razones correctas.
- Probar código y también **infraestructura** (CDK) sin desplegar nada.
- Probar sistemas **no deterministas** como agentes y flujos con LLM.
- Integrar todo en un pipeline de CI que proteja la calidad en cada cambio.

---

## 🧰 Herramientas

| Área | Python | TypeScript |
|---|---|---|
| Framework de pruebas | `pytest` | `jest` (con `ts-jest`) |
| Mocks y dobles | `unittest.mock`, `pytest-mock` | `jest.fn()`, `jest.mock()`, `jest.spyOn()` |
| Simular AWS | `moto` | `aws-sdk-client-mock` |
| Pruebas de infraestructura (CDK) | `aws_cdk.assertions` | `aws-cdk-lib/assertions` |
| Integración local | `LocalStack` | `LocalStack` |
| Pruebas de API | `httpx` / `requests` + `pytest` | `supertest` / `fetch` + `jest` |
| E2E | — | `Playwright` |
| Cobertura | `pytest-cov` | cobertura integrada de Jest |
| Mutation testing (opcional) | `mutmut` | `Stryker` |
| CI | GitHub Actions | GitHub Actions |

> Se eligen `pytest` y `jest` por ser los estándares más extendidos en vacantes y proyectos reales. El E2E se concentra en TypeScript porque Playwright es la opción con mejor soporte en ese ecosistema.

---

## 🗂️ Estructura del repositorio

```
.
├── README.md
├── python/
│   ├── requirements-dev.txt
│   ├── pytest.ini
│   ├── src/                 # Código bajo prueba
│   ├── tests/               # Pruebas con pytest
│   └── exercises/           # Un directorio por ejercicio
├── typescript/
│   ├── package.json
│   ├── tsconfig.json
│   ├── jest.config.js
│   ├── src/                 # Código bajo prueba
│   ├── tests/               # Pruebas con Jest
│   └── exercises/
├── cdk/                     # Constructs y stacks de ejemplo + sus pruebas (Fase 4)
├── e2e/                     # Pruebas Playwright (Fase 7)
├── docs/
│   └── notas/               # Aprendizajes, errores comunes y decisiones
└── .github/workflows/       # Pipelines de CI (Fase 9)
```

> La estructura es una guía y puede evolucionar. Lo importante es que cada ejercicio tenga su código, sus pruebas y una nota breve de lo aprendido.

---

## 🔁 Dinámica de cada ejercicio

Para que el avance sea real y no solo "ver código":

1. **Planteamiento:** un caso realista y el riesgo que se quiere cubrir.
2. **Implementación guiada** en Python y en TypeScript.
3. **Explicación línea por línea** de las decisiones: qué se prueba, qué se simula y por qué.
4. **Reto de mejora:** una variación que obliga a aplicar el concepto sin ayuda directa.
5. **Registro:** se marca el ejercicio como completo y se anota lo aprendido en `docs/notas/`.

---

## 🛣️ Ruta de aprendizaje

> Ruta tentativa. Puede ajustarse según el avance y los temas que surjan por el camino.

### Fase 0: Preparación del entorno
- Entorno virtual de Python, `pytest` y `pytest-cov`.
- Proyecto Node con TypeScript, `jest` y `ts-jest`.
- Cómo ejecutar, filtrar y leer los resultados de las pruebas en ambos lenguajes.
- **Meta:** una prueba trivial pasando en cada ecosistema.
- 👉 Guía paso a paso para macOS, Linux y Windows en la sección **«Fase 0: configuración del entorno»** más abajo.

### Fase 1: Fundamentos de unit testing
- Anatomía de una prueba: **Arrange, Act, Assert**.
- Aserciones, excepciones esperadas y casos límite.
- Fixtures (`pytest`) y `beforeEach` / `afterEach` (Jest).
- Parametrización de casos: `@pytest.mark.parametrize` y `test.each`.
- Introducción a TDD: rojo, verde, refactor.
- **Casos reales:** validación de datos de entrada, cálculo de descuentos e impuestos, normalización de textos.

### Fase 2: Dobles de prueba y código asíncrono
- Diferencia entre **mock, stub, spy y fake**, y cuándo usar cada uno.
- Aislar dependencias externas (HTTP, reloj, aleatoriedad).
- Pruebas de código asíncrono (`async/await`, promesas, corrutinas).
- Errores comunes: sobre-mockear, probar la implementación en lugar del comportamiento.
- **Casos reales:** cliente de un API externo con reintentos, servicio que depende de la hora actual.

### Fase 3: Testing de código real en AWS
- Pruebas de **handlers de Lambda** (eventos de entrada, respuestas, errores).
- Simular **DynamoDB, S3 y SQS** con `moto` y `aws-sdk-client-mock`.
- Manejo de credenciales y regiones en pruebas para que nunca toquen recursos reales.
- **Casos reales:** procesamiento de mensajes de una cola, escritura idempotente en una tabla, generación de URLs prefirmadas.

### Fase 4: Testing de infraestructura con AWS CDK
- Pruebas de **constructs y stacks** sin desplegar: `Template.fromStack`, `hasResourceProperties`, `Match`.
- **Snapshot tests** y cuándo ayudan o estorban.
- Validar reglas de seguridad y buenas prácticas: permisos mínimos en IAM, cifrado, acceso público bloqueado.
- **Casos reales:** un bucket seguro reutilizable, una Lambda con su cola y alarmas, un stack con parámetros por ambiente.

### Fase 5: Pruebas de integración
- Qué es una prueba de integración y qué no.
- **LocalStack** para ejecutar servicios AWS en local.
- Flujos con varios componentes: Lambda, cola y tabla trabajando juntos.
- Introducción a **contract testing** entre servicios.
- **Casos reales:** pipeline de eventos desde la entrada hasta la persistencia.

### Fase 6: Pruebas de API
- Probar endpoints: códigos de estado, esquemas, autenticación y errores.
- Datos de prueba y limpieza entre ejecuciones.
- Validación de contratos de respuesta.
- **Casos reales:** CRUD de recursos, paginación, manejo de límites de uso.

### Fase 7: End-to-End con Playwright (TypeScript)
- Selectores robustos y **Page Object Model**.
- Esperas automáticas, manejo de pruebas inestables (*flaky*).
- Autenticación reutilizable, capturas, videos y trazas para depurar.
- **Casos reales:** flujo de registro e inicio de sesión, carrito de compras y checkout.

### Fase 8: Testing de agentes y sistemas con IA generativa
- Por qué probar sistemas **no deterministas** exige otra mentalidad.
- Simular el modelo (por ejemplo Bedrock) para pruebas rápidas y repetibles.
- Probar **herramientas (tools)** de un agente de forma aislada y las decisiones de orquestación.
- Evaluaciones (*evals*): conjuntos de casos, métricas, LLM-as-judge y pruebas de regresión de prompts.
- Guardrails: verificar que el sistema rechaza lo que debe rechazar.
- **Casos reales:** un agente con herramientas que debe respetar reglas de negocio.

### Fase 9: Calidad continua y CI
- Cobertura: qué mide, qué no mide y por qué el 100 % no es la meta.
- Mutation testing para evaluar la calidad real de las pruebas.
- **GitHub Actions:** ejecutar pruebas de ambos lenguajes en cada *pull request*.
- Pre-commit hooks, tiempos de ejecución y estrategia para pruebas lentas o inestables.

### Fase 10: Proyecto integrador
- Un servicio serverless pequeño de punta a punta con:
  unit tests, pruebas con AWS simulado, pruebas del stack CDK, pruebas de API, un flujo E2E, evals para su componente de IA y CI completo.
- Documentación de la estrategia de pruebas elegida y por qué.

---

## ✅ Seguimiento de progreso

- [ ] Fase 0: Preparación del entorno
- [ ] Fase 1: Fundamentos de unit testing
- [ ] Fase 2: Dobles de prueba y código asíncrono
- [ ] Fase 3: Testing de código real en AWS
- [ ] Fase 4: Testing de infraestructura con CDK
- [ ] Fase 5: Pruebas de integración
- [ ] Fase 6: Pruebas de API
- [ ] Fase 7: End-to-End con Playwright
- [ ] Fase 8: Testing de agentes y GenAI
- [ ] Fase 9: Calidad continua y CI
- [ ] Fase 10: Proyecto integrador

---

## 🧭 Principios que guían el repo

- **Una buena prueba cuenta una historia:** su nombre debe describir el comportamiento esperado.
- **Probar comportamiento, no implementación:** si refactorizar sin cambiar el resultado rompe pruebas, algo está mal.
- **Pirámide de pruebas:** muchas pruebas unitarias rápidas, algunas de integración, pocas E2E.
- **Una prueba que nunca falla no protege nada:** se practica ver fallar la prueba antes de hacerla pasar.
- **Las pruebas son código de producción:** se revisan, se refactorizan y se mantienen.
- **Nada de recursos reales en pruebas unitarias:** rápidas, aisladas y repetibles.

---

## ⚙️ Fase 0: configuración del entorno

Guía paso a paso para dejar todo listo en **macOS, Linux y Windows**. Al terminar tendrás una prueba pasando en Python (`pytest`) y otra en TypeScript (`jest`).

### 1. Requisitos

| Herramienta | Versión | Para qué se usa |
|---|---|---|
| Git | Cualquier versión reciente | Clonar y versionar el repositorio |
| Python | 3.10 o superior (recomendado 3.12) | `pytest`, `moto`, CDK en Python |
| Node.js + npm | LTS vigente (v22 o superior) | `jest`, TypeScript, Playwright |
| Editor | VS Code (opcional, recomendado) | Escribir y depurar pruebas |

> Más adelante se necesitarán **AWS CLI** (Fase 3), **Docker** (Fase 5) y los navegadores de **Playwright** (Fase 7). No hace falta instalarlos todavía.

### 2. Instalar las herramientas base

<details>
<summary><b>🍎 macOS</b></summary>

```bash
# 1) Herramientas de línea de comandos de Apple
xcode-select --install

# 2) Instala Homebrew copiando el comando oficial de https://brew.sh
#    Al terminar, ejecuta los comandos que el instalador te indique
#    para agregar brew al PATH (en Apple Silicon suele ser:)
eval "$(/opt/homebrew/bin/brew shellenv)"

# 3) Git, Python y Node
brew install git python node
```

</details>

<details>
<summary><b>🪟 Windows 10/11</b></summary>

Abre **PowerShell** o **Windows Terminal** y ejecuta:

```powershell
winget install --id Git.Git -e
winget install --id Python.Python.3.12 -e
winget install --id OpenJS.NodeJS.LTS -e
```

**Cierra y vuelve a abrir la terminal** para que se actualice el PATH.

> En Windows, Python se invoca con el lanzador `py` (por ejemplo `py --version`).
>
> **Opcional pero recomendado para fases posteriores:** instala WSL2 con `wsl --install`. Dentro de WSL sigue las instrucciones de Linux. Facilita el uso de Docker y LocalStack más adelante.

</details>

<details>
<summary><b>🐧 Linux</b></summary>

**Debian / Ubuntu**

```bash
sudo apt update
sudo apt install -y git python3 python3-venv python3-pip curl
```

**Fedora**

```bash
sudo dnf install -y git python3 python3-pip curl
```

**Arch**

```bash
sudo pacman -S --needed git python python-pip curl
```

**Node.js (todas las distribuciones, con nvm)**

```bash
# 1) Instala nvm siguiendo las instrucciones oficiales:
#    https://github.com/nvm-sh/nvm
# 2) Abre una terminal nueva y ejecuta:
nvm install --lts
```

</details>

### 3. Verifica las versiones

```bash
git --version
python3 --version    # En Windows: py --version
node --version
npm --version
```

### 4. Clona el repositorio

```bash
git clone <URL-DEL-REPOSITORIO>
cd <nombre-del-repositorio>
```

### 5. Configura Python (pytest)

Desde la carpeta `python/`:

```bash
cd python
```

**Crea y activa el entorno virtual** (el comando cambia según el sistema):

| Paso | macOS / Linux | Windows (PowerShell) | Windows (cmd) |
|---|---|---|---|
| Crear | `python3 -m venv .venv` | `py -m venv .venv` | `py -m venv .venv` |
| Activar | `source .venv/bin/activate` | `.venv\Scripts\Activate.ps1` | `.venv\Scripts\activate.bat` |

Sabrás que está activo porque la terminal mostrará `(.venv)` al inicio de la línea. Para salir del entorno, ejecuta `deactivate`.

**Instala las dependencias** (igual en todos los sistemas, con el entorno activo):

```bash
python -m pip install --upgrade pip
pip install -r requirements-dev.txt
```

Contenido de `python/requirements-dev.txt`:

```text
pytest
pytest-cov
```

Contenido de `python/pytest.ini`:

```ini
[pytest]
testpaths = tests
pythonpath = src
```

**Prueba de humo.** Crea `python/tests/test_smoke.py`:

```python
def test_entorno_funciona():
    assert 1 + 1 == 2
```

Ejecútala:

```bash
pytest -v
```

Resultado esperado: `1 passed`.

### 6. Configura TypeScript (Jest)

Desde la carpeta `typescript/`:

```bash
cd ../typescript    # Si vienes de python/. Si no: cd typescript
```

Si el repo ya incluye `package.json`, basta con:

```bash
npm install
```

Si estás creando el proyecto desde cero:

```bash
npm init -y
npm install --save-dev typescript jest ts-jest
npx tsc --init
npx ts-jest config:init
npm pkg set scripts.test="jest"
```

**Prueba de humo.** Crea `typescript/tests/smoke.test.ts`:

```typescript
import { test, expect } from '@jest/globals';

test('el entorno funciona', () => {
  expect(1 + 1).toBe(2);
});
```

> Se importa desde `@jest/globals` para no depender de tipos globales adicionales y que funcione igual en cualquier configuración de TypeScript.

Ejecútala:

```bash
npm test
```

Resultado esperado: `1 passed`.

### 7. `.gitignore` recomendado

En la raíz del repo:

```text
.venv/
__pycache__/
.pytest_cache/
.coverage
htmlcov/
node_modules/
coverage/
```

### 8. Checklist de verificación

- [ ] `git`, `python`, `node` y `npm` responden con su versión.
- [ ] El entorno virtual de Python se activa y muestra `(.venv)`.
- [ ] `pytest -v` termina con `1 passed`.
- [ ] `npm test` termina con `1 passed`.
- [ ] Los archivos `.venv/` y `node_modules/` no aparecen en `git status`.

### 9. Problemas frecuentes

| Síntoma | Sistema | Solución |
|---|---|---|
| `python3: command not found` | Windows | Usa `py` en lugar de `python3`. |
| `py` o `node` no se reconocen | Windows | Cierra y reabre la terminal; si persiste, reinstala asegurando que se agregue al PATH. |
| La activación del venv está bloqueada ("running scripts is disabled") | Windows (PowerShell) | `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned` y vuelve a intentar. |
| `ensurepip is not available` al crear el venv | Debian / Ubuntu | `sudo apt install python3-venv`. |
| `brew: command not found` | macOS | Ejecuta el comando `eval "$(/opt/homebrew/bin/brew shellenv)"` que muestra el instalador y reabre la terminal. |
| `EACCES` al instalar paquetes con npm | macOS / Linux | No uses `sudo`; instala Node con `nvm` o `brew`. |
| `pytest: command not found` | Todos | El entorno virtual no está activo; actívalo de nuevo. |
| `Cannot find name 'test'` en Jest | Todos | Importa `test` y `expect` desde `@jest/globals`. |

---

## 🚀 Ejecutar las pruebas (día a día)

Con el entorno ya configurado (ver la sección **«Fase 0: configuración del entorno»**):

```bash
# Python (con el entorno virtual activo)
cd python
pytest -v --cov

# TypeScript
cd typescript
npm test
```

---

## 🤝 Contexto

Este repositorio documenta un proceso de aprendizaje real y es parte de una trayectoria enfocada en ingeniería de IA y nube en AWS. Si recorres la ruta por tu cuenta, usa la IA de la misma forma: pídele que te explique, que te rete y que te haga preguntas, no solo que te dé la respuesta.
