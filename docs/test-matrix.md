# Test matrix / Матрица испытаний

Status as of 2026-11-14. A pass means only the stated check passed on one device.

| Check / Проверка | Result / Результат | Limit / Ограничение |
|---|---|---|
| Board identity, kernel, build / Модель, ядро, сборка | Read from device / Считаны с устройства | One unit / Один экземпляр |
| CPU, RAM, storage, temperature / Ресурсы, температура | Sampled, no exhaustion / Дефицита не выявлено | No stress test / Без нагрузочного теста |
| Boot/system errors / Ошибки ядра и диска | No OOM/panic/I/O error found / Не найдены в проверенных логах | Retained history only / Только сохранённая история |
| Existing IPv4 PPPoE session / Действующий PPPoE | Stayed up through package updates; fresh session after reboot passed / Сохранился при обновлениях; новый сеанс после перезагрузки работает | One reconnect / Одно переподключение |
| Local SSH / SSH | New connections passed / Новые подключения работают | WAN exposure not tested externally / Внешняя проверка WAN не проводилась |
| LuCI / Панель OpenWrt | Login page and static resources passed / Форма входа и ресурсы доступны | Full authenticated workflow not retested / Все действия после входа не проверены |
| StealthSurf update / Обновление | Manual 1.0.101 → 1.0.106 passed / Ручная установка прошла | Future auto-update unproven / Будущее автообновление не проверено |
| VPN connectivity / VPN | Connected; HTTPS probe passed / Подключён, HTTPS работает | No failover injection / Отказ резервов не моделировался |
| Direct connectivity / Прямой интернет | HTTPS probe passed / HTTPS работает | Not all destinations / Не все ресурсы |
| LAN DNS + web access / DNS и HTTPS из LAN | Targeted probes performed / Выполнены точечные пробы | Not a mobile application/streaming test / Не проверка приложений и видео |
| Firewall / Межсетевой экран | Syntax check and reload passed / Проверка и применение прошли | No penetration test / Не тест на проникновение |
| Logging/archive / Запись и архивы | New log grows, fresh archive readable / Новый лог растёт, архив читается | Old rotation error unresolved / Старая ошибка ротации не решена |
| Rollback / Откат | Archives verified, timers prepared and disarmed / Архивы проверены, таймеры сняты | Actual restore not exercised / Восстановление не испытывалось |
| Reboot after updates / Перезагрузка после обновлений | Passed: new procd, PPPoE and automatic VPN start / Новый procd, PPPoE и автозапуск VPN работают | One warm reboot / Одна обычная перезагрузка |
| Power cycle / Отключение питания | Not tested / Не проверено | Separate recovery test / Нужна отдельная проверка |
| IPv6, VLAN, 2.5G, LAN-to-LAN, hardware offload | Not tested in this maintenance / В этом обслуживании не проверены | Other upstream reports concern their own builds / Чужие отчёты относятся к их сборкам |

Please add a new dated report rather than silently extending these results to another hardware unit or source revision.
