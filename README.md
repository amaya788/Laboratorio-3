# Laboratorio-3
🖧 Laboratorio 3 - Topologías de Red con Arduino

👥 Autores

· David Esteban Diaz Castro
· Ferney Arturo Amaya Gómez
· Jhonny Alejandro Mejia

En este repositorio de GitHub encontrarás la implementación completa de diferentes topologías de red junto con la configuración de switches y comunicación con Arduino, desarrollado como parte del Laboratorio 3 de la Universidad Santo Tomás.

📋 Descripción General

Este proyecto implementa cuatro topologías de red diferentes, cada una con sus características únicas, protocolos de comunicación y integración con sistemas embebidos Arduino:

· 🔷 Topología en Estrella - Comunicación centralizada
· 🌳 Topología en Árbol - Estructura jerárquica
· ⭕ Topología en Anillo - Sistema de token
· 🔷 Topología en Malla Parcial - Comunicación redundante

🏗️ Topologías Implementadas

<h2><p align="center"> <b>🔷 Topología en Estrella</b></h2>

La topología en estrella consiste en un servidor central que gestiona todas las comunicaciones entre los nodos clientes. El Arduino está conectado al servidor central.

Características:

· ✅ Centralizada y fácil de administrar
· ⚠️ Punto único de fallo
· 🔄 Comunicación a través de servidor central
· 🔌 Integración con Arduino en el nodo central

Componentes:

· Arduino conectado al servidor central
· Raspberry Pi como servidor central
· Múltiples Raspberry Pi como nodos clientes

<h2><p align="center"> <b>🌳 Topología en Árbol</b></h2>

La topología en árbol organiza los nodos de forma jerárquica, con un nodo raíz, nodos rama intermedios y nodos hoja finales.

Características:

· 📊 Estructura jerárquica y escalable
· 🎯 Organización por niveles
· 🛣️ Comunicación a través de rutas definidas
· 🔌 Arduino integrado en nodos específicos

Estructura:

· 🌳 Raíz (192.168.40.101) - Nodo principal con Arduino
· 🌿 Ramas (192.168.40.102, 192.168.40.103) - Nodos intermedios
· 🍃 Hojas (192.168.40.104-107) - Nodos finales

<h2><p align="center"> <b>⭕ Topología en Anillo</b></h2>

La topología en anillo implementa un sistema de token donde solo el nodo que posee el token puede comunicarse con el Arduino.

Características:

· 🎫 Sistema de token para control de acceso
· 🔄 Comunicación unidireccional
· ⚠️ Susceptible a fallos en cadena
· 🔌 Arduino conectado en PC3

Funcionamiento:

· 🔁 Token circula continuamente por el anillo
· 🎯 Solo el nodo con token puede enviar comandos al Arduino
· 🔍 Detección y manejo de nodos caídos

<h2><p align="center"> <b>🔷 Topología en Malla Parcial</b></h2>

La topología en malla parcial proporciona múltiples caminos de comunicación entre nodos, ofreciendo redundancia y tolerancia a fallos.

Características:

· 🛣️ Múltiples caminos de comunicación
· 🔄 Redundancia y tolerancia a fallos
· ⚠️ Mayor complejidad en la configuración
· 🌊 Flooding para enrutamiento de mensajes

Conexiones:

· 🖥️ PC1 (192.168.40.101) - Conecta a PC2 y PC3
· 🖥️ PC2 (192.168.40.102) - Conecta a PC1 y PC4
· 🖥️ PC3 (192.168.40.103) - Con Arduino, conecta a PC1 y PC4
· 🖥️ PC4 (192.168.40.104) - Conecta a PC2 y PC3

⚙️ Configuración del Switch

Comandos de Configuración

```bash
enable
configure terminal
host-name David
interface vlan 1
ip address 192.168.80.1 255.255.255.0
no shutdown
exit

# Configuración de puertos
interface fastethernet 0/1
description PC1
switchport mode access
no shutdown
exit

interface fastethernet 0/2
description PC2
switchport mode access
no shutdown
exit

interface fastethernet 0/3
description PC3
switchport mode access
no shutdown
exit

interface fastethernet 0/4
description PC4
switchport mode access
no shutdown
exit

end
write memory
```

Configuración de PCs

PC1:

```bash
netsh interface ip set address "Ethernet" static 192.168.80.101 255.255.255.0 192.168.80.1
ping 192.168.80.102
ping 192.168.80.103
ping 192.168.80.104
ping 192.168.80.1
```

PC2:

```bash
netsh interface ip set address "Ethernet" static 192.168.80.102 255.255.255.0 192.168.80.1
ping 192.168.80.101
ping 192.168.80.103
ping 192.168.80.104
ping 192.168.80.1
```

📁 Estructura del Proyecto

```
Laboratorio_3/
├── 📁 topologia_estrella/
│   ├── 🐍 servidor_estrella.py
│   ├── 🐍 cliente_estrella.py
│   └── 🔌 arduino_estrella.ino
├── 📁 topologia_arbol/
│   ├── 🐍 nodo_arbol.py
│   └── 🔌 arduino_arbol.ino
├── 📁 topologia_anillo/
│   ├── 🐍 nodo_anillo.py
│   └── 🔌 arduino_anillo.ino
├── 📁 topologia_malla/
│   ├── 🐍 nodo_malla.py
│   └── 🔌 arduino_malla.ino
├── 📁 configuracion_switch/
│   └── 📄 comandos_switch.txt
├── 📁 documentacion/
│   ├── 📄 manual_instalacion.md
│   └── 📄 guia_configuracion.md
└── 📄 README.md
```

🚀 Instalación y Uso

Prerrequisitos

· Python 3.7+
· Arduino IDE
· PuTTY o terminal SSH
· Switch configurable
· Múltiples PCs/Raspberry Pis

Configuración Inicial

1. Clonar el repositorio:

```bash
git clone https://github.com/tu-usuario/laboratorio-3-redes.git
cd laboratorio-3-redes
```

1. Configurar el switch usando los comandos proporcionados
2. Configurar las IPs estáticas en cada PC
3. Cargar el código Arduino en cada dispositivo

Ejecución por Topología

Estrella:

```bash
cd topologia_estrella
python servidor_estrella.py  # En el servidor central
python cliente_estrella.py   # En los nodos clientes
```

Árbol:

```bash
cd topologia_arbol
python nodo_arbol.py
```

Anillo:

```bash
cd topologia_anillo
python nodo_anillo.py
```

Malla:

```bash
cd topologia_malla
python nodo_malla.py
```

🔌 Integración con Arduino

Comandos Arduino Soportados

```arduino
ON      # 🔆 Encender LED
OFF     # 💡 Apagar LED  
STATUS  # 📊 Consultar estado
```

Código Base Arduino

```arduino
const int LED_PIN = 13;
int contador = 0;

void setup() {
    pinMode(LED_PIN, OUTPUT);
    Serial.begin(9600);
    delay(2000);
    Serial.println("ARDUINO - COMANDOS: ON, OFF, STATUS");
}

void loop() {
    if (Serial.available() > 0) {
        String comando = Serial.readStringUntil('\n');
        comando.trim();
        comando.toUpperCase();
        
        Serial.print("Comando: ");
        Serial.println(comando);
        
        if (comando == "ON") {
            digitalWrite(LED_PIN, HIGH);
            Serial.println("LED ENCENDIDO");
        }
        else if (comando == "OFF") {
            digitalWrite(LED_PIN, LOW);
            Serial.println("LED APAGADO");
        }
        else if (comando == "STATUS") {
            Serial.println("ARDUINO ACTIVO");
        }
        else {
            Serial.println("COMANDO NO RECONOCIDO");
        }
    }
    delay(100);
}
```

📊 Resultados y Conclusiones

Comparativa de Topologías

Topología ✅ Ventajas ⚠️ Desventajas 🎯 Caso de Uso
🔷 Estrella Fácil administración Centralizada Punto único de fallo Tráfico concentrado Redes pequeñas Control centralizado
🌳 Árbol Escalable Organizada Complejidad Dependencia jerárquica Redes corporativas Estructuras grandes
⭕ Anillo Acceso ordenado Simple Fallos en cadena Latencia Redes industriales Control de acceso
🔷 Malla Redundante Tolerante a fallos Complejidad Overhead Críticas Alta disponibilidad

Conclusiones

· ✅ Se demostró la implementación exitosa de cuatro topologías de red diferentes
· 🔌 Todas las topologías permitieron la integración con sistemas embebidos Arduino
· 📡 Cada topología presenta ventajas y desventajas específicas según el caso de uso
· 🔄 La comunicación socket TCP/IP demostró ser robusta para aplicaciones distribuidas
· 📨 El sistema de mensajes JSON permitió una comunicación flexible y extensible
· 🎯 La integración hardware-software se logró exitosamente en todos los escenarios

🛠️ Troubleshooting

Problemas Comunes

1. Conexión rechazada:
   · Verificar que el servidor esté ejecutándose
   · Confirmar IPs y puertos correctos
2. Arduino no detectado:
   · Verificar puerto COM
   · Revisar conexión USB
   · Confirmar baud rate (9600)
3. Ping fallido:
   · Revisar configuración de IP estática
   · Verificar máscara de red y gateway
   · Comprobar cables de red

Comandos de Verificación

```bash
# Verificar configuración IP
ipconfig /all

# Probar conectividad
ping 192.168.80.101
ping 192.168.80.102

# Verificar servicios
netstat -an | findstr 11000
```

👥 Autores

· David Esteban Diaz Castro
· Ferney Arturo Amaya Gómez
· Jhonny Alejandro Mejia

Universidad Santo Tomás
Facultad de Ingeniería
Octubre 5, 2025

📄 Licencia

Este proyecto es parte del trabajo académico de la Universidad Santo Tomás y se comparte con fines educativos.

---

<p align="center">
  <b>🖧 Laboratorio 3 - Topologías de Red con Arduino 🖧</b><br>
  <i>Implementación práctica de redes de computadoras con sistemas embebidos</i>
</p>

<div align="center">

https://img.shields.io/badge/Python-3.7%2B-blue?logo=python
https://img.shields.io/badge/Arduino-Compatible-green?logo=arduino
https://img.shields.io/badge/License-Academic-blue.svg

</div>
