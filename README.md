# 🔐 Informe de Pruebas de Seguridad - Sistema de Contraseñas

## ℹ️ Información del Proyecto

| Campo | Valor |
|-------|-------|
| **Empresa** | Departamento de Desarrollo |
| **Proyecto** | Validación del sistema de autenticación |
| **Tipo de prueba** | Pruebas de seguridad y usuario |
| **Alumno** | Santiago |
| **Módulo** | Desarrollo de Interfaces - Unidad 8 |
| **Fecha** | Enero 2026 |

---

## 1. Objetivo de las Pruebas

Evaluar la robustez del sistema de autenticación mediante contraseñas, verificando diferentes niveles de complejidad para determinar las políticas de seguridad que debe implementar la aplicación antes de su despliegue.

---

## 2. Herramientas Utilizadas

Se han utilizado dos herramientas profesionales de verificación de contraseñas:

| Herramienta | URL | Características |
|-------------|-----|-----------------|
| **Kaspersky Password Checker** | password.kaspersky.com | Verifica filtraciones, analiza componentes (números, símbolos, mayúsculas) |
| **Cyberprotector** | cyberprotector.com | Calcula tiempo de hackeo, verifica bases de datos comprometidas |

---

## 3. Casos de Prueba Ejecutados

### Prueba 1: Solo Números
- **Contraseña probada:** `12345`
- **Longitud:** 5 caracteres

| Herramienta | Resultado |
|-------------|-----------|
| Kaspersky | Apareció 3.998.166 veces en filtraciones |
| Cyberprotector | Encontrada 31.033.620 veces. Tiempo: NADA |

**Veredicto:** 🔴 MUY DÉBIL - Inaceptable para cualquier sistema

---

### Prueba 2: Solo Letras Minúsculas
- **Contraseña probada:** `contraseña`
- **Longitud:** 10 caracteres

| Herramienta | Resultado |
|-------------|-----------|
| Kaspersky | Apareció 101 veces. Faltan: números, símbolos, mayúsculas |
| Cyberprotector | Encontrada 162.268 veces. Tiempo teórico: 2.000 años |

**Veredicto:** 🔴 DÉBIL - Ya está comprometida, no usar

---

### Prueba 3: Mayúsculas y Minúsculas
- **Contraseña probada:** `CoNtrAseÑa`
- **Longitud:** 10 caracteres

| Herramienta | Resultado |
|-------------|-----------|
| Kaspersky | Sin fugas ✓ Faltan: números, símbolos |
| Cyberprotector | No comprometida ✓ Tiempo: 13.000 años |

**Veredicto:** 🟡 MEDIA - Mejorable, pero aceptable para uso básico

---

### Prueba 4: Letras y Números
- **Contraseña probada:** `Contraseña12345`
- **Longitud:** 15 caracteres

| Herramienta | Resultado |
|-------------|-----------|
| Kaspersky | Apareció 1 vez. Faltan: símbolos |
| Cyberprotector | No comprometida ✓ Tiempo: 352 cuatrillones de años |

**Veredicto:** 🟡 MEDIA-ALTA - La longitud compensa la falta de símbolos

---

### Prueba 5: Con Símbolos pero Corta
- **Contraseña probada:** `Cl@v3!`
- **Longitud:** 6 caracteres

| Herramienta | Resultado |
|-------------|-----------|
| Kaspersky | Sin fugas ✓ Tiene números, símbolos, mayúsculas. Falta: longitud |
| Cyberprotector | No comprometida ✓ Tiempo: **21 SEGUNDOS** |

**Veredicto:** 🔴 MUY DÉBIL - La longitud corta anula toda la complejidad

---

### Prueba 6: +10 Caracteres con Todo
- **Contraseña probada:** `M1Cl@v3Segur@2025!`
- **Longitud:** 18 caracteres

| Herramienta | Resultado |
|-------------|-----------|
| Kaspersky | Sin fugas ✓ Tiene TODO: números, símbolos, mayúsculas |
| Cyberprotector | No comprometida ✓ Tiempo: **146 quintillones de años** |

**Veredicto:** 🟢 MUY FUERTE - Contraseña ideal para sistemas críticos

---

## 4. Tabla Resumen de Resultados

| # | Tipo | Contraseña | Filtrada | Tiempo Hackeo | Nivel |
|---|------|------------|----------|---------------|-------|
| 1 | Solo números | `12345` | ❌ Sí (millones) | Instantáneo | 🔴 Muy débil |
| 2 | Solo minúsculas | `contraseña` | ❌ Sí (162.268) | 2.000 años* | 🔴 Débil |
| 3 | Mayús + minús | `CoNtrAseÑa` | ✅ No | 13.000 años | 🟡 Media |
| 4 | Letras + números | `Contraseña12345` | ⚠️ 1 vez | 352 cuatrillones | 🟡 Media-Alta |
| 5 | Símbolos (corta) | `Cl@v3!` | ✅ No | 21 segundos | 🔴 Muy débil |
| 6 | +10 chars con todo | `M1Cl@v3Segur@2025!` | ✅ No | 146 quintillones | 🟢 Muy fuerte |

*Aunque el tiempo teórico sea alto, si la contraseña ya está filtrada, el hackeo es instantáneo.

---

## 5. Análisis y Conclusiones

### 5.1 Factores que Afectan la Seguridad

| Factor | Impacto | Observación |
|--------|---------|-------------|
| **Longitud** | CRÍTICO | Una contraseña corta con símbolos (Cl@v3!) se hackea en 21 segundos |
| **Variedad de caracteres** | ALTO | Combinar mayúsculas, minúsculas, números y símbolos aumenta exponencialmente la seguridad |
| **No estar filtrada** | CRÍTICO | Si aparece en bases de datos, el tiempo de hackeo es instantáneo |
| **Evitar patrones comunes** | ALTO | "12345", "contraseña", "password" son las primeras en probarse |

### 5.2 Hallazgo Importante

> **La longitud es más importante que la complejidad.**
>
> Una contraseña larga solo con letras (`CoNtrAseÑa` = 13.000 años) es más segura que una corta con todo tipo de caracteres (`Cl@v3!` = 21 segundos).

### 5.3 Recomendación de Política de Contraseñas

Para el sistema de autenticación de la empresa, se recomienda implementar:

| Requisito | Valor Mínimo |
|-----------|--------------|
| Longitud mínima | 12 caracteres |
| Mayúsculas | Al menos 1 |
| Minúsculas | Al menos 1 |
| Números | Al menos 1 |
| Símbolos especiales | Al menos 1 |
| No estar en lista de contraseñas comunes | Obligatorio |
| Verificación contra bases de datos filtradas | Recomendado |

---

## 6. Recomendaciones para el Despliegue

1. **Implementar validación en tiempo real** que indique la fortaleza de la contraseña mientras el usuario la escribe.

2. **Rechazar contraseñas que aparezcan en bases de datos de filtraciones** conocidas (se pueden usar APIs como HaveIBeenPwned).

3. **No permitir contraseñas con patrones secuenciales** como "123456" o "abcdef".

4. **Forzar cambio de contraseña** si se detecta una filtración de datos.

5. **Implementar autenticación de dos factores (2FA)** como capa adicional de seguridad.

---

## 7. Conclusión Final

Las pruebas de seguridad demuestran que el sistema de autenticación debe exigir contraseñas de **mínimo 12 caracteres** que combinen **mayúsculas, minúsculas, números y símbolos**.

La prueba más reveladora fue la #5, donde una contraseña con todos los tipos de caracteres (`Cl@v3!`) se puede hackear en solo 21 segundos por ser demasiado corta.

**El sistema está listo para despliegue** siempre que se implementen las políticas de validación de contraseñas recomendadas en este informe.

---

*Documento generado como parte de las pruebas de la Unidad 8: Realización de Pruebas - Desarrollo de Interfaces*
