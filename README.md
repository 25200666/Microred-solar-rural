# Microred solar rural

Proyecto final de **Arquitectura del Computador** (2026-2) con Raspberry Pi Pico 2 W.

**Equipo:** Byte me  

**Integrantes:** Paul Adrian Horna Yarasca,  Michelle Grace Curi Silva  

**Proyecto:** N.º 10, Microred solar rural  


## Problema

Muchas comunidades rurales usan paneles solares con batería, pero no tienen forma de saber cuánta energía generan ni en qué estado está la batería. Si la batería se descarga por completo con frecuencia, se daña y la comunidad se queda sin electricidad sin previo aviso. Además, un panel fijo desaprovecha parte de la radiación solar.

## Qué hace el sistema

- Mide el voltaje, la corriente y la potencia del panel y de la batería.
- Mide la irradiancia (luz solar) disponible.
- Orienta el panel hacia el sol con un seguidor de un eje (servo).
- Publica los datos en la nube y los muestra en un dashboard.
- Envía una alerta de descarga profunda cuando la batería baja de un umbral.

## Hardware

| Componente | Interfaz | Función |
|---|---|---|
| Raspberry Pi Pico 2 W | — | Microcontrolador (RP2350) |
| INA219 (panel) | I2C | Voltaje y corriente del panel |
| INA219 (batería) | I2C | Voltaje y corriente de la batería |
| BH1750 | I2C | Irradiancia |
| Servo | PWM | Seguidor solar de un eje |
| Panel solar y batería con módulo de carga protegido | — | Fuente de energía a monitorear |

Los dos INA219 comparten el bus I2C con direcciones distintas.

## Reto de arquitectura

**Dos núcleos del RP2350** : un núcleo se encarga de la adquisición de sensores y del servo, y el otro de la comunicación Wi-Fi y la nube. Se medirá la regularidad del muestreo y el tiempo del ciclo de lectura con uno y con dos núcleos.

## Software

- MicroPython en la Pico 2 W
- Multitarea con `asyncio` (lectura de sensores, envío a la nube y lógica de alertas)
- Nube: [MQTT con HiveMQ o Adafruit IO / HTTP con ThingSpeak]. Por definir.

## Estructura del repositorio

```
.
├── README.md
├── src/          # código MicroPython comentado
├── docs/         # diagrama de conexiones y capturas
└── cad/          # archivos de la pieza 3D (STL y 3MF)
```

## Estado del proyecto

- [x] Elección del proyecto y definición del problema
- [x] Primer diseño de la pieza 3D (prueba en el FabLab)
- [ ] Sensores leyendo en protoboard
- [ ] Diagrama de conexiones
- [ ] Integración con asyncio
- [ ] Conectividad y dashboard
- [ ] Reto de arquitectura y medición
- [ ] Paper y defensa final
