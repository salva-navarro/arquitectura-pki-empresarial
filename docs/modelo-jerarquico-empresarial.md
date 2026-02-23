# Modelo Jerárquico de PKI Empresarial

## 1. Justificación del modelo jerárquico

La confianza en una PKI es transitiva y acumulativa.

Si una Root CA firma una CA subordinada,
y esta firma certificados finales,
la validez del sistema completo depende estructuralmente de la integridad de la raíz.

Por tanto, el diseño jerárquico no es una recomendación académica.
Es una exigencia estructural.

En entorno empresarial, el modelo mínimo aceptable es:

- 1 Root CA (offline)
- 1 o más Issuing CA (online)

Todo lo que sea menos que eso es simplificación peligrosa.
Todo lo que sea más debe estar justificado.

---

## 2. Root CA — Diseño y decisiones críticas

### 2.1 Principio fundamental

La Root CA es el ancla de confianza.
Su compromiso implica reconstrucción completa de la jerarquía.

No es un servidor.
Es un activo estratégico.

### 2.2 Requisitos estructurales

Una Root CA empresarial debe:

- Permanecer offline de forma permanente.
- No estar unida al dominio.
- Activarse únicamente bajo procedimiento formal.
- Tener acceso físico restringido.
- Generar su clave privada en entorno controlado.

Si la Root CA está siempre encendida “por comodidad”, no es una raíz. Es un riesgo.

---

### 2.3 Custodia de clave privada

Opciones habituales:

- Almacenamiento en software cifrado.
- HSM externo.
- HSM interno certificado.

Criterio arquitectónico:

Si la PKI soporta sistemas críticos (financieros, regulatorios, industriales),
la clave raíz debe residir en HSM.

No porque lo diga el fabricante.
Porque reduce superficie de ataque y riesgo de extracción.

---

### 2.4 Activación controlada

La Root CA solo debería activarse para:

- Firmar una nueva CA subordinada.
- Renovar certificados de subordinadas.
- Publicar nueva CRL raíz.
- Revocación excepcional de subordinada.

Cada activación debe:

- Estar documentada.
- Estar auditada.
- Seguir procedimiento formal.
- Generar evidencia.

No es paranoia. Es arquitectura responsable.

---

## 3. Issuing CA — Diseño operativo

La CA emisora es el componente con mayor exposición.

Es la que:

- Emite certificados.
- Interactúa con usuarios y sistemas.
- Publica CRL.
- Gestiona solicitudes.

Por tanto, es el punto más probable de compromiso.

---

### 3.1 Segmentación de red

Debe estar:

- En red segmentada.
- Sin acceso directo desde red de usuario.
- Con acceso administrativo restringido.
- Con separación entre plano de gestión y plano de emisión.

Una CA emisora accesible desde cualquier segmento interno es un error estructural.

---

### 3.2 Integración con dominio

Existen dos enfoques:

1. CA integrada en dominio corporativo.
2. CA en bosque dedicado de administración (tiered model).

Criterio:

En entornos de criticidad media, integración controlada puede ser aceptable.

En entornos regulados o de alta criticidad,
la CA emisora debe estar en entorno administrativo segregado.

Si el dominio cae, la PKI no debería caer con él.

---

### 3.3 Protección de claves privadas

Las claves de la CA emisora deben:

- Estar protegidas con HSM si el nivel de criticidad lo requiere.
- Tener backups cifrados.
- Estar sujetas a control de acceso estricto.
- Ser auditables.

Una CA emisora comprometida puede generar certificados válidos fraudulentos.
Ese es el riesgo real.

---

## 4. Diseño de CRL y OCSP

Este es uno de los puntos más ignorados en PKI empresariales.

Y luego llegan los problemas.

### 4.1 CRL (Certificate Revocation List)

Debe definirse:

- Intervalo de publicación.
- Tamaño máximo esperado.
- Ubicación accesible y redundante.
- Alta disponibilidad.

Una CRL mal dimensionada puede:

- Generar latencias.
- Bloquear autenticaciones.
- Saturar servicios.

La planificación de CRL no es un detalle operativo.
Es diseño estructural.

---

### 4.2 OCSP

OCSP permite validación más dinámica.

Debe considerarse cuando:

- El volumen de certificados es elevado.
- La latencia de CRL no es aceptable.
- Se requiere validación en tiempo casi real.

Pero OCSP introduce:

- Nuevo punto de dependencia.
- Nuevo vector de ataque.
- Nueva necesidad de alta disponibilidad.

Nada es gratis en arquitectura.

---

## 5. Escenarios de compromiso

La arquitectura debe contemplar:

### 5.1 Compromiso de CA emisora

Impacto:

- Revocación de subordinada.
- Reemisión masiva.
- Impacto operativo elevado.

Mitigación estructural:

- Segregación.
- Monitorización.
- Procedimientos claros de revocación.

---

### 5.2 Compromiso de Root CA

Impacto:

- Reemplazo total de jerarquía.
- Pérdida de confianza global.
- Reinstalación completa.

Mitigación:

- Aislamiento extremo.
- Procedimientos estrictos.
- HSM.
- Custodia formal.

Si ocurre, no es incidente.
Es evento estratégico.

---

## 6. Consideraciones de escalabilidad

La arquitectura debe anticipar:

- Incremento de emisión.
- Integración con cloud.
- Integración con DevOps.
- Automatización de ciclo de vida.

Diseñar solo para el presente garantiza rediseñar en dos años.

Y nadie quiere migrar una PKI en producción sin necesidad.

---

## 7. Conclusión del Modelo Jerárquico

Una PKI empresarial bien diseñada no es la más compleja.

Es la más clara.

- Root aislada.
- Issuing segmentadas.
- Gobierno definido.
- Ciclo de vida planificado.
- Evolución prevista.

Y, sobre todo,
sin atajos por comodidad.

Porque en PKI,
los atajos se pagan caros.
