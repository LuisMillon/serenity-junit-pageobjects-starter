# ANÁLISIS DETALLADO - Serenity JUnit Page Objects Starter
**Proyecto de Automatización de Pruebas Web con Serenity BDD y JUnit 5**

---

## 📑 TABLA DE CONTENIDOS

1. [Descripción General](#descripción-general)
2. [Propósito y Objetivo](#propósito-y-objetivo)
3. [Stack Tecnológico](#stack-tecnológico)
4. [Arquitectura](#arquitectura)
5. [Estructura del Proyecto](#estructura-del-proyecto)
6. [Componentes Principales](#componentes-principales)
7. [Flujos de Ejecución](#flujos-de-ejecución)
8. [Configuración Detallada](#configuración-detallada)
9. [Reglas de Negocio](#reglas-de-negocio)
10. [Especificaciones Técnicas](#especificaciones-técnicas)
11. [Dependencias y Compatibilidades](#dependencias-y-compatibilidades)
12. [Constraints y Limitaciones](#constraints-y-limitaciones)
13. [Criterios de Aceptación](#criterios-de-aceptación)
14. [Guía de Ejecución](#guía-de-ejecución)

---

## 1. DESCRIPCIÓN GENERAL

### 1.1 Definición del Proyecto

**Serenity JUnit Page Objects Starter** es un proyecto de plantilla (starter template) para automatización de pruebas de aceptación funcionales web utilizando el framework **Serenity BDD** integrado con **JUnit 5**. 

El proyecto demuestra patrones modernos de automatización de tests implementando:
- **Page Object Pattern**: Encapsulación de elementos UI
- **Action/Steps Pattern**: Abstracción de acciones de usuario
- **Screenplay Pattern**: Patrón BDD más expresivo y legible

### 1.2 Contexto del Proyecto

- **Versión**: 1.0.0-SNAPSHOT
- **Tipo de Empaquetado**: JAR
- **Licencia**: Apache 2.0
- **Grupo Maven**: net.serenity-bdd.starter
- **Artifact ID**: serenity-junit-starter
- **Estatus**: Proyecto educational/starter para aprender automatización

### 1.3 Aplicación Under Test (AUT)

El proyecto automatiza pruebas contra **DuckDuckGo** (https://duckduckgo.com/):
- **URL Base**: https://duckduckgo.com/
- **Funcionalidad**: Motor de búsqueda web
- **Interacción**: Búsqueda de términos y validación de resultados

---

## 2. PROPÓSITO Y OBJETIVO

### 2.1 Objetivo Principal

Proporcionar una plantilla lista para usar (starter project) que demuestre cómo:
- Organizar tests de aceptación con Serenity BDD
- Implementar patrones de diseño en automatización (Page Objects, Steps)
- Ejecutar tests con JUnit 5 en Maven y Gradle
- Generar reportes automáticos de pruebas
- Configurar WebDriver para navegadores
- Integrar con sistemas CI/CD

### 2.2 Objetivos Secundarios

- Demostrar buenas prácticas de organización de código de tests
- Servir como base para proyectos más complejos
- Proporcionar ejemplos de configuración de Serenity BDD
- Mostrar integración con herramientas de build modernas

### 2.3 Audiencia Objetivo

- Desarrolladores de QA/Test
- Ingenieros de Automatización
- Equipos Ágiles que implementan Test-Driven Development
- Capacitadores en automatización de tests

---

## 3. STACK TECNOLÓGICO

### 3.1 Versiones Específicas

#### Framework de Automatización y Testing

| Componente | Versión | Scope | Propósito |
|-----------|---------|-------|----------|
| Serenity BDD Core | 4.0.15 | test | Motor principal de automatización |
| Serenity JUnit5 | 4.0.15 | test | Integración con JUnit 5 |
| Serenity Screenplay | 4.0.15 | test | Patrón Screenplay para tests expresivos |
| Serenity Ensure | 4.0.15 | test | Assertions fluidas integradas |
| Serenity WebDriver | 4.0.15 | test | Wrapper e inyección de Selenium |
| Serenity Gradle Plugin | 4.0.15 | build | Orquestación de tests en Gradle |

#### Testing Framework

| Componente | Versión | Scope | Propósito |
|-----------|---------|-------|----------|
| JUnit 5 (Jupiter API) | 5.10.0 | test | API de testing y annotations |
| JUnit 5 (Jupiter Engine) | 5.10.0 | test | Motor de ejecución de tests |
| AssertJ | 3.22.0-3.23.1 | test | Assertions fluidas y expresivas |

#### Utilidades

| Componente | Versión | Scope | Propósito |
|-----------|---------|-------|----------|
| Logback Classic | 1.2.11 | compile+test | Logging con SLF4J |
| SLF4J | 1.7.7 | compile | Abstracción de logging |
| Lombok | 1.18.24 | test | Reducción de boilerplate |

#### Herramientas de Build

| Herramienta | Versión | Propósito |
|-----------|---------|----------|
| Maven | 3.6+ | Build tool, gestión de dependencias |
| Gradle | 7.x+ | Build tool alternativo |
| Gradle Wrapper | Incluido | Asegurar consistencia de versión Gradle |
| Maven Wrapper | Incluido | Asegurar consistencia de versión Maven |

#### Plugins Build

**Maven Plugins:**
- Maven Surefire Plugin 3.1.2 - Ejecución de tests unitarios (deshabilitado)
- Maven Failsafe Plugin 3.1.2 - Ejecución de tests de integración/aceptación
- Serenity Maven Plugin (implícito) - Generación de reportes

**Gradle Plugins:**
- Serenity Gradle Plugin 4.0.15 - Orquestación y reportes
- Java Plugin - Compilación Java

### 3.2 Dependencias Transitivas Implícitas

A través de Serenity Core se incluyen:
- **Selenium WebDriver**: Automatización de navegador
- **WebDriver Manager**: Gestión automática de drivers
- **Hamcrest**: Matchers para assertions
- **Guice**: Inyección de dependencias

### 3.3 Java Version

- **Source Compatibility**: Java 16
- **Target Compatibility**: Java 16
- **Encoding**: UTF-8
- **Requisito Mínimo**: JDK 16 (OpenJDK o Oracle)

### 3.4 Navegador y WebDriver

- **Navegador**: Google Chrome (necesario instalado en el sistema)
- **Driver**: ChromeDriver (descargado automáticamente por WebDriver Manager)
- **Modo de Ejecución**: Headless (sin interfaz gráfica)
- **Resolución**: 1000x800 píxeles

### 3.5 Ambiente de Ejecución

- **OS Soportados**: Windows, macOS, Linux
- **Terminal**: PowerShell (Windows), bash (Unix)
- **Java Home**: Variable JAVA_HOME correctamente configurada

---

## 4. ARQUITECTURA

### 4.1 Arquitectura General en Capas

```
┌─────────────────────────────────────────────────────────────┐
│  CAPA DE TESTS (Test Classes)                               │
│  - WhenSearchingForTerms.java                              │
│  - WhenSearchingByKeyword.java                             │
│  [Orquestan flujo de comportamiento del usuario]           │
└──────────────┬──────────────────────────────────────────────┘
               │ @Steps (inyección)
               │
┌──────────────▼──────────────────────────────────────────────┐
│  CAPA DE ACCIONES (Action/Steps Classes)                    │
│  - NavigateSteps / NavigateActions                          │
│  - SearchSteps / SearchActions                              │
│  [Abstractan acciones del usuario]                          │
└──────────────┬──────────────────────────────────────────────┘
               │ UIInteractionSteps
               │
┌──────────────▼──────────────────────────────────────────────┐
│  CAPA DE PAGE OBJECTS (PageObject/PageComponent)            │
│  - SearchForm                                               │
│  - SearchResultSidebar                                      │
│  [Encapsulan elementos y selectores UI]                     │
└──────────────┬──────────────────────────────────────────────┘
               │ extend PageObject
               │
┌──────────────▼──────────────────────────────────────────────┐
│  CAPA DE INTERACCIÓN (Selenium WebDriver)                   │
│  - find() / findAll()                                       │
│  - sendKeys() / click()                                     │
│  [Interactúa directamente con navegador]                    │
└──────────────┬──────────────────────────────────────────────┘
               │
┌──────────────▼──────────────────────────────────────────────┐
│  CAPA DEL NAVEGADOR (Chrome WebDriver)                      │
│  - ChromeDriver (componente nativo)                         │
│  - Google Chrome (aplicación de navegador)                  │
└─────────────────────────────────────────────────────────────┘
```

### 4.2 Patrones de Diseño Implementados

#### 4.2.1 Page Object Pattern

**Propósito**: Encapsular elementos y selectores de una página en una clase dedicada.

**Implementación**:
```java
@DefaultUrl("https://duckduckgo.com/")
public class SearchForm extends PageObject {
    public static final By SEARCH_FIELD = By.name("q");
    public static final By SEARCH_BUTTON = By.cssSelector("[aria-label='Search']");
    public static final By ARTICLE_HEADINGS = By.cssSelector("[data-testid=result] h2");
}
```

**Ventajas**:
- Centraliza selectores en un lugar
- Reduce duplicación de código
- Facilita mantenimiento
- Permite reuso de selectores

#### 4.2.2 Steps/Actions Pattern

**Propósito**: Abstraer acciones de usuario en métodos reutilizables anotados con `@Step`.

**Implementación**:
```java
public class SearchSteps extends UIInteractionSteps {
    @Step("User searches for '{0}'")
    public void searchForTerm(String searchTerm) {
        find(SearchForm.SEARCH_FIELD).sendKeys(searchTerm);
        find(SearchForm.SEARCH_BUTTON).click();
        // ...
    }
}
```

**Ventajas**:
- Aumenta legibilidad de tests
- Genera pasos automáticos en reportes
- Reutilizable en múltiples tests
- Lenguaje natural en reportes

#### 4.2.3 Screenplay Pattern

**Propósito**: Modelar tests como acciones de un "actor" realizando "tareas" con "habilidades".

**Implementación**:
```java
@ExtendWith(SerenityJUnit5Extension.class)
class WhenSearchingByKeyword {
    NavigateActions navigate;   // Actor realiza Navigation
    SearchActions search;       // Actor realiza Search
    SearchResultSidebar sidebar; // Actor verifica componentes
    
    @Test
    void theKeywordShouldAppearInTheResultsSidebar() {
        navigate.toTheDuckDuckGoSearchPage();
        search.byKeyword("Cucumber");
        Serenity.reportThat("...", () -> assertThat(...));
    }
}
```

**Ventajas**:
- Muy expresivo y legible (BDD)
- Sigue "Given-When-Then" implícitamente
- Fácil de entender para no-técnicos

### 4.3 Flujo de Inyección de Dependencias

Serenity utiliza **Guice** para inyección:

```
Test Class
  ↓ @Managed(driver="chrome")
  └→ WebDriver (instancia única)
  
Test Class
  ↓ @Steps
  ├→ NavigateSteps
  │   └→ SearchForm (inyectada)
  │       └→ WebDriver (heredado)
  │
  ├→ SearchSteps
  │   └→ SearchForm (misma instancia)
  │       └→ WebDriver (misma instancia)
  │
  └→ SearchResultSidebar
      └→ WebDriver (misma instancia)
```

---

## 5. ESTRUCTURA DEL PROYECTO

### 5.1 Árbol Completo del Proyecto

```
serenity-junit-pageobjects-starter/
├── pom.xml                              # Configuración Maven
├── build.gradle                         # Configuración Gradle
├── gradlew                              # Gradle Wrapper (Unix)
├── gradlew.bat                          # Gradle Wrapper (Windows)
├── mvnw                                 # Maven Wrapper (Unix)
├── mvnw.cmd                             # Maven Wrapper (Windows)
├── serenity.properties                  # Propiedades de Serenity
├── README.md                            # Documentación principal
├── LICENSE                              # Licencia Apache 2.0
│
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar           # JAR del wrapper
│       ├── gradle-wrapper.properties    # Propiedades del wrapper
│
├── src/
│   ├── main/
│   │   └── java/
│   │       └── starter/
│   │           └── README.md            # Notas sobre código main
│   │
│   └── test/
│       ├── java/
│       │   └── starter/
│       │       ├── acceptancetests/
│       │       │   └── WhenSearchingForTerms.java         # Tests Pattern Clásico
│       │       │
│       │       ├── actions/
│       │       │   ├── NavigateSteps.java                 # Steps - Navegación
│       │       │   └── SearchSteps.java                   # Steps - Búsqueda
│       │       │
│       │       ├── duckduckgo/
│       │       │   ├── WhenSearchingByKeyword.java        # Tests Pattern Screenplay
│       │       │   ├── NavigateActions.java               # Actions - Navegación
│       │       │   ├── SearchActions.java                 # Actions - Búsqueda
│       │       │   └── SearchResultSidebar.java           # Componente de página
│       │       │
│       │       └── pageobjects/
│       │           └── SearchForm.java                    # Page Object
│       │
│       └── resources/
│           ├── junit-platform.properties                  # Configuración JUnit 5
│           ├── logback-test.xml                           # Configuración Logging
│           └── serenity.conf                              # Configuración Serenity
│
└── target/
    ├── classes/                         # Clases compiladas (main)
    ├── test-classes/                    # Clases compiladas (test)
    ├── surefire-reports/                # Reportes de Surefire
    ├── failsafe-reports/                # Reportes de Failsafe
    └── site/
        └── serenity/
            ├── index.html               # Reporte principal
            ├── features.html            # Reporte de features
            ├── statistics.html          # Estadísticas
            └── [otros archivos HTML]    # Reportes detallados
```

### 5.2 Clasificación de Archivos

**Configuración**:
- `pom.xml` - Dependencias Maven
- `build.gradle` - Dependencias Gradle
- `serenity.properties` - Propiedades Serenity
- `serenity.conf` - Configuración WebDriver
- `junit-platform.properties` - Configuración JUnit 5
- `logback-test.xml` - Configuración Logging

**Código Fuente (Test)**:
- `src/test/java/starter/` - Todos los tests

**Código Ejecutable**:
- `src/main/java/starter/` - Vacío (diseñado para código de APP bajo test)

**Generados**:
- `target/` - Salida de compilación y reportes

---

## 6. COMPONENTES PRINCIPALES

### 6.1 Page Objects

#### SearchForm.java

**Ubicación**: `src/test/java/starter/pageobjects/SearchForm.java`

**Responsabilidad**: Encapsular la página de búsqueda de DuckDuckGo

**Definición**:
```java
@DefaultUrl("https://duckduckgo.com/")
public class SearchForm extends PageObject {
    public static final By SEARCH_FIELD = By.name("q");
    public static final By SEARCH_BUTTON = By.cssSelector("[aria-label='Search']");
    public static final By ARTICLE_HEADINGS = By.cssSelector("[data-testid=result] h2");
}
```

**Componentes**:
- **URL Base**: https://duckduckgo.com/ (inyectada automáticamente)
- **SEARCH_FIELD**: Selector `name="q"` → campo de texto de búsqueda
- **SEARCH_BUTTON**: Selector `[aria-label='Search']` → botón de búsqueda
- **ARTICLE_HEADINGS**: Selector `[data-testid=result] h2` → títulos de resultados

**Métodos Heredados** (de PageObject):
- `open()` - Abre la URL base
- `find(By)` - Encuentra elemento por selector
- `findAll(By)` - Encuentra todos los elementos
- `$()` - Atajo para encuentra elemento

### 6.2 Page Components

#### SearchResultSidebar.java

**Ubicación**: `src/test/java/starter/duckduckgo/SearchResultSidebar.java`

**Responsabilidad**: Encapsular el componente sidebar de resultados

**Definición**:
```java
public class SearchResultSidebar extends PageComponent {
    public String heading() {
        return $("[data-testid=about] h2").getText();
    }
}
```

**Componentes**:
- **Selector**: `[data-testid=about] h2` → encabezado del sidebar
- **Método**: `heading()` → extrae texto del encabezado

**Diferencia con PageObject**:
- `PageComponent` = Parte de una página (reusable en múltiples páginas)
- `PageObject` = Página completa

### 6.3 Action Classes (Pattern Clásico)

#### NavigateSteps.java

**Ubicación**: `src/test/java/starter/actions/NavigateSteps.java`

**Responsabilidad**: Acciones de navegación

**Definición**:
```java
public class NavigateSteps extends UIInteractionSteps {
    SearchForm searchForm;

    @Step("User opens the home page")
    public void opensTheHomePage() {
        searchForm.open();
    }
}
```

**Anotaciones**:
- `@Step(...)` - Documenta el paso para reportes

**Inyecciones**:
- `SearchForm searchForm` - Inyectada automáticamente por Serenity

#### SearchSteps.java

**Ubicación**: `src/test/java/starter/actions/SearchSteps.java`

**Responsabilidad**: Acciones de búsqueda

**Definición**:
```java
public class SearchSteps extends UIInteractionSteps {
    SearchForm searchForm;

    @Step("User searches for '{0}'")
    public void searchForTerm(String searchTerm) {
        find(SearchForm.SEARCH_FIELD).sendKeys(searchTerm);
        find(SearchForm.SEARCH_BUTTON).click();
        withTimeoutOf(Duration.ofSeconds(10))
                .waitFor(presenceOfElementLocated(SearchForm.ARTICLE_HEADINGS));
    }

    @Step("Check the search results")
    public List<String> getSearchResults() {
        return findAll(SearchForm.ARTICLE_HEADINGS).texts();
    }
}
```

**Métodos**:
- `searchForTerm(String)` - Ingresa término y espera resultados
- `getSearchResults()` - Retorna lista de títulos

**Características**:
- Espera explícita: 10 segundos máximo
- Parámetros capturados en reporte: `'{0}'`
- Retorno tipado: `List<String>`

### 6.4 Action Classes (Pattern Screenplay)

#### NavigateActions.java

**Ubicación**: `src/test/java/starter/duckduckgo/NavigateActions.java`

**Responsabilidad**: Acciones de navegación (Screenplay)

**Definición**:
```java
public class NavigateActions extends UIInteractions {
    @Step("Navigate to the home page")
    public void toTheDuckDuckGoSearchPage() {
        openUrl("https://duckduckgo.com/");
    }
}
```

**Diferencias con NavigateSteps**:
- Hereda de `UIInteractions` (no `UIInteractionSteps`)
- `openUrl()` directo (sin PageObject)
- Más directo, menos encapsulación

#### SearchActions.java

**Ubicación**: `src/test/java/starter/duckduckgo/SearchActions.java`

**Responsabilidad**: Acciones de búsqueda (Screenplay)

**Definición**:
```java
public class SearchActions extends UIInteractions {
    @Step("Search for '{0}'")
    public void byKeyword(String keyword) {
        $("#searchbox_input").sendKeys(keyword, Keys.ENTER);
    }
}
```

**Características**:
- Selector directo: `$("#searchbox_input")`
- Envía Keys.ENTER directamente (no mediante click)
- Sintaxis más concisa

### 6.5 Test Classes

#### WhenSearchingForTerms.java (Pattern Clásico)

**Ubicación**: `src/test/java/starter/acceptancetests/WhenSearchingForTerms.java`

**Responsabilidad**: Tests de búsqueda (Pattern Page Objects + Steps)

**Definición**:
```java
@ExtendWith(SerenityJUnit5Extension.class)
class WhenSearchingForTerms {

    @Steps
    NavigateSteps navigate;

    @Steps
    SearchSteps search;

    @Test
    @DisplayName("Should be able to search for red things")
    void searchForRedThings() {
        navigate.opensTheHomePage();
        search.searchForTerm("red");
        assertThat(search.getSearchResults())
            .anyMatch(title -> title.toLowerCase().contains("red"));
    }

    @Test
    @DisplayName("Result page title should mention the search term")
    void searchForGreenThings() {
        navigate.opensTheHomePage();
        search.searchForTerm("green");
        assertThat(search.getTitle()).containsIgnoringCase("green");
    }
}
```

**Anotaciones**:
- `@ExtendWith(SerenityJUnit5Extension.class)` - Integración Serenity
- `@Steps` - Inyección de Steps
- `@Test` - Test JUnit 5
- `@DisplayName(...)` - Nombre amigable en reportes

**Tests Definidos**:
1. `searchForRedThings()` - Busca "red", valida que al menos un resultado contiene "red"
2. `searchForGreenThings()` - Busca "green", valida que página menciona "green"

**Problemas Detectados**:
- Método `getTitle()` referenciado pero no implementado en SearchSteps ⚠️

#### WhenSearchingByKeyword.java (Pattern Screenplay)

**Ubicación**: `src/test/java/starter/duckduckgo/WhenSearchingByKeyword.java`

**Responsabilidad**: Tests de búsqueda (Pattern Screenplay)

**Definición**:
```java
@ExtendWith(SerenityJUnit5Extension.class)
class WhenSearchingByKeyword {

    @Managed(driver = "chrome", options = "headless")
    WebDriver driver;

    NavigateActions navigate;
    SearchActions search;
    SearchResultSidebar searchResultSidebar;

    @Test
    void theKeywordShouldAppearInTheResultsSidebar() {
        navigate.toTheDuckDuckGoSearchPage();
        search.byKeyword("Cucumber");

        Serenity.reportThat("The keyword should appear in the sidebar heading",
                () -> assertThat(searchResultSidebar.heading())
                    .isEqualTo("Cucumber")
        );
    }
}
```

**Anotaciones Específicas**:
- `@Managed(driver="chrome", options="headless")` - WebDriver gestionado por Serenity
- Inyección manual de Actions (no usa `@Steps`)

**Características**:
- WebDriver explícito: `@Managed`
- Inyección de dependencias manual
- Uso de `Serenity.reportThat()` para reporting avanzado

---

## 7. FLUJOS DE EJECUCIÓN

### 7.1 Flujo de Ejecución de Test (Caso 1: Búsqueda Red)

```
┌─────────────────────────────────────────────────────────────┐
│ START: JUnit 5 Extension (SerenityJUnit5Extension)          │
└────────────────┬────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────┐
│ SETUP: Inyección de Dependencias (Guice)                    │
├────────────────────────────────────────────────────────────┤
│ 1. Crea instancia de WebDriver (Chrome headless)           │
│ 2. Inyecta WebDriver en NavigateSteps                      │
│ 3. Inyecta WebDriver en SearchSteps                        │
│ 4. Inyecta SearchForm en Steps                             │
└────────────────┬────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────┐
│ @Test: void searchForRedThings()                            │
└────────────────┬────────────────────────────────────────────┘
                 │
├─────────┬──────▼──────────────────────────────────────────────┐
│ PASO 1: navigate.opensTheHomePage()                          │
│         ├→ searchForm.open()                                 │
│         │   └→ WebDriver.get("https://duckduckgo.com/")     │
│         └→ Reporte: "User opens the home page"             │
└─────────┴───────────────────────────────────────────────────┘
                 │
├─────────┬──────▼──────────────────────────────────────────────┐
│ PASO 2: search.searchForTerm("red")                          │
│         ├→ find(By.name("q")).sendKeys("red")               │
│         ├→ find([aria-label]).click()                       │
│         ├→ Wait(10 sec) for [data-testid=result] h2         │
│         └→ Reporte: "User searches for 'red'"               │
└─────────┴───────────────────────────────────────────────────┘
                 │
├─────────┬──────▼──────────────────────────────────────────────┐
│ PASO 3: search.getSearchResults()                            │
│         ├→ findAll([data-testid=result] h2)                 │
│         ├→ Extrae textos: ["Red...", "Crimson...", ...]    │
│         └→ Retorna List<String>                             │
└─────────┴───────────────────────────────────────────────────┘
                 │
├─────────┬──────▼──────────────────────────────────────────────┐
│ PASO 4: Assertion                                            │
│         ├→ assertThat(["Red...", "Crimson...", ...])       │
│         │   .anyMatch(t → t.toLowerCase().contains("red"))  │
│         ├→ ✓ Pasa: al menos uno contiene "red"             │
│         └→ Reporte: "Check the search results" [PASSED]     │
└─────────┴───────────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────┐
│ TEARDOWN: Cleanup                                           │
├────────────────────────────────────────────────────────────┤
│ 1. WebDriver.quit()                                        │
│ 2. Cierra navegador                                        │
│ 3. Libera recursos                                         │
└────────────────┬────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────┐
│ REPORTING: Serenity genera HTML                            │
├────────────────────────────────────────────────────────────┤
│ target/site/serenity/index.html                           │
│ - Pasos ejecutados                                        │
│ - Pantallazos (si falla)                                  │
│ - Tiempos                                                 │
│ - Screenshots de cada paso                                │
└────────────────┬────────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────────┐
│ END: Test completado                                       │
└─────────────────────────────────────────────────────────────┘
```

### 7.2 Flujo de Ejecución de Tests Completo (Maven)

```
$ ./mvnw clean verify

┌──────────────────────────────────────────────────────┐
│ 1. CLEAN PHASE                                       │
│    - Elimina target/                                 │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 2. VALIDATE PHASE                                    │
│    - Valida estructura POM                           │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 3. COMPILE PHASE                                     │
│    - Compila código src/main/java                   │
│    - Salida: target/classes                         │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 4. TEST-COMPILE PHASE                               │
│    - Compila código src/test/java                   │
│    - Salida: target/test-classes                    │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 5. TEST PHASE (Surefire)                            │
│    - Ejecuta tests unitarios (*Test.java)           │
│    - SKIP=true en este proyecto                     │
│    - Salida: target/surefire-reports                │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 6. INTEGRATION-TEST PHASE (Failsafe)               │
│    - Ejecuta tests de integración/aceptación        │
│    - Busca: When*.java, *Test.java                 │
│    - Sistema: webdriver.base.url                    │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 7. VERIFY PHASE                                      │
│    - Verifica resultados                            │
│    - Reportes: target/site/serenity/                │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ RESULTADO FINAL                                      │
│ ✓ BUILD SUCCESS (si todos pasan)                   │
│ ✗ BUILD FAILURE (si alguno falla)                  │
└──────────────────────────────────────────────────────┘
```

### 7.3 Flujo de Ejecución (Gradle)

```
$ ./gradlew test

┌──────────────────────────────────────────────────────┐
│ 1. TASK: clean                                       │
│    - Elimina build/                                  │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 2. TASK: compileJava                                │
│    - Compila src/main/java                          │
│    - Salida: build/classes/java/main                │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 3. TASK: processTestResources                       │
│    - Copia src/test/resources                       │
│    - Salida: build/resources/test                   │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 4. TASK: compileTestJava                            │
│    - Compila src/test/java                          │
│    - Salida: build/classes/java/test                │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 5. TASK: test (JUnit5)                              │
│    - Descubre tests: **/*Test.java, When*.java      │
│    - Ejecuta cada test clase                        │
│    - Salida: build/test-results/test                │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ 6. TASK: aggregate (finalizBy test)                 │
│    - Genera reportes Serenity                       │
│    - Salida: build/reports/serenity/                │
└──────────────────────────────────────────────────────┘
                      ↓
┌──────────────────────────────────────────────────────┐
│ RESULTADO FINAL                                      │
│ ✓ BUILD SUCCESSFUL (si todos pasan)               │
│ ✗ BUILD FAILED (si alguno falla)                   │
└──────────────────────────────────────────────────────┘
```

---

## 8. CONFIGURACIÓN DETALLADA

### 8.1 Configuración Maven (pom.xml)

```xml
<!-- Model Version y Identificación -->
<modelVersion>4.0.0</modelVersion>
<groupId>net.serenity-bdd.starter</groupId>
<artifactId>serenity-junit-starter</artifactId>
<version>1.0.0-SNAPSHOT</version>
<packaging>jar</packaging>

<!-- Propiedades -->
<properties>
    <serenity.version>4.0.15</serenity.version>
    <junit5.version>5.10.0</junit5.version>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <encoding>UTF-8</encoding>
    <tags></tags>  <!-- Para filtrar tests por tag -->
    <webdriver.base.url></webdriver.base.url>  <!-- URL base parametrizable -->
</properties>
```

**Interpretación**:
- `<packaging>jar</packaging>` - Empaquetado como JAR ejecutable
- `<version>1.0.0-SNAPSHOT</version>` - Versión en desarrollo
- `<serenity.version>4.0.15</serenity.version>` - Versión fija de Serenity
- `<tags></tags>` - Variable para ejecución selectiva de tests
- `<webdriver.base.url></webdriver.base.url>` - Parametrizable para diferentes ambientes

**Configuración Failsafe Plugin**:
```xml
<plugin>
    <artifactId>maven-failsafe-plugin</artifactId>
    <version>3.1.2</version>
    <configuration>
        <includes>
            <include>**/*Test.java</include>
            <include>**/Test*.java</include>
            <include>**/*TestSuite.java</include>
            <include>**/When*.java</include>  <!-- Tests nombrados "When" -->
        </includes>
        <systemPropertyVariables>
            <webdriver.base.url>${webdriver.base.url}</webdriver.base.url>
            <junit.jupiter.extensions.autodetection.enabled>true</junit.jupiter.extensions.autodetection.enabled>
        </systemPropertyVariables>
    </configuration>
</plugin>
```

**Configuración Surefire Plugin**:
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>3.1.2</version>
    <configuration>
        <skip>true</skip>  <!-- Deshabilitado: no ejecuta tests unitarios -->
    </configuration>
</plugin>
```

### 8.2 Configuración Gradle (build.gradle)

```groovy
plugins {
    id "net.serenity-bdd.serenity-gradle-plugin" version "4.0.15"
    id 'java'
}

defaultTasks 'clean', 'test', 'aggregate'

// Versiones
ext {
    slf4jVersion = '1.7.7'
    serenityCoreVersion = '4.0.15'
    junitVersion = '5.10.0'
    assertJVersion = '3.23.1'
    lombokVersion = '1.18.24'
    logbackVersion = '1.2.11'
}

// Compatibilidad Java
sourceCompatibility = 16
targetCompatibility = 16

// Configuración de tests
test {
    useJUnitPlatform()                        // Usa JUnit 5
    testLogging.showStandardStreams = true    // Muestra salida
    systemProperties System.getProperties()   // Propiedades del sistema
}

// Reportes Serenity
serenity {
    reports = ["single-page-html"]           // Reporte HTML en una página
    testRoot = "starter"                     // Raíz de clases de test
}

// Genera reportes después de tests
test.finalizedBy(aggregate)
```

**Interpretación**:
- `defaultTasks 'clean', 'test', 'aggregate'` - Tareas por defecto al ejecutar `gradle`
- `useJUnitPlatform()` - Usa el motor JUnit 5
- `testRoot = "starter"` - Busca tests en paquete `starter.*`
- `test.finalizedBy(aggregate)` - Siempre genera reportes después de tests

### 8.3 Configuración Serenity (serenity.conf)

```hocon
serenity {
  take.screenshots = FOR_FAILURES           # Solo captura en fallos
  test.root = "starter.acceptancetests"     # Raíz de búsqueda de tests
}

headless.mode = true                         # Modo headless

webdriver {
  driver = chrome                            # Chrome es el navegador
  capabilities {
    browserName = "chrome"
    acceptInsecureCerts = true               # Acepta certificados inseguros
    "goog:chromeOptions" {                   # Opciones específicas de Chrome
      args = [
        "remote-allow-origins=*",           # CORS
        "test-type",                        # Modo de test
        "no-sandbox",                       # Sin sandbox (para CI/CD)
        "ignore-certificate-errors",        # Ignora errores SSL
        "--window-size=1000,800",           # Tamaño de ventana
        "incognito",                        # Modo privado
        "disable-infobars",                 # Sin barras de información
        "disable-gpu",                      # Sin aceleración GPU
        "disable-default-apps",             # Sin apps por defecto
        "disable-popup-blocking"            # Sin bloqueo de popups
      ]
    }
  }
}
```

**Interpretación**:
- `take.screenshots = FOR_FAILURES` - Captura automática solo cuando falla
- `headless.mode = true` - Sin interfaz gráfica
- `no-sandbox` - Crítico para ejecución en contenedores/CI
- `--window-size=1000,800` - Resolución fija (importante para consistency)
- `incognito` - Sin caché ni cookies previas

### 8.4 Configuración JUnit 5 (junit-platform.properties)

```properties
junit.jupiter.execution.parallel.enabled=false
junit.jupiter.execution.parallel.config.strategy=fixed
junit.jupiter.execution.parallel.config.fixed.parallelism=4
junit.jupiter.execution.parallel.config.fixed.max-pool-size=4
```

**Interpretación**:
- `parallel.enabled=false` - Tests ejecutan secuencialmente (no en paralelo)
- `parallelism=4` - Si se habilita: máximo 4 threads paralelos
- `max-pool-size=4` - Pool máximo de 4 threads

### 8.5 Configuración Logging (logback-test.xml)

```xml
<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder>
        <pattern>
            %d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n
        </pattern>
    </encoder>
</appender>

<logger name="root" level="WARN"/>
<logger name="net.serenitybdd" level="INFO"/>
<logger name="net.thucydides" level="INFO"/>

<root level="WARN">
    <appender-ref ref="STDOUT"/>
</root>
```

**Interpretación**:
- Nivel por defecto: `WARN` (solo warnings y errores)
- Serenity: `INFO` (muestra información detallada)
- Patrón: `%d{HH:mm:ss.SSS}` hora, `%thread` thread, `%-5level` nivel, `%logger{36}` logger corto

---

## 9. REGLAS DE NEGOCIO

### 9.1 Dominios de Negocio

#### Dominio: Búsqueda Web

**Actor Principal**: Usuario (persona o sistema automatizado)

**Objetivo Principal**: Validar que el motor de búsqueda DuckDuckGo retorna resultados relevantes

### 9.2 Reglas Funcionales Core

#### **RN-001: Acceso a Motor de Búsqueda**

- **Descripción**: Todo usuario debe poder acceder a DuckDuckGo
- **Precondición**: Navegador Chrome disponible y funcional
- **Acción**: Navegar a `https://duckduckgo.com/`
- **Postcondición**: Página cargada y lista para búsqueda
- **Tolerancia de Error**: 0% (acceso debe ser 100% confiable)
- **Implementación**: `NavigateSteps.opensTheHomePage()` / `NavigateActions.toTheDuckDuckGoSearchPage()`

#### **RN-002: Ingreso de Término de Búsqueda**

- **Descripción**: Usuario puede ingresar un término de búsqueda
- **Precondición**: Página de búsqueda cargada
- **Acción**: 
  1. Localizar campo de búsqueda (`By.name("q")`)
  2. Ingresar cadena de texto
  3. Enviar búsqueda (click botón o presionar ENTER)
- **Postcondición**: Sistema procesa búsqueda
- **Constraint**: Término no vacío
- **Implementación**: `SearchSteps.searchForTerm()` / `SearchActions.byKeyword()`

#### **RN-003: Retorno de Resultados**

- **Descripción**: Sistema retorna lista de artículos/títulos
- **Precondición**: Búsqueda completada
- **Acción**: Extraer encabezados de resultados
- **Postcondición**: Lista de títulos disponible
- **Selector CSS**: `[data-testid=result] h2`
- **Timeout Máximo**: 10 segundos
- **Implementación**: `SearchSteps.getSearchResults()` retorna `List<String>`

#### **RN-004: Relevancia de Resultados (Case-Insensitive)**

- **Descripción**: Al menos uno de los resultados debe contener el término de búsqueda
- **Precondición**: Resultados retornados
- **Validación**: `title.toLowerCase().contains(searchTerm.toLowerCase())`
- **Ejemplos Válidos**:
  - Buscar: "red" → Resultado: "Red Cars" ✓
  - Buscar: "RED" → Resultado: "Red Cars" ✓
  - Buscar: "red" → Resultado: "CRIMSON" ✗
- **Tolerancia**: Mínimo 1 de N resultados
- **Implementación**: `assertThat(results).anyMatch(...)`

#### **RN-005: Información Contextual en Sidebar**

- **Descripción**: Sidebar muestra información sobre el término buscado
- **Precondición**: Búsqueda completada
- **Acción**: Extraer encabezado del sidebar
- **Selector CSS**: `[data-testid=about] h2`
- **Validación**: Encabezado debe coincidir exactamente con término
- **Sensibilidad**: Case-sensitive (coincidencia exacta)
- **Implementación**: `SearchResultSidebar.heading()` == término
- **Nota**: Componente no siempre está presente

#### **RN-006: Título de Página Menciona Término**

- **Descripción**: El título de la página de resultados debe mencionar el término buscado
- **Precondición**: Búsqueda completada
- **Validación**: `page.getTitle().containsIgnoringCase(searchTerm)`
- **Sensibilidad**: Case-insensitive
- **Status**: ⚠️ Método no implementado en `SearchSteps`

### 9.3 Reglas Técnicas No-Funcionales

#### **RN-N001: Configuración de Navegador**

- Navegador: Google Chrome
- Modo: Headless (sin interfaz gráfica)
- Resolución: 1000x800 píxeles
- Contexto: Incógnito (sin caché)
- Certificados: Acepta inseguros

#### **RN-N002: Timeouts y Esperas**

- Espera explícita por resultados: 10 segundos máximo
- Espera implícita: 0 segundos (no configurada)
- Timeout de comando Web: Por defecto Serenity

#### **RN-N003: Paralelismo**

- Ejecución de tests: Secuencial (no paralelo)
- Threads disponibles (si se habilita): 4

#### **RN-N004: Reporte y Evidence**

- Capturas de pantalla: Solo en fallos
- Reporte: HTML interactivo
- Ubicación: `target/site/serenity/` (Maven) o `build/reports/serenity/` (Gradle)
- Pasos capturados: Todos (via `@Step`)

#### **RN-N005: Compatibilidad**

- Java Version: 16+
- Maven: 3.6+
- Gradle: 7.x+
- Chrome: Latest (WebDriver Manager lo descarga)

---

## 10. ESPECIFICACIONES TÉCNICAS

### 10.1 Selectores CSS Utilizados

| Componente | Selector | XPath | Propósito |
|-----------|----------|-------|----------|
| Campo de búsqueda | `By.name("q")` | N/A | Campo de texto principal |
| Botón de búsqueda | `[aria-label='Search']` | `//button[@aria-label='Search']` | Botón de envío |
| Encabezados resultados | `[data-testid=result] h2` | `//div[@data-testid='result']//h2` | Títulos de resultados |
| Sidebar heading | `[data-testid=about] h2` | `//div[@data-testid='about']//h2` | Encabezado de info contextual |
| Atajo jQuery | `$("#searchbox_input")` | `//*[@id='searchbox_input']` | Input de búsqueda (Screenplay) |

### 10.2 Duración Esperada de Ejecución

- **Tiempo por test**: 3-8 segundos
- **Setup/Teardown**: 1-2 segundos
- **Tiempo total (2 tests)**: ~15 segundos
- **Tiempo total (full suite): ~20-30 segundos**

### 10.3 Condiciones Previas del Ambiente

**Hardware Mínimo**:
- CPU: 2 cores
- RAM: 2-4 GB
- Disco: 500 MB (free)

**Software Requerido**:
- JDK 16+
- Google Chrome (cualquier versión reciente)
- Maven 3.6+ ó Gradle 7.x+

**Configuración del Sistema**:
- JAVA_HOME correctamente configurada
- Chrome debe ser accesible desde línea de comandos
- Puerto 9222 disponible (debugging remoto Chrome)

### 10.4 Excepciones y Manejo de Errores

| Excepción | Causa Probable | Manejo |
|-----------|---|---|
| `NoSuchElementException` | Selector no encontrado | Timeout + Screenshot |
| `TimeoutException` | Elemento no carga en timeout | Marca test como FAILED |
| `WebDriverException` | Chrome crash | Reinicia WebDriver |
| `StaleElementReferenceException` | Elemento recargado | Reintenta encuentro |

---

## 11. DEPENDENCIAS Y COMPATIBILIDADES

### 11.1 Matriz de Compatibilidad

| Componente | Versión | Java Requerida | Notas |
|-----------|---------|---|---|
| Serenity 4.x | 4.0.15 | 8+ | Requiere Java 8 mínimo |
| JUnit 5 | 5.10.0 | 8+ | Moderno y flexible |
| AssertJ | 3.22.0+ | 8+ | Assertions expresivas |
| Selenium | 4.x (transitivo) | 8+ | A través de Serenity |
| Logback | 1.2.11 | 8+ | SLF4J compatible |
| Gradle | 7.x+ | Varía | Gradle 8 x soportado |
| Maven | 3.6+ | Varía | Maven 3.8+ recomendado |

### 11.2 Árbol de Dependencias (Transitivos Principales)

```
serenity-core:4.0.15
├── selenium-webdriver:4.x
│   ├── selenium-api:4.x
│   ├── selenium-chrome-driver:4.x
│   └── webdriver-manager:5.x
├── guice:5.x (inyección)
├── hamcrest:2.x (matchers)
├── commons-lang:3.x
└── slf4j-api:1.7.x

serenity-junit5:4.0.15
├── serenity-core (ver arriba)
└── junit:jupiter-api:5.x

jasserj-core:3.22.0
├── assertj-core:3.22.0
└── (sin dependencias adicionales mayores)
```

---

## 12. CONSTRAINTS Y LIMITACIONES

### 12.1 Limitaciones Funcionales

#### L-001: Método getTitle() no implementado

- **Status**: ⚠️ Código incompleto
- **Ubicación**: `SearchSteps.java`
- **Impacto**: Test `searchForGreenThings()` probablemente falle
- **Requerimiento**: Implementar método para obtener título de página

#### L-002: Solo búsqueda básica por texto

- **Limitación**: No soporta búsquedas complejas
- **No soporta**: Operadores (AND, OR), filtros de fecha, tipo, idioma
- **Alcance**: Solo búsqueda de cadena exacta

#### L-003: Componente sidebar no siempre disponible

- **Dependencia**: No todos los términos muestran sidebar
- **Fallback**: Necesario hacer pageobjects opcionales
- **Solución**: Usar `waitFor(presenceOfAllElementsLocatedBy(...))` con condición

#### L-004: Sin autenticación de usuario

- **Alcance**: No prueba funcionalidad de login
- **Cobertura**: Solo funcionalidad anónima

#### L-005: Sin validación de HTML/W3C

- **Constraint**: No valida validez HTML de resultados
- **Scope**: Solo validación de contenido textual

#### L-006: Sin pruebas de performance/carga

- **Alcance**: No mide tiempos de carga
- **Validación**: Solo que cargue dentro del timeout

### 12.2 Limitaciones Técnicas

#### LT-001: Headless mode solo en Chrome

- **Navegador Único**: Solo Chrome
- **Implicación**: No se puede testear en Firefox, Safari, Edge
- **Razón**: Configuración de serenity.conf limitada a Chrome

#### LT-002: Resolución fija 1000x800

- **Constraint**: Tests pueden fallar en otras resoluciones
- **No prueba**: Responsive design en otros tamaños
- **Requerimiento**: Parametrizar window-size para multi-resolución

#### LT-003: Ejecución secuencial

- **Limitación**: Sin paralelismo, tests lentos
- **Constraint**: `junit.jupiter.execution.parallel.enabled=false`
- **Opportunity**: Habilitar paralelismo para acelerar suite

#### LT-004: URL base hardcodeada

- **Limitación**: https://duckduckgo.com es URL fija
- **Restricción**: No es fácil cambiar ambiente (dev/staging/prod)
- **Mejora**: Usar propiedades `webdriver.base.url`

#### LT-005: Sin gestión de datos de test

- **No hay**: Base de datos de test, fixtures, seeders
- **Datos**: Hardcodeados en tests ("red", "green", "Cucumber")
- **Escalabilidad**: Difícil para parametrización masiva

### 12.3 Limitaciones de Ambiente

- Chrome debe estar instalado en el sistema
- Sin soporte para otros navegadores en configuración actual
- Sin soporte para testing en dispositivos móviles
- Sin Cross-browser testing configurado

---

## 13. CRITERIOS DE ACEPTACIÓN

### 13.1 Criterios de Aceptación Generales del Proyecto

#### CA-001: Acceso Exitoso a DuckDuckGo
```
Dado que ejecuto el test
Cuando intento acceder a https://duckduckgo.com/
Entonces la página carga en menos de 10 segundos
Y no hay errores de conexión
Y el campo de búsqueda está visible
```

#### CA-002: Búsqueda Funcional
```
Dado que estoy en la página de búsqueda
Cuando ingreso un término válido
Y presiono enter o click en botón
Entonces se ejecuta la búsqueda
Y los resultados cargan en menos de 10 segundos
Y se retorna al menos 1 resultado
```

#### CA-003: Relevancia de Resultados
```
Dado que ejecuté una búsqueda por "red"
Cuando se cargan los resultados
Entonces al menos uno de los títulos contiene la palabra "red" (case-insensitive)
Y la búsqueda no retorna cero resultados
```

#### CA-004: Información Contextual
```
Dado que busco por "Cucumber"
Cuando se carga la página de resultados
Entonces existe un sidebar con encabezado
Y el encabezado exactamente dice "Cucumber"
```

#### CA-005: Reportes Generados
```
Dado que se ejecutó una suite de tests
Cuando finaliza la ejecución
Entonces se genera un archivo index.html en target/site/serenity/
Y el reporte contiene lista de tests ejecutados
Y el reporte muestra pasos y pantallazos
Y el reporte indica estado (PASSED/FAILED)
```

#### CA-006: Build Exitoso
```
Dado que ejecuto "mvn clean verify" o "gradle test"
Cuando completar all phases
Entonces retorna exit code 0 (success)
Y genera reportes en target/site/serenity/
Y no hay errores de compilación o dependencias
```

### 13.2 Criterios de Calidad

| Criterio | Métrica | Target |
|----------|---------|--------|
| Code Coverage | Líneas cubiertas | 70%+ |
| Test Pass Rate | % tests pasando | 95%+ |
| Build Time | duración total | < 60 segundos |
| Mantenibilidad | Duplicación de código | < 5% |
| Reusabilidad | Tests reutilizables | 80%+ |
| Documentation | Cobertura de código | 100% |

---

## 14. GUÍA DE EJECUCIÓN

### 14.1 Requisitos Previos

```bash
# Verificar Java
java -version
# Resultado esperado: Java 16+

# Verificar Maven
mvn -version
# Resultado esperado: Apache Maven 3.6+

# Verificar Gradle
gradle -version
# Resultado esperado: Gradle 7.x+

# Verificar Chrome
chrome --version
# Resultado esperado: Google Chrome X.Y.Z
```

### 14.2 Ejecución con Maven

```bash
# Ejecutar todos los tests
./mvnw clean verify

# Ejecutar con tags específicas (si implementado)
./mvnw clean verify -Dtags="@smoke"

# Ejecutar una clase de test específica
./mvnw clean verify -Dinclude=starter/acceptancetests/WhenSearchingForTerms.java

# Sin captura de pantalla
./mvnw clean verify -Dserenity.take.screenshots=DISABLED
```

### 14.3 Ejecución con Gradle

```bash
# Ejecutar todos los tests
./gradlew clean test

# Ejecutar con logging detallado
./gradlew test --info

# Ejecutar sin cache
./gradlew clean test --no-build-cache

# Ejecutar en paralelo (si habilita junit-platform.properties)
./gradlew test --parallel
```

### 14.4 Ubicación de Reportes

- **Maven**: `target/site/serenity/index.html`
- **Gradle**: `build/reports/serenity/index.html`

**Abrir en navegador**:
```bash
# Windows
start target/site/serenity/index.html

# macOS
open target/site/serenity/index.html

# Linux
xdg-open target/site/serenity/index.html
```

---

## 15. APÉNDICE: MATRIZ DE COMPONENTES

| Componente | Tipo | Ubicación | Responsabilidad | Dependencias |
|-----------|------|-----------|-----------------|--------------|
| SearchForm | PageObject | pageobjects/ | Encapsula página búsqueda | Serenity PageObject |
| SearchResultSidebar | PageComponent | duckduckgo/ | Componente sidebar | Serenity PageComponent |
| NavigateSteps | Steps | actions/ | Navegación (clásico) | SearchForm, UIInteractionSteps |
| SearchSteps | Steps | actions/ | Búsqueda (clásico) | SearchForm, UIInteractionSteps |
| NavigateActions | Actions | duckduckgo/ | Navegación (Screenplay) | UIInteractions |
| SearchActions | Actions | duckduckgo/ | Búsqueda (Screenplay) | UIInteractions |
| WhenSearchingForTerms | Test | acceptancetests/ | Tests búsqueda clásico | NavigateSteps, SearchSteps, JUnit 5 |
| WhenSearchingByKeyword | Test | duckduckgo/ | Tests búsqueda Screenplay | NavigateActions, SearchActions, JUnit 5 |

---

**Documento Generado**: 04 de Abril de 2026  
**Versión del Proyecto**: 1.0.0-SNAPSHOT  
**Stack**: Serenity BDD 4.0.15 + JUnit 5 5.10.0 + Java 16
