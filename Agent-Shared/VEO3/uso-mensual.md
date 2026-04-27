---
created: 2026-04-27
owner: Clowy
status: active
---

# VEO 3 — Tracker de Créditos Mensuales

> Créditos se renuevan a fin de mes. No dejar vencer.

---

## Cuentas disponibles

| Cuenta | Email | Créditos/mes | Créditos usados | Disponibles | Renovación |
|--------|-------|-------------|-----------------|-------------|-----------|
| #1 | (verificar) | 1,000 | 0 | 1,000 | Fin de mes |
| #2 | (verificar) | 1,000 | 0 | 1,000 | Fin de mes |
| #3 | (verificar) | 1,000 | 0 | 1,000 | Fin de mes |
| **Total** | | **3,000** | **0** | **3,000** | |

**Importante:** Verificar en aistudio.google.com que cada cuenta muestra VEO 3 disponible y el contador de créditos.

---

## Estrategia de uso

**Prioridad 1 — Fiverr UGC portfolio (esta semana):**
- 3 videos de muestra, estilos diferentes
- ~10-15 créditos estimados
- Usar cuenta #1

**Prioridad 2 — Orders de Fiverr (semana 2+):**
- 5-10 videos por order (basic: 1 video + alternativas; standard: 3; premium: 5)
- Rotación entre cuentas para no agotar una sola

**Regla de rotación:**
- Usar cuenta #1 hasta 700 créditos usados → pasar a cuenta #2
- Usar cuenta #2 hasta 700 → pasar a cuenta #3
- Nunca agotar una sola cuenta antes de que se renueven las otras

---

## Log de uso

| Fecha | Cuenta | Videos generados | Créditos usados | Proyecto | Notas |
|-------|--------|-----------------|-----------------|---------|-------|
| - | - | - | - | - | - |

---

## Workflow para generación

1. **Clowy** prepara prompts en `01-PROYECTOS/FIVERR/clientes/[id]/prompts.md`
2. **Clowy** hace heartbeat: "Prompts listos, esperando generación de Tien"
3. **Tien** entra a aistudio.google.com con la cuenta designada
4. **Tien** genera cada video (Copy/paste de prompt → Generate → Download)
5. **Tien** pone videos en carpeta compartida / vault (si es pequeño) o pasa link
6. **Clowy** continúa con edición y entrega

**Tiempo estimado para Tien:** ~15 min por batch de 10 videos

---

## Alerta de créditos

Si alguna cuenta llega a menos de 200 créditos disponibles → Clowy notifica a Hermes via heartbeat con flag "Human input needed: Yes".

---

*Actualizar tabla de Log después de cada sesión de generación.*
