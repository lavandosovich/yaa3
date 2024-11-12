# ER-диаграмма

## Основные сущности и их атрибуты

### Legend

**pk** - primary key, здесь это так же уникальный индетификатор.     
**fk** - foreign key.   
**one-to-many** - связь, где одной сущности принадлежит множество сущностей.   
**many-to-many** - связь, где сущностям по обе стороны может принадлежать множество сущностей с противоположной стороны.   

### 1. User
   - `id` — pk.
   - `name` — имя пользователя.
   - `email` — электронная почта пользователя.
   - `password` — захеширонванный пароль пользователя.

### 2. House
   - `id` — pk.
   - `user_id` — идентификатор пользователя, к которому принадлежит дом, fk:User.
   - `address` — адрес дома.

### 3. Device
   - `id` — pk.
   - `type_id` — идентификатор типа устройства, fk:DeviceType.
   - `house_id` — идентификатор дома, fk:House.
   - `serial_number` — серийный номер устройства.
   - `status` — текущее состояние устройства - on/off.

### 4. DeviceType
   - `id` — pk.
   - `name` — название типа устройства.

### 5. TelemetryData
   - `id` — pk.
   - `device_id` — идентификатор устройства, которое сгенерировало телеметрию, fk:Device.
   - `timestamp` — временная метка записи.
   - `data` — jsonb данные телеметрии.

### 6. ScenarioSchedule
   - `id` - pk.
   - `house_id` - идентификатор дома, fk:House.
   - `scenario_plan` - jsonb план поведения теплого дома.
   - `cron` - крон исполнения

### 7. ScenarioScheduleDevice
   - `scenario_id` - fk:ScenarioSchedule.
   - `device_id` - fk:Device

## Связи между сущностями

1. User-House: one-to-many.
2. House-Device: one-to-many.
3. Device-DeviceType: one-to-many.
4. Device-TelemetryData: one-to-many.
5. House-ScenarioSchedule: one-to-many.
6. Device-ScenarioSchedule: many-to-many

## Объяснение диаграммы

- **User**: Содержит информацию о пользователях.
- **House**: Связан с пользователем через fk.
- **Device**: Связан с домом и устройством через fk'ии, и множествами сценариев через ScenarioScheduleDevice, many-to-many таблицу.
- **DeviceType**: Содержит информацию о типах устройств.
- **TelemetryData**: Связан с устройством через fk.
- **ScenarioSchedule**: Связан с домом через fk, так же со множеством устройств через ScenarioScheduleDevice