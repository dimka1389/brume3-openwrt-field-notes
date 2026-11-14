# Clean build starting point / Основа для чистой сборки

[English](../README.md) · [Русский](../README.ru.md)

## English

This is a documented starting point, not a tested release or a complete flashing guide. The original private image contains a personalized overlay, including authorized SSH keys and local setup. It must not be distributed. The clean variant described here has not been built and flashed as part of this maintenance session.

1. Use a separate Linux build environment and the [upstream build prerequisites](https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem). Use a fresh clone of [GLiNet-Tech/openwrt](https://github.com/GLiNet-Tech/openwrt), checked out at `1713e8be63b628fe2f1d336f4fb3a8aa152875af`. Check [PR #24237](https://github.com/openwrt/openwrt/pull/24237) for changed limitations before proceeding.
2. Initialize the feeds and check out the exact historical feed revisions listed below before installing feed definitions. Record the resulting source and feed hashes. These are historical revisions, not a claim of current security support.
3. Use the minimal seed below, then OpenWrt's `make defconfig`, `make download` and build process. Review the expanded configuration and build output. The kernel modules must come from that exact build.
4. Do not copy a `files/` directory, private overlay, account directory, password database, certificates/private keys or SSH authorization files from an existing router/project. Review the contents of the resulting image independently before any publication.
5. Firmware installation and recovery are a separate procedure. Validate the exact hardware, image metadata, storage layout and recovery method against the upstream work. A clean image can have different network/login defaults from the private installation. This document intentionally supplies no one-command flashing path.
6. StealthSurf is a separate vendor application, not bundled here. Check its [official compatibility requirements and installation instructions](https://stealthsurf.net/routers). Never embed a personal subscription or account in a shared image.

Before a downloadable release: build the clean variant, inspect it for embedded personal data, record toolchain/config/feed information and hashes, test installation and recovery on the exact model, and document the limits. Independent review is still needed; a text search alone does not certify a firmware image as free of secrets.

## Русский

Это отправная точка для сборки, не проверенный релиз и не полная инструкция прошивки. В исходном личном образе есть персональный overlay, включая разрешённые SSH-ключи и локальную настройку. Его нельзя распространять. Описанная чистая версия в ходе этого обслуживания отдельно не собиралась и не прошивалась.

1. Подготовьте отдельную Linux-среду по [требованиям OpenWrt](https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem). Возьмите свежий клон [GLiNet-Tech/openwrt](https://github.com/GLiNet-Tech/openwrt) и коммит `1713e8be63b628fe2f1d336f4fb3a8aa152875af`. Перед работой проверьте актуальные ограничения в [PR #24237](https://github.com/openwrt/openwrt/pull/24237).
2. Инициализируйте feeds и перед установкой их описаний переключите их на исторические ревизии ниже. Зафиксируйте хеши. Это историческая основа, а не заявление об актуальной поддержке безопасности.
3. Используйте минимальную заготовку ниже, затем штатные этапы OpenWrt `make defconfig`, `make download` и компиляцию. Проверьте итоговую конфигурацию и вывод сборки. Модули ядра должны относиться именно к полученной сборке.
4. Не переносите из личной установки каталог `files/`, overlay, аккаунт, базу паролей, сертификаты с закрытыми ключами или SSH-авторизацию. Перед публикацией независимо проверьте состав итогового образа.
5. Установка и восстановление — отдельная процедура: нужно проверить точную модель, метаданные образа, разметку хранилища и способ восстановления по исходному проекту. Настройки сети и входа чистого образа могут отличаться от личной установки. Команды «прошить одним действием» здесь нет.
6. StealthSurf устанавливается отдельно по [официальной инструкции](https://stealthsurf.net/routers), после проверки совместимости. Личный аккаунт и подписку нельзя включать в общий образ.

Перед выпуском скачиваемого образа нужны чистая сборка, проверка содержимого на персональные данные, сведения о toolchain/config/feeds и контрольных суммах, испытания установки и восстановления на точной модели, описание ограничений. Одного текстового поиска для сертификации образа как свободного от секретов недостаточно.

## Historical feed revisions / Исторические ревизии feeds

```text
luci 217e71dc75dae31ab670b0e602162a76559a0b47
packages 7eef26d5122e52301e0df3ddf9327cff16c1a713
routing ea8633da9c461a9bdc62a0323439d31180762e03
telephony 9bcb6d71db03377ff49ccb099be763add9a5b059
video 81bca9f3f30dabd790df9be111a776e799640a80
```

## Minimal build seed / Минимальная заготовка `.config`

Derived from the original build's package selection; excludes the personal overlay. This is not the full expanded build configuration. / Основано на выборе пакетов исходной сборки, без персонального overlay; это не полная развёрнутая конфигурация.

```text
CONFIG_TARGET_mediatek=y
CONFIG_TARGET_mediatek_filogic=y
CONFIG_TARGET_mediatek_filogic_DEVICE_glinet_gl-mt5000=y
CONFIG_PACKAGE_luci-ssl=y
CONFIG_LUCI_LANG_ru=y
CONFIG_PACKAGE_firewall4=y
CONFIG_PACKAGE_ppp=y
CONFIG_PACKAGE_ppp-mod-pppoe=y
CONFIG_PACKAGE_ip-full=y
CONFIG_PACKAGE_kmod-nft-tproxy=y
CONFIG_PACKAGE_kmod-nft-queue=y
CONFIG_PACKAGE_curl=y
CONFIG_PACKAGE_ca-bundle=y
CONFIG_PACKAGE_jsonfilter=y
```
