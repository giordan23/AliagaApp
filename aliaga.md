# Sistema de Gestión de Compras y Caja

## Índice
1. [Descripción General](#1-descripción-general)
2. [Estructura de la Aplicación](#2-estructura-de-la-aplicación)
3. [Procesos Clave](#3-procesos-clave)
4. [Características Especiales](#4-características-especiales)
5. [Consideraciones Técnicas](#5-consideraciones-técnicas)
6. [Especificaciones Técnicas](#6-especificaciones-técnicas)
7. [Estructura del Proyecto](#7-estructura-del-proyecto)
8. [Base de Datos](#8-base-de-datos)

## 1. Descripción General

Esta aplicación está diseñada para gestionar operaciones comerciales, incluyendo compras, ventas, adelantos y control de caja. El sistema proporciona una interfaz intuitiva para manejar todas las operaciones relacionadas con el negocio.

## 2. Estructura de la Aplicación

### 2.1 Página de Inicio

La página principal contiene cuatro botones principales de navegación:
* COMPRAR
* VENDER
* CAJA
* ADELANTOS

### 2.2 Página de Operaciones

**Funcionalidades principales:**
* Registro de compras
* Registro de ventas
* Gestión de adelantos
* Modificación de precios de compra por calidad:
  * Húmedo
  * Estándar
  * Seco
* Visualización de saldo disponible

### 2.3 Página de Caja

**Funcionalidades de gestión financiera:**
* Visualización de movimientos diarios:
  * Montos de apertura
  * Montos de cierre
  * Diferencias
* Control de saldo disponible
* Gestión de ingresos y retiros
* Operaciones de caja chica:
  * Descripción
  * Monto
  * Tipo (ingreso/egreso)

### 2.4 Página de Clientes

**Gestión y seguimiento de clientes:**
* Lista de clientes con adelantos pendientes
* Registro de ventas recibidas:
  * Cantidad en kilos
  * Calidad del producto
  * Zona
  * Montos
* Registro de ventas realizadas:
  * Cantidad en kilos
  * Calidad del producto
  * Montos
* Gestión de información de contacto:
  * Teléfono
  * Dirección
  * Zona

### 2.5 Página de Reportes

**Generación de reportes filtrados por:**
* Productos
* Calidad
* Fechas
* Zonas
* Valores monetarios

## 3. Procesos Clave

### 3.1 Proceso de Compra

1. Inicio desde botón "COMPRAR"
2. Redirección a página "Ingresar Cliente"
3. Proceso de registro de compra

### 3.2 Gestión de Saldo

**Operaciones que afectan el saldo disponible:**
* Ingresos
* Compras
* Adelantos
* Operaciones de caja chica

*Nota: Las ventas no afectan el saldo disponible*

## 4. Características Especiales

### 4.1 Autocompletado

El campo de ingreso de cliente cuenta con función de autocompletado.

### 4.2 Gestión Automática de Caja

#### Apertura de Caja
* Se activa con la primera operación de compra del día
* Verificación de cierre del día anterior
* Modal de confirmación si no hay cierre previo:
  ```
  "La caja no se ha cerrado ayer. ¿Desea aperturar la caja de hoy con S/.XYZ?"
  ```
  * Input editable para monto XYZ
  * En caso de rechazo: "No es posible registrar la compra porque no hay un monto de apertura de caja"

**El monto XYZ:**
* Se registra como cierre del día anterior
* Se usa como apertura del día actual

#### Cierre de Caja
* Proceso automático
* Respaldo con cierre manual en la siguiente apertura automática

## 5. Consideraciones Técnicas

### 5.1 Validaciones Importantes
* Verificación de cierre de caja anterior
* Control de saldos disponibles
* Registro correcto de operaciones que afectan el saldo

### 5.2 Interfaz de Usuario
* Diseño intuitivo con botones principales
* Formularios con autocompletado
* Modales para confirmaciones importantes

### 5.3 Gestión de Datos
* Seguimiento de operaciones por cliente
* Control de calidades de producto
* Registro de zonas geográficas
* Histórico de precios por calidad

### 5.4 Características Fundamentales
* Aplicación móvil optimizada para tablet
* Operaciones CRUD con lógica de negocio específica
* Capacidad de trabajo offline
* Operaciones críticas (manejo de dinero y transacciones)
* Rendimiento rápido y responsive

### 5.5 Consideraciones de Implementación
* Rendimiento optimizado para dispositivos móviles
* Gestión eficiente del estado local
* Sistema robusto de persistencia de datos
* Validaciones de negocio claramente definidas
* Diseño enfocado en mantenibilidad
* Arquitectura testeable
* Experiencia de usuario fluida

### 5.6 Arquitectura del Sistema

**Estructura de Capas:**
```
SistemaGestion/
├── Domain/     # Entidades y reglas de negocio core
├── Application/# Casos de uso y lógica de aplicación
├── Infrastructure/# Implementaciones técnicas (BD, etc)
└── Presentation/  # UI y ViewModels
```

**Patrones de Diseño Implementados:**
* Repository Pattern para acceso a datos
* MVVM (integrado con MAUI)
* Services para lógica de negocio reutilizable

## 6. Especificaciones Técnicas

### 6.1 Hardware (Tablet)
* Resolución de pantalla: 1280x800 (WXGA)
* Aspect ratio: 16:10
* Densidad de pantalla: mdpi/hdpi

### 6.2 Emulador (Visual Studio Device Manager)
* API Level: 33 (Android 13.0 Tiramisu)
* RAM asignada: 2GB (considerando PC de 8GB)
* Almacenamiento: 2GB
* CPU: 2 cores

### 6.3 Tecnologías
* Framework: .NET MAUI 8
* Target: net8.0-android
* Frontend: Material Design
* Base de datos: SQLite (local)
* IDE: Visual Studio Community 2022

### 6.4 Paquetes NuGet Principales
* CommunityToolkit.Maui.Material
* Microsoft.Maui.Controls.MaterialDesignControls
* Microsoft.EntityFrameworkCore.Sqlite

## 7. Estructura del Proyecto

### 7.1 Configuración Inicial

**Proyecto Principal:**
* Creación de solución en Visual Studio 2022
* Proyecto .NET MAUI principal: AliagaApp

**Configuración Android:**
* Target Android Version: Android 13.0 (API 33)
* Minimum Android Version: Android 11.0 (API 30)
* Package Format: Android APK

**Configuración de ventana:**
* Width: 1280
* Height: 800

### 7.2 Proyectos de la Solución

**AliagaApp (Proyecto Principal MAUI)**
* Views/
* ViewModels/
* Controls/
* Helpers/
* Resources/

**AliagaApp.Domain**
* Entities/
* Interfaces/
* Enums/
* Exceptions/

**AliagaApp.Application**
* Common/
* Interfaces/
* Services/
* DTOs/
* Validators/

**AliagaApp.Infrastructure**
* Data/
* Configurations/
* Repositories/
* Services/

### 7.3 Referencias entre Proyectos
* AliagaApp (principal) → Application, Infrastructure
* Application → Domain
* Infrastructure → Domain, Application

## 8. Base de Datos

### 8.1 Descripción General

Este sistema está diseñado para gestionar operaciones de caja, incluyendo movimientos financieros, control de clientes, productos y adelantos. La base de datos está implementada en SQLite.

### 8.2 Estructura de Tablas

#### USUARIO
**Gestiona los usuarios del sistema**
* `id_usuario`: Identificador único (AUTO)
* `nombre`: Nombre del usuario
* `rol`: Rol asignado
* `activo`: Estado del usuario (1=activo, 0=inactivo)

#### CAJA
**Representa las cajas disponibles en el sistema**
* `id_caja`: Identificador único (AUTO)
* `nombre`: Nombre de la caja
* `saldo_actual`: Saldo disponible (default: 0)
* `estado`: Estado de la caja (1=activo, 0=inactivo)

#### CAJA_CHICA
**Gestiona cajas chicas asociadas a cajas principales**
* `id_caja_chica`: Identificador único (AUTO)
* `id_caja`: Referencia a CAJA
* `monto_maximo`: Límite máximo permitido
* `saldo_actual`: Saldo disponible (default: 0)
* `estado`: Estado (1=activo, 0=inactivo)

#### CLIENTE
**Almacena información de clientes**
* `id_cliente`: Identificador único (AUTO)
* `nombre`: Nombre del cliente
* `documento`: Número de documento
* `telefono`: Contacto telefónico
* `zona`: Zona geográfica
* `estado`: Estado del cliente (1=activo, 0=inactivo)

#### PRODUCTO
**Catálogo de productos**
* `id_producto`: Identificador único (AUTO)
* `nombre_producto`: Nombre del producto
* `calidad`: Calidad del producto
* `precio_compra`: Precio de compra

#### TIPO_MOVIMIENTO
**Define los tipos de movimientos permitidos**
* `id_tipo_movimiento`: Identificador único (AUTO)
* `nombre`: Nombre del tipo de movimiento
* `naturaleza`: INGRESO o EGRESO

#### ADELANTO
**Gestiona adelantos a clientes**
* `id_adelanto`: Identificador único (AUTO)
* `id_cliente`: Cliente asociado
* `monto_total`: Monto total del adelanto
* `monto_pendiente`: Saldo pendiente
* `estado`: PENDIENTE o PAGADO
* `fecha_adelanto`: Fecha de registro
* `fecha_limite`: Fecha límite de pago

#### MOVIMIENTO_CAJA
**Registra todas las operaciones de caja**
* `id_movimiento`: Identificador único (AUTO)
* `id_caja`: Caja asociada
* `id_tipo_movimiento`: Tipo de movimiento
* `id_usuario`: Usuario que realiza la operación
* `id_cliente`: Cliente involucrado
* `id_adelanto`: Adelanto asociado (opcional)
* `monto_total`: Monto total del movimiento
* `referencia`: Referencia del movimiento
* `fecha_hora`: Fecha y hora del registro

#### DETALLE_MOVIMIENTO
**Detalle de productos en cada movimiento**
* `id_detalle`: Identificador único (AUTO)
* `id_movimiento`: Movimiento asociado
* `id_producto`: Producto
* `peso_kg`: Peso en kilogramos
* `descuento_kg`: Descuento en kilogramos
* `peso_final_kg`: Peso final después del descuento
* `precio_aplicado`: Precio unitario aplicado
* `subtotal`: Monto total del detalle

#### APERTURA_CIERRE
**Control de apertura y cierre de cajas**
* `id_apertura_cierre`: Identificador único (AUTO)
* `id_caja`: Caja asociada
* `id_usuario`: Usuario responsable
* `monto_apertura`: Monto inicial
* `monto_cierre`: Monto final
* `diferencia`: Diferencia entre apertura y cierre
* `fecha_apertura`: Fecha y hora de apertura
* `fecha_cierre`: Fecha y hora de cierre
* `observaciones`: Notas adicionales

### 8.3 Triggers

#### calcular_subtotal_peso
**Propósito**: Calcula automáticamente el peso final y subtotal en DETALLE_MOVIMIENTO
* Verifica que el peso final no sea negativo
* Calcula el peso final (peso_kg - descuento_kg)
* Calcula el subtotal (peso_final_kg * precio_aplicado)
* Se ejecuta ANTES de INSERT en DETALLE_MOVIMIENTO

#### actualizar_monto_total
**Propósito**: Actualiza el monto total en MOVIMIENTO_CAJA
* Suma todos los subtotales de DETALLE_MOVIMIENTO
* Actualiza monto_total en MOVIMIENTO_CAJA
* Se ejecuta DESPUÉS de INSERT en DETALLE_MOVIMIENTO

#### actualizar_saldo_caja
**Propósito**: Actualiza el saldo de la caja según el tipo de movimiento
* Para INGRESO: suma el monto_total al saldo_actual
* Para EGRESO: resta el monto_total al saldo_actual
* Se ejecuta DESPUÉS de INSERT en MOVIMIENTO_CAJA

#### actualizar_adelanto
**Propósito**: Actualiza el estado de los adelantos cuando se registran pagos
* Reduce el monto pendiente del adelanto
* Actualiza el estado a 'PAGADO' si el monto pendiente llega a 0
* Se ejecuta DESPUÉS de INSERT en MOVIMIENTO_CAJA cuando hay id_adelanto

### 8.4 Relaciones Principales
* CAJA_CHICA → CAJA
* MOVIMIENTO_CAJA → CAJA, TIPO_MOVIMIENTO, USUARIO, CLIENTE, ADELANTO
* DETALLE_MOVIMIENTO → MOVIMIENTO_CAJA, PRODUCTO
* ADELANTO → CLIENTE
* APERTURA_CIERRE → CAJA, USUARIO

### 8.5 Consideraciones de Diseño
1. Sistema de doble entrada para movimientos (ingresos/egresos)
2. Control de peso y descuentos en productos
3. Gestión de adelantos con seguimiento de pagos
4. Control de apertura/cierre de caja con balance
5. Sistema de usuarios con roles y estados