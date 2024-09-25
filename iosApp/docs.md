# MUSA-iOS

### Документация
1. [Структура проекта](#structure)
2. [Добавление зависимостей](#dependencies)
3. [Добавление новых модулей](#newModule)

<a name="structure"></a>
## Структура проекта

```
├── App                    // Главный модуль (здесь находятся SceneDelegate, Container, логика старта / сборки итд)
│
├── Core
│   ├── Extensions      // базовые extension-ы 
│   ├── Kit            // базовые вьюшки и сущности
│   └── Utils         // хелперы / менеджеры 
│
├── Features        // фича-модули
│   ├── Auth
│   ├── Learning
│   ├── Profile
│   └── Quran
│
├── Project.swift   // главный manifest файл проекта
│
├── Tuist
│   ├── Config.swift                                   // файл конфигурации Tuist в рамках проекта
│   ├── Package.swift                                 // зависимости
│   └── ProjectDescriptionHelpers                    // основные файлы manifest-а
│       ├── Factory
│       │   └── ModulesFactory.swift               // фабрика модулей
│       ├── Project+Templates.swift               // Основной файл с описанием проекта
│       ├── TargetConfiguration.swift            // описание конфигураций Debug & Release и соответсвующих Build settings
│       ├── TargetScheme.swift                  // описание scheme проекта, пока что не используется
│       └── Utils                              // утилиты
│           ├── App.swift                     // основная информация о приложении (bundleID, teamID, deploymentTarget..)
│           ├── AppVersions.swift            // версия приложения и номер сборки
│           ├── Module.swift                // структурка Module для дочерних модулей
│           └── PrivacyDescriptions.swift  // текста для Privacy
```

<a name="dependencies"></a>
## Добавление сторонних зависимостей

1. Перейти в настройки проекта `tuist edit`
2. Открыть `Package.swift`
3. Добавить зависимость в `dependencies`
4. Добавить название зависимости в нужный таргет. Если в главный таргет, то в `Project.swift`, если в дочерний модуль, то в `ModulesFactory.swift`


<a name="newModule"></a>
## Добавление новых модулей

1. Добавить файлы модуля в проект. Основную папку в `Features/`, а файлы модуля должны быть разделены по соответсвующим папкам `Resources` и `Sources`
2. Перейти в настройки проекта `tuist edit`
3. Открыть `ModulesFactory.swift`
4. Добавить в enum `ModuleTarget` новый `case newModule` с названием вашего модуля, добавить название (`name`) и путь к файлам модуля (`path`)
5. Прописать статичный метод для сборки модуля в `extension ModulesFactory`
    ```
    extension ModulesFactory {
        public static func makeNewModule() -> Module {
            makeModule(
                target: .newModule,
                frameworkDependencies: [
                    .target(name: ModuleTarget.coreKit.name),
                    .target(name: ModuleTarget.coreUtils.name),
                    .target(name: ModuleTarget.coreExtensions.name),
                    .external(name: "Nivelir"),
                    .external(name: "Factory"),
                ]
            )
        }
    }
    ```
6. Добавить модуль в качестве зависимости в главный таргет в `Project.swift`, внутри `moduleTargets`
    ```
        ...
        moduleTargets: coreTargets + [
            ...
            ModulesFactory.makeNewModule(),
        ]
    ```