# EShop Modular Monolith

Implementação da arquitetura modular monolítica.

## Estrutura

```text
eshop-modular-monoliths/
├── bootstrapper/
│   └── api/                    # Projeto Spring Boot
├── modules/                    # Pasta organizacional
│   ├── catalog/                # Projeto java-library
│   ├── basket/                 # Projeto java-library
│   └── ordering/               # Projeto java-library
├── shared/                     # Shared Class Library -> java-library
├── build.gradle
└── settings.gradle
```


O projeto `api`, dentro de `bootstrapper`, é o ponto de composição da aplicação:
conhece e inicializa os módulos. As pastas `bootstrapper` e `modules` não são
projetos Gradle. Os módulos podem usar tipos mínimos de `shared`, mas `shared`
não conhece a API nem qualquer módulo de negócio.

Cada módulo expõe seus contratos e DTOs em
`resousadev.eshop.<modulo>.api`. As implementações ficam em `internal` e não
devem ser importadas por outros módulos.

## Dependências

```text
:api
├── :catalog ──────────>      :shared
├── :basket ──> :ordering ──> :shared
└── :ordering ─────────────>  :shared
```

## Executar

```powershell
.\gradlew.bat :api:bootRun
```

## Testar

```powershell
.\gradlew.bat test
```
