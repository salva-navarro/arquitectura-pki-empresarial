# Arquitectura PKI Empresarial

Autor: Salva Navarro  
Perfil: Arquitecto de Infraestructuras de Clave Pública  
Ubicación: España  

---

## 1. Introducción

Una Infraestructura de Clave Pública (PKI) empresarial no es un servicio accesorio.
Es un componente estructural de la arquitectura de seguridad de la organización.

Cuando está mal diseñada, genera deuda criptográfica.
Cuando está bien definida, se convierte en un habilitador de confianza transversal.

Este documento recoge principios técnicos de diseño orientados a entornos empresariales con requisitos reales de disponibilidad, segregación y gobernanza.

---

## 2. Principios de Diseño

### 2.1 Separación estructural

- Autoridad Raíz (Root CA) permanentemente offline.
- Autoridades emisoras segmentadas.
- Separación administrativa estricta.
- Red diferenciada para servicios PKI críticos.

La PKI no debe depender de la salud del dominio principal.

---

### 2.2 Modelo de Jerarquía

Modelo base recomendado:

- Root CA offline.
- Issuing CA online.
- Integración con HSM cuando el nivel de criticidad lo requiera.
- Planificación explícita de CRL y OCSP.

La simplicidad estructural es preferible a arquitecturas sobrecomplicadas.

---

### 2.3 Gobierno Criptográfico

Una PKI empresarial exige:

- Políticas de emisión documentadas.
- Inventario completo de certificados.
- Gestión formal de revocaciones.
- Definición de SLAs internos.
- Revisión periódica de algoritmos y longitudes de clave.

Sin gobierno, la PKI degenera en emisión descontrolada.

---

### 2.4 Gestión del Ciclo de Vida

- Renovación anticipada planificada.
- Automatización controlada.
- Monitorización de expiraciones.
- Procedimientos de contingencia ante revocaciones masivas.

El riesgo operativo en PKI suele estar en el ciclo de vida, no en la criptografía.

---

### 2.5 Alineación con Zero Trust

- mTLS bajo control de arquitectura.
- Certificados no como bypass de políticas.
- Integración con postura de identidad.

PKI no sustituye identidad.
La complementa.

---

### 2.6 Preparación Post-Cuántica

- Inventario criptográfico previo.
- Evaluación de algoritmos vulnerables.
- Estrategia de agilidad criptográfica.
- Roadmap realista de transición.

No se trata de migrar mañana.
Se trata de estar preparado.

---

## 3. Enfoque

Este repositorio está centrado exclusivamente en arquitectura técnica.

No incluye:
- Marketing de seguridad.
- Recomendaciones comerciales.
- Discursos genéricos.

Su objetivo es documentar patrones de diseño y criterios de decisión en entornos empresariales reales.

---

Sitio oficial: https://salva-navarro.github.io
