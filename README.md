# MUSA

## Начало работы
1. Установить последнии версии IDE: [Android Studio](https://www.jetbrains.com/toolbox-app/) и [Xcode](https://xcodereleases.com/?scope=release)
2. Склонировать проект
    ```
	git clone https://gitlab.musa.kz/mobile/musa-mobile-app
	```

### Настройка среды Android
1. Открыть проект в Android Studio
2. Установить плагин [Kotlin Multiplatform](https://plugins.jetbrains.com/plugin/14936-kotlin-multiplatform)
3. Установить плагины оформления (_Опционально_)
    - [Material Theme UI](https://plugins.jetbrains.com/plugin/8006-material-theme-ui)
    - [Atom Material Icons](https://plugins.jetbrains.com/plugin/10044-atom-material-icons)
4. Build & Run

> Для запуска iOS таргета в Android Studio нужно сначала произвести настройку среды iOS (см. след. пункт), затем в настройках конфигурации выбрать сгенерированный iOS проект (MUSA.xcworkspace), схему (MUSA), конфигурацию (Debug / Release) и девайс.

### Настройка среды iOS
1. Установить [Homebrew](https://brew.sh/)
2. Установить [Tuist](https://docs.tuist.io/)
   ```
   brew install tuist  
   ```
3. Перейти в папку iosApp в root директории проекта
   ```
   cd {$ROOT}/iosApp
   ```
4. Произвести установку зависимостей и сгенерировать iOS проект
    ```
    tuist install
    tuist generate
    ```
5. Build & Run

## Документация по платформам
- [iOS App Doc](iosApp/docs.md)
- Android App Doc